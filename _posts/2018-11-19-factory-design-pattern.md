---
id: 1822
title: Factory Design Pattern
date: 2018-11-19T10:36:19+00:00
author: starptit
# layout: post
guid: http://swiftyvn.com/?p=1822
permalink: /2018/11/factory-design-pattern/
tags: [Uncategorized, Swift]
---

Một trong những design pattern mà quyển sách nào cũng đề cập, đó chính là Factory Pattern, điều đó đã chứng minh sự phổ biến của nó. Nếu bạn còn nhớ, ở bài viết trước, tôi có chia nhóm các loại design pattern khác nhau, bao gồm Creational, Structural và Behavioral. Factory Pattern thuộc loại Creational, do đó, vấn đề và nó giải quyết sẽ xoay quanh câu chuyện khởi tạo object, instantiation,&#8230; vân vân và mây mây. Bài viết này tương đối dài và nhiều chữ, thế nên hãy cố gắng kiên nhẫn đọc đến cuối nhé, vì theo tôi, đây là một pattern đơn giản, nhưng lại hỗn loạn về thông tin bậc nhất.

Bài viết này nói về gì?

<p style="padding-left: 60px;">
  I. Vài điều về Factory: Cung cấp khái niệm cơ bản về Factory, đặc điểm, tác dụng,&#8230;
</p>

<p style="padding-left: 60px;">
  II. Simple Factory: cách thức đơn giản nhất để áp dụng Factory.
</p>

<p style="padding-left: 60px;">
  III. Factory Method: design pattern chính thức, cách thực hiện nó, ưu điểm của nó,&#8230;
</p>

<p style="padding-left: 60px;">
  IV. Nhận xét và kết luận: tổng kết lại bài viết + nhận xét theo quan điểm của tác giả.
</p>

&nbsp;

## <span style="color: #00ccff;">I. Vài điều về Factory</span>

Factory là object, function hoặc method có nhiệm vụ khởi tạo nên các object khác, có nghĩa là, return của nó sẽ là 1 instance của 1 object khác.

_<span style="color: #ff0000;"># Tại sao chúng ta lại cần phải có factory ?</span>_

Đi tìm câu trả lời cho câu hỏi trên cũng chính là việc đi tìm ý nghĩa: tại sao chúng ta lại cần phải sử dụng một Object,function,&#8230; để khởi tạo nên instance khác?

#### Giảm tính kết dính

Giả sử bạn đang phải viết tính năng ghi log cho database, theo cách thông thường và đơn giản nhất, bạn sẽ viết như sau:

{% highlight swift %}
public struct DatabaseLogger {
    public func writeLog(content: String) {
        // TODO: write log
    }
}

class CreateUserViewController: UIViewController {
    func writeUserLog(log: String) {
        let logger = DatabaseLogger()
        logger.writeLog(content: log)
    }
}{% endhighlight %}

Nhưng điều gì sẽ xảy ra, nếu như team bạn nhận thấy log database không thực sự cần thiết, và muốn chuyển sang ghi log phần Networking?

{% highlight swift %}
public struct DatabaseLogger {
    public func writeLog(content: String) {
        // TODO: write log
    }
}

public struct NetworkingLogger {
    public func writeLog(content: String) {
        // TODO: write Networking Log
    }
}

class CreateUserViewController: UIViewController {
    func writeUserLog(log: String) {
//        let logger = DatabaseLogger()
        let logger = NetworkingLogger()
        logger.writeLog(content: log)
    }
}
{% endhighlight %}

Bạn phải thay thế hoặc chỉnh sửa những phần liên quan đến DatabaseLogger cũ, và vì Logger là function được sử dụng phổ biến trong ứng dụng, do đó bạn phải sửa đổi ở mọi nơi liên quan, điều này không hề dễ chịu gì phải không?

Với Factory, mọi việc trở nên đơn giản hơn:

{% highlight swift %}
public protocol ILogger {
    func writeLog(content: String)
}

public struct LoggerFactory {
    static func createLogger() -> ILogger {
//        return DatabaseLogger()
        return NetworkingLogger()
    }
}

public struct DatabaseLogger: ILogger {
    public func writeLog(content: String) {
        // TODO: write log
    }
}

public struct NetworkingLogger: ILogger {
    public func writeLog(content: String) {
        // TODO: write Networking Log
    }
}

