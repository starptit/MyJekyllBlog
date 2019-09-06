---
id: 616
title: "iOS pattern: Phần 2: Nguyên lý S.O.L.I.D (chữ S )"
date: 2017-01-20T10:05:07+00:00
author: starptit
# layout: post
guid: https://devislifeblog.wordpress.com/?p=616
permalink: /2017/01/ios-pattern-phan-2-nguyen-ly-s-o-l-i-d-chu-s/
tags: [Uncategorized, Swift]
---

Nguyên lý S.O.L.I.D (hay Uncle Bob) là một nguyên lý cực kì phổ biến trong ngành công nghệ phần mềm, có thể nói là must-be-known bởi mọi lập trình viên. Nếu như bạn đã đọc phần tổng quan trước, đoạn mà mình đã đặt ra một số tiêu chí quan trọng khi thiết kế code, thì có thể nói SOLID sẽ giúp code của các bạn đáp ứng được hầu hết các tiêu chí mà mình đặt ra. Mặt khác, vì tính phổ biến của mình, SOLID rất hay được đề cập trong quá trình phỏng vấn xin việc ở các công ty, đặc biệt là trong ngành công nghiệp outsource ở Việt Nam. SOLID rất quan trọng, áp dụng vào thực tế hiệu quả, nhưng cũng khá khó nhai và khó để áp dụng đúng. Tuy nhiên, các bạn cần nhớ nó là <span style="color:#ff0000;"><strong>NGUYÊN LÝ</strong></span>, tức là không hề bắt buộc, bạn cần phải tỉnh táo khi áp dụng, miễn sao nó đáp ứng được bộ tiêu chí mà mình đã nêu ra là được. SOLID cũng có mặt trái, nó khiến code của bạn dài hơn (đi ngược lại tiêu chí write less), luồng xử lý loằng ngoằng hơn, có thể gây khó khăn khi tìm vết và debug. Nhìn về tổng thể, lợi ích mà SOLID đem lại lớn hơn rất nhiều so với mặt trái của nó, do đó SOLID tồn tại vững chãi và đi sâu vào mind-set của các lập trình viên. Các design pattern được suy luận và sinh ra từ nguyên lý SOLID. Chúng ta có thể nhìn nhận thế này:

<!--more-->

Các tiêu chí mình nêu ra ở phần 1 &#8211;> SOLID &#8211;> Design pattern.

Trong series này, mình sẽ cố gắng trình bày SOLID theo cách nhìn khoa học và dễ hiểu và gần gũi với các dự án lập trình iOS.

## <span style="color:#993366;"><em><strong>1. What is SOLID (SOLID là gì):</strong></em></span>

S.O.L.I.D gồm 5 nguyên lý, 5 chữ cái đầu của chúng ghép lại thành cụm từ trên. Chú ý: bạn nào khá tiếng Anh thì đừng dọc đoạn dịch nghĩa của mình mà hãy nhớ theo tiếng Anh, còn bạn nào không tốt về ngoại ngữ thì có thể tham khảo cách dịch của mình để có cái nhìn trước về 5 nguyên lý này:

- **[S]**ingle Responsibility Principle (SRP): Nguyên lý đơn chức năng
- **[O]**pen Close Principle (OCP): Nguyên lý mở rộng và che giấu.
- **[L]**iskov Subsitution Principle (LSP): Nguyên lý thay thế Liskov
- **[I]**nterface Segregation Principle (ISP): Nguyên lý phân tách các &#8220;Interface&#8221;
- **[D]**ependancy Inversion Principle (DIP): Nguyên lý đảo ngược &#8220;Dependancy&#8221;

