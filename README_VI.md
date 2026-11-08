<p align="center">
<h1 align="center">《动手学大模型》 - Loạt bài thực hành lập trình Học Mô hình Lớn qua Thực hành</h1>
</p>
<p align="center">
  	<a href="https://img.shields.io/badge/version-v0.1.0-blue">
      <img alt="version" src="https://img.shields.io/badge/version-v0.1.0-blue?color=FF8000?color=009922" />
    </a>
  <a >
       <img alt="Status-building" src="https://img.shields.io/badge/Status-building-blue" />
  	</a>
  <a >
       <img alt="PRs-Welcome" src="https://img.shields.io/badge/PRs-Welcome-red" />
  	</a>
   	<a href="https://github.com/Lordog/dive-into-llms/stargazers">
       <img alt="stars" src="https://img.shields.io/github/stars/Lordog/dive-into-llms" />
  	</a>
  	<a href="https://github.com/Lordog/dive-into-llms/network/members">
       <img alt="FORK" src="https://img.shields.io/github/forks/Lordog/dive-into-llms?color=FF8000" />
  	</a>
    <a href="https://github.com/Lordog/dive-into-llms/issues">
      <img alt="Issues" src="https://img.shields.io/github/issues/Lordog/dive-into-llms?color=0088ff"/>
    </a>
    <br />
</p>


<div align="center">
<p align="center">
  <a href="#-động-lực-dự-án">Động lực dự án</a>/
  <a href="#-mục-lục-bài-giảng">Mục lục bài giảng</a>/
  <a href="#-danh-sách-người-đóng-góp">Danh sách người đóng góp</a>
</p>
</div>

> Đây là bản dịch tiếng Việt của [`README.md`](README.md). Nếu có sai sót, vui lòng tham khảo bản gốc.

## 💡 Cập nhật

2025/06/06 Cảm ơn sự quan tâm và phản hồi tích cực của mọi người! Chúng tôi đã cập nhật hướng dẫn này trên hai phương diện sau:

- [x] Ra mắt hướng dẫn cộng đồng 《Quy trình phát triển toàn diện mô hình lớn》 phiên bản nội địa hóa (bao gồm PPT, sổ tay thực hành và video), xin đặc biệt cảm ơn sự hỗ trợ của cộng đồng Huawei Ascend!
- [x] Cập nhật nội dung dựa trên loạt hướng dẫn thực hành lập trình ban đầu, đồng thời bổ sung các chủ đề mới (suy luận toán học, GUI Agent, căn chỉnh mô hình lớn, giấu tin, v.v.)!

## 🎯 Động lực dự án

