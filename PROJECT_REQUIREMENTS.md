# YÊU CẦU NGHIỆP VỤ & ĐẶC TẢ KỸ THUẬT DỰ ÁN ROUTINE
## REPOSITORY THAM CHIẾU: routine-web-demo

---

## 1. MỤC TIÊU DỰ ÁN
Xây dựng nền tảng thương mại điện tử thời trang Routine hiện đại, kết hợp trí tuệ nhân tạo (AI Agent Stylist) và điều hành thông minh (AI Business Intelligence), mang lại trải nghiệm mua sắm cá nhân hóa cho khách hàng và bộ công cụ quản trị dữ liệu chính xác cho doanh nghiệp.

---

## 2. STACK CÔNG NGHỆ CHUẨN XÁC
- **Frontend:**
  - Next.js 16.4.3 (App Router, Turbopack, SSR/SSG 38 routes).
  - React 19.2.3.
  - CSS Modules (Giao diện tối giản, thanh lịch, typography chuẩn Routine).
- **Backend:**
  - Node.js & Express 4.22.3 (CJS, bin/www kiến trúc chuẩn module hóa).
  - Server-Sent Events (SSE) `/api/v1/realtime` truyền tải sự kiện thời gian thực.
  - Nodemailer tích hợp SMTP gửi mã xác thực OTP và hóa đơn điện tử.
  - Multer lưu trữ media cục bộ và tích hợp Cloudinary SDK.
- **Database & ORM:**
  - MySQL 8.0 (Database: `routine_test_db`).
  - Prisma ORM 6.19.3 (29 Models, quan hệ 3NF, giao dịch ACID).
- **Trí Tuệ Nhân Tạo (AI):**
  - Google Gemini 2.5 Flash / 1.5 Flash.
  - Thư viện: `@google/genai` & `@google/generative-ai`.
  - Cơ chế: Multi-turn Context, Database Grounding, Heuristic Rule-engine Fallback.
- **Thanh toán:**
  - VNPay SDK 2.5.0 + HMAC-SHA512 + Dynamic Payment URL + Embedded Dynamic QR.

---

## 3. CÁC PHÂN HỆ NGHIỆP VỤ LÕI
1. **Catalog & Sản phẩm:** 54 sản phẩm thực, phân loại biến thể SKU (kích cỡ S, M, L, XL; màu sắc; số lượng tồn kho; mã vạch).
2. **Khách hàng & Xác thực:** Đăng ký bằng Email/SĐT, mã OTP 6 số hiệu lực 5 phút, lưu trữ mật khẩu mã hóa bcryptjs, phân quyền 3 cấp (CUSTOMER, STAFF, ADMIN).
3. **Giỏ hàng & Đặt hàng:** Giỏ hàng Guest đồng bộ sang Customer sau khi đăng nhập, tính phí ship theo khoảng cách showroom, áp dụng coupon giảm giá, trừ tồn kho an toàn.
4. **AI Stylist Agent:** Trợ lý ảo tư vấn trang phục theo dịp, màu, form dáng, ngân sách; đối chiếu kho MySQL thực; phát hiện ý định mua hàng; bàn giao lead sang chuyên viên.
5. **Admin Portal & AI BI:** Bảng điều khiển KPI, Quản lý đơn hàng, Quản lý kho, Quản lý khách hàng RFM, Live chat tiếp nhận lead và Module AI BI phân tích 5 nhóm dữ liệu kinh doanh.