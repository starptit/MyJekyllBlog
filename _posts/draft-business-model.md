<!-- ---
title: "Chuyện Phiếm 02: Thiên kiến kẻ sống sót - Supervivorship Bias"
categories: product
layout: article
tags: [product, mindset]
---
<p>Vì đã xác định bản thân sẽ phải đóng vai trò là Product Owner (thật ra trong quá trình vận hành, tôi thấy mình giống product manager hơn 😂), thế nên tôi phải nhìn sản phẩm dưới góc độ của product owner, chứ không thế là của General Project Manager như trước được nữa.

Ở bài viết trước tôi đã chia sẻ rằng điều đầu tiên một product owner cần phải làm là "thấu hiểu" được sản phẩm mà đội ngũ của mình đang xây dựng. Nếu ví von việc xây dựng một sản phẩm phần mềm giống như xây một cây cầu, thì trước hết, phải xác định được đối tượng phục vụ của cây cầu đó, các thông số kĩ thuật ràng buộc, và phải lên được một bản thiết kế cho nó (dạng blender hoặc prototype).

Đặc trưng của Product Owner là phải là người tư duy theo hướng kinh doanh (business oriented - điều này được quy định trong Scrum guide), thế nên trong bài viết này, tôi sẽ sử dụng một số thuật ngữ của dân kinh tế nhưng ở mức cơ bản nhất có thể để cho mọi người đều có thể hiểu được.
</p>

# Mô hình kinh doanh là gì
Trở lại với câu chuyện định hướng ACMS theo góc nhìn của product owner, có rất nhiều cách để PO có thể hoạch định và lên ý tưởng cho sản phẩm của mình, và một trong những cách phổ biến nhất là xây dựng một mô hình kinh doanh (business model).
Mô hình kinh doanh được định nghĩa đơn giản là một bản kế hoạch để sản phẩm có thể tạo ra được lợi nhuận (making profit). Nó giúp nhận diện cách thức mà sản phẩm hoặc dịch vụ sẽ được bán, ở các thị trường mục tiêu nào, bán cho tập khách hàng nào, và có những lợi thế kinh doanh cũng như thách thức gì cẩn phải đối mặt, ....
Thực chất mô hình kinh doanh không phải là điều gì xa lạ, trước giờ người ta vẫn thực hành nó, nhưng chưa chính thức gán cho nó cái nhãn mà thôi.
Mô hình kinh doanh không phải chỉ áp dụng với sản phẩm, mà nó có thể ứng dụng rất tốt ở level doanh nghiệp (dù là startup hay là doanh nghiệp đã hoạt động).
Mô hình kinh doanh còn có đặc tính là được cập nhật tùy thuộc vào các điều kiện tác động đến nó.
Tôi lấy ví dụ, mô hình kinh doanh ban đầu của Amela mọi người đều rõ là sẽ định hướng outsourcing. Tuy nhiên, ở sự kiện A-join  tháng 09/2022, anh Khoa đã công bố rất rõ rằng Amela sẽ bắt đầu xây dựng những sản phẩm của riêng mình (ACMS và Global2Me là ví dụ), và thông tin này thực chất chính là việc công bố cập nhật mô hình kinh doanh của Amela dựa trên các yếu tố về thị trường, con người, xã hội,...

Thực ra thì kiến thức về mô hình kinh doanh không mới, bạn đọc có thể tìm hiểu quyển "Business Model - Tạo lập mô hình kinh doanh ở tủ sách ở công ty". Cá nhân trong công ty, tôi thấy có bạn Yasui bên Amela Japan là có thực hành tạo lập mô hình này đẻ demo cho khách, và cũng nhận được nhiều phản hồi tích cực từ họ. Như vậy, không phải là chỉ có sản phẩm ACMS mới cần kiến thức này, mà gần như mọi sản phẩm phần mềm nào đều có thể xây dựng mô hình kinh doanh tương ứng.

