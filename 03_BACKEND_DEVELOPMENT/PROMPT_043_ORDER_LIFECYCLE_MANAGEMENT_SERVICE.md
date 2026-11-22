# PROMPT 043 – ORDER LIFECYCLE MANAGEMENT (PENDING, CONFIRMED, SHIPPED, DELIVERED, CANCELLED)

## 1. ROLE
Senior Full-stack Engineer / E-commerce Specialist

## 2. OBJECTIVE
Xây dựng toàn bộ máy trạng thái vòng đời đơn hàng (Order State Machine): Tạo đơn, xác nhận, đóng gói, giao hàng, hoàn thành, hủy đơn và hoàn trả tồn kho.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_02_CLOUDINARY_ADMIN_PRODUCT_MANAGEMENT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_02_CLOUDINARY_ADMIN_PRODUCT_MANAGEMENT.md)
> - [USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md)
> - [USER_MASTER_PROMPT_25_PRODUCTION_UPGRADE_NOTIFICATION_HANDOFF.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_25_PRODUCTION_UPGRADE_NOTIFICATION_HANDOFF.md)

## 3. CONTEXT
Đơn hàng là trung tâm của sàn thương mại điện tử. Quá trình xử lý đơn hàng phải chuyển dịch trạng thái theo sơ đồ hợp lệ (ví dụ: Không thể chuyển từ CANCELLED sang DELIVERED), đồng thời đồng bộ trạng thái thanh toán và thông báo đến người dùng.

## 4. PREREQUISITES
- PROMPT_022: Order Model
- PROMPT_042: Stock Reservation Service

## 5. INPUTS
- Order ID và trạng thái mới

## 6. DETAILED TASKS
1. **Xây dựng State Machine chuyển dịch trạng thái đơn hàng**:
   Định nghĩa ma trận chuyển đổi hợp lệ: PENDING -> [CONFIRMED, CANCELLED], CONFIRMED -> [PROCESSING, CANCELLED], PROCESSING -> [SHIPPING], SHIPPING -> [DELIVERED, CANCELLED]. Ngăn chặn mọi chuyển dịch bất hợp lệ.

2. **Xây dựng OrderService.createOrder**:
   Tạo mã đơn duy nhất ROUTINE-YYYYMMDD-XXXXX, nạp phí ship, mã giảm giá, kiểm tra tồn kho, tạo Order, OrderItems và dọn sạch giỏ hàng trong 1 transaction.

3. **Xây dựng OrderService.updateOrderStatus**:
   Cập nhật trạng thái đơn hàng, nếu CANCELLED thì hoàn trả tồn kho; tạo bản ghi Notification cho khách hàng.

4. **Cung cấp API Tra cứu Đơn hàng**:
   GET /api/v1/orders (danh sách đơn của tôi), GET /api/v1/orders/:orderCode (chi tiết đơn theo mã).

## 7. TECHNICAL REQUIREMENTS
- Prisma transaction nguyên tử
- Tự động sinh mã đơn hàng không trùng lặp
- Gửi sự kiện SSE realtime khi trạng thái đơn hàng thay đổi

## 8. INTEGRATION REQUIREMENTS
- Frontend Checkout, Order Success, Order History và Admin Order Manager

## 9. SAFETY CONSTRAINTS
- ⚠️ **Double Cancellation**: Không hoàn trả tồn kho 2 lần nếu đơn hàng đã bị hủy trước đó.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Tạo đơn hàng thành công lưu đầy đủ chi tiết sản phẩm, phí ship, giảm giá.
[ ] **AC-2**: Chuyển trạng thái đơn hàng tuân thủ đúng quy tắc state machine.
[ ] **AC-3**: Hủy đơn hàng tự động hoàn lại số lượng tồn kho cho các biến thể.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm thử tạo đơn hàng COD và hủy đơn kiểm tra hoàn trả kho

## 12. EXPECTED OUTPUT
- `backend/src/services/orderService.js`: Dịch vụ xử lý vòng đời đơn hàng
- `backend/src/controllers/orderController.js`: Controller quản lý đơn hàng
- `backend/src/routes/orderRoutes.js`: Định tuyến API đơn hàng

## 13. COMPLETION REPORT
- Máy trạng thái vòng đời đơn hàng Routine đã hoàn thành
