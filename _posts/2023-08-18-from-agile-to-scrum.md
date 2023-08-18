---
title: "From Agile to Scrum"
categories: product
layout: article
tags: [product, mindset]
---
Agile và Scrum không còn là thuật ngữ mới, không tính riêng ngành phần mềm, mà nó đã thực sự phổ biến ở rất nhiều ngành nghề khác rồi. Sự thịnh hành của Agile và Scrum kéo theo trào lưu nhà nhà đi học, người người thực hành với kì vọng có thể vận dụng nó để thay đổi được phong cách quản lý, tối ưu hoá năng suất,... hay vô vàn những lời giới thiệu có cánh khác. Thế nhưng, tôi cho rằng việc các tổ chức, cá nhân hype về trào lưu này lại ẩn chứa nhiều vấn đề mà họ không (hoặc là chưa) biết đến.

Giả sử với Scrum, thường các công ty sẽ được tổ chức training trong khoảng 2-4 ngày cuối tuần, với một bảng guideline và kèm theo các lý thuyết cơ bản về Scrum: events, artifacts, ...
Sau khoảng thời gian đó, họ sẽ nhận được chứng chỉ Certified ScrumMaster (CSM), đánh dấu mình đã tham gia và nắm bắt được các kiến thức về Scrum, cũng như đủ thẩm quyền để triển khai Scrum.

Tôi hiểu là practice trên không có gì sai, vì bản chất Scrum cũng định nghĩa rất rõ là nó là framework cực kỳ đơn giản và có thể giải thích chỉ bằng vài tờ giấy A4. Tuy nhiên, vế sau nó cũng nhấn mạnh về việc nó là một framework cực kỳ khó để master. Thế nên tôi cảm thấy nghi ngờ về việc liệu rằng Agile & Scrum, trước hết có được nhận thức đúng đắn không, chứ chưa nói đến việc thực hành nó nhé.

Thông qua series này, tôi mong muốn có thể tạo cơ hội để giải ngố, bàn luận, và tranh luận về Agile & Scrum, vì đơn giản là không nằm ngoài vòng xoáy, Scrum & Agile cũng được Amela apply vào trong quy trình phát triển của mình, nên những kiến thức và tư duy về chúng không khi nào là thừa thãi cả.

# Agile và Scrum là 1?
2 cụm từ Agile và Scrum thường được sử dụng thay thế nhau trong các hội thoại ở công việc thường ngày. Tức là, có chỗ nói: Ở team chúng tôi sử dụng Scrum để quản trị dự án; và cũng có team khác nói rằng: chỗ chúng tôi áp dụng quy trình Agile vào vận hành bộ phận của mình. Cách lạm dụng từ ngữ này gây ra hiểu lầm tai hại, rằng sẽ có nhiều người cho rằng Agile và Scrum bản chất là như nhau.

Tôi khẳng định: Agile là Agile, và Scrum là Scrum, chúng rất khác nhau.

Và để hiểu được sự khác biệt của 2 thuật ngữ này, chúng ta hãy mượn cỗ máy thời gian của Đô-rê-mon, để cùng quay trở lại tìm hiểu sự ra đời của Agile.

# Lịch sử ra đời Agile
## Trước Agile
Trước khi xuất hiện Agile, ngành công nghệ phần mềm đã phát triển và ứng dụng rất nhiều phương pháp quản trị khác nhau.

**Waterfall (mô hình thác nước)** được phát triển dựa trên mô hình vận hành nhà máy ô tô của Ford (ở những năm 1910s), đã trở nên cực kỳ phổ biến từ sau thập niên 70 của thế kỷ trước.
<div style="display: flex; align-items: center; justify-content: center;">
  <img class="wp-image-1879 aligncenter" src="/assets/images/post/fsta/fsta-anh1.png" alt="" width="326" height="270" srcset="/assets/images/post/fsta/fsta-anh1.png" sizes="(max-width: 600px) 100vw, 320px" />
</div>


