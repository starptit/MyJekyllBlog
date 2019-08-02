---
id: 1870
title: Builder Design Pattern
date: 2019-05-10T10:11:33+00:00
author: starptit
layout: post
guid: http://swiftyvn.com/?p=1870
permalink: /2019/05/builder-design-pattern/
categories:
  - Uncategorized
---

Đợt vừa rồi tôi có hơi bận viết blog nội bộ cho công ty nên có hơi bỏ bê trang này, nhưng không sao, SwiftyVN đã trở lại và đương nhiên là series về Design Pattern cũng sẽ quay lại 🤘. Vẫn tiếp nối chuỗi bài viết về loại Creational (khởi tạo), và cũng vẫn là một trong những pattern thuộc hàng phổ thông nhất, đó chính là **<span style="color: #993300;">Builder Design Pattern.</span>**

<img class="aligncenter wp-image-1878" src="/wp-content/uploads/2019/05/xfa1323749768.jpg" alt="" width="600" height="399" srcset="/wp-content/uploads/2019/05/xfa1323749768.jpg 800w, /wp-content/uploads/2019/05/xfa1323749768-300x200.jpg 300w, /wp-content/uploads/2019/05/xfa1323749768-768x511.jpg 768w" sizes="(max-width: 600px) 100vw, 600px" />

<!--more-->

### <span style="color: #ff9900;">Builder Design Pattern là gì?</span>

Trong OOP, <span style="color: #993300;"><strong>Builder pattern</strong></span> thuộc loại **<span style="color: #993300;">creational</span>** (khởi tạo), chính vì vậy mục tiêu chính sẽ nhằm giải quyết vấn đề liên quan đến việc khởi tạo đối tượng. Cụ thể hơn, Builder pattern sẽ chia nhỏ **_construction_** (khởi tạo) của một object phức tạp. Tôi giữ nguyên từ construction không phải để khoe tiếng Anh, mà hãy để ý thêm chút, construction có khiến bạn liên tưởng đến cái gì trong OOP không? Đó chính là constructor (hàm khởi tạo), vì lẽ  đó, phương pháp chia nhỏ của Builder pattern sẽ liên quan đến constructor trong Class. Builder pattern đặt logic và cấu hình mặc định (default configuration) liên quan đến việc khởi tạo object từ class ra bên ngoài, vào trong Builder class. Đặt ra ngoài thế nào, builder class và chi tiết ra sao? Xin mời đọc tiếp.

### <span style="color: #ff9900;">Nó giải quyết vấn đề gì?</span>

Để trả lời cho câu hỏi ở đề mục, hãy cùng tôi xem xét bài toán sau:

Giả sử tôi đang tạo chương trình quản lý cho quán trà sữa, một trong những core function trong ứng dụng của tôi đó là lấy yêu cầu đặt trà sữa từ khách hàng và lập hóa đơn thanh toán cho họ:

<img class="wp-image-1879 aligncenter" src="http://swiftyvn.com/wp-content/uploads/2019/05/BFV41761_DeliciousAsianDrinks_FBFINAL_v5-1024x1024.jpg" alt="" width="300" height="300" srcset="http://swiftyvn.com/wp-content/uploads/2019/05/BFV41761_DeliciousAsianDrinks_FBFINAL_v5-1024x1024.jpg 1024w, http://swiftyvn.com/wp-content/uploads/2019/05/BFV41761_DeliciousAsianDrinks_FBFINAL_v5-150x150.jpg 150w, http://swiftyvn.com/wp-content/uploads/2019/05/BFV41761_DeliciousAsianDrinks_FBFINAL_v5-300x300.jpg 300w, http://swiftyvn.com/wp-content/uploads/2019/05/BFV41761_DeliciousAsianDrinks_FBFINAL_v5-768x768.jpg 768w, http://swiftyvn.com/wp-content/uploads/2019/05/BFV41761_DeliciousAsianDrinks_FBFINAL_v5.jpg 1080w" sizes="(max-width: 300px) 100vw, 300px" />

<!-- <pre class="theme:xcode plain:false plain-toggle:false lang:swift decode:true"> -->

