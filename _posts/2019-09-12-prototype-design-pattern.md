---
id: 1871
title: Prototype Design Pattern
date: 2019-09-12T10:11:33+00:00
author: starptit
# layout: post
guid: http://swiftyvn.com/?p=1871
permalink: /2019/09/prototype-design-pattern/
categories: [Uncategorized, Swift]
comments: true
# tags: Swift
---
Welcome back, series về Design Pattern xin được tiếp tục, với một Design Pattern phổ biến khác: Prototype Design Pattern.

# Giới thiệu Prototype Pattern

Prototype Design Pattern thuộc loại Creation, đồng nghĩa với việc nó sẽ giải quyết một vấn đề nào đó của bài toán khởi tạo Object. `Prototype` dịch ra nghĩa là nguyên mẫu, nguyên bản, kết hợp với suy luận trên, ta có thể ngầm tiên đoán rằng ý tưởng của Pattern này là xây dựng, khởi tạo nguyên mẫu, nguyên bản của Object. 
Điều này có đúng không? Hãy thử so sánh với định nghĩa của nó:
> “Specify the kinds of objects to create using a prototypical instance, and create new objects by copying this prototype.”

Tạm dịch: Định rõ loại đối tượng cần khởi tạo bằng việc sử dụng nguyên mẫu, và khởi tạo bằng cách sao chép nguyên mẫu đó. (bản dịch này hơi cùi ಠ_ಠ) .

Đúng vậy, khởi tạo object thông qua các prototype của nó, và bằng cách copy chứ không initiate trực tiếp. Chắc hẳn trong đầu bạn đang có hàng tá câu hỏi kiểu như: tại sao lại là prototype, tại sao lại chọn cách copy,....?

# Phân tích định nghĩa Prototype Design Pattern
## Tại sao lại copy mà không initiate trực tiếp?
Ta sẽ đặt câu hỏi, tại sao lại phải copy, mà không trực tiếp initate instance khác, dựa trên instance hiện có, điều mà hiển nhiên đơn giản hơn. Phần lớn thời gian, bạn sẽ không cần phải copy object đâu, nhưng tại sao chúng ta lại phải sử dụng nó trong Prototype Pattern?
Khi tìm hiểu thông tin trên mạng, tôi được kha khá tài liệu giải thích rằng: những object mà cần phải copy là các `complex object` (phức tạp) hoặc `cost on initiating`(chi phí khởi tạo cao).  