Đặc trưng của mô hình này là chia nhỏ quá trình phát triển phần mềm thành nhiều giai đoạn nhỏ, và thực hiện chúng một cách tuần tự, hết bước requirements rồi mới thực hiện sang bước Analysis, cứ tuần tự thực hiện cho đến bước cuối cùng, tương tự như dòng chảy của thác nước vậy (thế nên nó mới được gọi là waterfall).

**Spiral (mô hình xoắn ốc)** - được phát kiến vào khoảng 1980s bởi Barry Boehm, với kỳ vọng giải quyết bài toán về trong quản trị rủi ro - là một khía cạnh quan trọng theo tư duy của Boehm. Spiral được thử nghiệm trong các dự án phần mềm quân sự của Mỹ, và sau đó được ứng dụng rộng rãi ra các ngành khác.
<div style="display: flex; align-items: center; justify-content: center;">
  <img class="wp-image-1879 aligncenter" src="/assets/images/post/fsta/fsta-anh2.png" alt="" width="421" height="261" srcset="/assets/images/post/fsta/fsta-anh2.png" sizes="(max-width: 600px) 100vw, 320px" />
</div>

Spiral hay còn được gọi là mô hình lặp, với đặc trưng chia nhỏ các giai đoạn phát triển thành nhiều vòng lặp, mỗi vòng lặp cũng sẽ gồm đầy đủ các bước như của Waterfall: requirement, analysis, design,... Tuy nhiên, mỗi vòng lặp sẽ yêu cầu tăng dần độ phức tạp và mức độ chi tiết của dự án, và các giai đoạn của từng vòng lặp sẽ đi qua theo hình dạng xoắn ốc (lý do nó được gọi là spiral). Nghe khá quen nhỉ? Đúng vậy, Spiral là nguồn cảm hứng cho sự ra đời của Scrum sau này.

Thập niên 1990-2000 là thời kỳ lên ngôi của **mô hình V-Model**. Mô hình này thực chất đã xuất hiện từ khá lâu, được phát triển dựa theo mô hình Das V-Modell của người Đức.
<div style="display: flex; align-items: center; justify-content: center;">
  <img class="wp-image-1879 aligncenter" src="/assets/images/post/fsta/fsta-anhx.png" alt="" width="300" height="240" srcset="/assets/images/post/fsta/fsta-anhx.png" sizes="(max-width: 600px) 100vw, 320px" />
</div>

Với mô hình V-model, các giai đoạn phát triển phần mềm được biểu diễn dưới dạng một đường thẳng đi xuống, từ yêu cầu, phân tích, thiết kế, cài đặt, và kiểm thử. Sau khi các giai đoạn phát triển hoàn thành, mô hình sẽ "lật ngược" thành một đường thẳng đi lên, đại diện cho các giai đoạn kiểm thử, bao gồm kiểm thử đơn vị, kiểm thử tích hợp, kiểm thử hệ thống và kiểm thử chấp nhận.

Ngoài ra, còn có khá nhiều mô hình khác: mô hình tăng trưởng (incremental), mô hình RAD, mô hình LEAN,...  tôi không thể đề cập hết vì giới hạn nội dung của bài viết.

## Vấn đề xảy ra
Ngành phần mềm đã ghi nhận rất nhiều phương pháp phát triển phần mềm rồi, thế nhưng sự thật lại nghiệt ngã hơn tưởng tượng
<div style="display: flex; align-items: center; justify-content: center;">
  <img class="wp-image-1879 aligncenter" src="/assets/images/post/fsta/fsta-anh3.jpeg" alt="" width="417" height="245" srcset="/assets/images/post/fsta/fsta-anh3.jpeg" sizes="(max-width: 600px) 100vw, 320px" />
</div>
<br/>
<div style="display: flex; align-items: center; justify-content: center;">
  <img class="wp-image-1879 aligncenter" src="/assets/images/post/fsta/fsta-anh4.png" alt="" width="481" height="298" srcset="/assets/images/post/fsta/fsta-anh4.png" sizes="(max-width: 600px) 100vw, 320px" />
</div>
2 biểu đồ trên nói lên rằng tỉ lệ thành công của các dự án nếu như áp dụng theo các phương pháp cổ điển như Waterfall rất thấp, kéo theo bối cảnh hàng tỉ $ sẽ bị lãng phí hàng năm.

