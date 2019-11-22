Bài viết về Prototype đã khép lại phần giới thiệu cho loại Pattern đầu tiên: Creational. Và để tiếp nối chuỗi bài viết về chủ đề này, tôi xin được tiếp tục giới thiệu loại Pattern thứ 2: Structural. Mở đầu cho Structural và cũng là chủ đề chính của bài viết lần này, là một loại Pattern quen thuộc khác, mà khi nhắc đến tên, chắc chắn ai dù làm Lập trình viên hay không, đều đã nghe qua: Adapter Design Pattern.

# <span style="color: #ff9900;"> Structural Design Pattern </span>

**<span style="color: #993300;">Structural (structure)</span>** dịch ra là cấu trúc, mà nếu nói đến cấu trúc, thì ta có thể ngầm hiểu rằng chúng ta phải tiến hành xây dựng, liên kết, kết hợp,... cái gì đó để tạo nên một chỉnh thể khác to lớn hơn. Tham chiếu vào lĩnh vực lập trình hướng đối tượng, với đối tượng (Object) là trọng tâm, kết hợp với việc đây là **<span style="color: #993300;">Design Pattern</span>**, ta tiên đoán được **<span style="color: #993300;">Structural Design Pattern</span>** sẽ là tập hợp những Pattern xoay quanh giải quyết bài toán xây dựng các mối quan hệ giữa các Class (vì nó là abstract của Object) với nhau, để cấu thành nên một cấu trúc hoàn chỉnh, hiệu quả. Thật vậy, nếu như Creational Design Pattern đến giải quyết các bài toán liên quan đến việc khởi tạo Object, thì Structural Design Pattern lại trọng tâm đến kết hợp Class để hình thành cấu trúc tốt hơn.


# <span style="color: #ff9900;">Adapter Design Pattern </span>
## <span style="color: #3BC651;">Giới thiệu Pattern</span>
Có lẽ đây là Pattern dễ giới thiệu và cũng dễ để mọi người hình dung ra nhất, vì đơn giản nó xuất hiện quá quá nhiều, không phải chỉ ở lĩnh vực phần mềm, mà là chính trong cuộc sống đời thường của chúng ta. Chính vì vậy, để giải thích và minh họa cho bài viết lần này, tôi sẽ cố gắng viết theo lối viết giản dị, không hoa mỹ, và gắn với cuộc sống nhất có thể.
Nào, thử nghĩ xem, bạn bắt gặp cụm từ Adapter này ở những đâu rồi? 

Để sạc điện thoại, ta có dây sạc và một cục hình trụ cắm vào ổ điện, cục đó gọi là Adapter.

Để xuất dữ liệu lên màn hình thông qua cổng HDMI ở máy Mac đời gần đây, ta cũng có một cục giúp ta làm việc đó, ta gọi đó là Adapter.

Những thiết bị điện theo chuẩn Âu (3 chấu), ta muốn chuyển nó về dạng 2 chân để dùng ở Việt Nam, ta cần một thiết bị hỗ trợ việc chuyển đổi đó, ta gọi đó nó là Adapter.

Để xài tai nghe jack 3.5mm trên iPhone đời mới, ta cần phải chuyển đổi nó sang cổng Li-ning, và thiết bị giúp ta làm việc đó, ta cũng gọi nó là Adapter.

...

Vậy Adapter bản chất là một unit gắn kết 2 bộ phận không tương thích, giúp chúng có khả năng giao tiếp và làm việc với nhau.

Định nghĩa hơi xịn (trích từ sách):

> Convert the interface of a class into another interface clients expect. Adapter lets classes work together that couldn't otherwise because of incompatible interfaces.

Tạm dịch:
```
Chuyển đổi giao tiếp của một class thành giao tiếp của class khác (class client).
Adapter giúp các class vốn không hoạt động được với nhau vì lý do không tương thích giao tiếp, giờ có thể tương tác được với nhau.
```
 
Bình thường ở các blog trước, tôi không dịch từ Interface vì ý nghĩa trừu tượng của nó, nhưng trong trường hợp này, việc dịch nghĩa giúp ích cho việc tiếp thu. Có một số blog dịch từ Interface thành giao diện, cái này tôi cực không đồng ý, vì nó làm sai lệch hoàn toàn ý nghĩa và có thể khiến người đọc cảm thấy bối rối.

## <span style="color: #3BC651;">Phân tích định nghĩa</span>
Thế nào là Inteface (giao tiếp)?

Giao tiếp là input / output dữ liệu của một vật thể nào đó. Ví dụ: tôi nói / viết (output) và nghe / đọc (input) tiếng Việt Nam, nên giao tiếp của tôi là tiếng Việt Nam. Bạn nói và nghe tiếng Anh, giao tiếp
của bạn là tiếng Anh. Hiển nhiên, tôi không thể tương tác với bạn được, để làm được việc này, tôi cần phải có một công cụ nào đó nhận tiếng Việt và trả ra tiếng Anh cho bạn, hoặc ngược lại. Vì vậy, chúng ta có Goolge Translate, hay thông dịch viên, kĩ sư cầu nối,... đóng vai trò là các Adapter.