Thế nào là phức tạp, thế nào là chi phí cao, thì họ không nói (╯°□°）╯︵ ┻━┻

Thử tư duy ngược xem:

Giả sử tôi có class như sau:
```swift

class Utility {
    private let apiConnection: NetworkConnector
    private let dbConnection: DatabaseConnector
    
    init() {
        apiConnection = NetworkConnector()
        dbConnection = DatabaseConnector()
    }
}

let instance1 = Utility()

```

Việc initiate class Utility, tương đương với việc phải khởi tạo đồng thời NetWorkConnector và DatabaseConnector. 2 class trên thực tế rất nặng, tương ứng với việc khởi tạo Utility cũng nặng, tức là, chi phí khởi tạo của nó cao. Như vậy, những class mà hàm khởi tạo cồng kềnh, hoặc yêu cầu các bước phức tạp, hoặc gây tốn nhiều tài nguyên khi khởi tạo,... là những class nên sử dụng Prototype.

Ví dụ khác:
```swift

class User {
    private let name: String
    private let age: Int
    private let address: String
    private let phone: String
    
    init(name: String,
         age: Int,
         address: String,
         phone: String) {
        self.name = name
        self.age = age
        self.address = address
        self.phone = phone
    }
}

let userA = User(name: "Shaw", age: 27, address: "Ha Noi", phone: "1900 1003")
let copyUserA = User(name: userA.name, age: userA.age, address: userA.adress, phone: userA.phone)

```

compiler sẽ báo lỗi ở copyUserA, vì đơn giản rằng các property của class User được định nghĩa là private, bạn không thể truy cập vào chúng để lấy giá trị để khởi tọa nên bản copyUserA được. Bạn có thể phản biện rằng thực chất tôi có thể tạo ra hàm get/set cho các property như những ngôn ngữ khác, và lập luận trên không còn đúng nữa. Tuy nhiên, tôi phải nhắc bạn rằng, không phải property nào cũng nên có đầy đủ get/set, có trường hợp property chỉ cho phép set mà thôi, đặc biệt, trong môi trường Application Runtime, việc truy cập bừa bãi vào các property sẽ rất dễ gây ra lỗi bảo mật, hoặc các vấn đề khác nghiêm trọng hơn. Cụ thể ra sao, sang phần sau sẽ rõ.

<img class="wp-image-1879 aligncenter" src="/assets/images/post/prototype_copy_outside.png" alt="" width="600" height="300" srcset="/assets/images/post/prototype_copy_outside.png" sizes="(max-width: 300px) 100vw, 300px" />
(Source: refactoring.guru)

# Thực hiện Proptotype Pattern
Tôi có bài toán giả định như sau, bạn đang xây dựng ứng dụng Mobile Banking (tương tự như mấy app Paypal, TPBank, BIDV, ...). Bất kì ứng dụng Mobile Banking nào cũng bao gồm chức năng chuyển tiền, thế nên tôi có class:

```swift
class PaymentDetail {
    private var senderAccount: Account
    private var receiverAccount: Account
    private var amount: Float // in Dollar $
    private var tax: Float // in percent
    private var note: String
    
    init(senderAccount: Account, receiverAccount: Account,
         amount: Float, tax: Float, note: String) {
        self.senderAccount = senderAccount
        self.receiverAccount  = receiverAccount
        self.amount = amount
        self.tax = tax
        self.note = note
    }
}
```

PaymentDetail thể hiện giao dịch giữa 2 bên người cho (senderAccount) và nhận (receiverAccount), một giao dịch được thực hiện thông qua một `phiên giao dịch (Transaction)`

```swift

class Transaction {
    func createTransaction(withPayment payment: PaymentDetail) {
        // send money via Payment
        // do stuff
    }
}
```

Hãy chú ý, đây là ứng dụng liên quan đến vấn đề chuyển tiền, việc tương tác với một PaymentDetail trực tiếp là cấm kỵ, có nhiều case phát sinh lỗi phức tạp (chuyển tiền không thành công, chuyển tiền vượt quá hạn mức, ....), thay vào đó, chúng ta nên tương tác với một bản copy tương ứng của nó, và đây là cơ hội để áp dụng Prototype Pattern. Bạn có thể nghi ngờ lại tại sao không dùng get/set và khởi tạo một object mới dựa trên object cũ, giống như đã tranh cãi ở trên phải không? Hãy nhớ, đây là ứng dụng yêu cầu tính bảo mật, các thông tin như tài khoản người gửi và người nhận không bao giờ có thể public được, vì trên môi trường Application Runtime, bạn không thể kiểm soát được hết tác nhân nào truy cập vào thông tin nhạy cảm đó.

```swift

/// CÁCH LÀM NÀY QUÁ NGÂY THƠ, SẼ BỊ CLOSE VÀ ĂN BLAME TRONG 1 NỐT NHẠC

class PaymentDetail {
    var senderAccount: Account // easy access
    var receiverAccount: Account // easy access
    private var amount: Float // in Dollar $
    private var tax: Float // in percent
    private var note: String
    
    init(senderAccount: Account, receiverAccount: Account,
         amount: Float, tax: Float, note: String) {
        self.senderAccount = senderAccount
        self.receiverAccount  = receiverAccount
        self.amount = amount
        self.tax = tax
        self.note = note
    }
}


class Transaction {
    func createTransaction(withPayment payment: PaymentDetail) {
        let clone = PaymentDetail(senderAccount: payment.senderAccount, receiverAccount: payment.receiverAccount
        ....
        // do stuff
    }
}
```

Initiate trực tiếp không được, Initiate từ object khác cũng không được, vậy chúng ta làm thế nào? Theo Prototype Pattern, cách đơn giản nhất: **COPY**.
Thật may mắn, Swift / Objective-C đã support sẵn cách copy object, thông qua NSCopying:

```swift
class PaymentDetail: NSObject, NSCopying {
    private var senderAccount: Account
    private var receiverAccount: Account
    private var amount: Float // in Dollar $
    private var tax: Float // in percent
    private var note: String
    
    init(senderAccount: Account, receiverAccount: Account,
         amount: Float, tax: Float, note: String) {
        self.senderAccount = senderAccount
        self.receiverAccount  = receiverAccount
        self.amount = amount
        self.tax = tax
        self.note = note
    }
    
    func copy(with zone: NSZone? = nil) -> Any {
        let clone = PaymentDetail(senderAccount: senderAccount, receiverAccount: receiverAccount, amount: amount, tax: tax, note: note)
        return clone
    }
}

class Transaction {
    func createTransaction(withPayment payment: PaymentDetail) {
        let clone = payment.copy(with: nil)
        // do stuff
    }
}
```
Đơn giản, dễ dùng, và quan trọng nhất là hiệu quả, đây chính là Prototype Pattern. Tương tự với trường hợp **`Utility class`** ở trên, ta chỉ cần sử dụng NSCopying là xong:

```swift
class Utility: NSCopying {
    private let apiConnection: NetworkConnector
    private let dbConnection: DatabaseConnector

    init() {
        apiConnection = NetworkConnector()
        dbConnection = DatabaseConnector()
    }
    
    func copy(with zone: NSZone? = nil) -> Any {
        let clone = Utility()
        return clone
    }
}

let instance = Utility()
let clone = instance.copy(with: nil)
```

Ơ nhưng mà, sao không dùng STRUCT ? Không phải struct copy đơn giản hơn class rất rất nhiều không ?
Câu trả lời đơn giản nhất là: không phải lúc nào bạn cũng có thể dùng struct, có nhiều lúc bạn buộc phải sử dụng class. Tuy nhiên, câu trả lời này là phần nổi của tảng băng chìm mà thôi, đoạn hay còn ở phía sau, cứ từ từ !

# Có gì cần chú ý ?
Chúng ta bàn nhiều về cách khởi tạo, và thống nhất có những trường hợp nên dùng Copy. Tuy nhiên, Copy như thế nào, và copy có gì đặc sắc cần để ý hay không, thì chúng ta chưa nhắc đến.
Thực tế, phương pháp Copy được chia thành 2 loại: **Shallow Copy** và **Deep Copy**

## Shallow Copy vs Deep Copy
**Shallow Copy** (sao chép bề mặt): giả sử ta có Object A, khi Object B sao chép Object A, ta sao chép toàn bộ property của A sang B, nếu property đó là primitive type (Int, String, Float,...) ta sẽ copy nó thành primitive type tương ứng, nếu như nó là *++reference++* (tham chiếu), thì *++reference++* cũng được copy, hay nói cách khác, A và B share reference, pointer sẽ trỏ đến cùng một vùng nhớ. Hệ quả là nếu A thay đổi thì B cũng thay đổi theo. Nghe quen quá nhỉ? Đúng, nó chính là ý tưởng của `Reference Type`, hay những Object được khởi tạo qua từ khóa Class trong Swift.

**Deep Copy** (sao chép sâu): cũng tương tự như Shallow copy, tuy nhiên chúng không share reference, thay vào đó, chúng sẽ khởi tạo reference hoàn toàn mới. Điều này khiến chi phí của Deep Copy sẽ lớn hơn Shallow Copy, tuy nhiên điểm lợi thế ở đây là reference sẽ hoàn toàn độc lập, thay đổi B sẽ không làm A thay đổi,... Vâng, và đó cũng là ý tưởng của `Value Tye`, tương ứng với Struct, Array, Tupble, String, Int,.... trong Swift.

<img class="wp-image-1879 aligncenter" src="/assets/images/post/shallow_deep_copy.jpg" alt="" width="400" height="200" srcset="/assets/images/post/shallow_deep_copy.jpg" sizes="(max-width: 300px) 100vw, 300px" />

(Source: stackoverflow)

--> Nên dùng Shallow Copy hay Deep Copy ?

Câu trả lời là ***TÙY***: tùy bài toán, tùy use case, tùy trường hợp,... cũng giống như việc nên dùng Class hay Struct vậy.

Giả sử với bài toán Payment trên, nên dùng Deep Copy, hoặc những bài toán phức tạp như liên quan đến multithread,... thì nên dùng Deep Copy.

Với cá nhân tôi, tôi thường sử dụng cơ chế Deep Copy khi áp dụng Prototype Design Pattern. Bạn có thể sẽ ngạc nhiên khi tôi nói thế, vì ở trên rõ ràng là tôi sử dụng ***`Class`*** trong cả 2 trường hợp mà. Tuy nhiên, ở trên tôi dùng `NSCopying`, đồng nghĩa với việc tôi biến các class copy lại nó trở thành dạng Deep Copy. Ngoài ra, bạn có thể dùng `Codable` trong Swift để có hiệu quả tương tự.

# Tổng kết
Tôi đã hoàn tất bài viết của mình về Prototype Pattern - một Design Pattern đơn giản, dễ thực hiện. Tuy nhiên, tôi vẫn lưu ý các bạn cần phải nhớ các điểm sau:

- Khi ta cần khởi tạo các Object mà constructor của nó phức tạp, chi phí khởi tạo cao,... thì hãy nhớ đến Prototype Design Pattern. Còn phức tạp, chi phí khởi tạo cao là gì, thì mời đọc lại phần đầu của bài viết.
- Phân biệt được Shallow Copy và Deep Copy, và hãy lựa chọn nó thích hợp nhất khi áp dụng Prototype Design Pattern.
- Hãy tự đánh giá điểm mạnh, điểm yếu của Pattern này.

Thực tế, ý tưởng về Prototype xuất hiện quanh ta, ví dụ nhé, sự phân bào sinh học:
<img class="wp-image-1879 aligncenter" src="/assets/images/post/prototype_cell_division.png" alt="" width="600" height="300" srcset="/assets/images/post/prototype_cell_division.png" sizes="(max-width: 300px) 100vw, 300px" />

(Source: refactoring.guru)