# MASTER PROMPT – ROUTINE E-COMMERCE PLATFORM (FROM ZERO)

## 1. TỔNG QUAN VÀ MỤC ĐÍCH
Tài liệu này là chỉ dẫn cấp cao (Master Prompt) dành cho Orchestrator AI Agent chịu trách nhiệm điều phối việc xây dựng toàn bộ hệ thống Routine E-Commerce Platform từ thư mục trống đến một sản phẩm thương mại điện tử hoàn chỉnh, đa kênh và sẵn sàng vận hành thực tế.

Hệ thống bao gồm:
- **Customer Storefront (Next.js 16.4.3 / React 19.2.3):** Trang chủ, Danh mục đa cấp, Chi tiết sản phẩm & Biến thể SKU, Giỏ hàng, Thanh toán, Hồ sơ, Smart Outfit.
- **AI Stylist Agent (Gemini 2.5 Flash):** Trợ lý tư vấn thời trang thông minh đa lượt (multi-turn), nhận diện thực thể/dịp mặc/ngân sách, truy xuất dữ liệu sản phẩm thực từ MySQL (Grounding), và tự động chuyển giao lead tư vấn (Handoff) cho chuyên viên.
- **Payment Gateway (VNPay 2.5.0):** Tích hợp thanh toán trực tuyến qua VNPAY Gateway và Embedded QR Code động với chữ ký số HMAC-SHA512 an toàn.
- **Admin & CRM Portal (Express RESTful + SSE Realtime):** Quản trị danh mục, kho hàng, đơn hàng, khách hàng, voucher, live chat tiếp quản lead và AI Business Intelligence.
- **Database Architecture (MySQL 8.0 + Prisma 6.19.3):** Hệ cơ sở dữ liệu quan hệ gồm 29 bảng chuẩn hóa 3NF, ràng buộc toàn vẹn và giao dịch ACID.

---

## 2. NGUYÊN TẮC THI CÔNG BẮT BUỘC
1. **Tuân thủ đúng thứ tự phụ thuộc:** Không thực hiện bất kỳ prompt nào khi các prompt điều kiện tiên quyết (Prerequisites) chưa hoàn thành và được nghiệm thu.
2. **Không sử dụng dữ liệu giả (No Mock Data):** Toàn bộ API và giao diện phải kết nối trực tiếp với cơ sở dữ liệu MySQL và logic nghiệp vụ backend thật.
3. **Không để AI bịa thông tin sản phẩm:** AI Stylist Agent bắt buộc phải truy vấn từ cơ sở dữ liệu sản phẩm thực tế của Routine.
4. **Bảo mật tuyệt đối (Zero Hardcoded Secrets):** Khóa bí mật JWT, API Key Gemini, Merchant Secret VNPAY và thông tin kết nối DB phải nạp qua biến môi trường `.env`.
5. **Chất lượng mã nguồn đạt chuẩn 0 Warnings:** Mã nguồn Frontend và Backend phải vượt qua ESLint với 0 errors và 0 warnings.
6. **Kiểm thử liên thông 100%:** Mỗi giai đoạn phải có bài test xác thực trước khi chuyển giao sang giai đoạn tiếp theo.

---

## 3. CẤU TRÚC BỘ THƯ VIỆN 11 GIAI ĐOẠN (128 PROMPTS)
- `00_PROJECT_FOUNDATION` (Prompt 001 - 010): Khảo sát, đặc tả SRS/BRD, thiết kế kiến trúc, hợp đồng API và chính sách an ninh.
- `01_ENVIRONMENT_SETUP` (Prompt 011 - 018): Khởi tạo dự án monorepo, cấu hình Node/Express, Next.js, ESLint và môi trường chạy song song.
- `02_DATABASE_ARCHITECTURE` (Prompt 019 - 030): Thiết kế 29 model Prisma, quan hệ khóa ngoại, migration và nạp dữ liệu mẫu ban đầu.
- `03_BACKEND_DEVELOPMENT` (Prompt 031 - 048): Xây dựng Express middleware, JWT auth, RBAC, 26 services và controllers quản trị dữ liệu.
- `04_FRONTEND_DESIGN` (Prompt 049 - 062): Xây dựng Design System, AppShell, Header ROUTINE, Footer, Hero Slider, ProductCard, Category và Responsive.
- `05_ECOMMERCE_FEATURES` (Prompt 063 - 078): Xây dựng luồng Đăng ký/OTP, Đăng nhập, Giỏ hàng, Wishlist, Checkout 3 bước, Đơn hàng và Đánh giá.
- `06_AI_STYLIST_AGENT` (Prompt 079 - 093): Tích hợp Gemini, NLP tiếng Việt, RAG Database Grounding, Phối đồ Smart Outfit, Multi-turn Context và Handoff.
- `07_ADMIN_CRM` (Prompt 094 - 105): Xây dựng Admin Dashboard, AI BI 5 nhóm phân tích, Bảng tối ưu responsive, Quản lý kho, Khách hàng và Realtime Chat.
- `08_PAYMENT_VNPAY` (Prompt 106 - 113): Tích hợp VNPAY Sandbox, Dynamic URL, Embedded QR, IPN Webhook, Idempotency và kiểm thử giao dịch.
- `09_TESTING_SECURITY` (Prompt 114 - 121): Kiểm thử tự động E2E bằng Playwright, Pen-test bảo mật API, Kiểm tra tính toàn vẹn DB và Stress-test.
- `10_DEPLOYMENT_FINALIZATION` (Prompt 122 - 128): Build Production Next.js 38 routes, Docker hóa, Backup định kỳ, SEO, Sổ tay vận hành và Nghiệm thu.

---

## 4. HƯỚNG DẪN DÀNH CHO AI AGENT THỰC HIỆN
1. Mở file `EXECUTION_ORDER.md` để xác định prompt tiếp theo cần thi công.
2. Đọc kỹ toàn bộ 13 mục trong file `PROMPT_XXX.md` tương ứng.
3. Thực thi đúng các nhiệm vụ chi tiết tại mục **6. DETAILED TASKS** và tuân thủ mục **7. TECHNICAL REQUIREMENTS**.
4. Chạy kiểm thử theo mục **11. TESTING REQUIREMENTS** và đối chiếu tiêu chí tại mục **10. ACCEPTANCE CRITERIA**.
5. Tạo biên bản báo cáo hoàn thành theo mẫu tại mục **13. COMPLETION REPORT** trước khi chuyển bước.