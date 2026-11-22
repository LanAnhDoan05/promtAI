# PROMPT 112 – PAYMENT FAILURE, TIMEOUT & STOCK RELEASE ROLLBACK WORKFLOW

## 1. ROLE
Backend Reliability Engineer

## 2. OBJECTIVE
Xây dựng quy trình xử lý giao dịch thất bại và giải phóng tồn kho (Rollback Workflow): Khi khách hủy giao dịch trên cổng VNPay, thẻ không đủ tiền, hoặc quá 15 phút không thanh toán: cập nhật đơn hàng sang FAILED hoặc CANCELLED, tự động hoàn trả số lượng hàng giữ tạm trong StockReservation về trạng thái RELEASED, và gửi thông báo hỗ trợ cho khách hàng.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_18_VNPAY_QR_AND_AI_HUMAN_HANDOFF.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_18_VNPAY_QR_AND_AI_HUMAN_HANDOFF.md)
> - [USER_MASTER_PROMPT_26_EMBEDDED_VNPAY_DYNAMIC_QR.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_26_EMBEDDED_VNPAY_DYNAMIC_QR.md)

## 3. CONTEXT
Nếu không giải phóng tồn kho khi giao dịch thất bại, hàng hóa sẽ bị "giam ảo" trong kho khiến những khách hàng khác không thể mua được.

## 4. PREREQUISITES
- PROMPT_110: VNPay IPN
- PROMPT_042: Stock Reservation

## 5. INPUTS
- Order ID và mã lỗi giao dịch

## 6. DETAILED TASKS
1. **Xử lý Giao Dịch Bị Hủy / Thất Bại Tức Thì**:
   Khi nhận mã lỗi từ Return/IPN (ví dụ vnp_ResponseCode = "24"): Cập nhật Order paymentStatus = "FAILED", gọi stockService.releaseStock(orderId) giải phóng ngay các sản phẩm đang giữ.

2. **Tác Vụ Quét Định Kỳ Đơn Hàng Hết Hạn Thanh Toán (Timeout Sweeper)**:
   Chạy cronjob mỗi 10 phút: Tìm các đơn hàng PENDING tạo quá 30 phút mà chưa thanh toán, tự động chuyển orderStatus = "CANCELLED", giải phóng giữ kho và ghi chú "Hết hạn thanh toán".

3. **Giao Diện Hướng Dẫn Thử Lại Thanh Toán Cho Khách**:
   Trên trang kết quả thất bại: Hiển thị lý do thất bại và nút "Thanh toán lại" hoặc "Đổi sang phương thức COD" tiện lợi.

## 7. TECHNICAL REQUIREMENTS
- Giải phóng kho an toàn trong transaction
- Cronjob chạy ngầm nhẹ nhàng không khóa bảng

## 8. INTEGRATION REQUIREMENTS
- Frontend Payment Result page và Backend Stock Service


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Premature Release Prevention**: Không giải phóng kho của đơn hàng nếu chưa hết thời gian chờ thanh toán 15 phút.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Khách hủy thanh toán VNPay thì tồn kho sản phẩm lập tức khả dụng trở lại cho khách khác.
[ ] **AC-2**: Đơn hàng quá hạn được tự động dọn dẹp và hủy an toàn.
[ ] **AC-3**: Khách hàng có thể bấm thanh toán lại đơn hàng dễ dàng.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Tạo đơn hàng VNPay, mô phỏng hủy thanh toán và kiểm tra tồn kho khả dụng

## 12. EXPECTED OUTPUT
- `backend/src/services/paymentRollbackService.js`: Dịch vụ xử lý hoàn tác thanh toán thất bại

## 13. COMPLETION REPORT
- Quy trình xử lý thanh toán thất bại và giải phóng tồn kho hoàn thành