5 nguyên lý này sẽ bám chặt vào tính các đặc trưng và trừu tượng của phong cách lập trình hướng đối tượng (OOP). Với mục tiêu là ứng dụng trong lập trình iOS, mình sẽ cố gắng trình bày chúng dễ hiểu và dễ gần với iOS nhất, tuy nhiên bạn cũng cần phải nhớ, chúng khá là trừu tượng và rắc rối, bạn cần phải luyện tập và tốt nhất là nên thử tự ứng dụng trong các dự án nhỏ nhỏ của mình.

Dài dòng đủ rồi, sau đây chúng ta sẽ cùng tìm hiểu nguyên lý đầu tiên: Single Responsibility Principle.

## <span style="color:#993366;"><em><strong>2. Single Responsibility Principle (SRP) là cái quái gì?</strong></em></span>

Để cho thuận tiện, mình sẽ gọi tắt nguyên lý này là SRP. Trước khi chúng ta đi vào chi tiết, hãy nhìn lại cái tên của nó và cùng giải nghĩa: Single là một, là đơn. Responsibility nghĩa là trách nhiệm, nhiệm vụ. Gộp lại, chúng ta có thể hình dung trong đầu, nó nói về vấn đề đơn trách nhiệm, ở trên mình có dịch nó là đơn chức năng &#8211;> các bạn đừng nên dịch theo nghĩa sát của nó, hãy mở rộng ra một chút và hãy tạm suy nghĩ nó theo từ &#8220;chức năng&#8221;.

Và nội dung của nguyên lý:

> A class should have only one reason to change.

Tạm dịch: Lớp (class) chỉ nên có duy nhất một lý do để thay đổi.

Cụm từ &#8220;reason to change&#8221; (lý do để thay đổi) thực sự rất trừu tượng, chỉ riêng 2 từ reason (lý do) và change (thay đổi) đã mang hàm nghĩa bao quát rồi. Nhưng bạn hãy thử ngẫm nó với cái trách nhiệm / chức năng mà ta đã phân tích từ tên gọi của nó, đơn chức năng và lý do thay đổi ??? Ta có thể phát biểu lại: mỗi class chỉ nên có duy nhất một chức năng ?? Như vậy nếu ta suy luận theo logic phủ định, lý do thay đổi ở đây có liên quan đa trách nhiệm.

&#8211;> Khi thiết kế class hoặc module hoặc function, chúng ta nên ghi nhớ rằng chúng chỉ nên có một và chỉ một nhiệm vụ mà thôi. Lý do là gì ? Mời các bạn đọc tiếp.

## <span style="color:#993366;"><em><strong>3. Tại sao lại cần nguyên lý SRP ?</strong></em></span>

Để trả lời cho câu hỏi tại sao, ta hãy hỏi ngược lại vấn đề, nếu như ta không áp dụng SRP vào trong code thì chuyện gì sẽ xảy ra?

Chúng ta đều biết ngành công nghiệp là ngành rất dễ thay đổi, thay đổi về công nghệ, thay đổi cấu trúc, thay đổi yêu cầu, hiểu nhầm business, phân tích nghiệp vụ sai,&#8230; tất cả những sự thay đổi đó đều dẫn đến việc chúng ta phải chỉnh sửa lại code cũ của mình. Những function nhỏ thì không sao, nhưng với các function và module lớn, như là xương sống của dự án mà thay đổi thì hiển nhiên sẽ gây tác động to lớn đến hệ thống.

Như mình đã nói ở phần trước, khi thay đổi kị nhất là gặp phải code kết dính và không rõ ràng, nếu bạn thiết kế 1 class đảm nhận quá nhiều chức năng, thuật ngữ gọi là GOD class thì khả năng chúng kết dính với nhau khá cao, và khi có bất kì thay đổi nào liên quan đến một chức năng nhỏ trong đó, bạn sẽ phải test lại toàn bộ cái class đó, rất bất tiện.

