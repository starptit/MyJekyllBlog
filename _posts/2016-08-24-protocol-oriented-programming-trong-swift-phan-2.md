---
id: 1443
title: Protocol-Oriented Programming trong Swift (phần 2)
date: 2016-08-24T09:15:22+00:00
author: starptit
layout: post
guid: https://devislifeblog.wordpress.com/?p=320
permalink: /2016/08/protocol-oriented-programming-trong-swift-phan-2/
categories:
  - Uncategorized
---
(If you are looking for English version, here you go: <a href="https://medium.com/@starptit/an-example-of-protocol-oriented-programming-in-swift-4c87804d4bd9#.c22prdn0v" target="_blank">POP English</a>)

Trong phần 2, mình sẽ trình bày cách sử dụng Protocol-Oriented Programming kết hợp với Struct để giải quyết một số vấn đề của Class đã trình bày trước đó.

&#8211;> Mục tiêu của phần này sẽ là:

3. HOW CAN WE USE POP OVER OOP IN SWIFT?

<p style="padding-left:30px;">
  a. Implicit Sharing Data:
</p>

<p style="padding-left:30px;">
  Bản chất của Implicit Sharing Data chính là dựa trên cơ chế truyền tham chiếu của Class, do đó, chúng ta chỉ cần thay thế Class bằng Struct:
</p>

<p style="padding-left:30px;">
  <img class=" size-full wp-image-384 aligncenter" src="https://devislifeblog.files.wordpress.com/2016/08/screen-shot-2016-08-24-at-3-07-21-pm.png" alt="Screen Shot 2016-08-24 at 3.07.21 PM.png" width="367" height="238" srcset="http://swiftyvn.com/wp-content/uploads/2016/08/screen-shot-2016-08-24-at-3-07-21-pm.png 367w, http://swiftyvn.com/wp-content/uploads/2016/08/screen-shot-2016-08-24-at-3-07-21-pm-300x195.png 300w" sizes="(max-width: 367px) 100vw, 367px" />
</p>

<!--more-->

<img class=" size-full wp-image-388 aligncenter" src="https://devislifeblog.files.wordpress.com/2016/08/screen-shot-2016-08-24-at-3-07-49-pm.png" alt="Screen Shot 2016-08-24 at 3.07.49 PM" width="617" height="140" srcset="http://swiftyvn.com/wp-content/uploads/2016/08/screen-shot-2016-08-24-at-3-07-49-pm.png 617w, http://swiftyvn.com/wp-content/uploads/2016/08/screen-shot-2016-08-24-at-3-07-49-pm-300x68.png 300w" sizes="(max-width: 617px) 100vw, 617px" /> 

<p style="padding-left:30px;">
  ==> Kết quả:
</p>

<p style="padding-left:30px;">
  <img class=" size-full wp-image-393 aligncenter" src="https://devislifeblog.files.wordpress.com/2016/08/screen-shot-2016-08-24-at-3-11-20-pm.png" alt="Screen Shot 2016-08-24 at 3.11.20 PM.png" width="366" height="73" srcset="http://swiftyvn.com/wp-content/uploads/2016/08/screen-shot-2016-08-24-at-3-11-20-pm.png 366w, http://swiftyvn.com/wp-content/uploads/2016/08/screen-shot-2016-08-24-at-3-11-20-pm-300x60.png 300w" sizes="(max-width: 366px) 100vw, 366px" />
</p>

