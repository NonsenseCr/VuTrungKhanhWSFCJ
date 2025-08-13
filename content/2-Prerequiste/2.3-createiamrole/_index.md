---
title : "Khởi tạo CodeArtifact Domain & Repository"
weight : 3
chapter : false
date : 2025-08-12
pre : " <b> 2.3 </b> "
---


## Mục tiêu
- Tạo CodeArtifact Domain
- Tạo Repository cho từng môi trường (dev/test/prod)
- Lưu thông tin repository để dùng trong pipeline CI/CD

## 1. Tạo Repository
1. Trong CodeArtifact, chọn tab **Repositories** → **Create repository**.
![VPC](/images/zzz/231.png)
2. Nhập tên repository, ví dụ: `secure-repo-dev`.
![VPC](/images/zzz/232.png)
3. Ở mục **Domain**, chọn domain 
![VPC](/images/zzz/233.png)
4. (Tuỳ chọn) Chọn **Upstream repositories** nếu muốn kết nối với public registry (npm, Maven, PyPI...).
5. Bấm **Create repository**.
![VPC](/images/zzz/234.png)
> Lặp lại bước này để tạo các repository cho môi trường `test` và `prod` nếu cần.



## 2. Lưu thông tin kết nối
Sau khi tạo repository: 
- Trong repository (secure-artifact) → bấm nút View connection instructions.

![VPC](/images/zzz/235.png)

- AWS sẽ mở một pop-up hoặc trang mới hiển thị các thông tin kết nối:

![VPC](/images/zzz/236.png)






