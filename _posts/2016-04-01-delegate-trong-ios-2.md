---
id: 1440
title: Delegate trong iOS
date: 2016-04-01T08:38:27+00:00
author: starptit
# layout: post
guid: https://devislifeblog.wordpress.com/?p=2
permalink: /2016/04/delegate-trong-ios-2/
tags: [Uncategorized, Swift]
---

Mình để ý thấy trên các trang chia sẻ kiến thức và hướng dẫn lập trình trong iOS, có rất nhiều bạn đặt câu hỏi về cách sử dụng protocol/ delegate trong lập trình iOS (cả Objective-C và Swift). Mình không khẳng định mình hiểu biết toàn bộ về Protocol trong iOS, nhưng mình tin rằng những chia sẻ dưới đây của mình có thể giúp các bạn có cái nhìn dễ hiểu hơn đối với Protocol. Trong bài viết này, mình sẽ không đi sâu về protocol, mình sẽ chỉ trình bày cách hoạt động, ý nghĩa sử dụng, và khi nào thì nên sử dụng nó, hi vọng sau khi nắm được cơ bản, các bạn có thể tìm hiểu sâu hơn, và vận dụng được nó tốt hơn.

<!--more-->

Nếu các bạn đặt câu hỏi Protocol là cái gì và sử dụng thế nào trên các trang chia sẻ, bạn sẽ nhận được câu trả lời tựa tựa như: nó để truyền dữ liệu, nó giống interface trong Java/C#,&#8230; Nhưng là mình, thì mình xin được trả lời như sau: đối với iOS mà nói, thì protocol thường được dùng để BẮT SỰ KIỆN. Nếu các bạn hiểu sâu chắc chắn sẽ bảo mình nói sai, đúng là mình sai. Nhưng trước mắt các bạn cứ nhớ lấy 3 chữ &#8220;BẮT SỰ KIỆN&#8221; đó dùm mình.

Protocol, hay delegate là 1 pattern, nếu các bạn tìm hiểu về design pattern, các bạn sẽ tìm thấy một pattern là &#8220;Delegate pattern&#8221;. Đúng, delegate pattern chính là protocol mà chúng ta đang nói đến đó. Interface trong Java/C# là một dạng của delegate pattern đó, cho nên nói protocol trong Objective-C/Swift giống interface là đúng. Nhưng khoan nhớ về nó như là interface trong Java đi, bạn cứ nhớ dùm mình cái &#8220;BẮT SỰ KIỆN&#8221; trên kia.

Khi các bạn đọc sách hay docs trên mạng về protocol trong Objective-C/Swift, bạn sẽ thấy nó vĩ mô hơn cái mình nói rất nhiều, bởi vì Objective-C/Swift không phải chỉ sinh ra để code iOS, nó còn có thể code nhiều platform khác, đặc biệt Swift, nó có thể code backend, frontend, chính vì vậy, đối với các bạn làm dev iOS, các bạn sẽ thấy rất khó để bắt và vận dụng cái mình vừa đọc vào Application của mình. Sở dĩ sách họ viết chi tiết như vậy, bởi vì như đã nói, protocol/ delegate là cả 1 pattern mà, nó phải đáp ứng đúng theo tiêu chí của design pattern chứ, hay nói cách khác, nó cũng phải có những đặc trưng tiêu biểu giống thằng interface trong java chứ. Nhưng trước mắt, bạn đừng để ý đến nó, vì cái mình nói dưới đây, là cái cơ bản nhất khi vận dụng delegate vào trong application iOS của các bạn rồi, thế nên các cái vĩ mô kia, các bạn tìm hiểu sau nhé.

