Entity Framework (EF) là 1 O/RM khá phổ biến khi nhắc tới các ORM sử dụng khi làm việc với C#. EF rất dễ sử dụng và hiệu quả, tuy nhiên biết sử dụng là 1 chuyện, sử dụng hiệu quả lại là chuyện khác. Trải qua 1 quãng thời gian sử dụng EF, mình đã "tích góp" được một số thủ thuật, hy vọng nó giúp ích cho mọi người nếu thường xuyên làm việc với EF.

### 01. Log query

Bạn có thể dễ dàng xem câu lệnh sql được sinh ra bằng 1 Action của database context

<script src="https://gist.github.com/oclockvn/731361f0005b955abe901e136653fa95.js"></script>

Log là 1 Action của database context, truyền vào 1 chuỗi (chuỗi này là câu query được sinh ra), và bạn có thể làm bất kỳ điều gì nếu muốn. Ở trên mình sử dụng Debug Output để in ra log.

<img alt="log action" data-src="https://goo.gl/Y7qAX5" src="data:image/gif;base64,R0lGODdhAQABAPAAAMPDwwAAACwAAAAAAQABAAACAkQBADs=">

Với log, bạn sẽ biết được nhiều thông số trong câu query, từ đó rút ra cách tối ưu cho câu query của mình. Ví dụ như đoạn code dưới đây:

<img alt="log select query" data-src="https://goo.gl/kbAeZv" src="data:image/gif;base64,R0lGODdhAQABAPAAAMPDwwAAACwAAAAAAQABAAACAkQBADs=">

Sẽ có log được sinh ra:

<img alt="log result" data-src="https://goo.gl/o4s4Vq" src="data:image/gif;base64,R0lGODdhAQABAPAAAMPDwwAAACwAAAAAAQABAAACAkQBADs=">

Bạn thấy đấy, log ghi ra thời gian mở connection (10/10/2016 10:01:58), câu lệnh select, thời gian thực thi, trong bao lâu (194ms)...

### IQueryable<> vs IEnumerable<>

Mình thấy là có rất nhiều người không chú ý tới sự khác biệt giữa 2 kiểu này. Hãy xem xét sự khác biệt sau để tận dụng chính xác sức mạnh của từng cái nhé.

#### 01. IQueryable<>

Sử dụng IQueryable để lấy ra danh sách Post active và Id < 10

<img alt="IQueryable action post" data-src="https://goo.gl/oKQIvk" src="data:image/gif;base64,R0lGODdhAQABAPAAAMPDwwAAACwAAAAAAQABAAACAkQBADs=">

Log được sinh ra:

<script src="https://gist.github.com/oclockvn/ee411f9881d546cca3122d8b32fd070b.js"></script>

Như kết quả, có "total 3 posts" được lấy lên với điều kiện WHERE

    WHERE ([Extent1].[IsActive] = 1) AND ([Extent1].[PostId] < 10)

Và cho dù bạn có `WHERE` thêm bao nhiêu lần đi chăng nữa (trước khi `ToList()` để thực thi câu lệnh), thì mọi `WHERE` đó đều được `AND` trong câu lệnh select, và đến khi `ToList()`, mọi query bạn thực hiện trên code đều được "build" thành 1 câu lệnh sql duy nhất và thực thi dưới database, sau đó mới trả về kết quả.

Có rất nhiều cái "lợi" và "hại" của việc sử dụng IQueryable, mình xin trích ra 2 cái dễ thấy nhất:

- **Lợi:** Kết quả trả về là kết quả "nhỏ gọn" nhất vì mọi điều kiện WHERE đều được thực thi dưới database. Bạn có thể lấy được ưu điểm của IQueryable nếu như bạn select...1000.0000 dòng mà kết quả chỉ có...10 dòng !!!
- **Hại:** Rõ ràng là mọi việc đều được thực hiện dưới db cho nên bạn sẽ không áp dụng được những phương thức where ... chỉ có thể viết bằng C# (nói vấn đề này sau).

#### 02. `IEnumerable<>`

Áp dụng câu lệnh tương tự nhưng đối với `IEnumerable<>`

