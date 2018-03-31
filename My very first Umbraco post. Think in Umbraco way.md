"**The friendliest CMS community on the planet**" - đấy là người ta bảo thế. Ờ thì mình thấy cũng đúng thiệt. Mọi thứ của nó đều thân thiện và dễ sử dụng.

> Umbraco là 1 CMS dành cho .NET Web development. Sử dụng mô hình MVC và cách cấu trúc cực kỳ linh động của mình, bạn có thể build 1 application vô cùng nhanh chóng và dễ dàng. Cùng với sự hỗ trợ mạnh mẽ của cộng đồng ([forum](https://our.umbraco.org/) / [slack channel](http://umbracians.chat/) và hàng tá blog về Umbraco), đây rõ ràng là 1 sự lựa chọn hoàn hảo cho .NET dev.

1 vài so sánh giữa 2 CMS free tốt nhất của .NET

- [Orchard vs Umbraco](https://www.similartech.com/compare/orchard-vs-umbraco)
- [Orchard vs Umbraco](http://vschart.com/compare/orchard-project/vs/umbraco)

Chào mừng tới series Umbraco và bài viết đầu tiên về Umbraco của mình. Tất cả những bài viết sẽ được cập nhật trên blog cá nhân và group [Umbraco Developer Viet Nam](https://www.facebook.com/groups/231382687411711/).

### Setup

Bạn có thể xem cách cài đặt ở [đây](https://our.umbraco.org/documentation/Getting-Started/Setup/) hoặc xem clip của mình tại [đây](https://youtu.be/PI9DjEVVG6s)

### Back office và các khái niệm cơ bản.

Lý thuyết thôi. Bạn vào [đây](https://our.umbraco.org/documentation/Getting-Started/Backoffice/) đọc 5 phút là xong. Giới thiệu cơ bản về back office (admin site), các khái niệm cơ bản và làm quen với giao diện làm việc của Umbraco.

### Document Type. Dùng Umbraco, nghĩ theo Umbraco.

Bạn có thể sẽ hơi mơ hồ 1 chút về các khái niệm của Umbraco nếu bạn cứ tiếp tục đọc hết bài này tới bài khác. Cách nhanh nhất để hiểu nó là bắt tay vào tạo 1 document type.

> Document type là 1 tập hợp của những giá trị (text / number / images / ... ) bạn muốn hiển thị lên Front-end (FE).

Hãy tưởng tượng bạn có 1 page muốn hiển thị 2 giá trị là `Title` và `Description`:

![umbraco home page.PNG](https://lh3.googleusercontent.com/jzcI5mrCuqgiQZrn7JGOJ0tYErmaTIuivBUMhj1ZmIHrx-apm2B6BDqd6vzUWVqHRMT6bH5fzuV7r6bD6Gdoq5LOfLld3C5YhaDGqlLIcazt3rELmzH3W8X41DU0ndXdxtTbeWIFCnyrg45C5Jq3AL8Bzqbh5h4RdNeVODuSkr4ACXMEW8B8htFJ7lJcKdI32KVMEBjNvwuv7ghTvYl2KwsL3wwNADyd4jyRw1OQnJSUg3PqanzkAXVT1dZlQ7L9PXlO2ve5Weiuk9Pq63jOjWqKkfNrJshGO4JEc7OyWk2eVfKGZGG5ZeCrBVFKDuITLh1RSLuEJlW2EIQDx3QKXVWJHSL3hlolxvjHxvVTLXq6I1__tOY8idmvMo02NfGnm_zPGoW39xUBpteORfc65ySWQ5ZsSmj-RiPI2RJbdLx4elnobfomV6lBPxVAwQ5ZC_kl33-JT7wHaOroZYRqmI2SgOwZZcNXV7IgCjGU4GXbQr_SOos_OGzh18QAcnNDSetNaD7ufIaeyLpdQGnVljoGCOCpGFuAaJISBTQpvqGvAcX8ttKoyXHuv2o9hxYu3tz6ev98N5CqWKQ8Zl4CjkP7XY_hOzIKJx0A1sI=w625-h389-no)

Thông thường bạn sẽ làm gì? Tạo 1 class với 2 properties, sau đó cho user nhập 2 giá trị này vào, cuối cùng lấy nó lên và hiển thị lên FE? Nghe có vẻ hợp lý...nếu bạn đang muốn viết hoàn toàn từ đầu. Nên nhớ mình đang dùng Umbraco đấy.

![create-new-document-type](https://lh3.googleusercontent.com/QTczjaoe9LRM6nA8KzldX1wfTAF0lbv9FjuR_FcW5ZY3CavxKSAx8Dx0AWOl7oNEDS22vushQoWdFQNYbxPdIVhM7nXnsrpkIfAmI8cBFzNDc8piikE4OhygZEt7VKTDPAsmehfOcpFk7xZ9fIRrwXVDDyUIHe70uJHQQGB5crs0XZQd5yTb4IRZdhE0nsnXolrpNPAYSNXdD1eTP9oxb6YAVwEhWx9v8DRfNOJ1CO7PalFDVKk8VouEG8EN02aaX7e-EeYuVkjpCdTP3M0JbXSits9lfoM_YTa7Ol9KuW1gttaY7Ui_K2C7l_FMsEIot-ilM9UWdlCKx947sG1UK6OcKR8c0Ty-cdUtLGejMBZfwVECvy_lZjC4Xjd_cTDWAd9lio2etkI7aCV5Nt3H-xjny0RnyE0nI22syZbX9gCS5nPlyaifFzj_AXr0sBFcEe6obgn2Nte8ByFrU31jZl-BBY32ARAWpkBltMgg3PrZYSFqz-DCkdJAi-VPtaTg88BrMUmL-n78lbLszrBlVnXAwEv5t96xsNtrae3hGzrrtE8nOxJG3smBxfe08Yj0CWZzS8X1idLUMak5GYHAT0mXSJvc902n-vfEcEA=w697-h435-no)

Mở **Settings** section, R-click vào **Document types** và chọn **Create** 

> R-click = Right click = chuột phải. Phòng trường hợp bạn không biết từ viết tắt này.

![create-new-document-type-without-template.png](https://lh3.googleusercontent.com/CrhoOPQ9uAYQW3L2HVjyJK1MvFcy-M8jEbS81CYvPAsi-gWm6vlXvX2UGbzHsIU9bUnFV-eRf1n6PivlGmPV5G0M_J6TsPz-ikgQYi42H6xIH9EMNabjm5saDYT5rMpfnzlaw8FAmTjLCggJfVQ4e6M5EvHl005ME48O5-DI6lcZOT5UBUQ-9kzqeOSuYFwl9Y8rVY_J368MBxCH07mMxMhLwSOJmJn5ZQ0d7p6gfSPYaUBLkezhC8vwyWZoZdGKpthKdhaKPVnfTkA9HkZPAqjLucZWuR3xivP7plCp_1I2x7OtuEcwT_7g-IqkZHHU_a5H_Ohflu58eFlAyV0rKmXVEZVeLz5WbGRCPLDQxXLZ13v5UAIdQ7A8qbhiK8Fm7s55inFckCkNCxSKlL9Gf8lGpKL5ZMk3lyFk0wCAF4-8AY_V9zsdKDMCo4rXKQJcBlr1QIXm3lOvVxcgaqba6V-i-Orylrpw7_KBQQVp4hR3Yay-YKbIzBVNDOWXXxLKKkVzf28VphVEQJZLq4fQ-jYc4gPJXC9Y6PMV0XsAKIyhzGUh4Yu-96KEHwBDZBsRgbJfM9jGQh5se-q49p7T9o4aUdXYXUITGbZxAoAhg-aUsCwSQrPwopfLbAdW_lg-PFjikMaxtFD_8_FqUJdYApanTqj1WuWF=w755-h418-no)

1 menu mới mở ra, chọn **Document Type without a template**

Empty Document type được tạo ra

![document-type-setting.png](https://lh3.googleusercontent.com/aKpxxOLDWlohdhdWu-03-tAwQWcFgEcj2vk_4nAfWTCHSAtNWbKiEhscX1FvFZly_9FzTduR2fGfYry5-YA3Dn14Z8yTJeV8tqCxTEsH3JQSMQZDVUbWGIy8Y5y6r1Rgo1rV9Gv4Lhz2wvCYFQGr2no9bFDOghxb4ClhgZhxlrXTUqjACVAn8sHu7krbsxCxNwoICxf5zajzeIHQyFYJMaYmS7vudBIx7JOdgi8TvBck2ww1eCXUAf3ddzwyjmNiLr3KxAGJe01rP7l7taD_TNzyrXUN6aWqYjXxQ4xhcy9n829INCU25N4-eUtJnjm5jJHAhqd2tw0sRQXkgYheve1N09R07V3uA56hGDcT8isBL-PvHJmuuPHMl1w2JGuU6RHUxDFITRleulkCbCi9YXHg0P13uaMRguouEw9meOfBwMTlYA6tJIChQYwYV70L6obfa0oDu9AszAg1hGAIryhBe14tAsjPcP_vnB6elz_QILNY7V_D0QE9H--VTfWSQMqfRLT_ZOyS3mgCj9_Uos0vg52Nng2lkbQHPRS31CvUQLWw3NK5gztjGOSnY6R8HCTNJgRjDnttXco1KUZ4mbZubWXun9J6Z-CGq-T6UUVAoCCr1lI6DLxSAELr8KuLlNN5qK5roG8BcKS8GOFu1JENFItLMhfK=w627-h343-no)

Có 3 phần bạn cần quan tâm được đánh số như trên hình.

1. Setting tên, icon, alias cho document type
2. Chuyển qua lại giữa các tab
3. Vùng thêm property

Trong đó cụ thể

#### Tab Design

![document-type-alias-setting](https://lh3.googleusercontent.com/N6EqiXqi8LGhmj08eyk7tKnRg026OkDZ7f8K0zr4MV5E-de94JbYFW8qQpkg1jyXqg-SarrNeRM_Xdf9_R0dAwl92jCkj_zmWiwJZcagqB9n1P01Nbd0Gojrb45qyhzx-wqYMjoKDwG8orKDpBzaS3zG8NkPlsccQm6D6Mxc6TMW4Op8CzEZyCWvfk3TskYs1PD3VLZGyzD25cf8IMOWNMlfrZlUrBdcXcW9YEDiMK6v8n1Q-X3mOKEOitc6fNB9vROipjz0KtTXOcBFtOXGmhI_n3G5L7qYrbz_YOJbDkGamTva_uyirvmXWJ8PdLAA_45ODF5ZGq4F-zHhw3Ot7uhRO5iIHmMHh71CUWZM6-RFF3HEQgCHc_GWS2bQC1ELWOV9LpU192Po-hd5BxRbEfACt5-GhiT8G-S255vQKea9OpBHHdlt0wEDx97YVF36KrODe1NI7sw-O3iEb9IENVi0k5cA7w-zRCFlKZr7kudDJmeTR74BKhjQJVAJBvnkHmwLW80EKQTMcanY9Kc7IcFXsnZGKIB0_cKmKOPrAlNriKbhwSKHMVw0apw0hEXEy_m5wSUIAOyeYtRMhXwF3cOxXeOli1694zfN4dlkB_vqJYLleqG1xDk3TLWrGr7OWDXuUIzEv5eH9S4nrDZLD1pvDkJs8ZDU=w502-h166-no)

1. Document type Icon
2. Document type Name
3. Document type Alias. Đây là phần quan trọng của 1 document type và bạn có thể sẽ cần dùng nó thường xuyên. Alias được generate từ Name, tuy nhiên bạn cũng có thể thay đổi nó bằng cách mở khóa bên cạnh.
4. Document type description. Mô tả cho doc type của bạn.

#### List view

![doc-type-list-view](https://lh3.googleusercontent.com/UunD7krdqyawdsZc2WCJ_NTHEFgUF2ijxcbcSTuGt0kpAYePPfUVWiLaKAFLftaieowQPH29yvHbqtbIsdvd4dv_1UpkPUGXPHWrdanCFJcFCCLFoEHvf-ZlSBmZe1PFTKWiyX-J19aCwVWAHb_xjDEhX6A7XcimjmMoxEVPdjDN7aD05EZlM-DcW8SD5JoHLVe19LPscf9UdXu70WfvjKomch-KJVva-tKeWE6H9m-b_4lWGafvtkhVOc0z9AXXxiBHwVehL7xOsJOPLLxVmMHyxJ4nl3K04zC8DH63C7SfAe32axV5nzc3SsAZQ_vBOV8s3j28EQ_HD8YsAU5-xhLrjwsiLCtETY3jDQHpjAeN3Iw-10mgIg1mcBWdDeXDhMGkyJFJMQP9Zs6LDBpd3QYG8DjM8Yx00jiU6geG-1lt8FZ4_H6Y4JLJY90D1GyQTVtVV9YzcfombWongkfjPUlxK_U2uoaClaBHofGuUdDQNnrZtqTXjpcP8hoAkyhY-Xi39ChxhG3EsyJvPvjb7fTHQHA8upB3k67H_0CA5m3Ytovao16mP7rUG2sczVPtdZf1cDCtSz2umVJGVKZFcfzN4j4fc_id61OuB7-gbxl_pPf32c-uW1YLtKnhAeYGv7uocfINh1FP6Gmz65emgLplM29edvtw=w749-h285-no)

Trong trường hợp node (là 1 doc type được thêm vào tree) có nhiều child node, bạn có thể chuyển đổi parent node thành List view để dễ quản lý hơn.

#### Permissions

![doc type permissions](https://lh3.googleusercontent.com/IXFD-N-I_fJI7PMRTtslUg5h-ziVO1d2gRJEeZZTBcz72O27tBzRTdxQ2lc--qHh6eGFu_XQVOTwqQqSSGfqPxlZPvONUVdPoVzvgsJehWwLi6Z_zR6tonh1coArY3Vj6cf4r2xwqkuxkistKeBEAkPZwQx1R_kvzoFNAyOnp90kKlMaJTmG2sVDOEtY4PEoTmkt3kyz4Anprj-90Ton7Br5VRDb2NP42Ir6OWFajAz9LXfxzzPUQ0m5TrBrRkbwov5_ikynLSFtGNLFzqFW21ej74IhxizkT-NjK-uIISH76nsQaBR-sbN8ZWQPhI1pS7daQeEW2ux6dKk5LojJqdkyRc5pa31vGffOJG3e0GpRhEBTbDASf_NpueihnE9GegSPs2nmyNcktd2n-y1jwjS_4EWk9SNNqvN9CArrOUU1fF6f-wjGN2IxnHPdb0bNZssa_XMKHIR8E-irLehXqhMXUNhLXaONRYAZVXDTWEGFpGB_AVQxtJq0HakN64BEkvm8b01xtwMNJCEuhoJsfZiFDs0yvAx0YJ5273pgogVf-VKpOSEZtnY0uNHJSIhFgzjyo0EbvnaHxFxvuqK3Mini0lKTvSnf2B4Rvu4534YEy43mpQLjygSWYneFlDn0Srx5E0p_Ibc75t8pN_A8QrCYT6TCHhW1=w748-h347-no)

Cho phép những loại doc type nào có thể được thêm vào child node của doc type hiện tại. Điều này có ý nghĩa với client của bạn, khi bạn cho phép họ quản lý trang web và chỉ muốn họ thêm mới 1 post doc type vào 1 danh mục chứ không muốn họ thêm doc type bất kỳ. Khi đó khi họ R-click vào menu thì chỉ tạo được post doc type mà thôi.

#### Template

![doc type template](https://lh3.googleusercontent.com/w8QJpaU_ZG8ixXbxFjEuVJuzkxkgIMr-KJLR2rsV-mbheaacRie0s9L-l8c8u0ajsuTSsS3L5AuzOq65UFA3wl-hhsjN7o9hWEjmdKJEb-2kcSmbpCr85i2DVFJEE2yvUdY5klJkOP1V4YVRZxIzkSUGkOr7MtWcoK3l1rfy1xQaMe_MsOVBirZxUbyqurwqDEdBzW9LgcTYP0EbIm9MUG7AZ2qx83kCJ4o54jVYdf97Te4HoyRp_vgf21yXew7BD16WGK9gisodOKVtEMTc3TNTxbxqaWzCndmQKRzFZKq5KtkdzZMrSYmK-0wBOOiBjohgEQEWh8WPutWmYdO7MJNzdFxp91MhhxEEO9ak5g4LDBS9n2FbT5KbwGdeetMC7kS5IMdPknRqUr3QAxto41pnLRP6vE5X0hqfZsla_D_GwclG8bf7dXJQRne4l3dui-nTUc3ynyrVke12NbbMOoVGY4AkHlRDRShbNDG4-rtUjb_vwhLiNmsRNqdA3UAeQwyceMNNhFzxqLKzhOMc3Dnp75oNLxyzYqF_fFIuIgmqEB8Rm-0Z2tkTuYwlFmaJ_AHSp_vvHbqfy0j5lVRgjTpzP5s6umhP-jjKakV_zuj7yAxWDwrdUTC-WoUYCfqCFsEFX3wpiV0OmLHgLuj2cKsrV9tZC1Ar=w748-h331-no)

Bạn có thể hiểu 1 doc type cũng gần giống với 1 page vậy (gần giống thôi nhé, có trường hợp document chỉ là 1 partial view), khi đó template sẽ là View cho cái page này. Và đây là nơi bạn thực hiện mối liên kết giữa doc type và Template.

Mình sẽ tạo template và quay lại phần này sau.

Bấm **Save** và bạn đã tạo 1 document type thành công.

### Property

Là thành phần quan trọng nhất của 1 document type. Nào, hãy tưởng tượng tiếp.

Quay lại với việc cho phép người dùng quản lý `Title` của page, bạn phải có chỗ để user nhập title vào rồi mới lưu xuống database được. Thông thường thì nó sẽ là 1 textbox (`input type="text"`), với Umbraco, đó gọi là **Property Editor** - PE (editor cho property).

Hãy xem kết quả khi bạn tạo 1 PE trước, sau đó quay lại với cách làm sao để tạo được nó:

![property editor](https://lh3.googleusercontent.com/OJgLEHQNNojXJs7IAN1Ea-KFCNwv-es-Vrp82NN-nJvZzrvVcUe8PfaNl29wO-_Obz9cGbOmzWrsmi9R-l8cFTEgrCDu63i9ZIgdkQMCGmwzsbZrc2OqrX7kW5Fk3JPYEf7LFSip-48J0zQLYLVDl76H3eefVufRjuue-f-oh57xmT6iwDbiTU-JIZyGGUUfo1Gpc36qeeYTcl0cnbz6Ic9bWejR8TPi-1IC5Z4kdG_x533f4SAbtVna5YOTKQiPRsxhJhYpm83tsbu_xGwnvLQCvlu8iiwywbzEbyLiFiMxCHDhXT0s4rb0zeWV6DdjssQcjw6aVYCuv43D4dO4gGJveb-n8xqBCNJ1a_YImKJFmVfWldm25oYNr-Jfikcn_73tYfdwls6rYKMbT-qHZOH7j5nj3GJO_CyFhPLAdALVnxVbdl-COGq2RKqUTnqhOa5Q_aQ8hi8IXfeKA7wxRIVEnoQDr7_Qk0fRbSO3evB9n0pxu2Q6Q8TQAAQpxImf-0SsSEH8RSsDLdMUe1e6AuYWS5vPwTc3SGzySQk0WGaPMijpkqqWo6Ok3xUZlWmih8kuNHq4oG8sFeB3Dz08WkUO9hJJiVUYq2fzWi9cAF7fvuMZJ1ew8j7flAvsKAIimF3E355Wu_3V4qfa68asudKre8DLgRHs=w732-h536-no)

1. Property Alias. Tương tự với document alias, đây là thành phần quan trọng của 1 property. Bạn sẽ sử dụng nó cho việc lấy data sau này.

2. Property Name. Bạn muốn viết gì thì viết, Umbraco chỉ quan tâm tới Alias. Nên nhớ là by default Alias được generate từ Name, tuy nhiên bạn cũng có thể thay đổi thành bất cứ thứ gì bạn muốn.

3. Mô tả cho property. Cho dễ nhớ và khách hàng biết cần nhập gì vào chỗ này thôi.

4. Property Editor. là dạng control (textbox/textarea/radio/checkbox...) mà bạn cho phép client thêm dữ liệu vào.

Thấy cái nút **Add property** bự chảng phía dưới không? Bấm vào để tạo mới 1 property nhé.

![property wizard](https://lh3.googleusercontent.com/QJIEMu4eupp0ZnKN0lmp6t5HfZNJ1ov7EarPrEf8nd13LzqeSkQJPZdQ-DJLlLL1E8Hk06PQk_dOK_THxcCHrDZKc00BWiY6yV0sqP7YUJO7CYxDFUIeXWuGweeFs9rXR9HmIofSR_VfBJAkJoBNq6lOD1wsH-hTo9pfnv0F_oegoCyYU0zVeUQeSDD6u4i6nbwwU5AweF37EpbVysj0cCqy83jAG2KoAl-vI2tUZN4tJ684zCnlS4krjlH-Aim-1XRxY02DNiiCPwhUJ5hRZc74lFRsritk0D9YgGw1fx2s9ZSq6Iwlw7gATMXSVMGKtLHU_jYc6U1xHDk7JeXeD29VYJapIYu7NBDP-E7blx7YEUVTpAkdh_qYvSUZizQ6uCfbh7uVm7Nvl9S796jPp9rsYt8TVZtQ1t_402ANM1Sq3CjQPnDJFEdqIM7ya4cNvF6pWMqSI1jCh5gvnmjuffU_CkXi4RdFMcuQZD1BPzqVg2so1edRtT5NiyJqvyVVvH2XXZ0yzDrHe-o9ZZfXEN3MXE-IfKX8s4O2nMSI2ICU4o2oSlbVNNRmrD--itaBMzHS_0yUSICgsyl3MqXViqVWySwc7UQ_JRRDS3U2asTYokTW_I_-74uon3wHEe9lQrSfL-hBO4NwLc9qZPw9r2y6eGWLcwGN=w747-h625-no)

Tiếp tục bấm vào **Add editor** để thêm editor cho property này

![property editor control](https://lh3.googleusercontent.com/1znIrWcuLHIiOxv-PW-SrufUTCMkiStlmb_ILTOaQPYnPNv6MKMcqPaGBuJZ-ZhzrlfCo4xAeUuyJd1OIqdTtqq8rep43WnTUkvsYeoeVbNDA9Nd-XC12QFSBdjSjGNcZcNLk3qvRY9Q7pXweAJYNViaYIafVFnRtJMIUpn_VQVb-oIP6TeJhvVC0_sthDJnfpqr0tMDydhZZbxLkcGbgH13zCJG-_QPtaHV--phsgJB42wHFAGAVnN6Vsl0dtUX0RBDinJLLG7iTqLS5MKprHUR46Ikh_LmrjaiQP1rc6R81athut5WTNrT5vHkRvyJ3BIncjN1NtbhGnzRiFQ1KWdDUq2_Wux3KAkBP8vJmyLIpQuKoo46-xPR4popRtEEB6vfLGM8HMdO0ky93l5AB7lPCQIYggo-GO_c5boh5R5GfAiw-aIa7g9DtUVFrdT6SWEbMv_0R3M4NTLpNDdda8ztcz6xnA2zzUzc3LFB2uQpGN2N3J89o84m7TD2TLitQwbL0TiwJa6fu2CjmSPgsKdBGBQDKVvZSQMEQoOIIsXdhdtMIa3DB_dGuv8pQm6M-B2ZORH5gvLmOLn2yGdBn2EOXxxqUnNJStF1iIh937-TeG-X6Xh9imJDH4zKgKgdJEgQYse-dceNR6AdNvtmf7ItGixtS3I7=w746-h627-no)

Chọn cái nào cho phù hợp? Bạn không phải là con nít nữa rồi, chẳng ai lại chọn cái **True/False** cho việc nhập `Title` cả. Textarea ư? Cũng là 1 ý kiến hay. Lựa chọn cái control nào để người ta nhập liệu tùy vào bạn đấy.

Sau tất cả, bấm **Save** và bạn đã đi được 50% chặng đường rồi :)

Tất cả những gì nãy giờ mình nói có thể gói gọn trong video [này](https://youtu.be/kii_qA-U9uc).

### Template

Cách tạo template cũng giống với cách tạo document type.

![template](https://lh3.googleusercontent.com/ta6AQ2uexTfXOEyEC15A67Y9-p_Jm51M25IkVCaZZ9cDExokSNqKrZfbTvNWnJqbKTkMpFM6eUzcj664PzqeOBux7HXnwfPPtOkKm_9-5SR7IUHcSSpHLPItaiueNReF5Y1LRiWLs_vPG3JEun3DDs3-zCqfA8niYjCkDf-2xQRVgOb9WnHkWGEICdQa6H-5BakU-SrNsKIExReIaCco_d-txyuMqD3tPlIHl1RI8LgD1tO7Se9XhjbQF9G6uF_I0PhuqCVIRg34OY5QJsIf_t2HyO1li8Y3-DPKWMjDuq9GdwHuyf-mZEEjqGVq-z2jHSmDAWd9aE9WUAHC2cuEppt05LP2Sx4wJDvYdMFbQxNmI1C_1TXHGNW6CzzkfdkWALngMRWSb9J3QziNMtDorfWhL4OCeNDwaJ8ccHJvZBmy7JOAdFyWbrpLCeC1vbcAIOY_h1uwwyJnjhFlYA-jlMvXGmgTn_U1RxWDjyaKTe7Y1_mVrEGP3IFsGjjI4-vJ-WEmflRoQ7V0DhEQLZcZPmKRS8-zzZ6bb4cV6ULc95PTgrwfK-vfMTqQbYktNoJquE9Fp83gMYenbchGh0VKbReEISyUDKF6lwpe9mJ5lyuTk8HKbpznqQfqdkQVVe57aPIe1aPlu3QhyN8-0VcjLBb_LFzQtiLK=w1131-h426-no)

Đừng thấy ghét mà xóa nội dung của cái template này nhé. Nhập tên sau đó bấm **Save** và bạn đã tạo ra được 1 template. Thấy cái `@{}` vàng vàng kia không, nó là cú pháp razor đấy, khá là quen với ASP.NET MVC nhỉ :))

Sau khi tạo template, quay lại document type và assign template này cho document type của bạn.

Với 1 template được tạo ra, 1 view tương ứng sẽ được tạo ra. Ví dụ ở đây là Home, thì sẽ có 1 file là `Home.cshtml` được tạo ra. Đây cũng là 1 điểm hay của Umbraco, bạn có thể làm việc hoàn toàn trên back office, hoặc cũng có thể sử dụng song song với Visual Studio để làm việc nhanh hơn.

![home template](https://lh3.googleusercontent.com/FxKGT6G9fNAOwmZEJjz_r_90nOf3pC-LkwLABN8QNwbU4w_KGk-uRCg-vb2UpZraLUHgPrbNGJuE_3QxEVbsw3rg4CE62DMMQQsgS8QW9y90njamCFnaJPK0diQnlrktwZhTf_liZs3JDSwZq7r3ssprJ8bybzRy2x00GOXPxs-DXrjUzOSfFgGF8fot1izU0dVKVqrJB1X84luCLl8suz33Am3Rw7GyEELYh973W0E9-eX_JhV3E3n3k8mXqGlvOqX3xrRK35KEWUS1WSXogxAETh6AvMbw-h2aABU1-9FvYtg-See2EKoXZYF0m9i_uE-VXpHx-sAS8RFytIS0kP6QvnlNec8AEdbXGM5Re90nsJzEPGTejM6zRWzGJRm971I3rO-Q8Y5CXe6P1j8UeZb5cCWPv1PP6dSc29faYSU210Z1E1a6GxYYM-I1P7ShZRMvZg_8F7iKnAipIjIeGAQ5WvaYKMUrPGyr--_Eqptf0pq3ARD8ybY9UpKUxpxpZNTx-wGVyEq20vhvv7eQSO7fE192I0-HKv_B6zxHu0FRSpTj0x4NDR8Y1fUUuRDm2BJgQiJ6BryECAQmolbEz9mWiO0boI919nZIeqLTRCQbTnoX9gIHwHrpYFaizLgWQWATIhxBRuHx0vxNN2qWoKbzAtA3QdII=w482-h503-no)

Nhớ là VS không tự include file tạo bên ngoài, cho nên bạn phải mở chức năng hiển thị file ẩn và include nó vào nếu muốn làm việc trên VS.

### Content

Là section cho phép quản lý nội dung từ những gì bạn đã tạo ra. Nãy giờ bạn chỉ mới thực hiện các khâu chuẩn bị. Content sẽ là nơi bạn thêm mới các node (là những document type) và nhập dữ liệu vào các property của doc type đó.

Việc tạo content node cũng giống hệt tạo document type và template trước đó. Bạn chọn Content section, R-click vào Content vào **Add**, 1 menu mới xuất hiện, chọn document type để thêm mới content.

![create-content](https://lh3.googleusercontent.com/12wsGuXJ0DsbPGHuw9n90sS4ImQLdU5FC2ovy-Uwvjg6pxbJvc1OK1GrI6rFg6mDax6qgY_DZqMIRU5dwQe8-N-qNaq1YNIeFdsZKDak4UPUkgFt7QCExim5vlLIBlVHDobkn25rU4t7z5Xpmk7wmrE0E8u1T0ca1a16fSsFR4dAhaZ17EkQOBQchOSYjWOY_6BBuVb0kWofMf9XkBhbiJtRs7B_pgvQ6U6HeNmnOgI28HQEAkM0_trESNulvucAncAtEOhUXUy0cy4xI4m_4tmmWP4ooJGcdz9e54CyIx5TnTBuvvfOLxCmielVMhkqVwW__PT5lhxZZJ-7EDuYiBg7qfoiOcp7yKBMJe3HXV5609TJbm27Lut8DttQRnxdkjcEyCTs4Rwzft-AUg19Avj8sRFlSBTwh1So7HODHxc_QwrRbYKvHDI4v8zj_23rrfx3qhAuxvw3rn3RF2aaBrU-1tuow4c_UEfyC0mF73ADyEyJ5OaYMqRqgz2ZA6PU3vzdUHSsdH5BUhrke_uwyAOJCxSpihoOIKvJ9sURrzNMRIvp-bw2bRB6aO1ehGRBK4WN4dOUDIsRsP8ClR64czCa9ba1kgAa4HRa6DUN9qg6j7J9N7ZqOVv99krgSmx7urlwIfkEx-f7wi2xk6Vt-PQdKRNNNxIc=w879-h370-no)

Content được tạo ra thuộc Home document type, và bạn sẽ thấy các input để mình nhập data vào, đó chính là các property editor mà bạn đã định nghĩa trong document type này. (1) chính là cái tab tên **Content** của bạn, bạn cũng có thể tạo bao nhiêu tab tùy thích bên document type để dễ dàng phân chia cách thêm nội dung trên 1 trang cho hợp lý.

![edit-content](https://lh3.googleusercontent.com/PSG3yrV9wEI73WRcbpRY8vLK2zqxALKpfUWO0Ra3AeO67UMUmaq2EkPv7oCrh71b5pyaXKk0b9ByxA0RdcKvnZbhutNB6am7HUg5IjZtrWmDvIw3-07kr40yNt4HLIkJaa1mk3izz3T38u1_lJdcHDyBN3Z2tLCQ9n-Dnb5MYBOPSxnLMTCnpxIXCmhXDqjM6QmVg4-ndOSXgMtg9clKGE9NdjEg-1scBVMXwbqL3IF8Qp-atnS-4KOF6WCZFNDhhBWls059qaEkc_Wro_Nz_nmgn6hzd0PlU--WMMOO8CyEwxZ2mXPVVZHVGVZvZ_K_murLbpBGTWPq_HY12O1F0BkIdKljwXtdKGQYHU0p7B1Ysd6qXFgUs691ewvndG9UZwXiCic4hZI4HINiboNthbKQojYQfXC7CL1OVv42dySLJhUnd0ZSOHxYPekDKTOnEDMzIqN221ftX1CmkPl6JniHURLquuCfT8ucJE5nES9tQC4z7rm5cQn52yJoQ2BGO5PRl8vkSgULpT_4T3W1Ok8o_GsjX8o_PJLRYi_zkNwQwyIMWOcad1j_2hKyMIQP05HPa4e2tMIPyce5CH2C9qXI-fNQXBiYQw3IJxGDWFiq48NvmAqFNj2a1VZ7SMhOM-kGZ-CmXKphgbBf1u1O4ROEUitiZQ1G=w907-h442-no)

1 document type khi tạo ra ngoài những thông tin mà mình định nghĩa còn có các thông tin mặc định, những thông tin này nằm ở tab **Info**

![info-tab](https://lh3.googleusercontent.com/_Yd4G4PA2LzDD6JIZMKXQ4fTR3q6ihOR3bYLPqleTlQyYbgmgvzIjpFqxvjKR7haXT1fI36Wh1DaLZImS6l-vr3n2Gq7FjBcfBvITN4NP8dn-Gu_EOHVDq3ToRK58Oi1PMEtcTwnF_mZMgmGzjWIcaBZPiZKZIM0VKGoqjsXMfOrT-jvW9BnSfefxFDshR93hdYgouZ5sOjo4vbXvWAVeOq_rotqMkXmfrT6f8Cv4bGBwodv4cwT7CcN_9UA1OFtYJR57bbgdH-fAOuuYyzSK7Ih4-5ZvmhHk7lS08JBMNAi_DEnIvYc3-cADjZFI8gddhYlX01XRPVvQmJVsmMioH7EP1P59_DMOTi5KCEXkBb3gUYdFDaWYEFchm4r7YoDu2z-e_ZSZ1hssBbmIfvnHW881OZClsPXmxkgWacWrZVK596iI2zNOdzq3KMBltp1X30LF9OKWV4J_GFLJVE9Jb3hb14P52PC9NiEtjnFxHaPi2zwykCFHHIttj-UHjC_J3hSW_yGwlUCrN-lIFY_M6Pq91qUYMpEQ4Rehawp9rGI9zZJmwLhN-V2jNLuhVwd5sgORoNLftuzRu1l8FTGwFH9xO1CbuyZlvZgcp5qkOWsGgW1dn7JqLg7pj3IeKvnQ1qoHmnz5Ttyx9qnztIvfdn0pIv6wk7M=w754-h610-no)

1 số properties cần quan tâm ở tab info này:

1. `Link`, chính là url trỏ tới bài viết ở front end.
2. `CreatedDate`, `CreatorName` ngày tạo và người tạo content.
3. Status, user chỉ có thể thấy khi content này được publish. Để publish, bấm **Save and publish**

Với những gì bạn tạo cho tới lúc này, hiển nhiên bạn chỉ có 1 trang trống. Mở template ra (bạn có thể mở bằng VS - nếu có, hoặc trực tiếp trên back office) và thêm 1 dòng đơn giản vào

![edit-template](https://lh3.googleusercontent.com/g9WudGrLwL4diBaYbAeuy_EDYfypPS2PRnteHxwQvnfPkvRZpNxSByz8V711b5T2cPmnpDJGzWbteal4FBboJlZHkJJjDR0h34E82gQnzTapt7gvnn7zIEupmvM3_ZMW_EJV_Lv8JNBDsQl8iv3rQFUmTk9K5XrU9h1uPYj6yLo7XNgf3YK2Yk1-y_4BGBfcflV59JuG6ZyxEMschjtQwC20gPR3KUbcY_DhYiAqXeklxKJEdmiirA9uPEyy_zy3GuS7ywHkRJk6tARFD0lrpBfhhO8bJ-76j8QXctStwhDI-hORZJZQtp8tKZ4MCZKz7UKjjJHPmQOdbpgd847d19iof_b174ZDDAykDEhL3K0M9wX0pF7WeulBboEkxoungh1nBiQPqwHLZSuSdTiqJcCcc-WUhl0Bl6QVyUSAFMDkaA8GBqplWvKKNNUAHpfi3P-kgjf45uIaeg97d3pAwCfFZLV37mjBBIqyrOET57QOp8UHO72fYNvUR3lwCfUutD1dSoGDo6ImMTxJjNmHTyu-SC0lOiyUsEK9UhSIKp83-tp6z6EstN8JqZdGCBiO3fadFyHTkevtJtz733WcOmw6vQsCh74vSZfvEiPCi_zhRzE4PgSdZ9dyprva-BDeX_8aMhjHDFkucqMGLX3egZI1XNL51_Xi=w819-h493-no)

Kết quả sẽ là:

![content-view](https://lh3.googleusercontent.com/YhHx6Zh48GeD7yz3QfGeDhJTzT28D505IHmn1nOj5MmGWo5FXhRhpefF2PeBVmZYnzXZDB0cg-B9X5vI0ij2NqGVlmE67mkDuJcxDavGfwl4gCoIH4T729I6Jz_ax7pE6WkSZrxcetjlxjhdiS-22nNvGg2vE8aEccVHi2WfZTWzorkrCazj8FPYE-gyIfVZ6GrJR3p1QglzcdclgrXUZEKxhBVSYd7yXVbtZrDb5543iDRX865Sj3YszL5SWcP2hzeBWOXWRqHatMmiplQaPdLVrV0Avmm-8R6NJ9DYbaGxVxOBBu7goOfDBkZ0g68bFeO8nFpnUultjN-MwuYU0oLwnbnibuHAVEN3BISphGsd6cAz_H9R3reU9X2n2LnF0A39xaYWV5OjPVZZgpAy8iDF3sUL8JAV23uWSBKFYaH_Q7v_hhbhKfp_Blu3ZCFJuv49d1Z4vMXTdKBtcQ8oKRxz2Demczh3WM_qObqUFHEPyL7COYZiblkIVi-BplZaQONn1m6woEAYZjyFkq3twR2QH1YCwCTjTpuAbf18Vo-RjmivcHWhTMET_TVJ5FcYRCPSNqoIZH3tmhQNMidnxXzPnCi4s3Y4pxqROSBwcDx8DyrYAk3CkSjrWKcvntQwiubgsBj_UN7_K1wUs2cZ5Fsld-fBSfiv=w486-h280-no)

### How to get real data

Để lấy dữ liệu mà bạn đã thêm ở back office, sử dụng extension của Umbraco

```
@Model.Content.GetPropertyValue("alias")
```

với `alias` chính là property alias. Lý do mà mình nói bạn đừng táy máy xóa default template là vì extension này chỉ sử dụng được khi bạn có directive `@inherits Umbraco.Web.Mvc.UmbracoTemplatePage` phía đầu trang.

Giờ thì có vẻ đơn giản hơn rồi, để lấy được `Title` với alias = `title` và `Description` alias = `description` thì bạn cứ việc

![get-data](https://lh3.googleusercontent.com/9VVASxTNf_6wEWroL8UPKHQSb3Np27yLegL02OTjrCUfPkUnfc8Ps3Dydj4Gq4BzgdYdgp38wcGzCc8FdR1lSab6AeNTDVEvb4GuSZvfNx8sOBOLH52hVGC2dZx5VWe71sNORslRako3nPvvhQ0KCn-MaNiKLUWCFF3aOaSDM-m3lnqqqzzkeZGWne_IW9JGnq9FEYzq4lWabnT6-M2TlQgOGzU09KTHHY4Xv_H2SksQAe73ggVV16vVeaHuKqfjFkHBEJw9t4YVpb552O0w81e0e6aj_4jI7O8wKIq4U_iUKPZz39ibfTE8lmokAKiZ9eRcKgjOJCj1SJ7dZ-xEV8vMC-fqCzrsfwQB8A2XAM1fvGQ1NnN2uil4dZkilqqhCuoertwdfnc7CZiaBSrgdpDJ84DAc1K0dr2tqGfoy0O73UbfTjZdYTtlQAI1leh1VWuA0ofsoQC8GJEztb74JyJTqqeVs8bLwCa7OoON1tJA-jGg_G7fRyVoiwrGc5fzJBPPsLgdz_FLwR7E6Urg6B4iG30ywftnKVWmIcOYuzFNBaMRcd7I_VYv2JkTtOKiEjrBAAXPakAOPCMnd8GoqO2yUJoR0AKmWoAyWpStOUdCAIbjhtQnhnhTvEl5s_9Pb-YUKOxmkBYnqpJqIwmgLkHSGj_QX7A5=w498-h258-no)

Và kết quả sẽ là:

![data](https://lh3.googleusercontent.com/dVlFyts3jdRP0hxX9hcyGvN6jYlZ3TJGOZW8udJOgGZXhoimY2G5bPpbqcjNtcAv3cJUxPKsyYTWKrSdFfU7P-T7Tv3LigJqJXviEBZXXw_9kQZi3g6gAtsuY0YIMYfpW0WAw6HdtotBTvq_G9J6yitm3k9U-SxMUpPf9MrQFD0oh6z1l0lYkINdfaAd3Q83EdUO9wa8Ysm1GtohvxCrkRNBX_FSH9WyoCZ2FhUhDQ79Vjt_aD2gh0NG6fQ0PYwmffc34bXXoFIFZAPwHcx6Aq3mSK-unCyGX9idluc2ma38mTHTJ2JSmRsKa4mGhLqkdEPC8ujadek88uNrdn_GIh95WEE8qqfAj__NoFbECE4RFiKmmfcXUgzaSv0FAkrgDYOpWek2Kx1nx5yKSzGm4FYtCvnr8nDfgNfyUr0VqxiEtXwZd6KTf5B1DCOy1rQwk2Re-sshLF3oZYMWguLZtMAs7X8aIjXBP5Z36GEIS6ZfwX8fC-CQZfwCi1HYfhdVNjzgMKKNNFPtPAMkLlNlV541IcABewfl9OZrn5Km6wRzc6YcEeSdhPhOxXoZseMbJY7b9m-SEEMpTdrxM7WT54sT09U5Cbt8kbBZs4dEOPeTQZfUKNrULGYXAZJxJw0Dpo4s4lS3trU8Ar9Qx7_5c9lzeXdRaqkV=w510-h337-no)

Xem video tại [đây](https://youtu.be/Np8gBKUTXxs)

Done! Bạn đã biết cách sử dụng Umbraco rồi đấy.

### Kết

Tuy là Umbraco dễ những cũng còn khá nhiều thứ mới lạ cần tìm hiểu. Hy vọng qua bài viết bạn đã có được 1 cái nhìn tổng quan về umbraco và cách thức sử dụng document type. Mình sẽ còn tiếp tục trong những bài viết sau, hy vọng mọi người đón đọc.

Xem toàn bộ playlist full-SD :v không che tại đây https://www.youtube.com/watch?v=kii_qA-U9uc&list=PLGQv5Xhv0tdpnP2tb9zEowleMmUCRKnBY