{% highlight swift %}
public class MilkTea {
private let taste: String // vị trà sữa: peach, origin, orange, kumquat,...
private let size: String // S-M-L
private let toppings: [String] // coconut, ....
private let sugarPercent: Double // phần trăm đường: 100% - 80% - 50 %
private let icyPercent: Double // phần trăm đá 100% - 80% - 50 %
  
 init(taste: String,
size: String,
toppings: [String],
sugarPercent: Double,
icyPercent: Double) {
self.taste = taste
self.size = size
self.toppings = toppings
self.sugarPercent = sugarPercent
self.icyPercent = icyPercent
}
}
{% endhighlight %}

<!-- </pre> -->

Có nhận xét gì về đoạn code trên:

- Constructor (hàm init) khá phức tạp.
- Sẽ luôn có thuộc tính ít cần giá trị mặc định: ví dụ: Size &#8211; M, 100% đường, 100% đá,&#8230;

Vì có những thuộc tính mặc định ít thay đổi, do đó không tránh khỏi việc phải lặp:

{% highlight swift %}

let bigOrigin = MilkTea(taste: "Origin", size: "L", toppings: [], sugarPercent: 1.0, icyPercent: 1.0)

let smallOriginDecreaseSuger = MilkTea(taste: "Origin", size: "M", toppings: [], sugarPercent: 0.5, icyPercent: 1.0)

let bigOriginWithToppings = MilkTea(taste: "Origin", size: "L", toppings: ["coconut"], sugarPercent: 1.0, icyPercent: 1.0)
{% endhighlight %}

Duplicate thật xấu xí, và không khi nào là tốt cả. Do đó, người ta sử dụng Builder Pattern.

### <span style="color: #ff9900;">Dùng nó thế nào?</span>

Vẫn theo format cũ, trước khi đi vào cụ thể, hãy tạm dừng để ngó qua Class Diagram của nó đã:

<img class="size-large wp-image-1874 aligncenter" src="http://swiftyvn.com/wp-content/uploads/2019/05/Untitled-Diagram-1024x320.png" alt="" width="768" height="240" srcset="http://swiftyvn.com/wp-content/uploads/2019/05/Untitled-Diagram-1024x320.png 1024w, http://swiftyvn.com/wp-content/uploads/2019/05/Untitled-Diagram-300x94.png 300w, http://swiftyvn.com/wp-content/uploads/2019/05/Untitled-Diagram-768x240.png 768w, http://swiftyvn.com/wp-content/uploads/2019/05/Untitled-Diagram.png 1314w" sizes="(max-width: 768px) 100vw, 768px" />

Phân tích Diagram trên:

1. **<span style="color: #993300;">Director</span>**: đại diện cho class / module cần kết quả từ việc khởi tạo MilkTea.
2. **<span style="color: #993300;">Builder</span>**: thiết kế trừu tượng cho các Builder, phục vụ cho việc Director có thể tương tác mà không cần quan tâm đến implementation của nó là gì. Mục đích typehint / swap / hoán đổi implementation mà không ảnh hưởng đến Director.
3. **<span style="color: #993300;">MilkTeaBuilder</span>**: class implement InterfaceBuilder, có nhiệm vụ khởi tạo Object MilkTea, thông qua hàm build().
4. **<span style="color: #993300;">MilkTea</span>**: object cần để khởi tạo.

Để đơn giản hóa và vì mục đích demo, nên tôi sẽ loại bỏ `interface Builder`. Như vậy, Director thay vì tương tác trực tiếp với MilkTea, thì giờ sẽ tương tác thông qua **<span style="color: #993300;">MilkTeaBuilder</span>**:

{% highlight swift %}

public final class MilkTeaBuilder {
private var taste: String = "origin"
private var size: String = "M"
private var toppings: [String] = []
private var sugarPercent: Double = 1.0
private var icyPercent: Double = 1.0
  
 public func chooseTaste(taste: String) { self.taste = taste }
public func chooseSize(size: String) { self.size = size }
public func addTopping(topping: String) { self.toppings.append(topping) }
public func chooseSugarPercent(percent: Double) { self.sugarPercent = percent }
public func chooseIcyPercent(percent: Double) { self.icyPercent = percent }
  