<img alt="IEnumerable select" data-src="https://goo.gl/7xwsgq" src="data:image/gif;base64,R0lGODdhAQABAPAAAMPDwwAAACwAAAAAAQABAAACAkQBADs=">

Xem log:

<script src="https://gist.github.com/oclockvn/20f7e8343081f0b0696b227941cc4442.js"></script>

Kết quả vẫn là 3 posts, tuy nhiên có chút khác biệt về where

    WHERE [Extent1].[IsActive] = 1

Yeah, sau lần where đầu tiên, EF sẽ móc "toàn bộ" kết quả trả về từ db lên server (giả sử có 1000.000 records - OMG), lên server xong rồi muốn where gì thì where, db không quan tâm nữa. Kể từ đây where là where ở memory.

Bạn có thể thấy sử dụng `IQueryable` thực thi trong 55ms > 22ms của `IEnumerable`, nhưng đây là đối với dữ liệu có số lượng nhỏ. Dĩ nhiên càng nhiều điều kiện where, thời gian thực thi càng lớn, nhưng memory sẽ hạn chế được việc lưu trữ và xử lý dữ liệu. 

Từ đây dễ thấy cái lợi của IQueryable là cái hại của IEnumerable, và ngược lại. Do đó để ứng dụng của mình có performance tốt nhất, bạn nên áp dụng hợp lý cách xử lý nhé.

Thế nào là áp dụng hợp lý? Tự làm để hiểu rõ hơn nhé :v

### Tracking Entity và AsNoTracking()

**Bạn có biết:** EF sẽ theo dõi (tracking) các entity set mỗi lần bạn select từ db. EF tracking bằng 1 `ObservableCollection<>` gọi là `Local`. Việc tracking sẽ giúp EF dễ dàng phát hiện sự thay đổi (`PropertyChanged`) và lưu trữ mỗi khi bạn `SaveChanges()`. Tuy nhiên, giả sử bạn chỉ muốn "read-only" bằng việc hiển thị lên table, tracking sẽ tốn thêm memory để lưu trữ (1 entity -> 1 local entity), và tất nhiên, cái nào tốn không cần thiết thì bạn chẳng dại gì mà giữ nó làm gì.

<img alt="tracking" data-src="https://goo.gl/hehhfE" src="data:image/gif;base64,R0lGODdhAQABAPAAAMPDwwAAACwAAAAAAQABAAACAkQBADs=">

log:

    before track: local = 0
    after track: local = 3

**Giải pháp đưa ra:** sử dụng extention method `AsNoTracking()`, và tác dụng của nó? Dĩ nhiên là để EF không tracking nữa rồi :)). `AsNoTracking()` còn giúp bạn làm việc với nhiều instance của `DbContext` cùng lúc đấy (VD sau).

<img alt="as no tracking" data-src="https://goo.gl/Ip29b2" src="data:image/gif;base64,R0lGODdhAQABAPAAAMPDwwAAACwAAAAAAQABAAACAkQBADs=">

**P/S:** sẽ có vấn đề xảy ra khi bạn `no tracking` mà Update entity. Bạn muốn biết nó là gì thì làm thử đi nhé :)))

### Hạn chế "round-trip" khi có thể

Bạn muốn delete 1 entity, và đây là cách mà bạn vẫn hay làm? (ví dụ thôi nhé :])

<img alt="delete entity" data-src="https://goo.gl/4B3Spz" src="data:image/gif;base64,R0lGODdhAQABAPAAAMPDwwAAACwAAAAAAQABAAACAkQBADs=">

Tìm đối tượng, nếu có thì xóa. Yes, không có gì là sai cả, mọi thứ hoạt động tốt. Tuy nhiên nếu bạn view log:

<script src="https://gist.github.com/oclockvn/b4da1bd305e957a72108f2ddd15c12ae.js"></script>

Lần đầu tiên bạn select entity lên, sau đó delete nó với tổng cộng 31ms + 56ms = ??? Và đây chỉ mới là delete 1 entity thôi đấy, nếu delete 100 entities thì sao?

Bằng cách sử dụng direct sql, bạn sẽ "đỡ vất vả" hơn nhiều:

