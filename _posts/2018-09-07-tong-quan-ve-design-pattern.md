---
id: 1801
title: Tổng quan về Design Pattern
date: 2018-09-07T09:05:23+00:00
author: starptit
layout: post
guid: http://swiftyvn.com/?p=1801
permalink: /2018/09/tong-quan-ve-design-pattern/
categories:
  - Uncategorized
---
Ra đời từ những năm 70 của thế kỉ trước, thực sự trở nên nổi tiếng và phổ biến thông qua cuốn sách &#8220;Design Patterns: Elements of Reusable Object-Oriented Software&#8221; (viết bởi 4 tác giả Erich Gamma, Richard Helm, Ralph Johnson và John Vlissides, còn được biết đến với tên gọi Gang of Four &#8211; GoF), Design Pattern dần dần trở thành tiêu chuẩn và là kiến thức buộc phải biết của mọi lập trình viên. Tôi chắc chắn rằng bạn đã từng nghe thuật ngữ này nhiều lần: khi tìm kiếm tài liệu, trong các cuộc thảo luận, trong các topics, quyển sách về lập trình,&#8230; Điều đó chứng minh tính hữu dụng và độ phổ biến của Design Pattern.

Vậy Design Pattern là gì? Nó có đặc điểm gì? Cần tìm hiểu nó như thế nào? Có những điều gì cần lưu ý khi nghiên cứu nó ?

Những câu hỏi trên tôi sẽ cố gắng giải đáp trong bài viết này &#8211; bài viết mở đầu cho series về Design pattern trong Swift.

<!--more-->

### **<span style="color: #d93829;">Design Pattern là gì?</span>**

Trong lĩnh vực phần mềm, <span style="color: #3366ff;"><em><strong>Design Pattern</strong></em></span> là tên gọi chung để chỉ các giải pháp giúp giải quyết những vấn đề cụ thể trong thiết kế phần mềm. Design dịch ra là thiết kế, còn Pattern là khuôn mẫu &#8211;> Design Pattern có thể là bản mô tả, là template, concept,&#8230; phục vụ mục đích thiết kế phần mềm hợp lý và hiệu quả. Design Pattern được xây dựng thông qua mồ hôi và kinh nghiệm đúc kết của hàng tá lập trình viên, dựa trên bài toán và giải pháp thực tế của họ.

Ngành phần mềm có rất nhiều kiểu lập trình: _functional programming, procedural programming, object-oriented programming_,&#8230; Mỗi kiểu đó đều có các loại Design Pattern khác nhau. Trong phạm vi bài viết về đề tài iOS và ngôn ngữ Swift, mình chỉ giới hạn nội dung cho chủ đề Design Pattern thu gọn trong kiểu lập trình hướng đối tượng (object-oriented programming).