<img class="aligncenter size-full wp-image-930" src="https://devislifeblog.files.wordpress.com/2017/01/2.png" alt="2.png" width="340" height="338" srcset="/wp-content/uploads/2017/01/2.png 340w, /wp-content/uploads/2017/01/2-150x150.png 150w, /wp-content/uploads/2017/01/2-300x298.png 300w, /wp-content/uploads/2017/01/2-100x100.png 100w" sizes="(max-width: 340px) 100vw, 340px" />

Hình ảnh hộp dụng cụ đa năng trên là ví dụ kinh điển cho trường hợp vi phạm SRP ( nó là cái GOD class mà mình nói ở trên): nó tuy tiện dụng nhưng lại rất cồng kềnh, giả sử bây giờ một con dao cạo mà bị hỏng &#8211;> bạn phải mở cả hộp ra, sửa lại con dao đó mà không biết chắc rằng sửa xong rồi có ảnh hưởng đến mấy cái cờ lê, tuốc lơ vít bên cạnh hay không?

Hãy nhìn vào ví dụ thực tế này:

<img class="  wp-image-860 aligncenter" src="https://devislifeblog.files.wordpress.com/2017/01/screen-shot-2017-01-20-at-14-39-31.png" alt="Screen Shot 2017-01-20 at 14.39.31.png" width="276" height="145" srcset="/wp-content/uploads/2017/01/screen-shot-2017-01-20-at-14-39-31.png 358w, /wp-content/uploads/2017/01/screen-shot-2017-01-20-at-14-39-31-300x158.png 300w" sizes="(max-width: 276px) 100vw, 276px" />

Thầy u mua cho chiếc xe máy để đi học, nên nhiệm vụ chính của cái xe là để đi học. Mọi chuyện vẫn ổn, cho đến khi có gấu, cái xe giờ lại phải thêm nhiệm vụ là chở gấu

<img class="  wp-image-865 aligncenter" src="https://devislifeblog.files.wordpress.com/2017/01/screen-shot-2017-01-20-at-14-44-26.png" alt="Screen Shot 2017-01-20 at 14.44.26.png" width="268" height="146" srcset="/wp-content/uploads/2017/01/screen-shot-2017-01-20-at-14-44-26.png 388w, /wp-content/uploads/2017/01/screen-shot-2017-01-20-at-14-44-26-300x164.png 300w" sizes="(max-width: 268px) 100vw, 268px" />

Xe giờ lại phải dán thêm mấy cái đề can, hoặc sửa lại bộ đèn nháy, độ lại bô,&#8230; thế nên bạn phải kiểm tra lại xem xe này còn đi học được không, sợ bô to vào trường người ta đuổi. Lúc này vẫn ổn, có gấu thì lúc nào chả ổn :)))).

Có gấu thì tốn tiền, mà sinh viên thì lấy đâu ra tiền, thế là lại phải làm thêm, sẵn có cái xe máy, đăng kí làm shipper.

<img class="aligncenter  wp-image-944" src="https://devislifeblog.files.wordpress.com/2017/01/screen-shot-2017-01-20-at-14-47-50.png" alt="Screen Shot 2017-01-20 at 14.47.50.png" width="293" height="175" srcset="/wp-content/uploads/2017/01/screen-shot-2017-01-20-at-14-47-50.png 450w, /wp-content/uploads/2017/01/screen-shot-2017-01-20-at-14-47-50-300x179.png 300w" sizes="(max-width: 293px) 100vw, 293px" />

<img class="  wp-image-870 aligncenter" src="https://devislifeblog.files.wordpress.com/2017/01/img0110a-2.jpg" alt="IMG0110A-2.jpg" width="451" height="338" srcset="/wp-content/uploads/2017/01/img0110a-2.jpg 640w, /wp-content/uploads/2017/01/img0110a-2-300x225.jpg 300w" sizes="(max-width: 451px) 100vw, 451px" />

Hí hửng lắp xong cái thùng để đi ship, thế rồi test chở gấu đi chơi &#8211;> gấu chê cái thùng xấu xí &#8211;> chia tay. Test tiếp đi học, cái thùng xấu xí nhìn dị hợm, mấy anh bảo vệ không cho vào trường &#8211;> R.I.P.

