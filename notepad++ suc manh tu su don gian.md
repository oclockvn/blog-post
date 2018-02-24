
Đối với các developer, hiện nay có rất nhiều sự lựa chọn cho 1 text editor. (Theo những gì mình biết và đã sử dụng trên Windows) Từ Sublime text, Atom, Brackets...cho tới Visual Studio Code. Tất cả đều hỗ trợ khá tốt do nhiều tính năng hữu ích cùng với bộ plugins đồ sộ. Tuy nhiên, Notepad++ vẫn là sự lựa chọn hàng đầu của mình. Vì sao? Nội dung bài viết này sẽ lý giải điều đó.

<img src="data:image/gif;base64,R0lGODdhAQABAPAAAMPDwwAAACwAAAAAAQABAAACAkQBADs=" alt="notepad++ preview" class="responsive-img" data-src="https://lh3.googleusercontent.com/0M-PS4T5SiQ_WWqkAdgAkej2dKtCPXac6iXVA2wg-oE=w832-h594-no">

Chú ý: bài viết này mình nhằm mục đích đưa ra các tính năng hữu ích và thú vị trên Notepad++ chứ không có mục đích so sánh hơn thua giữa các editor. Trong bài viết mình sử dụng khá nhiều từ tiếng Anh đan xen để khỏi phải lẫn lộn khi dịch ra (dịch ra chuối cả nải) =))

### Styles

Notepad++ cung cấp khá nhiều themes cho bạn lựa chọn. Bằng cách vào `Settings &gt; Styles Configurator...` và bạn có thể tùy chỉnh style cho phù hợp với sở thích của mình.

<img src="data:image/gif;base64,R0lGODdhAQABAPAAAMPDwwAAACwAAAAAAQABAAACAkQBADs=" alt="notepad++ styles" data-src="https://lh3.googleusercontent.com/Od303Yyk-8WFY9umUgpivn9uwdIJdaOSZLb8Sbk1okw=w836-h602-no">

Theme ưa thích của mình là Monokai (theme mặc định của Sublime text). Với theme này, bạn có 1 background màu tối và text color màu sáng, cộng với keywords sử dụng màu làm bạn có cái nhìn khá dịu. Font chữ ưa thích của mình là Monaco 10, và để sử dụng font này cho theme tùy chọn, bạn cần enable tất cả các global settings cho font để override setting mặc định của theme.

### Shortcut keys

Sử dụng phím tắt giúp bạn thao tác nhanh gấp nhiều lần thao tác với chuột. Tuy nhiên, không phải lúc nào bạn cũng cần nhớ hết các phím tắt, và đôi lúc bạn lại không biết rằng đối với cách làm này thì sử dụng phim tắt nhanh hơn...Mình xin liệt kê các phím tắt hữu dụng mà bạn "nên" nhớ khi làm việc với Notepad++

#### <kbd>Ctrl + D</kbd>: Duplicate line

Đây quả thực là tổ hợp phím quen thuộc và hữu dụng. Bạn chỉ việc để con trỏ chuột ở dòng muốn nhân đôi và nhấn Ctrl + D, dòng đó sẽ được nhân đôi và dán ngay phía dưới dòng hiện tại.

 
#### <kbd>Ctrl + (Shift) + L</kbd>: Remove line

Đây là tổ hợp phím khá hữu dụng mà có lẽ ít người biết tới. Với việc Ctrl + L, bạn đã cắt dòng hiện tại vào Clipboard, để xóa luôn mà không cần đưa vào Clipboard, bạn chỉ cần sử dụng thêm phím Shift.

 
#### <kbd>Ctrl + K</kbd> / <kbd>Ctrl + Shift + K</kbd>: Comment/Uncomment

Dựa trên language của file đang mở mà Notepad++ sẽ đưa ra 1 cách comment phù hợp với cú pháp của file đó. Ví dụ như đối với HTML là `<!-- -->`, javascript là `//`...
 
#### <kbd>Ctrl + F2</kbd> / <kbd>F2</kbd>: Toggle bookmark/Next bookmark

Bookmark (Chức năng bookmark khá giống với bookmark trên Visual Studio) là 1 điểm dùng để đánh dấu 1 dòng trong văn bản. Bạn có thể nhảy đến điểm bookmark ở bất cứ đâu trong văn bản bằng phím F2. Ngoài ra, để đặt/hủy bookmark, bạn còn có thể click vào lề bên trái của Notepad++.

<img src="data:image/gif;base64,R0lGODdhAQABAPAAAMPDwwAAACwAAAAAAQABAAACAkQBADs=" alt="notepad++ bookmark" class="" data-src="https://lh3.googleusercontent.com/wjYNJqaQAC-hFb7yZoMWmvDZh3VyzLy8jdHzbiuPZuA=w469-h400-no">

Chỉ cần có vậy, với 4 tổ hợp phím này, mình tin bạn có thể cải thiện tốc độ làm việc của mình gấp nhiều lần rồi đấy.

### Tính năng
 
#### Multiple view