Đứng trước bài toán đó, một sự kiện mang tính lịch sử đã diễn ra, với chủ đích thảo luận và tìm ra giải pháp để ngăn chặn sự lãng phí trên.

## Ngày lịch sử
Ngày 11/02 đến 13/02 năm 2001 đánh dấu cột mốc lịch sử. Tại hội nghị "Diên Hồng" được tổ chức tại Utah - Mỹ, 17 chuyên gia phần mềm hàng đầu thế giới cùng tụ họp, thảo luận và đề xuất các giải pháp nhằm giải quyết vấn đề tỉ lệ thành công của các dự án ở mức rất thấp (như đã đề cập bên trên). Trong số các chuyên gia đó có những cái tên chắc chắn bạn đã từng nghe rồi, như là: Martin Fowler, Robert C. Martin (Uncle Bob), Jeff Sutherland và Ken Schwaber (cha đẻ của Scrum),... 17 cây đa cây đề này cuối cùng đã thống nhất ý kiến với nhau để đưa ra một bản tuyên bố chung, gọi là tuyên ngôn Agile (Agile manifesto) với nội dung như sau:
 <div style="display: flex; align-items: center; justify-content: center;">
  <img class="wp-image-1879 aligncenter" src="/assets/images/post/fsta/fsta-anh5.png" alt="" width="700" height="444" srcset="/assets/images/post/fsta/fsta-anh5.png" sizes="(max-width: 700px) 100vw, 320px" />
</div>

Chú ý, ở đây sử dụng từ "hơn là", tức là nó có độ ưu tiên cao hơn, chứ không phải là bỏ bê hoàn toàn vế còn lại. Ví dụ: phần mềm chạy tốt hơn là tài liệu đầy đủ, cần phải diễn giải và hiểu rằng quan tâm đến việc phần mềm trước hết phải chạy tốt trước, sau đó mới tính đến các tài liệu kèm theo sau, chứ không phải là tôi chỉ cần phần mềm, không cần tài liệu.
## Có gì đặc biệt?
Bạn có nhận xét gì về sự kiện trên?
Thực chất Agile là sản phẩm được tạo ra bởi nhóm 17 chuyên gia, mỗi ông lại đại diện cho một trường phái, phương pháp quản trị của riêng mình. Ví dụ Ken & Jeff đại diện cho Scrum, Kent Beck là cha đẻ của Extreme Programming (XP),  Uncle Bob với Test-driven development, ... Bản tuyên ngôn Agile thực chất là bản tổng hợp và đồng thuận, chắt lọc từ nhiều phương pháp khác nhau để tìm ra những điểm chung nhất, cốt lõi nhất. Chính vì vậy, khi ta đọc Agile manifesto, sẽ thấy nó thực sự ... rất chung chung.

Nếu bạn là developer, thì điểm này rất tương đồng với 1 loại kỹ thuật nền tảng nhất trong OOP, đó là gì? Việc rút gọn những điểm khác biệt, để tìm ra điểm chung nhất giữa nhiều đối tượng, chính là đặc trung của kỹ thuật trừu tượng hoá (abstract).
### Nếu vậy thì Agile là gì?
Agile thực chất chỉ là sự trừu tượng hoá của nhiều phương pháp quản lý phần mềm khác nhau. Hay nói cách khác, Agile là tư tưởng, là mindset. Agile là tập hợp của nhiều phương pháp phát triển phần mềm khác nhau, thường được ví với chiếc ô Agile như sau:
<div style="display: flex; align-items: center; justify-content: center;">
  <img class="wp-image-1879 aligncenter" src="/assets/images/post/fsta/fsta-anh6.png" alt="" width="302" height="288" srcset="/assets/images/post/fsta/fsta-anh6.png" sizes="(max-width: 600px) 100vw, 320px" />
</div>

### Vậy Scrum là gì?
Scrum là một framework được phát triển từ những năm 1993, và sau đó được Jeff Sutherland và Ken Schwaber đem ra thảo luận ở sự kiện Agile 2001 để tạo nên bản Agile manifesto. Nói cách khác, Scrum và các đặc tính của mình chính là nhân tố hình thành nên Agile.

