---
title : "Tạo cảnh báo với SNS & EventBridge"
weight : 2
chapter : false
date : 2025-08-12
pre : " <b> 3.2 </b> "
---

{{% notice info %}}
Bước này giúp bạn cấu hình cảnh báo tự động khi pipeline hoặc quá trình quét bảo mật phát hiện lỗi nghiêm trọng (High/Critical CVE) hoặc thất bại.
{{% /notice %}}

## Mục tiêu
- Tạo SNS Topic để gửi thông báo qua email
- Tạo EventBridge Rule bắt sự kiện từ CloudWatch Metric hoặc ECR Enhanced Scanning
- Kết nối EventBridge với SNS

## 1. Tạo SNS Topic và đăng ký email
1. Đăng nhập **AWS Console** → vào **SNS**.
2. Chọn **Topics → Create topic**.
3. Loại topic: **Standard**.
4. Tên: `secure-artifact-alert`.
5. Bấm **Create topic**.
6. Trong topic vừa tạo, chọn **Create subscription**:
   - Protocol: `Email`
   - Endpoint: nhập địa chỉ email nhận thông báo.
7. Xác nhận email từ AWS (AWS sẽ gửi một email để confirm).

## 2. Tạo EventBridge Rule
1. Vào **EventBridge** → **Rules** → **Create rule**.
2. Tên: `pipeline-failure-alert`.
3. **Event source**: chọn **AWS events or EventBridge events**.
4. **Pattern**:
   - **Option 1 (CloudWatch Alarm)**: Chọn source từ `aws.cloudwatch` khi metric filter trong 3.1 > 0.
   - **Option 2 (ECR Scan Findings)**: Chọn source từ `aws.ecr` với detail chứa `"severity": ["HIGH","CRITICAL"]`.
5. Bấm **Next**.

## 3. Thêm Target là SNS
1. Trong **Select targets**, chọn **SNS topic**.
2. Chọn topic `secure-artifact-alert`.
3. Bấm **Next** → **Create rule**.

## 4. Kiểm tra
- Tạo một lỗi giả trong pipeline hoặc push Docker image có lỗ hổng High/Critical.
- Kiểm tra email nhận cảnh báo từ SNS.


