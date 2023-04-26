---
title: "Năm Mèo Nói Chuyện Clean Code: Mèo Đen Hay Mèo Trắng"
categories: coding
layout: article
tags: [coding, mindset]
---

> <span style="color:#993300">Mèo đen hay mèo trắng không quan trọng, miễn là nó bắt được chuột (Thuyết con mèo - Đặng Tiểu Bình)</span>

Dẫn luận thành

> <span style="color:#993300">Code xấu hay code đẹp không quan trọng, miễn là nó chạy được.</span>

<div style="display: flex; align-items: center; justify-content: center;">
  <img class="wp-image-1879 aligncenter" src="/assets/images/post/black_white_cats.jpeg" alt="" width="400" height="400" srcset="/assets/images/post/black_white_cats.jpeg" sizes="(max-width: 400px) 100vw, 320px" />
</div>

Khi tôi tóm tắt như vậy, chắc chắn sẽ có nhiều người phản đối, hay chê cười, vì đơn giản ai cũng hiểu là nếu đã là developer thì code smell, code spaghetti,... là một trong những tiêu chí quan trọng để phân loại level của developer. Chẳng có ông nào vỗ ngực là senior mà lại đem ra một đống sh\*t code cả. Hơn nữa, những dòng code được đo ni đóng giầy vào từng ông developer, nên nếu là một dev thực thụ, chắc chắn mọi người sẽ luôn muốn đảm bảo những dòng code của mình là clean nhất có thể. Nếu là một developer mà chấp nhận những dòng code xấu, thì chỉ có 2 trường hợp:

1. Ông là dev cùi
2. Tiêu chuẩn của ông thấp

Tôi thì không phải loại nào trong 2 loại trên, bản thân tôi cũng từng viết một số bài viết về clean code và design pattern, nên là trust me bro, tôi không phải là người dễ dãi với những dòng code. Trước đó, tôi cũng đã từng có khoảng thời gian tư duy kiểu clean code như một tôn giáo vậy, nhưng hiện tại quan điểm của tôi đã hoàn toàn thay đổi, có lẽ là nhờ vào kinh nghiệm sau một số năm làm việc trong nghề, được tiếp xúc với một số developer xịn, và nhìn nhận sản phẩm phần mềm theo nhiều góc độ khác nhau.

Clean code đối với tôi không còn là tôn giáo nữa, nó đơn giản chỉ là một khía cạnh (quan trọng) tôi để xem xét khi phát triển dự án phần mềm. Ở bài viết dưới đây, tôi sẽ cố gắng đưa ra các sự thật liên quan đến vấn đề clean code, dựa trên kinh nghiệm thực tiễn của bản thân, và những sự thật này chính là lý do khiến tôi thay đổi quan điểm của mình.

# <span style="color: #ff9900;">Fact #1: Mọi phần mềm sinh ra đều là để giải quyết vấn đề nào đó?</span>

3 chàng ngốc (3 idiots) là một bộ phim tôi yêu thích (tôi cá là nhiều bạn cũng vậy), trong đó có một phân cảnh được coi là kinh điển, đó là cảnh về "định nghĩa máy móc là gì" (what is a machine?).

Khi giáo sư hỏi Rancho (nhân vật chính) về định nghĩa máy móc, anh ta đã trả lời rằng: "Máy móc là bất kể thứ gì giúp giảm công sức của con người. Bất kể thứ gì đơn giản hoá công việc, tiết kiệm thời gian, đều là máy móc. Vào một ngày nóng nực, bấm 1 cái nút, gió thổi ra - ta có cái quạt - một dạng máy móc. Nói chuyện với bạn bè ở xa hàng dặm, ta có điện thoại di động - một loại máy móc. Từ cái bấm bút bi, cho đến cái khoá quần, tất cả đều là máy móc. Kéo lên kéo xuống chỉ qua một giây - đó là máy móc".

<iframe class="aligncenter" width="560" height="315" src="https://www.youtube.com/embed/DKzBmRRdPXo" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

Lý do tôi thích phân cảnh trên là vì nhân vật chính đã đơn giản hoá và biến máy móc về mục đích sau cùng của nó - giúp tiết kiệm công sức con người, và quan trọng là ... nó đúng.

