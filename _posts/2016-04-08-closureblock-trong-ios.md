---
id: 85
title: Closure/Block trong iOS
date: 2016-04-08T13:49:56+00:00
author: starptit
# layout: post
guid: https://devislifeblog.wordpress.com/?p=85
permalink: /2016/04/closureblock-trong-ios/
geo_public:
  - "0"
  - "0"
tags: [Uncategorized, Swift]
---

Closure là một functional tuyệt vời mà Swift cung cấp cho lập trình viên, thật ra Closure không phải điều đặc biệt chỉ có trên Swift, các ngôn ngữ khác đều có closure, tuy nhiên được gọi bằng cái tên khác do nhà phát triển ngôn ngữ nghĩ ra mà thôi, ví dụ: closure tương ứng với block trong Objective-C, hoặc là lambda trong Java, delegates trong C# (trong JavaScript cũng gọi là Anonymous Function).

Bài viết dưới đây, mình sẽ giới thiệu về Closure theo cách nhìn nhận của bản thân mình, mình sẽ tập trung vào trả lời các câu hỏi sau cho các bạn dễ hình dung:

- Closure là cái gì?
- Tại sao phải dùng Closure? Vai trò của nó là gì?
- Sử dụng Closure như thế nào?

<!--more-->

1. Closure là gì?

Closure là một tập các đoạn code logic được đặt cùng nhau trong một khối (giống với 1 hàm (function/method)), nhờ vào đó nó có thể được dùng để &#8220;pass around&#8221; ( cái này mình không dịch, các bạn có thể hiểu nó có thể dược dùng như một variable, hoặc truyền như một paramter, hay có thể là giá trị trả về của một function chẳng hạn).

Nói vậy thì hơi chung chung nhỉ, không sao, cứ nhớ cái quan trọng nhất của nó là &#8220;pass around&#8221; đi, rồi mình sẽ giải thích mục tiêu của Closure sau.

2. Tại sao phải dùng Closure? Vai trò của nó là gì?

Nếu như chỉ nói như ở trên thì nó có khác gì mấy với function đâu, cũng là một đống code nhét vào 1 khối, rồi thực hiện mỗi khi nó được gọi, vậy sinh ra cái Closure này làm cái quái gì chứ, tự dưng phải học đau cả đầu.

Không, sự thực không như vậy, hãy sử dụng tư duy trừu tượng để tưởng tượng như sau, bạn có kiểu Int, là mộp tập hợp một integer, kiểu String là tập hợp string, và bạn có thể gán chúng vào một biến, truyền làm parameters,&#8230; thì Closure cũng như vậy, nó là một tập hợp logic code, có thể gán vào một biến, truyền làm param mà mình đã nói ở trên. Mặt khác, bên trong Closure là một tập hợp dòng code, chính vì vậy, bạn có thể gọi nó ra để thực hiện như một hàm, và điều khiển luồng theo yêu cầu một cách thuận tiện và dễ dàng. Ví dụ:

<img class="alignnone size-full wp-image-121" src="https://devislifeblog.files.wordpress.com/2016/04/screen-shot-2016-04-08-at-2-51-12-pm.png" alt="Screen Shot 2016-04-08 at 2.51.12 PM.png" width="966" height="388" srcset="/wp-content/uploads/2016/04/screen-shot-2016-04-08-at-2-51-12-pm.png 966w, /wp-content/uploads/2016/04/screen-shot-2016-04-08-at-2-51-12-pm-300x120.png 300w, /wp-content/uploads/2016/04/screen-shot-2016-04-08-at-2-51-12-pm-768x308.png 768w" sizes="(max-width: 966px) 100vw, 966px" />

Ở trên mình khai báo một Closure, mình đặt tên nó là closure1, bạn khoan nhìn vào cách mình khai báo, hãy nhìn xuống phía dưới: mình có khai báo thêm một biến nữa, đặt tên là variable, và bạn thấy đó, mình hoàn toàn có thể gán variable = closure1. Tiếp đến, mình tiến hành gọi nó như là gọi hàm luôn closure1(), điều này tương ứng với khối lệnh bên trong closure1 được nạp để thực thi, ở đây như bạn thấy là in ra dòng &#8220;Hello i&#8217;m using closure to say hello with you&#8221;. Và bạn thấy dòng chữ đó được in ra ở góc phải kia rồi phải không. Vậy đấy, nó có thể gọi để thực hiện như một function, lại còn có thể gán và tùy biến như một kiểu, một biến luôn chứ, quá tiện phải không :D.

