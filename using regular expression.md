regular expression là 1 nghệ thuật, người sử dụng regular expression là 1 ...good coder

### Regular expression là gì?

regular expression là 1 khuôn mẫu các ký tự dùng để so khớp và xử lý chuỗi ký tự đầu vào. Bằng cách định nghĩa các pattern (mẫu), regular expression (regex) cho phép extract, replace, remove... chuỗi 1 cách hiệu quả nhất.

Nếu bạn thích thì dịch nó là "biểu thức chính quy" nhé :v, còn không cứ gọi là regex.

Ở mỗi ngôn ngữ khác nhau có 1 cách sử dụng khác nhau của regex (chủ yếu là cú pháp), điều đó không đáng bận tâm lắm. Bạn chỉ cần hiểu được ý nghĩa thì đâu cũng dùng được.

### Hãy bắt đầu từ những thứ đơn giản

regex có vẻ rất khó nhớ đối với nhiều người, nhưng nếu bạn hiểu nó thì bạn ..không nhớ nó cũng tự bay vào đầu, thiệt đấy :))

Khuôn mẫu của 1 regex đơn giản là thế này nhé:

```
(chọn 1 cái gì đó) + (số lượng bao nhiêu)
```

Đơn giản vl, ví dụ ngay nè:

#### Level 0: mọi ký tự đều là regex pattern

Ví dụ muốn tìm chữ ```hello world``` có nằm trong ```bla bla hello world bla bla``` hay không, mình có thể sử dụng regex sau:

    hello world


#### Level 1: Mình muốn search 3 con số nằm giữa chữ Hello và world như ví dụ dưới

    Hello 123 world

Vậy thì regex của mình sẽ là:

    \d{3}


Ý nghĩa: Tìm kiếm những con số **(digit: \d)** có số lượng là 3.

Vậy thì:

- Cái gì đó: là con số, có pattern là \d -> digit (rất gợi nhớ nhé)
- Số lượng: 3, đặt trong dấu {}

#### Level 2: Nâng pattern lên 1 chút

Ở level 1 mình đã biết cách chọn 1 con số, vậy 1 từ thì sao? cũng rất gợi nhớ nữa

    \w

Yes, nó là ```\w``` -> ```word``` đó.

Trường hợp trên là do mình đã biết có 3 con số, vậy nếu không biết chính xác số lượng thì sao?

    \d{1,}


**Ý nghĩa:** chọn những con số có số lượng ít nhất 1

Nếu bạn muốn chọn những con số có số lượng nằm trong 1 khoảng 1 tới 3

    \d{1,3}

Vậy nếu chọn 1 ký tự bất kỳ với 1 số lượng bất kỳ thì sao?

    .*

Vẫn cú pháp đơn giản ấy:

- `.` : chọn 1 ký tự bất kỳ.
- `*` : chọn số lượng bất kỳ. 

OK, vậy là bạn đã biết được cách chọn 1 nhóm các chữ số hoặc các ký tự với số lượng động. Bây giờ thử test xem nhé.

Hầu hết các text-editor hiện nay đều cung cấp regular expression search, cái mình vẫn hay dùng nhất là notepad++.

### Test regular expression với notepad++

#### VD1: tìm chuỗi

![notepad++ regex simple](https://goo.gl/xGNsSY)

Để sử dụng regular expression bạn nhớ chọn Search Mode là Regular expression nhé.

#### VD2: VD1 này có vẻ đơn giản, vậy thử cái "ít đơn giản" hơn xem sao: xóa content trong 2 thẻ meta dưới đây:

    <meta name="keywords" content="regex, c#" />
    <meta name="description" content="using regex" />

Cách đơn giản:

![regex replace](https://goo.gl/GdNirJ)

Ý nghĩa: thay thế chuỗi có mẫu ```content="ký-tự-bất-kỳ"``` thành chuỗi ```content=""```

#### Level 3: khớp trùng ở ký tự đầu tiên

Vấn đề ở VD2 sẽ xuất hiện nếu như mình đảo ngược vị trí của name và content

```
<meta name="..." content="..." />
---> 
<meta content="..." name="..."  /> 
```

Nếu vẫn giữ pattern cũ thì kết quả sẽ là:

![regex not first match](https://goo.gl/EMQKRi)

Ố ồ, nó không chịu dừng lại ở ký tự đầu tiên trùng khớp, cách xử lý sẽ là pattern sau:

![first match regex](https://goo.gl/m2bnGC)

Điểm đặc biệt ở đây là ký tự ```?``` trong pattern, ký tự này có nghĩa là tìm đến first-match (ký tự trùng đầu tiên) và dừng lại. Vì vậy muốn tìm ký tự ? trong 1 chuỗi thì bạn phải dùng ```\?``` (cũng như ký tự đặc biệt trong C# thôi).

Quay lại với chuỗi ở ví dụ trên, mình muốn đảo ngược 2 thuộc tính name và content với nhau, từ:

    <meta name="keywords" content="regex, c#" />
    <meta name="description" content="using regex" />

thành:

    <meta content="regex, c#" name="keywords" />
    <meta content="using regex" name="description" />

Với replace thường thì mission impossible cmnr :)), nhưng nó là chuyện nhỏ với regex thôi, bí quyết ở đây là sử dụng group.

#### Level 4: regex group

![regex group select](https://goo.gl/ySqvST)

Giải thích:

1. Search ```name=".*"``` và cho nó vào group 1 với cú pháp ```([search pattern])``` <- lưu ý dấu ```()``` sẽ mang pattern trong đó thành 1 group. Khi đó group này sẽ được chọn với cú pháp ```$[index]```.
2. Tương tự với group ```content=".*"```, bạn sẽ được ```$2```
3. Hoán đổi vị trí của $2 và $1 để đảo ngược vị trí

Kết quả:

![group replace](https://goo.gl/AyOc5f)

### Một số pattern nên nhớ

- ```^```: bắt đầu 1 chuỗi.
- ```$```: kết thúc 1 chuỗi.
- ```\s```: ký tự khoảng trắng (s = space)
- ```[AB]```: chọn A hoặc B (A or B). A and B thì đơn giản là ```AB``` <-- không có dấu ```[]```.

Tham khảo [Regular Expression Language - Quick Reference](https://msdn.microsoft.com/en-us/library/az24scfc(v=vs.110).aspx) để biết thêm các pattern nâng cao.

### Kết

Trên đây mình đã giới thiệu về regular expression và cách sử dụng của nó. Bạn cũng chỉ cần nhớ bao nhiêu đó thôi, khi nào đụng vấn đề gì có thể tra cứu thêm. Với những kỹ thuật trên, bạn có thể hoàn toàn search like-a-pro khi làm việc với các text-editor hoặc code-editor (IDE).

Ở bài viết sau mình sẽ giới thiệu cách sử dụng regular expression trong C#, đơn giản thôi (cứ tự nhủ như zậy đi ^^).