 public func build() -&gt; MilkTea {
return MilkTea(taste: taste,
size: size, toppings: toppings,
sugarPercent: sugarPercent,
icyPercent: icyPercent)
}
}

class Order {
let customerName: String
let products: [MilkTea]
  
 init(customerName: String, products: [MilkTea]) {
self.customerName = customerName
self.products = products
}
}

let milkTeaBuilder = MilkTeaBuilder()

// Customer 1
let customer1Name = "Shaw Vu"
milkTeaBuilder.chooseTaste(taste: "Peach")
milkTeaBuilder.chooseSize(size: "L")
let product1 = milkTeaBuilder.build()

let order1 = Order(customerName: customer1Name, products: [product1])

// Customer 2
let customer2Name = "Swifty VN"
milkTeaBuilder.chooseTaste(taste: "Origin")
milkTeaBuilder.chooseSize(size: "M")
let order2 = Order(customerName: customer2Name, products: [milkTeaBuilder.build()])
{% endhighlight %}

Order ở đây nắm vai trò tương đương Director trong Diagram trên. Rõ ràng, việc khởi tạo MilkTea với thông số mặc định đã đơn giản, gọn nhẹ hơn rất nhiều phải không? Và đó chính là cách viết Builder tuân theo Builder Design Pattern, không có gì to tát hay khó khăn.

