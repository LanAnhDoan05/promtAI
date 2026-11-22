# PROMPT 031 – EXPRESS HTTP SERVER ARCHITECTURE, MIDDLEWARES & GLOBAL ERROR HANDLER

## 1. ROLE
Senior Backend Engineer / Express Architect

## 2. OBJECTIVE
Thiết kế cấu trúc dự án backend Express.js chuẩn module hóa, cấu hình các middleware cốt lõi (CORS, Helmet, Morgan, JSON parser) và bộ xử lý lỗi tập trung (Global Error Handler).


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_02_CLOUDINARY_ADMIN_PRODUCT_MANAGEMENT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_02_CLOUDINARY_ADMIN_PRODUCT_MANAGEMENT.md)
> - [USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md)
> - [USER_MASTER_PROMPT_25_PRODUCTION_UPGRADE_NOTIFICATION_HANDOFF.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_25_PRODUCTION_UPGRADE_NOTIFICATION_HANDOFF.md)

## 3. CONTEXT
Backend Routine đóng vai trò là RESTful API server phục vụ cho cả Customer Storefront và Admin Portal. Cấu trúc backend cần tách biệt rõ ràng giữa routes, controllers, services, middlewares và config.

## 4. PREREQUISITES
- PROMPT_030: Phase 02 Database Integrity Gateway đã được phê duyệt

## 5. INPUTS
- Cấu trúc thư mục backend chuẩn MVC/Service pattern

## 6. DETAILED TASKS
1. **Thiết lập cấu trúc thư mục backend**:
   Tổ chức backend/src/ thành controllers/, services/, routes/, middlewares/, config/, utils/, và bin/www.

2. **Cấu hình Middleware Bảo mật và Tiện ích**:
   Cài đặt cors với whitelist domain frontend (localhost:3000 và production domain), helmet() bảo vệ HTTP header, express.json({ limit: "10mb" }), express.urlencoded({ extended: true }), và morgan("dev") cho logging.

3. **Xây dựng Custom Error Class và Global Error Handler**:
   Tạo class AppError extends Error với statusCode, status, isOperational. Xây dựng middleware errorMiddleware bắt mọi lỗi, định dạng JSON phản hồi { success: false, message, error } đồng nhất.

4. **Tạo Entrypoint Server và Graceful Shutdown**:
   Khởi động HTTP server trên cổng PORT (mặc định 5001) trong bin/www, lắng nghe sự kiện SIGTERM/SIGINT để đóng kết nối Prisma và server an toàn.

## 7. TECHNICAL REQUIREMENTS
- Node.js 18+ / Express ^4.22.3
- CORS whitelist chuẩn hóa
- Global Error Handler trả về status code HTTP tương ứng (400, 401, 403, 404, 500)

## 8. INTEGRATION REQUIREMENTS
- Các router API được gắn tiền tố /api/v1/*

## 9. SAFETY CONSTRAINTS
- ⚠️ **Information Leakage**: Không bao giờ để lộ stack trace lỗi ra môi trường production.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Server Express khởi động thành công trên cổng 5001.
[ ] **AC-2**: Truy cập GET /api/v1/health trả về status 200 OK.
[ ] **AC-3**: Lỗi ném ra từ bất kỳ controller nào đều được chuyển về Global Error Handler định dạng JSON.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Gửi request GET http://localhost:5001/api/v1/health kiểm tra phản hồi
2. **Tình huống kiểm thử 2**: Gửi request đến endpoint không tồn tại kiểm tra 404 handler

## 12. EXPECTED OUTPUT
- `backend/src/app.js`: Cấu hình ứng dụng Express và middlewares
- `backend/bin/www`: File thực thi khởi động HTTP server
- `backend/src/middlewares/errorHandler.js`: Bộ xử lý lỗi tập trung

## 13. COMPLETION REPORT
- Hạ tầng HTTP Server Express đã sẵn sàng tiếp nhận các module API
