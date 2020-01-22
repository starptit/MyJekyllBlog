---
id: 1621
title: "iOS pattern: Phần 4: Nguyên lý S.O.L.I.D (chữ L )"
date: 2017-09-12T12:19:06+00:00
author: starptit
# layout: post
guid: http://www.swiftyvn.com/?p=1621
permalink: /2017/09/ios-pattern-phan-4-nguyen-ly-s-o-l-i-d-chu-l/
tags: [Uncategorized, Swift]
---

Tiếp nối chuỗi series về nguyên lý S.O.L.I.D, bài viết này sẽ giới thiệu nguyên lý thứ 3, tạm dịch là nguyên lý thay thế Liskov (Liskov substitution principle – LSP) – chữ L. Liskov ở đây là tên riêng của một nhà khoa học máy tính người Mỹ, bà Barbara Liskov – bà đã giới thiệu về đặc tính thay thế giữa các đối tượng trong một hội nghị khoa học. Về sau, Robert C. Martin (Uncle Bob – cha đẻ của S.O.L.I.D) đã viết ra nguyên lý thứ 3 này, dựa trên phát biểu của bà Liskov, nên ông đã trân trọng lấy tên của bà để đặt cho nguyên lý.

**1. Nguyên lý thay thế Liskov là gì ?**

Luận điểm ban đầu của Barbara Liskov:

“Nếu S là subtype của T, thì T có thể dùng để thay thế S mà không làm mất đi tính đúng đắn của S”.

Được phát biểu thành:

Functions that use pointers or references to base classes must be able to use objects of derived classes without knowing it.

(Những hàm tham chiếu đến class cơ sở thì phải đảm bảo có thể sử dụng được trong các class con của nó).  
Như vậy, nguyên lý chỉ ra rằng, mọi hàm (method) của class cha thì phải hoạt động được và đúng trên các class con kế thừa từ nó. Class cho có các behaviors nào, thì class con cũng phải có các behaviors đó. Mời bạn xem ví dụ nhỏ mô phỏng từ thực tế sau đây:

{% highlight swift %}
class Bird{
    func fly(){
        // TODO: flying away
    }
}

class Eagle:Bird{
    override func fly(){
        // TODO: flying away
    }
}

class Penguin:Bird{
    override func fly(){
        //TODO: Flying away
        fatalError("Penguin cannot fly")
    }
}{% endhighlight %}

Class Bird là class cha, có ý nghĩa đại diện cho lớp chim chóc, lớp cha này có định nghĩa một function là fly, đại diện cho hành vi “bay” của loài chim. Tiếp đến, mình có 1 class con là Eagle (đại bàng) kế thừa từ class Bird, đồng nghĩa với việc Eagle có khả năng thực hiện hành vi “bay” giống như class Bird. Ok, đến đây vẫn ổn. Thế nhưng bây giờ mình tạo một class khác đặt tên là class Penguin (chim cánh cụt), hiển nhiên rằng Penguin cũng là một loài chim –> kế thừa từ class Bird –> có khả năng “bay”. Oops, trên thực tế chim cánh cụt thực ra là loài chim không thể bay –> vi phạm nguyên lý Liskov.

**2. Ví dụ về LSP trong iOS?**

Giả sử mình đang xây dựng một ứng dụng thương mại điện tử (e-commerce), cụ thể là module người sử dụng (User). Việc đầu tiên là ta cần tạo một Class User, và tiến hành phân tích nghiệp vụ cho class này, về cơ bản một user có quyền thực hiện 2 tác vụ chính là “thêm hàng vào giỏ hàng” và “thanh toán sản phẩm” :

{% highlight swift %}
class User{
    
    var userId:Int!
    var userName:String!
    var password:String!
    
    func addToCart(){ // thêm hàng vào giỏ hàng
        // TODO: add selected product to Cart
    }
    
    func proceedCart(){ // thanh toán giỏ hàng
        // TODO: pay the Cart
    }
}
{% endhighlight %}

Thiết kế trên hoàn toàn chuẩn theo như những gì sách nói, class gồm có property và method, bla bla,… Sau một thời gian sử dụng, lượng người dùng tăng lên, và có 1 số nhỏ người dùng dành tiền chi tiêu vào ứng dụng e-commerce của chúng ta, họ được xếp vào nhóm người dùng Vàng, được một số quyền hạn ưu tiên như giảm giá, tặng quà,… Công việc của chúng ta lúc này là phải chuyển hóa lượng người dùng trên vào trong ứng dụng. Sửa lại class User? Không ổn, nó đang chạy tốt, sửa lại gây ra rủi ro rất lớn. Tính kế thừa lúc này phát huy tác dụng, chúng ta chỉ cần tạo một class con kế thừa từ class trên là xong – easy as pie. Ta tạm đặt class mới là PremiumUser, có thêm thuộc tính biểu thị cho ưu đãi giảm giá:

{% highlight swift %}
class PremiumUser:User{
    
    var discount:Int! // mã giảm giá cho User
    
    override func addToCart() { // thêm hàng vào giỏ hàng
        // TODO: add selected product to Cart
        super.addToCart()
        
    }
    
    override func proceedCart() { // thanh toán giỏ hàng
        // TODO: pay the Cart with the Discount value
        
    }
}
{% endhighlight %}

Hàm addToCart() vẫn không có gì thay đổi, và tuân theo class cha User. Với hàm proceedCart(), kết quả cuối cùng của chúng ta phải thay đổi theo tỉ lệ giảm giá của User.