### Phương pháp luận
Vì lịch sử Agile được tạo nên từ sự trừu tượng hoá nhiều phương pháp quản lý dự án, thế nên phương pháp luận đúng khi muốn tìm hiểu Agile là phải tìm hiểu một phương pháp trong họ nhà Agile trước, sau đó suy luận ngược lên Agile (bottom-up), chứ không phải là căn cứ trên Agile, đi tìm hiểu các phương pháp bên dưới nó (Top-down).
Như vậy, không phải là From Agile to Scrum, mà phải là **From Scrum to Agile**

# Agile nhưng sâu hơn chút
## 12 nguyên tắc Agile
Ở phần trước, tôi đã kết luận lại bản chất Agile là mindset, vì thực sự nội dung của nó rất chung chung. Ở phần này, tôi sẽ nói tiếp, từ bản tuyên ngôn Agile, các nhà sáng lập đã phát triển thành 12 nguyên tắc đặc trưng, và 12 nguyên tắc này sẽ xuất hiện ở tất cả các phương pháp phát triển phần mềm thuộc họ Agile.

**Nguyên tắc 1: Làm hài lòng khách hàng**

Ưu tiên cao nhất là làm hài lòng khách hàng thông qua việc bàn giao phần mềm/sản phẩm có giá trị trong thời gian sớm và liên tục.

**Nguyên tắc 2: Sẵn sàng thay đổi**

Sẵn sàng cho những thay đổi - thậm chí những thay đổi này xuất hiện muộn.

**Nguyên tắc 3: Thường xuyên bàn giao sản phẩm**

Cung cấp phần mềm hoạt động được trong thời gian ngắn từ 1 vài tuần đến 1 vài tháng, càng ngắn càng được ưu tiên.
<div style="display: flex; align-items: center; justify-content: center;">
  <img class="wp-image-1879 aligncenter" src="/assets/images/post/fsta/fsta-anh7.png" alt="" width="463" height="233" srcset="/assets/images/post/fsta/fsta-anh7.png" sizes="(max-width: 600px) 100vw, 320px" />
</div>

**Nguyên tắc 4: Cộng tác cùng nhau**

Người kinh doanh và đội ngũ phát triển phải làm việc cùng nhau mỗi ngày trong suốt dự án.

**Nguyên tắc 5: Tin tưởng và hỗ trợ**

Xây dựng dự án xung quanh những cá nhân có động lực. Cho họ môi trường làm việc thuận lợi và sự hỗ trợ cần thiết. Hãy có niềm tin rằng họ sẽ làm tốt công việc của mình.

**Nguyên tắc 6: Đối thoại trực tiếp**

Đối thoại trực tiếp mặt đối mặt là phương pháp hữu hiệu nhất trong việc truyền đạt thông tin.
<div style="display: flex; align-items: center; justify-content: center;">
  <img class="wp-image-1879 aligncenter" src="/assets/images/post/fsta/fsta-anh8.png" alt="" width="463" height="235" srcset="/assets/images/post/fsta/fsta-anh8.png" sizes="(max-width: 600px) 100vw, 320px" />
</div>

**Nguyên tắc 7: Phần mềm chạy được**

Phần mềm chạy được là thước đo chính của tiến độ dự án.

**Nguyên tắc 8: Phát triển bền vững**

Phát triển bền vững và duy trì việc phát triển liên tục.

**Nguyên tắc 9: Liên tục chú ý**

Liên tục quan tâm đến kỹ thuật và thiết kế để tăng cường tính linh hoạt.
<div style="display: flex; align-items: center; justify-content: center;">
  <img class="wp-image-1879 aligncenter" src="/assets/images/post/fsta/fsta-anh9.png" alt="" width="464" height="234" srcset="/assets/images/post/fsta/fsta-anh9.png" sizes="(max-width: 600px) 100vw, 320px" />
</div>

**Nguyên tắc 10: Vận hành đơn giản**

Đơn giản - nghệ thuật tối đa hóa số lượng công việc không làm - là điều cần thiết.