Nghe vĩ mô quá nhỉ, hãy thử đơn giản hóa với ví dụ jack 3.5mm ở trên nhé. Với cái tai nghe, nó chỉ có thể trao đổi thông qua cổng kết nối 3.5mm, còn với cái iPhone, nó chỉ có thể tiếp nhận trao đổi qua cổng Lighting, không nhận cái khác. Trời không chịu đất, đất cũng chẳng chịu trời, vậy phải làm sao ạ?
Ta có Adapter, với 2 đầu, 1 đầu là jack 3.5mm để kết nối với tai nghe, đầu còn lại là Lighting để nói chuyện được với iPhone (việc bên trong cái adapter đó xử lý cái gì, chuyển đổi tín hiệu ra sao thì ta không bàn ở đây, vì nó thuần kĩ thuật, hãy chú trọng đến mô hình - concept của nó để hiểu trước đã).


## <span style="color: #3BC651;">Thực hiện Pattern</span>
Giả sử ta có bài toán:

```swift

struct Macbook {
    var port: USBC = USBC()
    
    func displayOnScreen() {
        // accept & display via USB connection
    }
}


struct Monitor {
    var port: HDMI = HDMI()
    
    func render() {
        // TODO: rendering logic
    }
}
```


Như đã phân tích ở trên: công việc của Adapter là chuyển đổi và tương thích giao tiếp giữa 2 Class khác nhau, vì vậy, Adapter bắt buộc phải có đủ giao tiếp của cả 2 Class.

Câu hỏi đặt ra: Làm thế nào để Adapter có đủ giao tiếp ?

Theo góc nhìn trong OOP, ta có 2 cách để làm điều đó:
1. Kế thừa (inherit).
2. Composition.

### Kế thừa
Theo phương pháp này, Adapter sẽ kế thừa cả Macbook và Monitor (đa kế thừa):
<div style="display: flex; align-items: center; justify-content: center;">
  <img class="wp-image-1879 aligncenter" src="/assets/images/post/adapter_multi_inherit.png" alt="" width="300" height="300" srcset="/assets/images/post/adapter_multi_inherit.png" sizes="(max-width: 300px) 100vw, 300px" />
</div>

Tuy nhiên, cách thực hiện như trên có vấn đề:
- Trên thực tế, Inherit là bad practise, tính kế thừa trong hầu hết trường hợp đều được khuyên là nên tránh (bạn có thể đọc bài viết về Protocol-Oriented Programming của tôi để hình dung thêm). Cụ thể ra sao thì tôi sẽ nói ở các bài viết sau, còn bây giờ thì hãy tạm tin và ghi nhớ điều này.
- Swift không hỗ trợ đa kế thừa (Multiple Inherit), vì vậy cách này không thực hiện được. Tuy nhiên, khi giới thiệu về nó, nhóm tác giả Gang-of Four sử dụng ngôn ngữ C++ để miêu tả, và là ngôn ngữ hỗ trợ đa kế thừa. Mặt khác, tôi muốn đề cập đầy đủ để dù bạn có tìm hiểu sâu hơn nữa hoặc tra cứu thông tin bên ngoài, bạn cũng không bị ngỡ ngàng.


### Composition
Composition là thuật ngữ chỉ quan hệ giữa các Class / Object mà tôi đã từng đề cập ở các bài viết trước. Cụ thể và chi tiết, lại xin phép hẹn bạn bài viết sau, tôi sẽ giải thích tường tận hơn. Còn với bài viết hôm nay, bạn chỉ cần hiểu lướt qua: Class A là property trong Class B, thì A là composition của B.

Ta có thể minh họa Composition vào bài toán này thông qua UML sau:
<div style="display: flex; align-items: center; justify-content: center;">
  <img class="wp-image-1879 aligncenter" src="/assets/images/post/adapter_composition.png" alt="" width="600" height="300" srcset="/assets/images/post/adapter_composition.png" sizes="(max-width: 300px) 100vw, 300px" />
</div>

```swift

struct Macbook {
    var port: USBC = USBC()
    
    func displayOnScreen() {
        // accept & display via USB connection
    }
}


protocol HDMIDisplay {
    func render()
}

struct Monitor: HDMIDisplay {
    var port: HDMI = HDMI()
    
    func render() {
        // TODO: rendering logic
    }
}


struct HDMIAdapter: HDMIDisplay {
    
    let macbook: Macbook ////// COMPOSITION
    
    init(macbook: Macbook) {
        self.macbook = macbook
    }
    
    func render() {
        macbook.displayOnScreen() // mock-up logic
    }
}

```

## <span style="color: #3BC651;">Nhận xét Adapter Pattern</span>
Adapter giúp kết nối và giao tiếp giữa 2 module, class không tương thích với nhau mà không cần phải sửa đổi chúng.

Nghe quen không ?