Closure thuận tiện như vậy, nên được sử dụng cực kì rộng rãi, closure thường xuyên được sử dụng để CALL BACK. Đúng vậy, chính vì sự linh hoạt có thể được truyền qua truyền lại, kết hợp với khả năng có thể thực thi lệnh bất cứ khi nào gọi của mình, mà Closure có thể được dùng để call back (gọi lại). Closure hoàn toàn có thể sử dụng các property của class hiện tại, tức là nó hoàn toàn có khả năng gán, thay đổi giá trị, hoặc thực hiện logic nào đó một cách tự nhiên, chính vì vậy khi kết hợp với khả năng call back của mình, closure trở nên cực kì quan trọng. Khả năng call back là như thế nào?. Xem hình sau:<img class="alignnone size-full wp-image-131" src="https://devislifeblog.files.wordpress.com/2016/04/screen-shot-2016-04-08-at-3-08-23-pm.png" alt="Screen Shot 2016-04-08 at 3.08.23 PM.png" width="833" height="296" srcset="/wp-content/uploads/2016/04/screen-shot-2016-04-08-at-3-08-23-pm.png 833w, /wp-content/uploads/2016/04/screen-shot-2016-04-08-at-3-08-23-pm-300x107.png 300w, /wp-content/uploads/2016/04/screen-shot-2016-04-08-at-3-08-23-pm-768x273.png 768w" sizes="(max-width: 833px) 100vw, 833px" />

Mình khai báo một closure là callBackClosure. Mình có một hàm tên là testFunct(), parameter của nó tên là handler truyền vào là cũng là một closure. Trong hàm testFunct(), mình in ra một dòng, tiếp đến mình tiến hành gọi handler ( nó là closure, nên nó gọi được như là một hàm mà). Cuối cùng, hàm testFunct() sẽ được gọi ở hàm main của mình, mình truyền callBackClosure vào làm parameter cho hàm testFunct(), cuối cùng là build và chạy thôi. Oh yeah, kết quả hiển thị kìa, bạn hiểu nó chứ ?? Ok, Mình giải nghĩa nhé, khi hàm testFunct được gọi thực hiện, nó sẽ thực hiện tuần tự từ trên xuống dưới, và vì mình in dòng &#8220;Yeah right&#8230;&#8221; ra trước, nên nó sẽ được hiển thị trước. Sau khi nó in ra dòng đó rồi thì sao? Nó sẽ gọi thực hiện cái code bên trong parameter handler của nó. Và param đó là cái gì ? Chính là callBackClosure mà mình truyền vào, đồng nghĩa với dòng lệnh bên trong closure đó được thực hiện.

Bạn đã thấy tính call back của nó chưa? Thật ra ví dụ này sẽ dễ hiểu và hình dung hơn, nếu mình đặt nó ở 2 class khác nhau, hay trong iOS là 2 viewController khác nhau.

Bản chất của cái callback được thực hiện chính là nhờ vào khả năng execute code mỗi lần được gọi của closure. Giả sử, bạn có 2 class riêng biệt, class 1 có define closure, class 2 gọi closure đó, và ngay khi class 2 gọi, đoạn code trong closure được thực hiện tức thì, bạn hoàn toàn có thể xử lý, debug khối lệnh của closure này ngay tại thời điểm đó.

Chính nhờ tính callback này mà Closure có thể sử dụng thay thế delegate ( đọc bài delegate để hiểu delegate là cái gì nhé) trong một số trường hợp, thật ra là thay thế ở cái khoản bắt sự kiện mà thôi, còn thay thế cả một delegate pattern (protocol) thì không thể.

3. Sử dụng Closure thế nào:

Bạn nào học C# mà biết thằng Delegates thì sẽ hình dung Closure dễ dàng hơn, hoặc học JavaScript mà biết closure native của nó thì lại càng tiện. Thôi không ba hoa nữa:

<img class="alignnone size-full wp-image-155" src="https://devislifeblog.files.wordpress.com/2016/04/screen-shot-2016-04-08-at-3-53-01-pm.png" alt="Screen Shot 2016-04-08 at 3.53.01 PM.png" width="1206" height="531" srcset="/wp-content/uploads/2016/04/screen-shot-2016-04-08-at-3-53-01-pm.png 1206w, /wp-content/uploads/2016/04/screen-shot-2016-04-08-at-3-53-01-pm-300x132.png 300w, /wp-content/uploads/2016/04/screen-shot-2016-04-08-at-3-53-01-pm-768x338.png 768w, /wp-content/uploads/2016/04/screen-shot-2016-04-08-at-3-53-01-pm-1024x451.png 1024w" sizes="(max-width: 1206px) 100vw, 1206px" />