class CreateUserViewController: UIViewController {
    func writeUserLog(log: String) {
        let logger = LoggerFactory.createLogger()
        logger.writeLog(content: "Log something")
    }
}{% endhighlight %}

Việc khởi tạo ra Logger để sử dụng hoàn toàn nằm ở FactoryLogger, do đó, nếu cần sửa, chúng ta chỉ cần sửa ở mình nó mà thôi, tránh được hoàn toàn tình huống phải sửa ở nhiều chỗ kể trên.

#### Che giấu việc khởi tạo phức tạp

Bản chất của Factory là return lại 1 instance, vì vậy, cái phức tạp cần che giấu được nói đến ở đây chính là che giấu đi cái việc khởi tạo ra instance đó. Vậy tại sao lại phải che giấu ? Hãy xét ví dụ sau:

Giả sử tôi đang thiết kế ứng dụng hẹn hò tương tự như Tinder, tôi muốn xây dựng module đưa ra gợi ý kết bạn cho User, việc đưa ra gợi ý được tùy chọn dựa trên danh sách các tiêu tiêu chí.

{% highlight swift %}
struct SuggesstMatching {

    init(user: User, list: PropertyList) {
    
    }
    
    func suggesst() -> [User] {
        // To Do: find and suggest user
        return []
    }
}

class HomeViewController: UIViewController {
    func suggestFriend() {
        let user = User()
        let propertyList = PropertyList()

        let suggestMatching = SuggesstMatching(user: user, list: propertyList)
        let suggestingUser = suggestMatching.suggesst()
    }
}

class FavoriteViewController: UIViewController {
    
    func findFriend() {
        let user = User()
        let propertyList = PropertyList()
        
        let suggestMatching = SuggesstMatching(user: user, list: propertyList)
        let suggestingUser = suggestMatching.suggesst()
    }
}
{% endhighlight %}

SuggestMatching là module đảm nhận business logic, User đại diện cho người dùng, PropertyList đại diện cho danh sách tiêu chí. Module này được sử dụng ở Favorite & HomeViewController để tìm ra danh sách gợi ý kết bạn. Vậy có vấn đề gì với những dòng code này ?

- Việc khởi tạo SuggestMatching module bị lặp lại.
- Rất có thể PropertyList sau này cập nhật và thay đổi, do đó có nguy cơ khá cao có thể phải sửa lại code.
- Ở góc nhìn của Home & FavoriteViewController, chúng hoàn toàn không quan tâm đến việc khởi tạo SuggestMatching.

&#8211;> Rõ ràng SuggestMatching được khởi tạo phức tạp, hơn nữa 2 ViewController lại không cần quan tâm đến cái phức tạp đó. Nếu sử dụng Factory, bài toán trên sẽ có dạng như sau:

{% highlight swift %}
struct SuggesstMatchingFactory {
    static func getSuggestMatching() -> SuggesstMatching {
        let user = User()
        let propertyList = PropertyList()
        
        return SuggesstMatching(user: user, list: propertyList)
    }
}

class HomeViewController: UIViewController {
    func suggestFriend() {
        let suggestMatching = SuggesstMatchingFactory.getSuggestMatching()
        let suggestingUser = suggestMatching.suggesst()
    }
}{% endhighlight %}

Việc làm thế nào để lấy ra SuggestMatching sẽ do Factory đảm nhiệm, tương đương với việc sửa đổi cũng chỉ nằm gọn trong cái Factory đó, các class / module khác cần thì chỉ việc gọi ra để dùng, đơn giản, thuận tiện và dễ quản lý hơn.

Một vấn đề khác mà Factory có thể giải quyết được:

{% highlight swift %}
struct SuggesstMatching {

    init(user: User, list: PropertyList) {}

    init(user1: User, user2: User) {}
    
    init(user: User, place: String) {}
    
    init(user: [User]) {}
    
    func suggesst() -> [User] {
        // To Do: find and suggest user
        return []
    }
}
{% endhighlight %}

Giả sử SuggestMatching có rất nhiều kiểu để instantiate, việc viết gọn vào Factory chắc chắn là một giải pháp tốt. Chưa kể đến những trường hợp cần kết hợp nhiều dependency để tạo ra 1 instance, các dependency đó lại có thêm nhiều kiểu để khởi tạo &#8211;> độ phức tạp sẽ tăng theo hàm mũ, và Factory sẽ giúp bạn ít đau đớn hơn khi phải sửa đổi chúng.

