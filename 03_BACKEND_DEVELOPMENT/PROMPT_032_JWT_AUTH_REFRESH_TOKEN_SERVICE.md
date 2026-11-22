# PROMPT 032 – JWT AUTHENTICATION, REFRESH TOKEN & PASSWORD HASHING SERVICE

## 1. ROLE
Backend Security Engineer

## 2. OBJECTIVE
Xây dựng hệ thống xác thực người dùng sử dụng JSON Web Token (JWT Access Token & Refresh Token) và mã hóa mật khẩu bảo mật bằng bcryptjs.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_02_CLOUDINARY_ADMIN_PRODUCT_MANAGEMENT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_02_CLOUDINARY_ADMIN_PRODUCT_MANAGEMENT.md)
> - [USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md)
> - [USER_MASTER_PROMPT_25_PRODUCTION_UPGRADE_NOTIFICATION_HANDOFF.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_25_PRODUCTION_UPGRADE_NOTIFICATION_HANDOFF.md)

## 3. CONTEXT
Routine cần bảo vệ tài khoản khách hàng và ban quản trị. Hệ thống sử dụng cơ chế Access Token (hết hạn sau 15-60 phút) và Refresh Token (hết hạn sau 7-30 ngày) lưu trong cookie an toàn hoặc header.

## 4. PREREQUISITES
- PROMPT_031: Express HTTP Server Architecture
- PROMPT_020: User Model

## 5. INPUTS
- Biến môi trường JWT_SECRET, JWT_EXPIRES_IN, JWT_REFRESH_SECRET

## 6. DETAILED TASKS
1. **Xây dựng AuthService và JWT Utils**:
   Tạo utils/jwt.js cung cấp hàm signAccessToken, signRefreshToken, verifyToken. Thiết lập thuật toán HS256.

2. **Xây dựng Password Hashing Service**:
   Tạo utils/password.js cung cấp hàm hashPassword(plainText, saltRounds=10) và comparePassword(plainText, hash).

3. **Xây dựng AuthController và Routes**:
   Cung cấp các endpoint: POST /api/v1/auth/register, POST /api/v1/auth/login, POST /api/v1/auth/refresh, POST /api/v1/auth/logout, GET /api/v1/auth/me.

## 7. TECHNICAL REQUIREMENTS
- jsonwebtoken ^9.0.0
- bcryptjs ^2.4.3
- Không trả về trường password trong phản hồi User API

## 8. INTEGRATION REQUIREMENTS
- Frontend lưu Access Token vào state/localStorage và Refresh Token vào HTTP-only cookie hoặc storage


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Brute-force & Credential Stuffing**: Không phân biệt thông báo lỗi "Email không tồn tại" và "Mật khẩu sai" để tránh lộ thông tin người dùng.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Đăng ký tài khoản mới mã hóa mật khẩu thành công trong database.
[ ] **AC-2**: Đăng nhập với email/mật khẩu đúng trả về accessToken và thông tin user.
[ ] **AC-3**: Gọi /api/v1/auth/me với Bearer Token trả về đúng profile user.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm thử đăng ký user mới qua cURL/Postman
2. **Tình huống kiểm thử 2**: Kiểm thử đăng nhập thành công và đăng nhập sai mật khẩu

## 12. EXPECTED OUTPUT
- `backend/src/services/authService.js`: Logic nghiệp vụ xác thực
- `backend/src/controllers/authController.js`: Controller tiếp nhận request đăng nhập/đăng ký
- `backend/src/routes/authRoutes.js`: Các route xác thực

## 13. COMPLETION REPORT
- Module xác thực JWT cốt lõi đã hoàn thành