<img class="alignnone size-full wp-image-153" src="https://devislifeblog.files.wordpress.com/2016/04/screen-shot-2016-04-08-at-3-52-06-pm.png" alt="Screen Shot 2016-04-08 at 3.52.06 PM.png" width="1025" height="241" srcset="/wp-content/uploads/2016/04/screen-shot-2016-04-08-at-3-52-06-pm.png 1025w, /wp-content/uploads/2016/04/screen-shot-2016-04-08-at-3-52-06-pm-300x71.png 300w, /wp-content/uploads/2016/04/screen-shot-2016-04-08-at-3-52-06-pm-768x181.png 768w, /wp-content/uploads/2016/04/screen-shot-2016-04-08-at-3-52-06-pm-1024x241.png 1024w" sizes="(max-width: 1025px) 100vw, 1025px" />

Bonus :)))

<img class="alignnone size-full wp-image-191" src="https://devislifeblog.files.wordpress.com/2016/04/screen-shot-2016-04-06-at-17-35-58.png" alt="Screen Shot 2016-04-06 at 17.35.58.png" width="1426" height="756" />

Swift được sử dụng rộng rãi trong các thư viện của Swift, vì việc gọi hàm hay sử dụng delegate trong một số trường hợp sẽ khá rối code và rắc rối để follow theo luồng xử lý của nó. Ví dụ khi tương tác với Server API, ở các version trước của iOS sử dụng NSUrlConnection, và theo đó bạn phải implement một đống delegate kèm theo. Thế nhưng ở iOS 8 trở đi, Apple đã thay thế hoàn toàn bằng NSURLSession với thực hiện callback hoàn toàn bằng closure:

<img class="alignnone size-full wp-image-160" src="https://devislifeblog.files.wordpress.com/2016/04/screen-shot-2016-04-08-at-4-02-32-pm.png" alt="Screen Shot 2016-04-08 at 4.02.32 PM.png" width="785" height="238" />

<img class="alignnone size-full wp-image-161" src="https://devislifeblog.files.wordpress.com/2016/04/screen-shot-2016-04-08-at-4-04-39-pm.png" alt="Screen Shot 2016-04-08 at 4.04.39 PM.png" width="799" height="199" srcset="/wp-content/uploads/2016/04/screen-shot-2016-04-08-at-4-04-39-pm.png 799w, /wp-content/uploads/2016/04/screen-shot-2016-04-08-at-4-04-39-pm-300x75.png 300w, /wp-content/uploads/2016/04/screen-shot-2016-04-08-at-4-04-39-pm-768x191.png 768w" sizes="(max-width: 799px) 100vw, 799px" />

Hoặc ví dụ đơn giản nhất về ứng dụng và sử dụng closure trong Swift chính là việc Apple đã vận dụng chúng trong filter và xử lý các Array của mình.

<img class="alignnone size-full wp-image-166" src="https://devislifeblog.files.wordpress.com/2016/04/screen-shot-2016-04-08-at-4-14-42-pm.png" alt="Screen Shot 2016-04-08 at 4.14.42 PM.png" width="820" height="381" />

4. Sử dụng closure để thay thế delegate:

Closure hoàn toàn có thể sử dụng để bắt sự kiện (send message) giữa 2 View Controller nhờ vào khả năng call back đã nói ở trên. Xem xét ví dụ sau:

<img class="alignnone size-large wp-image-179" src="https://devislifeblog.files.wordpress.com/2016/04/screen-shot-2016-04-08-at-20-32-31.png?w=700" alt="Screen Shot 2016-04-08 at 20.32.31" width="700" height="475" srcset="/wp-content/uploads/2016/04/screen-shot-2016-04-08-at-20-32-31.png 1950w, /wp-content/uploads/2016/04/screen-shot-2016-04-08-at-20-32-31-300x204.png 300w, /wp-content/uploads/2016/04/screen-shot-2016-04-08-at-20-32-31-768x521.png 768w, /wp-content/uploads/2016/04/screen-shot-2016-04-08-at-20-32-31-1024x695.png 1024w" sizes="(max-width: 700px) 100vw, 700px" />

Mình có 2 ViewController, đặt tên là ViewController và NextViewController.

