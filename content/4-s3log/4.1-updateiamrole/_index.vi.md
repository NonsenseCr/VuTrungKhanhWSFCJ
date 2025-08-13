---
title : "Kiểm thử với artifact chứa dependency lỗi"
weight : 1
chapter : false
date : 2025-08-12
pre : " <b> 4.1 </b> "
---

{{% notice info %}}
Bước này giúp bạn kiểm tra khả năng phát hiện và chặn artifact có chứa dependency lỗ hổng bảo mật trong pipeline.
{{% /notice %}}

## Mục tiêu
- Tạo hoặc sử dụng dự án mẫu có dependency dính CVE đã biết
- Chạy pipeline để xác nhận công cụ quét bảo mật hoạt động
- Đảm bảo artifact bị reject và cảnh báo được gửi

## 1. Chuẩn bị dự án có dependency lỗi
1. Chọn ngôn ngữ bạn đang sử dụng (npm, Maven, Python...).
2. Thêm dependency có CVE đã biết vào file cấu hình:
   - **npm**: Thêm phiên bản cũ của thư viện `lodash` vào `package.json`.
   - **Maven**: Thêm thư viện `commons-collections` phiên bản cũ vào `pom.xml`.
   - **Python**: Thêm `flask==0.5` vào `requirements.txt`.

Ví dụ với npm:

```bash
npm install lodash@4.17.4 --save
```
## 2. Commit & Push thay đổi

```bash
git add .
```
```bash
git commit -m "testing"
```
```bash
git push origin main
```

## 3. Quan sát pipeline GitHub Actions
Mở tab Actions trong repository.

Chọn workflow vừa chạy.

Kiểm tra bước Snyk scan hoặc ECR scan:

-Nếu phát hiện CVE mức High/Critical → job sẽ fail.

-EventBridge/SNS sẽ gửi cảnh báo (nếu cấu hình ở chương 3.2).

## 4. Xác minh kết quả
Artifact sẽ không được publish lên CodeArtifact/ECR.

Email cảnh báo từ SNS (hoặc Slack) được gửi thành công.