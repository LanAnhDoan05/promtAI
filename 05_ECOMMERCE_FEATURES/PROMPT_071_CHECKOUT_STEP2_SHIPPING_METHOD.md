# PROMPT 071 – CHECKOUT STEP 2: SHIPPING METHOD SELECTION & DYNAMIC DISTANCE CALCULATION

## 1. ROLE
Frontend & Logistics Integration Developer

## 2. OBJECTIVE
Xây dựng Bước 2 của quy trình thanh toán: Tự động gọi API POST /api/v1/shipping/calculate dựa trên địa chỉ đã chọn ở Bước 1 để hiển thị khoảng cách vận chuyển thực tế (km), số ngày giao hàng dự kiến, và các phương thức giao hàng (Giao Tiêu Chuẩn, Giao Hỏa Tốc).


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_21_ADDRESS_VALIDATION_AI_CONSULTATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_21_ADDRESS_VALIDATION_AI_CONSULTATION.md)
> - [USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md)

## 3. CONTEXT
Routine cung cấp biểu phí vận chuyển minh bạch dựa trên khoảng cách từ kho đến nhà khách. Khách hàng nhìn thấy rõ khoảng cách km và thời gian dự kiến nhận hàng.

## 4. PREREQUISITES
- PROMPT_070: Checkout Step 1
- PROMPT_040: Dynamic Shipping Service

## 5. INPUTS
- Tọa độ hoặc Tỉnh/Thành từ Step 1

## 6. DETAILED TASKS
1. **Tự động gọi API tính cước vận chuyển**:
   Khi người dùng chọn xong địa chỉ: gửi request tính cước, hiển thị spinner tải cước vận chuyển.

2. **Hiển thị Lựa Chọn Phương Thức Vận Chuyển**:
   Các thẻ chọn: "Giao hàng tiêu chuẩn" (ví dụ: 25.000đ - 2-3 ngày, cách kho 8.5 km), "Giao hàng hỏa tốc nội thành" (nếu < 15km).

3. **Cập nhật Phí Vận Chuyển vào Tổng Tiền Đơn Hàng**:
   Cập nhật shippingFee vào CheckoutState và cộng vào tổng số tiền thanh toán cuối cùng.

## 7. TECHNICAL REQUIREMENTS
- Hiển thị khoảng cách km làm tròn 1 chữ số thập phân
- Tự động áp dụng Miễn phí ship nếu đơn hàng đạt điều kiện Freeship

## 8. INTEGRATION REQUIREMENTS
- Kết nối giữa ShippingAddressStep và PaymentMethodStep


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Stale Shipping Fee Prevention**: Nếu khách hàng quay lại Step 1 đổi địa chỉ, phải tính toán lại phí ship ngay lập tức.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Thay đổi địa chỉ tự động cập nhật lại phí ship và khoảng cách km.
[ ] **AC-2**: Hiển thị chính xác số ngày giao hàng dự kiến.
[ ] **AC-3**: Phí ship được tính vào tổng thanh toán.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm thử với địa chỉ nội thành và địa chỉ ngoại tỉnh kiểm tra mức phí

## 12. EXPECTED OUTPUT
- `frontend/src/components/Checkout/ShippingMethodStep.jsx`: Component bước chọn phương thức vận chuyển

## 13. COMPLETION REPORT
- Bước 2 tính cước vận chuyển động theo khoảng cách hoàn thành