**Nguyên tắc 11: Team tự tổ chức**

Các kiến trúc, yêu cầu và thiết kế tốt nhất được tạo nên từ các nhóm tự tổ chức.

**Nguyên tắc 12: Phản ánh và điều chỉnh**

Trong khoảng thời gian đều đặn, nhóm phản ánh về cách trở nên hiệu quả hơn, sau đó điều chỉnh cho phù hợp.
<div style="display: flex; align-items: center; justify-content: center;">
  <img class="wp-image-1879 aligncenter" src="/assets/images/post/fsta/fsta-anh10.png" alt="" width="464" height="232" srcset="/assets/images/post/fsta/fsta-anh10.png" sizes="(max-width: 600px) 100vw, 320px" />
</div>
Nếu bạn thấy 12 nguyên tắc này dài và khó nhớ, thì không sao cả, bạn có thể chọn cách học thuộc lòng nó, nhưng tôi sẽ không khuyên bạn như vậy, bạn chỉ cần hiểu được bản chất của vấn đề là hoàn toàn có thể suy luận ra 12 nguyên tắc này.

## Vậy bản chất của vấn đề là gì?
### Bản chất #1: Nhu cầu của con người thay đổi quá nhanh chóng
Sự phát triển của Internet từ cuối những năm 90 đã tác động rất mạnh đến đời sống, văn hoá, xã hội, khiến chúng thay đổi chóng mặt, trong khi các phương pháp quản lý phần mềm lại không thể bắt kịp xu thế, không thể đáp ứng được nhu cầu và trở nên lạc hậu. Và từ thực tế đau khổ đó thì chúng ta mới có hội nghị ở Utah (2001) và sự ra đời của Agile. Đối với người Việt chúng ta, điều này có thể khó hình dung vì thời điểm đó đất nước còn lạc hậu, và công nghệ Internet băng rộng (ADSL) tận năm 2003 mới xuất hiện tại Việt Nam. Tuy nhiên, nếu quan sát kỹ tình hình thế giới, thì thời điểm cuối năm 90 đầu những năm 2000, chính là thời điểm sụp đổ của nền tài chính toàn cầu, được biết đến với tên gọi "bong bóng dot-com" (Dot-com bubble). Chính cái bong bóng này đã khiến cho Internet và trào lưu ăn theo của nó phát triển cực thịnh toàn cầu, kéo theo đó chính là biến đổi cách con người giao tiếp và trao đổi thông tin, và khi con người ta trao đổi nhiều hơn, thì nhiều tình huống sẽ phát sinh hơn, dẫn đến nhu cầu của con người ta sẽ thay đổi nhanh chóng hơn.

Khi Steve Jobs lần đầu giới thiệu chiếc iPhone đầu tiên vào năm 2007, thì nhân loại cũng đồng thời bước vào kỷ nguyên mới, kỷ nguyên của điện thoại thông minh. Sự thịnh hành của smartphone càng đẩy mạnh tốc độ trao đổi thông tin - tương ứng nhu cầu của con người cũng tăng theo.

Bạn không thể phủ nhận rằng việc con người ta dễ dàng tiếp cận và trao đổi thông tin như thế này khiến cho các requirement cũng phải update để chạy theo. Chính vì vậy, việc requirements thay đổi thường xuyên, với tần suất dày hơn không phải là điều mà người quản trị dự án có thể control được, ta buộc phải thừa nhận, chấp thuận nó, và đối ứng với nó là công việc của chúng ta. Do đó, "welcome change" là một nguyên lý căn bản trong bộ 12 nguyên lý.

### Bản chất #2: Mọi thứ đều là giả định.
Một sản phẩm phần mềm ra đời là kết quả của quá trình tìm hiểu thị trường, lên ý tưởng, research, suy nghĩ, thực thi,... của ai?
Là của một người, hoặc của một nhóm người: C-level, PO, customer support, developer,... Có nghĩa rằng, sản phẩm được xây dựng thực chất dựa trên giả định của nhóm người trên về thành công của sản phẩm. Ví dụ, tôi nghiên cứu thấy khách hàng cần một bộ liên lạc doanh nghiệp chuyên nghiệp thay cho Skype, Yahoo!,... tôi lên ý tưởng tạo ra Slack, khách hàng cần matching giữa xe ôm và khách đi đường, tôi nghiên cứu và tạo ra Grab.

