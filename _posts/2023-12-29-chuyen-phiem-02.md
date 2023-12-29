---
title: "Chuyện Phiếm 02: Thiên kiến kẻ sống sót - Survivorship Bias"
categories: product
layout: article
tags: [product, mindset, stories, biases]
---

<!-- Do định hướng blog là nơi chia sẻ góc nhìn và cách tôi rèn luyện khả năng diễn giải và phát biểu ý tưởng, thêm việc nhận thấy bản thân đang chậm chạp đi đáng kể (có lẽ là dấu hiệu tuổi tác), nên tôi nảy ra ý tưởng thử viết những mẩu chuyện được phác thảo và hoàn thiện trong thời gian ngắn. Những mẩu chuyện này được tổng hợp thành các series, trước mắt tôi là series chuyện phiếm.

<div style="display: flex; align-items: center; justify-content: center;">
  <img class="wp-image-1879 aligncenter" src="/assets/images/post/dorian_gray_picture.jpeg" alt="" width="600" height="400" srcset="/assets/images/post/dorian_gray_picture.jpeg" sizes="(max-width: 600px) 100vw, 320px" />
</div>
<span style="color:#993300">Thảy nghệ thuật đều vô dụng - Bức hoạ Dorian Gray (Oscar Wilde)</span> -->

# <span style="color: #ff9900;">Chuyện #1: Mặc giáp cho máy bay</span>

<p>Trong Thế Chiến II, thời điểm chiến sự giữa các phe đang diễn ra hết sức khốc liệt, các tướng lĩnh phe Đồng Minh nhận thấy tình trạng có rất nhiều máy bay chiến đấu và máy bay ném bom trở về từ chiến trường Đức với chi chít lỗ đạn. Họ hiểu rằng cần phải tìm cách gia cố thêm nhằm tăng số lượng máy bay sống sót trở về căn cứ. Tuy nhiên, không thể gia cố toàn bộ bộ phận được, bởi vì:
<ul>
  <li> Chi phí sẽ rất lớn </li>
  <li> Nếu máy bay quá nặng thì sẽ tiêu hao thêm nhiều nhiên liệu </li>
  <li> Và quá nặng thì chúng thậm chí không thể cất cạnh nổi. </li>
</ul>
</p>

Vậy bài toán đặt ra là **<span style="color:#00704A">phải lựa chọn những bộ phận, khu vực nào trên máy bay để tiến hành gia cố ?</span>**

Bài toán trên được giao cho Abraham Wald (một nhà toán học gốc Do Thái), lúc đó đang là thành viên của Nhóm nghiên cứu thống kê Mỹ (SRG).

Đầu tiên, Wald tiến hành thu thập dữ liệu, quan sát và ghi chú các mẫu máy bay trở về căn cứ. Thực tế, dựa trên dữ liệu mà ông thu thập, máy bay ném bom Mỹ bị bắn vào thân máy tới gần gấp đôi tốc độ chúng bị bắn vào nền động cơ. Phần còn lại của máy bay, bao gồm cánh, thậm chí còn nhận nhiều đạn hơn cả thân máy, và thậm chí hệ thống nhiên liệu còn bị tấn công thường xuyên hơn là động cơ của máy bay.

<div style="display: flex; align-items: center; justify-content: center;">
  <img class="wp-image-1879 aligncenter" src="/assets/images/post/sv_bias/aircraft.png" alt="" width="500" height="375" srcset="/assets/images/post/sv_bias/aircraft.png" sizes="(max-width: 600px) 100vw, 320px" />
</div>

Quyết định dường như đơn giản, theo các quan chức quốc phòng cấp cao: áp dụng lớp giáp vào những vùng thương tổn nặng nề nhất (trúng nhiều đạn nhất) như là thân máy, cánh máy bay.

Tuy nhiên, Wald cho rằng nhận định đó là sai lầm. Ông giải thích với Bộ Quốc phòng rằng điều đúng đắn cần làm là bổ sung lớp giáp vào những nơi không có lỗ đạn, thay vì áp dụng ở những nơi ghi nhận số lượng lỗ đạn cao. Tại sao?

