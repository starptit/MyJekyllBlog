---
title: "Năm Mèo Nói Chuyện Refactor Code: Mèo Đen Hay Mèo Trắng"
categories: coding
layout: article
---

Mèo đen hay mèo trắng không quan trọng, miễn là nó bắt được chuột (Thuyết con mèo - Đặng Tiểu Bình)

Dẫn luận thành

Code xấu hay code đẹp không quan trọng, miễn là nó chạy được.

Khi tôi tóm tắt như vậy, chắc chắn sẽ có nhiều người phản đối, hay chê cười, vì đơn giản ai cũng hiểu là nếu đã là developer thì code smell, code spaghetti,... là một trong những tiêu chí quan trọng để phân loại level của developer. Chẳng có ông nào vỗ ngực là senior mà lại đem ra một đống sh\*t code cả. Hơn nữa, những dòng code được đo ni đóng giầy vào từng ông developer, nên nếu là một dev thực thụ, chắc chắn mọi người sẽ luôn muốn đảm bảo những dòng code của mình là clean nhất có thể. Nếu là một developer mà chấp nhận những dòng code xấu, thì chỉ có 2 trường hợp:

1. Ông là dev cùi
2. Tiêu chuẩn của ông thấp

Tôi thì không phải loại nào trong 2 loại trên, bản thân tôi cũng từng viết một số bài viết về clean code và design pattern, nên là trust me bro, tôi không phải là người dễ dãi với những dòng code. Trước đó, tôi cũng đã từng có khoảng thời gian tư duy kiểu clean code như một tôn giáo vậy, nhưng hiện tại quan điểm của tôi đã hoàn toàn thay đổi, có lẽ vì kinh nghiệm sau một số năm làm việc trong nghề, được tiếp xúc với một số developer xịn, và nhìn nhận sản phẩm phần mềm theo nhiều góc độ khác nhau.

# <span style="color: #ff9900;">Mọi phần mềm sinh ra đều là để giải quyết vấn đề nào đó?</span>
<p>Giá trị cốt lõi của việc áp dụng các đột phá công nghệ, là nằm ở việc công nghệ đó đem lại lợi ích gì cho kinh doanh sản xuất, cho đời sống xã hội; cụ thể hơn, công nghệ đó giải quyết được vấn đề gì. Chẳng phải ngẫu nhiên mà người ta thường dùng cụm từ "giải pháp công nghệ", tức là bản thân nó là giải pháp (solution) cho vấn đề gì.

Hãy thử quan sát một số ví dụ sau:
- Để giải quyết các vấn đề về liên lạc, chúng ta xây dựng ra các ứng dụng nhắn tin tức thì (Instant Message) như Yahoo, Skype, Messenger,... Rồi sau đó để giải quyết vấn đề liên lạc phục vụ riêng cho doanh nghiệp, chúng ta lại có Slack, MS Teams,... Hay để nhắn tin private, chúng ta lại có các phần mềm như Telegram, Snapchat,...
- Để giải quyết việc quản lý Kế Toán doanh nghiệp, chúng ta có Misa.
- Để giải quyết vấn đề kết nối các ngân hàng, chúng ta có OpenBanking.
...

Như vậy thì liên quan gì đến việc clean code?
Dựa trên mục đich cuối cùng của ngành phần mềm, ta buộc thừa nhận rằng việc phần mềm chạy được, giải quyết đúng vấn đề, hay "gãi đúng chỗ ngứa" là điều quan trọng hơn thẩy. Khi đem lên bàn cân, người ta dễ dàng lựa chọn một phần mềm chạy được mà code xấu, hơn là một phần mềm code đẹp nhưng lại chạy chẳng ra hồn.
Giả sử bạn muốn xem giờ, tôi cho bạn 2 lựa chọn: 1 cái apple watch hết pin, và 1 cái casino 300k vẫn chạy đúng giờ, thì bạn sẽ lựa chọn cái nào?

Điều này nhìn có vẻ ít quan trọng, nhưng thực tế thì ngược lại. Nó ảnh hưởng nhiều đến tư duy của một lập trình viên. Bạn đã từng bao giờ gặp 
</p>
# <span style="color: #ff9900;">Code sinh ra để người đọc</span>

