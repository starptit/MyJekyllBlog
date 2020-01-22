---
id: 1769
title: "iOS Pattern Phần 8: Dependency Injection (Phần cuối)"
date: 2018-07-11T16:07:31+00:00
author: starptit
# layout: post
guid: http://www.swiftyvn.com/?p=1769
permalink: /2018/07/ios-pattern-phan-8-dependency-injection-phan-cuoi/
tags: [Uncategorized, Swift]
---

Ở phần trước, tôi đã giới thiệu cho các bạn khái niệm về Inversion of Control, để tiếp nối mạch logic, tôi sẽ trình bày nốt về Dependency Injection &#8211; một kĩ thuật, phương pháp khá hay và phổ biến trong ngành lập trình. Vậy nó là gì? Nó làm sao? Dùng nó thế nào? Hãy đọc bài viết để có câu trả lời cho riêng mình nhé!

<!--more-->

## <span style="color: #ff6600;">Dependency Injection là gì ?</span>

<span style="color: #993366;"><strong>Dependency Injection (DI)</strong></span> dịch ra tiếng Việt có nghĩa là &#8220;chèn Dependency&#8221;. Cái tên nói lên tất cả, DI là kĩ thuật sử dụng các Dependencies bằng cách chèn chúng vào module/ class. Vậy chèn là gì?

Kĩ thuật chèn ở đây chính là việc chúng ta <span style="color: #993366;"><strong>passing</strong></span> các dependency.

Ví dụ:

{% highlight swift %}
class UserListViewController: UIViewController {
    var userService: UserService!
    var dbService: DatabaseService!
    
    override func viewDidLoad() {
        // initializer
        userService = UserService()
    }
    
    // injection
    func setDatabaseService(dbService: DatabaseService) {
        self.dbService = dbService
    }
}

{% endhighlight %}

Ở trên ta có 2 dependency là userService, và dbService, trong đó userService được sử dụng bằng cách khởi tạo trực tiếp bên trong UserListViewController, còn dbService được passing qua hàm setDatabaseService. Ở đây ta nói, ta đang sử dụng Dependency Injection với dbService.

Nhưng tại sao lại cần phải passing/inject dbService ? Tại sao không làm như userService? Nó có đem lại lợi ích gì hơn không ?

Okay, 1 vạn câu hỏi tại sao. Đừng vội, bạn sẽ tìm được câu trả lời sau ở đoạn sau ngay thôi.

Tóm lại, đọc đến đây, tôi muốn bạn hiểu và nắm được:

- Injecton là gì?
- Dependency Injection là gì?

## <span style="color: #ff6600;">Phân tích kĩ thuật Depedency Injection:</span>

So sánh 2 cách sử dụng dependency trên, rõ ràng ở trường hợp của userService, chúng ta đã vô tình kết dính userService vào UserListViewController, điều này là tối kị trong việc thiết kế code, vì nó sẽ làm giảm khả năng maintain, cũng như gây khó khăn khi sửa đổi source code. Ví dụ, giả sử UserService thay đổi constructor của nó:

{% highlight swift %}
class UserService {
    
    init(with identifier: String) {
        
    }
    
}

class UserListViewController: UIViewController {
    var userService: UserService!
    var dbService: DatabaseService!
    
    override func viewDidLoad() {
        // old initializer
//        userService = userService()
        
        // new initializer
        userService = UserService(with: "UserService")
    }
    
    // injection
    func setDatabaseService(dbService: DatabaseService) {
        self.dbService = dbService
    }
}

{% endhighlight %}

Ta phải thay đổi code trong viewDidLoad của UserListViewController tương ứng. Rõ ràng, thay đổi từ phía dendency buộc module sử dụng nó phải thay đổi theo, compile lại, test lại, không ổn một chút nào phải không?

Với bài toán thay đổi DatabaseService thì sao?

{% highlight swift %}
class DatabaseService {
    init(with identifier: String) {
        
    }
    init(with property: [String: Any]) {
        
    }
}

class UserListViewController: UIViewController {
    var userService: UserService!
    var dbService: DatabaseService!
    
