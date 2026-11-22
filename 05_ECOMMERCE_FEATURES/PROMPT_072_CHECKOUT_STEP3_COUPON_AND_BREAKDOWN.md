# PROMPT 072 – CHECKOUT STEP 3: COUPON APPLICATION & REALTIME PRICE BREAKDOWN

## 1. ROLE
Frontend Financial Logic Developer

## 2. OBJECTIVE
Xây dựng Bước 3 của quy trình thanh toán: Áp dụng mã giảm giá trực tiếp tại checkout, hiển thị chi tiết bảng kê tài chính minh bạch: Tạm tính (Subtotal), Phí vận chuyển (Shipping Fee), Giảm giá voucher (Discount Amount) và Tổng thanh toán cuối cùng (Final Total).


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_21_ADDRESS_VALIDATION_AI_CONSULTATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_21_ADDRESS_VALIDATION_AI_CONSULTATION.md)
> - [USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md)

## 3. CONTEXT
Sự minh bạch về số tiền thanh toán giúp khách hàng an tâm đặt hàng. Bảng kê tài chính phải khớp từng chữ số với số tiền sẽ gửi sang cổng thanh toán VNPay.

## 4. PREREQUISITES
- PROMPT_071: Checkout Step 2
- PROMPT_041: Coupon Engine

## 5. INPUTS
- Subtotal, ShippingFee, CouponCode

## 6. DETAILED TASKS
1. **Xây dựng Bảng Kê Chi Tiết Tiền (Price Breakdown Card)**:
   Hiển thị 4 dòng rõ ràng: 1) Tiền hàng; 2) Phí vận chuyển; 3) Giảm giá khuyến mãi; 4) TỔNG CỘNG THANH TOÁN (in đậm, cỡ chữ lớn).

2. **Khung Áp Dụng / Đổi Mã Voucher tại Checkout**:
   Cho phép khách nhập mã khác hoặc chọn từ danh sách "Voucher của bạn" (như WELCOME10), kiểm tra điều kiện ngay lập tức.

3. **Hiển thị Danh Sách Thu Gọn Sản Phẩm Trong Đơn**:
   Danh sách mini các sản phẩm đang mua kèm ảnh nhỏ, tên, biến thể size/màu và số lượng.

## 7. TECHNICAL REQUIREMENTS
- Định dạng tiền tệ VNĐ thống nhất
- Toán học số học chính xác: FinalTotal = Subtotal + ShippingFee - DiscountAmount

## 8. INTEGRATION REQUIREMENTS
- Đồng bộ dữ liệu sang Step 4 Payment Selection


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Negative Total Prevention**: Tổng số tiền thanh toán không bao giờ được nhỏ hơn 0 (FinalTotal >= 0).

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Bảng kê tiền hiển thị đầy đủ và tính toán số học chính xác 100%.
[ ] **AC-2**: Áp dụng mã giảm giá cập nhật lại tổng thanh toán ngay lập tức.
[ ] **AC-3**: Danh sách sản phẩm mini hiển thị đúng các món trong giỏ hàng.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm thử tính toán: 500.000đ hàng + 30.000đ ship - 50.000đ voucher = 480.000đ

## 12. EXPECTED OUTPUT
- `frontend/src/components/Checkout/OrderSummaryBreakdown.jsx`: Bảng kê chi tiết tài chính đơn hàng

## 13. COMPLETION REPORT
- Bước 3 bảng kê chi tiết tài chính và khuyến mãi hoàn thành
