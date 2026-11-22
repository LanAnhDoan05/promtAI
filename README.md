# ROUTINE E-COMMERCE PLATFORM – FROM-ZERO PROMPT LIBRARY
## THƯ VIỆN PROMPT XÂY DỰNG DỰ ÁN ROUTINE TỪ CON SỐ 0 CHO AI AGENT

[![GitHub Repository](https://img.shields.io/badge/GitHub-LanAnhDoan05%2FpromtAI-black?style=flat&logo=github)](https://github.com/LanAnhDoan05/promtAI)
[![Total Prompts](https://img.shields.io/badge/Total%20Prompts-128%20Sequential%20Prompts-blue?style=flat)](#)
[![Production Master Prompts](https://img.shields.io/badge/User%20Master%20Prompts-30%20Comprehensive-orange?style=flat)](#)
[![Stack](https://img.shields.io/badge/Stack-Next.js%2016%20%7C%20Express%20%7C%20MySQL%20%7C%20Prisma%20%7C%20Gemini%20%7C%20VNPay-green?style=flat)](#)

---

### 1. GIỚI THIỆU

Thư viện này cung cấp một lộ trình hoàn chỉnh gồm **128 Prompt độc lập, tuần tự và chuyên sâu**, kèm theo **30 Master Prompt thực tế từ Người dùng** và **6 Tài liệu kiến trúc điều phối tổng thể**.

Bất kỳ AI Agent nào (Claude, Gemini, ChatGPT, Codex, Antigravity) cũng có thể sử dụng bộ prompt này để xây dựng lại toàn bộ nền tảng thương mại điện tử **Routine E-commerce Platform** từ một thư mục hoàn toàn trống đến một hệ thống Full-stack đa kênh sẵn sàng vận hành thực tế.

---

### 2. TÀI LIỆU ĐIỀU PHỐI TỔNG THỂ (MASTER ARCHITECTURE)

| Tài liệu | Mô tả chi tiết |
| :--- | :--- |
| 📖 **[MASTER_PROMPT.md](./MASTER_PROMPT.md)** | Chỉ dẫn cấp cao dành cho Orchestrator AI Agent điều phối toàn bộ dự án |
| 📋 **[EXECUTION_ORDER.md](./EXECUTION_ORDER.md)** | Thứ tự thi công chi tiết của 128 prompt và 10 Gateways nghiệm thu |
| ⚙️ **[PROJECT_REQUIREMENTS.md](./PROJECT_REQUIREMENTS.md)** | Đặc tả yêu cầu hệ thống, công nghệ Full-stack và phạm vi tính năng |
| 🏗️ **[ARCHITECTURE_OVERVIEW.md](./ARCHITECTURE_OVERVIEW.md)** | Sơ đồ kiến trúc C4, luồng dữ liệu, sequence VNPay QR và AI Stylist |
| 🗺️ **[PROMPT_DEPENDENCY_MAP.md](./PROMPT_DEPENDENCY_MAP.md)** | Ma trận phụ thuộc giữa 11 Phase và đường găng quan trọng (Critical Path) |
| ✅ **[ACCEPTANCE_CRITERIA.md](./ACCEPTANCE_CRITERIA.md)** | Bộ tiêu chuẩn nghiệm thu và kiểm toán chất lượng toàn diện |

---

### 3. MASTER PROMPT THỰC TẾ TỪ NGƯỜI DÙNG (USER ORIGINAL PRODUCTION PROMPTS)

Thư mục **[`00_USER_PRODUCTION_MASTER_PROMPTS/`](./00_USER_PRODUCTION_MASTER_PROMPTS/)** lưu trữ trọn vẹn toàn văn **30 Master Prompt chuyên sâu** (từ 2.000 đến 23.000 ký tự mỗi prompt) do chính Chủ dự án chỉ đạo và kiểm chứng trực tiếp:

* `USER_MASTER_PROMPT_16_AI_STYLIST_AND_SALES_STANDARDS.md` - Quy chuẩn AI Stylist & Sales Consultant
* `USER_MASTER_PROMPT_18_VNPAY_QR_AND_AI_HUMAN_HANDOFF.md` - Hoàn thiện QR thanh toán và Handoff chuyên viên
* `USER_MASTER_PROMPT_26_EMBEDDED_VNPAY_DYNAMIC_QR.md` - Nhúng mã QR thanh toán động VNPay tại checkout
* `USER_MASTER_PROMPT_28_AI_BI_IMPLEMENTATION_AND_E2E_AUDIT.md` - Module AI Business Intelligence & Phân tích kinh doanh
* `USER_MASTER_PROMPT_29_BI_DASHBOARD_TABLES_UI_OPTIMIZATION.md` - Tối ưu 2 bảng thống kê BI Dashboard không tràn ngang
* *Và 25 Master Prompt thực tế khác.*

---

### 4. BẢNG PHÂN BỔ 11 PHASE VÀ 128 PROMPT THI CÔNG

Mỗi file prompt trong thư viện đều tuân thủ nghiêm ngặt **13 phần chuẩn hóa**:
`1. ROLE` | `2. OBJECTIVE` | `3. CONTEXT` | `4. PREREQUISITES` | `5. INPUTS` | `6. DETAILED TASKS` | `7. TECHNICAL REQUIREMENTS` | `8. INTEGRATION REQUIREMENTS` | `9. SAFETY CONSTRAINTS` | `10. ACCEPTANCE CRITERIA` | `11. TESTING REQUIREMENTS` | `12. EXPECTED OUTPUT` | `13. COMPLETION REPORT`

| Phase | Thư mục | Số lượng Prompt | Mục tiêu trọng tâm |
| :---: | :--- | :---: | :--- |
| **00** | [`00_PROJECT_FOUNDATION/`](./00_PROJECT_FOUNDATION/) | **10** (001 - 010) | Khảo sát, BRD, SRS, Thiết kế Kiến trúc, Tiêu chuẩn Code, Gateway 0 |
| **01** | [`01_ENVIRONMENT_SETUP/`](./01_ENVIRONMENT_SETUP/) | **8** (011 - 018) | Khởi tạo Monorepo, Express, Next.js, .env, ESLint, Gateway 1 |
| **02** | [`02_DATABASE_ARCHITECTURE/`](./02_DATABASE_ARCHITECTURE/) | **12** (019 - 030) | MySQL 8.0, 29 Models Prisma, Quan hệ, Indexes, Seed Data, Gateway 2 |
| **03** | [`03_BACKEND_DEVELOPMENT/`](./03_BACKEND_DEVELOPMENT/) | **18** (031 - 048) | RESTful API, JWT Auth, RBAC, Catalog, Orders, Stock Lock, SSE, Gateway 3 |
| **04** | [`04_FRONTEND_DESIGN/`](./04_FRONTEND_DESIGN/) | **14** (049 - 062) | Design System, Header ROUTINE, PLP, PDP, 5 Viewports Responsive, Gateway 4 |
| **05** | [`05_ECOMMERCE_FEATURES/`](./05_ECOMMERCE_FEATURES/) | **16** (063 - 078) | Cart, Wishlist, Checkout 4 bước, Quản lý đơn, Profile, In hóa đơn, Gateway 5 |
| **06** | [`06_AI_STYLIST_AGENT/`](./06_AI_STYLIST_AGENT/) | **15** (079 - 093) | Gemini 2.5 Flash, Grounding MySQL, Tool Calling, 5-Turn Workflow, Gateway 6 |
| **07** | [`07_ADMIN_CRM/`](./07_ADMIN_CRM/) | **12** (094 - 105) | Admin Portal, Dashboard KPI, AI BI Module, Live Chat SSE Desk, Gateway 7 |
| **08** | [`08_PAYMENT_VNPAY/`](./08_PAYMENT_VNPAY/) | **8** (106 - 113) | VNPay SDK 2.5.0, Dynamic QR nhúng, Return URL, Webhook IPN, Gateway 8 |
| **09** | [`09_TESTING_SECURITY/`](./09_TESTING_SECURITY/) | **8** (114 - 121) | Jest, Pen-testing SQLi/XSS/RBAC, Stress Concurrency, Playwright E2E, Gateway 9 |
| **10** | [`10_DEPLOYMENT_FINALIZATION/`](./10_DEPLOYMENT_FINALIZATION/) | **7** (122 - 128) | Build 38 Routes, PM2 Cluster, Docker Compose, Backup DB, Final Go-Live |

---

### 5. HƯỚNG DẪN SỬ DỤNG CHO AI AGENT

1. **Bước 1:** Bắt đầu bằng việc đọc [`MASTER_PROMPT.md`](./MASTER_PROMPT.md) và [`EXECUTION_ORDER.md`](./EXECUTION_ORDER.md) để nắm toàn bộ sơ đồ điều phối.
2. **Bước 2:** Thực thi tuần tự từ `PROMPT_001.md` đến `PROMPT_128.md`. Tuyệt đối không nhảy cóc qua Phase mới khi chưa được phê duyệt qua cổng Gateway tương ứng.
3. **Bước 3:** Đối chiếu với các Master Prompt thực tế trong thư mục [`00_USER_PRODUCTION_MASTER_PROMPTS/`](./00_USER_PRODUCTION_MASTER_PROMPTS/) khi gặp các nghiệp vụ phức tạp (như phân biệt VietQR vs VNPAY-QR, tối ưu bảng BI không tràn ngang, hoặc chống ảo giác dữ liệu cho Gemini AI).
4. **Bước 4:** Kiểm tra đầy đủ `ACCEPTANCE CRITERIA` và chạy `TESTING REQUIREMENTS` của từng prompt trước khi báo cáo hoàn thành.

---

*Bản quyền nội dung thuộc về Dự án Routine E-commerce Platform.*