Đây chính là điểm mấu chốt, sản phẩm là giả định của một nhóm người, nhưng thực ra trong nền kinh tế hiện tại, cái gì mới là kẻ quyết định thành hay bại của sản phẩm?
Đó chính là **thị trường (market)**, hay người ta thường nói rằng: Trong kinh doanh, thị trường luôn luôn đúng (market is always right).

Làm thế nào để xác định được rằng giả định về thành công sản phẩm là đúng hay sai?
Chẳng có cách nào khác, phải đem ra thị trường để validate, và tự thị trường sẽ cho bạn câu trả lời. Cụ thể, bạn phải đem sản phẩm của bạn đi ra thị trường sớm nhất, và nhiều nhất có thể, và lắng nghe các phản hồi từ thị trường để đưa ra các điều chỉnh phù hợp. Và các phản hồi này lại quay trở lại câu chuyện của #1, welcome changes. Đây không còn là thời kỳ mà một sản phẩm xây dựng trong 1-2 năm rồi mới tung ra thị trường nữa rồi, đây là thời kỳ mà 90% startup failed trong năm đầu tiên, hay nói vui vẻ theo cách của dân Sillicon Valley, là `fail fast and fail cheap`.

Tính chất này rất quan trọng, nó là lý do tại sao chúng ta lại cần liên tục deliver, liên tục cải tiến, liên tục phản ánh và thay đổi, và là cốt lõi của nguyên lý 1,2,3 và 12.

### Bản chất #3: Trao quyền là chìa khoá của team thành công
Nghiên cứu từ những năm 40 của Abraham Maslow đã chỉ ra rằng con người sẽ có hứng thú, sáng tạo và đóng góp khả năng của mình nhiều hơn nếu họ được trao quyền. Năm 1986, Hirotaka và Ikujiro Nonaka (2 người có ảnh hưởng rất lớn đến học thuyết của Scrum), đã đề cập đến thuật ngữ team tự tổ chức trong bài báo đăng trên tạp chí Harvard Business Review, theo quan điểm của 2 ông, yếu tố team tự tổ chức (self-organizing) là nhân tố giúp cho đội nhóm có thể tạo ra những chuyển biến thần tốc.
Ở thời điểm ra đời của Agile năm 2001, thống kê có đến 70% doanh nghiệp áp dụng  phương pháp trao quyền cho nhân viên của mình.
Team được trao quyền cần nhận được sự tin tưởng và tôn trọng quyết định đến từ các thành viên khác ngoài team, nếu không thì việc trao quyền sẽ không có ý nghĩa, giống như Tào Tháo từng nói: "Không tin thì không dùng, đã dùng là phải tin" là vì vậy.

Tính chất trao quyền này chính là yếu tố cuối cùng cần ghi nhớ để hiểu và tự suy luận ra 12 nguyên tắc Agile.

# Tổng kết
Ở bài viết này, tôi đã lội dòng lịch sử để giới thiệu cách mà Agile ra đời, qua đó phân biệt Agile & Scrum, cũng như giới thiệu phương pháp luận mà tôi cho là hợp lý để cho bất kì ai dù là newbie cũng có thể hiểu được chúng. Tóm gón lại, tôi chỉ cần bạn đọc nắm được các điểm sau qua bài viết:
- Phân biệt Agile & Scrum
- 12 nguyên tắc của Agile
- Bản chất tạo nên Agile

Nếu bạn cảm thấy thích series này, tôi rất welcome nếu bạn có thể comment ở phía dưới bài viết, để chúng ta có thể cùng thảo luận nhằm hiểu sâu hơn về chủ đề này. Ngoài ra, tôi sẽ bàn luận sâu hơn về Scrum ở phần sau nếu như bài viết này đạt nhiều hơn 50 người đọc hoặc 1 điều kiện X (X bí mật).
{% include disqus_comments.html %}