# Tìm hiểu mô hình kinh doanh
Có rất nhiều yếu tố để tạo lập mô hình kinh doanh, sau cùng, người ta đúc kết và thể hiện nó dưới dạng sơ đồ (canvas), loại sơ đồ này được gọi là business model canvas.
![image.png](https://wiki-amela-production.s3.ap-southeast-1.amazonaws.com/post/wiki-1669868561-image.png)
Hình trên minh họa cho các thành phần cần phải phân tích khi tạo lập mô hình kinh doanh. Tổng cộng có 9 yếu tố đóng góp và tham gia vào quá trình xây dựng một mô hình kinh doanh. Sau đây, tôi sẽ giới thiệu sơ lược lần lượt từng yếu tố.
## Customer Segment (CS) - Phân khúc khách hàng
![image.png](https://wiki-amela-production.s3.ap-southeast-1.amazonaws.com/post/wiki-1669891275-image.png)

Yếu tố đầu tiên là phân khúc khách hàng - hiển nhiên rồi, trước khi bán sản phẩm thì phải hiểu khách hàng của mình là ai. Phải hiểu khách hàng, thì mới có thể tập trung sản phẩm phục vụ đúng nhu cầu của họ, qua đó tối đa doanh thu và lợi nhuận. Việc xác định khách hàng cần phải được thực hiện kỹ, thậm chí còn cần phải cập nhật lại khi sản phẩm đã launching (Business model có tính cập nhật). Các phân khúc khách hàng bao gồm các loại sau:
1. Mass market: thị trường đại chúng, tức là bất kỳ cá nhân phổ thông nào cũng đều có thể là khách hàng của sản phẩm. Khách hàng ở loại phân khúc này đông đảo nhất, do đó cạnh tranh cũng là lớn nhất.
2. Niche market (thị trường ngách): là phân khúc khách hàng dựa trên một đặc trưng nào đó (để phân biệt với tệp khách hàng đại chúng). Ví dụ như tệp khách hàng hạng sang, khách hàng chỉ thuộc vào 1 ngành nghế nhất định, ....
3. Multi-side market (thị trường đa chiều): là tệp khách hàng có quan hệ với nhau. Ví dụ: tiktok tạo ra một platform, các tiktoker là người phái sinh dựa trên platform đó, và sản phẩm đang xây dựng nhắm đến đối tượng là tiktoker.

Sau khi đã xác định được phân khúc và đối tượng khách hàng, thì cần phải tìm ra đặc trưng của những khách hàng này. Các đặc trưng này bao gồm:
- Kích thước của phân khúc khách hàng
- Nhu cầu hiện tại và tương lai của khách hàng
- Đặc điểm cá nhân: tuổi, giới tính, ngành nghề, sở thích, ....
- Tìm ra painpoint của họ
- Mối quan hệ với các segment khác.
## Value Propositions (VP) - Đề xuất giá trị
![image.png](https://wiki-amela-production.s3.ap-southeast-1.amazonaws.com/post/wiki-1669889772-image.png)
Đề xuất, mô tả những giá trị, mục tiêu mà sản phẩm/dịch vụ đã và sẽ đem lại cho phân khúc khách hàng kể trên. Ta có thể hiểu nôm na rằng đây là giá trị cạnh tranh chúng ta đem lại, là lý do vì sao khách hàng sẽ sử dụng sản phẩm của chúng ta, mà không phải sản phẩm khác. Ở customer segment, chúng ta đã hoạch định được chân dung khách hàng mà sản phẩm nắm tới, phân tách đặc tích cũng như nhu cầu từ họ, do đó, bước này sẽ dựa trên các thông tin hữu ích đó để xây dựng bộ các giá trị đề xuất.

## Channels (CH) - Kênh phân phối
![image.png](https://wiki-amela-production.s3.ap-southeast-1.amazonaws.com/post/wiki-1669891334-image.png)

Làm thế nào để sản phẩm có thể đến được tay khách hàng? Chính là dựa trên các kênh phân phối.
Kênh phân phối là cầu nối giữa value proposition và customer segment. Thông thường sẽ có 2 kênh phân phối chính:
1. Kênh nội bộ (ví dụ các cửa hàng trưng bày sản phẩm)
2. Kênh đối tác (ví dụ các nhà phân phối, đại lý, siêu thị)

Tuy nhiên, với các sản phẩm phần mềm, các kênh phân phối với khách hàng chủ yếu phụ thuộc mạnh vào khâu Marketing vì đặc thù của nó, và chủ yếu các kênh phân phối sẽ là các công cụ, nền tảng mạng xã hội, hoặc là các kênh kết nối trên mạng Internet.
Các kênh phân phối rất đa dạng, do đó, để xác định trong business model, một người PO cần phải nắm rõ các thủ thuật để xác định độ ưu tiên, hoặc đánh giá ưu/nhược điểm của các kênh.
## Customer Relationships (CR) -  Quan hệ khách hàng
![image.png](https://wiki-amela-production.s3.ap-southeast-1.amazonaws.com/post/wiki-1669891358-image.png)

Giống như tên gọi, đề mục này tập trung xây dựng các chiến lược và cách thức dự kiến triển khai để thắt chặt quan hệ với khách hàng, nhằm giữ chân họ và tạo ra tệp khách hàng trung thành (loyalty customer).
Bên cạnh đó, không thể bỏ qua việc tính toán các kế hoạch để tiếp cận nhiều khách hàng mới.
Về mặt nguyên lý, có khoảng 6 loại quan hệ khách hàng như sau:
1. Hỗ trợ cá nhân (personal assistance): tương tác trực tiếp với khách hàng qua một nhân viên, và người nhân viên này sẽ đi với khách hàng từ bước tư vấn, mua và sau khi đã mua sản phẩm.
2. Hỗ trợ cá nhân toàn vẹn (dedicated personal assistance):  tương tác chặt với khách hàng thông một nhóm đại diện phục vụ khách hàng. Có thể hiểu như đây là bộ phận Customer Success vậy.
3. Tự phục vụ (self-service): cung cấp các công cụ hỗ trợ chăm sóc khách, từ đó khách hàng sẽ tự phục vụ chính họ.
4. Dịch vụ tự động (automated service): tương tự như self-service, tuy nhiên kết hợp với các dữ liệu cá nhân của khách hàng, qua đó nâng cao trải nghiệm của khách hàng. Một ví dụ điển hình cho loại hình này là việc các tính năng auto-suggestions.
5. Cộng đồng (communities): tạo dựng một cộng đồng mở, nơi mọi khách hàng đều có thể truy cập và trao đổi, thảo luận, hướng dẫn sản phẩm.
6. Tương hỗ (co-creation): khách hàng cùng tham gia vào quá trình xây dựng và phát triển sản phẩm.

## Revenue Stream (RS) - Dòng doanh thu
![image.png](https://wiki-amela-production.s3.ap-southeast-1.amazonaws.com/post/wiki-1669891375-image.png)
Đã nói đến sản phẩm, và nói đến bán hàng, thì chắc chắn phải đề cập đến doanh thu. Có rất nhiều cách để tạo ra dòng doanh thu như: bán tài sản, copyright, phí sử dụng (subscription), chia sẻ phí hoa hồng (commission fee), môi giới, ...
Tuy nhiên cần phải lưu ý rằng, doanh thu không phải được đo lường 100% bằng tiền, vì mỗi sản phẩm khác nhau đều có ý nghĩa khác nhau. Ví dụ với hệ thống ACMS, hiện tại đang phát hành nội bộ miễn phí cho cả công ty, doanh thu nghiễm nhiên là 0, vậy thì sản phẩm fail à?
## Key Resources (KR) - Nguồn lực chính
![image.png](https://wiki-amela-production.s3.ap-southeast-1.amazonaws.com/post/wiki-1669891416-image.png)

Nguồn lực hay tài nguyên cần thiết để xây dựng và phát triển sản phẩm. Ở đây, có thể hiểu là nguồn lực tài chính, con người, vật lý, trí tuệ,...

Với ACMS, nguồn lực lớn nhất mà chúng tôi có là con người, tiếp đó là được đảm bảo tài chính từ công ty (dĩ nhiên không phải tài chính vô hạn, nhưng ít nhất cũng có cam kết tài chính đủ để phát triển sản phẩm).

## Key Activities (KA) - Hoạt động chính
![image.png](https://wiki-amela-production.s3.ap-southeast-1.amazonaws.com/post/wiki-1669891433-image.png)

Là các hành động quan trọng cần duy trì để ổn định và phát triển sản phẩm. Có thể hiểu rằng, các hoạt động chính này sẽ tạo ra value proposition (VP), qua đó, tạo ra dòng doanh thu (revenue stream) để khiến mô hình kinh doanh trở nên hiệu quả.
Từ góc độ quản lý, theo kinh nghiệm của tôi, nên brainstorm các hoạt động có thể nghĩ ra, sau đó sắp xếp chúng theo một độ ưu tiên nhất định, cân nhắc các tác động tương ứng và cuối cùng là bổ sung hoặc loại bỏ.
## Key Partnerships (KP) - Đối tác chính
![image.png](https://wiki-amela-production.s3.ap-southeast-1.amazonaws.com/post/wiki-1669891462-image.png)

Đối tác là những tác nhân ngoài đóng góp, hỗ trợ vào quá trình xây dựng sản phẩm. Vai trò của đối tác sẽ giúp giảm thiểu rủi ro của mô hình kinh doanh, và hợp tác để tạo ra value proposition (VP).

Vậy đối tác của ACMS là gì?
Đó chính là các division trong công ty, người hỗ trợ cung cấp resource để triển khai dự án
Đó là bộ phận truyền thông - nơi giúp lan toả thông tin và hướng dẫn các bạn nhân viên (khách hàng) có thể tiếp cạn và sử dụng sản phẩm.
....
## Cost Structure (C$) - Cơ cấu chi phí
![image.png](https://wiki-amela-production.s3.ap-southeast-1.amazonaws.com/post/wiki-1669891481-image.png)

Chi phí là những khoản đầu tư bỏ ra, tiêu tốn trong quá trình xây dựng và vận hành sản phẩm. Vì chi phí là một loại tổn thất (loss), và là một đối số để tính toán đến lợi nhuận đem lại của sản phẩm:
`Lợi nhuận = Doanh Thu - Chi Phí`
Nên chi phí cần phải được đo lường và tính toán cẩn thận, nếu chi phí quá lớn thì hiển nhiên lợi nhuận sẽ thấp, hoặc thậm chí là lỗ, ảnh hưởng trực tiếp đến thành bại của sản phẩm.
Trong thế giới kinh tế, chi phí sẽ gồm nhiều loại như: chi phí cố định (fixed cost), chi phí biến đổi (variable cost), chi phí chìm (sink cost), chi phí cơ hội (opportunity cost),...

ACMS cũng gồm nhiều loại chi phí khác nhau, tôi đơn cử:
- chi phí cố định: điện, nước, internet, văn phòng, ...
- chi phí biến đổi: nhân công (thuê các division), vận hành
- chi phí cơ hội: tại sao lại phải xây ACMS mà không tiếp tục dùng Base
....

# Lean Model Canvas
Trong vòng chục năm nay, khi mà Agile & Scrum khuấy đảo và thay đổi hoàn toàn cách thức quản trị và vận hành của các doanh nghiệp, thì Business Model Canvas cũng phát triển theo. Lean Model Canvas kế thừa và phát huy các đặc điểm của Business Model Canvas, tuy nhiên, nhìn nhận nó dưới góc độ của tư tưởng Lean - Tinh gọn (tư tưởng Lean là gì thì tôi sẽ giải thích ở bài viết trong series về Agile & Scrum).
Mô hình Lean Model Canvas phù hợp với các doanh nghiệp startup hoặc các sản phẩm mới build (như ACMS), và trên thực tế, tôi cũng lựa chọn Lean Model Canvas khi xây dựng mô hình kinh doanh cho hệ sinh thái của ACMS. Vì bản chất của chúng cũng giống nhau, và bạn hoàn toàn có thể suy luận từ Business Model canvas sang dạng Lean được, nên tôi sẽ nói khái quát và ngắn gọn về nó.
Mô hình Lean thay đổi một số trọng tâm như sau:
![image.png](https://wiki-amela-production.s3.ap-southeast-1.amazonaws.com/post/wiki-1669890147-image.png)
### Key Partnership -> Problems. 
Với những doanh nghiệp dạng startup, thì việc test ý tưởng quan trọng hơn (fail fast and fail cheap), nên trong vòng đời ngắn ngủi của mình, việc sản phẩm launching dựa hoàn toàn vào nguồn lực nội tại của đội ngũ phát triển là điều rất phổ biến. Trái lại, vì bản chất là test ý tưởng, nên cần quan tâm đến việc sản phẩm / ý tưởng đó giải quyết vấn đề (problems) gì hơn. Vì vậy mà metric problems ra đời, và theo quy ước, cũng chỉ liệt kê 3 problems mà thôi, không hơn. Vì với điều kiện hạn hẹp của các startup, không thể có đủ thời gian và nguồn lực để giải quyết tất cả problem được, thay vào đó, hãy tập trung vào những problem kinh điển nhất.

Vì tính chất bảo mật dự án, tôi không thể nói chi tiết về các vấn đề nhận biết để khởi nguyên lên sự ra đời của ACMS được. Tuy nhiên, tôi có thể bật mí, đó chính là dựa trên thực tế các hạn chế trong việc quản lý dự án, và quản lý doanh nghiệp nói chung.

### Key activities -> Solutions.
> Nêu vấn đề thì cần nêu giải pháp, nếu không thì giải quyết người nêu vấn đề.

Ở trên Lean canvas đã nêu lên vấn đề rồi, thì bây giờ phải suggest các giải pháp để thể hiện rõ vì sao mô hình kinh doanh của tôi là hiệu quả, và nó giải quyết được vấn đề gì, bằng cách nào. Về bản chất, mọi sản phẩm sinh ra đều dựa trên một hoặc nhiều giả định (assumption) của nhiều người về thị trường, về việc sản phẩm đó sẽ gãi đúng chỗ ngứa của khách hàng, và được họ tiếp nhận nồng nhiệt. Khi tạo lập mô hình kinh doanh, cần phải liệt kê và phân định các loại giải pháp đó, và về giá trị đem lại cho khách hàng. Cũng giống như problems, chỉ được phép đưa ra 3 solutions mà thôi.

### Key Resources -> Key Metrics
Với các sản phẩm dạng startup, thì nguồn lực thông thường rất hạn hẹp, hầu như chỉ có đội ngũ phát triển là chính, thế nên không cần thiết phải phân tích quá nhiều về key resources. Thay vào đó, Lean canvas gợi ý nên phân tích về "key metrics" - là các thông số, dữ liệu (metrics) định lượng hoá để đo lường mức độ thành công của sản phẩm.

Đối với ACMS, Key success metrics được đo lường thông qua:
1. lưu lượng truy cập, Daily, monthly access
2. Số lượng feedback
3. Số lượng các công việc thực hiện và hỗ trợ trong hệ thống, và ngoài hệ thống

### Customer Relationships -> Unfair Advantage
Thay đổi từ quan hệ khách hàng sang các lợi thế độc quyền. Lợi thế độc quyền là lợi thế mà chỉ mình sản phẩm đó nắm giữ, là lợi thế độc tôn giúp tăng vị thế cạnh tranh, cũng như chống đỡ trước nạn sao chép mô hình từ các sản phẩm khác.
Đối với ACMS, lợi thế cạnh tranh ở đây chính là việc bắt buộc 100% nhân viên Amela sử dụng ACMS trong công việc và hoạt động nội bộ.

Ngoài ra còn một số thay đổi nhỏ như value proposition (giá trị đề xuất) giờ biến thành Unique value proposition (giá trị đề xuất độc quyền so với các đối thủ khác)

# Bài học từ tạo lập mô hình kinh doanh
Nếu bạn nghĩ rằng việc tạo lập mô hình kinh doanh là không cần thiết, thì hãy xem thử 2 ví dụ về 2 gã khổng lồ sau.
## Starbucks business model
Mô hình kinh doanh của Starbucks là gì?
Ôi dời dễ ợt, nó là mô hình kinh doanh nhượng quyền chuỗi nhà hàng cafe (thuật ngữ gọi là franchise), nơi mà doanh thu chủ yếu đến từ việc bán cafe, cốc chén và các sản phẩm phái sinh.
Xin chúc mừng, bạn như một cái lốp xe vậy, hơi non.
![image.png](https://wiki-amela-production.s3.ap-southeast-1.amazonaws.com/post/wiki-1669891539-image.png)

Starbucks đã từng có một thời kỳ hoàng kim đáng tự hào kể từ khi Howard Schultz chính thức tham gia vào đội ngũ lãnh đạo của công ty.
Tuy nhiên, đến năm 2008, trước sự sai lệch về điều hành kèm theo sự sụp đổ của nền tài chính toàn cầu, Starbucks đã tụt dốc không phanh và suýt nữa phá sản. 
Đồ thị của nó theo đúng hình Sin như sau
![image.png](https://wiki-amela-production.s3.ap-southeast-1.amazonaws.com/post/wiki-1669884392-image.png)

Thế nhưng Starbucks đã trở lại cực kỳ mạnh mẽ trong những năm sau, và lấy lại vị thế gã khổng lồ cafe của mình. Tất cả chỉ dựa vào một thứ, đó chính là thay đổi mô hình kinh doanh.

Bạn có biết Starbucks vươn mình thành cái gì không?
Đó chính là một hình thái "ngân hàng không chính thức". Bất ngờ chưa? Cụ tỉ là thế nào?

Một trong những quyết định để đời của Starbucks là tập trung vào xây dựng nền tảng công nghệ, tiêu biểu là hệ thống thẻ thành viên (membership). Tiếp đến họ phát hành nó số hoá trên ứng dụng di động của mình. Bên cạnh việc lưu trữ thông tin thành viên, Starbucks giới thiệu hình thức tích điểm theo lần mua để nhận ưu đãi, và cho phép user nạp thẳng tiền vào tài khoản để thanh toán trong hệ sinh thái của Starbucks. Starbucks là một trong những kẻ tiên phong khai sinh ra mô hình này và giờ nó phổ biến thế nào thì ai cũng biết. Tuy nhiên, với lợi thế tiên phong, cộng thêm uy tín từ thương hiệu, có rất rất nhiều người không ngần ngại gửi tiền vào tài khoản trên ứng dụng của starbucks. Chưa hết, giá của một cốc cafe theo chiến lược luôn là số lẻ (ví dụ không bao giờ là 3$ chẵn, nó có thể là 2.95$), và điều này càng kích thích người dùng nạp nhiều vào (vì thường họ sẽ nạp số tiền chẵn). Giả sử họ nạp vào 3$, và mua cốc cafe 2.95$, vậy 50 cent dư ra đó sẽ chẳng thể dành để mua gì, mà nằm yên trong tài khoản của họ, hay chính xác là nằm yên trên tài khoản của Starbucks. (theo báo cáo của Starbucks, họ đút túi 125 triệu USD trong năm 2019, bởi chính đặc tính này của người dùng).

Ngoài ra, khách hàng khi đã nạp vào rồi thì lại rất ít có xu hướng rút ra, vì thói quen người Mỹ uống Starbucks giống như người Hà Nội trà đá vậy đó, do đó tiền cứ mãi nằm yên trong tài khoản của Starbucks mà thôi.

Vì đặc điểm này, Starbucks được coi là một dạng ngân hàng không chính thức. Trong giới tài chính, đồng tiền nằm yên là đồng tiền chết, và với nguồn lực dự trữ khủng như vậy, Starbucks hoàn toàn có thể sử dụng khoản tiền này vào các phần việc khác gia tăng lợi nhuận cho họ (tương tự các ngân hàng đem tiền của người gửi đi cho vay).

Theo báo cáo tài chính của Starbucks, hiện tại họ có khoảng 1.7 tỷ USD trữ trong tài khoản của mình. Khoản tiền nay quy ra tiền Việt thì đâu đó vào khoảng 40.000 tỷ (với tỉ giá hiện tại 1$ = 24.000 VND). Để thấy rõ mức khủng của Starbucks, thì dự trữ lớn nhất năm 2021 của các ngân hàng Việt Nam thuộc về BIDV, với con số là 29.000 tỷ (~ 73% của Starbucks)
![image.png](https://wiki-amela-production.s3.ap-southeast-1.amazonaws.com/post/wiki-1669891571-image.png)


Mặt khác, việc gửi tiền trên Starbucks không hề được hưởng lãi suất, trong khi lãi suất ở Việt Nam hiện tại đang khoảng 8-9%, thì người gửi tiền vào Starbucks lại chẳng nhận được 1 xu nào tiền lãi. Điều này đem lại rất nhiều lợi ích kinh tế cho Starbucks, vì họ dự trữ tiền gửi mà không hề phải trả lãi, vượt trội hơn hẳn so với các ngân hàng hiện tại.

## McDonald business model
Nhắc đến McDonald, chắc hẳn ai cũng liên tưởng đến những chiếc hamburger siêu rẻ, hay những chiếc đùi gà chiên cùng ít khoai tây chiên rắc kèm với ly coca tươi thơm ngon. McDonald là một trong những thương hiệu cung cấp dịch vụ thức ăn nhanh (fast food) thành công nhất toàn cầu. Vì vậy, mô hình kinh doanh của McDonald cũng là loại hình franchise nhượng quyền kinh điển ?
Lại non rồi
![image.png](https://wiki-amela-production.s3.ap-southeast-1.amazonaws.com/post/wiki-1669891598-image.png)

> Phân lô bán nền muôn đời thịnh.

Bản chất McDonald là một doanh nghiệp bất động sản, điều này được chính chủ tịch của McDonald xác nhận, lý do họ bán hamburger vì họ cho rằng nó đem lại lợi nhuận lớn và giúp các bên nhận nhượng quyền trả phí thuê mặt bằng.

Thực vậy, theo báo cáo tài chính năm 2019, tổng giá trị tài sản của McDonald trước khi trừ khấu hao (depreciation) rơi vào khoảng 39 tỷ USD, biến McDonald trở thành hãng kinh doanh bất động sản lớn thứ 5 thế giới.

Mô hình kinh doanh của họ là gì?
![image.png](https://wiki-amela-production.s3.ap-southeast-1.amazonaws.com/post/wiki-1669887923-image.png)
Đầu tiên, McDonald sẽ mua đất ở các vị trí đắc địa, đi kèm với họ là các đối tác tài chính (ngân hàng, quỹ đầu tư,...) để mua lại toàn bộ mặt bằng này. McDonald bỏ ra 1/3 số tiền, và 2/3 còn lại sẽ vay từ các đối tác tài chính, lợi nhuận từ việc bán hamburger sẽ dùng để trả lãi cho các khoản vay bất động sản. Chỉ sau vài năm, McDonald đã có thể trả hết nợ và trở thành người chủ thực sử của lô đất. Vì tính chất tăng giá qua thời gian của bất động sản, tài sản của McDonald cũng tăng theo, vì vậy họ lại càng được ưu đãi tiếp cận các khoản vay lãi suất thấp.
Mặt khác, McDonald ép buộc các cửa hàng trong chuỗi kinh doanh trên mặt bằng này, cần phải trả phí nhượng quyền và phí thuê mặt bằng (phí này còn đắt gấp rưỡi giá thị trường).
Đây là mô hình kinh doanh do chính McDonald nghĩ ra, và nó được đặt tên là mô hình kinh doanh bất động sản dòng tiền kép (từ việc thuê mặt bằng, và nhượng quyền franchise).
Theo báo cáo tài chính năm 2019, McDonald kiếm về 11,6 tỷ USD từ tiền thuê bất động sản, chiếm 64% tổng doanh thu.
# Tổng kết
Bài viết trên tôi đã cung cấp khái niệm và ý nghĩa cơ bản của việc tạo lập mô hình kinh doanh. Tôi cũng đã nêu lên tầm quan trọng của mô hình kinh doanh thông qua 2 case study của Starbuck và McDonald.
Vì lý do bảo mật thông tin dự án, tôi không thể chia sẻ sâu hơn về business model hiện tại của ACMS được. Có thể ở các phase tiếp theo, khi business model hiện tại đã lỗi thời và được bật đèn xanh từ các sếp. Tôi sẽ quay lại và cập nhật nó sau.
Dưới đây, tôi sẽ chia sẻ các template để mọi người có thể clone lại và sử dụng trong các dự án của mình.
## Draw.io
[- Business model canvas](https://app.diagrams.net/?create=https%3A%2F%2Fjgraph.github.io%2Fdrawio-diagrams%2Ftemplates%2Fbusiness%2Fbusiness_model_canvas_1.xml)
## Notion.so
[- Business model canvas](https://www.notion.so/templates/business-model-canvas)
[- Lean model canvas](https://www.notion.so/Lean-Canvas-template-81fb381d27934abbaa295bc2fb6ac6d8)

{% include disqus_comments.html %} -->