## <span style="color: #00ccff;"><strong>II. Bài toán thực tế:</strong></span>

Tôi đang phát triển tính năng cập nhật thông tin người dùng, trong đó có phần cập nhật địa chỉ (quận, huyện, tỉnh thành) nơi họ sinh sống. Tôi sẽ có 2 cách chính để lấy thông tin tỉnh thành sẵn có: lấy từ File, lấy từ Database.

{% highlight swift %}
struct Place {
    private let id: Int
    private let name: String
    
    public init(id: Int, name: String) {
        self.id = id
        self.name = name
    }
}

struct FilePlaceConnector {
    func getPlaceList() -> [Place] {
        // load File System
        // get Place list from Files
        return placeListFromFile
    }
}

struct DatabaseConnector {
    func loadPlaceListFromDatabase() -> [Place] {
        // setup DB connection
        // query to get Place list
        
        return placeDatabaesList
    }
}{% endhighlight %}

Thế nhưng, Hà Tây sát nhập vào Hà Nội, rồi Việt Nam thống nhất Hoàng Sa, Trường Sa, dẫn đến team của tôi quyết định thêm phần lấy thông tin địa chỉ từ API để sửa đổi real-time dễ dàng hơn. Theo như những phân tích ở trên, sử dụng Factory ở trường hợp này là cần thiết và hợp lý. Tuy nhiên, sử dụng như thế nào ?

## <span style="color: #00ccff;"><strong>III. Simple Factory</strong></span>

Cách đầu tiên là sử dụng một thủ thuật gọi là Simple Factory, cụ thể:

<img class="size-full wp-image-1830 aligncenter" src="/wp-content/uploads/2018/11/Untitled-Diagram-2.png" alt="" width="974" height="296" srcset="/wp-content/uploads/2018/11/Untitled-Diagram-2.png 974w, /wp-content/uploads/2018/11/Untitled-Diagram-2-300x91.png 300w, /wp-content/uploads/2018/11/Untitled-Diagram-2-768x233.png 768w" sizes="(max-width: 974px) 100vw, 974px" />

{% highlight swift %}
enum ConnectionType {
    case file
    case api
    case database
}

protocol PlaceConnectorProtocol {
    func loadPlaceList() -> [Place]
}

struct FilePlaceConnector: PlaceConnectorProtocol {
    func loadPlaceList() -> [Place] {
        // load File System
        // get Place list from Files
        return placeListFromFile
    }
}


struct APIPlaceConnector: PlaceConnectorProtocol {
    func loadPlaceList() -> [Place] {
        // setup connection
        // get Place list from API
        
        return placeListFromAPI
    }
}

struct DatabaseConnector: PlaceConnectorProtocol {
    func loadPlaceList() -> [Place] {
        // setup DB connection
        // query to get Place list
        
        return placeDatabaesList
    }
}

struct PlaceConnectorFactory {
    static func getPlaceConnector(type: ConnectionType) -> PlaceConnectorProtocol {
        switch type {
        case .file:
            return FilePlaceConnector()
        case .api:
            return APIPlaceConnector()
        case .database:
            return DatabaseConnector()
        }
    }
}

class ClientController: UIViewController {
    func fetchPlace() {
        let placeService: PlaceConnectorProtocol = PlaceConnectorFactory.getPlaceConnector(type: .file)
        placeService.loadPlaceList()
    }
}{% endhighlight %}

Vì nó là &#8220;Simple Factory&#8221;, nên ưu điểm của nó chính là tận dụng ưu điểm của Factory đã trình bày ở trên, tận dụng tốt đặc điểm đa hình trong OOP. Tuy nhiên cũng cần lưu ý:

- Simple Factory khá hữu dụng với các bài toán liên quan đến tính đa hình (với số lượng object chung nhiều).
- Simple Factory <span style="color: #ff0000;"><strong>KHÔNG</strong></span> được coi là Design Pattern.

Simple Factory không hề phức tạp, chỉ là vận dụng linh hoạt tính đa hình để khởi tạo nên các class con, rõ ràng, chỉ là chút kiến thức căn bản về OOP mà thôi. Vì vậy tôi khuyên bạn, nếu còn chưa rõ về OOP, thì hãy tìm hiểu lại ngay đi.

