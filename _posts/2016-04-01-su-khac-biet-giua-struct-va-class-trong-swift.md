---
id: 78
title: Sự khác biệt giữa Struct và Class trong Swift
date: 2016-04-01T14:22:04+00:00
author: starptit
layout: post
guid: https://devislifeblog.wordpress.com/?p=78
permalink: /2016/04/su-khac-biet-giua-struct-va-class-trong-swift/
categories:
  - Uncategorized
---
Struct (cấu trúc) và Class(lớp) trong Swift có nhiều điểm tương đồng với nhau, Apple đã mô tả sự tương đồng giữa chúng như sau:

<div class="page" title="Page 141">
  <div class="layoutArea">
    <div class="column">
      <p>
        &#8220;Classes and structures are general-purpose, flexible constructs that become the building blocks of your program&#8217;s code. You define properties and methods to add functionality to your classes and structures by using the already familiar syntax of constants, variables, and functions.&#8221;
      </p>
      
      <p>
        Khái niệm về Struct và Class không mới, 2 khái niệm này xuất hiện trong ngôn ngữ lập trình bậc trung  và ngôn ngữ hướng đối tượng như C/C++. Tuy nhiên, Struct và Class trong Swift lại có chút khác biệt, đặc biệt là Struct. Struct trong C/C++ chỉ có property và function, còn trong Swift, Struct được nâng cấp thêm nhiều feature mới, gần gũi với Class hơn.
      </p>
      
      <p>
        <!--more-->
      </p>
      
      <p>
        Chúng ta có thể liệt kê một số điểm giống nhau giữa Struct và Class trong Swift như sau:
      </p>
      
      <ul>
        <li>
          Properties: struct và class đều có property (thuộc tính).
        </li>
        <li>
          Method: cả struct và class đều có method (phương thức).
        </li>
        <li>
          Initializier: struct và class hỗ trợ các phương thức khởi tạo mặc định, hoặc các phương thức khởi tạo tuỳ chỉnh theo mục đích và logic của lập trình viên.
        </li>
        <li>
          Subscript: Struct và class hỗ trợ các subscript syntax (câu lệnh con bên trong một thuộc tính, hoặc một hàm).
        </li>
        <li>
          Extension: Extension là khái niệm mới trong Swift, nó giúp lập trình viên có thể mở rộng các struct, hoặc class sẵn có hoặc đã được xây dựng từ trước.
        </li>
      </ul>
      
      <p>
        <img class="alignnone size-full wp-image-80" src="https://devislifeblog.files.wordpress.com/2016/04/screen-shot-2016-03-23-at-13-23-58.png" alt="Screen Shot 2016-03-23 at 13.23.58.png" width="914" height="1062" srcset="http://swiftyvn.com/wp-content/uploads/2016/04/screen-shot-2016-03-23-at-13-23-58.png 914w, http://swiftyvn.com/wp-content/uploads/2016/04/screen-shot-2016-03-23-at-13-23-58-258x300.png 258w, http://swiftyvn.com/wp-content/uploads/2016/04/screen-shot-2016-03-23-at-13-23-58-768x892.png 768w, http://swiftyvn.com/wp-content/uploads/2016/04/screen-shot-2016-03-23-at-13-23-58-881x1024.png 881w" sizes="(max-width: 914px) 100vw, 914px" />
      </p>
      
      <p>
        Chắc chắn, không có nhà phát triển ngôn ngữ nào lại tạo ra 2 định nghĩa cùng một mục đích và giống nhau hoàn toàn cả,  giữa struct và class phải có điểm riêng biệt và khác biệt so với cái còn lại. Chính những khác biệt này là điểm quan trọng đem đến cho lập trình viên nhiều lựa chọn hơn khi quyết định sử dụng struct hay class. Vậy khác biệt đó là gì?
      </p>
      
      <ul>
        <li>
          Type (kiểu): struct là value type còn class là reference type.
        </li>
        <li>
          Inheritance (kế thừa): Struct không thể kế thừa, còn class thì có thể ( hiển nhiên &#8211; OOP mà).
        </li>
        <li>
          Deinitializers: Struct không có hàm huỷ (destructor trong java/C++), chỉ có hàm khởi tạo initializer (constructor trong java/C++), còn Class thì có đầy đủ
        </li>
        <li>
          Multiple reference (đa tham chiếu): chúng ta có thể có nhiều đối tượng cùng tham chiếu đến 1 class instance, còn ở struct thì không thể (vì nó là value type mà).
        </li>
      </ul>
      
      <p>
        Ở trên có nói đến Value type, và reference type. Vậy nó là cái gì?
      </p>
      
      <p>
        Trên thế giới có rất nhiều mô hình lập trình (programming paradigm), giả sử, chúng ta học code ban đầu, từ print hello world ở C/C++, viết các hàm riêng , kết hợp các lệnh goto, while -loops, if else,&#8230; đơn giản nhét vào một khối các lệnh ,&#8230; đó là kiểu lập trình cơ bản nhất, gọi là lập trình kiểu cấu trúc (structure programming). Hiện tại, có 2 kiểu lập trình cực kỳ phổ biến trên thế giới, đó là Object-Oriented Programming (hướng đối tượng) và Functional Programming (lập trình chức năng). Các Class trong OOP sử dụng dạng tham chiếu &#8211; ánh xạ bộ nhớ, còn trong Functional Programming, chúng lại sử dụng cách copy và release. Điều này có ý nghĩa cực kì quan trọng, quan trọng thế nào thì hãy xem hình sau.
      </p>
      
      <p>
        <img class="alignnone size-full wp-image-82" src="https://devislifeblog.files.wordpress.com/2016/04/screen-shot-2016-03-23-at-14-14-40.png" alt="Screen Shot 2016-03-23 at 14.14.40.png" width="1382" height="688" srcset="http://swiftyvn.com/wp-content/uploads/2016/04/screen-shot-2016-03-23-at-14-14-40.png 1382w, http://swiftyvn.com/wp-content/uploads/2016/04/screen-shot-2016-03-23-at-14-14-40-300x149.png 300w, http://swiftyvn.com/wp-content/uploads/2016/04/screen-shot-2016-03-23-at-14-14-40-768x382.png 768w, http://swiftyvn.com/wp-content/uploads/2016/04/screen-shot-2016-03-23-at-14-14-40-1024x510.png 1024w" sizes="(max-width: 1382px) 100vw, 1382px" />
      </p>
      
      <p>
        Tại sao cùng code mà kết quả lại khác nhau? Đó chính là vì đặc điểm giữa struct và class. Struct COPY và TẠO MỚI, còn class thì GIỮ THAM CHIẾU. Thêm một ví dụ nữa:
      </p>
      
      <p>
        <img class="alignnone size-full wp-image-83" src="https://devislifeblog.files.wordpress.com/2016/04/screen-shot-2016-03-23-at-15-04-59.png" alt="Screen Shot 2016-03-23 at 15.04.59.png" width="1380" height="1078" srcset="http://swiftyvn.com/wp-content/uploads/2016/04/screen-shot-2016-03-23-at-15-04-59.png 1380w, http://swiftyvn.com/wp-content/uploads/2016/04/screen-shot-2016-03-23-at-15-04-59-300x234.png 300w, http://swiftyvn.com/wp-content/uploads/2016/04/screen-shot-2016-03-23-at-15-04-59-768x600.png 768w, http://swiftyvn.com/wp-content/uploads/2016/04/screen-shot-2016-03-23-at-15-04-59-1024x800.png 1024w" sizes="(max-width: 1380px) 100vw, 1380px" />
      </p>
      
      <p>
        Chúng ta có thể thấy rõ ràng, khi dòng lệnh chạy trong hàm changeName, property &#8220;name&#8221; của cả struct và class đều thay đổi tương ứng. Nhưng đến khi ra khỏi hàm, property &#8220;name&#8221; trong struct vẫn giữ nguyên giá trị, trong khi class lại thay đổi ??? Tại sao lại như vậy??? Lý do rất đơn giản, Struct không hề truyền địa chỉ của mình, mà thay vào đó, hàm changeName sẽ copy lại myStruct truyền vào. Đến khi hàm kết thúc, giá trị copy đó bị release đi, và nó không hề ảnh hưởng đến myStruct truyền vào.
      </p>
      
      <p>
        Chúng ta có thể tưởng tượng như sau, chúng ta có 1 quyển sách, và bạn của chúng ta muốn đọc nó. Vậy, chúng ta có những cách nào để chia sẻ cho bạn bè quyển sách đó??? Cách thứ nhất, chúng ta đem quyển sách của chính ta cho họ mượn, còn cách thứ 2, chúng ta photo copy ra 1 bản, và đưa bản copy đó cho bạn bè mượn. Bây giờ xảy ra tình huống như thế này: bạn chúng ta đọc được một đoạn rất thú vị, liền dùng bút nhớ để đánh dấu nó lại. Nếu chúng ta chọn cách thứ nhất, vết đánh dấu sẽ lưu mãi trong quyển sách, và mỗi lần ta đọc nó, ta đều thấy vết đó. Còn cách thứ 2, vết đánh dấu chỉ xuất hiện ở quyển copy của bạn, còn quyển của chính ta đang đọc thì không sao hết, không có vết đánh dấu nào.
      </p>
      
      <p>
        Ở đây, Class đại diện cho cách thứ 1 (reference type), còn Struct đại diện cho cách thứ 2 (value type).
      </p>
      
      <p>
        Ok như vậy là chúng ta đã xong phần quan trọng nhất để phân biệt struct và class trong swift. Struct trong swift cực kì mạnh mẽ, các kiểu dữ liệu như String, Int, Double,&#8230; đều xây dựng từ Swift. Việc sử dụng Struct hay Class tuỳ thuộc vào mục đích và logic của chúng ta. Struct hiện tại đang được sử dụng khá rộng rãi, thậm chí hệ thống server như GO sử dụng toàn bộ cấu trúc Struct. Điểm mạnh lớn nhất của Struct so với Class đó chính là quản lý bộ nhớ. Vì Struct toàn bộ là copy rồi release nên không bị retain cycle giống Class, do đó đem lại tối ưu bộ nhớ dễ dàng hơn. Ngoài ra, việc tuân theo nguyên lý của Functional Programming còn giúp cho Struct không bị &#8220;State change&#8221; (state change chính là ví dụ cuối cùng ở trên).
      </p>
    </div>
  </div>
</div>

&nbsp;