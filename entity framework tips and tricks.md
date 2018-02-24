Entity Framework (EF) là 1 O/RM khá phổ biến khi nhắc tới các ORM sử dụng khi làm việc với C#. EF rất dễ sử dụng và hiệu quả, tuy nhiên biết sử dụng là 1 chuyện, sử dụng hiệu quả lại là chuyện khác. Trải qua 1 quãng thời gian sử dụng EF, mình đã "tích góp" được một số thủ thuật, hy vọng nó giúp ích cho mọi người nếu thường xuyên làm việc với EF.

### 01. Log query

Bạn có thể dễ dàng xem câu lệnh sql được sinh ra bằng 1 Action của database context

    using (var db = new DbEntities())
    {
        db.Database.Log = msg => Debug.WriteLine(msg);
    }

Log là 1 Action của database context, truyền vào 1 chuỗi (chuỗi này là câu query được sinh ra), và bạn có thể làm bất kỳ điều gì nếu muốn. Ở trên mình sử dụng Debug Output để in ra log.

![log action](https://goo.gl/Y7qAX5)

Với log, bạn sẽ biết được nhiều thông số trong câu query, từ đó rút ra cách tối ưu cho câu query của mình. Ví dụ như đoạn code dưới đây:

![log select query](https://goo.gl/kbAeZv)

Sẽ có log được sinh ra:

![log result](https://goo.gl/o4s4Vq)

Bạn thấy đấy, log ghi ra thời gian mở connection (10/10/2016 10:01:58), câu lệnh select, thời gian thực thi, trong bao lâu (194ms)...

### IQueryable<> vs IEnumerable<>

Mình thấy là có rất nhiều người không chú ý tới sự khác biệt giữa 2 kiểu này. Hãy xem xét sự khác biệt sau để tận dụng chính xác sức mạnh của từng cái nhé.

#### 01. IQueryable<>

Sử dụng IQueryable để lấy ra danh sách Post active và Id < 10

![IQueryable action post](https://goo.gl/oKQIvk)

Log được sinh ra:

```
Opened connection at 10/22/2016 10:15:54 AM +07:00

SELECT 
    [Extent1].[PostId] AS [PostId], 
    [Extent1].[Title] AS [Title],    
    -- other columns    
    FROM [dbo].[Posts] AS [Extent1]
    WHERE ([Extent1].[IsActive] = 1) AND ([Extent1].[PostId] < 10)


-- Executing at 10/22/2016 10:15:55 AM +07:00

-- Completed in 55 ms with result: SqlDataReader



Closed connection at 10/22/2016 10:15:55 AM +07:00

total 3 posts
``` 

Như kết quả, có "total 3 posts" được lấy lên với điều kiện WHERE

```sql
WHERE ([Extent1].[IsActive] = 1) AND ([Extent1].[PostId] < 10)
```

Và cho dù bạn có `WHERE` thêm bao nhiêu lần đi chăng nữa (trước khi `ToList()` để thực thi câu lệnh), thì mọi `WHERE` đó đều được `AND` trong câu lệnh select, và đến khi `ToList()`, mọi query bạn thực hiện trên code đều được "build" thành 1 câu lệnh sql duy nhất và thực thi dưới database, sau đó mới trả về kết quả.

Có rất nhiều cái "lợi" và "hại" của việc sử dụng IQueryable, mình xin trích ra 2 cái dễ thấy nhất:

- **Lợi:** Kết quả trả về là kết quả "nhỏ gọn" nhất vì mọi điều kiện WHERE đều được thực thi dưới database. Bạn có thể lấy được ưu điểm của IQueryable nếu như bạn select...1000.0000 dòng mà kết quả chỉ có...10 dòng !!!
- **Hại:** Rõ ràng là mọi việc đều được thực hiện dưới db cho nên bạn sẽ không áp dụng được những phương thức where ... chỉ có thể viết bằng C# (nói vấn đề này sau).

#### 02. IEnumerable<>

Áp dụng câu lệnh tương tự nhưng đối với IEnumerable<>

![IEnumerable select](https://goo.gl/7xwsgq)

Xem log:

```
Opened connection at 10/22/2016 10:34:14 AM +07:00

SELECT 
    [Extent1].[PostId] AS [PostId], 
    [Extent1].[Title] AS [Title], 
    -- other columns
    WHERE [Extent1].[IsActive] = 1


-- Executing at 10/22/2016 10:34:15 AM +07:00

-- Completed in 22 ms with result: SqlDataReader



Closed connection at 10/22/2016 10:34:15 AM +07:00

total 3 posts
```

Kết quả vẫn là 3 posts, tuy nhiên có chút khác biệt về where

```sql
WHERE [Extent1].[IsActive] = 1
```

Yeah, sau lần where đầu tiên, EF sẽ móc "toàn bộ" kết quả trả về từ db lên server (giả sử có 1000.000 records - OMG), lên server xong rồi muốn where gì thì where, db không quan tâm nữa. Kể từ đây where là where ở memory.

Bạn có thể thấy sử dụng `IQueryable` thực thi trong 55ms > 22ms của `IEnumerable`, nhưng đây là đối với dữ liệu có số lượng nhỏ. Dĩ nhiên càng nhiều điều kiện where, thời gian thực thi càng lớn, nhưng memory sẽ hạn chế được việc lưu trữ và xử lý dữ liệu. 

Từ đây dễ thấy cái lợi của IQueryable là cái hại của IEnumerable, và ngược lại. Do đó để ứng dụng của mình có performance tốt nhất, bạn nên áp dụng hợp lý cách xử lý nhé.

Thế nào là áp dụng hợp lý? Tự làm để hiểu rõ hơn nhé :v

### Tracking Entity và AsNoTracking()

**Bạn có biết:** EF sẽ theo dõi (tracking) các entity set mỗi lần bạn select từ db. EF tracking bằng 1 `ObservableCollection<>` gọi là `Local`. Việc tracking sẽ giúp EF dễ dàng phát hiện sự thay đổi (`PropertyChanged`) và lưu trữ mỗi khi bạn `SaveChanges()`. Tuy nhiên, giả sử bạn chỉ muốn "read-only" bằng việc hiển thị lên table, tracking sẽ tốn thêm memory để lưu trữ (1 entity -> 1 local entity), và tất nhiên, cái nào tốn không cần thiết thì bạn chẳng dại gì mà giữ nó làm gì.

![tracking](https://goo.gl/hehhfE)

log:

```
before track: local = 0
after track: local = 3
``` 

**Giải pháp đưa ra:** sử dụng extention method `AsNoTracking()`, và tác dụng của nó? Dĩ nhiên là để EF không tracking nữa rồi :)). `AsNoTracking()` còn giúp bạn làm việc với nhiều instance của `DbContext` cùng lúc đấy (VD sau).

![as no tracking](https://goo.gl/Ip29b2)

**P/S:** sẽ có vấn đề xảy ra khi bạn `no tracking` mà Update entity. Bạn muốn biết nó là gì thì làm thử đi nhé :)))

### Hạn chế "round-trip" khi có thể

Bạn muốn delete 1 entity, và đây là cách mà bạn vẫn hay làm? (ví dụ thôi nhé :])

![delete entity](https://goo.gl/4B3Spz)

Tìm đối tượng, nếu có thì xóa. Yes, không có gì là sai cả, mọi thứ hoạt động tốt. Tuy nhiên nếu bạn view log:

```
Opened connection at 10/22/2016 11:15:03 AM +07:00

SELECT TOP (2) 
    [Extent1].[CommentId] AS [CommentId], 
    [Extent1].[CommentBy] AS [CommentBy], 
    -- other columns
    FROM [dbo].[Comments] AS [Extent1]
    WHERE [Extent1].[CommentId] = @p0


-- p0: '1' (Type = Int32)

-- Executing at 10/22/2016 11:15:03 AM +07:00

-- Completed in 31 ms with result: SqlDataReader



Closed connection at 10/22/2016 11:15:03 AM +07:00

Opened connection at 10/22/2016 11:15:03 AM +07:00

Started transaction at 10/22/2016 11:15:03 AM +07:00

DELETE [dbo].[Comments]
WHERE ([CommentId] = @0)


-- @0: '1' (Type = Int32)

-- Executing at 10/22/2016 11:15:03 AM +07:00

-- Completed in 56 ms with result: 1



Committed transaction at 10/22/2016 11:15:03 AM +07:00

Closed connection at 10/22/2016 11:15:03 AM +07:00
```

Lần đầu tiên bạn select entity lên, sau đó delete nó với tổng cộng 31ms + 56ms = ??? Và đây chỉ mới là delete 1 entity thôi đấy, nếu delete 100 entities thì sao?

Bằng cách sử dụng direct sql, bạn sẽ "đỡ vất vả" hơn nhiều:

![execute sql command](https://goo.gl/samche)

Log cái nè:

```
Opened connection at 10/22/2016 11:20:36 AM +07:00

Started transaction at 10/22/2016 11:20:36 AM +07:00

delete from Comments where CommentId=@id


-- @id: '2' (Type = Int32, IsNullable = false)

-- Executing at 10/22/2016 11:20:36 AM +07:00

-- Completed in 18 ms with result: 1



Committed transaction at 10/22/2016 11:20:36 AM +07:00

Closed connection at 10/22/2016 11:20:36 AM +07:00
```

18ms với result = 1 (success), và được thực hiện bằng transaction đấy nhé :))

Với việc sử dụng direct sql, bạn phải trực tiếp viết câu lệnh t-sql vào code, và nhớ sử dụng parameter để chống sql injection nhé. Tuy nhiên bỏ ra 1 chút sức để đạt được kết quả tốt thì không tệ chút nào phải không ^^!

Thực ra không cần phải dùng direct sql mới nhanh, vẫn có nhiều cách query tiết kiệm được bộ nhớ như sử dụng `IQueryable` ở trên.

### Store procedure

Đối với EF database first, bạn dễ dàng thực thi store procedure bằng cách import và sử dụng như 1 function bình thường

Import:

![import store proc](https://goo.gl/SDL2EZ)

Using:

![using store proc](https://goo.gl/aa5G4y)

Đối với EF code first, bạn không có data model nhưng vẫn có thể dễ dàng sử dụng store bằng direct sql:

![sql query](https://goo.gl/NvbM66)

Vậy là bạn có 2 cách để thực thi direct sql, ```ExecuteSqlCommand``` và ```SqlQuery```. Sự khác nhau giữa 2 cách là gì? [Đọc](http://stackoverflow.com/questions/24248307/what-is-the-difference-between-executesqlcommand-vs-sqlquery-when-doing-a-db-a) + làm để hiểu rõ hơn nhé :v (PM mình nếu có thắc mắc).

### Join

Join là lệnh được thực hiện khá nhiều khi thao tác với db. Bạn vẫn có thể dễ dàng thực hiện lệnh join với EF, tuy nhiên bạn có biết?

Khi sử dụng linq, bạn đang thực thi inner join

![linq join](https://goo.gl/IOrfMJ)

Log:

![inner join log](https://goo.gl/KS3LMZ)

Để sử dụng left join, bạn sử dụng: ```DefaultIfEmpty()```

![left join](https://goo.gl/cAAiVi)

Log:

![left join result](https://goo.gl/90UMGI)

Và, để sử dụng join với multiple on condition, bạn có thể tận dụng anonymous type của C#:

![multiple on](https://goo.gl/f6GMBo)

### Và..

Trên đây chỉ là những cái hay gặp, còn rất nhiều nữa nên có lẽ mình sẽ viết trong part 2.

Bạn biết đấy, càng hiện đại thì càng hại điện, cho nên tiết kiệm điện tới cỡ nào là do bạn mà thôi :))

Nếu bạn có thủ thuật gì hay, đừng ngại chia sẻ nhé ^^!