Khi đối chiếu với ngành phần mềm, tôi tin rằng chúng ta cũng cần phải đơn giản hoá nó về bản chất mục đích người ta cần nó. Vậy bản chất mục đích đó là gì?

Giá trị cốt lõi của việc áp dụng các đột phá công nghệ, là nằm ở việc công nghệ đó đem lại lợi ích gì cho kinh doanh sản xuất, cho đời sống xã hội; cụ thể hơn, công nghệ đó giải quyết được vấn đề gì. Chẳng phải ngẫu nhiên mà người ta thường dùng cụm từ "giải pháp công nghệ", tức là bản thân nó là giải pháp (solution) cho vấn đề.

Hãy thử quan sát một số ví dụ sau:

- Để giải quyết các vấn đề về liên lạc, chúng ta xây dựng ra các ứng dụng nhắn tin tức thì (Instant Message) như Yahoo, Skype, Messenger,... Rồi sau đó để giải quyết vấn đề liên lạc phục vụ riêng cho doanh nghiệp, chúng ta lại có Slack, MS Teams,... Hay để nhắn tin private, chúng ta lại có các phần mềm như Telegram, Snapchat,...
- Để phục vụ nhu cầu kết nối, mạng xã hội ra đời, chúng ta có Facebook, Instagram, Tiktok,...
- Để giúp quản lý tài chính, chúng ta có các ứng dụng như: MoneyLover, Finance Assistant,...
- Để thúc đẩy trading cryptocurrency, chúng ta có Binance, FTX, ...
- Để giải quyết việc quản lý Kế Toán doanh nghiệp, chúng ta có Misa.
- Để giải quyết vấn đề kết nối các ngân hàng, chúng ta có OpenBanking.

...

**<span style="color:#00704A">Như vậy thì liên quan gì đến việc clean code?</span>**

Dựa trên mục đich cuối cùng của ngành phần mềm, ta buộc thừa nhận rằng việc phần mềm chạy được, giải quyết đúng vấn đề, hay "gãi đúng chỗ ngứa" là điều quan trọng hơn thảy. Khi đem lên bàn cân, người ta dễ dàng lựa chọn một phần mềm chạy được mà code xấu, hơn là một phần mềm code đẹp nhưng lại chạy chẳng ra hồn.
Giả sử bạn muốn xem giờ, tôi cho bạn 2 lựa chọn: 1 cái apple watch hết pin, và 1 cái casino 300k vẫn chạy đúng giờ, thì bạn sẽ lựa chọn cái nào?

Điều này nhìn có vẻ ít quan trọng, nhưng thực tế thì ngược lại, và ảnh hưởng nhiều đến tư duy / mindset của một lập trình viên. Tại sao tôi lại nói như vậy? Hiểu được việc sản phẩm phần mềm thực chất sinh ra để giải quyết bài toán nào đó, đồng nghĩa với việc đối với lập trình viên, thì cần quan tâm đến giải pháp đang xây dựng có thực sự tối ưu cho bài toán đó không, hơn là dành sự ưu tiên của mình vào việc clean code. Tôi xin nhấn mạnh, là ưu tiên hơn, chứ không phải là không ngó ngàng gì đến code hết nhé.

Tư duy này được tóm tắt là: "First, solve the problem. Then, write the code" (John Johnson)

<div style="display: flex; align-items: center; justify-content: center;">
  <img class="wp-image-1879 aligncenter" src="/assets/images/post/solve_problem_write_code.jpeg" alt="" width="600" height="400" srcset="/assets/images/post/solve_problem_write_code.jpeg" sizes="(max-width: 600px) 100vw, 320px" />
</div>
# <span style="color: #ff9900;">Fact #2: Code đẹp phục vụ cho con người</span>
Martin Fowler đã từng nói 1 câu rất nổi tiếng: "Any fool can write code that a computer can understand. Good programmers write code that humans can understand."
Kẻ cuối cùng thực thi code là máy tính, và nó chỉ nhận lệnh dạng nhị phân (0 và 1), cho nên các lý thuyết về clean code của OOP (hoặc function, procedure pramming,...) đối với nó không có nghĩa lý gì hết. Suy cho cùng, đích đến cuối cùng của việc code đẹp hay xấu là nằm ở việc developer khác có dễ dàng tiếp cận và hiểu được đoạn code đó hay không.

