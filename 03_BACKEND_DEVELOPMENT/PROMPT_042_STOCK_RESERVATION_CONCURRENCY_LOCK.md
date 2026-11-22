# PROMPT 042 – STOCK RESERVATION & CONCURRENCY LOCK SERVICE

## 1. ROLE
Senior Backend Engineer / Concurrency Specialist

## 2. OBJECTIVE
Xây dựng cơ chế khóa giữ tồn kho tạm thời (Stock Reservation) trong 15 phút khi khách hàng chuyển sang bước thanh toán trực tuyến, và tác vụ định kỳ tự động nhả kho nếu giao dịch quá hạn.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_02_CLOUDINARY_ADMIN_PRODUCT_MANAGEMENT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_02_CLOUDINARY_ADMIN_PRODUCT_MANAGEMENT.md)
> - [USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md)
> - [USER_MASTER_PROMPT_25_PRODUCTION_UPGRADE_NOTIFICATION_HANDOFF.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_25_PRODUCTION_UPGRADE_NOTIFICATION_HANDOFF.md)

## 3. CONTEXT
Khi nhiều khách hàng cùng mua chiếc áo sơ mi size L cuối cùng và chuyển sang cổng thanh toán VNPay, nếu không có cơ chế giữ kho (Reservation), cả hai người có thể cùng thanh toán thành công dẫn đến tình trạng bán vượt tồn kho (Overselling).

## 4. PREREQUISITES
- PROMPT_022: StockReservation Model

## 5. INPUTS
- Danh sách variantId và quantity cần giữ, thời gian timeout (15 phút)

## 6. DETAILED TASKS
1. **Xây dựng StockService.reserveStock**:
   Chạy trong Prisma $transaction: Kiểm tra tồn kho khả dụng (stock - active_reserved >= requested_quantity). Tạo bản ghi StockReservation với status = "ACTIVE", expiresAt = now + 15 phút.

2. **Xây dựng StockService.commitStock**:
   Khi đơn hàng thanh toán thành công: chuyển trạng thái reservation thành "CONSUMED", đồng thời trừ trực tiếp số lượng trong ProductVariant.stock.

3. **Xây dựng StockService.releaseStock**:
   Khi khách hủy đơn hoặc giao dịch thất bại: chuyển trạng thái reservation thành "RELEASED".

4. **Tác vụ dọn dẹp giữ kho hết hạn (Cron Cleanup)**:
   Tạo hàm chạy định kỳ mỗi 5 phút quét các bản ghi StockReservation có status = "ACTIVE" và expiresAt < now để chuyển thành "RELEASED".

## 7. TECHNICAL REQUIREMENTS
- Giao dịch ACID với Prisma $transaction
- Khóa cô lập giao dịch ngăn chặn Race Condition khi thanh toán đồng thời

## 8. INTEGRATION REQUIREMENTS
- Checkout Controller gọi reserveStock; VNPay Return/IPN gọi commitStock hoặc releaseStock

## 9. SAFETY CONSTRAINTS
- ⚠️ **Overselling Protection**: Tuyệt đối không cho phép tạo reservation nếu số lượng yêu cầu vượt quá tồn kho khả dụng.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Tạo đơn hàng giữ kho thành công trong 15 phút.
[ ] **AC-2**: Sau 15 phút nếu không thanh toán, tác vụ cleanup tự động giải phóng tồn kho.
[ ] **AC-3**: Thanh toán thành công trừ trực tiếp vào tồn kho thật.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Mô phỏng 2 request đặt hàng đồng thời với số lượng tồn kho chỉ còn 1 sản phẩm

## 12. EXPECTED OUTPUT
- `backend/src/services/stockService.js`: Dịch vụ quản lý giữ và xuất tồn kho an toàn

## 13. COMPLETION REPORT
- Cơ chế giữ kho chống overselling đa luồng đã hoàn thành