# <span style="color: #ff9900;">Công nghệ thay đổi và code cũng vậy </span>

# <span style="color: #ff9900;">Level của team bạn</span>

# <span style="color: #ff9900;">Technical Debt</span>

# <span style="color: #ff9900;">Kết Luận</span>

<div style="display: flex; align-items: center; justify-content: center;">
  <img class="wp-image-1879 aligncenter" src="/assets/images/post/marshmallow-tower.jpeg" alt="" width="600" height="400" srcset="/assets/images/post/marshmallow-tower.jpeg" sizes="(max-width: 600px) 100vw, 320px" />
</div>
<p>
Vậy theo bạn, nhóm nào là nổi trội hơn cả?
</p>
***Kỹ sư, Quản lý,... ?***

Không. Nhóm thắng cuộc ở đây là <span style="color:#FF6464">trẻ mẫu giáo</span>. Đúng vậy, nhóm trẻ 6 tuổi là kẻ thắng cuộc ở thử thách trên, trong khi nhóm về bét lại là <span style="color:#B3FFAE">sinh viên MBA.</span>

Vậy điều gì đã khiến những đứa trẻ trở đánh bại tất cả? Liệu rằng chúng có tư duy hay kế hoạch gì đặc biệt chăng? Hay vì chúng là trẻ em nên quen thuộc với kẹo dẻo hơn người lớn?
Tất cả đều không đúng, một đứa trẻ làm sao có thể thông minh hơn nhóm kỹ sư và quản lý, chúng không thể hiểu biết về kiến trúc hơn đội người lớn được. Vậy bí quyết ở đây là gì?

Đó chính là cách mà trẻ con **tiếp cận bài toán.** Chúng chỉ đơn thuần là bắt tay vào làm và làm. Chúng thử nghiệm nhiều cách hơn, cứ xây đổ thì chúng lại xây lại, cho đến khi xây ra được một kiến trúc cao nhất trong các lần thử.

Hay nói cách khác, <span style="color:#FF6464">_**chúng bắt đầu từ những thất bại và học hỏi chúng ngay lập tức.**_</span> Chúng cứ xây thử rồi kiểm tra, sau đó lại thử tiếp và kiểm tra tiếp, cho đến khi hết 18 phút quy định. Chúng không hành động theo một con đường được vạch sẵn nào cả, và kỳ diệu (có thật không?) là đây lại là cách đem đến chiến thắng.

<div style="display: flex; align-items: center; justify-content: center;">
  <img class="wp-image-1879 aligncenter" src="/assets/images/post/children_winner.jpeg" alt="" width="500" height="500" srcset="/assets/images/post/children_winner.jpeg" sizes="(max-width: 500px) 100vw, 320px" />
</div>

Sinh viên MBA, trái lại, là những kẻ nghĩ và tính toán rất nhiều rồi mới hành động, thì kết cục lại là kẻ về bét.

Rõ ràng, nghĩ nhiều so với việc xắn tay vào làm, thì việc xắn tay vào làm hẳn nhiên là tốt hơn rồi.

Vậy suy nghĩ nhiều là xấu?

Không phải vậy, về sau khi challenge phổ biến, thì người chiến thắng lại là các **kỹ sư.**

# <span style="color: #ff9900;">Tôi thử challenge</span>

Hồi còn làm ở công ty cũ, tôi cũng đã có cơ hội join thử cái challenge này (Thực ra là công ty tổ chức, và tôi thì mặc nhiên phải tham gia).
Chúng tôi chia làm 4 đội, mỗi đội 3 người, tôi cũng không nhớ cụ thể cơ cấu ban bệ thành phần tham gia, nhưng duy chỉ có team tôi đặc biệt là vì có 3 người là kỹ sư (2 ông IT, 1 ông kỹ sư hàng không), đến nỗi các sếp còn bảo là unfair team.

