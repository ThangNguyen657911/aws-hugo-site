---
title: "Worklog Tuần 6"
date: 2026-06-01
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---
{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}


### Mục tiêu tuần 6:

* Tìm hiểu và triển khai giải pháp quản lý truy cập tập trung thông qua AWS IAM Identity Center (AWS SSO).
* Nghiên cứu cơ chế kiểm soát quyền hạn nâng cao bằng cách áp dụng IAM Permissions Boundary để giới hạn phạm vi phân quyền cho các IAM Entity.
* Tìm hiểu giải pháp mã hóa dữ liệu bảo mật với AWS Key Management Service (KMS) và xây dựng hệ thống giám sát an ninh chủ động với AWS Security Hub.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - **AWS IAM Identity Center (AWS SSO):** <br>&emsp; + Tìm hiểu lý thuyết về Single Sign-On (SSO) và lợi ích của quản lý định danh tập trung <br>&emsp; + So sánh kiến trúc IAM truyền thống và IAM Identity Center | 07/06/2026   | 07/06/2026      | <https://docs.aws.amazon.com/> |
| 3   | - **Thực hành AWS IAM Identity Center:** <br>&emsp; + Kích hoạt dịch vụ IAM Identity Center tại vùng (Region) đang làm việc <br>&emsp; + Khởi tạo User nhóm quyền quản trị thông qua Identity Center Portal để đăng nhập hệ thống an toàn | 08/06/2026   | 08/06/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - **AWS IAM Permissions Boundary:** <br>&emsp; + Nghiên cứu khái niệm ranh giới quyền hạn (Permissions Boundary) <br>&emsp; + Cách kết hợp Policy thông thường và Permissions Boundary để thiết lập giới hạn an toàn cao nhất (*Effective Permissions*) | 09/06/2026   | 09/06/2026      | <https://docs.aws.amazon.com/> |
| 5   | - **Thực hành Permissions Boundary & AWS KMS:** <br>&emsp; + Thiết lập Permissions Boundary cho một IAM User, thực nghiệm việc tạo quyền vượt mức để kiểm tra cơ chế chặn <br>&emsp; + Tìm hiểu AWS KMS, tạo Customer Managed Key (CMK) và thực hiện mã hóa/giải mã cơ bản | 10/06/2026   | 10/06/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - **AWS Security Hub:** <br>&emsp; + Tìm hiểu cách Security Hub thu thập, tổng hợp các cảnh báo bảo mật từ nhiều dịch vụ <br>&emsp; + Nghiên cứu các tiêu chuẩn bảo mật chính như AWS Foundational Security Best Practices và CIS AWS Foundations Benchmark | 11/06/2026   | 11/06/2026      | <https://docs.aws.amazon.com/> |
| 7   | - **Thực hành AWS Security Hub:** <br>&emsp; + Kích hoạt AWS Security Hub trên AWS Console <br>&emsp; + Đọc và phân tích các chỉ số bảo mật (Security score), tìm hiểu cách khắc phục một số lỗ hổng bảo mật cơ bản do hệ thống cảnh báo | 12/06/2026   | 12/06/2026      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 6:

* **Về AWS IAM Identity Center (AWS SSO):**
  * Hiểu rõ kiến trúc quản lý truy cập nhiều tài khoản (Multi-account) và cơ chế liên kết định danh tập trung giúp giảm thiểu rủi ro rò rỉ thông tin đăng nhập.

  * Thực hành kích hoạt thành công **AWS IAM Identity Center**, tạo một Identity Portal riêng biệt cùng các tài khoản định danh phục vụ tác vụ quản lý hằng ngày thay thế hoàn toàn cho IAM User truyền thống.

* **Về AWS IAM Permissions Boundary:**
  * Nắm vững cơ chế đánh giá quyền hạn (Policy Evaluation Logic) phức tạp của AWS khi có sự xuất hiện của Permissions Boundary.

  * Áp dụng thành công **Permissions Boundary** để giới hạn quyền lực tối đa cho một IAM User phụ trách phát triển (Developer). Dù User này được gán Policy có quyền quản trị tối cao (`AdministratorAccess`), họ vẫn không thể thực hiện các thao tác phá hoại hoặc can thiệp sâu vào tài nguyên hệ thống ngoài phạm vi ranh giới được chỉ định sẵn.

* **Về AWS Key Management Service (KMS):**
  * Nắm rõ nguyên lý hoạt động của mã hóa đối xứng (Symmetric Encryption) và mã hóa bất đối xứng (Asymmetric Encryption) trong môi trường Cloud.
  * Phân biệt được sự khác nhau giữa các loại khóa: AWS Managed Keys và Customer Managed Keys (CMK). Thực hành khởi tạo thành công 1 khóa CMK, cấu hình Key Policy để phân quyền sử dụng khóa và ứng dụng nó để mã hóa/giải mã thử nghiệm một tập tin dữ liệu.

* **Về AWS Security Hub:**
  * Hiểu được vai trò của Security Hub như một trung tâm quản lý tư thế an ninh đám mây (CSPM), tự động liên kết các phát hiện (findings) bất thường từ Amazon GuardDuty, Amazon Inspector và AWS IAM.
  * Kích hoạt thành công dịch vụ **AWS Security Hub**, áp dụng tiêu chuẩn bảo mật *AWS Foundational Security Best Practices*. Dựa trên danh sách cảnh báo thu thập được, phân tích và bước đầu xử lý các rủi ro bảo mật tồn đọng trên tài khoản như: thu hồi Access Key chưa sử dụng, cấu hình lại các quy tắc Security Group bị hở cổng nhạy cảm ra môi trường Internet.