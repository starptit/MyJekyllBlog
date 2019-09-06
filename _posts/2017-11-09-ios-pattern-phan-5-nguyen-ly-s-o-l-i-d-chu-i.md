---
id: 1632
title: "iOS pattern: Phần 5: Nguyên lý S.O.L.I.D (chữ I )"
date: 2017-11-09T15:54:07+00:00
author: starptit
# layout: post
guid: http://www.swiftyvn.com/?p=1632
permalink: /2017/11/ios-pattern-phan-5-nguyen-ly-s-o-l-i-d-chu-i/
tags: [Uncategorized, Swift]
---

Hôm trước trên group, có một bạn chia sẻ rằng đi phỏng vấn bị một anh hỏi xoáy về sự khác biệt giữa Delegate và DataSource trong iOS. Nếu là bạn thì bạn trả lời ra sao?  
Với mình, câu hỏi trên hoàn toàn vô nghĩa, câu trả lời đơn giản là về bản chất nó chẳng khác gì nhau.  
Khoan đợi đã, nếu không khác nhau thì tại sao họ lại phải chia ra?  
&#8211;> Đáp án chính là chủ đề của bài viết hôm nay: Interface Segregation Principle (ISP &#8211; chữ I), nguyên lý phân tách Interface.

(Note: Interface là một khái niệm phổ biến trong lập trình hướng đối tượng, với Swift và Objective-C, Interface được thể hiện bằng keyword Protocol. Tuy nhiên, trong thiết kế và nghiên cứu về OOP, Interface là từ được sử dụng chung cho mọi ngôn ngữ, do đó trong blog của mình, mình vẫn ưu tiên dùng Interface thay cho Protocol.)

## **1. Nguyên lý ISP là gì (What is ISP) ?**

> CLIENTS SHOULD NOT BE FORCED TO DEPEND UPON INTERFACES  
> THAT THEY DO NOT USE.

