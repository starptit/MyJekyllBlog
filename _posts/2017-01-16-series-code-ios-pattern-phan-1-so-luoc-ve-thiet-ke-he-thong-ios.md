---
id: 520
title: "Series code iOS pattern: Phần 1: Sơ lược về thiết kế hệ thống iOS"
date: 2017-01-16T10:37:01+00:00
author: starptit
# layout: post
guid: https://devislifeblog.wordpress.com/?p=520
permalink: /2017/01/series-code-ios-pattern-phan-1-so-luoc-ve-thiet-ke-he-thong-ios/
tags: [Uncategorized, Swift]
---

Bài viết này là bài mở đầu cho series về iOS Pattern, series này sẽ bao quát một số vấn đề về kiến trúc (architecture), thiết kế source code (design pattern) nhằm cải thiện chất lượng code và tư duy hệ thống của các bạn.

Nếu các bạn là junior developers mà tiến đến xa hơn Senior hoặc team lead, thì các bạn bắt buộc phải tìm hiểu những vấn đề mà mình nêu ra.

Mình đọc một số topic trên mạng về series này rồi, họ viết khá hay và dễ hiểu, tuy nhiên chưa có case nào cụ thể cho lập trình iOS, hoặc các ví dụ họ đưa ra khá đơn giản, nhưng lại viết bằng ngôn ngữ abc nào đó, khiến cho các bạn newbie khá khó khăn trong việc vận hành cũng như áp dụng vào source iOS của mình. Cuối cùng mình đưa ra quyết định thực hiện lại nó theo phong cách iOS (Swift), một phần cũng để tự củng cố thêm kiến thức, cộng thêm hi vọng chỉ giáo từ các bạn khá hơn, vì phần này mình hoàn toàn tự đọc hiểu, không có thầy thợ hướng dẫn, sai sót hoặc nhầm lẫn là điều bình thường, mong được góp ý để hoàn thiện hơn.

\*\*\* Chú ý: từ hệ thống mình dùng trong bài có ý nghĩa là source code, template, pattern, &#8230;

<!--more-->

1. Tại sao tôi lại cần phải biết về thiết kế hệ thống ?

Bạn hãy coi việc hoàn thành một sản phẩm phần mềm như xây một cái nhà chẳng hạn, việc bạn viết code cũng giống như mấy ông thợ xây đóng gạch chát vữa vậy. Ông kiến trúc sư phải phác thảo ra hình dáng cái nhà trước, rồi ông thợ cả mới bắt đầu thêm thêm bớt bớt, đóng khuôn đóng mẫu để bạn bắt tay vào xây theo, đắp theo. Cái mà mình đang nói đến chính là cái bản vẽ thiết kế của ông kiến trúc sư và khuôn mẫu của ông thợ cả đã làm đó. Hãy thử tưởng tượng, bạn xây nhà mà không có bản vẽ, cứ vừa xây vừa nghĩ xem xây đắp thế nào  cho thành hình cái nhà, thì chắc lúc xây xong, nó lại ra dáng cái lều mất. Trong coding nó cũng vậy, bạn cứ cắm đầu vào code mà không nghĩ đến thiết kế của nó trước, thì sau này maintain, chính bạn sẽ là người lãnh đủ.

Hơn nữa, một source code được thiết kế tốt, có thể giúp bạn tiết kiệm được rất nhiều thời gian và công sức trong việc fix bug và maintain, cũng như phát triển thêm các module, function mới. Ngoài ra, hiểu biết về thiết kế của các template này sẽ giúp bạn đọc hiểu code người khác dễ hơn, code ít bốc mùi (smell code) hơn.

2. Một số nguyên tắc khi thiết kế hệ thống?

Khi bắt tay vào thiết kế module hay function nào đó, bạn cần cân nhắc xem nó đã đáp ứng được một số yêu cầu dưới đây chưa? Thực chất design pattern hay architecture hay template gì đó cũng chỉ là giải pháp đưa ra để nhằm đảm bảo code và hệ thống của bạn đáp ứng được các tiêu chí đó. Chính vì vậy mà không phải lúc nào áp dụng pattern vào cũng là tốt, bạn cần phải xem xét và đánh giá cẩn thận, lập trình viên giỏi hay không chính là ở bước này: biết áp dụng cái gì và không áp dụng cái gì. Nếu không thì dự án của bạn sẽ như thế này:

<img class=" size-full wp-image-575 aligncenter" src="https://devislifeblog.files.wordpress.com/2017/01/1.jpg" alt="1" width="459" height="330" srcset="/wp-content/uploads/2017/01/1.jpg 459w, /wp-content/uploads/2017/01/1-300x216.jpg 300w" sizes="(max-width: 459px) 100vw, 459px" />

Dài dòng đủ rồi, các nguyên tắc đó đây:

- Clear and Ease of use (rõ ràng và dễ sử dụng): mọi thiết kế đều thể hiện tư duy của bạn, bạn làm nó dễ dàng và dễ dùng thì người khác có thể dễ hiểu và nắm bắt hơn, chưa kể sau này bạn còn phải đọc lại chính nó để maintain. Đừng để tình trạng: &#8220;Khi tôi viết đoạn code này, chỉ có tôi và Chúa hiểu. Giờ ngồi đọc lại, chỉ có Chúa mới hiểu&#8221;, thằng cha maintainer nó sẽ vừa code vừa chửi bạn đấy, lúc đó tha hồ mà hắt xì hơi.
- Reusability (tính tái sử dụng): đơn giản thôi, function bạn đang thiết kế có thể sẽ được sử dụng lại ở đâu đó, bởi bạn hoặc partner trong team hoặc maintainer,&#8230; chính ví vậy bạn viết chúng theo hướng tái sử dụng, thì tương lai bạn chỉ cần gọi ra để dùng lại, đỡ mất thời gian viết lại + test lại. Ví dụ: module gửi nhận request Server, chắc chắn được dùng rất nhiều &#8211;> bạn chỉ cần viết chúng ở một nơi, các lần sau bạn không cần phải viết lại code như thế nữa, cứ gọi chạy là được, rất tiện lợi phải không ?
- Decoupling (tính phân rã): một trong những nguyên nhân khiến code của bạn smell và khó maintain đó chính là chúng kết dính với nhau, tức là một function A lại liên quan đến function B, C, D,&#8230; Điều này rất nguy hiểm vì khi một trong các function trên thay đổi &#8211;> function A của bạn có thể chạy sai và ngược lại, mặt khác, bạn phải test lại toàn bộ các function liên quan đến nó nữa, có khi nó còn liên quan đến phần code của người khác, lại phải ngồi mày mò rất mất thời gian và công sức. Kinh nghiệm của mình thì mình hay tách nó ra thành các service khác nhau, hoặc tạo một class Manager để dễ control.
- Testability (dễ test): bạn viết code càng dễ test bao nhiêu, thì bạn càng ít nguy cơ bị báo bug bấy nhiêu, hơn nữa còn giảm thiểu thời gian cho pha Testing. Thường thường  thì bạn nên tổ chức unit test ngay tại chỗ, XCode có cung cấp công cụ để bạn thực hiện unit test.
- Modifying and Extending (chỉnh sửa và mở rộng): Một thiết kế tốt là thiết kế có thể giúp hạn chế việc chỉnh sửa các function cũ và có thể mở rộng thêm nhiều function mới bên cạnh function cũ. Các function cũ có thể đã được release hoặc code của người khác, sẽ thật là nguy hiểm nếu bạn có quyền chỉnh sửa code người khác, vì bạn không biết nó liên quan đến đâu, chẳng may sửa 1 cái mà sập cả hệ thống thì quỳ, nếu bạn muốn sửa hay bổ sung, hãy viết một function mới bên cạnh function cũ và sử dụng chúng cho công việc của bạn.

Trên đây mình đã liệt kê một số nguyên tắc cần phải nhớ khi thiết kế code cho dự án của bạn, mình đã thử áp dụng và cũng đã trải nghiệm tính hiệu quả của nó qua một số dự án rồi. Phần 1 này mình chỉ viết sơ lược và tổng quan, chưa đến phần cụ thể nên nó vẫn còn khá là dễ nhai. Trong phần tiếp theo mình sẽ viết về nguyên lý S.O.L.I.D, hay còn gọi là luật Uncle Bob (Uncle Bob rules).


{% include disqus_comments.html %}