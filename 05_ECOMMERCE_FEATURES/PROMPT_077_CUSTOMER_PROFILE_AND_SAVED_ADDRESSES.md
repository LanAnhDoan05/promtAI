# PROMPT 077 – CUSTOMER PROFILE MANAGEMENT & SAVED ADDRESS BOOK CRUD

## 1. ROLE
Frontend Full-stack Developer

## 2. OBJECTIVE
Xây dựng trang Quản lý hồ sơ cá nhân và Sổ địa chỉ (app/account/profile/page.js và app/account/addresses/page.js): Cập nhật thông tin cá nhân (Họ tên, Số điện thoại, Email, Avatar), đổi mật khẩu tài khoản, và quản lý sổ địa chỉ giao hàng (Thêm, Sửa, Xóa, Đặt làm địa chỉ mặc định).


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_21_ADDRESS_VALIDATION_AI_CONSULTATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_21_ADDRESS_VALIDATION_AI_CONSULTATION.md)
> - [USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md)

## 3. CONTEXT
Khách hàng có thể quản lý nhiều địa chỉ nhận hàng (Nhà riêng, Cơ quan) để checkout tiện lợi hơn.

## 4. PREREQUISITES
- PROMPT_063: UserContext
- PROMPT_020: Address Model

## 5. INPUTS
- Thông tin Profile User và danh sách Address từ API

## 6. DETAILED TASKS
1. **Xây dựng Trang Hồ Sơ Cá Nhân (Profile Page)**:
   Form cập nhật họ tên, số điện thoại, tải lên ảnh đại diện avatar (tích hợp Cloudinary). Nút Lưu thay đổi.

2. **Xây dựng Khung Đổi Mật Khẩu**:
   Nhập mật khẩu hiện tại, mật khẩu mới, xác nhận mật khẩu mới. Kiểm tra bảo mật trước khi gửi API.

3. **Xây dựng Trang Quản Lý Sổ Địa Chỉ (Address Book)**:
   Danh sách các địa chỉ đã lưu. Nút "Thêm địa chỉ mới", nút "Sửa", nút "Xóa", và nút "Đặt làm mặc định".

## 7. TECHNICAL REQUIREMENTS
- Client validation chặt chẽ
- Cập nhật state UserContext ngay khi lưu thành công

## 8. INTEGRATION REQUIREMENTS
- Dữ liệu sổ địa chỉ tự động nạp vào Bước 1 của trang Checkout


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Old Password Verification**: Bắt buộc phải nhập đúng mật khẩu hiện tại mới cho phép đổi mật khẩu mới.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Cập nhật thông tin cá nhân thành công và phản ánh ngay lên Header.
[ ] **AC-2**: Thêm, sửa, xóa địa chỉ trong sổ địa chỉ hoạt động trơn tru.
[ ] **AC-3**: Đặt địa chỉ mặc định thành công.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm thử thêm 2 địa chỉ và đổi địa chỉ mặc định

## 12. EXPECTED OUTPUT
- `frontend/src/app/account/profile/page.js`: Trang thông tin tài khoản
- `frontend/src/app/account/addresses/page.js`: Trang sổ địa chỉ nhận hàng

## 13. COMPLETION REPORT
- Hồ sơ cá nhân và quản lý sổ địa chỉ hoàn thành