(Tạm dịch: &#8220;Clients&#8221; không nên bị &#8220;force&#8221; phải phụ thuộc vào những &#8220;Interfaces&#8221; mà Clients không sử dụng.)

&#8211; Clients: không phải chỉ là người sử dụng, clients ở đây là các class/module implement các interface mà chúng ta thiết kế.  
&#8211; force: ép buộc phải tuân theo, interface có một đặc điểm là khi implement, bạn buộc phải implement toàn bộ method đã dược define của nó (tuy nhiên với Swift/Objective-C, chúng ta có thể sử dụng keyword Optional để điều chỉnh việc này).

## **2. Tại sao lại cần ISP (Why ISP) ?**

Ta thử đặt ngược lại câu hỏi? Nếu không có ISP thì sao? Nghĩa là Clients phụ thuộc vào các Interface mà nó không sử dụng.

Hãy nhìn vào một ví dụ thực tế:  
[<img class="size-full wp-image-1647 aligncenter" src="http://206.189.90.168/wordpress/wp-content/uploads/2017/11/image.axd_.jpeg" alt="" width="486" height="484" srcset="/wp-content/uploads/2017/11/image.axd_.jpeg 486w, /wp-content/uploads/2017/11/image.axd_-150x150.jpeg 150w, /wp-content/uploads/2017/11/image.axd_-300x300.jpeg 300w, /wp-content/uploads/2017/11/image.axd_-100x100.jpeg 100w" sizes="(max-width: 486px) 100vw, 486px" />](http://206.189.90.168/wordpress/wp-content/uploads/2017/11/image.axd_.jpeg)

&#8211; Cái cổng nào mới là hợp lý để nhét vào cái iPhone bên cạnh?  
&#8211; Cái iPhone chỉ có 1 cổng giao tiếp là Jack 3.5mm &#8211;> còn đống HDMI, microUSB,&#8230; kia là thừa thãi, cồng kềnh, vướng víu, gây bất tiện khi sử dụng.

Khi mapping vào việc Coding của chúng ta, khi nhận được một Interface to đùng, hiển nhiên chúng ta cũng sẽ nảy sinh trong đầu những câu hỏi tương tự:  
&#8211; Cần dùng method nào?  
&#8211; Các method còn lại thì sao?  
&#8211; Chúng ta phải implement một đống method thừa thãi để làm gì?  
&#8211; Complier phải tốn thời gian biên dịch những method không cần sử dụng đó.

## **3. Sử dụng ISP như thế nào (How to use ISP) ?**

Bản chất của vấn đề ở đây là việc chúng ta đã sử dụng một Interface quá to.  
&#8211;> Chúng ta chỉ cần chia nhỏ Interface đó ra, và lợi dụng tính chất Class có thể implement nhiều interface để kết hợp chúng lại nếu cần thiết.  
**_Tuy nhiên, chia nhỏ thế nào?_**  
Hiển nhiên việc đơn giản nhất là mỗi method, chúng ta chia nó ra thành 1 Interface. Cách làm này về mặt lý thuyết là đúng, nhưng lại làm nảy sinh vấn đề khác, làm project phình to vì phải tạo nhiều Interface, và trên thực tế, để hiệu quả hơn, người ta thường nhóm một vài method lại, dựa trên tiêu chí chung nào đó phụ thuộc vào nhu cầu sử dụng của họ. Các tiêu chí nhóm này không phải luôn cố định, do đó độ hiệu quả của nguyên lý này phụ thuộc vào cách phân tích thiết kế và kinh nghiệm của lập trình viên. Thông thường, với mình, mình hay xét trên một số tiêu chí:  
&#8211; Không quá 5 method trong một Interface ( 5 là con số mình tự đề ra, vì mình thấy nó là con số không quá to, cũng không quá nhỏ).  
&#8211; Mục tiêu và nhiệm vụ của các method (ví dụ như nhóm các method xử lý login vào chung một interface, các method sử lý signup vào chung một interface).  
&#8211; Những yêu cầu thay đổi, logic có thể phát sinh khiến interface thay đổi.  
&#8211; Những use case, test case đặc biệt có thể khiến interface hoạt động sai.

## **4. Ví dụ thực tế:**

[<img class=" wp-image-1648 aligncenter" src="http://206.189.90.168/wordpress/wp-content/uploads/2017/11/IMG_0967-576x1024.png" alt="" width="354" height="630" srcset="/wp-content/uploads/2017/11/IMG_0967-576x1024.png 576w, /wp-content/uploads/2017/11/IMG_0967-169x300.png 169w, /wp-content/uploads/2017/11/IMG_0967-768x1365.png 768w, /wp-content/uploads/2017/11/IMG_0967.png 1242w" sizes="(max-width: 354px) 100vw, 354px" />](http://206.189.90.168/wordpress/wp-content/uploads/2017/11/IMG_0967.png)

Giả sử với bài post trên, chúng ta có thể: Like, Comment, Share, Download ảnh. Tương ứng, ta có Interface sau:

<pre class="theme:sublime-text toolbar:2 lang:swift decode:true">protocol IFacebookContent{
    func like()
    func addComment()
    func shareContent()
    func downloadContent()
}

class ImageHandler:IFacebookContent{
    func like() {
        //TODO: Like Image
    }
    
    func addComment() {
        //TODO: Add Comment to Image
    }
    
    func shareContent() {
        //TODO: Share Image
    }
    
    func downloadContent() {
        //TODO: Download Image
    }
}
</pre>

Facebook muốn hỗ trợ Video và cho phép hiển thị content theo dạng Video:  
[<img class=" wp-image-1649 aligncenter" src="http://206.189.90.168/wordpress/wp-content/uploads/2017/11/IMG_0968-576x1024.jpg" alt="" width="317" height="563" srcset="/wp-content/uploads/2017/11/IMG_0968-576x1024.jpg 576w, /wp-content/uploads/2017/11/IMG_0968-169x300.jpg 169w, /wp-content/uploads/2017/11/IMG_0968-768x1365.jpg 768w, /wp-content/uploads/2017/11/IMG_0968.jpg 1242w" sizes="(max-width: 317px) 100vw, 317px" />](http://206.189.90.168/wordpress/wp-content/uploads/2017/11/IMG_0968.jpg)

<pre class="theme:sublime-text toolbar:2 lang:swift decode:true">class VideoHandler:IFacebookContent{
    func like(){
        //TODO: Like Video
    }
    
    func addComment() {
        //TODO: Add Comment to Video
    }
    
    func shareContent() {
        //TODO: Share Video
    }
    
    func downloadContent() {
        //Oops, Facebook chưa cho phép người dùng tải Video
    }
}
</pre>

&#8211;> function downloadContent cho Video bị lỗi. Giả sử VideoHandler được gọi hoặc được sử dụng trong module A, module A lại được module B gọi,&#8230; &#8211;> rất tốn thời gian để dò lỗi và có thể ảnh hưởng lẫn nhau dẫn đến việc phải test lại.

Rồi một ngày anh Mark yêu cầu app của anh ấy phải đảm bảo được tính riêng tư và bảo mật, như là tôi là chủ tài khoản, tôi chỉ muốn cho bạn bè của tôi comment/like và tương tác với tôi:

[<img class=" wp-image-1650 aligncenter" src="http://206.189.90.168/wordpress/wp-content/uploads/2017/11/IMG_0969-576x1024.png" alt="" width="429" height="763" srcset="/wp-content/uploads/2017/11/IMG_0969-576x1024.png 576w, /wp-content/uploads/2017/11/IMG_0969-169x300.png 169w, /wp-content/uploads/2017/11/IMG_0969-768x1365.png 768w, /wp-content/uploads/2017/11/IMG_0969.png 1242w" sizes="(max-width: 429px) 100vw, 429px" />](http://206.189.90.168/wordpress/wp-content/uploads/2017/11/IMG_0969.png)

Như ảnh trên, ta thấy người dùng hiện tại chỉ có duy nhất quyền được share nội dung:

<pre class="theme:sublime-text toolbar:2 lang:swift decode:true ">class PersonalContentHandler:IFacebookContent{
    func like(){
        //OOps, không phải bạn tôi, ai cho anh like
    }
    
    func addComment() {
        //OOps, không phải bạn tôi, ai cho anh comment
    }
    
    func shareContent() {
        //TODO: Share Content
    }
    
    func downloadContent() {
        //OOps, không phải bạn tôi, ai cho anh download
    }
}
</pre>

## **5. Cách khắc phục:**

Tuân theo nguyên lý phân tách Interface (ISP), nhiệm vụ của ta là chia nhỏ Interface trên:

<pre class="theme:sublime-text toolbar:2 lang:swift decode:true ">protocol ILikeContent{
    func likeContent()
}

protocol ICommentContent{
    func addComment()
}

protocol IShareContent{
    func shareContent()
}

protocol IDownloadContent{
    func downloadContent()
}
</pre>

Các class/module con lúc này sẽ chỉ implement cái mà chúng cần:

<pre class="theme:sublime-text toolbar:2 lang:swift decode:true">class ImageHandler:ILikeContent,ICommentContent,IShareContent,IDownloadContent{
    func likeContent() {
        //TODO: Like Image
    }
    
    func addComment() {
        //TODO: Add Comment to Image
    }
    
    func shareContent() {
        //TODO: Share Image
    }
    
    func downloadContent() {
        //TODO: Download Image
    }
}

class VideoHandler:ILikeContent,ICommentContent,IShareContent{
    func likeContent(){
        //TODO: Like Video
    }
    
    func addComment() {
        //TODO: Add Comment to Video
    }
    
    func shareContent() {
        //TODO: Share Video
    }
}

class PersonalContentHandler:IShareContent{
    func shareContent() {
        //TODO: Share Content
    }
}
</pre>

## **6. Tổng kết:**

Nguyên lý phân tách các Interface (ISP) là một nguyên lý cực kỳ phổ biến, mục tiêu chính của nó là chia một Interface cồng kềnh thành các Interface nhỏ, để dễ thao tác, xử lý cũng như maintain hơn. Việc chia nhỏ này cũng phù hợp với triết lý &#8220;Chia để trị&#8221; (Divide and conquer) nổi tiếng trong ngành phần mềm. Ý tưởng của ISP khá đơn giản và dễ tiếp cận, được ứng dụng trong hầu hết các framework hoặc thư viện lớn (ví dụ như Delegate & Datasource ở phần mở bài), tuy nhiên để sử dụng linh hoạt, đòi hỏi lập trình viên phải có kinh nghiệm, biết phân tích thiết kế sao cho phù hợp với yêu cầu của từng bài toán.