## <span style="color:#993366;"><em><strong>4. Áp dụng nguyên lý SRP thế nào ?</strong></em></span>

Câu hỏi đặt ra, chúng ta nên áp dụng phương pháp này như thế nào. Dựa vào lý thuyết, công việc của chúng ta là chia nhỏ các class / module / function ra thành các thành phần nhỏ hơn, tùy thuộc vào một mục đích nào đó (được gọi là trách nhiệm hay chức năng). Việc chia nhỏ như thế này hoàn toàn dễ hiểu, có thể coi như việc áp dụng tư duy chia để trị (devide and conquer) của ngành IT vào. Chia nhỏ sẽ giúp chúng ta dễ quản lý hơn, vì mỗi phần đều có chức năng và nhiệm vụ riêng của nó, thế nên chúng ta chỉ cần một bản thiết kế class đủ chuẩn, là chúng ta hoàn toàn có nắm bắt được hệ thống dễ dàng. Hơn nữa việc sửa đổi sẽ dễ dàng hơn, vì thay ở chức năng nào thì sửa chức năng đó và test cũng ở đó.

SRP dễ hiểu nhưng khó áp dụng, vì tính trừu tượng của nó, đặc biệt là cụm từ &#8220;reason to change&#8221; (lý do thay đổi). Việc mình áp nó vào chức năng hay trách nhiệm chỉ đơn giản là để cho dễ hiểu và dễ hình dung hơn thôi, chứ kỳ thực khi thiết kế class bạn phải xem xét đến các nguyên nhân có thể khiến nó thay đổi. Việc nghĩ được các trường hợp này cực kỳ khó, ai làm tester rồi thì sẽ hiểu.

Kỳ thực trên thực tế, chúng ta vẫn có những class vi phạm nguyên lý này trắng trợn, đó là các class áp dụng singleton (một design pattern), hay là các class Utils,&#8230; Đặc điểm chung của chúng chính là chúng khó thay đổi, hoặc thay đổi cũng không ảnh hưởng đến các module function khác. Đây chính là lúc các bạn không nên áp dụng SRP, trong các class mà chẳng bao giờ thay đổi, hoặc là ít thay đổi và không liên quan gì nhau.

Lời khuyên của mình là các bạn chưa thử bao giờ thì cứ nên áp dụng, áp dụng càng triệt để càng tốt, dần dần qua các dự án, bạn sẽ tự đúc rút được kinh nghiệm áp dụng nó cho riêng mình.

## <span style="color:#993366;"><em><strong>5. Ví dụ về SRP trong iOS:</strong></em></span>

Lý thuyết dài dòng đủ rồi, các bạn hãy quan sát ví dụ thực tế dưới đây để hiểu rõ hơn phần lý thuyết mình đã trình bày ở bên trên: Bài toán phổ biến nhất trong lập trình mobile: giao tiếp với server, ở đây mình lấy ví dụ bằng việc gọi qua API Webservice. Ví dụ rất đơn giản: tạo request &#8211;> gọi đến server &#8211;> lấy response trả về. Hiện nay kiểu dữ liệu JSON đang khá phổ biến, thế nên có nhiều bạn xây dựng như sau:

<img class=" size-full wp-image-627 aligncenter" src="https://devislifeblog.files.wordpress.com/2017/01/screen-shot-2017-01-18-at-11-20-19-am.png" alt="Screen Shot 2017-01-18 at 11.20.19 AM.png" width="514" height="485" srcset="/wp-content/uploads/2017/01/screen-shot-2017-01-18-at-11-20-19-am.png 514w, /wp-content/uploads/2017/01/screen-shot-2017-01-18-at-11-20-19-am-300x283.png 300w" sizes="(max-width: 514px) 100vw, 514px" />

