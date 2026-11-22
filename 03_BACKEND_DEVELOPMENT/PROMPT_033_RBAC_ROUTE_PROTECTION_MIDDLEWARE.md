# PROMPT 033 – ROLE-BASED ACCESS CONTROL (RBAC) & ROUTE PROTECTION MIDDLEWARE

## 1. ROLE
Backend Security Engineer

## 2. OBJECTIVE
Xây dựng các middleware xác thực Bearer Token (verifyAuth) và kiểm tra phân quyền người dùng (requireRole/restrictTo: ADMIN, STAFF, CUSTOMER).


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_02_CLOUDINARY_ADMIN_PRODUCT_MANAGEMENT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_02_CLOUDINARY_ADMIN_PRODUCT_MANAGEMENT.md)
> - [USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md)
> - [USER_MASTER_PROMPT_25_PRODUCTION_UPGRADE_NOTIFICATION_HANDOFF.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_25_PRODUCTION_UPGRADE_NOTIFICATION_HANDOFF.md)

## 3. CONTEXT
Các route quản trị như tạo sản phẩm, đổi trạng thái đơn hàng, xem báo cáo doanh thu chỉ dành cho ADMIN hoặc STAFF. Khách hàng thông thường truy cập các route này phải bị từ chối với HTTP 403 Forbidden.

## 4. PREREQUISITES
- PROMPT_032: JWT Authentication Service

## 5. INPUTS
- Danh sách vai trò người dùng trong hệ thống Routine

## 6. DETAILED TASKS
1. **Tạo Middleware authenticate (verifyToken)**:
   Trích xuất token từ Authorization header (Bearer <token>), giải mã bằng JWT_SECRET, nạp user từ database (kiểm tra status ACTIVE) và gán vào req.user. Nếu token thiếu hoặc không hợp lệ, trả về 401 Unauthorized.

2. **Tạo Middleware authorize (...roles)**:
   Nhận danh sách roles cho phép (ví dụ: ["ADMIN", "STAFF"]). Kiểm tra req.user.role có nằm trong danh sách không. Nếu không, ném lỗi 403 Forbidden với thông điệp rõ ràng.

3. **Tạo Middleware optionalAuth**:
   Hỗ trợ các route công khai nhưng có thể cá nhân hóa nếu khách đã đăng nhập (như xem sản phẩm, gợi ý outfit).

## 7. TECHNICAL REQUIREMENTS
- Xử lý TokenExpiredError và JsonWebTokenError riêng biệt
- Hỗ trợ gắn kết req.user vào toàn bộ lifecycle của request

## 8. INTEGRATION REQUIREMENTS
- Áp dụng cho toàn bộ các route trong /api/v1/admin/* và các route tài khoản cá nhân


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Privilege Escalation**: Tuyệt đối không tin tưởng role được truyền từ body hay params của client.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Request không có token vào route bảo vệ nhận HTTP 401.
[ ] **AC-2**: Request với role CUSTOMER vào route yêu cầu ADMIN nhận HTTP 403.
[ ] **AC-3**: Request với role ADMIN truy cập thành công.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Gửi request không token tới /api/v1/admin/dashboard kiểm tra 401
2. **Tình huống kiểm thử 2**: Gửi request với token Customer tới /api/v1/admin/dashboard kiểm tra 403

## 12. EXPECTED OUTPUT
- `backend/src/middlewares/authMiddleware.js`: Middleware xác thực và phân quyền

## 13. COMPLETION REPORT
- Hệ thống phân quyền RBAC hoạt động chính xác và an toàn