Việc bắt user phải có tài khoản, mật khẩu,… rồi mới được mua hàng, đặt hàng vào giỏ gây cản trở cho quá trình mua hàng của những người lần đầu tiên sử dụng app, hay họ chưa kịp đăng ký. Từ nghiệp vụ, chúng ta phải bổ sung thêm một class nữa để đại diện cho những User chưa đăng ký này. Những User này có quyền xem và thêm hàng vào giỏ, nhưng lại không thanh toán được vì không đủ thông tin:

{% highlight swift %}
class UnconfirmUser:User{
    override func addToCart() { // thêm hàng vào giỏ hàng
        // TODO: add selected product to Cart
        super.addToCart()
        
    }
    
    override func proceedCart() { // thanh toán giỏ hàng
        fatalError("missing Logic")
    }
}
{% endhighlight %}

–> vi phạm LSP. Hàm proceedCart() kế thừa từ class cha (User), không thể thực thi trong class con (UnconfirmUser).

**3. Tại sao lại cần phải tránh vi phạm LSP?**

Ta hãy đặt câu hỏi ngược lại, nếu như vi phạm LSP thì sao? Điều gì sẽ xảy ra, hoặc ảnh hưởng đến dự án thế nào?

Viêc một class con không tuân thủ theo thiết kế ban đầu của class cha có thể gây ra lỗ hổng về mặt logic, có thể khiến cho app hoạt động không đúng, cũng như gây khó khăn trong việc debug và maintain. Vì bản chất của tính kế thừa là kế thừa thuộc tính và phương thức, nhưng một số thuộc tính và phương thức ở trong trường hợp này lại không hoạt động, dẫn đến khó khăn trong việc truy tìm dấu vết. Với các dự án nhỏ hoặc các class đơn giản thì bạn có thể không cần quan tâm đến nguyên lý này, nhưng nếu với các class to hoặc kế thừa chồng (ông <- cha <- cháu,…) thì việc vi phạm LSP nguy hại hơn nhiều lần, chưa kể tình trạng chia sẻ class giữa các module, hoặc class được dùng chung hoặc được maintain bởi các thành viên trong team. **4. Làm thế nào để tránh vi phạm LSP?**

Bản chất của vi phạm LSP là do các thuộc tính và phương thức của class cha không được class con kế thừa hoàn toàn lại. Trong lập trình hướng đối tượng (OOP), có cách nào để nhiều class thực hiện lại cùng phương thức không? Đó chính là implement các Interface (với iOS là protocol). Trong ngành lập trình, có một câu nói cực kỳ nổi tiếng mà bạn buộc phải biết :

Program to an interface not an implementation  
Thật vậy, bài toán lúc này khá đơn giản, bạn tập trung các method của class cha vào các interface cụ thể, và cho class con implement (nếu có thể). Giả sử với ví dụ ban đầu về class Bird, ta có thể viết nó lại như sau:

{% highlight swift %}
protocol Flyable{
    func fly()
}

class Bird{
}

class Eagle:Bird,Flyable{
    func fly() {
        
    }
}

class Penguin:Bird{
    
}

{% endhighlight %}

Ta tách hành vi bay ra thành 1 Protocol. Với class Eagle, nó có thể bay, nên ta cho phép nó implement protocl Flyable, class Penguin không thể bay –> ta không cho nó implement. Bài toán được giải quyết, hết sức đơn giản. Tương tự với bài toán User trong hệ thống thương mại điện tử trên:

{% highlight swift %}
protocol ProceedingCart{
    func proceedCart()
}


class User{
    
    var userId:Int!
    var userName:String!
    var password:String!
    
    func addToCart(){ // thêm hàng vào giỏ hàng
        // TODO: add selected product to Cart
    }
}



class PremiumUser:User,ProceedingCart{
    
    var discount:Int! // mã giảm giá cho User
    
    override func addToCart() { // thêm hàng vào giỏ hàng
        // TODO: add selected product to Cart
        super.addToCart()
        
    }
    
    func proceedCart() { // thanh toán giỏ hàng
        // TODO: pay the Cart with the Discount value
        
    }
}


class UnconfirmUser:User{
    override func addToCart() { // thêm hàng vào giỏ hàng
        // TODO: add selected product to Cart
        super.addToCart()
        
    }
}{% endhighlight %}

**5. Tổng kết:**

Trong thực tế, chúng ta rất hay vi phạm nguyên lý LSP, hầu hết đều do suy nghĩ khi thiết kế class, đưa tư duy đời thường vào (ví dụ, rõ ràng chúng ta đều biết chim cánh cụt là lớp con của loài chim). Như mình đã trình bày ở trên, với các class nhỏ hoặc có ít class con, thì việc vi phạm LSP có thể chấp nhận được. Qua bài viết này, mình hi vọng các bạn có thể nắm bắt được cơ bản về nguyên lý LSP, và câu nói nổi tiếng mà mình đề cập ở mục 4. Thực tế, mình đã làm việc kha khá dự án, cùng kha khá người và mình để ý rằng các lập trình viên iOS khá lười viết protocol (trừ trường hợp xài delegate), việc này mình hoàn toàn không đồng ý, nhiều người thích nhét cả đống function vào một class rồi rải rác chúng ở các class khác, khiến cho việc debug và maintain rất khó khăn.

{% include disqus_comments.html %}