# KIẾN TRÚC TỔNG THỂ HỆ THỐNG ROUTINE E-COMMERCE PLATFORM
## SƠ ĐỒ KHỐI, LUỒNG DỮ LIỆU & TƯƠNG TÁC THÀNH PHẦN

---

## 1. SƠ ĐỒ KIẾN TRÚC TỔNG THỂ (C4 MODEL - SYSTEM CONTEXT)
```mermaid
flowchart TD
    ClientBrowser["Client Web Browser (Desktop / Tablet / Mobile)"]
    NextFrontend["Frontend Next.js 16.4.3 (Port 3000)\n- App Router (38 routes)\n- React 19 Contexts\n- CSS Modules UI"]
    ExpressBackend["Backend Express 4.22.3 (Port 5001)\n- RESTful API v1\n- JWT & RBAC Middleware\n- SSE Realtime Stream\n- 26 Services & Controllers"]
    MySQLDB[("MySQL Database 8.0\n- Prisma ORM 6.19.3\n- 29 Tables 3NF\n- routine_test_db")]
    GeminiAI["Google Gemini AI API (Gemini 2.5 Flash)\n- Fashion Intent & Entity Extraction\n- Grounded Product Suggestions\n- AI BI Strategic Recommendations"]
    VNPayGateway["VNPay Payment Gateway Sandbox\n- HMAC-SHA512 Signature\n- Embedded Dynamic QR\n- IPN Webhook Verification"]
    SMTPServer["SMTP Email Server\n- OTP Verification\n- Order E-Invoices"]

    ClientBrowser <-->|HTTP / HTTPS| NextFrontend
    NextFrontend <-->|REST API / JSON| ExpressBackend
    NextFrontend <-->|SSE Stream /realtime| ExpressBackend
    ExpressBackend <-->|Prisma Client / TCP| MySQLDB
    ExpressBackend <-->|REST / SDK| GeminiAI
    ExpressBackend <-->|URL / IPN Webhook| VNPayGateway
    ExpressBackend <-->|SMTP / TLS| SMTPServer
```

---

## 2. LUỒNG DỮ LIỆU THANH TOÁN VNPAY EMBEDDED QR
```mermaid
sequenceDiagram
    autonumber
    actor Customer as Khách Hàng
    participant FE as Frontend Checkout
    participant BE as Backend Express
    participant DB as MySQL Database
    participant VNP as VNPAY Gateway

    Customer->>FE: Bấm "Thanh toán qua VNPAY"
    FE->>BE: POST /api/v1/payment/create-payment-url (orderId)
    BE->>DB: Kiểm tra đơn hàng & Khóa tạm tồn kho
    BE->>BE: Tạo URL thanh toán kèm chữ ký HMAC-SHA512
    BE-->>FE: Trả về paymentUrl & Chuỗi dữ liệu QR
    FE->>FE: Tạo mã QR VNPAY động hiển thị tại trang Checkout
    Customer->>FE: Quét mã QR bằng App Ngân hàng
    Customer->>VNP: Xác nhận thanh toán
    VNP->>BE: GET /api/v1/payment/vnpay-ipn (Kèm chữ ký bảo mật)
    BE->>BE: Xác minh chữ ký vnp_SecureHash & Kiểm tra số tiền
    BE->>DB: Cập nhật PaymentTransaction & Đơn hàng sang PAID
    BE-->>VNP: Trả về RspCode: 00 (Confirm Success)
    BE->>FE: Bắn sự kiện SSE order_paid
    FE->>Customer: Tự động chuyển hướng sang trang Hóa đơn thành công
```

---

## 3. LUỒNG TƯƠNG TÁC AI STYLIST & CHUYỂN GIAO LEAD (HANDOFF)
```mermaid
sequenceDiagram
    autonumber
    actor Khach as Khách Hàng
    participant UI as AI Stylist Floating Widget
    participant BE as AI Service & Grounding Engine
    participant DB as MySQL (Products & Logs)
    participant Gemini as Google Gemini 2.5 Flash
    actor Staff as Chuyên Viên Tư Vấn (Admin)

    Khach->>UI: "Tôi muốn tìm áo khoác nam màu nâu dưới 1.5 triệu"
    UI->>BE: POST /api/v1/ai/chat (prompt, conversationId)
    BE->>Gemini: Phân tích Ý định & Trích xuất thực thể (Áo khoác, Nam, Nâu, <1.5tr)
    Gemini-->>BE: Trả về JSON filter { category: "Áo khoác", gender: "men", color: "brown", maxPrice: 1500000 }
    BE->>DB: Truy vấn sản phẩm thực khớp điều kiện (Grounding)
    DB-->>BE: 2 sản phẩm tồn kho thực tế (Wool Blend Coat, Denim Jacket)
    BE->>Gemini: Tổng hợp câu trả lời tự nhiên từ danh sách sản phẩm thật
    Gemini-->>BE: Câu trả lời gợi ý kèm danh sách ID sản phẩm
    BE->>DB: Lưu tin nhắn vào ai_conversation_messages
    BE-->>UI: Hiển thị lời khuyên & Thẻ sản phẩm tương tác
    Khach->>UI: "Cho tôi gặp nhân viên tư vấn trực tiếp"
    UI->>BE: POST /api/v1/ai/handoff
    BE->>DB: Tạo Notification CONSULTATION_REQUESTED & Đổi trạng thái LEAD
    BE->>Staff: Bắn tín hiệu SSE chuông thông báo trên Admin
    Staff->>UI: Chuyên viên nhắn tin tiếp quản phiên chat thời gian thực
```