    override func viewDidLoad() {
        // old initializer
        //        userService = userService()
        
        // new initializer
        userService = UserService(with: "UserService")
    }
    
    // injection
    func setDatabaseService(dbService: DatabaseService) {
        self.dbService = dbService
    }
}

{% endhighlight %}

Chẳng có gì thay đổi ở phía UserListViewController cả, bởi vì cái mà UserListViewController cần từ DatabaseService chỉ là 1 instance của nó, để có thể dùng instance đó thực hiện các logic và xử lý nó cần. Đứng trên quan điểm của UserListViewController: này anh DatabaseService, tôi là UserListViewController, tôi cần xử lý tác vụ về Database, do đó tôi mượn anh để thực hiện, tôi và anh là 2 người riêng biệt, do đó tôi không muốn quản lý hay liên quan gì đến nội tại hoạt động của anh, cái tôi cần là tôi giao anh 1 việc, anh trả tôi kết quả.

Việc inject / passing DatabaseService đã giúp chúng ta đảm bảo được quan điểm trên.

&#8211;> Tóm lại: phần này tôi cần bạn hiểu:

- Lợi ích của việc injection
- Tại sao lại cần phải injection

## <span style="color: #ff6600;">Làm thể nào để Inject Dependency ?</span>

Bản chất của Injection là việc các bạn passing dependency đến các class/module muốn sử dụng, do đó, chúng ta có 3 cách cơ bản đẻ có thể thực hiện injection: constructor injection, setter injection và interface injection.

**<span style="color: #008000;"><em>a. Setter Injection:</em></span>**

Đây chính là phương pháp mà tôi đã thực hiện ở ví dụ đầu bài viết. Đối với các ngôn ngữ OOP nói chung, thông thường để đảm bảo tính đóng gói và bảo mật, các property thường được gán private, và truy cập trong thông qua cặp method getter/setter. Tuy nhiên, Swift không vậy, getter và setter của swift có thể được viết theo dạng closure, do đó, nếu muốn thực hiện inject thông qua setter, bạn buộc phải thực hiện theo template của các ngôn ngữ OOP khác:

{% highlight swift %}
class UserListViewController: UIViewController {
    var userService: UserService!
    var dbService: DatabaseService!
    
    // injection
    func setDatabaseService(dbService: DatabaseService) {
        self.dbService = dbService
    }
    
    func setUserService(userService: UserService) {
        self.userService = userService
    }
}

{% endhighlight %}

Đặc điểm của phương pháp này là rất nhanh gọn và trực quan, vì hầu như các IDE đều hỗ trợ việc sinh ra getter và setter tự động.

**_<span style="color: #008000;">b. Constructor Injection:</span>_**

Tương tự như setter Injection, phương pháp này sử dụng các hàm khởi tạo để thực hiện inject:

{% highlight swift %}
class UserListViewController: UIViewController {
    let userService: UserService
    let dbService: DatabaseService
    
    init(userService: UserService, dbService: DatabaseService) {
        self.userService = userService
        self.dbService = dbService
        super.init(nibName: "UserListViewController", bundle: nil)
    }
    
    required init?(coder aDecoder: NSCoder) {
        fatalError("init(coder:) has not been implemented")
    }
    
}

{% endhighlight %}

Constructor Injection cũng khá phổ biến, tuy nhiên nhược điểm của nó là:

- Dễ thay đổi khi constructor thay đổi, và việc thay đổi constructor trong giai đoạn thiết kế và phát triển là điều bình thường
- Khi có quá nhiều dependency, hàm dễ trở nên dài và cồng kềnh.
- Không tối ưu và hoạt động tốt với lập trình iOS.

Nhược điểm không tối ưu với lập trình iOS khá quan trọng, bởi vì các UIViewController trong iOS thường được khởi tạo từ xib/storyboard, thông qua hàm

{% highlight swift %}
func instantiateViewController(withIdentifier identifier: String) -> UIViewController

{% endhighlight %}

Hàm này KHÔNG phải là hàm khởi tạo, do đó nó không tối ưu với UIViewController. Nếu bạn không inject module như Manager, Helper,&#8230; hoặc khởi tạo UIViewController bằng code, thì bạn hoàn toàn có thể sử dụng phương pháp này. Tuy nhiên, theo thói quen, tôi rất ít khi dùng constructor injection.