Ở hình trên mình xây dựng một request gửi đến domain http://troidat.com, có vẻ như không có gì đặc biệt đúng không ?? Nhưng bạn hãy thử nghĩ về chức năng của chúng xem, ta có thể thấy rõ ràng ViewControllerA đảm nhận 2 nhiệm vụ: xử lý UI cho View (viewDidload, viewWillAppear, viewDidAppear,&#8230;) và gửi Request đến server. Rõ ràng là nó đã vi phạm nguyên lý SRP rồi.

Ừ nhưng 2 nhiệm vụ như vậy thì sao nhỉ, chả thấy có gì đặc biệt cả, 2 logic riêng biệt, hơn nữa gửi Request đến server còn là một công việc thường xuyên được thực hiện nữa chứ, thế nên Copy paste thần chưởng được dịp phát huy công hiệu, ta sẽ copy nó sang ViewControllerB, C, D,&#8230; bất cứ ViewController nào cần gửi request.

1 tuần sau, khách hàng báo lại, hệ thống của họ cần bảo mật, họ mới bổ sung TLS và mua SSL certificate (HTTPS) rồi, và báo lại cho bạn để bạn thay đổi add thêm cái certificate đó vào. Bụng bảo dạ, cay thật, nhưng vẫn phải làm, và vì bạn không chia theo chức năng, nên cứ đoạn nào có gọi service là bạn phải mở ra mà sửa lại, ví dụ như:

<img class="aligncenter size-full wp-image-693" src="https://devislifeblog.files.wordpress.com/2017/01/screen-shot-2017-01-18-at-2-26-27-pm.png" alt="Screen Shot 2017-01-18 at 2.26.27 PM.png" width="459" height="421" srcset="/wp-content/uploads/2017/01/screen-shot-2017-01-18-at-2-26-27-pm.png 459w, /wp-content/uploads/2017/01/screen-shot-2017-01-18-at-2-26-27-pm-300x275.png 300w" sizes="(max-width: 459px) 100vw, 459px" />

