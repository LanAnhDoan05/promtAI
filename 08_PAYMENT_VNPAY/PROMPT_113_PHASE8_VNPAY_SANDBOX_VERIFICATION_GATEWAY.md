# PROMPT 113 – PHASE 08 VNPAY SANDBOX END-TO-END PAYMENT VERIFICATION GATEWAY

## 1. ROLE
Lead Payment Integration Engineer / Principal Architect

## 2. OBJECTIVE
Thực hiện kiểm thử nghiệm thu toàn diện toàn bộ phân hệ thanh toán VNPay Phase 08 trong môi trường Sandbox: Tạo URL thanh toán động -> Quét Embedded Dynamic QR -> Trả kết quả Return URL -> Nhận Webhook IPN Server-to-Server -> Kiểm tra chữ ký HMAC-SHA512 -> Trừ tồn kho thật -> Kiểm tra Idempotency chống trùng lặp, và ký duyệt Gateway 8.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_18_VNPAY_QR_AND_AI_HUMAN_HANDOFF.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_18_VNPAY_QR_AND_AI_HUMAN_HANDOFF.md)
> - [USER_MASTER_PROMPT_26_EMBEDDED_VNPAY_DYNAMIC_QR.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_26_EMBEDDED_VNPAY_DYNAMIC_QR.md)

## 3. CONTEXT
Gateway 8 là chốt chặn tài chính quan trọng bậc nhất. Hệ thống phải đảm bảo độ chính xác 100% từng đồng tiền thanh toán và an toàn bảo mật chữ ký số trước khi tiến hành kiểm thử tổng thể hệ thống.

## 4. PREREQUISITES
- PROMPT_106 đến PROMPT_112

## 5. INPUTS
- Tài khoản thẻ test VNPay Sandbox (Ngân hàng NCB)

## 6. DETAILED TASKS
1. **Kiểm thử Giao Dịch Thành Công Toàn Trình (Happy Path)**:
   Tạo đơn hàng 250.000đ -> Chọn VNPay -> Quét QR / Chuyển cổng Sandbox -> Nhập thẻ test NCB -> Nhập OTP 123456 -> Thanh toán thành công -> IPN nhận mã 00 -> Đơn hàng chuyển sang PAID.

2. **Kiểm thử Giao Dịch Thất Bại và Hủy Bỏ**:
   Mô phỏng hủy giao dịch tại cổng VNPay -> Kiểm tra hệ thống nhận mã 24 -> Trạng thái FAILED -> Tồn kho được giải phóng.

3. **Kiểm thử Tấn Công Sửa Đổi Dữ Liệu (Tampering Attack)**:
   Giả mạo thay đổi số tiền trong URL hoặc sửa chữ ký hash -> Xác minh hệ thống từ chối và cảnh báo vi phạm.

4. **Lập Báo cáo Nghiệm thu Gateway 8**:
   Xuất bản tài liệu QR_PAYMENT_E2E_TEST_REPORT.md và ký phê duyệt chuyển giao sang Phase 09 Testing & Security.

## 7. TECHNICAL REQUIREMENTS
- 100% các kịch bản thanh toán Sandbox thành công
- Bảo mật chữ ký số HMAC-SHA512 tuyệt đối

## 8. INTEGRATION REQUIREMENTS
- Mở khóa triển khai Phase 09 (Testing, Security & Quality Assurance)

## 9. SAFETY CONSTRAINTS
- ⚠️ **Quality Gate Rule**: Bất kỳ lỗi sai lệch số tiền hoặc lỗi xác thực chữ ký nào đều không được thông qua Gateway 8.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: [ ] AC-1: Luồng thanh toán VNPay Sandbox hoạt động hoàn hảo từ checkout đến xác nhận.
[ ] **AC-2**: [ ] AC-2: Webhook IPN xử lý chữ ký số chuẩn xác và trừ kho thật.
[ ] **AC-3**: [ ] AC-3: Cơ chế chống trùng lặp Idempotency hoạt động tin cậy.
[ ] **AC-4**: [ ] AC-4: Báo cáo nghiệm thu Gateway 8 được phê duyệt.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Chạy kịch bản kiểm thử thanh toán VNPay Sandbox với thẻ test ngân hàng NCB

## 12. EXPECTED OUTPUT
- `docs/QR_PAYMENT_E2E_TEST_REPORT.md`: Báo cáo nghiệm thu tích hợp cổng thanh toán VNPay

## 13. COMPLETION REPORT
- Ký duyệt Gateway 8: Cấp phép bắt đầu Phase 09 Testing & Security
