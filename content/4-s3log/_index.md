---
title : "Testing & Demo"
weight : 4
chapter : false
date : 2025-08-12
pre : " <b> 4. </b> "
---

{{% notice info %}}
Chúng ta kiểm thử toàn bộ pipeline đã xây dựng, bao gồm các tình huống thành công và thất bại
{{% /notice %}}

Trong phần này, chúng ta sẽ:
- Kiểm thử với artifact chứa dependency lỗi.
- Chạy full pipeline để xác nhận quy trình build → scan → approve/reject.
- Thực hiện load test để đánh giá hiệu năng pipeline.
- Mô phỏng sự cố để kiểm tra cơ chế failover.
- Xuất báo cáo kết quả thực hành.

---

### **Nội dung thực hành**
- [Kiểm thử với artifact chứa dependency lỗi](4.1-test-vulnerable-artifact/)
- [Chạy full pipeline: build → scan → approve/reject](4.2-run-full-pipeline/)
- [Load test pipeline (parallel scan)](4.3-load-test-pipeline/)
- [Failover test (simulate outage)](4.4-failover-test/)
- [Xuất báo cáo workshop](4.5-generate-report/)
