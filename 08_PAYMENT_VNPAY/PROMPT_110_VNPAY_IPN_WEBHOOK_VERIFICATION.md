# PROMPT 110 – VNPAY INSTANT PAYMENT NOTIFICATION (`VNPAY-IPN`) WEBHOOK & CHECKSUM VERIFICATION

## 1. ROLE
Payment Security Engineer / Senior Backend Architect

## 2. OBJECTIVE
Xây dựng webhook xử lý thông báo thanh toán tức thì Server-to-Server từ máy chủ VNPay: GET /api/v1/payment/vnpay-ipn: Kiểm tra chữ ký số HMAC-SHA512, kiểm tra sự tồn tại của đơn hàng, kiểm tra tính đúng đắn của số tiền thanh toán (vnp_Amount == order.totalAmount * 100), kiểm tra trạng thái đơn hàng (chưa được thanh toán trước đó), cập nhật trạng thái đơn hàng sang PAID trong transaction và trả về mã phản hồi chuẩn VNPay ({ RspCode: "00", Message: "Confirm Success" }).


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_18_VNPAY_QR_AND_AI_HUMAN_HANDOFF.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_18_VNPAY_QR_AND_AI_HUMAN_HANDOFF.md)
> - [USER_MASTER_PROMPT_26_EMBEDDED_VNPAY_DYNAMIC_QR.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_26_EMBEDDED_VNPAY_DYNAMIC_QR.md)

## 3. CONTEXT
IPN là cơ chế thanh toán tin cậy nhất giữa máy chủ VNPay và Routine. Kể cả khi khách hàng bị mất mạng, tắt máy tính ngay sau khi quét QR, VNPay vẫn gọi ngầm vào endpoint IPN này để xác nhận tiền đã về tài khoản.

## 4. PREREQUISITES
- PROMPT_106: VNPay Config
- PROMPT_042: Stock Reservation

## 5. INPUTS
- Query params do máy chủ VNPay gửi tới endpoint IPN

## 6. DETAILED TASKS
1. **Xác Thực Chữ Ký Số Checksum**:
   Lấy toàn bộ query, sắp xếp a-z, loại bỏ vnp_SecureHash và vnp_SecureHashType, tính HMAC-SHA512. Nếu hash tính được != vnp_SecureHash: trả về { RspCode: "97", Message: "Checksum failed" }.

2. **Kiểm Tra Sự Tồn Tại Đơn Hàng và Số Tiền (Amount Match)**:
   Tìm đơn hàng theo vnp_TxnRef. Nếu không thấy: trả về { RspCode: "01", Message: "Order not found" }. So sánh: parseInt(vnp_Amount) === Math.round(order.totalAmount * 100). Nếu không khớp: trả về { RspCode: "04", Message: "Amount invalid" }.

3. **Kiểm Tra Trạng Thái Đơn Hàng (Idempotency Check)**:
   Nếu đơn hàng đã có paymentStatus === "PAID": trả về { RspCode: "02", Message: "Order already confirmed" }.

4. **Cập Nhật Trạng Thái Giao Dịch và Trừ Kho Bằng Transaction**:
   Chạy trong Prisma $transaction: Cập nhật Order paymentStatus = "PAID", orderStatus = "CONFIRMED"; Cập nhật PaymentTransaction sang SUCCESS; Gọi stockService.commitStock(orderId) chuyển tồn kho từ giữ tạm sang trừ thật.

## 7. TECHNICAL REQUIREMENTS
- Tuyệt đối tuân thủ bảng mã RspCode của VNPay: "00", "01", "02", "04", "97"
- Xử lý Idempotent 100% chống xử lý trùng lặp khi VNPay gửi lại IPN nhiều lần

## 8. INTEGRATION REQUIREMENTS
- Endpoint công khai được đăng ký với VNPay Merchant Portal

## 9. SAFETY CONSTRAINTS
- ⚠️ **Financial Integrity Lock**: Không bao giờ xác nhận đơn hàng nếu số tiền thanh toán trong IPN nhỏ hơn số tiền của đơn hàng.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Webhook IPN xử lý và trả về RspCode: "00" cho giao dịch hợp lệ.
[ ] **AC-2**: Tồn kho được trừ chính xác vào kho thật khi IPN xác nhận.
[ ] **AC-3**: Chữ ký sai lập tức bị từ chối với mã 97.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Mô phỏng gọi webhook IPN với checksum hợp lệ và kiểm tra trạng thái đơn hàng trong database

## 12. EXPECTED OUTPUT
- `backend/src/controllers/paymentController.js`: Hàm xử lý vnpayIpn hoàn chỉnh

## 13. COMPLETION REPORT
- Webhook VNPay IPN xử lý chữ ký số và đối soát giao dịch an toàn hoàn thành