Khi bắt đầu challenge, đồng đội của tôi rất tự tin và chia sẻ rằng mình đã từng biết đến challenge này rồi, và chúng tôi cứ làm theo best practices là xong mà thôi.
Như tôi đã nõi ở trên, khi challenge phổ biến thì người chiến thắng là các kỹ sư. Họ bắt đầu biết vận dụng các kiến trúc cấu trúc sau khi đã nghiên cứu và tính toán đủ lâu. Kiến trúc tối ưu nhất được đưa ra là xây theo <span style="color:#FF6464">dạng lập phương (Cube)</span>, sau đó build từng tầng lên thành dạng <span style="color:#FF6464">Kim tự tháp (Pyramid).</span>

Và đó chính là những gì mà đồng đội truyền đạt lại cho chúng tôi. Chúng tôi cũng làm đầy đủ các bước, lên ý tưởng, phác hoạ, sau đó triển khai. Cấu trúc mà chúng tôi chọn là xây dựng các khối lập phương.

<div style="display: flex; align-items: center; justify-content: center;">
  <img class="wp-image-1879 aligncenter" src="/assets/images/post/2000px.jpeg" alt="" width="600" height="400" srcset="/assets/images/post/2000px.jpeg" sizes="(max-width: 600px) 100vw, 320px" />