Design Pattern trong OOP thường biểu thị mối quan hệ và tương tác giữa Class, Object với nhau (Class với Object, Class với Class, Object với Object, &#8230;), dựa trên 2 nguyên lý thiết kế đối tượng nổi tiếng mà mình đã trình bày trong series S.O.L.I.D:

  * **Program to an interface not implementation** ( Lập trình hướng đến các Interface và tính trừu tượng).
  * **Object Composition over inheritance** (Sử dụng Composition thay vì Inheritance &#8211; kế thừa).

Nếu bạn quên thì không sao, hãy cố gắng ghi nhớ 2 nguyên lý này, và đọc tiếp các phần sau của series, chắc chắn mình sẽ còn nhắc lại nó, để các bạn có thể hiểu và thấy được mối liên hệ giữa chúng với các design patterns.

<span style="color: #3182d9;"><em><strong>==> Tóm lại, mình cần bạn nhớ:</strong></em></span>

  1. Design Pattern là template, concept,&#8230; hoặc chỉ đơn giản cung cấp một phương pháp thiết kế phần mềm.
  2. Design Pattern có liên quan chặt chẽ đến 2 nguyên lý thiết kế đối tượng: về interface và về composition ở trên.

### <span style="color: #d93829;"><strong>Phân loại Design Pattern</strong></span>

Có bao nhiêu Design Pattern? Rất rất nhiều, tương đương với việc có rất nhiều cách để phân loại, và cũng không thể đảm bảo có phương pháp phân loại nào có thể phân loại được hết các Design Pattern. Tuy nhiên, tần suất và độ phổ biến của các design pattern lại khác nhau, vì lẽ đó, người ta thường nhặt các design patterns phổ biến hơn ra, và cố gắng phân loại chúng. Trong quyển sách mình đề cập ở phần giới thiệu, các tác giả (4 tác giả GoF) đã nêu ra 23 loại design pattern khác nhau, và phân loại chúng thành 3 loại: Creational, Structural, Behavioral. Về sau, sinh ra thêm nhiều patterns khác, tuy nhiên cách phân thành 3 loại như trước đây vẫn được tôn trọng và tuân theo.<figure id="attachment_1805" style="width: 955px" class="wp-caption aligncenter">

<img class="wp-image-1805 size-full" src="http://swiftyvn.com/wp-content/uploads/2018/09/Untitled.png" alt="" width="955" height="457" srcset="http://swiftyvn.com/wp-content/uploads/2018/09/Untitled.png 955w, http://swiftyvn.com/wp-content/uploads/2018/09/Untitled-300x144.png 300w, http://swiftyvn.com/wp-content/uploads/2018/09/Untitled-768x368.png 768w" sizes="(max-width: 955px) 100vw, 955px" /> <figcaption class="wp-caption-text">(Source: smarttechie.org)</figcaption></figure> 

&nbsp;

##### <span style="color: #3182d9;"><em><strong>Creational:</strong></em></span>

Tập trung vào bài toán khởi tạo object một cách trừu tượng. Loại này gồm các patterns:

  * Singleton Pattern
  * Factory Pattern
  * Builder Pattern
  * Lazy Initialization Pattern
  * Prototype Pattern
  * &#8230;

##### <span style="color: #3182d9;"><em><strong>Structural:</strong></em></span>

Tập trung vào bài toán liên kết và quan hệ giữa các Class, Object. Loại này gồm các patterns:

  * Adapter Pattern
  * Bridge Pattern
  * Decorator Pattern
  * Façade Pattern
  * Proxy Pattern
  * Flyweight Pattern
  * &#8230;.

##### <span style="color: #3182d9;"><em><strong>Behavioral:</strong></em></span>

Tập trung vào giải quyết bài toán giao tiếp giữa các Object. Loại này gồm các patterns:

  * Iterator Pattern
  * Chain of Responsibility Pattern
  * Command Pattern
  * Memento Pattern
  * &#8230;.

Trong series của mình, tôi sẽ điều chỉnh nội dung và đề cập đến những Design Pattern mà tôi cho là cần thiết và có thường gặp đối với lập trình viên iOS. Cụ thể là pattern nào, chúng ra sao, xin hẹn trình bày ở các bài viết sau.

_**<span style="color: #3182d9;">==> Tóm lại, bạn cần nhớ:</span>**_ Design pattern phổ biến được chia làm 3 loại: Creational, Structural, Behavioral. Bên trong mỗi loại bao gồm nhiều design pattern khác nữa.

Fun fact: MVC, MVVM, V.I.P.E.R, MVP, Redux,&#8230; là gì? Chúng thường được biết đến đại điện cho kiến trúc hệ thống, nhưng thật ra, chúng có thể coi là Architectural Pattern, và đúng vậy, cũng có thể coi chúng là design pattern ( thực tế có khá nhiều bài viết và tài liệu đề cập chúng như là design pattern). Tuy nhiên chúng không thuộc loại nào trong 3 loại trên, do đó, mong các bạn hiểu rõ về thực chất của sự phân loại này.

### **<span style="color: #d93829;">Nghiên Cứu Design Pattern Cần Kiến Thức Gì?</span>**

##### _**<span style="color: #3182d9;">Kiến thức về OOP</span>**_

Chúng ta đang bàn về Design Pattern trong OOP, hiển nhiên rằng kiến thức, tư duy về OOP là điều bắt buộc. Trước hết, bạn cần hiểu, nắm bắt, và vận dụng được những đặc trưng và tính chất của lập trình hướng đối tượng. Rất nhiều Design Pattern, thực chất chỉ là cách vận dụng các tính chất của OOP một cách mềm dẻo và linh hoạt. Tôi khuyến khích các bạn nên rà soát lại kiến thức của mình về OOP cẩn thận, cần hiểu rõ tính chất trừu tượng, đa hình, composition,&#8230;

Tôi đã từng phỏng vấn một số lập trình viên, họ đều nói rằng họ biết và có thể vận dụng Design Pattern được, tuy nhiên khi tôi đề cập đến vấn đề OOP, họ đều trả lời rất mơ hồ và không rõ ràng. Cách hiểu đó tôi e rằng, mới chỉ là phần ngọn, vì khá nhiều Design pattern được viết theo lối áp đặt, tức là khiến người đọc lầm tưởng rằng nó là cố định, là template không thay đổi. Vì vậy, cá nhân tôi vẫn chân thành khuyên các bạn nên tìm hiểu thật kĩ OOP.

##### <span style="color: #3182d9;"><em><strong>Biết cách đọc Diagram</strong></em></span>

Design Pattern trong OOP là template, concept phục vụ cho vấn đề thiết kế, chẳng có gì dễ hiểu và trực quan để nhìn nhận và nghiên cứu thiết kế bằng việc vẽ, thể hiện nó dưới dạng sơ đồ (Diagram) cả. Biểu đồ thường được dùng để minh họa cho Design Pattern có tên gọi Sơ đồ Lớp (Class Diagram).<figure id="attachment_1803" style="width: 917px" class="wp-caption aligncenter">

<img class="wp-image-1803 size-full" src="http://swiftyvn.com/wp-content/uploads/2018/09/12-uml-class-diagram-example.png" alt="" width="917" height="436" srcset="http://swiftyvn.com/wp-content/uploads/2018/09/12-uml-class-diagram-example.png 917w, http://swiftyvn.com/wp-content/uploads/2018/09/12-uml-class-diagram-example-300x143.png 300w, http://swiftyvn.com/wp-content/uploads/2018/09/12-uml-class-diagram-example-768x365.png 768w" sizes="(max-width: 917px) 100vw, 917px" /> <figcaption class="wp-caption-text">(Source: visual-paradigm.com)</figcaption></figure> 

Ngoài lề chút, bạn cũng nên tìm hiểu về các UML Diagram khác (Class Diagram là 1 trong các UML Diagram).

Bộ não con người học hỏi tốt hơn nếu biết vận dụng 2 bán cầu, do đó cách tìm hiểu thông qua các Diagram luôn là cách tốt và đáng vận dụng (trong mọi lĩnh vực luôn nhé). Việc hiểu biết Diagram còn giúp bạn dễ dàng trao đổi và thảo luận ý kiến, mô hình với các developer khác.

##### _**<span style="color: #3182d9;">Đọc hiểu và tìm tài liệu</span>**_

Tài liệu về Design Pattern thì vô số, mình mới đọc một ít và chọn ra một số quyển khá ổn:

  * Sách Design Patterns: Elements of Reusable Object-Oriented Software (dĩ nhiên, quyển này là bất hủ)
  * Sách Pro Design Patterns in Swift
  * Sách Swift Design Patterns.
  * Sách Design Pattern của Ray Wenderlich
  * [Series Design Pattern của AppCoda](https://www.appcoda.com/design-pattern-creational/)
  * [Series Design Pattern của Ray Wenderlich](https://www.raywenderlich.com/477-design-patterns-on-ios-using-swift-part-1-2)
  * [Tutorial Design Pattern của Tutorialspoint](https://www.tutorialspoint.com/design_pattern/index.htm)

### <span style="color: #d93829;"><strong>Lưu Ý Về Design Pattern</strong></span>

##### _**<span style="color: #3182d9;">Đừng trói buộc Design Pattern</span>**_

Design Pattern là template, concept, nhưng thực hiện nó thế nào là ở bạn. Đừng tư duy bó hẹp nó vào một mô hình cụ thể, cái này mình đã từng gặp trong thời gian đầu tìm hiểu.

Design Pattern chỉ là một cách để giải quyết vấn đề thiết kế, và nó không phải là cách duy nhất. Do đó, bạn cần thực sự tỉnh táo và linh hoạt, nếu bạn là team lead, nên xem xét và cân nhắc các giải pháp hoặc pattern khác nữa, dựa trên kinh nghiệm của team members và vấn đề thực tế.

##### <span style="color: #3182d9;"><em><strong>Đừng ảo tưởng về Design Pattern</strong></em></span>

Vấn đề này thường gặp ở những người mới làm quen và thuần thục một vài Design Pattern. Bạn thường có xu hướng tưởng tượng rằng Design Pattern là tất cả, là GOD, nhưng thực sự không phải vậy. Design Pattern cũng có nhược điểm của nó, ví dụ như nó khiến thiết kế của bạn trở nên rối rắm và khó debug hơn ( cũng tương tự như S.O.L.I.D), hoặc bản thân Design Pattern đó cũng đã có nhược điểm, nhưng người ta vẫn sử dụng vì ưu điểm của nó vượt trội so hơn với mặt nhược. Trường hợp hay gặp nhất là áp dụng bừa bãi Singleton Pattern vào source code, điều này gây nên nhiều technical dept mà người sử dụng không hề hay biết (cụ thể tôi sẽ trình bày ở những bài viết sau).

Nên nhớ, có design pattern, thì cũng có Anti-pattern.

### **<span style="color: #d93829;">Kết Luận</span>**

Qua bài viết, bạn cần hiểu được: Tổng quan về Design Pattern, Phân Loại nó như thế nào, và cần lưu ý gì khi nghiên cứu và ứng dụng nó. Design Pattern không phải là tất cả, nhưng lại là một chủ đề quan trọng và thường xuyên được đem ra mổ xẻ, trao đổi trong ngành phần mềm. Nó không phải là viên đạn bạc (silver-bullet), nhưng nó được đúc kết dựa trên kinh nghiệm hàng chục năm của nhiều lập trình viên. Mặt khác, nó cung cấp những giải pháp giúp thiết kế phần mềm an toàn, hiệu quả, giảm thiểu bug, chi phí bảo trì phát sinh. Bởi vậy, bạn nên tìm hiểu nghiên cứu nó ngay đi. À mà tìm hiểu nó cần gì ấy nhỉ? OOP và UML Diagram là 2 thứ không thể không học.

P.s: Nếu nội dung bài viết có lỗi nào, hoặc bạn muốn tôi viết OOP và UML Diagram, thì hãy cứ mạnh dạn để lại comment, hoặc gửi tin nhắn inbox cho tôi. Tôi sẽ feedback ngay khi có thể.

&nbsp;