Tính năng này giúp bạn có thể mở nhiều view để làm việc cùng lúc với nhiều file. Để thực hiện các bạn vào `View > Move/Clone Current Document > Move to Other View` hoặc đơn giản là R-Click vào tab cần move và chọn `Move to Other View`

<img src="data:image/gif;base64,R0lGODdhAQABAPAAAMPDwwAAACwAAAAAAQABAAACAkQBADs=" alt="notepad++ multiple view" data-src="https://lh3.googleusercontent.com/MKId55i_v0LiNLCyfTkcy5POD5xrvDCLF5E2SiiXQys=w577-h400-no">
 
#### Document Map

Document Map là một navigator preview của văn bản đang làm việc. Đây là một tính năng rất phổ biến ở nhiều editor hiện đại, tuy nhiên ở Notepad++ thì Document Map lại làm việc không được tốt cho lắm, việc Document Map không synchronize với document làm cho bạn khá vất vả để đối chiếu 2 bên. Để kích hoạt map, bạn vào View &gt; Document Map. Hy vọng ở các phiên bản update sau này, Notepad++ sẽ cải thiện chức năng này.

<img src="data:image/gif;base64,R0lGODdhAQABAPAAAMPDwwAAACwAAAAAAQABAAACAkQBADs=" alt="notepad++ document map" data-src="https://lh3.googleusercontent.com/s107DLRrLOO0KtaId7g_qmW3prCQJO0-z15eIDSgmoI=w658-h461-no">
 
#### Function List

Đây cũng là 1 chức năng vô cùng tiện lợi ở những language được viết ở dạng function, như javascript là 1 ví dụ điển hình. Notepad++ sẽ tổng hợp các function có trong document và đưa ra ở dạng cây. Tuy nhiên nó cũng có điểm "dở" là đưa luôn cả anonymous function làm mình đôi lúc "chả biết đường nào mà lần" :v

Để xuất hiện Function List, bạn vào View &gt; Function List

<img src="data:image/gif;base64,R0lGODdhAQABAPAAAMPDwwAAACwAAAAAAQABAAACAkQBADs=" alt="notepad++ function list" data-src="https://lh3.googleusercontent.com/318QoC99na1OSnex_mNeQ9Tre0AAL_Eyn3nxyTeb5pw=w592-h400-no">

### Preferences...

Bạn có thể chỉnh sửa một số chức năng mở rộng trong mục Preferences. Nếu mặc định đã làm bạn thỏa mãn, có thể bạn cần xem xét thêm 2 chức năng sau đây.
 
#### Html/Xml close tag

<img src="data:image/gif;base64,R0lGODdhAQABAPAAAMPDwwAAACwAAAAAAQABAAACAkQBADs=" alt="notpad++ close tag" data-src="https://lh3.googleusercontent.com/nBl1akBhlnDB1Q3NFfm3JUupLo2h_IrAOqLd3vjCNMU=w697-h422-no">

Chắc bạn cũng ngán khi phải đóng 1 thẻ HTML nhỉ, chức năng này giúp bạn tự động thêm thẻ đóng cho tài liệu HTML, XML mỗi khi ký hiệu `>` được viết.
 
#### Update siliently

Mỗi khi bạn thay đổi nội dung file ở ngoài phạm vi Notepad++, bạn lại phải gặp popup thông báo bla bla bla và xác nhận thay đổi. Đôi khi việc này có ích, đôi khi nó cũng khá phiền phức. Để tránh nó, bạn chỉ cần chọn chức năng Update silently là xong.

<img src="data:image/gif;base64,R0lGODdhAQABAPAAAMPDwwAAACwAAAAAAQABAAACAkQBADs=" alt="notepad++ update silently" data-src="https://lh3.googleusercontent.com/dInJ-QQa5fm9cowpRzGrd-20QK5uPwoyh68aaK2v3rk=w849-h515-no">

### Plugins

Mình xin giới thiệu một số plugins trợ giúp khá đắc lực. Bạn có thể cài đặt và tự trải nghiệm nhé.

Để cài đặt plugins, bạn vào `Plugins > Plugin Manager > Show Plugin Manager` và chọn plugins muốn cài đặt.
 
- **Compare**: plugin giúp bạn so sánh sự khác nhau giữa 2 file side by side. Nó giống như một phiên bản diff của 2 file vậy.
- **Indent by fold**: plugin giúp bạn tự động format document theo chuẩn.
- **Customize Toolbar**: giúp bạn tùy chỉnh (thêm/bớt) một số menu item trên toolbar của mình.
- **Emmet**: nó giống như 1 phiên bản thu gọn của Web Essentials trên Visual Studio vậy. Tuy nhiên mình chưa sử dụng được plugin này vì lỗi gì đó (chả biết hư gì =)) )
- **Gmod lua Lexer**: mỗi khi bạn thêm mới 1 dòng, plugin này sẽ highlight dòng đó.
- **Location Navigate**: Tương tự như chức năng Navigate trên Visual Studio, bạn sẽ quay con trỏ lại nơi liền trước/sau điểm hiện tại.

Trên đây là những tính năng đã giữ Notepad++ lại bên mình từ trước tới nay. Nếu bạn biết gì hay, đừng ngại chia sẻ nhé.