Wald suy luận rằng dữ liệu về máy bay được thu thập từ những máy bay đã thành công trở về căn cứ để được thống kê cho cuộc nghiên cứu. Điều đó có nghĩa là chúng có thể chịu được lực bắn mạnh ở những nơi như cánh và thân máy và vẫn có thể bay. Tuy nhiên, rất ít máy bay trở về với hỏng hóc động cơ - không phải vì có rất ít máy bay bị bắn vào đó... mà vì hầu hết các máy bay bị tấn công động cơ đơn giản không bao giờ trở lại để được quan sát cả.

<div style="display: flex; align-items: center; justify-content: center;">
  <img class="wp-image-1879 aligncenter" src="/assets/images/post/sv_bias/statistic.png" alt="" width="500" height="375" srcset="/assets/images/post/sv_bias/statistic.png" sizes="(max-width: 600px) 100vw, 320px" />
</div>

Các khuyến nghị của Wald đã được áp dụng nhanh chóng, góp phần cứu sống hàng trăm phi công trong cuộc chiến, và nguyên lý này vẫn tiếp tục được áp dụng bởi Không Quân Mỹ trong hàng chục năm sau.

# <span style="color: #ff9900;">Chuyện #2: Dòng sông thử thách</span>

Trong chuyến company trip cùng Amela tháng 09 vừa rồi, tôi và nhóm bạn có tham gia trò `Dòng sông thử thách`. Đại khái là trò chơi cũng thuộc dạng chill chill, một nhóm ~ 4 người leo lên con thuyền dạng tròn như thuyền thúng vậy. Sau đó, thuyền được thả trôi theo dòng nước theo 1 hải trình khép kín, người chơi chỉ việc enjoy cái moment này thôi. Tuy nhiên, trò này còn có đặc điểm là:

1. Nước rất xiết nên bắn tung tóe mỗi khi đẩy thuyền đi.
2. Thuyền tròn, vì vậy sẽ bị xoay đủ vòng, ngoài ra còn va đập vào 2 bên thành, khiến nước bắn càng dữ hơn.

<div style="display: flex; align-items: center; justify-content: center;">
  <img class="wp-image-1879 aligncenter" src="/assets/images/post/sv_bias/dong_song_thu_thac.jpeg" alt="" width="560" height="375" srcset="/assets/images/post/sv_bias/dong_song_thu_thac.jpeg" sizes="(max-width: 600px) 100vw, 320px" />
</div>

Đúc kết lại thì trò này tuy chill, nhưng bù lại nước bắn rất nhiều (ướt hết đồ luôn).

**<span style="color:#00704A">=> Vấn đề là tôi phải lựa chọn chỗ ngồi thế nào trong 4 chỗ, để ít bị nước bắn nhất.</span>**

Đầu tiên, tôi quan sát tỉ mỉ 4 chỗ ngồi trước khi bước lên, và nhận thấy có 1 chỗ là khô ráo nhất so với 3 vị trí còn lại. Tôi tư duy rằng, vị trí khô ráo nhất tương ứng với nước bắn lên ít nhất, do đó nó là giải pháp tối ưu. Tôi nhanh chân an tọa tại vị trí mà tôi nhận định là đặc địa và tận hưởng hành trình.

Thế nhưng, đến cuối chặng, vị trí bị nước bắn lên nhiều nhất là vị trí tôi chọn, và người ướt nhiều nhất cũng chính là tôi.

<span style="color:#ff9900">Vậy, vì sao lại thế? Logic trên có lỗ hổng gì à?</span>

Sự thật là vị trí khô ráo nhất mà tôi chọn, không phải là vị trí ít nước bắn nhất, mà thật ra là bắn nước nhiều nhất, nhưng nó khô ráo bởi vì người chơi trước ngồi ở chỗ đó đã hứng hết toàn bộ nước bắn rồi. Bằng chứng là đến khi tôi đứng dậy, vị trí của tôi vẫn là khô ráo nhất, trong khi quần áo của tôi thì ướt gần hết.

