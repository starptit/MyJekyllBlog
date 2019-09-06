---
id: 1837
title: Singleton Design Pattern
date: 2019-01-31T10:54:24+00:00
author: starptit
# layout: post
guid: http://swiftyvn.com/?p=1837
permalink: /2019/01/singleton-design-pattern/
tags: [Uncategorized, Swift]
---

Chủ đề lần này, tôi muốn viết về một loại Design Pattern khác cũng rất hay gặp, đó chính là Singleton Design Pattern. Tương tự như Factory Pattern, Singleton thuộc loại Creational, nó giải quyết bài toán liên quan đến vấn đề khởi tạo object (instation).

<img class="size-full wp-image-1862 aligncenter" src="/wp-content/uploads/2019/01/its-a-design.jpg" alt="" width="600" height="400" srcset="/wp-content/uploads/2019/01/its-a-design.jpg 600w, /wp-content/uploads/2019/01/its-a-design-300x200.jpg 300w" sizes="(max-width: 600px) 100vw, 600px" />

### <span style="color: #ff6600;">Singleton Là Gì, Và Tại Sao Cần Phải Sử Dụng Nó</span>

Mục đích sử dụng Singleton được viết ngắn gọn trong quyển sách của G.O.F:

> Ensure a class only has one instance, and provide a global point of access to it.

(Tạm dịch: đảm bảo class chỉ có duy nhất 1 instance, tất cả đều có quyền truy cập và sử dụng instance đó)

Vậy tại sao class lại cần duy nhất 1 instance trong cả ứng dụng ?

Xuất phát từ thực tế, một số class như xử lý cache, quản lý database, notification,&#8230; thường xuyên được sử dụng ở nhiều class khác nhau. Điều này đồng nghĩa với việc instance của cùng một class được khởi tạo và sử dụng ở nhiều nơi. Hệ quả là code bị duplicate, khó quản lý, chi phí sửa đổi cao,&#8230;

Giả sử ứng dụng của tôi là dạng web-app, phần quan trọng bậc nhất đối với web-app là phải quản lý Cookies. Tôi hoàn toàn có thể code theo kiểu sau:

<pre class="theme:xcode float-enable:true wrap-toggle:false plain:false lang:swift decode:true">class CookiesManager {
    
    func saveCookies() {
        // do stuff
    }
    
    func loadCookies() {
        // do stuff
    }
    
    func refreshCookies() {
        // do stuff
    }
}

class ViewControllerA: UIViewController {
    override func viewDidLoad() {
        let cookiesManager = CookiesManager()
        cookiesManager.loadCookies()
    }
}

class ViewControllerB: UIViewController {
    override func viewDidLoad() {
        let cookiesManager = CookiesManager()
        cookiesManager.refreshCookies()
    }
}</pre>

Tuy nhiên đoạn code trên cũng có vấn đề: Việc quản lý cookies cần được thực hiện trong suốt Runtime của ứng dụng, đồng nghĩa với việc CookiesManager có thể phải khởi tạo nhiều instance tại nhiều nơi.

Vẫn đề trên sẽ biến mất hoàn toàn nếu như CookiesManager chỉ tồn tại duy nhất 1 instance, vì lẽ đó, Singleton Pattern (theo lý thuyết) là giải pháp hợp lý.

### <span style="color: #ff6600;">Viết Singleton Thế Nào Cho Đúng</span>

Bước đầu tiên khi tìm hiểu về Design Pattern không có gì khác ngoài việc nghiên cứu UML Diagram của nó:

<img class="size-large wp-image-1843 aligncenter" src="/wp-content/uploads/2019/01/Untitled-Diagram-4.png" alt="" width="378" height="366" srcset="/wp-content/uploads/2019/01/Untitled-Diagram-4.png 378w, /wp-content/uploads/2019/01/Untitled-Diagram-4-300x290.png 300w" sizes="(max-width: 378px) 100vw, 378px" />

