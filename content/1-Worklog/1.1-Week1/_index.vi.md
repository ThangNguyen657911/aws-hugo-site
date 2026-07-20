---
title: "Worklog Tuần 1"
date: 2026-04-27
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---
{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}


### Mục tiêu tuần 1:

* Kết nối, làm quen với các thành viên trong First Cloud AI Journey và nắm rõ văn hóa, quy định làm việc tại đơn vị thực tập.
* Đăng ký, thiết lập và bảo mật tài khoản AWS Account root kết hợp quản lý chi phí thông qua AWS Budgets.
* Tìm hiểu và thực hành cơ bản về quản lý định danh hệ thống với AWS IAM và các kênh hỗ trợ kỹ thuật từ AWS Support.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Làm quen và tìm hiểu và lưu ý các nội quy, quy định, văn hóa làm việc tại đơn vị thực tập | 04/05/2026   | 04/05/2026      | Tài liệu nội bộ đơn vị thực tập |
| 3   | - **AWS Account & Budgets:** <br>&emsp; + Tìm hiểu quy trình đăng ký tài khoản AWS Free Tier <br>&emsp; + Tìm hiểu về các nhiệm vụ nhận thưởng <br>&emsp; + Tìm hiểu về AWS Budgets và cách thiết lập cảnh báo chi phí tránh phát sinh ngoài ý muốn | 05/05/2026   | 05/05/2026      | <https://cloudjourney.awsstudygroup.com/> <br> <https://docs.aws.amazon.com/> |
| 4   | - **Thực hành AWS Account & Budgets:** <br>&emsp; + Khởi tạo tài khoản AWS cá nhân <br>&emsp; + Tạo Budget đầu tiên (Set threshold cảnh báo qua Email khi chi phí vượt ngưỡng mong muốn) | 06/05/2026   | 06/05/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - **AWS Support:** <br>&emsp; + Tìm hiểu về các gói hỗ trợ của AWS (Basic, Developer, Business, Enterprise) <br>&emsp; + Cách tạo Support ticket và tra cứu tài liệu hỗ trợ kỹ thuật | 07/05/2026   | 07/05/2026      | <https://docs.aws.amazon.com/> |
| 6   | - **AWS IAM (Identity and Access Management):** <br>&emsp; + Khái niệm cơ bản: Users, Groups, Roles, Policies <br>&emsp; + Các quy tắc bảo mật thực tế tốt nhất (Best practices) của IAM <br>&emsp; + Kích hoạt Multi-Factor Authentication (MFA) cho tài khoản Root | 08/05/2026   | 08/05/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 7   | - **Thực hành IAM:** <br>&emsp; + Thiết lập MFA cho Root Account <br>&emsp; + Tạo một IAM User quản trị (Admin) để sử dụng hằng ngày <br>&emsp; + Phân quyền thông qua IAM Group và gán IAM Policies tương ứng <br>&emsp; + Đăng nhập thử nghiệm và kiểm tra quyền hạn của User mới | 09/05/2026   | 09/05/2026      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 1:

* **Về văn hóa & nội quy làm việc:**
  * Hiểu rõ và cam kết tuân thủ đúng các quy định về giờ giấc làm việc, tính bảo mật thông tin tài nguyên hệ thống, quy trình báo cáo tiến độ và tác phong làm việc chuyên nghiệp tại đơn vị thực tập.

* **Về AWS Account & Budgets:**
  * Đăng ký và kích hoạt thành công tài khoản AWS Free Tier cá nhân.
  * Hoàn thành các nhiệm vụ nhận thưởng
  * Thiết lập cấu hình thành công công cụ **AWS Budgets** với hạn mức cảnh báo thực tế (gửi email cảnh báo tự động khi chi phí thực tế hoặc chi phí dự kiến vượt quá $1, hoặc khi đạt 80% hạn mức Free Tier) giúp kiểm soát chi phí hiệu quả trong suốt quá trình thực tập và học tập.

* **Về AWS Support:**
  * Hiểu rõ sự khác biệt về quyền lợi, thời gian phản hồi và chi phí giữa các gói AWS Support Plan (Basic, Developer, Business, Enterprise).
  * Biết cách sử dụng giao diện AWS Support Center để mở ticket hỗ trợ kỹ thuật hoặc yêu cầu tăng giới hạn tài nguyên (Service Quotas) khi cần thiết.

* **Về AWS IAM (Identity and Access Management):**
  * Nắm vững nguyên lý hoạt động của IAM và mô hình phân quyền bảo mật tối thiểu (*Least Privilege Access*).
  * Hiểu rõ sự khác nhau giữa **IAM User** (định danh cho người dùng cụ thể), **IAM Group** (nhóm người dùng chung quyền), **IAM Role** (ủy quyền tạm thời cho người dùng hoặc dịch vụ AWS) và **IAM Policy** (tài liệu JSON định nghĩa quyền hạn cho phép hoặc từ chối).
  * Tăng cường bảo mật tối đa cho tài khoản gốc bằng cách kích hoạt thành công tính năng xác thực đa nhân tố **MFA (Multi-Factor Authentication)** thông qua ứng dụng Authenticator di động.
  * Tạo thành công một **IAM User** phân quyền quản trị riêng biệt và đăng nhập kiểm tra thực tế, đảm bảo không sử dụng Root Account cho các thao tác cấu hình hệ thống hàng ngày theo đúng khuyến nghị bảo mật của AWS.