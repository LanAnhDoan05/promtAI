# PROMPT 111 – PAYMENT IDEMPOTENCY, TRANSACTION LOGGING & RECONCILIATION SERVICE

## 1. ROLE
Senior Payment & Database Architect

## 2. OBJECTIVE
Xây dựng cơ chế chống trùng lặp giao dịch (Payment Idempotency), lưu vết toàn bộ raw payload lịch sử giao dịch thanh toán vào bảng PaymentTransaction, và xây dựng API đối soát giao dịch định kỳ cho kế toán Routine.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_18_VNPAY_QR_AND_AI_HUMAN_HANDOFF.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_18_VNPAY_QR_AND_AI_HUMAN_HANDOFF.md)
> - [USER_MASTER_PROMPT_26_EMBEDDED_VNPAY_DYNAMIC_QR.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_26_EMBEDDED_VNPAY_DYNAMIC_QR.md)

## 3. CONTEXT
Các sự cố mạng có thể khiến máy chủ thanh toán gửi lại thông báo nhiều lần hoặc người dùng bấm F5 liên tục. Cơ chế Idempotency đảm bảo dù nhận 10 request giống nhau, hệ thống chỉ trừ tiền và ghi nhận đơn hàng đúng 1 lần duy nhất.

## 4. PREREQUISITES
- PROMPT_110: VNPay IPN Webhook

## 5. INPUTS
- vnp_TxnRef, vnp_TransactionNo, raw payload

## 6. DETAILED TASKS
1. **Đảm Bảo Tính Nguyên Tử bằng Khóa Độc Quyền (Mutex Lock)**:
   Sử dụng database row-level locking hoặc unique constraint trên vnpTxnRef để ngăn chặn 2 thread xử lý IPN đồng thời cùng một lúc.

2. **Ghi Toàn Bộ Lịch Sử Payload vào PaymentTransaction**:
   Lưu transactionNo, bankCode, cardType, secureHash, rawResponse dạng JSON để phục vụ đối soát khi có tranh chấp.

3. **Xây dựng API Đối Soát Giao Dịch (Reconciliation API)**:
   GET /api/v1/admin/payments/reconcile: Lọc các giao dịch thành công trong ngày, tính tổng tiền đối soát với sao kê ngân hàng.

## 7. TECHNICAL REQUIREMENTS
- Unique index trên vnpTxnRef
- Audit trail đầy đủ phục vụ thanh tra tài chính

## 8. INTEGRATION REQUIREMENTS
- Admin Portal module Kế toán / Thanh toán


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Double Credit Prevention**: Tuyệt đối không tăng doanh thu hoặc trừ kho 2 lần cho cùng một mã giao dịch.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Gửi 5 request IPN trùng lặp chỉ có request đầu tiên xử lý thay đổi dữ liệu, các request sau nhận mã 02.
[ ] **AC-2**: Bảng PaymentTransaction lưu trữ đầy đủ chi tiết mọi lần thử thanh toán.
[ ] **AC-3**: Báo cáo đối soát khớp 100% với số tiền thực tế.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Mô phỏng gửi đồng thời 3 request IPN cùng 1 mã giao dịch

## 12. EXPECTED OUTPUT
- `backend/src/services/paymentReconciliationService.js`: Dịch vụ đối soát thanh toán

## 13. COMPLETION REPORT
- Cơ chế Idempotency và đối soát giao dịch thanh toán hoàn thành