Nào, bây giờ đi vào ý nghĩa thôi, ở trên mình nói là nó dùng để bắt sự kiện phải không? Vậy nó bắt sự kiện là bắt sự kiện như thế nào. Chắc hẳn các bạn lập trình iOS đều ít nhiều phải gặp một vài trường hợp thế này: Bạn có 2 view controller (gọi là vcA và vcB nhé), khi bạn click vào một cái nút ở vcB để thực hiện logic hay tính toán gì đó chẳng hạn, và bạn muốn vcA nhận được dữ liệu hay kết quả logic mà vcB vừa làm, thì phải làm thế nào? Đúng là có rất nhiều cách để thực hiện điều này, như là singleton, biến toàn cục, hay set data vào NSUserDefaults,&#8230; nhưng cách đơn giản và phổ biến nhất, chính là sử dụng Delegate. Vậy cái bắt sự kiện mà mình nói là sao? Đó chính là sự kiện click vào cái nút ở vcB. Khi vcB click vào cái nút đó, nó sẽ gửi 1 thông điệp cho vcA, thông qua delegate, bằng cách, nó sẽ gửi cho delegate, và delegate sẽ gửi đến vcA. Bạn đã thấy nó bắt sự kiện chưa? Hãy nhìn cách mình implement nó nhé:

<img class="alignnone size-full wp-image-29" src="https://devislifeblog.files.wordpress.com/2016/04/screen-shot-2016-04-01-at-15-14-24.png" alt="Screen Shot 2016-04-01 at 15.14.24" width="1308" height="866" srcset="/wp-content/uploads/2016/04/screen-shot-2016-04-01-at-15-14-24.png 1308w, /wp-content/uploads/2016/04/screen-shot-2016-04-01-at-15-14-24-300x199.png 300w, /wp-content/uploads/2016/04/screen-shot-2016-04-01-at-15-14-24-768x508.png 768w, /wp-content/uploads/2016/04/screen-shot-2016-04-01-at-15-14-24-1024x678.png 1024w" sizes="(max-width: 1308px) 100vw, 1308px" />

1. Mình có 2 View A và View B. View A có 1 nút: PushView, khi click vào nút này sẽ chuyển sang hiển thị view B.
2. Tại View B, mình có 1 nút, &#8220;Click Me Send Delegate&#8221;, mình sẽ sử dụng Delegate để giúp view A nhận diện được khi nào cái nút trên viewB được click.

Dùng như thế nào? Dùng như sau:

Tại View B, mình khai báo Protocol, có tên là didClickOnButton:

<img class="alignnone size-full wp-image-39" src="https://devislifeblog.files.wordpress.com/2016/04/screen-shot-2016-04-01-at-15-18-46.png" alt="Screen Shot 2016-04-01 at 15.18.46.png" width="1046" height="424" srcset="/wp-content/uploads/2016/04/screen-shot-2016-04-01-at-15-18-46.png 1046w, /wp-content/uploads/2016/04/screen-shot-2016-04-01-at-15-18-46-300x122.png 300w, /wp-content/uploads/2016/04/screen-shot-2016-04-01-at-15-18-46-768x311.png 768w, /wp-content/uploads/2016/04/screen-shot-2016-04-01-at-15-18-46-1024x415.png 1024w" sizes="(max-width: 1046px) 100vw, 1046px" />

Bạn để ý cái id<didClickOnButton> delegate; kia nhé, nó chính là thằng nhận thông báo từ thằng B và gửi lại cho thằng A đó.

Ok, tại file .h của thằng view A, mình khai báo nó sẽ thực thi cái delegate didClickOnButton trên kia. Còn tại thằng file thực thi .m của view A, mình code như sau:

<img class="alignnone size-full wp-image-45" src="https://devislifeblog.files.wordpress.com/2016/04/screen-shot-2016-04-01-at-15-21-54.png" alt="Screen Shot 2016-04-01 at 15.21.54.png" width="1130" height="320" srcset="/wp-content/uploads/2016/04/screen-shot-2016-04-01-at-15-21-54.png 1130w, /wp-content/uploads/2016/04/screen-shot-2016-04-01-at-15-21-54-300x85.png 300w, /wp-content/uploads/2016/04/screen-shot-2016-04-01-at-15-21-54-768x217.png 768w, /wp-content/uploads/2016/04/screen-shot-2016-04-01-at-15-21-54-1024x290.png 1024w" sizes="(max-width: 1130px) 100vw, 1130px" />

