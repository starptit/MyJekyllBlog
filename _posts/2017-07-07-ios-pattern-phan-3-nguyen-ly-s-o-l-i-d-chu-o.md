---
id: 958
title: 'iOS pattern: Phần 3: Nguyên lý S.O.L.I.D (chữ O )'
date: 2017-07-07T10:45:43+00:00
author: starptit
layout: post
guid: https://devislifeblog.wordpress.com/?p=958
permalink: /2017/07/ios-pattern-phan-3-nguyen-ly-s-o-l-i-d-chu-o/
categories:
  - Uncategorized
---
Ở phần trước, chúng ta đã tìm hiểu về nguyên lý đầu tiên &#8211; SRP, một nguyên lý khá dễ hiểu nhưng không dễ để thực hiện. Trong bài viết này, mình sẽ tiếp tục giới thiệu về nguyên lý thứ 2, nguyên lý Open-Closed Principle (OCP &#8211; chữ O). Tuy nhiên trước khi đi vào chi tiết, mình cũng xin được nhắc lại cho các bạn, rằng S.O.L.I.D nằm ở mức nguyên lý (principle), chính vì vậy bạn không bắt buộc phải tuân thủ hay áp dụng nó triệt để. Tuy nhiên, những kiến thức về S.O.L.I.D rất hữu ích, nó là nền tảng cho việc clean code, củng cố thêm những hiểu biết về hệ thống kiến trúc, cách tổ chức, phân bố class, source code, module,.. trong một project. Hơn nữa, S.O.L.I.D và design pattern luôn là một trong những câu hỏi phổ biến của các nhà tuyển dụng, biết S.O.L.I.D không giúp bạn từ Junior thành Senior, nhưng nếu bạn là Senior, bắt buộc bạn phải có hiểu biết về S.O.L.I.D.

<!--more-->

  1. ## _**Tại sao lại cần OCP ?**_

OCP bắt nguồn từ thực tế trong ngành phần mềm, source code rất thường xuyên hoặc có khả năng được sử dụng lại, đồng nghĩa với việc code đó được nhiều developer khác động chạm vào. Hệ quả là làm giảm tính đúng đắn khi chạy, và gây khó khăn trong việc maintain. Đây là một điều tối kỵ trong việc lập trình. Thế nhưng, cũng rất vô lý nếu developer phải lập trình lại những phần việc mà người khác đã làm và hoàn thiện, một sự lãng phí thời gian và công sức. Vậy đâu là giải pháp cho vấn đề này, đó chính là lúc chúng ta cần tìm hiểu và áp dụng OCP.

<h2 style="text-align:justify;">
  <em><strong>2. OCP là gì?</strong></em>
</h2>

> _software entities (classes, modules, functions, etc.) should be open for extension, but closed for modification._

Nội dung nguyên lý được chia rõ ràng thành 2 phần liên quan chặt chẽ với nhau: Open và Close, vừa phải Open, nhưng cũng bắt buộc phải Close.

_a) Open for extension:_

Các class, module, function của chúng ta cần phải đảm bảo rằng chúng có khả năng mở rộng. Mở rộng ở đây là người khác có khả năng sử dụng lại phần việc bạn đã làm vào bài toán của họ, đồng thời họ có thể thêm thắt các tính năng khác mà không làm ảnh hưởng đến những gì bạn đã viết.

_b) Close for modification:_

Các class, module, function cần phải thiết kế để ngăn chặn khả năng sửa đổi.

&#8211;> Software entities cần phải đảm bảo khả năng mở rộng từ người khác, nhưng đồng thời cũng phải bảo vệ việc chỉnh sửa từ họ.

Tổng quan của nguyên lý này đặt ra cho bạn một phương pháp: trước khi bắt tay vào thiết kế và lập trình một class, module, function,.. nào đó, bạn hãy tự hỏi bản thân rằng nếu người khác muốn sử dụng, thì họ có thể sử dụng được hay không, và nếu sử dụng thì họ có phải chỉnh sửa gì bên trong cái phần mà mình đã viết không?