<div style="display: flex; align-items: center; justify-content: center;">
  <img class="wp-image-1879 aligncenter" src="/assets/images/post/any_fool_code.jpeg" alt="" width="700" height="400" srcset="/assets/images/post/any_fool_code.jpeg" sizes="(max-width: 700px) 100vw, 320px" />
</div>
Vì nó phụ thuộc vào con người, cho nên một trong những yếu tố quan trọng cần phải suy xét là level của team bạn. Bạn không thể áp dụng máy móc một hoặc một vài pattern phức tạp, khiến code lòng vòng, chỉ để phục vụ mục đích code "đẹp" hơn, trong khi cả team bạn toàn ông fresher / junior chẳng thể hiểu được ý nghĩa và vận dụng thành thạo được cách phân chia đó. Việc áp dụng coding practice sẽ làm giảm tốc độ phát triển của team (trong ngắn hạn vì mọi người cần phải làm quen với nó) và dẫn đến việc estimate bị sai, hệ quả tất yếu sẽ là miss deadline, và điều này có nhiều lúc còn nguy hiểm hơn việc code xấu nhiều lần.

Việc code có "đẹp" hay không còn phụ thuộc vào kiến thức và tư duy của chính người đọc code nữa. Trong ~ 9 năm làm việc, tôi có cơ hội tiếp xúc với một số developer mà tôi hay gọi vui là "Chí Phèo Coder" - kiểu dạng hắn vừa code vừa chửi, đọc code của ai hắn cũng chửi. Cách tốt nhất để xử lý trong case này là để cho họ thấy thiên đường của họ thực chất cũng là bãi rác đối với người khác. Tôi đã từng thử để họ triển khai ý tưởng của họ, và cuối cùng chứng minh cho họ thấy, cái họ đang làm có output thậm chí còn chẳng bằng những đoạn code cũ - thứ họ đã từng chê bai vậy.
Công bằng mà nói, có nhiều lý do có thể dẫn đến việc developer cũ xử lý đoạn code đó theo hướng như vậy, và những người đến sau thì thường không có đủ bối cảnh để phán xét, cho nên phần nhiều là phán xét chủ quan.

<div style="display: flex; align-items: center; justify-content: center;">
  <img class="wp-image-1879 aligncenter" src="/assets/images/post/rewrite_code.jpeg" alt="" width="600" height="200" srcset="/assets/images/post/rewrite_code.jpeg" sizes="(max-width: 600px) 100vw, 320px" />
</div>
# <span style="color: #ff9900;">Fact #3: Nghiệp vụ luôn đi trước</span>
Một sự thật khác tôi muốn đề cập đó là việc: "Nghiệp vụ luôn đi trước". Nghiệp vụ là khởi nguồn của việc thiết kế hệ thống. Ở trên tôi có nhắc đến việc phần mềm sinh ra để giải quyết vấn đề, và nghiệp vụ ở đây đóng vai trò phát hiện vấn đề, cũng như mô tả cách thức vấn đề đó cần được giải quyết. Bất kể khi nào nghiệp vụ thay đổi, thì code cũng sẽ biến đổi tương ứng. Mối liên hệ này dẫn đến những trường hợp khi nghiệp vụ thay đổi nhiều, thì code cũng sẽ phải update kha khá, thậm chí là đập đi xây lại hoàn toàn.
Nếu một lập trình viên tốn nhiều thời gian vào xây dựng, chia nhỏ module code của mình để cho nó clean hơn, thì giả sử sau này nghiệp vụ phần đó thay đổi nhiều, và phần code hoàn thiện đó bị loại bỏ đi thì sẽ là một sự lãng phí lớn.

Thực tế, trong thời đại ngày nay, thì tình trạng nghiệp vụ update thường xuyên ... lại là chuyện thường ngày ở huyện.

Với sự trỗi dậy của trào lưu Agile "welcome to change", thì tần suất update nghiệp vụ lại càng cao hơn bao giờ hết. Đặc biệt là với các startup, hay những sản phẩm đang trong giai đoạn MVP, Alpha, Beta,... Tần suất này sẽ giảm dần, khi mà sản phẩm đã đi vào ổn định (tức là thị trường đồng tình với sản phẩm), và đây là thời điểm vàng để developer bắt đầu tận dụng nguồn lực để refactor, để làm sang, xịn, mịn lại source code của mình.

