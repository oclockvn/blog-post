Bạn biết jquery, nhưng code jquery của bạn liệu có "đẹp"? Uh ah, những chiêu thu nhặt sau của mình có-thể-bạn-chưa-để-ý sẽ giúp ích cho bạn hơn nhiều đấy.

Bạn muốn kiểm chứng? Đọc để biết và gg hoặc do it yourself để nhớ lâu hơn nhé :))

Lưu ý: đây là những best practice "của mình", được đúc kết trong quá trình làm việc và kinh nghiệm. Bạn biết trường hợp này có cách giải quyết tốt hơn, hoặc bạn biết vẫn còn nhiều best practice khác, tại sao lại không chia sẻ nhỉ ^^

### 1. Naming convention

Cái này là optional thôi, nhưng theo quan điểm của mình thì bạn sẽ dễ dàng nhận biết 1 jquery object và 1 javascript object hơn nếu như đặt tên theo cách dưới đây:

    var $jqueryObject = $('.some-class'); // jquery name with `$` before name
    var javascriptObject = {}; // javascript name with camel case convention


### 2. Caching

Trong các vòng lặp, cache array length sẽ có tốc nhanh hơn:

bad:

    for (var i = 0; i < arr.length; i++) { // access arr every loop
        // do something
    }

good:

    var len = arr.length; // access 1 time

    for (var i = 0; i < len; i++) {
        // do something
    }

Tương tự đối với jquery, thay vì khởi tạo đối tượng trong mỗi lần gọi, hãy khai báo 1 đối tượng để lưu giữ thể hiện:

bad:

    for (var i = 0; i < 1000; i++) {
        $('.some-class').addClass('active');
    }


good:

    var $item = $('.some-class');

    for (var i = 0; i < 1000; i++) {
        $item.addClass('active');
    }

### 3. Append

Trong các trường hợp append dữ liệu, sử dụng chuỗi sẽ giúp tăng performance:

bad:

    for (var i = 0; i < 1000; i++) {
        var $a = $('<a href="#">click me</a>');
        $('.div').append($a);
    }

good:

    var html = '';

    for (var i = 0; i < 1000; i++) {
        html += '<a href="#">click me</a>';    
    }

    $('.div').append(html);

### 4. Check for reference

`ReferenceError` là lỗi nảy sinh khi 1 đối tượng không tồn tại gọi thực hiện các phương thức. Do đó hãy nhớ kiểm tra trước khi thực hiện 1 hành động nào đó (nếu bạn không chắc chắn nó sẽ tồn tại). jquery selector sẽ trả về 1 empty array nếu selector không tìm thấy, do đó việc kiểm tra selector có kết quả hay không vô cùng đơn giản:

    var $someNonExistElements = $('.bla-bla-bla');

    if ($someNonExistElements.length == 0)
        return;

    $someNonExistElements.show(); // <-- here you good to go

### 5. Using `closest()`

Hãy so sánh 2 cách viết sau:

    var $grandGrandGrandGrandParent1 = $('.child').parent().parent().parent().parent();

    var $grandGrandGrandGrandParent2 = $('.child').closest('.grand-parent');

Rõ ràng cách 2 dễ đọc và dễ nhận biết hơn rất nhiều đúng không? Hàm ```closest()``` có tác dụng tìm thẻ cha gần nhất thỏa selector.

### 6. Using `on()`

So sánh 2 cách viết sau:

attach click event:

    $('.button').click(function(){}); // $('.button').click(someFunc);

delegate click event:

    $(document).on('click', '.button', function(){}); // $(document).on('click', '.button', someFunc);

Bạn có biết sự khác biệt giữa 2 cách viết này không? Nên sử dụng cách nào?

- Cách 1: gắn sự kiện ```someFunc``` vào thẻ ```.button``` **hiện-đang-có** trong DOM. Cách viết này sẽ vô tác dụng nếu như bạn append 1 ```.button``` mới vào DOM, và bạn phải cẩn thận nếu không muốn bị [memory leak](http://lmgtfy.com?q=memory+leak+javascript+pattern) khi remove element ```.button``` ra khỏi DOM. Đồng thời bạn phải khai báo sự kiện này trong ```$(document).ready()``` (hoặc cuối trang) để đảm bảo sự kiện được gọi 1 cách chính xác.
- Cách 2: bất kỳ element ```.button``` nào cũng có thể gọi sự kiện ```someFunc``` cho dù xuất hiện ở bất kỳ thời điểm nào. Bạn không cần khai báo trong ```$(document).ready()```, và với cách viết này bạn có thể tái sử dụng hàm bằng cách truyền tham số vào hàm

    $(document).on('click', '.button', function(e) {
        var receivedData = e.data.sendData; // ==> 1
    }, {sendData: 1}); // $(document).on('click', '.button', someFunc);

Optional: nên sử dụng function declare thay vì viết anonymous function, như vậy code sẽ dễ đọc và tái sử dụng hơn:

Anonymous:

    $(document).on('click', '.button', function(){});

Declare:

    function someFunc() {};

    $(document).on('click', '.button', someFunc);

### 7. Sử dụng chaining methods

jquery cho phép bạn gọi các method 1 cách nối tiếp liên tục (chaining), thay vì:

    var $someClass = $('.some-class');

    $someClass.addClass('.active');
    $someClass.fadeIn();
    $someClass.slideDown();
    $someClass.css({'background', '#f42'});

bạn có thể viết ngắn gọn như sau:

    $('.some-class').addClass('.active').fadeIn().slideDown();
    // or
    $('.some-class')
                .addClass('.active')
                .fadeIn()
                .slideDown(); 

### 8. Tối ưu selector

selector càng ngắn, tốc độ select càng nhanh. Ví dụ thay vì selector dưới đây:

    var $spanInTable = $('.table-container .table td span');

bạn có thể viết gọn lại:

    var $spanInTable = $('.table-container span');

Chú ý là viết gọn nếu có thể thôi nhé :))