Nếu bạn cảm thấy chưa thật sự hiểu, hãy nghĩ đến các third party library, hoặc các plugin khác, chúng là ví dụ tiêu biểu và điển hình của việc Open-Closed một module: bạn hoàn toàn có thể sử dụng, thậm chí có thể custom lại theo ý muốn của mình, mà không cần phải đọc lại hay sửa đổi lại source code cũ của họ (dĩ nhiên là trừ fix bug :))).

## _**3. iOS vốn đã support OCP:**_

Thực ra, chính bản thân Apple đã cung cấp cho chúng ta công cụ để thực hiện coding theo nguyên lý OCP này, bạn có đoán ra đó là gì không?

Chính là **Extension **&#8211; một tính năng tuyệt vời giúp các bạn có thể mở rộng các class khác mà không cần phải động chạm vào những function cũ của nó. (Trong Objective-C, nó được gọi là Category).

Ví dụ với bài toán lấy màu từ mã hexa:

<img class="aligncenter size-full wp-image-1406" src="http://206.189.90.168/wordpress/wp-content/uploads/2017/07/screen-shot-2017-07-07-at-11-13-59-am.png" alt="Screen Shot 2017-07-07 at 11.13.59 AM.png" width="435" height="329" srcset="/wp-content/uploads/2017/07/screen-shot-2017-07-07-at-11-13-59-am.png 435w, /wp-content/uploads/2017/07/screen-shot-2017-07-07-at-11-13-59-am-300x227.png 300w" sizes="(max-width: 435px) 100vw, 435px" /> 

Chúng ta đơn giản chỉ cần viết một hàm init mới cho class UIColor thông qua việc sử dụng Extension. Hiển nhiên, chúng ta không biết class UIColor được xây dựng như nào vì Apple đã giấu nó, và những phần đã giấu đó chúng ta không thể thay đổi gì được, không thể xóa, không thể viết thêm code vào bên trong (close for modification), tuy nhiên chúng ta vẫn có thể sử dụng UIColor cho mục đích của chúng ta một cách dễ dàng (open for extension).

Tuy nhiên, extension chỉ support chúng ta ở mức độ các class thôi, còn đối với các level cao hơn thì sao? Lúc này, chúng ta bắt buộc phải vận dụng tư duy khác để áp dụng thôi, hay cùng xem ví dụ ở phần sau.

## _**4. Ví dụ thực tế về OCP:**_

Hãy nhìn vào ứng dụng Instagram nổi tiếng, chúng ta có thể thấy trong màn hình upload ảnh, ta có thêm chức năng khác đó là chức năng chia sẻ bức ảnh này lên các mạng xã hội khác (theo ảnh dưới là Facebook, Twitter, Tumblr,&#8230;).

<img class="  wp-image-1419 aligncenter" src="http://206.189.90.168/wordpress/wp-content/uploads/2017/07/img_0757.png" alt="IMG_0757.PNG" width="411" height="731" srcset="/wp-content/uploads/2017/07/img_0757.png 1242w, /wp-content/uploads/2017/07/img_0757-169x300.png 169w, /wp-content/uploads/2017/07/img_0757-768x1365.png 768w, /wp-content/uploads/2017/07/img_0757-576x1024.png 576w" sizes="(max-width: 411px) 100vw, 411px" /> 

_a) Nông dân chân chính:_

<img class="aligncenter size-full wp-image-1438" src="http://206.189.90.168/wordpress/wp-content/uploads/2017/07/screen-shot-2017-07-07-at-2-33-55-pm.png" alt="Screen Shot 2017-07-07 at 2.33.55 PM.png" width="575" height="459" srcset="/wp-content/uploads/2017/07/screen-shot-2017-07-07-at-2-33-55-pm.png 575w, /wp-content/uploads/2017/07/screen-shot-2017-07-07-at-2-33-55-pm-300x239.png 300w" sizes="(max-width: 575px) 100vw, 575px" /> 

