# PROMPT 022 – ORDER, ORDERITEM & STOCKRESERVATION MODELS WITH ACID CONCURRENCY

## 1. ROLE
Database Architect / Senior Transaction Engineer

## 2. OBJECTIVE
Xây dựng mô hình dữ liệu Đơn hàng (Order), Chi tiết đơn hàng (OrderItem) và Khóa giữ tồn kho tạm thời (StockReservation) hỗ trợ giao dịch ACID.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_09_REAL_DATA_AND_BUSINESS_LOGIC.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_09_REAL_DATA_AND_BUSINESS_LOGIC.md)
> - [USER_MASTER_PROMPT_13_MYSQL_AI_ADDRESS_SHIPPING_SYNC.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_13_MYSQL_AI_ADDRESS_SHIPPING_SYNC.md)
> - [USER_MASTER_PROMPT_12_ROUTINE_VN_CATALOG_SCRAPING.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_12_ROUTINE_VN_CATALOG_SCRAPING.md)

## 3. CONTEXT
Đơn hàng thương mại điện tử cần theo dõi trạng thái vòng đời (PENDING, CONFIRMED, PROCESSING, SHIPPING, DELIVERED, CANCELLED), số tiền tổng, phí ship, giảm giá, và thông tin người nhận. StockReservation đảm bảo khi khách chuyển sang cổng thanh toán thì hàng trong kho được giữ trong 15 phút tránh overselling.

## 4. PREREQUISITES
- PROMPT_021: Category, Product & ProductVariant Models

## 5. INPUTS
- Quy trình nghiệp vụ đặt hàng và quản trị kho của Routine

## 6. DETAILED TASKS
1. **Định nghĩa Model Order**:
   Bao gồm id, orderCode (String @unique), userId (Int?), customerName, customerPhone, customerEmail, shippingAddress, province, district, ward, subtotal (Decimal), shippingFee (Decimal), discountAmount (Decimal @default(0)), totalAmount (Decimal), paymentMethod (COD, VNPAY, BANKING), paymentStatus (PENDING, PAID, FAILED, REFUNDED), orderStatus (PENDING, CONFIRMED, SHIPPING, DELIVERED, CANCELLED), note, couponCode, createdAt, updatedAt.

2. **Định nghĩa Model OrderItem**:
   Bao gồm id, orderId (Int), productId (Int), variantId (Int), productName, color, size, sku, quantity (Int), price (Decimal), totalPrice (Decimal), image, createdAt.

3. **Định nghĩa Model StockReservation**:
   Bao gồm id, orderId (Int?), variantId (Int), quantity (Int), expiresAt (DateTime), status (ACTIVE, CONSUMED, RELEASED), createdAt.

## 7. TECHNICAL REQUIREMENTS
- OrderCode định dạng mã duy nhất dạng ROUTINE-YYYYMMDD-XXXXX
- Quan hệ Order -> OrderItem (Cascade Delete hoặc Restrict)
- Index trên orderCode, userId, orderStatus, paymentStatus, createdAt
- Index trên StockReservation (variantId, status, expiresAt)

## 8. INTEGRATION REQUIREMENTS
- Liên kết với PaymentTransaction và ProductVariant

## 9. SAFETY CONSTRAINTS
- ⚠️ **ACID Transaction Guarantee**: Mọi thao tác tạo đơn và trừ/giữ kho phải nằm trong $transaction.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Models Order, OrderItem, StockReservation được thêm vào schema.prisma.
[ ] **AC-2**: Quan hệ khóa ngoại chính xác, kiểu tiền tệ chuẩn Decimal(12,2).
[ ] **AC-3**: npx prisma validate kiểm tra thành công.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm tra cú pháp schema.prisma bằng npx prisma validate

## 12. EXPECTED OUTPUT
- `backend/prisma/schema.prisma`: Thêm Order, OrderItem, StockReservation models

## 13. COMPLETION REPORT
- Đã định nghĩa toàn bộ mô hình đơn hàng và cơ chế giữ kho an toàn