</div>
(Source: https://makefuncreating.com/crafts/how-to-build-a-tall-spaghetti-and-marshmallow-tower/)

Và team chúng tôi đã xuất sắc giành giải nhất.
<span style="color:#F8FFDB">_Có cái nịt_</span>

Chính xác thì team chúng tôi về gần bét (3/4) đội tham dự.

Còn team giành giải nhất, tréo ngoe thay, lại là team của <span style="color:#FF6464">phòng Marketing (nơi mà chẳng có một ai là kỹ sư cả).</span>

Giải pháp của họ là gì?
Giống hệt những đứa trẻ kể trên, họ chỉ thử nghiệm, học hỏi và thử nghiệm tiếp, không có gì đặc biệt ở đây hết.

Vậy tại sao chúng tôi lại thua?
Chúng tôi đã không tính đến một yếu tố cực kỳ quan trọng, đó chính là <span style="color:#FF6464">**THỜI GIAN.**</span> Chúng tôi chỉ có chính xác <ins>**_18 phút_**</ins> cho toàn bộ công việc, từ lên ý tưởng, phân tích thiết kế, và triển khai (kể cả testing và release nữa, LOL). Kiến trúc chúng tôi phác thảo là chính xác, tuy nhiên thời gian để chúng tôi triển khai nó thì không đủ, và dẫn đến kết cục cuối cùng là chúng tôi đã thua cay đắng.

# <span style="color: #ff9900;">Tôi học được gì</span>

Nếu đem lên bàn cân, thì spaghetti tower marshmallow challenge chẳng khác gì bài toán xây dựng một sản phẩm mà tôi - một người kỹ sư IT đang phải giải quyết hàng ngày.

Chúng tôi cũng có target, ý nghĩa, thời gian, nhân sự, budget,... và cái cấu trúc cao nhất mà challenge yêu cầu cũng tương ứng với việc xây dựng một sản phẩm phần mềm tốt nhất (thế nào là tốt thì tôi sẽ giải thích ở một bài viết khác)

Nhìn từ góc độ quản lý dự án, thì challenge này là một dự án, nguồn lực chúng tôi đã có, và định nghĩa hoàn thành của dự án cũng đã có.

Vậy thì cụ thể tôi học được gì?

<span style="color:#54B435">Bài học đầu tiên:</span> Khi xây dựng một sản phẩm, mà trong tay chúng ta chưa có một mô hình, hoặc con đường cụ thể nào, thì cách tối ưu nhất là hãy cứ thử - fail - học - thử. Hãy làm như tụi trẻ con ở nghiên cứu của Peter Skillman kể trên. Điều này cũng được các công ty ở Sillicon valley thực hiện triệt để, thậm chí còn có một thuật ngữ nổi tiếng cho việc này "fail fast and fail cheap".
Điều này cũng là dể hiểu thôi vì theo một số thống kê không chính thức, có khoảng 90% các startup sẽ chết (10% chết trong ngay năm đầu tiên), và chỉ có 10% là kẻ thành công (hoặc là chưa chết cho đến thời điểm thống kê). Vì vậy, sẽ quá là lãng phí nếu các startup nghĩ quá nhiều mà không làm gì hết (như các sinh viên MBA ở thí nghiệm trên), trong khi vẫn chưa rõ ràng một con đường thành công nào cả.

<div style="display: flex; align-items: center; justify-content: center;">
  <img class="wp-image-1879 aligncenter" src="/assets/images/post/start_up_fail_percentage.jpeg" alt="" width="500" height="275" srcset="/assets/images/post/start_up_fail_percentage.jpeg" sizes="(max-width: 500px) 100vw, 320px" />
</div>

Tuy nhiên, nếu đã có con đường dẫn đến thành Rome rồi thì ta cứ men theo nó mà đi thôi, lúc này việc thử nghiệm nhiều lại hoá thành dở hơi và lãng phí. Khoan, bạn vẫn chưa quên lần thực nghiệm của tôi ở trên chứ? Tôi có model rõ ràng rồi, tôi có phác hoạ rồi, vậy mà tôi vẫn về sau là sao?
Lý do tôi cũng đã kể trên rồi, bạn phải chú ý đến thời gian nữa. Nhưng thời gian chỉ là một cách minh hoạ ngắn thôi, bản chất ở đây là bạn phải chú ý đến nguồn lực của bạn. Bạn cần phải tính toán xem mình, với những thứ trong tay, có khả năng theo con đường kia đến thành Room thành công hay không? Giả sử như bên đó bắt bạn phải đi xe ngựa, trong khi team lại đi dép cao su Trường Sơn, mà bạn vẫn cắm đầu bắt team phải đi, thì kết quả là gì ai cũng rõ. Và đó cũng chính là <span style="color:#54B435">bài học thứ 2.</span>

Ngoài ra, trong quá trình phát triển sản phẩm, tôi cá rằng phần lớn sản phẩm của bạn cũng sẽ dựa trên một vài sản phẩm nào đó đã có sẵn trên thị trường, và bạn sẽ thêm một số tính năng khác mà bạn giả định rằng sẽ vượt trội hơn đối thủ, và đem lại lợi thế cạnh tranh, cũng như được người dùng đón nhận. Ở trường hợp này, bạn hãy học hỏi và đi theo con đường của các sản phẩm tương tự để tiết kiệm thời gian và nguồn lực, tuy nhiên, cần phải chủ ý, đến đoạn bạn cần phải tách đoàn và see you again (như Dom & Brian trong Fast and Furious vậy).

Tôi cũng không phản đối việc sản phẩm của bạn có thể là độc nhất, là đột phá sáng tạo, tuy nhiên xác suất đó có nhiều không? Và nếu giả sử bạn rơi vào trường hợp này, thì chiến lược ở đây hẳn bạn cũng đã rõ rồi, là làm theo bọn trẻ con mẫu giáo thử - fail - học - thử. Và quan trọng, việc thử nghiệm này phải do thị trường quyết định, không phải là bạn, CEO,CFO,... hay bất cứ ai đánh giá cả.

Ngoài ra, trong quá trình phát triển sản phẩm, sẽ có những lúc bạn cũng sẽ cần phải phát triển một hoặc một vài tính năng mới rơi vào 1 trong 2 trường hợp trên (là đã có đường đến Rome hay là chưa ai mở), thì chiến lược là gì bạn đã hiểu rồi chứ.

Tuy nhiên, nếu trong tay bạn có đủ nguồn lực, hãy tự tin là cô gái mở đường đi, vì risk đi kèm với return mà, high risk high return. Bạn mở đường thành công, bạn là winner - winner take all.

> "Trên đời này làm gì có đáy, người ta bán mãi cũng thành đáy thôi" (Lỗ To)

À tôi nhầm,

<span style="color:#993300"> **"Trên đời này làm gì có đường, người ta đi mãi thì thành đường thôi" (Lỗ Tấn)**</span>

{% include disqus_comments.html %}