Nói như vậy không phải là cứ code ẩu, code xấu đi vì đằng nào chả refactor lại. Code cũng cần phải đảm bảo ở một chất lượng nhất định, và điều này cần được nghiên cứu cũng như triển khai dưới sự đồng thuận của cả team, và quan trọng hơn là cần phải hiểu code xấu như vậy thì sẽ để lại hậu quả gì, chi tiết thì tôi sẽ nói ở phía cuối bài viết.

Bạn có thể suy nghĩ rằng tôi hoàn toàn có thể dự đoán được nghiệp vụ sẽ thay đổi theo hướng nào, qua đó chuẩn bị plan hoặc code theo hướng dễ dàng mở rộng hơn thì sao?
Tôi đồng ý, nếu là một lập trình viên kinh nghiệm, thì hầu hết mọi người đều sẽ làm như vậy, nó hoàn toàn tuân theo Open-Closed Principle (trong bộ S.O.L.I.D). Nhưng tôi cũng phải cảnh báo, requirements thay đổi ra sao, nhiều lúc nó sẽ nằm ngoài dự đoán của cả đội, và cho dù bạn cố gắng thế nào, cũng không thể hoàn toàn tính toán được hết các case liên quan. Chưa kể rằng nhiều khi tốn công vào việc phòng ngừa các case, có thể kéo dài thời gian phát triển, và nếu như tính toán của bạn là sai, thì những công sức bạn bỏ ra sẽ không phục vụ mục đích gì cả, và rơi vào trường hợp kinh điển trong coding, đó là You-aint-gonna-need-it (YAGNI).

Đa phần ở những thời điểm đầu tiên của giai đoạn phát triển, code của bạn sẽ rất đẹp, rất xịn, và bạn rất tự hào về nó. Tuy nhiên thời gian qua đi, những thay đổi về phía nghiệp vụ, và áp lực của deadline sẽ dí sát đến bạn, và lúc này những đoạn code sai lệch sẽ xuất hiện. OCP được đánh giá là nguyên lý đơn giản, nhưng cũng khó thực hiện nhất là vì vậy.

# <span style="color: #ff9900;">Fact #4: Công nghệ thay đổi và code cũng vậy</span>

Có lẽ tôi không cần phải nói nhiều về việc công nghệ đã thay đổi liên tục và chóng mặt thế nào, nhưng tôi cũng muốn chia sẻ về việc code và clean code cũng thay đổi theo năm tháng chứ không phải là bất biến.
Tôi không phủ nhận rằng có rất nhiều coding mindset có thể trường tồn như SOLID, DRY, YAGNI, KISS,... thế nhưng cũng không đảm bảo 100% rằng nó sẽ mãi mãi đúng. Ví dụ ở bài viết singleton tôi cũng có chia sẻ về việc nó từ phổ biến lại trở thành một anti-pattern.
Ví dụ khác, MVC là một trong những architecture pattern phổ biến bậc nhất trong ngành lập trình, kể cả intern hay fresher developer đều cũng ít nhất nghe đến tên của nó rồi. MVC cũng là kiến trúc ưu tiên khi xây dựng các phần mềm. Các framework thông dụng như Django (Python), Spring (Java), Laravel (PHP), ... cũng đều là MVC-based hết cả. Ở thời kỳ sơ khai lập trình iOS, hầu hết các lập trình viên cũng lựa chọn MVC làm kiến trúc chính để xây dựng, thậm chí core của UIKit còn là các UIViewController. Tuy nhiên về sau, các lập trình viên đều nhận thấy rằng MVC không còn là chân ái nữa, song song với đó là sự phát triển của Data-Driven tác động đến các dev frontend. Thời gian sau là sự bùng nổ của Functional Reactive Programming (FRP), kéo theo việc các dev đổ xô sang các kiến trúc khác như MVVM, MVP, Clean architecture,... và Apple thậm chí còn migrate sang SwiftUI và Combine để thay thế cho ViewController.