Trước khi chuyển màn hình, mình gán thằng delegate của thằng viewB = self; Là sao nhỉ? thằng destView.delegate kia chính là thằng id<didClickOnButton> delegate; mà mình đã nói ở trên, còn thằng self ở đây là thằng didClickOnButton mà mình báo là thực thi ở file .h của thằng A. Các bạn chú ý đoạn này quan trọng lắm nhé, bạn phải gán delegate cho một đối tượng chỉ định ( ở đây là self &#8211; didClickOnButton), ý nghĩa của dòng lệnh này là giúp thằng delegate của view B biết là nó sẽ phải gửi đến thằng nào, nếu bạn bỏ nó đi, nó sẽ không bao giờ hoạt động, dĩ nhiên rồi, vì có biết gửi đến thằng nào đâu mà gửi, chẳng lẽ gửi linh tinh thì thằng OS nó chẳng đấm chết :D.

Cái thằng clickRegconize() là method thực thi của thằng protocol didClickOnButton, thằng này chính là thằng message nhận được đó.

Cuối cùng , tại hành động click của view B, mình sử dụng thằng delegate như sau:

<img class="alignnone size-full wp-image-57" src="https://devislifeblog.files.wordpress.com/2016/04/screen-shot-2016-04-01-at-15-28-03.png" alt="Screen Shot 2016-04-01 at 15.28.03.png" width="924" height="146" srcset="/wp-content/uploads/2016/04/screen-shot-2016-04-01-at-15-28-03.png 924w, /wp-content/uploads/2016/04/screen-shot-2016-04-01-at-15-28-03-300x47.png 300w, /wp-content/uploads/2016/04/screen-shot-2016-04-01-at-15-28-03-768x121.png 768w" sizes="(max-width: 924px) 100vw, 924px" />

Dòng lệnh này có ý nghĩa, khi có sự kiện click vào cái nút &#8220;Click Me Send Delegate&#8221;, thì đồng thời nó sẽ nhờ thằng delegate, gửi thông điệp qua hàm clickRegconize ( bạn chú ý nhé, clickRegconize là hàm được định nghĩa trước trong procol didClickOnButton , xem hình 1).

Và đây là kết quả mình nhận được:

<img class="alignnone size-full wp-image-67" src="https://devislifeblog.files.wordpress.com/2016/04/screen-shot-2016-04-01-at-15-33-08.png" alt="Screen Shot 2016-04-01 at 15.33.08" width="798" height="110" srcset="/wp-content/uploads/2016/04/screen-shot-2016-04-01-at-15-33-08.png 798w, /wp-content/uploads/2016/04/screen-shot-2016-04-01-at-15-33-08-300x41.png 300w, /wp-content/uploads/2016/04/screen-shot-2016-04-01-at-15-33-08-768x106.png 768w" sizes="(max-width: 798px) 100vw, 798px" />

Tada, chuỗi &#8220;Sao Vuuuuu&#8221; đã được in ra, tương ứng với hàm clickRegconize ở View A (hình 2) đã được thực hiện rồi, nghĩa là thằng view A đã nhận biết khi thằng view B click vào cái nút &#8220;Click Me Send Delegate&#8221;.

OK, ngẫm lại nhé: View B click nút &#8211;> bắt sự kiện này và gửi đến view A. Tại sao lại gửi được? Là nhờ Delegate. Gửi bằng cách nào: View b send cho delegate, delegate send cho view A.

Xong cái phần hiểu rồi, giờ là phần nhớ, nhớ thế nào cho nó dễ nhỉ? Delegate &#8211; delegation trong tiếng Anh có nghĩa là đại biểu, vậy các bạn cứ bám nghĩa này mà nhớ là đơn giản nhất. Ví dụ nhé, hôm nọ mình đọc tin, có một anh người Việt ở Nhật vi phạm luật pháp, và bên Nhật muốn thông báo cho gia đình người Việt của anh này biết tin, vậy họ làm thế nào nhỉ??? Đơn giản thôi, họ sẽ báo cho Đại Sứ Quán Việt Nam tại Nhật. Đại Sứ Quán Việt Nam sẽ gửi lại thông báo cho chính quyền nơi gia đình anh này sống, và việc tiếp theo là ở chính quyền đó. Bạn có thấy giống delegate không? Muốn thông báo sự kiện cho người khác &#8211;> nhờ anh Đại biểu ( Đại sứ Quán) để làm trung gian truyền tin. Tại sao lại cần đại biểu, vì chính quyền Việt Nam không thể xuất hiện ở Nhật được, nên buộc phải để đại biểu ở đó nhằm liên lạc. Áp dụng cho delegate? View A và view B rõ ràng là 2 view độc lập, view A không thể xuất hiện ở view B và ngược lại, vậy muốn truyền tin cho nhau thì làm thế nào? Dùng đại biểu (delegate) chứ sao :D.

Nhìn vào delegate trong các thư viện của cocoa trong iOS, với thằng UITextField, bạn có UITextFieldDelgate. Khi bạn implement nó, nó sẽ có các method nào??

<img class="alignnone size-full wp-image-75" src="https://devislifeblog.files.wordpress.com/2016/04/screen-shot-2016-04-01-at-21-01-06.png" alt="Screen Shot 2016-04-01 at 21.01.06.png" width="1552" height="398" srcset="/wp-content/uploads/2016/04/screen-shot-2016-04-01-at-21-01-06.png 1552w, /wp-content/uploads/2016/04/screen-shot-2016-04-01-at-21-01-06-300x77.png 300w, /wp-content/uploads/2016/04/screen-shot-2016-04-01-at-21-01-06-768x197.png 768w, /wp-content/uploads/2016/04/screen-shot-2016-04-01-at-21-01-06-1024x263.png 1024w" sizes="(max-width: 1552px) 100vw, 1552px" />

Nhìn kĩ nhé, đó có phải đều là các method nhằm bắt sự kiện khi bạn tương tác với textfield không? textFieldBeginEditing: bắt sự kiện khi bạn bắt đầu nhập text vào textfield. textFieldShouldClear: bắt sự kiện khi bạn xoá hết text trong textfield. textFieldShouldEndEditing: bắt sự kiện khi bạn đã hoàn thành hành động nhập text vào textField,&#8230;. Bạn thấy đó, khi bạn thao tác với UITextFiekd, UITextField sẽ gửi thông báo cho bạn là bạn vừa làm abcxyz gì đó tương ứng, thông qua delegate, và dựa vào đó bạn có thể điều chỉnh theo logic của mình.

Ví dụ khác nhé, bạn có nhớ UITableViewDelegate không? Cái hàm didSelectRowAtIndexpath của nó là gì? Không phải là bắt sự kiện khi bạn click (select) 1 cell bất kì trong tableview đó sao???

Tóm lại là sau cái bài chia sẻ này, hi vọng các bạn nắm được ý chính sau:

- Protocol: trong iOS, nó dược dùng để gửi thông điệp giữa 2 ViewController với nhau, hoặc 2 class với nhau.
- Cách hoạt động: view B cần thông báo cho view A rằng mình vừa thực hiện một hành động nào đó : viewB gửi message qua delegate (nhờ các hàm trong protocol, nên nhớ là hàm thì có parameters, nên bạn truyền dữ liệu chính là truyền qua các parameters này). Delegate nhận message rồi gửi lại cho view A. View A thực hiện logic của mình.
- Cách implement: View nào cần gửi thông báo thì view đó cần 1 biến thể hiện delegate (ở ví dụ là view B- hình 1). Trong hàm thực hiện hành động của viewB, nhờ delegate gửi message bằng cách thực hiện method khai báo ở protocol của delegate. View A implement protocol, thực thi lại method mà view B vừa gửi.

Xong rồi, hi vọng bài viết này giúp ích được cho các bạn. À mà mình nói luôn là các bạn sau khi đọc bài này, nên thử code lại, làm vài lần cho hiểu. Sau đó các bạn nên đọc thêm về protocol trong Objective-C/Swift nhé, vì bài viết của mình chỉ nhắm đến đối tượng các bạn code iOS thôi. Nếu bạn để ý kĩ thì thực ra cái bắt sự kiện này cũng giống như trên Java thôi, bạn có nhớ mấy cái ActionListener chứ??? Cái đó chính là interface đó. Rồi khi tìm hiểu sâu hơn bạn sẽ thấy cái mình vừa nói là phần nổi của protocol, sự thực thì protocol nó mạnh mẽ hơn nhiều, đặc biệt là trong Swift, và nó giống hệ interface luôn.

{% include disqus_comments.html %}