## <span style="color: #00ccff;"><strong>IV. Factory method:</strong></span>

Từ Simple Factory, ta có thể phát triển thành phương pháp Factory Method, và phương pháp này được coi là một Design Pattern. Vậy Factory Method là như thế nào? Xin mời đọc tiếp.

Factory Method Pattern được đề cập đến trong quyển sách nổi tiếng của Gang-Of-Four (đề cập ở bài viết trước), định nghĩa của nó như sau:

<div class="page" title="Page 127">
  <div class="layoutArea">
    <div class="column">
      <blockquote>
        <p>
          Define an interface for creating an object, but let subclasses decide which class to instantiate. Factory Method lets a class defer instantiation to subclasses.
        </p>
        
        <p>
          (Tạm dịch: định nghĩa một Interface có nhiệm vụ khởi tạo object, nhưng để các subclasses-class con quyết định loại class nào sẽ được tạo instance. Factory Method giúp cho 1 class trì hoãn phần khởi tạo của mình cho các subclass.)
        </p>
      </blockquote>
      
      <p>
        Tôi sẽ diễn giải định nghĩa trên bằng code:
      </p>
      
      <p>
        <img class="size-large wp-image-1832 aligncenter" src="/wp-content/uploads/2018/11/Untitled-Diagram-3-1024x542.png" alt="" width="768" height="407" srcset="/wp-content/uploads/2018/11/Untitled-Diagram-3-1024x542.png 1024w, /wp-content/uploads/2018/11/Untitled-Diagram-3-300x159.png 300w, /wp-content/uploads/2018/11/Untitled-Diagram-3-768x407.png 768w, /wp-content/uploads/2018/11/Untitled-Diagram-3.png 1046w" sizes="(max-width: 768px) 100vw, 768px" />
      </p>
      
      <p>
        <em>// Vì Swift không hỗ trợ Abstract Class như các ngôn ngữ khác, nên tôi sẽ dùng Protocol Extension để thay thế.</em>
      </p>
      
      {% highlight swift %}
      protocol PlaceConnectorFactory {
    func getPlaceConnector() -> PlaceConnectorProtocol
}

extension PlaceConnectorFactory {
func loadPlaceList() {
let placeConnector = getPlaceConnector()
placeConnector.loadPlaceList()
}
}

struct DatabaseConnectorFactory: PlaceConnectorFactory {
func getPlaceConnector() -> PlaceConnectorProtocol {
// Setup Database Environment
// Connect Database and return instance
DatabaseConnector()
}
}

struct APIConnectorFactory: PlaceConnectorFactory {
func getPlaceConnector() -> PlaceConnectorProtocol {
// Setup Request
// Request
// Response
APIPlaceConnector()
}
}

var placeConnector: PlaceConnectorFactory!

//placeConnector = DatabaseConnectorFactory()
placeConnector = APIConnectorFactory()

placeConnector.loadPlaceList(){% endhighlight %}
  
 <p>
Dễ dàng thấy Factory hiện tại đã được chia thành các sub-factory con (DatabaseConnectorFactory, APIConnectorFactory), và việc instantiate nó sẽ tùy thuộc vào từng hoàn cảnh để sử dụng. Có nhận xét gì về cách thực hiện trên ?
</p>
  
 <ul>
<li>
Việc class nào được instantiate phụ thuộc vào sub-factory, do đó có thể dễ dàng hoán đổi, ngay cả trong Runtime.
</li>
<li>
Có thể điều khiển việc khởi tạo dễ dàng hơn, và viết logic business cũng dễ dàng hơn (so với Simple Factory).
</li>
<li>
Do việc khởi tạo nằm ở các sub-factory, việc chỉnh sửa cũng sẽ đơn giản hơn, ví dụ: thêm dependency (vấn đề này rất hay xảy ra).
</li>
<li>
Có thể mở rộng các Factory mới, dựa trên các factory cũ. Đặc điểm này khá hay, nhất là khi bạn muốn viết các custom Factory, dựa trên các Factory sẵn có của thư viện, framework,&#8230;
</li>
</ul>
  
 <p>
Vậy khi nào chúng ta nên sử dụng Factory Method ?
</p>
  
 <ul>
