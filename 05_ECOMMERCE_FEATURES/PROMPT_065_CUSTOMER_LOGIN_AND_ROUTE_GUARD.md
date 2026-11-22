# PROMPT 065 – CUSTOMER LOGIN FLOW, JWT PERSISTENCE & PROTECTED ROUTE GUARD

## 1. ROLE
Frontend Security & UX Engineer

## 2. OBJECTIVE
Xây dựng trang Đăng nhập (app/login/page.js): Hỗ trợ đăng nhập bằng Email và Mật khẩu, ghi nhớ đăng nhập, chuyển hướng thông minh sau khi đăng nhập (redirect query param), và component Route Guard bảo vệ các trang cá nhân.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_21_ADDRESS_VALIDATION_AI_CONSULTATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_21_ADDRESS_VALIDATION_AI_CONSULTATION.md)
> - [USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md)

## 3. CONTEXT
Nếu khách hàng chưa đăng nhập mà bấm vào "Thanh toán" hoặc "Tài khoản", hệ thống chuyển hướng đến /login?redirect=/checkout. Sau khi đăng nhập thành công, khách được tự động đưa trở lại đúng trang thanh toán đang dở dang.

## 4. PREREQUISITES
- PROMPT_063: UserContext

## 5. INPUTS
- Form credentials: email, password, rememberMe

## 6. DETAILED TASKS
1. **Xây dựng Trang Đăng Nhập Routine**:
   Thiết kế giao diện đăng nhập tối giản, logo Routine, liên kết "Quên mật khẩu?" và liên kết chuyển nhanh sang trang "Đăng ký".

2. **Xử lý Logic Đăng nhập và Chuyển hướng**:
   Gọi hàm login từ UserContext. Trích xuất searchParams.get("redirect") để chuyển hướng đúng trang đích, hoặc mặc định về /account.

3. **Xây dựng Component ProtectedRoute Guard**:
   Tạo HOC hoặc component bọc kiểm tra: nếu loading thì hiện Spinner; nếu !isAuthenticated thì chuyển hướng về /login kèm redirect path.

## 7. TECHNICAL REQUIREMENTS
- Sử dụng next/navigation: useRouter, useSearchParams
- Hỗ trợ phím Enter để submit form

## 8. INTEGRATION REQUIREMENTS
- Áp dụng ProtectedRoute cho /account/* và /checkout


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Open Redirect Vulnerability**: Xác thực redirect URL chỉ được là đường dẫn nội bộ (bắt đầu bằng /), không chuyển hướng sang domain lạ bên ngoài.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Đăng nhập với tài khoản hợp lệ thành công và chuyển đúng trang yêu cầu trước đó.
[ ] **AC-2**: Nhập sai mật khẩu hiển thị thông báo lỗi rõ ràng màu đỏ.
[ ] **AC-3**: Truy cập /account khi chưa đăng nhập bị đẩy về /login.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm thử luồng: truy cập /checkout -> bị chuyển về /login -> đăng nhập -> quay lại /checkout

## 12. EXPECTED OUTPUT
- `frontend/src/app/login/page.js`: Trang đăng nhập
- `frontend/src/components/Auth/ProtectedRoute.jsx`: Bộ bảo vệ route cá nhân

## 13. COMPLETION REPORT
- Quy trình đăng nhập và bảo vệ route hoàn thành an toàn
