# PROMPT 074 – ORDER SUBMISSION, STOCK LOCK & ORDER CREATION SERVICE INTEGRATION

## 1. ROLE
Full-stack Integration Engineer

## 2. OBJECTIVE
Xây dựng luồng Gửi đơn hàng (Submit Order): Khóa nút đặt hàng chống bấm đúp, gửi request POST /api/v1/orders tạo đơn hàng trong database, kích hoạt giữ tồn kho (Stock Lock), dọn sạch giỏ hàng và điều hướng thông minh (nếu COD chuyển sang trang Xác nhận đơn hàng, nếu VNPay chuyển sang luồng thanh toán VNPay).


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_21_ADDRESS_VALIDATION_AI_CONSULTATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_21_ADDRESS_VALIDATION_AI_CONSULTATION.md)
> - [USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md)

## 3. CONTEXT
Khoảnh khắc bấm nút "ĐẶT HÀNG" là thao tác then chốt nhất. Hệ thống cần bảo đảm tính toàn vẹn dữ liệu, hiển thị overlay loading chuyên nghiệp và xử lý phản hồi chính xác.

## 4. PREREQUISITES
- PROMPT_073: Checkout Step 4
- PROMPT_043: Order Service

## 5. INPUTS
- Toàn bộ CheckoutState: items, shippingAddress, shippingFee, couponCode, paymentMethod, notes

## 6. DETAILED TASKS
1. **Xây dựng Hàm handleSubmitOrder**:
   Kiểm tra toàn bộ tính hợp lệ của dữ liệu. Bật trạng thái submitting (hiện nút quay tròn, khóa mọi tương tác).

2. **Gửi API Tạo Đơn Hàng đến Backend**:
   Gửi POST /api/v1/orders. Backend chạy transaction: tạo Order, OrderItem, StockReservation, tăng lượt dùng Coupon, xóa Cart.

3. **Điều Hướng Theo Phương Thức Thanh Toán**:
   Nếu paymentMethod === "COD": làm sạch giỏ hàng, chuyển hướng tới /order-success?code=ROUTINE-XXXXX. Nếu paymentMethod === "VNPAY": chuyển tiếp sang bước hiển thị Embedded VNPay QR hoặc chuyển hướng URL cổng thanh toán.

## 7. TECHNICAL REQUIREMENTS
- Chống double submission bằng cờ isSubmitting
- Xóa giỏ hàng trên CartContext ngay sau khi tạo đơn thành công

## 8. INTEGRATION REQUIREMENTS
- Checkout Page, OrderService Backend, CartContext


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Out of Stock on Submit**: Nếu trong lúc khách đang checkout mà sản phẩm bị người khác mua hết, hiển thị thông báo lỗi hết hàng và cập nhật lại giỏ mà không tạo đơn rác.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Bấm Đặt hàng tạo thành công bản ghi Order trong cơ sở dữ liệu.
[ ] **AC-2**: Đơn hàng COD chuyển hướng thành công đến trang Xác nhận đơn hàng.
[ ] **AC-3**: Giỏ hàng được dọn sạch sau khi đặt hàng thành công.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm thử đặt đơn hàng COD từ đầu đến cuối và kiểm tra database

## 12. EXPECTED OUTPUT
- `frontend/src/app/checkout/page.js`: Trang Checkout tổng hợp 4 bước

## 13. COMPLETION REPORT
- Quy trình tạo đơn hàng và khóa tồn kho đã hoàn thành
