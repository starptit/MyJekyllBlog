---
id: 1690
title: "iOS pattern: Phần 6: Nguyên lý S.O.L.I.D (chữ D )"
date: 2018-03-22T16:31:28+00:00
author: starptit
# layout: post
guid: http://www.swiftyvn.com/?p=1690
permalink: /2018/03/ios-pattern-phan-6-nguyen-ly-s-o-l-i-d-chu-d/
tags: [Uncategorized, Swift]
---

Chào mừng các bạn đến với bài viết cuối cùng về chủ đề nguyên lý S.O.L.I.D. Cũng được một thời gian dài kể từ bài viết gần nhất của mình về S.O.L.I.D, vì vậy trước khi đi vào bài viết, mình khuyến khích các bạn đọc lại series này, từ phần đầu tiên, để có thể nhớ lại mục tiêu và phương pháp tiếp cận mà mình đã trình bày.

Nguyên lý cuối cùng này là nguyên lý đem đến cho mình nhiều hứng thú nhất trong quá trình tìm hiểu và áp dụng, nó giúp mình giải đáp những hiểu lầm về S.O.L.I.D, và trên thực tế, đây là nguyên lý mà mình áp dụng nhiều nhất.

<!--more-->

Chủ đề của bài viết được mình chia ra làm 2 phần: phần đầu tiên trình bày nguyên lý, các khái niệm cơ bản. Phần tiếp theo sẽ trình bày một số phương pháp thường dùng để đảm bảo nguyên lý.

<h1 style="text-align: center;">
  <em><strong>Phần 1: Tìm hiểu nguyên lý D.I.P</strong></em>
</h1>

### **_1. Nguyên lý chữ D là gì? (What is it?)_**

Như bạn thấy ở trên, tên đầy đủ của nguyên lý này là Dependency Inversion Principle, mình tạm dịch là nguyên lý đảo ngược Dependency. Mình không dịch từ Dependency, vì đơn giản đây là một khái niệm chung trong ngành phần mềm, và như các blog trước, mình để nguyên để giúp các bạn có thể dễ dàng nắm bắt hơn nếu tham khảo các tài liệu nước ngoài khác.

#### _**a. Dependency là cái gì ?**_

Nếu nói tổng quát, ta có thể hiểu như sau:

Dependency (còn gọi là coupling) biểu thị quan hệ phụ thuộc giữa A và B, khi A được sử dụng trên B (hoặc ngược lại).

Ở đây, A và B có thể là class, module, function,&#8230; Khi A được sử dụng trên B, thì ta nói A là dependency của B (và ngược lại).

Ví dụ với bài toán sau:

A là thư viện MapKit, B là MapViewController, B sử dụng A để hiển thị map &#8211;> ta nói MapKit là dependency của MapViewController.

Dependency là một thuật ngữ phổ biến trong ngành lập trình, để tránh tư duy bó hẹp và hiểu sai về dependency, mời bạn xem xét thêm ví dụ sau:

[<img class="alignnone size-large" src="http://ashishkakkad.com/wp-content/uploads/2016/01/CocoaPodsLogo.png" width="1540" height="383" />](http://ashishkakkad.com/wp-content/uploads/2016/01/CocoaPodsLogo.png)

Nhiệm vụ của Cocopods là làm gì? Giúp install và maintain các 3rd-library.

Các thư viện này được sử dụng như thế nào? Chúng được khởi tạo hoặc được gọi bởi các class/module của chúng ta &#8211;> đồng nghĩa với việc các 3rd-library này là dependency của class/module nói trên (tuân theo định nghĩa).

Cocoapods hay Carthage hay những dịch vụ tương tự được gọi là: Dependency Manager.

(Nếu bạn tìm hiểu thêm, bạn sẽ nhận thấy Dependency Manager được sử dụng rất rộng rãi, trong Java-android gọi luôn là dependencies, trong NodeJs thì là node_modules, npm, trong Python có pip, anaconda, Ruby có gem, hay ở mức Hệ Điều Hành macOs có Homebrew,&#8230;).

&#8211;> Nếu bạn chưa rõ, hãy hiểu theo cách đơn giản, tuy không hoàn toàn chính xác: dependency là các thành phần riêng biệt, được &#8220;cài cắm&#8221; vào một thành phần khác, để thực hiện một công việc nào đó.

#### **_b . Nguyên lý đảo ngược Dependency:_**

> <p class="">
>   A. High-level modules should not depend on low-level modules. Both should depend on abstractions.
> </p>
>
> &nbsp;
>
> <p class="">
>   B. Abstractions should not depend on details. Details should depend on abstractions.
> </p>

Nguyên lý được phát biểu với 2 ý chính:

- Các modules cấp cao không nên phụ thuộc vào các module cấp thấp, cả 2 nên phụ thuộc vào abstraction.
- Abstraction không nên phụ thuộc vào details, ngược lại, detail nên phụ thuộc vào abstraction.

Abstraction (sự trừu tượng) kỹ thuật lược bỏ các chi tiết bên trong, do đó các abstraction rất cơn bản và đơn giản, đặc điểm này vô cùng quan trọng, nhất là trong vấn đề giao tiếp giữa các module với nhau. Thật vậy, giao tiếp với các abstraction có nghĩa là giao tiếp với những phần cơ bản nhất và đơn giản nhất, hiển nhiên là dễ dàng hơn so với việc phải quan tâm thêm các thành phần khác.

Các bạn chú ý, từ module được dùng ở đây không nhất thiết phải đao to búa lớn như service, file, project,&#8230; nó hoàn toàn có thể là class, kể cả là function. Hiểu là vậy, nhưng để tránh loạn ngữ, mình xin phép sử dụng từ module cho toàn bài viết.

Quan hệ giữa high-level module và low-level module là gì? Về mặt khái niệm, module cao cấp là các module sử dụng các module cấp thấp hơn vào một nghiệp vụ nào đó mà nó cần. Tuy nhiên, để đánh giá module là low-level hay high-level, ta cần phải xem xét nó dựa trên quan hệ với module mà nó giao tiếp, vì có trường hợp nó là low-level với module này, nhưng cũng là high-level với module khác.

Ví dụ với bài toán MapKit ở trên, hiển nhiên MapKit là low-level với MapViewController, nhưng bản thân bên trong MapKit lại có một số module cấp thấp khác như module lấy tọa độ (Coordinate). Do đó, MapKit là low-level với MapViewController, nhưng là high-level với Coordinate.

&#8211;> module cấp thấp sẽ là dependency của module cấp cao (theo định nghĩa, đúng chứ ?)

Có thể đọc đến đây bạn thấy nó hơi tối nghĩa và khó hiểu? Không sao, tạm thời cứ đánh dấu nó lại, mình sẽ giải thích chi tiết hơn ở mục dưới.

Tóm lại, phần này các bạn cần nhớ:

- Dependency là gì ?
- Abstraction là gì ?
- High-level và low-level module là gì?
- Nguyên lý Dependency Inversion có 2 mục tiêu chính là gì ?

### _**2. Phân tích và giải nghĩa nguyên lý:**_

Cùng xem xét ví dụ sau:

{% highlight swift %}
class APIService {
    func fetchUserList() {
        // TODO: - Fetch User List by calling API
    }
}

class UserManager {
    
    func getUserList(){
        let apiService = APIService()
        apiService.fetchUserList()
    }
}

{% endhighlight %}

Rất tốt, bạn đã biết vận dụng nguyên lý SRP (phần 1) để tạo một class UserManager nhằm quản lý nghiệp vụ liên quan đến User. Từ các định nghĩa nêu ở trên, ta có thể xác định được:

- UserManager: là high level module
- APIService: là low level module, đồng thời là dependency của UserManager.

Ta có thể rút ra những nhận xét về ví dụ trên:

- Hàm getUserList() rất khó test, vì nó liên quan đến module APIService bên trong, dẫn đến muốn test hàm này cần phải test APIService trước.
- Hàm getUserList() không reuse code được, dẫn đến UserManager cũng không reuse lại code được, vì nó phụ thuộc hoàn toàn vào APIService.
- Thiết kế trên không linh hoạt, giả sử class APIService có thay đổi, dẫn đến hàm getUserList() trên cũng thay đổi kéo theo là UserManager. Thật nguy hiểm nếu bạn sử dụng APIService để thực hiện tác vụ trong nhiều class khác nhau.
- Thiết kế trên vi phạm nguyên lý DIP, do UserManager (high-level) bị phụ thuộc vào APIService (low-level).

Từ kết luận trên, ta có thể thấy rõ module chúng ta vừa lập trình hoàn toàn thất bại trong việc tối ưu source code, và cực kỳ tệ khi phản ứng với các thay đổi từ cả bên trong lẫn bên ngoài. Lại nói, đối với ngành lập trình, thay đổi là vấn đề thường xuyên, đừng bảo với tôi là bạn chưa khi nào gặp những việc như:  thư viện cập nhật, fix bug, requirement từ khách hàng bị thay đổi,&#8230;

Tạm thời phớt lờ những nhận xét trên, bạn tiếp tục sử dụng UserManager vào các module khác nữa:

{% highlight swift %}
class APIService {
    func fetchUserList() {
        // TODO: - Fetch User List by calling API
    }
}

class UserManager {
    
    func getUserList(){
        let apiService = APIService()
        apiService.fetchUserList()
    }
}

class ViewControllerA: UIViewController{
    let userManager: UserManager = UserManager()
    
    func getListUserData() {
        userManager.getUserList()
    }
}

class ViewControllerB: UIViewController {
    let userManager: UserManager = UserManager()
    
    func getListUserData() {
        userManager.getUserList()
    }
}

{% endhighlight %}

Hoàn thành công việc, bạn hoàn toàn hài lòng và yên tâm về những đoạn code trên, bạn nghĩ rằng chúng đã làm tốt phần việc của mình ?

Không, không thật sự như vậy đâu. Mọi thứ đúng là ổn, cho đến một ngày:

Thư viện bạn dùng để gọi API Service thay đổi: cập nhật version cho thư viện, hoặc tệ hơn là bị thay thế bởi một thư viện khác (deprecated). Mỗi đợt iOS version mới release thì sẽ có cả tá thư viện cũ bị deprecated, hoặc swift nâng cấp version thì cũng kéo theo thay đổi hàng loạt đến các thư viện 3rd-party khác. Nói vậy để bạn hiểu rằng trường hợp mà mình đang ví dụ đây là chuyện bình thường và xác suất nó rơi vào dự án của bạn cũng không hề thấp.

Đối với thách thức trên, bạn thường sẽ sửa lại như sau:

{% highlight swift %}
class APIService {
    func fetchUserList() {
        // TODO: - Fetch User List by calling API
        
        // remove old code
        ...
        
        // upgrade to new version
        ....
    }
}

class UserManager {
    
    func getUserList(){
        let apiService = APIService()
        apiService.fetchUserList()
    }
}

{% endhighlight %}

class APIService đã thay đổi, kéo theo là UserManager, và UserViewControllerA, UserViewControllerB. Chi tiết này khiến cho bạn phải tiến hành test lại toàn bộ những class kéo theo trên. Hiển nhiên việc trên không hề dễ chịu chút nào, chưa kể trường hợp gặp lỗi, hoặc thay đổi kéo theo trên nhiều class khác nữa. Vì việc này nó là thói quen và tư duy lập trình thông thường của bạn, nên việc nó được áp dụng vào toàn bộ project, hoặc các module khác mà bạn phụ trách rất dễ xảy ra. Hãy thử tưởng tượng hậu quả nếu trường hợp trên xảy ra với tất cả những module bạn đã làm. Đa số những vấn đề kể trên bắt đầu phát sinh vào chu kỳ maintain hoặc giai đoạn fix bug, khi đó áp lực về công việc, thời gian, khách hàng,&#8230; sẽ cực kỳ kinh khủng, và với những module tệ hại đến mức sửa 1 hỏng 10 thì sao? Oops, Good Game Well Played !

Vậy khắc phục thế nào?

Theo như nguyên lý, UserManager và APIService nên phụ thuộc chung 1 abstraction, ta hãy cứ tạm coi nguyên lý trên là đúng, và sửa lại đoạn code trên 1 chút:

{% highlight swift %}
protocol IUserService{
    func fetchUserList()
}

class APIService: IUserService {
    func fetchUserList() {
        // TODO: - Fetch User List by calling API
        
        // remove old code
        ...
            
            // upgrade to new version
        ....
    }
}

class UserManager {
    
    let userService: IUserService
    
    init(userService: IUserService) {
        self.userService = userService
    }
    
    func getUserList(){
        userService.fetchUserList()
    }
    
}

class ViewControllerA: UIViewController{
    let userManager: UserManager = UserManager(userService: APIService())
    
    func getListUserData() {
        userManager.getUserList()
    }
}


class ViewControllerB: UIViewController {
    let userManager: UserManager = UserManager(userService: APIService())
    
    func getListUserData() {
        userManager.getUserList()
    }
}

{% endhighlight %}

Ở đây, ta tạo một protocol IUserService và định nghĩa hàm fetchUserList(). APIService là module cấp thấp, sẽ implement protocol trên, còn module cấp cao UserManager sẽ sử dụng protocol trên vào nghiệp vụ của mình. Điều này có lợi gì?

- Hàm getUserList() chỉ quan tâm và giao tiếp với Interface IUserService, việc thực thi bên trong là nằm ở các module conform đến Interface. Điều này dẫn đến hệ quả là hàm getUserList() dễ test, và dễ reuse hơn.
- Giả sử hàm fetchUserList() thay đổi thì sao? Thay đổi đó là nằm ở các module thực thi Interface IUserService, UserManager không quan tâm, vì thằng mà nó trực tiếp tương tác là IUserService chứ không phải các thằng module cấp thấp.
- Nhờ sử dụng Interface, các module cấp con linh hoạt hơn và có thể swap cho nhau.

Sau một thời gian phát triển, khách hàng yêu cầu ứng dụng phải hỗ trợ offline, nghĩa là dữ liệu phải được lưu và xử lý local, nói đơn giản hơn là bạn phải cung cấp tính năng fetchUser từ local. Với kiểu thiết kế như ban đầu, công việc của chúng ta lúc này lại cực kỳ phức tạp:

{% highlight swift %}
class APIService {
    func fetchUserList() {
        // TODO: - Fetch User List by calling API
    }
}

class DBManagerService {
    func fetchLocalUser() {
        // TODO: - Fetch User List from DB Local
    }
}

class UserManager {
    
    func getUserList(){
        let apiService = APIService()
        apiService.fetchUserList()
    }
    
    func getLocalUserList() {
        let dbService = DBManagerService()
        dbService.fetchLocalUser()
    }
    
}

class ViewControllerA: UIViewController{
    let userManager: UserManager = UserManager()
    
    func getListUserData() {
        userManager.getUserList()
    }

}

// ViewControllerB cần hỗ trợ tính năng offline
class ViewControllerB: UIViewController {
    let userManager: UserManager = UserManager()
    
    func getLocalUserData() {
        userManager.getLocalUserList()
    }
}

{% endhighlight %}

So sánh với với cách thiết kế của phương pháp ứng dụng nguyên lý DIP:

{% highlight swift %}
protocol IUserService{
    func fetchUserList()
}

class APIService: IUserService {
    func fetchUserList() {
        // TODO: - Fetch User List by calling API
    }
}

class DBManagerService: IUserService {
    func fetchUserList() {
        // TODO: - Fetch User List from DB local
    }
}

class UserManager {
    
    let userService: IUserService
    
    init(userService: IUserService) {
        self.userService = userService
    }
    
    func getUserList(){
        userService.fetchUserList()
    }
    
}

class ViewControllerA: UIViewController{
    let userManager: UserManager = UserManager(userService: APIService())
    
    func getListUserData() {
        userManager.getUserList()
    }
}

// ViewControllerB cần hỗ trợ tính năng offline
class ViewControllerB: UIViewController {
    let userManager: UserManager = UserManager(userService: DBManagerService())
    
    func getListUserData() {
        userManager.getUserList()
    }
}

{% endhighlight %}

Bạn có để ý thấy điều đặc biệt?

Với cách thiết kế thứ 2, bạn hoàn toàn có thể swap qua lại các sub-module (APIService và DBManagerService) miễn là nó cùng kế thừa một Interface nào đó (ở đây là IUserService), điều này đem đến tính linh hoạt cho hệ thống của các bạn. Nếu xét tường tận, rõ ràng các module khác không quan tâm đến việc là listUser lấy được từ đâu (service hay local), vì với nó, nó chỉ cần dữ liệu đó để phục vụ cho tác vụ của nó, còn việc từ đâu mà có thì nó không nên (không cần luôn) biết.

### _**3. Đánh giá và kết luận:**_

Theo tư duy đại trà, lập trình viên thường có xu hướng xây dựng hệ thống theo kiểu top-down, nghĩa là một module to, chia thành các module nhỏ, các module nhỏ này có thể được chia nhỏ hơn nữa nếu cần. Mục đích của việc này không nằm ngoài việc tạo ra một sơ đồ luồng tổng quát, nhìn vào đó ta có thể thấy được cách mà các module to quản lý và thực thi các module nhỏ. Tuy nhiên, điều này lại khiến cho module to phụ thuộc vào các module nhỏ, và như đã phân tích trong suốt bài viết, điều này tiềm ẩn nhiều rủi ro. Việc tách mối liên hệ giữa module cấp cao và cấp thấp dựa trên abstractions được coi là việc làm ngược ( vì rõ ràng bình thường là top-down), ngược phương pháp, và ngược cả tư duy. Chữ ngược (inversion) trong nguyên lý, chính là biểu thị cho điều này.

Các dependency thường gắn liền với các rủi ro, sự rủi ro này đến từ nhiều khía cạnh, nhưng lý do cơ bản nhất là chúng rất dễ bị thay đổi.

Bản chất của DIP là vận dụng các abstractions. Các abstractions này cung cấp một góc nhìn đến đối tượng, mặt khác abstractions lại cực kì tối giản, hệ quả là giao tiếp đến abstractions cũng vô cùng đơn giản và thuận tiện. Abstractions là những cái chung chung nhất, do đó abstractions cung cấp khả năng hoán đổi linh hoạt, điều này giúp giảm chi phí vận hành đáng kể. (Vấn đề ưu điểm của việc hoán đổi, mình sẽ trình bày trong bài viết về Strategy Design pattern sau).

Bản thân DIP là nguyên lý, nó chỉ cung cấp khái niệm, còn việc ứng dụng và vận hành thế nào thì lại là câu chuyện khác. Cách thiết kế trong bài viết chỉ đơn giản để mô phỏng ứng dụng nhỏ, tuyệt nhiên không phải là cách duy nhất. Để đảm bảo DIP có khá nhiều design pattern, tuy nhiên có nhiều người hay nhầm lẫn khái niệm về các pattern đó với DIP, cụ thể thì mình sẽ trình bày ở phần 2 của bài viết, mình chỉ nhấn mạnh rằng: DIP ở mức nguyên lý, và mọi pattern khác chỉ để đảm bảo nguyên lý đó, không có nghĩa 2 cái là 1.