Nếu bạn là nông dân chân chính, bạn sẽ code theo kiểu như trên, viết 4 hàm riêng để xử lý việc share đến các mạng xã hội (SNS &#8211; Social Networks Systems: mạng xã hội) khác nhau, và bước cuối cùng, sẽ lặp trong list để tìm ra các mạng xã hội mà người dùng đã chọn và gọi hàm share tương ứng.

Mọi thứ đều hoàn hảo, hoạt động trơn tru, chẳng có lỗi lầm gì, thật tuyệt vời !!!

Thế nhưng, câu chuyện mới chỉ bắt đầu, vào một ngày đẹp trời, sếp yêu cầu chúng ta support thêm mạng xã hội Weibo của Trung Quốc. Chúng ta buộc phải chọc lại ViewController, viết thêm hàm shareWeibo, và sửa lại hàm shareImage. Việc sửa lại code và viết thêm này khiến chúng ta phải test lại ViewController trên, và đồng thời cũng phải test lại hàm shareImage, rất tốn thời gian, chưa kể đây còn là code của chúng ta, nếu như đây là code của người khác (như 1 ông đã nghỉ việc rồi) thì sao?

<img class="  wp-image-1462 aligncenter" src="http://206.189.90.168/wordpress/wp-content/uploads/2017/07/screen-shot-2017-07-07-at-3-31-53-pm.png?w=1092" alt="Screen Shot 2017-07-07 at 3.31.53 PM.png" width="439" height="275" srcset="/wp-content/uploads/2017/07/screen-shot-2017-07-07-at-3-31-53-pm.png 868w, /wp-content/uploads/2017/07/screen-shot-2017-07-07-at-3-31-53-pm-300x188.png 300w, /wp-content/uploads/2017/07/screen-shot-2017-07-07-at-3-31-53-pm-768x481.png 768w" sizes="(max-width: 439px) 100vw, 439px" /> 

&#8211;> Đây chính là lúc bộc lộ điểm yếu code nông dân: code không mở rộng được, và cũng buộc phải chọc vào sửa mỗi khi có yêu cầu thay đổi, kéo theo một đống hệ lụy: deadline, nhiều bugs, tốn thời gian sửa, thời gian test, ảnh hưởng đến các chức năng khác ,&#8230;.

Vậy thì phải làm thê nào???

_b) Nông dân biết dùng máy cày:_

Nếu chúng ta nhìn lại bài toán, việc chúng ta share đến Facebook, Twitter, Tumblr,&#8230; không quan trọng, việc này được gọi chung là Share SNS, chính vì vậy, chúng ta có thể vận dụng tính đa hình và tính kế thừa trong OOP để giải quyết bài toán này:

<img class="  wp-image-1476 aligncenter" src="http://206.189.90.168/wordpress/wp-content/uploads/2017/07/screen-shot-2017-07-07-at-3-55-19-pm.png" alt="Screen Shot 2017-07-07 at 3.55.19 PM.png" width="426" height="311" srcset="/wp-content/uploads/2017/07/screen-shot-2017-07-07-at-3-55-19-pm.png 886w, /wp-content/uploads/2017/07/screen-shot-2017-07-07-at-3-55-19-pm-300x219.png 300w, /wp-content/uploads/2017/07/screen-shot-2017-07-07-at-3-55-19-pm-768x562.png 768w" sizes="(max-width: 426px) 100vw, 426px" /> 

Chúng ta tạo các class khác nhau và cho chúng kế thừa từ một class cha, lúc này danh sách các mạng xã hội mà chúng ta đã chọn để chiasẻ sẽ có dạng như sau:

<img class="aligncenter size-full wp-image-1482" src="http://206.189.90.168/wordpress/wp-content/uploads/2017/07/screen-shot-2017-07-07-at-5-08-21-pm.png" alt="Screen Shot 2017-07-07 at 5.08.21 PM.png" width="1034" height="62" srcset="/wp-content/uploads/2017/07/screen-shot-2017-07-07-at-5-08-21-pm.png 1034w, /wp-content/uploads/2017/07/screen-shot-2017-07-07-at-5-08-21-pm-300x18.png 300w, /wp-content/uploads/2017/07/screen-shot-2017-07-07-at-5-08-21-pm-768x46.png 768w, /wp-content/uploads/2017/07/screen-shot-2017-07-07-at-5-08-21-pm-1024x61.png 1024w" sizes="(max-width: 1034px) 100vw, 1034px" /> 

