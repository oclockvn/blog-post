# Sử dụng automapper trong asp.net mvc

### Không còn "copy" nữa...

Chắc hẳn bạn vẫn còn nhớ (hoặc đã từng - hoặc đang) sử dụng đoạn code dưới đây

<script src="https://gist.github.com/oclockvn/a5e01ba543692a4ffd098bceed0b0bc1.js"></script>

hoặc đại loại 1 đoạn code copy giá trị tương tự:

<script src="https://gist.github.com/oclockvn/08320bb625bbdd6682cdcd42e1dd91e8.js"></script>

Sở dĩ phải copy giá trị của các object bởi đơn giản object là kiểu tham chiếu (reference type) nếu bạn không muốn xảy ra chuyện *ơ hay, Id của tao sao mày dám đổi :))*

2 cách trên không có gì sai hay chuối cả, và hiện tại vẫn có rất nhiều người - người mà chưa biết đến automapper - vẫn đang sử dụng. Mình tạm gọi việc copy dữ liệu giữa 2 object là mapping.

Mapping: gán giá trị từ thuộc tính A trong đối tượng a cho thuộc tính tương ứng B trong đối tượng b: 

    b.B = a.A

### ...bởi vì đã có automapper

Automapper là 1 thư viện mapping object-object. Nó cho phép copy giá trị từ 2 object có các  property (thuộc tính) giống tên nhau - không phân biệt hoa thường. Hơn thế nữa, nó còn có thể map các property giống tên nhưng khác kiểu dữ liệu(*) và cho phép bạn custom việc chuyển đổi giữa các property theo ý mình.

Automapper cho phép download miễn phí thông qua nuget, bạn có thể sử dụng lệnh sau trong Package Manager Console để cài đặt version mới nhất

    Install-Package AutoMapper

### sử dụng automapper

Giả sử bạn có 2 class như sau

<script src="https://gist.github.com/oclockvn/8bfafdb6a3e72d0577d03884780c37f9.js"></script>

Bạn có thể map Foo instance sang Bar instance bằng 2 bước đơn giản:

![automapper simple](https://goo.gl/qhOnuI)

1: setup để khai báo rằng object Bar sẽ được map từ object Foo (dòng 31)  
2: map từ Foo sang Bar (dòng 36)

Với cách setup như trên, bạn đang dùng instance api để khởi tạo đối tượng Mapper. Với các version cũ hơn của automapper, bạn có thể sử dụng static api như sau:

![automapper static api](https://goo.gl/lgGhPg)

Việc đăng ký mapper chỉ xảy ra 1 lần trên 1 AppDomain, điều này dễ dàng thực hiện bằng cách đăng ký trong `Application_Start`

![automapper boostrapper Application_Start](https://goo.gl/8tkK8F)

Đăng ký sử dụng static api cũng làm tương tự, nhưng bạn không cần phải giữ lại instance của mapper để sử dụng lại. Cách đăng ký sử dụng static api có vẻ tiện hơn, nhưng đã bị deprecated ở các version 5.x của automapper (mình cũng thích dùng static api hơn).

### Convert 2 property khác nhau

Giả sử trường hợp như sau:

<script src="https://gist.github.com/oclockvn/068d5db391b43a1c5606522c5f608eb3.js"></script>

Lợi hại chưa, automapper có thể map 2 property khác kiểu dữ liệu nếu trùng tên. Tuy nhiên, nếu convert fail thì exception sẽ văng ra

    var foo = new Foo { Id = "5s" };
    var bar = Mapper.Map<Foo, Bar>(foo); // exception

![automapper convert fail](https://goo.gl/giKJdy)

### Custom automapper convert

Có 2 cách để custom converter theo ý của mình: trong config và implement `ITypeConverter`

#### 1. Custom converter trong config

Bạn có thể custom convert trong config ở 2 vị trí khác nhau: khi đăng ký map và trong quá trình map.

#### 1.1. Đăng ký map

Với 2 class như sau

![automapper classes](https://goo.gl/3xA1c6)

Bạn có thể custom cho `Fullname` của `Bar` map với `Name` của `Foo` bằng cách sử dụng extension `ForMember` trong config:

![custom map register](https://goo.gl/Z5H5ey)

ForMember nhận vào 2 tham số

<script src="https://gist.github.com/oclockvn/38a315b2079eea8decd3f92477213931.js"></script>

Tham số đầu tiên dùng để chỉ định target property, tham số thứ 2 là 1 Action option dùng để chỉ định source property

#### 1.2. Trong quá trình map

Bạn cũng có thể custom trong quá trình mapping như sau

![automapper custom map](https://goo.gl/79F06I)

Và kết quả:

![automapper custom result](https://goo.gl/kCgOYN)

Trên đây là cách custom cho những object có nhiều property giống nhau, chỉ chỉnh sửa 1 vài logic nhỏ trước/sau khi mapping. Đối với 2 object hoàn toàn khác nhau, cách đơn giản nhất là viết 1 customer converter.

#### 2. Custom map bằng cách implement `ITypeConverter`

Bằng cách kế thừa interface ITypeConverter, bạn có quyền hoàn toàn muốn làm gì thì làm :))

<script src="https://gist.github.com/oclockvn/8ed6dfc0ff7ea602957bbac476e324b0.js"></script>

và đăng ký nó trong config bằng cách:

<script src="https://gist.github.com/oclockvn/882a8a0d33742c531c8aaa0740761fa3.js"></script>

Chú ý:

Trong các phiên bản 4.x trở xuống, implement ITypeConverter có đôi chút khác về tham số trong phương thức Convert

<script src="https://gist.github.com/oclockvn/a3d63a10eff6d4e741d00611bc03a71d.js"></script>

### Automapper in action

Trong các project của mình, mình thích sử dụng cách viết class kế thừa hơn là config (cũng tùy trường hợp nên dùng cái nào)

#### Step 1: đăng ký 1 lần trong `global.asax`

![Application_Start](https://goo.gl/0dYdL7)

#### Step 2: đăng ký mapping và conveter (1 lần trong đời và sử dụng mãi mãi ^^)

![mapping register](https://goo.gl/MLRFLt)

#### Step 3: Map

![map](https://goo.gl/Jzjn5W)

### kết

Trong ứng dụng, việc chuyển đổi giá trị từ object này sang object kia rất hay gặp, và thanks god, automapper đã làm chuyện đó trở nên đơn giản và thuận tiện hơn :)

Hy vọng qua bài viết, các bạn có thể áp dụng tốt automapper vào các project của mình.