Cách thực hiện trên bản chất là chia nhỏ các properties của MilkTea ra thành các getter, setter được thiết lập trong class Builder, và sau đó tuần tự lần lượt thực hiện set giá trị cho chúng (chooseTaste,  chooseSize, addTopping,&#8230;), rồi khởi tạo object thông qua hàm build().

Nghe thật đơn giản nhi? Đọc tiếp đi.

### <span style="color: #ff9900;">Có gì chú ý?</span>

Được rồi, dừng lại tại đây, hãy dành 5 phút cuộc đời để đọc và ngẫm nghĩ lại bài viết này từ đầu, bạn có nhận ra điều gì không?

Nếu như tôi nhận được Pull Request kiểu này từ các thành viên trong team, tôi sẽ chẳng ngần ngại mà close và bắt người đó phải xóa đi viết lại ngay lập tức.

Thực tế mà nói, chủ đề Builder Pattern nhan nhản trên mạng, bạn có thể search 1 lúc, sẽ thấy cả tá bài viết với lối mòn như tôi vừa làm. Lý do tôi yêu cầu bạn dành 5 phút đọc lại bài viết là vì tôi muốn bạn có thể phản biện được cách xây dựng Builder Pattern của tôi. (Trong thời đại thông tin bùng nổ này, thiết nghĩ tư duy phản biện và phân tích thông tin là cực kỳ quan trọng, vì vậy, tôi hi vọng bạn cũng nên dừng lại và phân tích nội dung các thông tin mà mình kiếm được)

Okay, đi hơi xa rồi đó, cách làm trên thay vì được khuyến khích, trái lại trở thành **<span style="color: #ff0000;">Anti-pattern</span>**, tức là nên tránh làm theo. Lý giải cho điều này, vâng, xin mời bạn đọc tiếp.

(Builder Pattern xây dựng theo cách trên thực ra thường dùng để tránh vấn đề <span style="color: #993300;"><strong><em>Telescoping Initializer / Telescoping Constructor</em></strong><span style="color: #000000;">)</span></span>

<span style="color: #339966;"><em><strong>Telescoping Initializer</strong></em></span>

Telescoping Initializer là trường hợp khi một Class có quá nhiều initializer / constructor theo định dạng kiểu như sau:

{% highlight swift %}
public class MilkTea {
private let taste: String // vị trà sữa: peach, origin, orange, kumquat,...
private let size: String // S-M-L
private let toppings: [String] // coconut, ....
private let sugarPercent: Double // phần trăm đường: 100% - 80% - 50 %
private let icyPercent: Double // phần trăm đá 100% - 80% - 50 %
  
 init(taste: String,
size: String,
toppings: [String],
sugarPercent: Double,
icyPercent: Double) {
self.taste = taste
self.size = size
self.toppings = toppings
self.sugarPercent = sugarPercent
self.icyPercent = icyPercent
}
  
 init(taste: String) {
self.taste = taste
self.size = "M"
self.toppings = []
self.sugarPercent = 1.0
self.icyPercent = 1.0
}
  
 init(taste: String, size: String) {
self.taste = taste
self.size = size
self.toppings = []
self.sugarPercent = 1.0
self.icyPercent = 1.0
}
  
 init(size: String) {
self.taste = "origin"
self.size = size
self.toppings = []
self.sugarPercent = 1.0
self.icyPercent = 1.0
}
  
 ....
}
{% endhighlight %}

Nên nhớ, Builder Pattern được giới thiệu lần đầu từ cuốn sách của Gang of Four, ngôn ngữ họ sử dụng là C++, và lại xuất bản từ 30-40 năm trước. Swift là ngôn ngữ hiện đại, vấn đề Telescoping Initializer này không còn là trở ngại nữa, tương đương với cách xây dựng Builder Pattern mà tôi đã cất công trình bày là vô dụng.

<span style="color: #339966;"><strong><em>Anti-pattern</em></strong></span>

Telescoping Initializer không còn là vấn đề -> Builder Pattern như trên vô dụng -> không cần thiết -> anti-pattern. Swift cung cấp feature <span style="color: #ff0000;"><strong><code>default parameters</code></strong></span>, và nhờ vào feature này, chúng ta hoàn toàn có thể loại bỏ Builder:

{% highlight swift %}
public class MilkTea {
private let taste: String // vị trà sữa: peach, origin, orange, kumquat,...
private let size: String // S-M-L
private let toppings: [String] // coconut, ....
private let sugarPercent: Double // phần trăm đường: 100% - 80% - 50 %
private let icyPercent: Double // phần trăm đá 100% - 80% - 50 %
  
 init(taste: String = "origin",
size: String = "M",
toppings: [String] = [],
sugarPercent: Double = 1.0,
icyPercent: Double = 1.0) {
self.taste = taste
self.size = size
self.toppings = toppings
self.sugarPercent = sugarPercent
self.icyPercent = icyPercent
}
}

MilkTea(taste: "peach")
MilkTea(size: "L")
MilkTea(taste: "Kumquat", size: "S", toppings: [])
{% endhighlight %}

<span style="color: #339966;"><em><strong>Builder Pattern trong Swift là vô dụng?</strong></em></span>

Câu trả lời là không. Tôi muốn trình bày kĩ vì bản thân tôi cũng bị ngáo ngơ khi tìm hiểu về Builder trong Swift, vì như trên, các tài liệu trên mạng thường trùng lặp và hướng người đọc vào vấn đề Telescoping &#8211; vấn đề thường gặp ở các ngôn ngữ cổ điển.

Cái hay của Builder ở nằm ở việc giảm thiểu sự phức tạp khi khơi tạo Object, thông qua hàm <span style="color: #993300;"><code>build() -&gt; Type</code></span> &#8211; bản chất là việc đóng gói quá trình khởi tạo này lại, bạn có thể thực hiện các logic, làm abcxyz gì đó, rồi mới trả về Object sau cùng. Đặc điểm quan trọng này là lý do chính khiến Builder Pattern vẫn đã và đang được ứng dụng trong Swift iOS.

### <span style="color: #ff9900;">Ứng dụng trong iOS?</span>

Challenge 1 chút, có ví dụ đơn giản nào mà constructor của class phức tạp không?

Đó chính là trường hợp Constructor Dependency Injection:

{% highlight swift %}

class ViewController: UIViewController {

    init(apiService: IAPIService,
         databaseService: IDBService) {

    }

}

class ViewControllerBuilder {

    func build() -&gt; ViewController {
        let apiService = APIService(alamofire, environment)
        // do stuff
        let dbService = DBService()

        return ViewController(
            apiService: apiService,
            databaseService: dbService
        )
    }

}
{% endhighlight %}

Có rất nhiều dependencies phức tạp, theo kiểu khởi tạo dựa theo các dependency khác, đồng nghĩa với việc không thể sử dụng default parameters. Hơn nữa, vì nó phức tạp, cho nên chúng ta nghĩ đến việc tách riêng nó ra để xử lý, và Builder là một trong những cách tiếp cận đáng xem xét.

Tư tưởng Builder được áp dụng trong module Router / Navigator / Coordinator trong các dự án iOS, ví dụ: Router trong kiến trúc V-I-P-E-R, hoặc RIBs (hàng của UBer), Alamofire / Moya,&#8230;.

{% highlight swift %}
Source: https://gist.github.com/jazzbpn/afd9f178fe4d8a212d83750e1b4a5389#file-viper-noticerouter-swift // Router in VIPER architectur

class NoticeRouter:PresenterToRouterProtocol{
  
 static func createModule() -&gt; NoticeViewController {
  
 let view = mainstoryboard.instantiateViewController(withIdentifier: "MyViewController") as! NoticeViewController
  
 let presenter: ViewToPresenterProtocol & InteractorToPresenterProtocol = NoticePresenter()
let interactor: PresenterToInteractorProtocol = NoticeInteractor()
let router:PresenterToRouterProtocol = NoticeRouter()
  
 view.presentor = presenter
presenter.view = view
presenter.router = router
presenter.interactor = interactor
interactor.presenter = presenter
  
 return view
  
 }
  
 static var mainstoryboard: UIStoryboard{
return UIStoryboard(name:"Main",bundle: Bundle.main)
}
  
 func pushToMovieScreen(navigationConroller navigationController:UINavigationController) {
  
 let movieModue = MovieRouter.createMovieModule()
navigationController.pushViewController(movieModue,animated: true)
  
 }
  
}
{% endhighlight %}

{% highlight swift %}// Uber/RIBs - Router example

protocol RootBuildable: Buildable {
func build() -&gt; LaunchRouting
}

final class RootBuilder: Builder&lt;RootDependency&gt;, RootBuildable {

    override init(dependency: RootDependency) {
        super.init(dependency: dependency)
    }

    func build() -&gt; LaunchRouting {
        let viewController = RootViewController()
        let component = RootComponent(dependency: dependency, rootViewController: viewController)
        let interactor = RootInteractor(presenter: viewController)

        let loggedOutBuilder = LoggedOutBuilder(dependency: component)
        let loggedInBuilder = LoggedInBuilder(dependency: component)
        return RootRouter(interactor: interactor,
                          viewController: viewController,
                          loggedOutBuilder: loggedOutBuilder,
                          loggedInBuilder: loggedInBuilder)
    }

}
{% endhighlight %}

### <span style="color: #ff9900;">Kết luận</span>

Builder Design Pattern tuy là pattern đơn giản và dễ thực hiện, nhưng trong Swift, nó vẫn hoàn toàn có thể là anti-pattern như tôi đã phân tích ở trên. Tôi vẫn luôn khuyến khích bạn đọc tiếp cận được với tư duy và ý tưởng của Pattern hơn là cách implement của nó.  Không nên áp dụng một pattern nào đó chỉ vì có người bảo rằng bạn nên làm vậy.

Tóm lại, qua bài viết này, tôi cần bạn phải nắm được:

- Builder Pattern là gì? Tư tưởng của nó là gì?
- Thực hiện Builder Pattern như thế nào?
- Telescoping initializer và trường hợp Builder pattern trở thành anti-pattern
- Người ta đang sử dụng Builder Pattern như nào?

Cám ơn các bạn đã dành thời gian đọc đến tận dòng này.

Tham khảo:

- Prodesign Pattern in Swift
- Design Pattern by Tutorial
- https://gist.github.com/jazzbpn/afd9f178fe4d8a212d83750e1b4a5389#file-viper-noticerouter-swift
- https://github.com/uber/RIBs/wiki/iOS-Tutorial-2
- https://github.com/Alamofire/Alamofire/blob/master/Documentation/AdvancedUsage.md