Bạn đoán đúng rồi đó, Adapter tuân thủ chặt chẽ nguyên lý `Open-Closed Principle (trong bộ S.O.L.I.D)`. Bằng việc sử dụng Adapter, ta có thể dễ dàng tích hợp các module mới vào module cũ, mà không sợ ảnh hưởng đến chúng. Chính tính chất này giúp Adapter rất hữu dụng trong việc trong việc maintain và upgrade hệ thống. Adapter là giải pháp hiệu quả khi cần tương thích với những module đóng hoặc những module rủi ro khi sửa đổi (3rd library, framework, close-source, ...). Tuy nhiên, nhược điểm của Adapter là cồng kềnh (more codes more bugs). Theo kinh nghiệm cá nhân, tôi thường dùng Adapter với thư viện import, framework cũ, còn với bản thân source code thì tôi không dùng, hoặc dùng tạm thời, nhưng sẽ lên kế hoạch refactor quy về 1 chuẩn interface và loại bỏ Adapter đi.

## <span style="color: #3BC651;">Có gì cần chú ý?</span>
Khi tìm hiểu kĩ hơn, bạn sẽ thấy họ phân Adapter Pattern như sau:

<div style="display: flex; align-items: center; justify-content: center;">
  <img class="wp-image-1879 aligncenter" src="/assets/images/post/adapter_origin_design.png" alt="" width="600" height="300" srcset="/assets/images/post/adapter_origin_design.png" sizes="(max-width: 300px) 100vw, 300px" />
</div>
<!-- <p style="font-size: 12px; font-style: italic">(source: Design Patterns - Elements of reusable Object-Oriented Software.)<p> -->

Trong đó:
- Target: đối tượng / unit cần tương thích (ở đây là cái HDMIDisplay / Monitor)
- Adaptee: đối tượng / unit cần chuyển đổi interface (ở đây là cái Macbook)
- Adapter: unit đóng vai trò chuyển đổi interface của Adaptee sao cho tương thích với interface của Target (ở đây là HDMIAdapter)

Cách phân chia như vậy đơn giản, dễ dàng để theo dõi, cũng dễ nhớ, dễ thực hiện nữa. Hơn nữa, dù sao đây cũng là Pattern - tức là khuôn mẫu, là một cái khung đóng sẵn để chúng ta áp vào, vậy nên bạn có quyền hoài nghi về bài viết này của tôi. Tuy nhiên, tôi chọn cách tiếp cận vấn đề từ quan sát thực tế, hơn nữa, không phải lúc nào theo khuôn mẫu cũng là đúng, ví dụ như cách thực hiện Đa kế thừa ở trên kia. Bên cạnh đó, tôi khuyến khích cách tư duy dựa vào mục đích (intent) của pattern hơn, vì đó mới là mục đích ra đời của design pattern. Công nghệ luôn cập nhật và ngôn ngữ lập trình cũng vậy, với Adapter Design Pattern, mục đích của nó là **<span style="color: #993300;">Convert the interface of a class into another interface clients expect</span>**, tôi hoàn toàn có thể biến đổi cấu trúc code như sau:

```swift
extension Macbook: HDMIDisplay {
    func render() {
        self.displayOnScreen() // mockup - logic
    }
}
```
Tôi hoàn toàn có thể vứt cục adapter đi mà vẫn đạt được mục đích của mình. Đó là lý do mà nếu bạn tìm kiếm Adapter Pattern cho Swift, sẽ có nhiều bài viết lựa chọn cách làm trên của tôi. Nếu bạn từng làm việc với phần Alamofire nâng cao (advanced), bạn sẽ thấy họ tích hợp một class là **<span style="color: #993300;">RequestAdapter</span>** với concept như tôi vừa làm trên, chứ không phải theo pattern chuẩn.



# <span style="color: #ff9900;"> Kết luận</span>
Lại thêm một Design Pattern nữa được giới thiệu, Adapter Pattern vẫn luôn là một trong những Pattern tôi yêu thích, nhất là ý tưởng của nó và sự gắn kết với đời sống thực tế.

Tóm lại, Tôi cần bạn nhớ:
- Structural Design Pattern là gì, và nó khác gì với Creational Design Pattern
- Adapter là gì: định nghĩa, cách thực hiện.
- Adapter pattern có gì hay, có gì đặc biệt, và có gì cần chú ý?

Cá nhân tôi không rõ mọi người có thích bài viết lần này không, vì tôi đưa khá nhiều quan điểm cá nhân vào. Hiện thời blog này tôi chưa tích hợp phần comment, nên nếu bạn có gì khúc mắc, cứ thoải mái liên hệ tôi thông qua Facebook / Github / Twitter ở phía dưới Footer.

Link tham khảo:
- https://refactoring.guru/design-patterns/adapter
- https://refactoring.guru/design-patterns/adapter/swift/example
- https://dzone.com/articles/the-adapter-pattern-in-swift
- https://sourcemaking.com/design_patterns/adapter
- https://www.geeksforgeeks.org/adapter-pattern/