<img alt="execute sql command" data-src="https://goo.gl/samche" src="data:image/gif;base64,R0lGODdhAQABAPAAAMPDwwAAACwAAAAAAQABAAACAkQBADs=">

Log cái nè:

<script src="https://gist.github.com/oclockvn/200c753fe02f672a4336e0c1b91d9a5b.js"></script>

18ms với result = 1 (success), và được thực hiện bằng transaction đấy nhé :))

Với việc sử dụng direct sql, bạn phải trực tiếp viết câu lệnh sql vào code, và nhớ sử dụng parameter để chống sql injection nhé. Tuy nhiên bỏ ra 1 chút sức để đạt được kết quả tốt thì không tệ chút nào phải không ^^!

Thực ra không cần phải dùng direct sql mới nhanh, vẫn có nhiều cách query tiết kiệm được bộ nhớ như sử dụng `IQueryable` ở trên.

### Store procedure

Đối với EF database first, bạn dễ dàng thực thi store procedure bằng cách import và sử dụng như 1 function bình thường

Import:

<img alt="import store proc" data-src="https://goo.gl/SDL2EZ" src="data:image/gif;base64,R0lGODdhAQABAPAAAMPDwwAAACwAAAAAAQABAAACAkQBADs=">

Usage:

<img alt="using store proc" data-src="https://goo.gl/aa5G4y" src="data:image/gif;base64,R0lGODdhAQABAPAAAMPDwwAAACwAAAAAAQABAAACAkQBADs=">

Đối với EF code first, bạn không có data model nhưng vẫn có thể dễ dàng sử dụng store bằng direct sql:

<img alt="sql query" data-src="https://goo.gl/NvbM66" src="data:image/gif;base64,R0lGODdhAQABAPAAAMPDwwAAACwAAAAAAQABAAACAkQBADs=">

Vậy là bạn có 2 cách để thực thi direct sql, ```ExecuteSqlCommand``` và ```SqlQuery```. Sự khác nhau giữa 2 cách là gì? [Đọc](http://stackoverflow.com/questions/24248307/what-is-the-difference-between-executesqlcommand-vs-sqlquery-when-doing-a-db-a) + làm để hiểu rõ hơn nhé :v (PM mình nếu có thắc mắc).

### Join

Join là lệnh được thực hiện khá nhiều khi thao tác với db. Bạn vẫn có thể dễ dàng thực hiện lệnh join với EF, tuy nhiên bạn có biết?

Khi sử dụng linq, bạn đang thực thi inner join

<img alt="linq join" data-src="https://goo.gl/IOrfMJ" src="data:image/gif;base64,R0lGODdhAQABAPAAAMPDwwAAACwAAAAAAQABAAACAkQBADs=">

Log:

<img alt="inner join log" data-src="https://goo.gl/KS3LMZ" src="data:image/gif;base64,R0lGODdhAQABAPAAAMPDwwAAACwAAAAAAQABAAACAkQBADs=">

Để sử dụng left join, bạn sử dụng: ```DefaultIfEmpty()```

<img alt="left join" data-src="https://goo.gl/cAAiVi" src="data:image/gif;base64,R0lGODdhAQABAPAAAMPDwwAAACwAAAAAAQABAAACAkQBADs=">

Log:

<img alt="left join result" data-src="https://goo.gl/90UMGI" src="data:image/gif;base64,R0lGODdhAQABAPAAAMPDwwAAACwAAAAAAQABAAACAkQBADs=">

Và, để sử dụng join với multiple on condition, bạn có thể tận dụng anonymous type của C#:

<img alt="multiple on" data-src="https://goo.gl/f6GMBo" src="data:image/gif;base64,R0lGODdhAQABAPAAAMPDwwAAACwAAAAAAQABAAACAkQBADs=">

### Và..

Trên đây chỉ là những cái hay gặp, còn rất nhiều nữa nên có lẽ mình sẽ viết trong part 2.

Bạn biết đấy, càng hiện đại thì càng hại điện, cho nên tiết kiệm điện tới cỡ nào là do bạn mà thôi :))

Nếu bạn có thủ thuật gì hay, đừng ngại chia sẻ nhé ^^!