Và hàm shareImage trong ViewController lúc này trở thành:

<img class="aligncenter size-full wp-image-1485" src="http://206.189.90.168/wordpress/wp-content/uploads/2017/07/screen-shot-2017-07-07-at-5-09-27-pm.png" alt="Screen Shot 2017-07-07 at 5.09.27 PM.png" width="1008" height="252" srcset="/wp-content/uploads/2017/07/screen-shot-2017-07-07-at-5-09-27-pm.png 1008w, /wp-content/uploads/2017/07/screen-shot-2017-07-07-at-5-09-27-pm-300x75.png 300w, /wp-content/uploads/2017/07/screen-shot-2017-07-07-at-5-09-27-pm-768x192.png 768w" sizes="(max-width: 1008px) 100vw, 1008px" /> 

&#8211;> Lợi ích của nó là gì so với cách cũ?

Quay lại với ví dụ đã bộc lộc điểm yếu của cách code nông dân chân chính: bây giờ sếp yêu cầu ta thêm thêm chức năng chia sẻ cho Weibo (Trung Quốc) và LineMessenger (Nhật), ta chỉ việc viết thêm các class mới như sau:

<img class="  wp-image-1493 aligncenter" src="http://206.189.90.168/wordpress/wp-content/uploads/2017/07/screen-shot-2017-07-07-at-5-15-44-pm.png" alt="Screen Shot 2017-07-07 at 5.15.44 PM.png" width="523" height="305" srcset="/wp-content/uploads/2017/07/screen-shot-2017-07-07-at-5-15-44-pm.png 876w, /wp-content/uploads/2017/07/screen-shot-2017-07-07-at-5-15-44-pm-300x175.png 300w, /wp-content/uploads/2017/07/screen-shot-2017-07-07-at-5-15-44-pm-768x447.png 768w" sizes="(max-width: 523px) 100vw, 523px" /> 

Và hàm shareImage trong ViewController lúc này thì sao:

<img class="aligncenter size-full wp-image-1485" src="http://206.189.90.168/wordpress/wp-content/uploads/2017/07/screen-shot-2017-07-07-at-5-09-27-pm.png" alt="Screen Shot 2017-07-07 at 5.09.27 PM.png" width="1008" height="252" srcset="/wp-content/uploads/2017/07/screen-shot-2017-07-07-at-5-09-27-pm.png 1008w, /wp-content/uploads/2017/07/screen-shot-2017-07-07-at-5-09-27-pm-300x75.png 300w, /wp-content/uploads/2017/07/screen-shot-2017-07-07-at-5-09-27-pm-768x192.png 768w" sizes="(max-width: 1008px) 100vw, 1008px" /> 

Ta có thể thấy rằng nó không hề thay đổi gì hết, đồng nghĩa với việc chúng ta không cần phải sửa hay động chạm gì vào nó &#8211;> không phải test, không phải debug, không phải tốn thời gian (close for modification). Trong khi đó, mục tiêu là ghép thêm tính năng share weibo và line messenger vẫn có thể thực hiện được dễ dàng (open for extension).

## _**5. Tổng kết:**_

Nguyên lý OCP này rất dễ nhớ, chỉ bao gồm 2 phần liên quan chặt chẽ, đó là open for extension, và close for modification. Tuy nhiên, cũng như các nguyên lý S.O.L.I.D khác, OCP khá trừu tượng và chung chung, hiểu được thì rất dễ, nhưng áp dụng được nó thì không phải là vấn đề đơn giản. Các bạn cần nhớ cách mình trình bày ở đây chỉ là một trong những cách code tuân thủ theo OCP, bạn đừng có ghi nhớ dập khuôn, hay áp dụng bừa bãi.

&nbsp;