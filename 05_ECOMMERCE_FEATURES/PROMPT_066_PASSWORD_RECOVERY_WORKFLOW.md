# PROMPT 066 – PASSWORD RESET & ACCOUNT RECOVERY WORKFLOW

## 1. ROLE
Frontend & Backend Security Developer

## 2. OBJECTIVE
Xây dựng quy trình Quên mật khẩu và Khôi phục tài khoản (app/forgot-password/page.js và app/reset-password/page.js): Gửi mã xác nhận qua email/OTP và đặt lại mật khẩu mới an toàn.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_21_ADDRESS_VALIDATION_AI_CONSULTATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_21_ADDRESS_VALIDATION_AI_CONSULTATION.md)
> - [USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md)

## 3. CONTEXT
Khách hàng có thể quên mật khẩu truy cập. Cần có quy trình gửi email khôi phục kèm token có thời hạn 15 phút để đảm bảo quyền sở hữu tài khoản.

## 4. PREREQUISITES
- PROMPT_032: Backend Auth Service
- PROMPT_065: Login Flow

## 5. INPUTS
- Email khách hàng và Reset Token

## 6. DETAILED TASKS
1. **Xây dựng Trang Yêu Cầu Khôi Phục (/forgot-password)**:
   Form nhập email đã đăng ký. Gửi yêu cầu POST /api/v1/auth/forgot-password, hiển thị thông báo đã gửi liên kết khôi phục.

2. **Xây dựng Trang Đặt Lại Mật Khẩu (/reset-password)**:
   Lấy token từ query URL. Form nhập mật khẩu mới và xác nhận mật khẩu. Gửi request POST /api/v1/auth/reset-password.

3. **Xử lý các tình huống lỗi hết hạn token**:
   Nếu token quá hạn hoặc không hợp lệ, hiển thị thông báo và nút yêu cầu gửi lại liên kết mới.

## 7. TECHNICAL REQUIREMENTS
- Token khôi phục mã hóa 1 chiều (SHA-256) trong database
- Thời hạn token tối đa 15 phút

## 8. INTEGRATION REQUIREMENTS
- Liên kết trực tiếp từ trang /login


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Account Enumeration**: Dù email có tồn tại trong hệ thống hay không, phản hồi thông báo luôn báo "Đã gửi liên kết khôi phục nếu email hợp lệ" để bảo mật danh tính người dùng.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Gửi yêu cầu khôi phục mật khẩu nhận được thông báo thành công.
[ ] **AC-2**: Đặt lại mật khẩu với token hợp lệ thành công và đăng nhập được bằng mật khẩu mới.
[ ] **AC-3**: Token hết hạn bị từ chối với thông báo rõ ràng.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm thử gửi yêu cầu và đặt mật khẩu mới hoàn tất

## 12. EXPECTED OUTPUT
- `frontend/src/app/forgot-password/page.js`: Trang yêu cầu quên mật khẩu
- `frontend/src/app/reset-password/page.js`: Trang đặt lại mật khẩu mới

## 13. COMPLETION REPORT
- Quy trình khôi phục mật khẩu tài khoản hoàn thành