Hoặc thay vì:

    // using document.querySelectorAll()
    var $element = $('#anId .then-a-class.active');

Nên viết là:

    // using document.getElementById()
    var $element = $('#anId').find('.then-a-class').filter('.active');

Sở dĩ cách sau (`$('#anId').find..`) có tốc độ nhanh hơn là vì phạm vi tìm kiếm được thu hẹp lại (tìm trong 1 region nhỏ hơn) - xem (9). Tuy nhiên cách viết có phần rắc rối hơn và không đáng bận tâm mấy cho những website nhỏ. Do đó bạn cứ chọn cách nào mình thấy thích là được.

### 9. Dùng `find()` và `filter()` thay cho selector

Thay vì:

    var $activeElement = $('.ul li.active');

bạn có thể viết:

    var $activeElement = $('.ul').find('li').filter('.acive');

Ừm, có vẻ hơi dài hơn nhỉ! Tuy dài hơn nhưng [tốc độ](http://learn.jquery.com/performance/optimize-selectors/) nó nhanh hơn đấy :)

### 10. Ajax

jquery đã bổ xung thư viện hỗ trợ ajax cho phép sử dụng ajax rất dễ dàng. Nhưng bạn có biết là có nhiều cách gọi ajax? Ví dụ muốn get dữ liệu:

C1: 

    $.getJSON('/controller/action?type=json', function(resp) { } );

C2:

    $.get('/controller/action', function(resp) { } );

C3:

    var $req = $.ajax({
        url: '/controller/action',
        data: {type: 'json'},
        success: function(resp) { }
    });

Vậy liệu bạn có biết rằng C1 và C2 cuối cùng vẫn phải gọi C3:

Đây:

![ajax get](https://goo.gl/lzClFo)

và đây:

![ajax get json](https://goo.gl/FtaMKU)

Tuy có viết dài hơn 1 chút, nhưng cách 3 cho phép bạn "setting" nhiều hơn. Có thể xem C1 và C2 là "2 helper" khi sử dụng ajax, nhưng mình vẫn prefer C3 hơn ^^! (không thông qua trung gian đỡ tốn tiền hơn :v).

### Và cuối cùng, sử dụng các thư viện (plugin) có sẵn khi có thể

Vâng, đây là trường hợp mà cái mình tự làm ra chưa chắc (chưa chắc thôi nhé) đã "ngon" bằng cái có sẵn. jquery là thư viện javascript rất phổ biến, và đã có rất nhiều developer, cộng đồng phát triển các thư viện có sẵn để thực hiện các thao tác thường sử dụng. Sử dụng các plugin cũng giúp bạn rút ngắn thời gian làm việc, và tăng "chất" cho sản phẩm của mình.

Dưới đây là các plugins mình hay dùng:

1. [sticky object](https://github.com/garand/sticky): fix 1 selector cố định thỏa điều kiện. 
2. [scroll spy](https://github.com/softwarespot/jquery-scrollspy): gọi sự kiện khi scroll tới vị trí nào đó.
3. [bootbox](http://bootboxjs.com/#): bootstrap popup alert
4. [toastr](http://codeseven.github.io/toastr/): đơn giản, dễ sử dụng.
5. [alertify](http://alertifyjs.com/): đơn giản, dễ sử dụng + đẹp.
6. [dropzone](http://www.dropzonejs.com/): upload file drag + drop
7. [mask input](https://igorescobar.github.io/jQuery-Mask-Plugin/): tạo mẫu nhập liệu cho input
8. [mixitup](https://mixitup.kunkalabs.com/): filter, order với animation
9. [typewatch](https://github.com/dennyferra/TypeWatch): delay 1 quãng thời gian sau khi người dùng không nhập để gọi callback.
10. [datatables](https://datatables.net/): plugins mạnh mẽ cho table dùng để sort, filter, paging...

...và còn rất nhiều cái mà bạn có thể tự gg khi cần nhé. Lưu ý là nên chọn plugin nào có repo được đông đảo người dùng, nhiều star và có tài liệu rõ ràng cụ thể nhé.