Một người lập trình viên đời sau khi đọc code của những người đi trước mình thì hoàn toàn có thể xảy ra phản ứng tâm lý là nghĩ rằng code này như sh\*t vậy? Sao lại phải dùng MVC, trong khi best practices bây giờ là MVVM cơ mà?

Sự thật này đồng nghĩa với việc code đẹp cũng chỉ có tính thời gian, bây giờ nó là code đẹp, nhưng tương lai nó xấu là bình thường. Đó là lý do vì sao mà code refactoring lại là common practices xuyên suốt quá trình phát triển, chẳng ai dám tự tin vỗ ngực, code của tôi là chân lý bất biến theo năm tháng được hết. Vì lẽ đó, code của bạn rồi cũng sẽ thành sh\*t cả thôi.

<div style="display: flex; align-items: center; justify-content: center;">
  <img class="wp-image-1879 aligncenter" src="/assets/images/post/mvc_mvvm.png" alt="" width="600" height="250" srcset="/assets/images/post/mvc_mvvm.png" sizes="(max-width: 600px) 100vw, 320px" />
</div>
# <span style="color: #ff9900;">Code xấu thì sao?</span>

Hậu quả lớn nhất của code xấu là gây ra technical debt (nợ kỹ thuật). Về mặt lý thuyết thì technical debt này nếu không được giải quyết thì nó sẽ càng lớn theo thời gian và theo chính sự phát triển của số lượng code. Vì nó là debt (nợ), nên chắc chắn sẽ phải trả, trả sớm thì lãi ít, trả muộn thì lãi cao, và nhiều khi còn phá sản vì nợ. Các trường hợp dễ gặp như code xấu ảnh hưởng đến việc maintain, giả sử như phần mềm gặp bug, thì đống messy code sẽ gây cản trở đến vấn đề tìm, debug và sửa chữa bug đó. Ngay cả khi đã fix xong, thì người fix cũng không thể tự tin về phạm vi ảnh hưởng của đoạn code anh ta vừa thay đổi được.
Trường hợp khác, code xấu gây khó khăn trong việc phát triển thêm (khi có thay đổi từ nghiệp vụ), hay scale hệ thống. Bạn không thể xây thêm tầng khi móng của bạn không chắc được, code cũng vậy, không thể mở rộng nếu nó quá phức tạp được.

Các vấn đề về code xấu, technical debt này nên được quản lý rõ ràng, và được nhận thức chung bởi mọi người trong cùng 1 team. Chính vì vậy với các team ít kinh nghiệm, thì tôi khuyến cáo người leader nên trực tiếp tham gia code để đánh giá được tình hình chính xác nhất. Vì lý do sinh ra technical debt là vì team chấp nhận nó để đánh đổi lấy một mục tiêu nào đó (như là kịp deadline, test tính năng,...), nên khi bắt đầu coding, bạn cần phải xác định rõ rằng mình có cần và có đáng đánh đổi không, thậm chí là phải hỏi tư vấn từ leader.

<div style="display: flex; align-items: center; justify-content: center;">
  <img class="wp-image-1879 aligncenter" src="/assets/images/post/tech_debt.png" alt="" width="500" height="250" srcset="/assets/images/post/tech_debt.png" sizes="(max-width: 600px) 100vw, 320px" />
</div>

# <span style="color: #ff9900;">Kết Luận</span>

Bài viết này tôi không phê phán clean code là sai trái, cái tôi nhấn mạnh ở đây rằng clean code là tốt, nhưng nó không được đặt độ ưu tiên cao nhất khi so sánh với các tiêu chí khác trong việc phát triển phần mềm. Việc dự án tồn tại code smell không phải là điều gì bất thường hoặc cực kỳ tồi tệ cả, quan trọng là người team phát triển phải nhận thức được vấn đề về code xấu, và độ ảnh hưởng của nó, sau cùng phải lên được kế hoạch xử lý tương ứng.

Việc phần mềm sinh ra suy cho cùng vẫn để giải quyết một vấn đề nào đó (như fact #1 tôi có nói), chính vì vậy code như thế nào thì code, cần phải đảm bảo code chạy được và xử lý được vấn đề mà nó đang giải quyết. Tóm gọn lại:

- Phần mềm chạy được quan trọng hơn code xấu hay đẹp
- Code nào rồi cũng thành sh\*t mà thôi.

{% include disqus_comments.html %}