<p style="padding-left:30px;">
  Vì Parrot là Struct , mà Struct lại là Value Type, tức là nó truyền tham trị, copy và release, nên khi chúng ta thay đổi giá trị của hisParrot, thực chất là chúng ta chỉ thay đổi giá trị của một bản sao chép. Chúng ta có thể tưởng tượng như thế này: chúng ta có 1 con vẹt (myParrot) tên là Jack, trường hợp truyền tham chiếu ở Class, tương đương với việc chúng ta đưa Jack cho một người bạn khác, người bạn đó đặt lại tên Jack lại thành Sparrow &#8211;> con Jack của chúng ta bây giờ thành Sparrow. Ngược lại, trường hợp của Struct, chúng ta nhân bản Jack, và đưa con vẹt nhân bản đó cho anh bạn, anh bạn cũng đặt lại tên cho nó là Sparrow, tuy nhiên, con vẹt mà anh bạn đặt tên là con vẹt nhân bản, chúng ta vẫn giữ con Jack. Tức là bây giờ sẽ có 2 con vẹt, 1 con Jack (ta giữ), và 1 con Sparrow (anh bạn giữ).
</p>

<p style="padding-left:30px;">
  Một thay đổi nhỏ chuyển từ Class sang Struct &#8211;> không còn memory leak, không còn implicit sharing data, không còn deadlock,&#8230;. Cool, phải không. Rõ ràng, tâp trung vào Class (tức hướng về OOP) không phải là ý kiến hay.
</p>

<img class="aligncenter size-full wp-image-402" src="https://devislifeblog.files.wordpress.com/2016/08/r5btd.jpg" alt="r5btd.jpg" width="386" height="250" srcset="http://swiftyvn.com/wp-content/uploads/2016/08/r5btd.jpg 386w, http://swiftyvn.com/wp-content/uploads/2016/08/r5btd-300x194.jpg 300w" sizes="(max-width: 386px) 100vw, 386px" /> 

<p style="padding-left:30px;">
  b. Inheritance problem:
</p>

<p style="padding-left:30px;">
  Quay trở lại bài toán về chú chim cánh cụt ở phần trước: chim cánh cụt không có lông vũ, cũng như không thể bay, nhưng chú vẫn thuộc họ nhà chim.
</p>

<p style="padding-left:30px;">
  Vậy giờ làm thế nào nhỉ ?
</p>

  * Decouple ra 2 class: Bird và PenguinBird &#8211;> Không ổn, sai hẳn nguyên lý của OOP.
  * Tạo một Protocol mới chỉ hành động Fly &#8211;> Phải viết lại code rất nhiều.
  * Đặt lại static func fly() &#8211;> trong trường hợp có nhiều Object thì sao? Rồi còn vấn đề về Concurrency, multi threading,&#8230;

<p style="padding-left:30px;">
  Welcome to Protocol-Oriented Programming:
</p>

<img class=" size-full wp-image-309 aligncenter" src="https://devislifeblog.files.wordpress.com/2016/08/screen-shot-2016-08-22-at-3-18-43-pm.png" alt="Screen Shot 2016-08-22 at 3.18.43 PM.png" width="422" height="372" /> 

<p style="padding-left:30px;">
  Mình chuyển Bird từ Class sang Protocol, và decouple phương thức fly() và thuộc tính feather thành 2 protocol : Flyable (dành cho những loài chim có thể bay), Featherable (dành cho những loài chim có lông vũ). Nhờ vào tính năng Extension (Category trong Objective-C), mình có thể tùy biến mở rộng Protocol đã khai báo trước đó, các struct không cần phải implement lại phương thức fly() và thuộc tính feather nếu không thực sự cần thiết. &#8211;> 3 vấn đề trên của Class đã được giải quyết.
</p>

<p style="padding-left:30px;">
  Chú chim cánh cụt giờ có thể vui vẻ được rồi :D.
</p>

<img class=" size-full wp-image-412 aligncenter" src="https://devislifeblog.files.wordpress.com/2016/08/happy-feet.jpg" alt="happy-feet.jpg" width="500" height="499" srcset="http://swiftyvn.com/wp-content/uploads/2016/08/happy-feet.jpg 500w, http://swiftyvn.com/wp-content/uploads/2016/08/happy-feet-150x150.jpg 150w, http://swiftyvn.com/wp-content/uploads/2016/08/happy-feet-300x300.jpg 300w, http://swiftyvn.com/wp-content/uploads/2016/08/happy-feet-100x100.jpg 100w" sizes="(max-width: 500px) 100vw, 500px" /> 