1 tháng sau, anh code backend fix bug nên phải bổ sung thêm trường custom HTTP Headers vào, headers[&#8220;X-Authen-Token&#8221;] = &#8220;MariaOzawa&#8221;. Lúc này lại cay lần 2, mò lại đống code, hí húi thêm cái HTTP Headers, chỗ nào có gọi service thì lại phải mở ra sửa &#8211;> R.I.P

<img class=" size-full wp-image-707 aligncenter" src="https://devislifeblog.files.wordpress.com/2017/01/screen-shot-2017-01-18-at-2-44-58-pm.png" alt="Screen Shot 2017-01-18 at 2.44.58 PM.png" width="506" height="510" srcset="/wp-content/uploads/2017/01/screen-shot-2017-01-18-at-2-44-58-pm.png 506w, /wp-content/uploads/2017/01/screen-shot-2017-01-18-at-2-44-58-pm-150x150.png 150w, /wp-content/uploads/2017/01/screen-shot-2017-01-18-at-2-44-58-pm-298x300.png 298w, /wp-content/uploads/2017/01/screen-shot-2017-01-18-at-2-44-58-pm-100x100.png 100w" sizes="(max-width: 506px) 100vw, 506px" />

2 tuần sau, anh code backend lại nổi hứng: &#8220;em ơi thêm cho anh cái multipart data gửi lên server mình nhé, không xài 3rd server nữa&#8221;. Ok ok, mở code lần 3, lần lượt sửa các ViewControllerA,B,C,&#8230;. &#8212;> Thưa sếp, em nghỉ việc.

Rõ ràng chỉ vì 1 chức năng, sau 3 lần sửa đổi, bạn phải sửa cả tá ViewController khác cũng với số lần tương ứng. Sửa xong lại phải unit test, test xong lại chuyển sang cho team test chuyên nghiệp check lại, rất ảnh hưởng đến tiến độ công việc, thời gian dự án, và cũng khiến coder phát điên.

_**Sửa đổi theo SRP:**_

Theo như nguyên lý SRP, mỗi một class hoặc một module chỉ nên có một nhiệm vụ duy nhất, vậy nên bạn cần phải tách 2 nhiệm vụ xử lý UI và giao tiếp với Server thành 2 class khác nhau. Cái nhược điểm của cách code ban đầu chính là module của các bạn nằm rải rác trong nhiều class, khiến cho khi bạn thay đổi, bạn chỉnh sửa và test lại rất nhiều lần, rồi còn có thể nhầm lẫn trong các lần sửa, &#8230; Nếu bạn tạo 1 class riêng cho việc gọi Service, giả sử sau này có thay đổi, thì bạn chỉ cần mở và  chỉnh sửa ngay trong class này mà không làm ảnh hưởng đến các class khác. Ngoài ra, việc tiến hành unit test cũng dễ hơn, do nó chỉ đảm nhận một chức năng duy nhất.

<img class="aligncenter size-full wp-image-719" src="https://devislifeblog.files.wordpress.com/2017/01/screen-shot-2017-01-18-at-2-56-25-pm.png" alt="Screen Shot 2017-01-18 at 2.56.25 PM.png" width="465" height="378" srcset="/wp-content/uploads/2017/01/screen-shot-2017-01-18-at-2-56-25-pm.png 465w, /wp-content/uploads/2017/01/screen-shot-2017-01-18-at-2-56-25-pm-300x244.png 300w" sizes="(max-width: 465px) 100vw, 465px" />

Ở đây, mình chuyển các hàm giao tiếp với Server vào trong class ServerCommunicate, việc xử lý của các ViewController sẽ tách biệt hơn thông qua class này:

<img class="aligncenter size-full wp-image-724" src="https://devislifeblog.files.wordpress.com/2017/01/screen-shot-2017-01-18-at-3-00-39-pm.png" alt="Screen Shot 2017-01-18 at 3.00.39 PM.png" width="633" height="367" srcset="/wp-content/uploads/2017/01/screen-shot-2017-01-18-at-3-00-39-pm.png 633w, /wp-content/uploads/2017/01/screen-shot-2017-01-18-at-3-00-39-pm-300x174.png 300w" sizes="(max-width: 633px) 100vw, 633px" />

Bây giờ xét các trường hợp trên:

- Thêm SSL certificate
- Thêm HTTP Headers
- Thêm MultipartData

<img class="aligncenter size-full wp-image-731" src="https://devislifeblog.files.wordpress.com/2017/01/screen-shot-2017-01-18-at-3-06-44-pm.png" alt="Screen Shot 2017-01-18 at 3.06.44 PM.png" width="510" height="652" srcset="/wp-content/uploads/2017/01/screen-shot-2017-01-18-at-3-06-44-pm.png 510w, /wp-content/uploads/2017/01/screen-shot-2017-01-18-at-3-06-44-pm-235x300.png 235w" sizes="(max-width: 510px) 100vw, 510px" />

Class ServerCommunicate sẽ phình ra thế này, tất nhiên rồi. Nhưng các ViewController thì sao ta ?

<img class="aligncenter size-full wp-image-734" src="https://devislifeblog.files.wordpress.com/2017/01/screen-shot-2017-01-18-at-3-00-39-pm1.png" alt="Screen Shot 2017-01-18 at 3.00.39 PM.png" width="633" height="367" srcset="/wp-content/uploads/2017/01/screen-shot-2017-01-18-at-3-00-39-pm1.png 633w, /wp-content/uploads/2017/01/screen-shot-2017-01-18-at-3-00-39-pm1-300x174.png 300w" sizes="(max-width: 633px) 100vw, 633px" />

Nó vẫn y vậy, không thay đổi gì cả. Đơn giản, nó chỉ có nhiệm vụ là update các View, tôi không quan tâm các anh thêm bớt gửi nhận gì trong đoạn gửi lên server, cái tôi cần là khi tôi gọi service, các anh trả về cho tôi data để tôi update lại theo logic của mình.

&#8211;> Không cần phải sửa các ViewController này

&#8211;> Nếu muốn test thì chỉ cần test Class ServerCommunicate là đủ.

**_<span style="color:#993366;">Như vậy là xong đúng không?</span>_**

Không, chưa hẳn là xong đâu, bạn hãy nhìn Class ServerCommunicate dưới góc độ &#8220;responsibility&#8221;, class này hiện tại đang nắm giữ 2 nhiệm vụ chính:

- Xây dựng payload data, Request,&#8230; để gửi lên server
- Nhận kết quả trả về và parse sang dạng dữ liệu JSON.

&#8211;> 1 class đảm nhận 2 nhiệm vụ &#8211;> vi phạm Single Responsibility Principle.

Trên thực tế, có một số dự án bạn sẽ gặp phải tình trạng đầu voi đuôi chuột, tức là đầu vào (request) là con voi, nhưng đầu ra (response) là con chuột. Cái Class trên chỉ hoạt động đúng khi đầu vào và đầu ra là dạng JSON, thế nhưng giả sử hệ thống của họ lại yêu cầu bạn gọi đến một server khác, xài định dạng của SOAP (XML) thì sao ? Rồi còn một số trường hợp khác như là họ chỉ đổi định dạng trả về, từ JSON chuyển thành SOAP, hoặc Protobuf,&#8230;

&#8211;> bạn phải sửa lại đoạn resposne, rồi lại phải test lại cả class, test lại request,&#8230;.

&#8211;> Nên sửa lại theo SRP, tức là chia làm 2 class khác nhau, 1 class đảm nhận request và 1 class đảm nhận Response.

<img class="  wp-image-757 aligncenter" src="https://devislifeblog.files.wordpress.com/2017/01/screen-shot-2017-01-19-at-11-34-56.png?w=1150" alt="Screen Shot 2017-01-19 at 11.34.56.png" width="386" height="404" srcset="/wp-content/uploads/2017/01/screen-shot-2017-01-19-at-11-34-56.png 808w, /wp-content/uploads/2017/01/screen-shot-2017-01-19-at-11-34-56-287x300.png 287w, /wp-content/uploads/2017/01/screen-shot-2017-01-19-at-11-34-56-768x802.png 768w" sizes="(max-width: 386px) 100vw, 386px" />

Ở trên mình khai báo 1 enum để phân loại các Data Type, mình còn tạo thêm 1 class chuyên cho việc tạo dựng các request gửi lên. Hàm chung để tạo request của mình à hàm buildRequest, nó có trách nhiệm tạo request ứng với loại request mà mình đang mong muốn.

<img class=" size-full wp-image-763 aligncenter" src="https://devislifeblog.files.wordpress.com/2017/01/screen-shot-2017-01-19-at-11-42-15.png?w=792" alt="Screen Shot 2017-01-19 at 11.42.15.png" width="396" height="358" srcset="/wp-content/uploads/2017/01/screen-shot-2017-01-19-at-11-42-15.png 746w, /wp-content/uploads/2017/01/screen-shot-2017-01-19-at-11-42-15-300x271.png 300w" sizes="(max-width: 396px) 100vw, 396px" />

Tương tự với class Response, mình tách việc parse response ra riêng so với phần tạo request.

<img class="aligncenter size-full wp-image-768" src="https://devislifeblog.files.wordpress.com/2017/01/screen-shot-2017-01-19-at-11-46-52.png" alt="Screen Shot 2017-01-19 at 11.46.52.png" width="1426" height="386" srcset="/wp-content/uploads/2017/01/screen-shot-2017-01-19-at-11-46-52.png 1426w, /wp-content/uploads/2017/01/screen-shot-2017-01-19-at-11-46-52-300x81.png 300w, /wp-content/uploads/2017/01/screen-shot-2017-01-19-at-11-46-52-768x208.png 768w, /wp-content/uploads/2017/01/screen-shot-2017-01-19-at-11-46-52-1024x277.png 1024w" sizes="(max-width: 1426px) 100vw, 1426px" />

Class ServerCommunicate nếu được thiết kế theo kiểu tách rời module gửi request, và module parse response, thì sẽ có dạng như trên. Thiết kế kiểu này thì có ích lợi gì ???

- Nếu bây giờ thay đổi thêm đầu vào là một dạng Custom DataType nào đó, thì chỉ cần bổ sung ở class RequestGenerator, hoàn toàn không ảnh hưởng đến 2 class còn lại. Điều này cũng tương tự với trường hợp nếu như thay đổi ở class ResponseParse.
- Class ServerCommunicate không cần quan tâm đến Request là gì, Response như nào, cái nó quan tâm là nó cần 1 đầu vào (request) và nó sẽ trả ra 1 đầu ra (response) tương ứng. Việc xử lý đầu vào và đầu ra thế nào là nhiệm vụ của thằng khác.

Trên thực tế, việc thay đổi đầu ra đầu vào như vậy không phải lúc nào cũng xảy ra, và cũng khá hạn chế, nhất là với các dự án Outsourcing, còn làm Product thì có xác suất cao hơn. Do đó, bước chia nhỏ class ServerCommunicate đó có thể không cần thiết phải thực hiện mà vẫn đảm bảo được tính ổn định của dự án. Đây chính là tính phức tạp khi áp dụng mà mình đã nói, ranh giới giữa nên hay không nên ở đây rất mong manh.

## <span style="color:#993366;"><em><strong>6. Tổng kết:</strong></em></span>

Vậy là mình đã trình bày xong những suy nghĩ và kiến thức của bản thân về SRP, chữ S đầu tiên của SOLID. Hi vọng qua bài viết, các bạn có thể hiểu được nguyên lý này và áp dụng được nó cho dự án của các bạn, cũng như đọc hiểu được code của những người khác.

Sau đây mình xin tổng kết lại các vấn đề về SRP:

- Nó là gì: là một nguyên lý về thiết kế nhằm cải thiện chất lượng code của các bạn.
- Nó nói gì: Một class/function/module chỉ nên có duy nhất một lý do để thay đổi, hay chỉ đảm nhận duy nhất một nhiệm vụ.
- Tại sao lại cần nó: nó giúp cải thiện chất lượng code và chất lượng dự án của các bạn. Bắt nguồn từ bộ tiêu chí mình đã giới thiệu ở phần trước.
- Dùng nó như thế nào: Hãy nhìn các class/function/module của các bạn theo góc nhìn chức năng và những thay đổi có thể xảy ra. Cách tốt nhất là chia nhỏ chúng ra thành các sub class/module, và mỗi phần nhỏ đó sẽ đảm nhậm một chức năng từ tập chức năng to ban đầu.
- Chú ý:

**_&#8211;> Ưu điểm:_**

- Code sạch và rõ ràng hơn, logic cũng được thể hiện rõ hơn, vì đã được chia nhỏ ra.

- Dễ mở rộng, bảo trì code.

- Dễ dàng tái sử dụng code và giảm thiểu lỗi phát sinh.

- Dễ test hơn, vì cần phần nào thì test phần đó mà.

- Giảm tính kết dính của code.

_**&#8211;> Nhược điểm:**_

- Dễ áp dụng nhưng khó áp dụng chuẩn, vì đơn giản khái niệm chuẩn và định nghĩa để áp dụng của nó quá mơ hồ.

- Có thể khiến dự án phình to ra, vì phát sinh ra nhiều sub class và module hơn.

Bài viết đến đây là kết thúc, xin cám ơn các bạn đã theo dõi.