-Tại ViewController: mình có 1 nút, khi click vào sẽ push sang NextViewController.

-Tại NextViewController: mình cũng có 1 nút, khi click vào thì ViewController cũng biết sự kiện này, và thực hiện ngay lập tức.

Kịch bản này thông thường sẽ dùng delegate, nhưng hôm nay mình muốn dùng Closure để thử nghiệm. Vậy cách dùng thế nào?

Tại ViewController:

<img class="alignnone size-large wp-image-181" src="https://devislifeblog.files.wordpress.com/2016/04/screen-shot-2016-04-08-at-20-36-13.png?w=700" alt="Screen Shot 2016-04-08 at 20.36.13" width="700" height="207" srcset="/wp-content/uploads/2016/04/screen-shot-2016-04-08-at-20-36-13.png 1530w, /wp-content/uploads/2016/04/screen-shot-2016-04-08-at-20-36-13-300x89.png 300w, /wp-content/uploads/2016/04/screen-shot-2016-04-08-at-20-36-13-768x227.png 768w, /wp-content/uploads/2016/04/screen-shot-2016-04-08-at-20-36-13-1024x303.png 1024w" sizes="(max-width: 700px) 100vw, 700px" />

handleClick là 1 Closure, mình định nghĩa nó giống 1 biến, được đặt tại NextViewController, đồng thời mình viết code thực thi bên trong của nó là dòng &#8220;I&#8217;m called whenever you click at NextView&#8221;.

Tại NextViewController:

<img class="alignnone size-large wp-image-182" src="https://devislifeblog.files.wordpress.com/2016/04/screen-shot-2016-04-08-at-20-36-25.png?w=700" alt="Screen Shot 2016-04-08 at 20.36.25" width="700" height="226" srcset="/wp-content/uploads/2016/04/screen-shot-2016-04-08-at-20-36-25.png 996w, /wp-content/uploads/2016/04/screen-shot-2016-04-08-at-20-36-25-300x97.png 300w, /wp-content/uploads/2016/04/screen-shot-2016-04-08-at-20-36-25-768x248.png 768w" sizes="(max-width: 700px) 100vw, 700px" />

Mình khai báo 1 Closure là handleClick, bản chất là () -> (), tức là nhận vào void và trả về void. Kế đến, mình thực hiện gọi closure này mỗi khi click vào nút.

Và đây là kết quả thực hiện mỗi lần mình click vào cái nút ở NextViewController.

<img class="alignnone size-large wp-image-183" src="https://devislifeblog.files.wordpress.com/2016/04/screen-shot-2016-04-08-at-20-40-24.png?w=700" alt="Screen Shot 2016-04-08 at 20.40.24" width="700" height="342" srcset="/wp-content/uploads/2016/04/screen-shot-2016-04-08-at-20-40-24.png 1036w, /wp-content/uploads/2016/04/screen-shot-2016-04-08-at-20-40-24-300x147.png 300w, /wp-content/uploads/2016/04/screen-shot-2016-04-08-at-20-40-24-768x375.png 768w, /wp-content/uploads/2016/04/screen-shot-2016-04-08-at-20-40-24-1024x500.png 1024w" sizes="(max-width: 700px) 100vw, 700px" />

Mình sẽ giải nghĩa hoạt động của nó, khi bạn click vào nút ở NextViewController, đồng thời bạn sẽ gọi để execute cái closure handleClick, vậy những dòng lệnh để thực thi nó nằm ở đâu? Không phải chính là đoạn print() ở hàm prepareSegue trong ViewController trước hay sao? Như vậy, closure sẽ thực thi đoạn code đó, và vì closure hoàn toàn có thể sử dụng các variable hay property của class ViewController, thế nên bạn có thể custom chúng theo logic mong muốn &#8211;> đây chính là call back mà mình đã nói.

Nếu bạn tinh ý, bạn sẽ thấy, cái ví dụ về NSURLConnection và NSURLSession kia, thực chất chính là ví dụ về delegate và closure thay thế delegate, và bạn hãy tư duy mở rộng nó ra với toàn bộ các closure được tích hợp sẵn trong SDK của Apple nhé :D.

Ok, vậy là mình đã xong những khái niệm cơ bản về Closure, hi vọng blog này giúp cho các bạn hiểu rõ hơn về chúng, bạn chỉ cần nhớ 3 vấn đề cốt lõi mình đặt ra ở đầu blog là đủ.

&nbsp;
