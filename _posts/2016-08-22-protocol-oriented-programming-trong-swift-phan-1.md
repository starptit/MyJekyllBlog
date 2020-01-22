---
id: 1442
title: Protocol-Oriented Programming trong Swift (Phần 1)
date: 2016-08-22T09:39:17+00:00
author: starptit
# layout: post
guid: https://devislifeblog.wordpress.com/?p=217
permalink: /2016/08/protocol-oriented-programming-trong-swift-phan-1/
tags: [Uncategorized, Swift]
---

(If you are looking for English version, here you go: <a href="https://medium.com/@starptit/an-example-of-protocol-oriented-programming-in-swift-4c87804d4bd9#.c22prdn0v" target="_blank">POP English</a>)

<del></del><del></del>Lập trình hướng đối tượng (OOP &#8211; Object Oriented Programming): Ok Done.

<img class=" size-full wp-image-229 aligncenter" src="https://devislifeblog.files.wordpress.com/2016/08/oop-meme.jpg" alt="oop-meme.jpg" width="400" height="330" srcset="/wp-content/uploads/2016/08/oop-meme.jpg 400w, /wp-content/uploads/2016/08/oop-meme-300x248.jpg 300w" sizes="(max-width: 400px) 100vw, 400px" />

Lập trình hướng Protocol (POP &#8211; Protocol Oriented Programming): Dafuq ????

<!--more-->

<img class=" size-full wp-image-223 aligncenter" src="https://devislifeblog.files.wordpress.com/2016/08/d52f9ca95731da7aab0b7c704df9154b32d08d4f6d87b25a848ed2df9386451e.jpg" alt="d52f9ca95731da7aab0b7c704df9154b32d08d4f6d87b25a848ed2df9386451e" width="620" height="455" srcset="/wp-content/uploads/2016/08/d52f9ca95731da7aab0b7c704df9154b32d08d4f6d87b25a848ed2df9386451e.jpg 620w, /wp-content/uploads/2016/08/d52f9ca95731da7aab0b7c704df9154b32d08d4f6d87b25a848ed2df9386451e-300x220.jpg 300w" sizes="(max-width: 620px) 100vw, 620px" />

##### <span style="color:#800000;"><em>// Protocol: từ này mình không biết dịch thế nào cho hợp lý : giao thức, giao tác, &#8230; nghe nó không tròn ý lắm, nên mình xin đặt tên theo nguyên bản. (Protocol này tương tự như Interface của Java và C#)</em></span>

Thuật ngữ Protocol-Oriented Programming (POP) được giới thiệu lần đầu tại hội nghị lập trình viên thường niên của Apple &#8211; WWDC 2015, với bản cập nhật Swift 2.0. Tại đây, Apple đã gọi ngôn ngữ của mình (Swift) là POP, chứ không phải là OOP như một số ngôn ngữ bậc cao khác : Java, Python, C#, C++,&#8230;

&#8212;> Protocol-Oriented Programming là cái quái gì ?

<p style="padding-left:30px;">
  1. What the Hell is POP?
</p>

<p style="padding-left:30px;">
  Nếu bạn đã làm quen với OOP rồi thì khi so sánh với POP, bạn sẽ thấy nhiều điểm tương đồng. Hãy nghĩ một chút về OOP, khi bạn giải quyết vấn đề bằng OOP, bạn sẽ suy nghĩ hướng giải quyết bài toán thông qua các Class và Object (instance của Class). Với POP, bạn thay vì suy nghĩ dưới góc độ của Class, bạn sẽ chuyển sang tập trung vào các Protocol ( lý do sẽ được giải thích sau). Xu hướng lập trình Swift hiện đại là cố gắng sử dụng POP kết hợp với Struct, thay vì sử dụng Class. Protocol linh hoạt hơn Class; instance của Struct được cấp phát trên Stack, còn instance của Class được cấp phát trên Heap nên phương pháp này thực thi tốt hơn. Tặng bạn câu note của Apple tại WWDC:
</p>

<p style="padding-left:30px;">
  &#8220;THINK ABOUT PROTOCOL FIRST&#8221;
</p>

<p style="padding-left:30px;">
  &#8211;> POP là phương pháp lập trình thiết kế và làm việc ưu tiên với các Protocol, thay vì Class như OOP.
</p>

<p style="padding-left:30px;">
  2. Dude, Why we need to use POP?
</p>

<p style="text-align:left;padding-left:30px;">
  POP được đưa ra để thay thế OOP, hiển nhiên POP phải có ưu điểm gì đó vượt trội hơn, hay nói cách khác OOP phải có điểm hạn chế gì thì Apple mới quyết định thay thế nó chứ.
</p>

<p style="text-align:left;padding-left:30px;">
  Những việc mà Class làm được, thì Struct và Enum đều có thể làm được, như: tính đóng gói (encapsulation), đa hình (polymorp), kế thừa (inheritance),&#8230;
</p>

<p style="text-align:left;padding-left:30px;">
  ==> OOP làm được gì, thì POP cũng có thể làm được việc đó.
</p>

<p style="text-align:left;padding-left:30px;">
  Nói về điểm yếu của Class và OOP, hãy thử xem xét một số ví dụ sau:
</p>

<p style="text-align:left;padding-left:60px;">
  a. Implicit Sharing Data (Chia sẻ dữ liệu ngầm)
</p>

<p style="padding-left:60px;">
  Trong ngôn ngữ Swift, Class là Reference Type, còn Struct là Values Type. Việc chúng ta truyền instance của Class (Object), thực chất là chúng ta truyền Reference (tham chiếu) của nó. Giả sử mình có một Class thể hiện họ nhà Chim sau:
</p>

<img class="aligncenter size-full wp-image-329" src="https://devislifeblog.files.wordpress.com/2016/08/screen-shot-2016-08-24-at-11-26-00-am.png" alt="Screen Shot 2016-08-24 at 11.26.00 AM.png" width="383" height="212" />

<p style="padding-left:60px;">
  Mình tạo 1 instance của Bird, và tạo thêm một reference mới của nó, thông qua 2 biến &#8220;myParrot&#8221; và &#8220;hisParrot&#8221;. Thử xem reference tác động như thế nào nhé:
</p>

<p style="padding-left:30px;">
  <img class="aligncenter size-full wp-image-337" src="https://devislifeblog.files.wordpress.com/2016/08/screen-shot-2016-08-24-at-11-30-02-am.png" alt="Screen Shot 2016-08-24 at 11.30.02 AM.png" width="644" height="136" />
</p>

<p style="padding-left:60px;">
  Kết quả:
</p>

<img class=" size-full wp-image-340 aligncenter" src="https://devislifeblog.files.wordpress.com/2016/08/screen-shot-2016-08-24-at-11-34-39-am.png" alt="Screen Shot 2016-08-24 at 11.34.39 AM.png" width="299" height="63" />

<p style="padding-left:60px;">
  ==> Khi hisParrot thay đổi &#8220;name&#8221; của nó, thì đồng thời myParrot cũng thay đổi theo, do cả 2 cùng tham chiếu đến 1 địa chỉ. Vấn đề này gọi là &#8220;Implicit Sharing Data&#8221;.
</p>

<p style="padding-left:60px;">
  Implicit Sharing Data quan trọng và cần được chú ý đối với các bài toán đa tham chiếu, và đa luồng. Trong xử lý đa luồng, bài toán khó nhằn bậc nhất chính là phải xử lý đồng thời (concurrency). Implicit Sharing Data rất dễ gây ra các lỗi như giá trị nhảy lung tung (do nhiều luồng cùng thay đổi), Deadlock (do việc chờ đợi quyền thay đổi vùng tham chiếu),&#8230;<img class="aligncenter size-full wp-image-361" src="https://devislifeblog.files.wordpress.com/2016/08/65068231.jpg" alt="65068231.jpg" width="250" height="250" srcset="/wp-content/uploads/2016/08/65068231.jpg 250w, /wp-content/uploads/2016/08/65068231-150x150.jpg 150w, /wp-content/uploads/2016/08/65068231-100x100.jpg 100w" sizes="(max-width: 250px) 100vw, 250px" />
</p>

<p style="text-align:left;padding-left:60px;">
  b. Inheritance problem (vấn đề về tính kế thừa):
</p>

<p style="text-align:left;padding-left:60px;">
  <img class="alignnone size-full wp-image-288 aligncenter" src="https://devislifeblog.files.wordpress.com/2016/08/screen-shot-2016-08-22-at-2-45-02-pm.png" alt="Screen Shot 2016-08-22 at 2.45.02 PM.png" width="597" height="504" srcset="/wp-content/uploads/2016/08/screen-shot-2016-08-22-at-2-45-02-pm.png 597w, /wp-content/uploads/2016/08/screen-shot-2016-08-22-at-2-45-02-pm-300x253.png 300w" sizes="(max-width: 597px) 100vw, 597px" />
</p>

<p style="text-align:left;padding-left:60px;">
  Ta có Class cha là Bird, và các subclass kế thừa từ nó là Parrot và Eagle. Ok, các class con này không có vấn đề gì hết, thế nhưng giả sử ta có trường hợp sau:
</p>

<p style="text-align:left;padding-left:60px;">
  <img class=" size-full wp-image-292 aligncenter" src="https://devislifeblog.files.wordpress.com/2016/08/screen-shot-2016-08-22-at-2-48-29-pm.png" alt="Screen Shot 2016-08-22 at 2.48.29 PM.png" width="435" height="178" srcset="/wp-content/uploads/2016/08/screen-shot-2016-08-22-at-2-48-29-pm.png 435w, /wp-content/uploads/2016/08/screen-shot-2016-08-22-at-2-48-29-pm-300x123.png 300w" sizes="(max-width: 435px) 100vw, 435px" />
</p>

<p style="text-align:left;padding-left:60px;">
  Bây giờ ta có một class con khác, là class Penguin, Penguin rõ ràng cũng là một loài chim, thế nhưng nó lại không có lông vũ, và cũng không thể bay.
</p>

<p style="text-align:left;padding-left:30px;">
  <img class="aligncenter size-full wp-image-298" src="https://devislifeblog.files.wordpress.com/2016/08/123.png" alt="123.png" width="241" height="358" srcset="/wp-content/uploads/2016/08/123.png 241w, /wp-content/uploads/2016/08/123-202x300.png 202w" sizes="(max-width: 241px) 100vw, 241px" />
</p>

<p style="padding-left:60px;">
  c. Classes Relationship Problem (vấn đề về mối quan hệ giữa Các Class):
</p>

<p style="padding-left:60px;">
  Giả sử mình có một Class như sau:
</p>

<p style="padding-left:60px;">
  <img class=" size-full wp-image-370 aligncenter" src="https://devislifeblog.files.wordpress.com/2016/08/screen-shot-2016-08-24-at-2-08-07-pm.png" alt="Screen Shot 2016-08-24 at 2.08.07 PM.png" width="455" height="121" srcset="/wp-content/uploads/2016/08/screen-shot-2016-08-24-at-2-08-07-pm.png 455w, /wp-content/uploads/2016/08/screen-shot-2016-08-24-at-2-08-07-pm-300x80.png 300w" sizes="(max-width: 455px) 100vw, 455px" />
</p>

<p style="padding-left:60px;">
  <img class="aligncenter size-full wp-image-374" src="https://devislifeblog.files.wordpress.com/2016/08/screen-shot-2016-08-24-at-2-12-59-pm1.png" alt="Screen Shot 2016-08-24 at 2.12.59 PM.png" width="533" height="271" srcset="/wp-content/uploads/2016/08/screen-shot-2016-08-24-at-2-12-59-pm1.png 533w, /wp-content/uploads/2016/08/screen-shot-2016-08-24-at-2-12-59-pm1-300x153.png 300w" sizes="(max-width: 533px) 100vw, 533px" />
</p>

<p style="padding-left:60px;">
  Class Number và Class Text là 2 class con kế thừa từ Class này, tuy nhiên khi mình override lại hàm isGreaterThan từ class cha của nó, một vấn đề nảy sinh: mình muốn so sánh property value của nó, để quyết định kết quả trả lại, thế nhưng, vì tham số mình truyền vào có kiểu là kiểu của Class cha (AbstractComparation), nên mình buộc phải ép kiểu để so sánh. Điều này khá bất tiện, như bạn thấy, trong hình mình có 2 class con, mình phải ép kiểu 2 lần, nếu sau này mở rộng ra hàng chục hàng trăm class con, thì có nghĩa mình cũng phải ép kiểu hàng chục hàng trăm lần.
</p>

<p style="padding-left:60px;">
  Apple gọi vấn đề này là Type Relationship Lost.
</p>

Ở trên mình đã trình bày 3 vấn đề về điểm yếu khi sử dụng Class (OOP) trong Swift. Tại phần sau mình sẽ đưa ra cách giải quyết những vấn đề trên bằng POP và Struct.

Hết phần 1. [Link phần 2](https://devislifeblog.wordpress.com/2016/08/24/protocol-oriented-programming-trong-swift-phan-2/)


{% include disqus_comments.html %}