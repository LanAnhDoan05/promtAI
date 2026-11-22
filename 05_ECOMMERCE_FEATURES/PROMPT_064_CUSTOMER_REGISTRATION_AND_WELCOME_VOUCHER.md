# PROMPT 064 – CUSTOMER REGISTRATION FLOW WITH REALTIME VALIDATION & WELCOME VOUCHER

## 1. ROLE
Frontend Full-stack Developer

## 2. OBJECTIVE
Xây dựng trang Đăng ký tài khoản (app/register/page.js): Kiểm tra dữ liệu thời gian thực (Họ tên, Email hợp lệ, Mật khẩu tối thiểu 6 ký tự, Xác nhận mật khẩu trùng khớp), tự động tặng voucher chào mừng 10% (WELCOME10) và tự động đăng nhập sau khi tạo tài khoản.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_21_ADDRESS_VALIDATION_AI_CONSULTATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_21_ADDRESS_VALIDATION_AI_CONSULTATION.md)
> - [USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md)

## 3. CONTEXT
Quy trình đăng ký tài khoản cần nhanh chóng, rõ ràng và khuyến khích khách hàng mới bằng quà tặng voucher chào mừng áp dụng ngay cho đơn hàng đầu tiên.

## 4. PREREQUISITES
- PROMPT_063: UserContext

## 5. INPUTS
- Form dữ liệu: fullName, email, phone, password, confirmPassword

## 6. DETAILED TASKS
1. **Xây dựng Giao diện Form Đăng Ký**:
   Thiết kế form tinh tế phong cách Routine với ô nhập họ tên, email, số điện thoại, mật khẩu, và nút con mắt ẩn/hiện mật khẩu.

2. **Kiểm tra Dữ liệu Thời gian Thực (Client-side Validation)**:
   Báo lỗi ngay dưới từng ô input nếu email sai định dạng, mật khẩu < 6 ký tự, hoặc mật khẩu xác nhận không khớp.

3. **Xử lý Đăng Ký và Tặng Voucher Chào Mừng**:
   Gửi request POST /api/v1/auth/register. Khi thành công, hiển thị Toast chúc mừng kèm mã giảm giá WELCOME10, lưu phiên và chuyển hướng tới trang chủ.

## 7. TECHNICAL REQUIREMENTS
- Validation regex email chuẩn
- Khóa nút Đăng ký khi đang submit để chống bấm đúp (double submission)

## 8. INTEGRATION REQUIREMENTS
- Gọi Auth API backend và cập nhật UserContext


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Password Masking**: Mật khẩu phải mặc định ở dạng type="password".

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Điền đúng thông tin tạo tài khoản thành công trong database.
[ ] **AC-2**: Điền thiếu hoặc sai thông tin hiển thị thông báo lỗi chi tiết.
[ ] **AC-3**: Đăng ký thành công nhận được thông báo mã voucher chào mừng.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm thử đăng ký với email trùng lặp kiểm tra thông báo lỗi từ server

## 12. EXPECTED OUTPUT
- `frontend/src/app/register/page.js`: Trang đăng ký tài khoản Routine

## 13. COMPLETION REPORT
- Quy trình đăng ký tài khoản và kích hoạt voucher chào mừng hoàn thành