<li>
Như định nghĩa: khi bạn muốn các sub-class quyết định cái nào sẽ được instantiate.
</li>
<li>
Khi bạn có 1 nhóm các class cùng tính đa hình (polymorphism) và chúng có nguy cơ sửa đổi cao trong quá trình develop và maintain.
</li>
<li>
Khi bạn muốn mở rộng hoặc thiết kế 1 module để sử dụng chung.
</li>
</ul>
  
 <p>
Từ Factory Method, người ta mở rộng và phát triển nó hơn nữa, thành một pattern khác trừu tượng hơn, đó chính là <em><strong><span style="color: #00ccff;">Abstract Factory</span></strong></em>. Tuy nhiên, pattern này được sử dụng cho các bài toán phức tạp, và tôi tin rằng nếu tôi đề cập nó ở bài viết này, bạn sẽ tẩu hỏa nhập ma ngay. Mặc khác,<span style="color: #00ccff;"><em><strong> Abstract Factory</strong></em></span> hoàn toàn có thể suy luận và tìm hiểu thông qua góc nhìn từ Factory Method, thế nên hãy hiểu kỹ Factory Method trước, việc còn lại sẽ đơn giản hơn nhiều.
</p>
</div>

  </div>
</div>

## <span style="color: #00ccff;"><strong>V. Nhận xét và kết luận:</strong></span>

Qua bài viết, tôi đã trình bày cho các bạn cơ bản về Factory và cách chúng được sử dụng. Thuật ngữ về Factory Pattern bạn có thể tìm thấy rất rất nhiều trên Internet, vì đơn giản là nó là pattern quá phổ biến và thông dụng. Bản thân Apple cũng sử dụng chúng trong framework UIKit, [bạn có thể tìm thấy ở đây.](https://developer.apple.com/library/archive/documentation/General/Conceptual/CocoaEncyclopedia/ClassFactoryMethods/ClassFactoryMethods.html) Tuy nhiên, một phần vì sự đa dạng của tài liệu, nhiều người sẽ bị bối rối và bế tắc khi tìm hiểu về đề tài này. Bản thân tôi khi mới nghiên cứu cũng gặp vấn đề tương tự, sau đó tôi đã tìm hiểu thêm và tổng kết lại được một số đề mục nêu ở trên. Bạn cần phải hiểu rõ Factory, Simple Factory, và Factory Method, chúng là gì và chúng phân biệt như thế nào. Một số topic đề cập đến chủ đề này rất mập mờ, thậm chí còn đánh đồng khái niệm với nhau, bạn hãy cẩn thận khi tiếp thu thông tin từ những topic như vậy.

Để ý kỹ, có thể thấy Factory khiến các module loằng ngoằng và phức tạp hơn, vì vậy, nó cũng có thể coi là 1 **<span style="color: #ff0000;">Anti-pattern</span>** (pattern không nên dùng), ví dụ như trong các trường hợp sau:

- Khi chỉ có mình bạn và duy nhất bạn code, phù hợp với các dự án nhỏ, pet project,&#8230;
- Khi số lượng class chung đặc điểm đa hình ít, và cũng ít có khả năng thay đổi ở tương lai, hoặc khả năng thay đổi (ở việc khởi tạo nó) tốn ít chi phí.
- Đừng sử dụng nó chỉ vì nó là 1 design pattern, một developer tốt cần phải biết cân nhắc chi phí giữa việc thực thi pattern, so với những gì nó mang lại, có thật sự là hiệu quả không.

Đành rằng nó phổ biến, nhưng không có nghĩa nó là tốt ở mọi trường hợp, hãy phân tích và so sánh thật cẩn thận trước khi đưa ra quyết định. Với kinh nghiệm của tôi, tôi có xu hướng sử dụng Simple Factory hơn là Factory Method, lý do chính là vì nó đơn giản và các bài toán tôi gặp cũng không quá phức tạp. Tuy nhiên, khi phát triển một số tính năng phức tạp ở phía backend, thì tôi lại thường sử dụng Factory Method hơn, cũng có lần tôi maintain 1 source sử dụng Abstract Factory, phải công nhận là nó loằng ngoằng và tôi đánh giá là không cần thiết cho lắm, tuy nhiên, đó là phạm trù khác và topic khác.

P.s: nếu có thời gian, hãy tìm hiểu thêm về Abstract Factory Design Pattern.
