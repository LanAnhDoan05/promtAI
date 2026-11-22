# PROMPT 070 – CHECKOUT STEP 1: SHIPPING ADDRESS SELECTION, COORDINATE PINNING & PROVINCE API

## 1. ROLE
Senior Frontend Engineer / Geolocation Specialist

## 2. OBJECTIVE
Xây dựng Bước 1 của quy trình thanh toán (Checkout Step 1): Chọn địa chỉ nhận hàng có sẵn trong sổ địa chỉ hoặc thêm địa chỉ mới, dropdown Tỉnh/Thành, Quận/Huyện, Phường/Xã chuẩn Việt Nam, hỗ trợ định vị tọa độ (Latitude, Longitude) tự động để phục vụ tính phí ship chính xác.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_21_ADDRESS_VALIDATION_AI_CONSULTATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_21_ADDRESS_VALIDATION_AI_CONSULTATION.md)
> - [USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md)

## 3. CONTEXT
Địa chỉ nhận hàng chính xác là điều kiện tiên quyết để giao hàng thành công và tính phí vận chuyển động. Khách hàng đã đăng nhập có thể chọn nhanh từ sổ địa chỉ; khách vãng lai điền thông tin trực tiếp.

## 4. PREREQUISITES
- PROMPT_068: Cart Page
- PROMPT_040: Dynamic Shipping Service

## 5. INPUTS
- Sổ địa chỉ của User hoặc Form địa chỉ mới

## 6. DETAILED TASKS
1. **Xây dựng Danh Sách Sổ Địa Chỉ Đã Lưu**:
   Khách hàng có thể chọn 1 trong các địa chỉ đã lưu (hiển thị radio card), có huy hiệu "Mặc định". Nút "Thêm địa chỉ mới".

2. **Form Nhập Địa Chỉ Mới với Dropdown 3 cấp**:
   Tích hợp danh mục hành chính Việt Nam: Tỉnh/Thành phố -> Quận/Huyện -> Phường/Xã (tự động lọc cấp dưới khi chọn cấp trên).

3. **Cơ chế Tự động Ghim Tọa độ Địa lý**:
   Sử dụng Geocoding hoặc bảng tọa độ hành chính chuẩn để tự động gán latitude/longitude khi khách chọn địa chỉ, làm tham số tính khoảng cách km.

## 7. TECHNICAL REQUIREMENTS
- Validate bắt buộc: Tên người nhận, Số điện thoại (10 chữ số), Địa chỉ chi tiết
- Tọa độ số thực Float lưu chuẩn xác

## 8. INTEGRATION REQUIREMENTS
- Lưu selectedAddress vào CheckoutState và truyền sang Step 2


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Phone Number Regex**: Kiểm tra số điện thoại đúng đầu số nhà mạng Việt Nam (03, 05, 07, 08, 09).

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Chọn địa chỉ có sẵn cập nhật ngay tọa độ và thông tin giao hàng.
[ ] **AC-2**: Thêm địa chỉ mới lưu thành công vào cơ sở dữ liệu.
[ ] **AC-3**: Tọa độ được tính toán và truyền thành công sang bộ tính cước vận chuyển.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm thử nhập địa chỉ tại TP. Hồ Chí Minh và kiểm tra tọa độ tương ứng

## 12. EXPECTED OUTPUT
- `frontend/src/components/Checkout/ShippingAddressStep.jsx`: Component bước chọn địa chỉ giao hàng

## 13. COMPLETION REPORT
- Bước 1 chọn địa chỉ nhận hàng và tọa độ địa lý hoàn thành