<span style="color: #008000;"><em><strong>c. Interface Injection:</strong></em></span>

Interface Injection, nghĩa là bạn inject dependency của các bạn thông qua Interface:

{% highlight swift %}
protocol Injectable {
    func inject(userService: UserService, dbService: DatabaseService)
}

class UserListViewController: UIViewController, Injectable {
    var userService: UserService!
    var dbService: DatabaseService!
    
    func inject(userService: UserService, dbService: DatabaseService) {
        self.userService = userService
        self.dbService = dbService
    }
}

{% endhighlight %}

Lợi thế mà Interface đem lại chính là tính trừu tượng, bạn có thể hoán đổi hoặc tương tác với các module khác nếu chúng cùng tuân theo 1 Interface. Bản thân tôi thực tế không sử dụng nhiều phương pháp này, một phần vì tôi muốn tách biệt hẳn các module mặc dù chúng có thể hoán đổi, đây hoàn toàn là quan điểm cá nhân, cho nên các bạn hãy cứ thử sử dụng chúng nếu nó có lợi cho bài toàn của bạn.

À quên, Swift là Protocol-Oriented Programming, hãy thêm một chút Swifty vào đoạn code trên nhé:

{% highlight swift %}
protocol Injectable {
    var userService: UserService! { get set }
    var dbService: DatabaseService! { get set }
}

extension Injectable {
    mutating func inject(userService: UserService, dbService: DatabaseService) {
        self.userService = userService
        self.dbService = dbService
    }
}

class UserListViewController: UIViewController, Injectable {
    var userService: UserService!
    var dbService: DatabaseService!
}

var userVC: Injectable = UserListViewController()
userVC.inject(userService: UserService(), dbService: DatabaseService())

{% endhighlight %}

Okay, qua đoạn này, tôi muốn bạn phải hiểu được:

- Injection có những phương pháp nào?
- Phân tích từng phương pháp
- Ưu / Nhược điểm của từng phương pháp
- Thử nghĩ về một bài toán và áp dụng cả 3 phương pháp kể trên.

## <span style="color: #ff6600;">Dependency Injection và Dependency Inversion Principle:</span>

Đừng hoa mắt vì 2 cái tên mà đọc nhầm nhé 😂:

- **<span style="color: #ff0000;">Dependency Injection (DI)</span>**: kĩ thuật inject các dependencies (bài viết hôm nay)
- <span style="color: #ff0000;"><strong>Dependency Inversion Principle (D.I.P):</strong></span> nguyên lý đảo ngược các Dependencies (phần 6 &#8211; series S.O.L.I.D)

Có một sự thật kì lạ, khi tôi tìm hiểu về đề tài này, nhiều blogger và thông tin từ trang hỏi đáp thường sử dụng 2 định nghĩa này kèm với nhau. Điều này là đúng, tuy nhiên theo tôi ,nó gây ra bối rối cho nhiều người, và hơn hết, cách tìm hiểu trên chỉ cho bạn hiểu phần ngọn chứ không hề là bản chất của vấn đề.

Hãy nhìn bài toán theo góc độ sau:

DI giúp việc inject &#8211; passing các low level vào các high level (từ dependency ở đây chính là có ý nghĩa này, nếu bạn chưa hiểu, mời đọc lại định nghĩa ở [phần 6](http://www.swiftyvn.com/ios-pattern-phan-6-nguyen-ly-s-o-l-i-d-chu-d/)). Và theo nguyên lý D.I.P, không nên để high-level phụ thuộc vào low level module, cả 2 nên phụ thuộc vào abstractions. Đây chính là lý do mà chúng ta nên vận dụng nguyên lý D.I.P khi tích hợp kỹ thuật Dependency Injection, và cũng là lý do khiến nhiều blogger thường viết chúng chung vào nhau là vì vậy.

Áp dụng nguyên lý D.I.P vào D.I khá đơn giản, công việc của chúng ta chỉ là chuyển phụ thuộc giữa 2 bên (inject và được inject) thành phụ thuộc trừu tượng là xong:

{% highlight swift %}
protocol IUserService {
    func getUser()
}

class UserService: IUserService {
    func getUser() {
        
    }
}

class UserListViewControllerA: UIViewController {
    var userService: IUserService!
    func setUserService(userService: IUserService) {
        self.userService = userService
    }
}

let setterInjectUserListVC = UserListViewControllerA()
setterInjectUserListVC.setUserService(userService: UserService())


class UserListViewControllerB: UIViewController {
    let userService: IUserService
    
        init(userService: IUserService) {
            self.userService = userService
            super.init(nibName: "UserListViewController", bundle: nil)
        }
    
        required init?(coder aDecoder: NSCoder) {
            fatalError("init(coder:) has not been implemented")
        }
}

let constructorInjectUserListVC = UserListViewControllerB(userService: UserService())



protocol Injectable {
    var userService: IUserService! { get set }
}

extension Injectable {
    mutating func inject(userService: IUserService) {
        self.userService = userService
    }
}

class UserListViewControllerC: UIViewController, Injectable {
    var userService: IUserService!
}

var interfaceInjectUserListVC: Injectable = UserListViewControllerC()
interfaceInjectUserListVC.inject(userService: UserService())

{% endhighlight %}

Việc kết hợp DI và D.I.P rất phổ biến, hầu như những project tôi tham gia thì 99% họ đều làm như vậy. Lợi ích của nó rất rõ ràng, giảm thiểu code kết dính, giúp dễ maintain, sửa đổi và test hơn. Tuy nhiên nó sẽ làm cho code của bạn loằng ngoằng và rối rắm hơn, khó khăn cho người mới join vào dự án.

Nếu bạn vẫn thắc mắc nó có thực sự tốt hơn, thì một lần nữa, xin mời bài đọc lại [phần 6,](http://www.swiftyvn.com/ios-pattern-phan-6-nguyen-ly-s-o-l-i-d-chu-d/) vì lúc này ưu điểm và nhược điểm hoàn toàn nằm ở nguyên lý D.I.P chứ không còn nằm ở phương pháp DI nữa rồi.

## <span style="color: #ff6600;">Kết luận:</span>

Tóm tắt lại những ý chính bạn cần nắm được sau khi đã đọc hết bài viết:

- Dependency Injection là gì?
- Dependency Injection có lợi thế gì, nó giải quyết bài toán gì, và tại sao lại cần có nó?
- Các cách thực hiện Dependency Injection là gì? Ưu/ nhược điểm của chúng.
- Phân biệt Dependency Injection và Dependency Inversion Principle.

Dependency Injection là kĩ thuật phổ biến mà gần như developer nào cũng biết, khi kết hợp cùng nguyên lý đảo ngược Dependency (D.I.P), nó sẽ giúp bạn phân tách rõ ràng các module với nhau, qua đó đảm bảo tính đơn chức năng, tăng tính mềm dẻo, giảm sự kết dính giữa các module. Ngoài ra, DI và D.I.P còn là một trong những cách tiêu biểu nhằm hạn chế code phình to, đặc biệt là đối với các UIViewController. Kĩ thuật này giúp chúng ta khởi tạo các services (mỗi service là một module cấp thấp, hay còn gọi là dependency) phục vụ cho nghiệp vụ của module cấp cao. Với kinh nghiệm bản thân, tôi khuyên các bạn nên thử thực hành nó với 2 module hay gặp nhất, đó là gửi API Request, và  xử lý thao tác với Database (DatabaseService).

Series về iOS Pattern cũng xin được tạm dừng tại đây, nếu bạn có thắc mắc hay gợi ý về chủ đề mà bạn muốn tôi viết, hãy cứ để lại comment ở bài viết.

Tài liệu tham khảo:

- https://en.wikipedia.org/wiki/Dependency_injection
- https://www.martinfowler.com/articles/injection.html#InterfaceInjection
- https://marcosantadev.com/solid-principles-applied-swift/
- https://medium.com/swift-programming/dependency-injection-with-the-cake-pattern-3cf87f9e97af

{% include disqus_comments.html %}