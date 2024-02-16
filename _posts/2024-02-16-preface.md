---
layout: post
title: Vì sao và vì sao
subtitle: Khởi đầu cho một hành trình
gh-repo: daattali/beautiful-jekyll
gh-badge: [star, fork, follow]
tags: [test]
comments: true
author: Chí Trung HÀ
---

## Nguồn cơn
Hiện nay, đã có rất nhiều tài liệu, khóa học, cả tiếng Anh và tiếng Việt, cả đóng phí lẫn miễn phí, dạy về học máy, học sâu, từ lý thuyết đến ứng dụng. Không khó, chỉ một vài từ khóa tìm kiếm trên Google hay Bing, sẽ dẫn bạn đến một đại dương học liệu để bắt đầu tìm hiểu về học máy.
Một vài nguồn tài liệu tiếng Việt, hoặc được dịch, chuyển thể công phu sang tiếng Việt có thể kể ra ở đây như:
* [Machine learning cơ bản](https://machinelearningcoban.com/)
* [Deep Learning cơ bản](https://nttuan8.com/)
* [Đắm mình vào học sâu](https://d2l.aivivn.com/)
* [Học sâu](https://dlbookvn.gitlab.io/)
* [Khoa học dữ liệu - Khanh's blog](https://phamdinhkhanh.github.io/content)

Một số nguồn tiếng Anh tuyệt vời, rất dễ đọc và có đầy đủ ví dụ đi kèm:
* [Machine Learning Mastery](https://machinelearningmastery.com/)
* [omputer Vision, Deep Learning and OpenCV](https://pyimagesearch.com/)
* [Learn mathematics for data science and machine learning](https://hadrienj.github.io/)

Nếu bạn giỏi toán và/hoặc rất yêu thích toán, bạn nên đọc những tài liệu này (à, còn mình thì không):
* [Deep Learning. Ian Goodfellow and Yoshua Bengio and Aaron Courville](https://www.deeplearningbook.org/) là cuốn học sâu đã được dịch sang tiếng Việt ở trên
* [Deep Learning. Foundations and Concepts. Christopher M. Bishop with Hugh Bishop](https://www.bishopbook.com/?fbclid=IwAR0y0v_loLNRonRCR1o6oDKKfy5bVmjKS9ocPpMr7AiZKWE2bywqhuSCVtg)

Vấn đề khó khăn nhất với chúng ta là, trong một biển các phương pháp như vậy, thì phương pháp (mô hình) nào là phù hợp nhất cho tập dữ liệu? Điều quan trọng là phải đánh giá chính xác hiệu suất của một phương pháp, để biết nó hoạt động tốt hay kém như thế nào (các phương pháp đơn giản hơn thường hoạt động tốt như những phương pháp phức tạp hơn!) trên cùng một tập dữ liệu.

Vì thế, mục tiêu của tài liệu này là đi tìm hiểu từ những thứ đơn giản nhất, đến những thứ phức tạp hơn. Cố gắng nắm bắt và theo kịp hơi thở của đời sống hiện đại (prun - trong lĩnh vực học máy). Nhưng diễn đạt mọi thứ một cách sao cho đơn giản nhất, dễ hiểu nhất.
Nhưng điều này có vẻ mâu thuẫn.

Như vậy, trong khi cố gắng làm cho mọi thứ cô đọng, điều này có vẻ mâu thuẫn với việc làm cho các thứ dễ hiểu nhất.
Tiêu chí mà mình đặt ra là:
* Học sao cho thư giãn, vừa học vừa thư giãn!
* Mỗi một bài viết, có thể đọc trong 6 phút

Vì sao lại có con số như vậy, trước hết hẳn có một nghiên cứu nào đó về con số 6 (\emojismile- lộc!). Khi học tiếng Anh, tôi rất thích nghe chương trình [6 Minutes English](https://www.bbc.co.uk/learningenglish/english/features/6-minute-english). 6 phút là khoảng thời gian vừa đủ để ta có thể theo dõi liền mạch, không đứt mạch tư duy, không bị mệt mỏi hay phải ngắt nghỉ nhiều lần. Quả thật tôi cũng không hiểu tại sao các bạn có sức chịu đựng ngồi một mạch hàng tiếng đồng hồ để ngồi nghe giảng ở trên giảng đường (*chỉ là đùa chút thôi, vì tôi biết các bạn có khả năng đó!*).

Tuy nhiên, tùy vào khả năng và cách tiếp cận của bạn, bạn có thể mở rộng 6 phút đó ra, bổ sung 6 phút cho việc nghiền ngẫm lại một vấn đề chưa thỏa đáng, 6 phút để xem thêm kiến thức ở một đường dẫn phía cuối chương, 6 phút để tìm kiếm giải pháp ở trên một nền tảng khác như `Tensorflow`, hay nhờ [ChatGPT](https://chat.openai.com/auth/login) hay [Copilot](https://copilot.microsoft.com/) chỉ ra các phương án lập trình khác.

Mỗi tác giả khác nhau lại sử dụng một hệ thống ký hiệu toán học khác nhau. Vì vậy, chúng ta chỉ nên tập trung vào ý nghĩa, cách vận hành của phương pháp, và các cài đặt, triển khai chúng trên thực tế, thay vì sa đà vào những tầng lớp hay nguồn cơn sâu xa về mặt toán học. Nói một cách khác, cố gắng giản đơn một cách hết mức có thể các vấn đề về toán (những thứ đã được các nhà toán học chứng minh) mà chỉ cần hiểu ý nghĩa và cách vận dụng chúng.

Tôi đã xem qua nhiều tài liệu dạy về học máy, học sâu, cũng tham khảo một số khóa học online. Tuy nhiên có lẽ do mất gốc về kiến thức toán học, lại chưa đủ sử kiên trì, và tính cả thèm nhưng chóng chán, nên không tài liệu nào tôi theo dõi đủ đầu đuôi, mãi vẫn không nhập tâm được điều gì. Cho đến năm 2022. Tôi gặp cuốn sách [Deep learning with Pytorch Step-by-step. A Beginner’s Guide](https://leanpub.com/pytorch) tạm dịch là Học sâu với Pytorch, từng bước cho người mới bắt đầu, của tác giả [Daniel Voigt Godoy](https://www.linkedin.com/in/dvgodoy/). Tôi đã đọc nó một mạch từ đầu đến cuối với niềm hứng thú. Trong đầu chợt liên hệ với những khó khăn mà một số bạn mới bắt đầu vào lĩnh vực học máy, học sâu đang gặp phải.

 Vì vậy, tôi bắt đầu viết loạt bài này với phần lớn nội dung tuân thủ theo cuốn sách trên, lược bớt hoặc bổ sung một số phần mà theo quan điểm của cá nhân tôi là cần thiết. Tuy nhiên không giới hạn ở đó, có rất nhiều nguồn tài liệu và ví dụ tham khảo khác được thêm vào, như tài liệu [An Introduction to Statistical Learning](https://www.statlearning.com/) chẳng hạn và vô số nguồn tài liệu khác nữa mà bạn sẽ gặp trong các phần tiếp theo. Hy vọng, Loạt bài viết này sẽ phần nào đó giúp đỡ chính tôi và các bạn, hệ thống hóa lại kiến thức, một các cơ bản nhất, về học máy và học sâu, theo đúng phong cách của những người chập chững mới tập đi, từng bước từng bước một.

Nội dung mỗi phần sẽ cố gắng thể hiện ngắn gọn, tăng dần từ dễ đến khó, từ các kiến thức cổ điển đến những thứ hiện đại nhất, với tinh thần "ít thôi nhưng dài lâu" 😊.

Theo Daniel Voigt Godoy, việc tập trung vào những điều cơ bản: cuốn sách này có thể sẽ có thời hạn sử dụng lâu hơn. Việc sách kỹ thuật, đặc biệt là những cuốn tập trung vào công nghệ tiên tiến, nhanh chóng trở nên lỗi thời là điều khá phổ biến. Hy vọng rằng điều này sẽ không xảy ra ở đây vì các cơ chế cơ bản không thay đổi và các khái niệm cũng vậy. Dù cú pháp lập trình sẽ thay đổi theo thời gian.

Bạn có thể đọc trực tiếp cuốn sách của tác giả để có thêm một số thông tin khác. Sẽ có sự khác nhau đôi chút. Tài liệu này mặc dù trên tinh thần là tuân thủ theo nội dung cuốn sách trên, tuy nhiên cũng có phần chỉ lược dịch, có phần thì bổ sung những nội dung khác theo cách hiểu của cá nhân tôi.

Ai sẽ đọc tài liệu này? Nếu bạn lướt tới đây, có nghĩa chính bạn có thể là người sẽ cần đến, sẽ theo dõi tài liệu này. Và nếu bạn quan tâm đến học máy, học sâu, ngôn ngữ lập trình Python và các nền tảng như Pytorch, thì hy vọng đây có thể là một điểm khởi đầu tốt cho bạn.

Nếu bạn đang tìm một cuốn sách mà bạn có thể tìm hiểu về deep learning và PyTorch mà không cần phải mất hàng giờ để giải mã văn bản và các  đoạn mã khó hiểu, với hàng đống ký hiệu, công thức toán học rắc rối, đồng thời là một cuốn sách dễ đọc và thú vị, lại còn viết bằng tiếng Việt yêu dấu của chúng ta, thì đây chính là nó 😊

Lẽ dĩ nhiên, nếu bạn cần bổ sung hay trích dẫn vào luận văn, luận án, thì bạn sẽ cần đến những tài liệu học thuật cao siêu kia.

Và thật là tuyện vời nếu bạn đã trang bị cho mình một số kiến thức sau (nếu không bạn sẽ cần thêm nhiều lần 6 phút cho mỗi một phần của cuốn sách):
* một chút về lập trình Python, các hàm, các khái niệm, hoặc bạn có thể bắt đầu tại [Python Tutorial](https://docs.python.org/3/tutorial/)
* đã làm việc qua với PyData stack: [numpy](https://numpy.org/) cho xử lý số, ma trận, [matplotlib](https://matplotlib.org/) cho trực quan hóa dữ liệu, [pandas](https://pandas.pydata.org/) cho xử lý dữ liệu dạng bảng.
* đã làm việc với [Jupyter](https://jupyter.org/install) trên máy tính cá nhân, hoặc [JupyterHub](https://jupyter.org/hub) và/hoặc [Google Colab](https://colab.research.google.com/), [Binder](https://mybinder.org/)
* biết cài đặt [Anaconda](https://www.anaconda.com/) hoặc `miniconda`, và các thư viện cần thiết trên máy tính cá nhân;
 * đã biết một số khái niệm cơ bản trong học máy (ML), học sâu (DL) như học có giám sát, hàm mất mát, underfitting và overfitting, v.v.

## Tại sao là Pytorch?
Tất nhiên rồi, để nắm bắt học sâu, đồng nghĩa bạn phải học một trong các nền tảng như `Tensorflow` và/hoặc `Pytorch`. Mã `Pytorch` thì có vẻ python hơn, hoặc đơn giản chỉ vì cuốn sách gốc tác giả trình bày các ví dụ bằng `Pytorch`. Hoặc lý do khác, ai biết được, nhưng bản thân tôi cũng thích `Pytorch` hơn và một lý do nữa là không hiểu biết lắm về `Tensorflow` và các nền tảng khác. Cũng không sao, nếu bạn không thích Pytorch thì bạn đã không đọc đến đây và có thể thử hỏi Copilot hoặc GPT với câu hỏi: "đoạn mã ... với Tensorflow sẽ như thế nào". 

> [!TIP]
> "*Tôi đã sử dụng PyTorch được vài tháng và tôi chưa bao giờ cảm thấy tốt hơn. Tôi có nhiều năng lượng hơn. Da tôi sáng hơn. Thị lực của tôi đã được cải thiện*". [Andrej Karpathy](https://karpathy.ai/) - AI Director at Tesla, một nhân vật nổi tiếng trong lĩnh vực AI, đã mô tả như vậy trên [X](https://twitter.com/karpathy/status/868178954032513024).

Pytorch cũng được nhìn nhận như một Framework về học máy [phát triển nhanh nhất](https://www.businessinsider.com/pytorch-facebook-tesla-uber-genentech-stanford-berkeley-2019-8) và có [hệ sinh thái](https://pytorch.org/ecosystem/) và cộng đồng lớn. Rất nhiều công cụ và thư viện được xây dựng trên Pytorch. Nó là [Framework ưa thích](https://thegradient.pub/state-of-ml-frameworks-2019-pytorch-dominates-research-tensorflow-dominates-industry/) cả cho nghiên cứu và xây dựng các ứng dụng thực tiễn.

Một số công ty phát triển hệ sinh thái học máy của mình dựa trên Pytorch gồm: Facebook [Meta](https://ai.meta.com/research/), nhà phát triển chính của Pytorch, [Tesla](https://www.youtube.com/watch?v=oBklltKXtDE), [OpenAI](https://openai.com/blog/openai-pytorch) (OpenAI đến giờ phút này thì quá nổi tiếng rồi phải không nào, tài liệu tiếng Việt này được biên soạn nhờ sự hỗ trợ của ChatGPT, Microsoft Copilot), [fastai](https://www.fast.ai/), Uber (phát triển các thư viện như [Pyro](http://pyro.ai/), [Horovod](https://github.com/horovod/horovod),  và cả [Airbnb](https://hub.packtpub.com/microsoft-airbnb-genentech-toyota-pytorch-to-build-deploy-production-ready-ai/) nữa.

Không chỉ là Pytorch, tinh thần của tác giả gốc và tài liệu tiếng Việt này là giúp chúng ta bắt đầu với PyTorch, đồng thời cung cấp cho bạn sự hiểu biết vững chắc về cách thức hoạt động của nó, cũng như tăng cường khả năng lập trình Python, xây dựng kiến thức về học máy từ những điều cơ bản nhất.

Nội dung các bài viết sau đây chia làm 4 phần chính:

**Phần I. Cơ bản về học sâu**

Tìm hiểu các kiến thức cơ bản nhất để bắt đầu với học máy, học sâu với Pytorch. 

**Phần II. Thị giác máy tính**

Một chút bắt đầu với dạng dữ liệu hình ảnh, làm quen với một số mô hình học sâu sử dụng trong xử lý hình ảnh.

**Phần III. Chuỗi**

Tìm hiểu các mô hình học sâu chủ yếu sử dụng cho xử lý dữ liệu dạng chuỗi, như các văn bản (RNN, GRU, LSTM, s2s models, cơ chế chú ý, tự chú ý, Transformers)

**Phần IV. Xử lý ngôn ngữ tự nhiên**

Bàn luận về xử lý dữ liệu dạng chuỗi, nhưng đặc biệt hơn, nó là ngôn ngữ tự nhiên của chúng ta (tách từ, nhúng từ, nhúng từ theo ngữ cảnh, ELMo, BERT, GPT-2)


**Phần V. Trí tuệ nhân tạo tạo sinh**

Từ năm 2023, trí tuệ nhân tạo tạo sinh đã bắt đầu làm mưa làm gió trên toàn thế giới, chúng ta sẽ giữ mình không quá tụt hậu so với thế giới trong phần này.


**Một vài lưu ý để bạn dễ theo dõi những bài viết này**
Các ví dụ về một đoạn mã:

~~~
def foo(x):
  return (x + 5)

foo(3)
~~~

Ví dụ về mã lệnh được highlighting:

```python có
def foo(x):
  return (x + 5)

foo(3)
```

Một ví dụ khác về code với các dòng lệnh được đánh số

{% highlight python linenos %}
def foo(x):
  return (x + 5)

foo(3)
{% endhighlight %}

## Boxes
Bạn có thể gặp những đoạn văn bản được để trong hộp hay có dấu hiệu gây chú ý như những ví dụ này:

### Notification

{: .box-note}
**Note:** Nhưng thông tin bổ ích mà bạn nên đọc.

> [!NOTE]
> Nhưng thông tin bổ ích mà bạn nên đọc.

> [!TIP]
> Những lời khuyên mà bạn có thể áp dụng cho cuộc sống dễ dàng hơn.
 
### Warning

{: .box-warning}
**Warning:** Cảnh báo về những điều không nên làm

> [!WARNING]
> Những điều quan trọng mà bạn nên biết và tuân thủ

> [!CAUTION]
> Những cảnh báo quan trọng về những không nên làm

### Error

{: .box-error}
**Error:** Những cảnh báo về lỗi chúng ta hay mắc phải

> [!IMPORTANT]
> Những thông tin quan trọng nên biết.


> [!NOTE]
> Các nguồn trích dẫn tham khảo, thay vì để đánh thứ tự như các tài liệu khoa học, sách, báo khoa học thường có, trong tài liệu này chúng được để ở phần Đọc thêm cuối mỗi chương và có đường dẫn trực tiếp đến tài liệu nguồn cho bạn đỡ mất công tìm kiếm, thay vì phải mất thời gian tra cứu dài lê thê (khá mất thời gian của bạn đấy!).
