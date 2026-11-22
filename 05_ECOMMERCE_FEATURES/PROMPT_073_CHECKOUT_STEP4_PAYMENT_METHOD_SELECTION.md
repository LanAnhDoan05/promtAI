# PROMPT 073 – CHECKOUT STEP 4: PAYMENT METHOD SELECTION (COD, BANK TRANSFER, VNPAY)

## 1. ROLE
Frontend Payment UI Developer

## 2. OBJECTIVE
Xây dựng Bước 4 của quy trình thanh toán: Lựa chọn phương thức thanh toán: 1) Thanh toán khi nhận hàng (COD); 2) Chuyển khoản ngân hàng (VietQR); 3) Thanh toán trực tuyến qua VNPAY (Thẻ ATM nội địa, Thẻ quốc tế Visa/Master, VNPAY QR).


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_21_ADDRESS_VALIDATION_AI_CONSULTATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_21_ADDRESS_VALIDATION_AI_CONSULTATION.md)
> - [USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md)

## 3. CONTEXT
Khách hàng có nhiều lựa chọn thanh toán linh hoạt. Giao diện làm nổi bật các ưu đãi khi thanh toán qua VNPay và hướng dẫn chi tiết cho từng phương thức.

## 4. PREREQUISITES
- PROMPT_072: Checkout Step 3

## 5. INPUTS
- Danh sách các phương thức thanh toán được hỗ trợ

## 6. DETAILED TASKS
1. **Xây dựng Danh Sách Radio Phương Thức Thanh Toán**:
   1) COD (Thanh toán tiền mặt khi nhận hàng); 2) Chuyển khoản ngân hàng (Hiển thị số tài khoản và cú pháp chuyển khoản); 3) VNPAY (Cổng thanh toán điện tử an toàn, hỗ trợ quét mã QR và thẻ ngân hàng).

2. **Xử lý Hiển thị Chi Tiết theo Phương Thức Được Chọn**:
   Khi chọn VNPAY: Hiển thị logo các ngân hàng và lưu ý khách hàng chuẩn bị ứng dụng ngân hàng hoặc thẻ.

3. **Ô Nhập Ghi Chú Đơn Hàng (Order Notes)**:
   Ô textarea để khách ghi chú cho shipper (ví dụ: "Giao giờ hành chính", "Gọi trước khi giao").

## 7. TECHNICAL REQUIREMENTS
- Lưu selectedPaymentMethod vào CheckoutState (mặc định COD hoặc VNPAY)

## 8. INTEGRATION REQUIREMENTS
- Truyền phương thức thanh toán sang bước Đặt Hàng (Submit Order)


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Method Selection Mandatory**: Bắt buộc khách hàng phải chọn 1 phương thức thanh toán trước khi kích hoạt nút Đặt hàng.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Khách hàng chuyển đổi qua lại giữa COD, Chuyển khoản, VNPay dễ dàng.
[ ] **AC-2**: Ghi chú đơn hàng được lưu lại đầy đủ.
[ ] **AC-3**: Phương thức thanh toán được chọn được truyền chính xác vào payload tạo đơn.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm thử chọn từng phương thức và kiểm tra state tương ứng

## 12. EXPECTED OUTPUT
- `frontend/src/components/Checkout/PaymentMethodStep.jsx`: Component chọn phương thức thanh toán

## 13. COMPLETION REPORT
- Bước 4 lựa chọn phương thức thanh toán hoàn thành
