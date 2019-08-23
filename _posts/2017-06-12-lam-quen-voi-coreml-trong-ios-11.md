---
id: 959
title: Làm quen với CoreML trong iOS 11
date: 2017-06-12T08:03:44+00:00
author: starptit
layout: post
guid: https://devislifeblog.wordpress.com/?p=959
permalink: /2017/06/lam-quen-voi-coreml-trong-ios-11/
categories: [Uncategorized, Swift]
---

Tại hội nghị WWDC 2017 đang diễn ra, Apple đã ra mắt một bộ kit mới, hỗ trợ cho việc tích hợp học máy (Machine Learning &#8211; ML), đó chính là CoreML. Bản thân mình cũng đang chân ướt chân ráo vào ML được một thời gian ngắn, nên mình quyết định viết blog này nhằm mục đích chia sẻ và giới thiệu những gì mình biết, mình hiểu, và hi vọng sẽ cung cấp được cho các bạn cái nhìn sơ khai nhất về ML và CoreML trong iOS.

Trước khi đi vào vấn đề chính, mình sẽ chia sẻ qua một chút kiến thức ở dạng vỡ lòng nhất của ML, nhằm tạo mindset cho các bạn về vấn đề mà chúng ta sẽ tìm hiểu trong bài viết này. ML thật sự là một lĩnh vực rất lớn, để nói về nó thì không thể chỉ vỏn vẹn trong một vài bài viết được, hơn nữa, người viết cũng thừa nhận bản thân không đủ kiến thức để chia sẻ toàn bộ ML cho các bạn. Dựa trên tinh thần chia sẻ và học tập, nếu các bạn có thắc mắc hay câu hỏi gì, hãy để lại comment và mình sẽ hồi đáp.

<!--more-->

<h1 style="text-align:center;">
  <strong>Phần I: ML trong tầm tay.</strong>
</h1>

1. _**Nghĩ khác đi:**_

Ví dụ thực tiễn về AI và ML hiện tại không thiếu, các hệ thống nhận dạng khuôn mặt, vật thể, giọng nói,&#8230; hay các hệ thống tự đưa ra quyết định như xe tự hành, Alpha Go,&#8230; ML xuất hiện khắp mọi với tốc độ chóng mặt và độ chuẩn xác cực kỳ cao. Chúng ta hẳn sẽ tự hỏi, điều gì đã đem đến sức mạnh cho ML, và nó có gì khác so với những gì chúng ta từng biết hay không?

Ta lấy ví dụ đơn giản với hệ thống nhận dạng vật thể thông qua ảnh, bạn đưa vào một bức ảnh, chẳng hạn là con mèo, bạn muốn nó trả cho bạn kết quả &#8220;đó là ảnh của con mèo&#8221;, theo bạn, nó sẽ làm thế nào ?

Đây là bài toán filter thông thường trong lập trình, việc của chúng chỉ là for loop để duyệt, rồi tìm ra bức ảnh giống hoặc gần giống nhất với cái ảnh ta nhét vào, rồi xài mấy thuật toán tối ưu như là sắp xếp trước (sort) filter sau hoặc xài multithreading để duyệt cho nhanh, so easy. Thế nhưng bạn ơi, nếu dữ liệu của bạn lên đến hàng trăm nghìn, rồi hàng triệu thậm chí hàng trăm triệu thì sao? Đó mới chỉ là 1 đầu vào, đến khi họ muốn nhét thêm nhiều đầu vào (ở ví dụ này là nhét thêm ảnh mèo, ảnh gấu) thì sao??

Hồi chưa biết, mình cũng từng nghĩ như thế, và mình cũng băn khoăn là nếu như vậy thì làm sao mà AI nó đưa kết quả nhanh được như vậy. Không, suy nghĩ đó là SAI HOÀN TOÀN, hãy bỏ nó đi, clear your mind.

Cùng nghĩ về cụm từ &#8220;Học Máy&#8221; (Machine Learning) &#8211; nghĩa là ta cho cái máy nó học. Vậy cái máy thì nó học gì? Đúng, chính là học các dữ liệu mà bạn cung cấp. Nhưng cái chúng ta đang khúc mắc ở đây chính là động từ &#8220;HỌC&#8221;, với một cái máy tính, học ở đây là làm gì? Nhìn lại vấn đề, bài toán thực sự của chúng ta là chuyển một tập ảnh vật thể xác định, sang một tập các kết quả phán quyết (con mèo, con gà, con gấu, &#8230; ). Đây chính là bài toán ánh xạ trong toán học:<figure id="attachment_1037" style="width: 330px" class="wp-caption aligncenter">

<img class=" size-full wp-image-1037 aligncenter" src="https://devislifeblog.files.wordpress.com/2017/06/330px-codomain2-svg.png" alt="330px-codomain2-svg" width="330" height="248" srcset="/wp-content/uploads/2017/06/330px-codomain2-svg.png 330w, /wp-content/uploads/2017/06/330px-codomain2-svg-300x225.png 300w" sizes="(max-width: 330px) 100vw, 330px" /> <figcaption class="wp-caption-text">(nguồn: wikipedia)</figcaption></figure>

ánh xạ là việc 1 đại lượng trong tập X, cho ra 1 kết quả nằm trong tập Y, dựa trên công thức tính toán của hàm f. Bạn có thấy nó quen quen không? Đúng, nó chính là ML mà chúng ta đang nói đến đấy. Ở đây X là tập các ảnh vật thể, còn Y là các nhãn phân loại con vật (mèo, gà, chó,..) mà mình nói ở trên. Đầu vào của chúng ta là một bức ảnh (tức là nằm trong tập &#8220;ảnh&#8221; &#8211; X), và đầu ra là kết quả phán định ảnh này là ảnh con mèo (tập Y) . Vậy ML làm gì? Thực ra việc của ML là tìm ra mối liên hệ ánh xạ giữa X và Y, hay nói cách khác, việc &#8220;học&#8221; ở đây chính là tìm ra hàm f, dựa trên X và Y.

Vậy, việc tìm ra hàm f có ý nghĩa gì?

**_2. Sự khác biệt:_**

Như đã nói ở trên, hàm f chính là công thức, là chìa khóa để chúng ta có thể ánh xạ qua lại giữa đầu vào và đầu ra. Khác với cách giải bằng phương pháp lọc (filter) ban đầu, giờ đây mỗi khi chúng ta có đầu vào (một bức ảnh), đưa nó qua hàm f để tính, và nhận kết quả đầu ra. Việc tính toán này rất nhanh, vì lúc này chúng ta chỉ áp dụng công thức toán học, so với việc phải dò trong tập dữ liệu ban đầu.

Tuy nhiên, việc tìm ra hàm f này cực kỳ phức tạp, trên thực tế, chúng ta không tìm hàm f, mà thay vào đó chúng ta cố gắng tìm một hàm h nào đó, sao cho nó gần giống với hàm f nhất có thể, cái gần giống ở đây chính là việc cho ra kết quả dựa trên đầu vào, phải gần nhau:<figure id="attachment_1073" style="width: 349px" class="wp-caption aligncenter">

<img class="  wp-image-1073 aligncenter" src="https://devislifeblog.files.wordpress.com/2017/06/screen-shot-2016-07-23-at-7-05-47-am.png" alt="screen-shot-2016-07-23-at-7-05-47-am" width="349" height="137" srcset="/wp-content/uploads/2017/06/screen-shot-2016-07-23-at-7-05-47-am.png 1221w, /wp-content/uploads/2017/06/screen-shot-2016-07-23-at-7-05-47-am-300x118.png 300w, /wp-content/uploads/2017/06/screen-shot-2016-07-23-at-7-05-47-am-768x301.png 768w, /wp-content/uploads/2017/06/screen-shot-2016-07-23-at-7-05-47-am-1024x402.png 1024w" sizes="(max-width: 349px) 100vw, 349px" /> <figcaption class="wp-caption-text">(nguồn: septeni-technology)</figcaption></figure>

Việc học máy của chúng ta cuối cùng có thể quy về việc tìm cho ra hàm h, bước suy đoán tìm ra hàm này dựa trên dữ liệu đầu vào, được gọi là bước huấn luyện dữ liệu (training data), và hàm h thu được, chính là mô hình dữ liệu (model). Cơ sở suy luận để tìm ra hàm h này cần nhiều kiến thức về toán học cao cấp: giải tích, đại số tuyến tính, xác suất thống kê,&#8230; Chi tiết cụ thể mình sẽ không trình bày lần này, vì nó rất rộng và trong bài viết này, các bạn cũng không cần dùng đến mức sâu như vậy. Quay trở lại với hàm h, vì đây là hàm suy diễn gần đúng, cho nên so với hàm mong muốn (là hàm f) sẽ có sai số nhất định, do đó sinh ra khái niệm confidence (độ tin tưởng) nhằm chỉ xác suất tiên đoán nó là kết quả đúng là bao nhiêu. Ngoài ra, ML còn bị ảnh hưởng bởi dữ liệu đầu vào, hiển nhiên nếu ta cho ít dữ liệu, thì việc suy đoán sẽ khó, hoặc suy đoán hàm h không chuẩn. Bên cạnh đó, trước khi đưa vào suy đoán, ML còn phải tách đầu vào thành các đặc trưng khác nhau (feature) để giảm thiểu khối lượng tính toán và tăng cường độ chính xác cho kết quả ( ví dụ như tách đặc trưng của con mèo so với con chó, con gà,&#8230;).

<span style="color:#ff0000;"><strong>&#8211;> Tổng kết: Bạn cần nhớ gì qua phần này ?</strong></span>

- Công việc của ML là tìm kiếm hàm H gần giống với hàm ánh xạ chuẩn giữa 2 tập đầu vào và đầu ra.
- Training data là bước sử dụng dữ liệu đầu vào để tìm hàm H.
- Model là hàm H thu được, và đó chính là kết quả của học máy.
- Confidence: xác suất chính xác của kết quả phán định bởi model.

&nbsp;

<h1 style="text-align:center;">
  <strong>Phần II: Làm quen với CoreML.</strong>
</h1>

Huấn luyện dữ liệu là một công đoạn không hề đơn giản, với chi phí tính toán và thời gian lớn, điều này phụ thuộc vào các bước toán học và số lượng cũng như độ phức tạp của tập đầu vào. Mình đã thử tự tay training 1 tập 20.000 bức ảnh (dạng bit) và công đoạn này ngốn ~ 30 phút. Tuy rằng hiện nay một số framework hỗ trợ việc training data ngay trên mobile, tiêu biểu nhất là TensorFlow (viết bằng Objective-C++ và C), nhưng cũng chỉ giải quyết một số bài toàn nhỏ.

&#8211;> Training data trên mobile là việc làm không khuyến khích và không đem lại nhiều ý nghĩa. Người dùng có thể sẵn lòng bỏ ra 1 khoảng thời gian không nhỏ chỉ để đợi cái ứng dụng của chúng ta training data không?

Trở về với công việc chính của chúng ta &#8211; những người lập trình viên iOS, vậy chúng ta kỳ vọng điều gì ở ML ? Đúng, chúng ta không huấn luyện dữ liệu, thay vào đó chúng ta ứng dụng kết quả của chúng, chính là Model (hay hàm H ở trên). Và tại WWDC2017, Apple đã giúp chúng ta điều này bằng việc cung cấp CoreML.

1. _**CoreML là gì (What is CoreML):**_

Trên [trang chủ](https://developer.apple.com/documentation/coreml) của mình, Apple chỉ viết ngắn gọn thế này:

> _Integrate machine learning models into your app._

CoreML giúp tích hợp model vào trong ứng dụng của bạn. Tích hợp như thế nào ? Hồi sau sẽ rõ.

CoreML còn hỗ trợ một số native framework khác của Apple, như là Vision (cho việc phân tích ảnh), Foundation (cho việc xử lý nhận dạng âm thanh và ngữ nghĩa),&#8230;

_**2. Sử dụng CoreML như thế nào: (how to use it)**_

Vì bản chất của CoreML là tích hợp model đã được huấn luyện vào trong ứng dụng

_<span style="color:#3366ff;">&#8211;> Bước đầu tiên: phải có Model. Vậy model này lấy ở đâu?</span>_

CoreML hiện tại chỉ nhận đúng một định dạng là .mlmodel, do đó, nếu chúng ta muốn sử dụng model bên ngoài, chúng ta cần phải convert nó sang định dạng này. Apple có hỗ trợ  sẵn [CoreMLTools](https://pypi.python.org/pypi/coremltools) để làm việc này. Trong phạm vi và mục tiêu của một bài làm quen, chúng ta sẽ không cần thao tác phức tạp đến vậy, chúng ta chỉ cần sử dụng những mlmodel có sẵn, do Apple chính Apple đưa ra, các bạn có thể tải chúng về [tại đây.](https://developer.apple.com/machine-learning/)

<img class="aligncenter size-full wp-image-1171" src="https://devislifeblog.files.wordpress.com/2017/06/screen-shot-2017-06-12-at-10-16-58-am.png?w=637" alt="Screen Shot 2017-06-12 at 10.16.58 AM.png" width="637" height="426" srcset="/wp-content/uploads/2017/06/screen-shot-2017-06-12-at-10-16-58-am.png 1059w, /wp-content/uploads/2017/06/screen-shot-2017-06-12-at-10-16-58-am-300x201.png 300w, /wp-content/uploads/2017/06/screen-shot-2017-06-12-at-10-16-58-am-768x514.png 768w, /wp-content/uploads/2017/06/screen-shot-2017-06-12-at-10-16-58-am-1024x686.png 1024w" sizes="(max-width: 637px) 100vw, 637px" />

Ở đây mình dùng model tên là VGG16.

_<span style="color:#3366ff;">&#8211;> Bước thứ 2: Tích hợp model vào trong project và xcode.</span>_

Đầu tiên, các bạn kéo thả file vừa download vào trong thư mục:

<img class="alignnone size-full wp-image-1176" src="https://devislifeblog.files.wordpress.com/2017/06/1.gif" alt="1.gif" width="836" height="512" />

Tiếp đến: các bạn kéo thả nó vào trong project tại xcode và lựa chọn target cho nó là project của bạn. Lưu ý bước này rất quan trọng, vì nếu bạn không lựa chọn target cho nó, thì đồng nghĩa nó không được add vào project và bundle lúc đóng gói của project, vì vậy bạn không thể dùng được nó.

<img class="  wp-image-1183 aligncenter" src="https://devislifeblog.files.wordpress.com/2017/06/2.gif" alt="2" width="249" height="459" />

<img class="  wp-image-1184 aligncenter" src="https://devislifeblog.files.wordpress.com/2017/06/3.gif" alt="3" width="230" height="423" />

Giờ thì hãy chọn file VGG16.mlmodel của các bạn trên XCode, và cùng tìm hiểu:

<img class="alignnone size-full wp-image-1194" src="https://devislifeblog.files.wordpress.com/2017/06/screen-shot-2017-06-12-at-10-38-15-am1.png" alt="Screen Shot 2017-06-12 at 10.38.15 AM.png" width="738" height="484" srcset="/wp-content/uploads/2017/06/screen-shot-2017-06-12-at-10-38-15-am1.png 738w, /wp-content/uploads/2017/06/screen-shot-2017-06-12-at-10-38-15-am1-300x197.png 300w" sizes="(max-width: 738px) 100vw, 738px" />

- Mục 1 là thông tin về mlmodel, không có gì quan trọng.
- Mục 2 là Model Class. Khi các bạn import file mlmodel vào Xcode, Xcode sẽ tự động sinh ra cho bạn cái Model Class này, đây chính sức mạnh then chốt của CoreML &#8211; từ model, bạn có class.
- Mục 3 là detail input và output, như trong hình: model của chúng ta nhận đầu vào là 1 ảnh có dạng Image,<BGR,224,224>, và output gồm 2 giá trị là classLabelProbs và classLabel.

Dưới đây là class mà Xcode sinh sẵn từ model cho chúng ta:

<img class="alignnone size-full wp-image-1232" src="https://devislifeblog.files.wordpress.com/2017/06/screen-shot-2017-06-12-at-1-42-00-pm.png" alt="Screen Shot 2017-06-12 at 1.42.00 PM.png" width="717" height="679" srcset="/wp-content/uploads/2017/06/screen-shot-2017-06-12-at-1-42-00-pm.png 717w, /wp-content/uploads/2017/06/screen-shot-2017-06-12-at-1-42-00-pm-300x284.png 300w" sizes="(max-width: 717px) 100vw, 717px" />

<img class="alignnone size-full wp-image-1233" src="https://devislifeblog.files.wordpress.com/2017/06/screen-shot-2017-06-12-at-1-42-29-pm.png" alt="Screen Shot 2017-06-12 at 1.42.29 PM.png" width="633" height="483" srcset="/wp-content/uploads/2017/06/screen-shot-2017-06-12-at-1-42-29-pm.png 633w, /wp-content/uploads/2017/06/screen-shot-2017-06-12-at-1-42-29-pm-300x229.png 300w" sizes="(max-width: 633px) 100vw, 633px" />

_**3. Ví dụ về sử dụng CoreML:**_

Ý tưởng bài toán: chọn ảnh trong Gallery &#8211;> dùng CoreML để tiên đoán xem ảnh đó mô tả cái gì?.

<span style="color:#3366ff;"><em>a) Thiết kế UI:</em></span>

<img class=" size-full wp-image-1205 aligncenter" src="https://devislifeblog.files.wordpress.com/2017/06/screen-shot-2017-06-12-at-1-16-56-pm.png" alt="Screen Shot 2017-06-12 at 1.16.56 PM.png" width="324" height="560" srcset="/wp-content/uploads/2017/06/screen-shot-2017-06-12-at-1-16-56-pm.png 324w, /wp-content/uploads/2017/06/screen-shot-2017-06-12-at-1-16-56-pm-174x300.png 174w" sizes="(max-width: 324px) 100vw, 324px" />

Mình có 1 cái ảnh, để thể hiện ảnh mình chọn, 1 cái label để thể hiện kết quả có được khi kiểm tra với ML, 1 nút &#8220;Add&#8221; để show màn hình chọn ảnh trong bộ sưu tập của máy. Đối với các bạn test trên simulator, các bạn nên kéo thêm ảnh bên ngoài vào trong, thay vì 4 ảnh mặc định.

<img class="aligncenter size-full wp-image-1213" src="https://devislifeblog.files.wordpress.com/2017/06/4.gif" alt="4.gif" width="502" height="320" />

<span style="color:#3366ff;"><em>b) Nào mình cùng code:</em></span>

Đầu tiên các bạn cần thực hiện phần việc click vào button để show lên màn hình chọn ảnh:

<img class="aligncenter size-full wp-image-1217" src="https://devislifeblog.files.wordpress.com/2017/06/screen-shot-2017-06-12-at-1-23-54-pm.png" alt="Screen Shot 2017-06-12 at 1.23.54 PM.png" width="512" height="251" srcset="/wp-content/uploads/2017/06/screen-shot-2017-06-12-at-1-23-54-pm.png 512w, /wp-content/uploads/2017/06/screen-shot-2017-06-12-at-1-23-54-pm-300x147.png 300w" sizes="(max-width: 512px) 100vw, 512px" />

Chú ý, vì model của chúng ta đã được Xcode chuyển thành class, cho nên chúng ta có thể sử dụng nó như một class bình thường, ví dụ tạo instance cho nó, ở đây mình gán cho nó vào 1 biến:

<img class=" size-full wp-image-1222 aligncenter" src="https://devislifeblog.files.wordpress.com/2017/06/screen-shot-2017-06-12-at-1-25-31-pm.png" alt="Screen Shot 2017-06-12 at 1.25.31 PM.png" width="250" height="50" />

Nhìn lại model của chúng ta, khi được convert theo XCode, đầu vào lúc này nhận vào 1 image có dạng PixelBuffer &#8211;> chúng ta cần phải convert ảnh cũng chúng ta sang dạng này. Mình tạo 1 class Utils để đảm nhận 2 việc resizeImage và convert nó sang PixelBuffer:

<img class="aligncenter size-full wp-image-1251" src="https://devislifeblog.files.wordpress.com/2017/06/screen-shot-2017-06-12-at-2-15-40-pm.png" alt="Screen Shot 2017-06-12 at 2.15.40 PM.png" width="1105" height="881" srcset="/wp-content/uploads/2017/06/screen-shot-2017-06-12-at-2-15-40-pm.png 1105w, /wp-content/uploads/2017/06/screen-shot-2017-06-12-at-2-15-40-pm-300x239.png 300w, /wp-content/uploads/2017/06/screen-shot-2017-06-12-at-2-15-40-pm-768x612.png 768w, /wp-content/uploads/2017/06/screen-shot-2017-06-12-at-2-15-40-pm-1024x816.png 1024w" sizes="(max-width: 1105px) 100vw, 1105px" />

Ok, chúng ta đã xong 90% công việc rồi, giờ quay lại với ViewController, phần việc còn lại của chúng ta chỉ là sử dụng model để tiên đoán ảnh chúng ta chọn:

<img class="aligncenter size-full wp-image-1255" src="https://devislifeblog.files.wordpress.com/2017/06/screen-shot-2017-06-12-at-2-17-15-pm.png" alt="Screen Shot 2017-06-12 at 2.17.15 PM.png" width="864" height="313" srcset="/wp-content/uploads/2017/06/screen-shot-2017-06-12-at-2-17-15-pm.png 864w, /wp-content/uploads/2017/06/screen-shot-2017-06-12-at-2-17-15-pm-300x109.png 300w, /wp-content/uploads/2017/06/screen-shot-2017-06-12-at-2-17-15-pm-768x278.png 768w" sizes="(max-width: 864px) 100vw, 864px" />

Lưu ý vì đầu vào của chúng ta là ảnh <BGR,224,224> (224 ở đây là width và height của ảnh) nên chúng ta phải resize về đúng width height này. Đến đây, chúng ta đã hoàn tất mọi công đoạn để có thể sử dụng 1 ảnh trong gallery làm đầu vào cho model, trong code là biến imgAsPixelBuffer.

_<span style="color:#3366ff;">Bước cuối cùng: CoreML sẽ giúp chúng ta phần việc tiên đoán còn lại, chỉ đơn giản bằng một câu lệnh: model.prediction():</span>_

<img class="aligncenter size-full wp-image-1264" src="https://devislifeblog.files.wordpress.com/2017/06/screen-shot-2017-06-12-at-2-21-14-pm.png" alt="Screen Shot 2017-06-12 at 2.21.14 PM.png" width="613" height="106" srcset="/wp-content/uploads/2017/06/screen-shot-2017-06-12-at-2-21-14-pm.png 613w, /wp-content/uploads/2017/06/screen-shot-2017-06-12-at-2-21-14-pm-300x52.png 300w" sizes="(max-width: 613px) 100vw, 613px" />

Đây là toàn bộ source code cho ViewController:

<img class=" size-full wp-image-1267 aligncenter" src="https://devislifeblog.files.wordpress.com/2017/06/screen-shot-2017-06-12-at-2-22-24-pm.png" alt="Screen Shot 2017-06-12 at 2.22.24 PM.png" width="878" height="932" srcset="/wp-content/uploads/2017/06/screen-shot-2017-06-12-at-2-22-24-pm.png 878w, /wp-content/uploads/2017/06/screen-shot-2017-06-12-at-2-22-24-pm-283x300.png 283w, /wp-content/uploads/2017/06/screen-shot-2017-06-12-at-2-22-24-pm-768x815.png 768w" sizes="(max-width: 878px) 100vw, 878px" />

&nbsp;

**<span style="color:#ff0000;">==> Test kết quả:</span>**

<img class="aligncenter size-full wp-image-1272" src="https://devislifeblog.files.wordpress.com/2017/06/5.gif" alt="5.gif" width="386" height="636" />

&nbsp;

- Nhét ảnh con sư tử &#8211;> ra lion, king of beasts,..
- Nhét ảnh con mèo &#8211;> ra egytian cat (mèo ai cập).
- Nhét ảnh con cún &#8211;> ra golden retriever (chú chó vàng).

&nbsp;

Các bạn có thể download Source Code [tại đây](https://github.com/starptit/CoreMLExample/tree/master/CoreMLExample/CoreMLExample).

=============================================================

<h1 style="text-align:center;">
  <strong>TỔNG KẾT</strong>
</h1>

Qua blog này, các bạn cần nhớ được gì:

a. Căn bản ML, nó là cái gì: nó là quan hệ toán học giữa đầu vào và đầu ra, quá trình học máy là quá trình tìm cho ra hàm liên hệ này với xác suất gần đúng tốt nhất.

b. CoreML là gì và làm gì? Nó là một framework được Apple giới thiệu nhằm tích hợp model vào trong ứng dụng của Apple.

c. Dùng nó thế nào: Cần một model , import vào để nó gen class và dùng thôi.
