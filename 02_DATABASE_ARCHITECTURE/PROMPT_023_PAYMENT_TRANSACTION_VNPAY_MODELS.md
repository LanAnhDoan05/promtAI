# PROMPT 023 – PAYMENTTRANSACTION & VNPAY AUDIT MODELS

## 1. ROLE
Payment Integration Engineer / Database Specialist

## 2. OBJECTIVE
Xây dựng mô hình dữ liệu lưu trữ lịch sử giao dịch thanh toán (PaymentTransaction) phục vụ đối soát, kiểm tra chữ ký số HMAC và lưu trace VNPay IPN.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_09_REAL_DATA_AND_BUSINESS_LOGIC.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_09_REAL_DATA_AND_BUSINESS_LOGIC.md)
> - [USER_MASTER_PROMPT_13_MYSQL_AI_ADDRESS_SHIPPING_SYNC.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_13_MYSQL_AI_ADDRESS_SHIPPING_SYNC.md)
> - [USER_MASTER_PROMPT_12_ROUTINE_VN_CATALOG_SCRAPING.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_12_ROUTINE_VN_CATALOG_SCRAPING.md)

## 3. CONTEXT
Khi khách hàng thanh toán qua cổng VNPay (URL hoặc Embedded QR), mỗi lượt thử giao dịch tạo một record PaymentTransaction lưu lại mã giao dịch ngân hàng, mã đơn hàng, số tiền, mã phản hồi (vnp_ResponseCode), trạng thái (SUCCESS, PENDING, FAILED) và raw payload để đối soát khi có khiếu nại.

## 4. PREREQUISITES
- PROMPT_022: Order, OrderItem & StockReservation Models

## 5. INPUTS
- Đặc tả kỹ thuật VNPay Gateway SDK 2.5.0

## 6. DETAILED TASKS
1. **Định nghĩa Model PaymentTransaction**:
   Bao gồm id, orderId (Int), transactionNo (String?), vnpTxnRef (String @unique), amount (Decimal(12,2)), bankCode (String?), cardType (String?), responseCode (String?), transactionStatus (String @default("PENDING")), secureHash (String?), rawResponse (Json?), createdAt, updatedAt.

2. **Thiết lập quan hệ với Order**:
   Thiết lập order Order @relation(fields: [orderId], references: [id], onDelete: Cascade). Đánh index trên vnpTxnRef, orderId, transactionStatus.

## 7. TECHNICAL REQUIREMENTS
- vnpTxnRef phải là duy nhất (@unique) để đảm bảo tính Idempotent cho Webhook IPN
- Lưu rawResponse dạng Json hoặc Text để phục vụ audit log
- Decimal(12,2) cho trường amount

## 8. INTEGRATION REQUIREMENTS
- VNPay Service và IPN Controller đọc/ghi bảng này


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Tránh Ghi Đè Giao Dịch Đã Thành Công**: Chỉ cập nhật trạng thái khi giao dịch đang PENDING, không cho phép rollback giao dịch SUCCESS nếu không qua quy trình hoàn tiền chính thức.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Model PaymentTransaction được định nghĩa đầy đủ trường trong schema.prisma.
[ ] **AC-2**: Ràng buộc unique trên vnpTxnRef hoạt động chính xác.
[ ] **AC-3**: npx prisma validate kiểm tra thành công.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Chạy npx prisma validate xác nhận cấu trúc model

## 12. EXPECTED OUTPUT
- `backend/prisma/schema.prisma`: Thêm PaymentTransaction model

## 13. COMPLETION REPORT
- Mô hình giao dịch thanh toán và đối soát VNPay sẵn sàng
