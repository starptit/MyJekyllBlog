---
id: 1738
title: "iOS pattern: Phần 7: Inversion of Control"
date: 2018-06-01T16:54:59+00:00
author: starptit
layout: post
guid: http://www.swiftyvn.com/?p=1738
permalink: /2018/06/ios-pattern-phan-7-inversion-of-control/
categories: [Uncategorized, Swift]
---

Ở 6 phần trước, mình đã lần lượt trình bày cho các bạn bộ nguyên tắc S.O.L.I.D. Để tiếp nối chủ đề này, bài viết hôm nay sẽ giới thiệu một nguyên lý khác cũng khá phổ biến không kém S.O.L.I.D, và được áp dụng rất rất nhiều. Đó chính là nguyên lý _**Inversion Of Control**_<!--more-->

# _Inversion of Control_

Trước khi đi vào vấn đề chính, hãy thử trả lời câu hỏi sau:

Bạn làm gì vào ngày cuối tuần?

Đi cafe, chơi Dota, đọc sách, xem phim, picnic, quay tay,&#8230;

Vậy còn ngày thường thì sao?

Do hợp đồng lao động, bạn phải đi làm và có mặt lúc 8h, code, ăn trưa 1 tiếng, họp, báo cáo,&#8230;.

=> Bạn có nhận thấy điểm khác biệt ? Chính là khả năng _điều khiển lịch hoạt động_ trong ngày.

Vào ngày cuối tuần, bạn được tự do lựa chọn, còn ngày thường thì sao? Bạn không còn tự quyết định, lịch hoạt động của bạn phụ thuộc vào chỉ thị của người khác &#8211; sếp của bạn. Có thể nói, lịch trình của bạn đã bị đảo ngược, từ tự điều khiển sang bị điều khiển.

# _Inversion of Control Là Gì?_

**Inversion of Control (IoC)** tạm dịch là đảo ngược điều khiển, vậy đảo ngược điều khiển của cái gì ?

Đó chính là luồng (flow control) của ứng dụng.

Thuật ngữ này lần đầu tiên được đề cập trong quyển ***Design Patterns: Elements of Reusable Object-Oriented Software,*** về sau được **Martin Fowle**r bàn luận trong blog của mình. Theo như **Martin Fowler**, IoC là kiến thức trừu tượng, ông lý giải bằng việc chỉ ra sự khác biệt giữa Framework và Library: Code của chúng ta sẽ gọi Library để thực thi, còn Framework thì thực thi và gọi ngược code của chúng ta.

# _Ví Dụ Về IoC:_

Với framework _UIKit_ của iOS, giả sử với bài toán, ấn một cái nút, và in ra dòng &#8216;Hello World&#8217; :

<pre class="theme:solarized-dark toolbar:2 plain:false lang:default decode:true ">let button = UIButton()
button.addTarget(self, action: #selector(buttonTapped(_:)), for: .touchUpInside)

func buttonTapped(_ sender: Any) {
    print("Hello World")
}</pre>

Có nhận xét gì về đoạn code trên ?

Khi User tap vào nút, UIKit sẽ nắm bắt sự kiện này, xử lý, và sau đó sẽ in ra dòng chữ &#8220;Hello World&#8221; bằng việc gọi code của bạn thông qua hàm buttonTapped(\_:).

_Đúng, code của bạn được gọi_. Đó chính là điểm khác biệt của framework: xây dựng xương sống, điều khiển luồng bên trong, và gọi code của bạn khi cần.

Ví dụ khác, chắc chắn ai cũng đã và đang sử dụng UITableView, thế nhưng bạn có từng để ý đến cách mà chúng ta làm việc với nó không?

<pre class="theme:solarized-dark toolbar:2 plain:false lang:default decode:true ">extension ViewController: UITableViewDelegate, UITableViewDataSource {
    func numberOfSections(in tableView: UITableView) -> Int {
       return 1
    }
    
    func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        return userList.count
    }
    
    func tableView(_ tableView: UITableView, heightForRowAt indexPath: IndexPath) -> CGFloat {
        return UITableViewAutomaticDimension
    }
    
    func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        let reuseCell: UITableViewCell = tableView.dequeueReusableCell(withIdentifier: "reuseCell")!
        return reuseCell
    }
    
    func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath) {
        print("tapped")
    }
}</pre>

Hãy quan sát theo hướng luồng điều khiển:

UITableView khi khởi tạo, gọi đến numberOfSection, numberOfRow, khi chuẩn bị renderCell, sẽ gọi đến cellForRow, wilDisplayCell,&#8230; . Bạn có điều khiển gì về cách nó render, nó lấy dữ liệu như thế nào, nó điền dữ liệu đó vào đâu không?

Rõ ràng là không, bạn đơn thuần chỉ định nghĩa các thông tin dựa trên UITableViewDataSource mà thôi. Việc gọi thế nào và khi nào được gọi, hoàn toàn nằm ở UIKit và UITableView <=> quyền điều khiển không phải là ở bạn.