Loạt hướng dẫn thực hành lập trình 《动手学大模型》 (Học Mô hình Lớn qua Thực hành) được phát triển từ bài giảng các khóa 《Công nghệ tiên tiến xử lý ngôn ngữ tự nhiên》 (NIS8021) và 《Công nghệ an toàn trí tuệ nhân tạo》 (NIS3353) của Đại học Giao thông Thượng Hải (giảng viên: [张倬胜](https://bcmi.sjtu.edu.cn/home/zhangzs/)), nhằm cung cấp tài liệu tham khảo lập trình nhập môn liên quan đến mô hình lớn. Hướng dẫn này mang tính chất cộng đồng, hoàn toàn miễn phí. Thông qua những bài thực hành đơn giản, chúng tôi giúp các bạn sinh viên nhanh chóng nhập môn mô hình lớn, thuận lợi hơn trong việc thực hiện đồ án môn học hoặc nghiên cứu học thuật.

## 📚 Mục lục bài giảng

| Nội dung bài giảng | Giới thiệu | Địa chỉ |
| ---------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Tinh chỉnh và Triển khai | Hướng dẫn tinh chỉnh và triển khai mô hình tiền huấn luyện: Bạn muốn nâng cao hiệu suất của mô hình tiền huấn luyện trên một tác vụ cụ thể? Hãy cùng chọn mô hình tiền huấn luyện phù hợp, tinh chỉnh trên tác vụ cụ thể và triển khai mô hình đã tinh chỉnh thành một Demo dễ sử dụng! | [[Bài giảng](https://github.com/Lordog/dive-into-llms/tree/main/documents/chapter1/dive-into-llm.pdf)] [[Hướng dẫn](https://github.com/Lordog/dive-into-llms/tree/main/documents/chapter1/README.md)] [[Script](https://github.com/Lordog/dive-into-llms/tree/main/documents/chapter1/dive-tuning.ipynb)] |
| Học qua gợi ý và Chuỗi suy luận | Hướng dẫn gọi API và suy luận với mô hình lớn: "AI cần lời động viên trực tuyến? Câu trả lời của mô hình lớn cho một số câu hỏi khiến người ta bất ngờ, nhưng có thể nó chỉ muốn một câu『động viên』" | [[Bài giảng](https://github.com/Lordog/dive-into-llms/tree/main/documents/chapter2/dive-into-prompting.pdf)] [[Hướng dẫn](https://github.com/Lordog/dive-into-llms/tree/main/documents/chapter2/README.md)] [[Script](https://github.com/Lordog/dive-into-llms/tree/main/documents/chapter2/dive-prompting.ipynb)] |
| Chỉnh sửa tri thức | Phương pháp và công cụ chỉnh sửa tri thức của mô hình ngôn ngữ: Bạn muốn thao tác ký ức của mô hình ngôn ngữ về một tri thức được chỉ định? Hãy cùng chọn phương pháp chỉnh sửa phù hợp, chỉnh sửa tri thức cụ thể và kiểm chứng mô hình sau khi chỉnh sửa! | [[Bài giảng](https://github.com/Lordog/dive-into-llms/blob/main/documents/chapter3/dive_edit_0410.pdf)] [[Hướng dẫn](https://github.com/Lordog/dive-into-llms/tree/main/documents/chapter3/README.md)]  [[Script](https://github.com/Lordog/dive-into-llms/tree/main/documents/chapter3/dive_edit.ipynb)] |
| Suy luận toán học | Làm thế nào để mô hình lớn học được suy luận toán học? Hãy cùng nhanh chóng chưng cất một mini R1! | [[Bài giảng](https://github.com/Lordog/dive-into-llms/blob/main/documents/chapter4/math.pdf)] [[Hướng dẫn](https://github.com/Lordog/dive-into-llms/tree/main/documents/chapter4/README.md)]  [[Script](https://github.com/Lordog/dive-into-llms/tree/main/documents/chapter4/sft_math.ipynb)] |
| Thủy vân mô hình | Thủy vân văn bản của mô hình ngôn ngữ: nhúng thủy vân mà mắt người không nhìn thấy vào nội dung do mô hình ngôn ngữ sinh ra | [[Bài giảng](https://github.com/Lordog/dive-into-llms/blob/main/documents/chapter5/watermark.pdf)] [[Hướng dẫn](https://github.com/Lordog/dive-into-llms/tree/main/documents/chapter5/README.md)]  [[Script](https://github.com/Lordog/dive-into-llms/tree/main/documents/chapter5/watermark.ipynb)] |
| Tấn công Jailbreak | Muốn có bảo mật tốt hơn thì phải bắt đầu từ việc học cách tấn công. Hãy cùng tìm hiểu cách tấn công jailbreak bẻ khóa mô hình lớn! | [[Bài giảng](https://github.com/Lordog/dive-into-llms/blob/main/documents/chapter6/dive-Jailbreak.pdf)] [[Hướng dẫn](https://github.com/Lordog/dive-into-llms/tree/main/documents/chapter6/README.md)] [[Script](https://github.com/Lordog/dive-into-llms/tree/main/documents/chapter6/dive-jailbreak.ipynb)] |
| Giấu tin trong mô hình lớn | "Mực vô hình"! Muốn mô hình lớn vừa trả lời trôi chảy vừa lén mang theo thông tin mà chỉ "người trong nhà" mới nhận ra? Giấu tin trong mô hình lớn sẽ cho bạn câu trả lời! | [[Bài giảng](https://github.com/Lordog/dive-into-llms/blob/main/documents/chapter7/stega.pdf)] [[Hướng dẫn](https://github.com/Lordog/dive-into-llms/tree/main/documents/chapter7/README.md)] [[Script](https://github.com/Lordog/dive-into-llms/tree/main/documents/chapter7/llm_stega.ipynb)] |
| Mô hình đa phương thức | Là mô hình ngôn ngữ lớn đa phương thức có khả năng mô phỏng thế giới thực đầy đủ hơn, làm thế nào để đạt được khả năng hiểu và sinh đa phương thức mạnh mẽ hơn? Liệu mô hình ngôn ngữ lớn đa phương thức có thể giúp hiện thực hóa AGI? | [[Bài giảng](https://github.com/Lordog/dive-into-llms/blob/main/documents/chapter8/mllms.pdf)]  [[Hướng dẫn](https://github.com/Lordog/dive-into-llms/tree/main/documents/chapter8/README.md)] [[Script](https://github.com/Lordog/dive-into-llms/tree/main/documents/chapter8/mllms.ipynb)] |
| Tác tử GUI | Muốn được phục vụ tận nơi, rảnh tay? Vậy hãy cùng để AI Agent giúp bạn gọi đồ ăn, trả lời tin nhắn, mua sắm so giá! | [[Bài giảng](https://github.com/Lordog/dive-into-llms/blob/main/documents/chapter9/GUIagent.pdf)]  [[Hướng dẫn](https://github.com/Lordog/dive-into-llms/tree/main/documents/chapter9/README.md)] [[Script](https://github.com/Lordog/dive-into-llms/tree/main/documents/chapter9/GUIagent.ipynb)] |
| An toàn tác tử | Tác tử mô hình lớn đang tiến tới hành trình trở thành hệ điều hành của tương lai. Tuy nhiên, liệu mô hình lớn có nhận thức được các mối đe dọa rủi ro trong bối cảnh tác tử mở? | [[Bài giảng](https://github.com/Lordog/dive-into-llms/blob/main/documents/chapter10/dive-into-safety.pdf)] [[Hướng dẫn](https://github.com/Lordog/dive-into-llms/tree/main/documents/chapter10/README.md)] [[Script](https://github.com/Lordog/dive-into-llms/tree/main/documents/chapter10/agent.ipynb)] |
| Căn chỉnh an toàn RLHF | Hướng dẫn thí nghiệm RLHF dựa trên PPO: Hướng dẫn này "rất nguy hiểm", sau khi đọc hãy kiểm tra xem mô hình lớn của bạn có đang cười lạnh không. | [[Bài giảng](https://github.com/Lordog/dive-into-llms/blob/main/documents/chapter11/RLHF.pdf)] [[Hướng dẫn](https://github.com/Lordog/dive-into-llms/tree/main/documents/chapter11/README.md)] [[Script](https://github.com/Lordog/dive-into-llms/tree/main/documents/chapter11/RLHF.ipynb)] |



## 🔥 Mới ra mắt: 《Quy trình phát triển toàn diện mô hình lớn》 phiên bản nội địa hóa

- **✨ Hướng dẫn cộng đồng 《Quy trình phát triển toàn diện mô hình lớn》 do chúng tôi kết hợp với Huawei Ascend ra mắt chính thức! Công nghệ tiên tiến kết hợp thực hành mã nguồn, cầm tay chỉ việc đưa bạn làm chủ AI mô hình lớn ✨**:

  Trên cơ sở loạt hướng dẫn 《动手学大模型》 ban đầu, chúng tôi đã phối hợp với Huawei phát triển loạt khóa học 《Quy trình phát triển toàn diện mô hình lớn》. Loạt hướng dẫn này được phát triển dựa trên phần cứng và phần mềm nền tảng Ascend, bao gồm PPT, sổ tay thực hành, video và nhiều hình thức khác. Hướng dẫn được chia thành các cấp độ sơ cấp, trung cấp và cao cấp, hướng tới những nhu cầu thực hành mô hình lớn khác nhau, nhằm đưa công nghệ tiên tiến thông qua thực hành mã nguồn, cung cấp cho các nhà nghiên cứu, nhà phát triển hướng dẫn phát triển toàn diện từ cơ bản đến nâng cao để nhanh chóng làm quen, ứng dụng các mô hình Ascend đã hỗ trợ và chuyển đổi, tinh chỉnh mô hình mới.

- **🚀 Truy cập cộng đồng Ascend để khám phá loạt khóa học 《Quy trình phát triển toàn diện mô hình lớn》**:

  👉《[Khu vực học phát triển mô hình lớn](https://www.hiascend.com/edu/growth/lm-development#classification-floor-1)》@ Cộng đồng Ascend 👈

- **✨ Nội dung khóa học ✨**

  <!-- <img src="./pics/icon/title.jpg" width="300"/>
  <img src="./pics/icon/cover.png" width="300"/>
  <img src="./pics/icon/team.png" width="300"/>
  <img src="./pics/icon/agent.png" width="300"/> -->

<p align = "center">
  <img src="./pics/icon/title.jpg" width="48%"/>
  <img src="./pics/icon/cover.png" width="48%"/>
  <img src="./pics/icon/team.png" width="48%"/>
  <img src="./pics/icon/agent.png" width="48%"/>
</p>

## 🙏 Tuyên bố miễn trừ trách nhiệm

Toàn bộ nội dung của hướng dẫn này chỉ đến từ kinh nghiệm cá nhân của những người đóng góp, dữ liệu trên internet và những tích lũy liên quan trong công việc nghiên cứu khoa học hàng ngày. Mọi kỹ thuật chỉ mang tính tham khảo, không đảm bảo đúng 100%. Nếu có bất kỳ vấn đề gì, hoan nghênh gửi Issue hoặc PR. Ngoài ra, các huy hiệu (badge) được sử dụng trong dự án này đến từ internet, nếu xâm phạm bản quyền hình ảnh của bạn vui lòng liên hệ chúng tôi để xóa, cảm ơn.

## 🤝 Hoan nghênh đóng góp

Hướng dẫn này hiện là một dự án đang trong quá trình thực hiện, khó tránh khỏi thiếu sót, hoan nghênh mọi PR và thảo luận issue.

## ❤️ Danh sách người đóng góp

Cảm ơn các thầy cô và các bạn sau đây đã ủng hộ và đóng góp cho dự án này:

**Đội ngũ phát triển loạt hướng dẫn 《动手学大模型》**:

- Đại học Giao thông Thượng Hải: [张倬胜](https://bcmi.sjtu.edu.cn/home/zhangzs/)、[袁童鑫](https://github.com/Lordog)、[马欣贝](https://scholar.google.com/citations?user=LpUi3EgAAAAJ&hl=zh-CN&oi=ao)、 [何志威](https://zwhe99.github.io)、[杜巍](https://scholar.google.com/citations?user=tFYUBLkAAAAJ&hl=en)、[赵皓东](https://dongdongzhaoup.github.io/)、[吴宗儒](https://zrw00.github.io/)、[吴铮](https://wuzheng02.github.io/)、[董凌众](https://github.com/LZ-Dong)、[张玉龙](https://aslan-yulong.github.io/)

- Đại học Quốc gia Singapore: [费豪](http://haofei.vip/)

**Đội ngũ phát triển loạt hướng dẫn 《Quy trình phát triển toàn diện mô hình lớn》:**

- Đại học Giao thông Thượng Hải: [张倬胜](https://bcmi.sjtu.edu.cn/home/zhangzs/)、[刘功申](https://infosec.sjtu.edu.cn/DirectoryDetail.aspx?id=75)、[陈星宇](https://scholar.google.com/citations?user=d-dNtjrMJ5YC&hl=en)、[程彭洲](https://scholar.google.com/citations?user=qxnwzDUAAAAJ&hl=en)、[董凌众](https://github.com/LZ-Dong)、 [何志威](https://zwhe99.github.io)、[鞠天杰](https://scholar.google.com/citations?user=f8PPcnoAAAAJ&hl=en)、[马欣贝](https://scholar.google.com/citations?user=LpUi3EgAAAAJ&hl=zh-CN&oi=ao)、 [吴铮](https://scholar.google.com/citations?hl=zh-CN&user=qBM1UbUAAAAJ&view_op=list_works&gmla=AIfU4H6PG9JyjRub6BYIIZ4isQE7MBAM3Eoec6OJfX4z_8-pOE8bI1Wgdo3XL5qOZWR3U-h-lIP2q0zXt5gzyFKMSg7MNnBBWLv5d1IVG30UANczTP0)、[吴宗儒](https://zrw00.github.io/)、[闫子赫](https://scholar.google.com/citations?user=O2YfSHoAAAAJ&hl=zh-CN)、[姚杳](https://scholar.google.com/citations?user=tLMP3IkAAAAJ)、[袁童鑫](https://github.com/Lordog)、[赵皓东](https://dongdongzhaoup.github.io/);

- Cộng đồng Huawei Ascend: ZOMI、谢乾、程黎明、楼梨华、焦泽昱

## 🌟 Lịch sử Star

[![Star History Chart](https://api.star-history.com/svg?repos=Lordog/dive-into-llms&type=Date)](https://star-history.com/#Lordog/dive-into-llms&Date)
