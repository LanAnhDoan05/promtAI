# PROMPT 013 – KHỞI TẠO NEXT.JS 16.4.3 (TURBOPACK, REACT 19.2.3)

## 1. ROLE
Senior Frontend Engineer

## 2. OBJECTIVE
Khởi tạo dự án Next.js 16.4.3 với App Router, Turbopack và React 19.2.3 trong thư mục `frontend/`.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_04_SELF_TEST_ENVIRONMENT_HANDOVER.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_04_SELF_TEST_ENVIRONMENT_HANDOVER.md)
> - [USER_MASTER_PROMPT_15_ADMIN_CUSTOMER_CONCURRENT_OPS.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_15_ADMIN_CUSTOMER_CONCURRENT_OPS.md)

## 3. CONTEXT
Storefront và Admin Portal được xây dựng trên nền tảng Next.js hiện đại, hỗ trợ Server-Side Rendering (SSR) và Static Site Generation (SSG).

## 4. PREREQUISITES
- PROMPT_011 hoàn thành

## 5. INPUTS
- docs/00_CODING_STANDARDS.md

## 6. DETAILED TASKS
1. **Khởi tạo `package.json` cho Frontend**:
   Cài đặt `next@16.4.3`, `react@19.2.3`, `react-dom@19.2.3`, script `dev`, `build`, `start`, `lint`.

2. **Cấu hình `frontend/next.config.js`**:
   Thiết lập Turbopack, cấu hình domain cho ảnh sản phẩm và cài đặt tối ưu hóa biên dịch.

3. **Tạo cấu trúc thư mục App Router**:
   Khởi tạo `frontend/app/layout.js`, `frontend/app/page.js`, `frontend/app/globals.css`.

## 7. TECHNICAL REQUIREMENTS
- Sử dụng Next.js App Router (thư mục `app/`)
- Hỗ trợ CSS Modules mặc định

## 8. INTEGRATION REQUIREMENTS
- Frontend lắng nghe trên cổng 3000, cấu hình kết nối tới Backend 5001.


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Tránh xung đột React 19**: Đảm bảo các thư viện UI tương thích hoàn toàn với React 19.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Chạy `npm run dev` trong `frontend/` khởi động thành công trên `http://localhost:3000`
[ ] **AC-2**: Trang chủ hiển thị thông điệp chào mừng cơ bản của Routine

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Mở trình duyệt truy cập `http://localhost:3000` kiểm tra không có lỗi console

## 12. EXPECTED OUTPUT
- `frontend/package.json`: Cấu hình dependencies Frontend
- `frontend/next.config.js`: File cấu hình Next.js
- `frontend/app/layout.js`: Root layout của ứng dụng Next.js

## 13. COMPLETION REPORT
- Xác nhận Next.js 16 khởi tạo thành công và chạy ổn định trên cổng 3000.