Biến đổi UML trên thành code:

<pre class="theme:xcode float-enable:true wrap-toggle:false plain:false lang:swift decode:true">class Singleton {
    
    init() {}
    
    private static var instance = Singleton()
    
    public static func getInstance() -> Singleton {
        return instance
    }
}</pre>

Code rất đơn giản, nếu muốn sử dụng instance của Singleton, ta chỉ cần gọi: <span style="color: #ff0000;"><strong><code>Singleton.getInstance()</code></strong></span> là xong. Cách implement trên khá phổ biển, nhất là với các ngôn ngữ Java, C#,&#8230; TUY NHIÊN, Swift là ngôn ngữ hiện đại và thông minh, do đó, với Swift, chúng ta có cách khác đơn giản và hiệu quả hơn:

<pre class="theme:xcode float-enable:true wrap-toggle:false plain:false lang:swift decode:true">class Singleton {
    static let shared: Singleton = Singleton()
}</pre>

Đơn giản hơn thì nhìn rõ rồi, nhưng tại sao lại nói hiệu quả hơn ?

Swift là static language cho nên biến / hàm /class được đánh dấu là static thì sẽ được khởi tạo ở thời điểm biên dịch (compile time). Tuy nhiên, đối với các hằng số global hoặc biến global thì Swift sẽ mặc định khởi tạo theo kiểu lazily (tức là khi nào nó bắt đầu được sử dụng thì nó mới được khởi tạo), tham khảo <span style="color: #3366ff;"><a style="color: #3366ff;" href="https://docs.swift.org/swift-book/LanguageGuide/Properties.html#ID257">link sau</a></span>. Nếu sử dụng cú pháp <span style="color: #ff0000;"><strong><em><code>static let</code></em></strong></span>, Swift sẽ hiểu đó là global variables, đồng nghĩa với việc biến shared sẽ được được khởi tạo khi mà nó chuẩn bị được sử dụng (lazy cũng là một loại pattern, sẽ có bài viết về nó sau).

UML của Singleton lúc này sẽ được update thành:

<img class="size-full wp-image-1844 aligncenter" src="/wp-content/uploads/2019/01/Untitled-Diagram-5.png" alt="" width="398" height="256" srcset="/wp-content/uploads/2019/01/Untitled-Diagram-5.png 398w, /wp-content/uploads/2019/01/Untitled-Diagram-5-300x193.png 300w" sizes="(max-width: 398px) 100vw, 398px" />

&nbsp;

Quay trở lại với trường hợp CookiesManager, áp dụng Singleton Pattern:

<pre class="theme:xcode float-enable:true wrap-toggle:false plain:false lang:swift decode:true">class CookiesManager {
    static let shared = CookiesManager()
    
    func saveCookies() {
        // do stuff
    }
    
    func loadCookies() {
        // do stuff
    }
    
    func refreshCookies() {
        // do stuff
    }
}

class ViewControllerA: UIViewController {
    override func viewDidLoad() {
        CookiesManager.shared.saveCookies()
    }
}

class ViewControllerB: UIViewController {
    override func viewDidLoad() {
            CookiesManager.shared.refreshCookies()
    }
}</pre>

Thực tế, bạn rất dễ dàng bắt gặp Singleton Pattern được Apple áp dụng trong một số module thông dụng:

<pre class="theme:xcode float-enable:true wrap-toggle:false plain:false lang:swift decode:true">UIApplication.shared
NotificationCenter.default
UserDefaults.standard</pre>

### <span style="color: #ff6600;">Phân Tích Singleton Pattern</span>

Singleton thường được đem ra so sánh với sử dụng thuộc tính **<span style="color: #ff0000;"><code>static</code></span>** trong class (tôi tạm gọi tắt là static class). Bản chất Singleton là cung cấp 1 instance duy nhất, đồng nghĩa function, variables, properties,&#8230; của nó cũng là duy nhất, điều này hoàn toàn có thể thực hiện bằng cách sử dụng static:

<pre class="theme:xcode float-enable:true wrap-toggle:false plain:false lang:swift decode:true ">class CookiesManager {
    static func saveCookies() {}
    static func loadCookies() {}
    static func refreshCookies() {}
}

class ViewControllerA: UIViewController {
    override func viewDidLoad() {
        CookiesManager.saveCookies()
    }
}</pre>

Hiển nhiên rằng Singleton phải có ưu điểm gì nổi trội hơn static class:

&#8211; Singleton là <span style="color: #ff0000;"><strong><em><code>instance</code></em></strong></span>, developer có quyền điều khiển việc cấp phát, giải phóng bộ nhớ của instance đó. Static class được cấp phát từ compile time, và chạy trong suốt runtime, developer không được can thiệp vào quá trình này. (Tuy ở một số ngôn ngữ static class có thể được lazy loading, tuy nhiên static class lại không giải phóng được bộ nhớ, do đó nó vẫn thua thiệt hơn Singleton ở điểm này).

&#8211; Vì bản chất là instance của class, do đó Singleton hưởng lợi từ đặc tính trong OOP của class: kế thừa, đa hình, trừu tượng,&#8230;.

&#8211; Singleton có thể kết hợp được với Design Pattern khác.

Tuy nhiên, Singleton không hẳn là pattern tốt, nó không phải là viên đạn bạc để chúng ta áp dụng mọi nơi, trên thực tế, có khá nhiều trường hợp khiến Singleton trở thành Anti-pattern.

Trong định nghĩa của Singleton, chúng ta cần chú ý đến:

> Ensure a class only has one instance, **and provide a global point of access to it.**

Chính phần chữ bôi đậm (tạm dịch: cung cấp khả năng truy cập global đến instance của Singleton) là điều khiến Singleton trở nên xấu xí. Lý do:

1. Singleton là duy nhất, là global state, nhưng class/module nào cũng có quyền truy cập, sử dụng và chỉnh sửa, nghĩa là Global nhưng share state. Giả sử với CookiesManager, ViewControllerA đang tiến hành lưu cookies, cùng lúc đó, ViewControllerB lại thực hiện clear toàn bộ cookies ===> BOOMS!! Đây là bài toán xử lý concurrency tối kị trong lập trình. Chưa kể nếu nhét trong multiple thread thì nó còn phức tạp và kinh khủng thế nào nữa ?
2. Singleton không dễ viết Unit Test.

Khá nhiều lập trình viên khi mới biết Singleton thì rất thích thú và áp dụng tràn lan (vì nó viết dễ mà lại tiện), Global share state kể trên đúng ra phải là lý do để hắt hủi, thì lại trở thành lý do khiến họ ưa thích Singleton. Đây là lỗi tư duy phổ biến và nên tránh, hãy suy nghĩ thật kỹ trước khi quyết định, để chắc chắn bạn cần Singleton để giải quyết bài toán của mình.

### <span style="color: #ff6600;">Kết Luận</span>

Tổng kết lại, bài viết này trình bày về Singleton Design Pattern, tuy đơn giản nhưng lại cực kỳ phổ biến trong ngành lập trình hướng đối tượng. Tôi đã lần lượt giải đáp các câu hỏi:

- Singleton là gì, tại sao lại cần nó?
- Viết Singleton thế nào cho đúng?
- Phân tích Singleton.

Nhắc lại, Singleton tốt thật, tiện thật, nhưng cũng hoàn toàn có thể là Anti-pattern, đừng lạm dụng nó, hãy chú ý đến vấn đề Global share state của nó trước khi quyết định áp dụng.

Link tham khảo:

- <https://krakendev.io/blog/the-right-way-to-write-a-singleton>
- <https://gurunh.com/2018/05/singleton-dung-hay-khong/>
- <http://coding-geek.com/design-pattern-singleton-prototype-and-builder/>
