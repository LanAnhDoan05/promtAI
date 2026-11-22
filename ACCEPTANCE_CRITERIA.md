# BỘ TIÊU CHÍ NGHIỆM THU TỔNG THỂ (GLOBAL ACCEPTANCE CRITERIA)
## ROUTINE E-COMMERCE PLATFORM

---

## 1. TIÊU CHÍ CHUNG CHO MỌI PROMPT
Mỗi prompt chỉ được đánh dấu là **HOÀN THÀNH (PASS)** khi thỏa mãn đầy đủ các điều kiện sau:
1. **Không tạo mã lỗi:** Mã nguồn sinh ra biên dịch thành công, không sinh lỗi cú pháp hay runtime exception.
2. **ESLint 0 Cảnh Báo:** Tuyệt đối không có lỗi hoặc cảnh báo ESLint. Không sử dụng comment tắt cảnh báo (`@ts-ignore`, `/* eslint-disable */`).
3. **Bảo toàn dữ liệu:** Không xóa dữ liệu lịch sử hoặc nạp dữ liệu rác vào database.
4. **Bảo mật:** Không để lộ API Key, Secret hay mật khẩu trong mã nguồn Frontend hoặc commit công khai.
5. **Có minh chứng kiểm thử:** Phải chạy script kiểm thử tự động hoặc chụp ảnh minh chứng trước khi nghiệm thu.

---

## 2. TIÊU CHÍ NGHIỆM THU TỪNG PHÂN HỆ
### A. Phân Hệ Cơ Sở Dữ Liệu
- Schema Prisma hợp lệ (`npx prisma validate` pass).
- Migration chạy sạch sẽ không gây mất mát dữ liệu (`npx prisma migrate status` đồng bộ).
- 29 bảng dữ liệu liên kết khóa ngoại chặt chẽ, hỗ trợ giao dịch ACID.

### B. Phân Hệ Backend Express
- Server khởi động ổn định trên cổng 5001, endpoint `/api/v1/health` trả về `status: healthy`.
- Xác thực JWT stateless chính xác, chặn 401 với request không token, chặn 403 với người dùng không phải ADMIN.
- Phí vận chuyển tính toán chuẩn xác theo tọa độ địa lý.
- Luồng tạo đơn hàng tự động khóa tạm tồn kho và ghi log thanh toán.

### C. Phân Hệ Frontend Next.js
- Biên dịch production (`npm run build`) thành công trọn vẹn **38/38 routes**.
- Thương hiệu hiển thị thống nhất là **ROUTINE** trên toàn bộ Desktop, Tablet và Mobile.
- Giao diện hai bảng Dashboard BI hiển thị cân xứng 50% - 50%, không bị tràn ngang ở mọi độ phân giải (1920, 1440, 1366, 768, 390px).

### D. Phân Hệ Trợ Lý AI Stylist
- Nhận diện đúng ý định khách hàng qua ngôn ngữ tự nhiên tiếng Việt.
- Cơ chế Grounding truy xuất 100% từ bảng `products` của MySQL, cấm bịa tên/giá/size/ảnh sản phẩm.
- Duy trì ngữ cảnh đa lượt (Multi-turn Context) thông minh qua ít nhất 5 lượt hỏi đáp liên tiếp.
- Cơ chế Handoff bắn tín hiệu SSE chuẩn xác sang màn hình Admin Leads của nhân viên.

### E. Phân Hệ Thanh Toán VNPay
- Tạo URL thanh toán kèm chữ ký HMAC-SHA512 hợp lệ.
- Mã QR VNPAY động nhúng trực tiếp trên trang Checkout, không bắt buộc rời giao diện Routine.
- IPN Webhook xác thực chữ ký số, cập nhật trạng thái đơn hàng sang `PAID` và kích hoạt trừ tồn kho vĩnh viễn.