Chính từ ví dụ về Framework này, Martin Fowler đã kết luận hóm hỉnh: &#8220;Don&#8217;t call us, we will call you&#8221;. Kết luận trên còn được biết đến với tên gọi là Holloywood&#8217;s Principle (định luật Hollywood), vì vậy khi tìm hiểu các tài liệu tham khảo, bạn sẽ rất dễ thấy định luật trên xuất hiện. (Định luật Hollywood bắt nguồn từ việc tuyển diễn viên của các nhà làm phim Hollywood, được dùng ở đây vì là cách chơi chữ tiếng Anh).

# _Ý Nghĩa Của IoC?_

Ý nghĩa lớn nhất của IoC là giảm kết dính (decoupling). Hãy thử nhìn lại 2 ví dụ trên, khi quyền điều khiển không còn nằm ở phía bạn, đồng nghĩa với việc bạn không cần phải quan tâm và không có trách nhiệm với những gì đang hoạt động bên trong. Qua đó, nếu lỗi hoặc sửa đổi phát sinh ở phía nào, bạn chỉ việc sửa đổi ở phía đó, không làm ảnh hưởng đến những chỗ khác.

Đặc điểm và ý nghĩa này khiến cho nhiều người cho rằng, IoC là một trong những cách để thể hiện nguyên lý Dependency Inversion (phần 6).

<p style="text-align: center;">
  <a href="http://206.189.90.168/wordpress/wp-content/uploads/2018/06/ioc-and-mapper-in-c-6-638.jpg"><img class="size-full wp-image-1750 aligncenter" src="http://206.189.90.168/wordpress/wp-content/uploads/2018/06/ioc-and-mapper-in-c-6-638.jpg" alt="" width="638" height="479" srcset="/wp-content/uploads/2018/06/ioc-and-mapper-in-c-6-638.jpg 638w, /wp-content/uploads/2018/06/ioc-and-mapper-in-c-6-638-300x225.jpg 300w" sizes="(max-width: 638px) 100vw, 638px" />(Nguồn ảnh: Google)</a>
</p>

Theo mình, D.I.P tập trung vào vấn đề Dependency, nghĩa là giữa module cấp cao và cấp thấp với nhau, còn IoC thì tập trung vào vấn đề luồng dữ liệu (flow control), do đó không đúng khi nói IoC là một cách để đảm bảo D.I.P. Bản thân Martin Fowler cũng từng nói IoC  là nguyên lý tổng quát, ông thể hiện nó thông qua ServiceLocator cùng với Dependency Injection pattern, chứ không bàn luận về Dependency Inversion. Mặt khác, mình không tìm thấy tài liệu nào đủ sức thuyết phục để chứng minh hoặc phủ nhận mối liên hệ giữa D.I.P và IoC. Do đó, quan điểm cá nhân của mình không thừa nhận IoC là con của D.I.P như biểu đồ trên.

# _Thực Hiện IoC?_

Để thực hiện IoC, chúng ta có thể sử dụng một số pattern sau:

- Delegate
- Template Method
- Service Locator
- Dependency Injection
- &#8230;

Delegate mình đã trình bày rồi, bạn có thể tìm đọc lại. Hiệu quả của delegate được thể hiện rõ nhất thông qua ví dụ về UITableViewDataSource & UITableViewDelegate kể trên.

Template Method, để tránh hiểu nhầm, mình sẽ trình bày ở series về Design Pattern sau này.

Service Locator & Dependency Injection là 2 design pattern phổ biến và đặc trưng để minh họa cho IoC, cụ thể mình sẽ trình bày trong bài viết tới.

Chú ý, ở đây là Dependency Injection, chứ không phải là Inversion nhé, đừng nhầm lẫn.

# _Kết Luận_

Rút ra được gì qua bài viết?

- IoC là gì?
- Định luật HollyWood
- IoC làm gì
- IoC và D.I.P

IoC trừu tượng và tổng quát, gây rối cho khá nhiều người khi tìm hiểu. Thế nhưng IoC lại cực kỳ phổ biến trong ngành lập trình, việc nắm bắt và vận dụng được nó luôn luôn cần thiết. Một số framework nổi tiếng áp dụng ý tưởng từ IoC: Spring (java), Unity (C#),&#8230;.

Mọi thứ đều có 2 mặt, IoC không phải là hoàn toàn tốt, áp dụng quá đà IoC có thể khiến project của bạn rối rắm, và khó nắm bắt được luồng hoạt động. IoC thường được tiếp cận thông qua tìm hiểu các pattern như: Dependency Injection, Service Locator,&#8230;  (đã được liệt kê ở trên, và sẽ được trình bày ở những bài viết sau).

Cám ơn các bạn đã dành thời gian đọc bài !

Tài liệu tham khảo:

- https://martinfowler.com/articles/injection.html#ConstructorInjectionWithPicocontainer
- https://martinfowler.com/bliki/InversionOfControl.html
- https://en.wikipedia.org/wiki/Inversion\_of\_control

&nbsp;