<img class="aligncenter size-full wp-image-314" src="https://devislifeblog.files.wordpress.com/2016/08/screen-shot-2016-08-22-at-3-32-30-pm.png" alt="Screen Shot 2016-08-22 at 3.32.30 PM.png" width="598" height="424" /> 

<p style="padding-left:30px;">
  ( Giả sử giờ có thêm chim đà điểu, một loài thuộc họ nhà chim, có lông vũ, nhưng không thể bay &#8211;> cách phân tách ra các protocol đã phát huy được tác dụng)
</p>

<p style="padding-left:30px;">
  c. Classes Relationship Problem (hay Type Relationship Lost):
</p>

<p style="padding-left:30px;">
  Vấn đề của lost relationship của classes đó là việc chúng ta liên tục phải ép kiểu (casting) lại các subclass mỗi khi chúng override. Để giải quyết vấn đề này, chúng ta có thể chuyển đổi từ việc sử dụng Class sang Struct và Protocol:
</p>

<img class="aligncenter size-full wp-image-428" src="https://devislifeblog.files.wordpress.com/2016/08/screen-shot-2016-08-24-at-3-45-48-pm.png" alt="Screen Shot 2016-08-24 at 3.45.48 PM.png" width="421" height="354" srcset="http://swiftyvn.com/wp-content/uploads/2016/08/screen-shot-2016-08-24-at-3-45-48-pm.png 421w, http://swiftyvn.com/wp-content/uploads/2016/08/screen-shot-2016-08-24-at-3-45-48-pm-300x252.png 300w" sizes="(max-width: 421px) 100vw, 421px" /> 

<p style="padding-left:30px;">
  AbstractComparation từ Class đã chuyển thành Protocol, và các subclass của nó được chuyển thành struct. Việc chuyển từ Class thành Protocol giúp cho AbstractComparation linh hoạt hơn, như ví dụ trong hình là việc inject Dependency vào, nhờ đó, mình không còn cần phải ép kiểu nữa.
</p>

4. Summary:

Dựa vào những điểm yếu đó, Apple đã tập trung phát triển Protocol và Struct, cuối cùng đưa ra khái niệm mới về Protocol-Oriented Programming. Ví dụ điển hình nhất trong số những vấn đề mình đã trình bày chính là ví dụ về giải quyết vấn đề kế thừa trong Class (ví dụ về Chim cánh cụt). Hiển nhiên cái này chỉ là nguyên lý, còn áp dụng hay không thì phụ thuộc vào bài toán và kinh nghiệm của các bạn. Hi vọng bài viết đã giúp các bạn có được cái nhìn về POP trong lập trình Swift.

Một số link tham khảo:

  * Link gốc của Apple: <a href="https://developer.apple.com/videos/play/wwdc2015/408/" target="_blank">https://developer.apple.com/videos/play/wwdc2015/408/</a>
  * Ứng dụng POP: <a href="https://realm.io/news/appbuilders-natasha-muraschev-practical-protocol-oriented-programming/" target="_blank">https://realm.io/news/appbuilders-natasha-muraschev-practical-protocol-oriented-programming/</a>
  * Link Raywenderlich: <a href="https://www.raywenderlich.com/109156/introducing-protocol-oriented-programming-in-swift-2" target="_blank">https://www.raywenderlich.com/109156/introducing-protocol-oriented-programming-in-swift-2</a>
  * Link đưa ra lập luận phản bác, do chính cộng tác viên với tác giả của Apple đưa ra: <a href="http://blog.metaobject.com/2015/06/protocol-oriented-programming-is-object.html" target="_blank">http://blog.metaobject.com/2015/06/protocol-oriented-programming-is-object.html</a>. Link này viết rất hay, tuy khó hiểu, nhưng nếu ngồi phân tích lại thì lập luận mà tác giả đưa ra cực kì sắc sảo.

Hết.

&nbsp;