---
title : "CloudWatch với EventBridge"
date : 2024-01-01 
weight : 4 
chapter : false
pre : " <b> 5.4. </b> "
---

#### Tổng quan

Trong kiến trúc Retail Operations Monitoring Platform (ROMP), hệ thống được xây dựng theo mô hình Serverless và Event-Driven, trong đó Amazon EventBridge và Amazon CloudWatch là hai dịch vụ quan trọng giúp tự động hóa quy trình giám sát và theo dõi hoạt động của toàn bộ hệ thống.

Amazon EventBridge đóng vai trò là bộ lập lịch (Scheduler) và điều phối sự kiện của hệ thống. Thay vì yêu cầu người dùng hoặc quản trị viên chạy chương trình thủ công, EventBridge sẽ kích hoạt các AWS Lambda theo chu kỳ được cấu hình, chẳng hạn mỗi 5 phút hoặc 15 phút. Khi đến thời điểm thực thi, EventBridge sẽ gửi một sự kiện (Event) đến Lambda, từ đó Lambda bắt đầu kết nối đến cơ sở dữ liệu Oracle, thu thập dữ liệu và thực hiện các Business Rule để phát hiện các bất thường như hàng tồn kho thấp, hết hàng, sản phẩm sắp hết hạn hoặc chương trình khuyến mãi sắp kết thúc. Cơ chế này giúp hệ thống hoạt động hoàn toàn tự động, đảm bảo việc giám sát được thực hiện liên tục mà không cần can thiệp thủ công.

Sau khi Lambda được kích hoạt và hoàn thành quá trình xử lý, toàn bộ thông tin thực thi sẽ được ghi nhận trên Amazon CloudWatch. CloudWatch đóng vai trò là dịch vụ giám sát và theo dõi hoạt động của hệ thống, cho phép lưu trữ log, thống kê số lần thực thi, thời gian xử lý, tỷ lệ thành công hoặc lỗi của Lambda. Các thông tin này giúp nhóm vận hành nhanh chóng xác định nguyên nhân khi xảy ra sự cố, đồng thời đánh giá hiệu năng của hệ thống theo thời gian.

Sự kết hợp giữa EventBridge và CloudWatch tạo nên một quy trình vận hành khép kín. EventBridge chịu trách nhiệm kích hoạt các tác vụ theo lịch, trong khi CloudWatch theo dõi và ghi nhận toàn bộ quá trình thực thi. Nhờ đó, ROMP có thể vận hành theo mô hình tự động, giám sát liên tục và cung cấp đầy đủ thông tin để kiểm tra, bảo trì và tối ưu hệ thống.

####  [5.4.1 Cấu hình CloudWatch](5.4.1-prepare/)
####  [5.4.2 Cấu hình EventBridge](5.4.2-create-interface-enpoint/)