Xét lại, quả thật tôi đã đi theo lối mòn thống kê như những tướng linh của phe Đồng Minh khi quan sát máy bay trúng đạn vậy, trong khi góc nhìn đúng phải giống như Wald. Tức là phải quan sát cả quan điểm vì sao tôi lại có mẫu quan sát đó.

# <span style="color: #ff9900;">Thiên kiến kẻ sống sót</span>

Hiện tượng tư duy trên gọi là thiên kiến kẻ sống sót (survivorship bias) - hiểu nôm na là chúng ta hay nhìn vào những người hay vật đã vượt qua một quy trình chọn lọc nào đó, và tin rằng những gì họ làm có tác dụng giúp họ vượt qua quy trình chọn lọc đó.

Một ví dụ cực kỳ phổ biến của thiên kiến này đó là ví dụ về các tỷ phú bỏ học. Khi nhìn vào những Steve Jobs, Mark Zuckerberg, Bill Gates,... ta dễ lầm tưởng rằng việc bỏ học rồi khởi nghiệp là dễ trở thành tỉ phú. Thế nhưng sự thật số lượng người bỏ học, khởi nghiệp và thất bại thì lại không nổi tiếng, nên ta không biết đến nó, và quan trọng là số lượng tập này mới chiếm đại đa số.

<div style="display: flex; align-items: center; justify-content: center;">
  <img class="wp-image-1879 aligncenter" src="/assets/images/post/sv_bias/leave-school-they-said.png" alt="" width="320" height="560" srcset="/assets/images/post/sv_bias/leave-school-they-said.png" sizes="(max-width: 600px) 100vw, 320px" />
</div>

Ví dụ khác, bạn đã bao giờ nghe đến danh sách những quyền sách mà tỷ phú hay đọc kiểu "7 thói quen bạn trẻ thành thụ", "Hút cần cùng Tonybuoitoi", "Tôi tài giỏi, bạn đ' thế", ... chưa? Nhiều người nghe xong sẽ lầm tưởng rằng họ chỉ cần đọc theo những đầu sách đó của người thành đạt, thì họ cũng sẽ thành đạt, nhưng không hề biết hàng tá người khác cũng đọc sách / thói quen tương tự mà không hề thành đạt. Tôi thật sự cạn lời khi đọc tin ông bố chuẩn bị tủ sách này cho con 5 tuổi.

<div style="display: flex; align-items: center; justify-content: center;">
  <img class="wp-image-1879 aligncenter" src="/assets/images/post/sv_bias/list_sach.png" alt="" width="400" height="800" srcset="/assets/images/post/sv_bias/list_sach.png" sizes="(max-width: 600px) 100vw, 320px" />
</div>

Thiên kiến này được tận dụng cực tốt bởi các nhà marketing đại tài. Ví dụ, đợt trước Youtube tràn lan các quảng cáo thuốc của ông A, bà B đã dùng và khỏi bệnh để minh chứng cho thuốc hiệu quả, trong khi thuốc không hề được chứng nhận bởi cơ quan Y tế nào cả. Điều này gây lầm tưởng cho người bệnh rằng, tôi chỉ cần uống thuốc là tôi sẽ khỏi như ông A, bà B, trong khi không biết thuốc họ đang sử dụng có thật sự an toàn và hiệu quả hay không.

<span style="color:#ee0033">Vậy, làm thế nào để tránh thiên kiến kẻ sống sót?</span>

Nguyên tắc đơn giản nhất, đừng vội tin những gì bạn đang thấy. Cụ thể, cần phải suy ngẫm những trường hợp khác thì sao?

> Warren Buffett thành công vì ông bắt đầu đầu tư chứng khoán từ năm 11 tuổi, thế nên chúng ta hãy đầu tư sớm.

Ừ đúng rồi, nhưng làm thế nào mà một **thằng nhóc 11 tuổi có đủ tiền và tư cách pháp nhân để mua được chứng khoán** thì không ai nói.

{% include disqus_comments.html %}
