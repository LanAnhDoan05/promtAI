# PROMPT 109 – VNPAY RETURN URL (`VNPAY-RETURN`) CONSUMER ENDPOINT & RESULT PAGE

## 1. ROLE
Backend API & Frontend Developer

## 2. OBJECTIVE
Xây dựng endpoint xử lý kết quả trả về từ cổng VNPay khi khách hàng hoàn tất thanh toán trên trình duyệt: GET /api/v1/payment/vnpay-return và trang giao diện hiển thị kết quả thanh toán (/payment-result): Kiểm tra chữ ký vnp_SecureHash, hiển thị thông báo Thành công / Thất bại, mã giao dịch ngân hàng và nút quay về đơn hàng.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_18_VNPAY_QR_AND_AI_HUMAN_HANDOFF.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_18_VNPAY_QR_AND_AI_HUMAN_HANDOFF.md)
> - [USER_MASTER_PROMPT_26_EMBEDDED_VNPAY_DYNAMIC_QR.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_26_EMBEDDED_VNPAY_DYNAMIC_QR.md)

## 3. CONTEXT
Sau khi khách hàng thanh toán trên cổng VNPay hoặc app ngân hàng, trình duyệt sẽ được chuyển hướng về trang Return URL của website Routine để thông báo kết quả cho khách.

## 4. PREREQUISITES
- PROMPT_107: Dynamic VNPay URL
- PROMPT_075: Order Confirmation

## 5. INPUTS
- Các tham số query trả về từ VNPay: vnp_ResponseCode, vnp_TxnRef, vnp_TransactionNo, vnp_SecureHash, ...

## 6. DETAILED TASKS
1. **Backend Endpoint GET /api/v1/payment/vnpay-return**:
   Trích xuất toàn bộ query params, tách riêng vnp_SecureHash, sắp xếp lại các tham số còn lại và băm HMAC-SHA512 để so khớp chữ ký. Nếu chữ ký sai, báo lỗi gian lận.

2. **Kiểm tra Mã Phản Hồi (vnp_ResponseCode)**:
   Nếu vnp_ResponseCode === "00": Giao dịch thành công. Cập nhật Order paymentStatus = "PAID", orderStatus = "CONFIRMED". Nếu khác "00": Giao dịch thất bại (khách hủy, số dư không đủ...).

3. **Xây dựng Trang Giao Diện Kết Quả Thanh Toán (/payment-result)**:
   Hiển thị: Icon thành công (xanh) hoặc thất bại (đỏ), Tên ngân hàng, Số tiền, Mã giao dịch VNPay, Lời cảm ơn và nút "Xem chi tiết đơn hàng".

## 7. TECHNICAL REQUIREMENTS
- Xác thực chữ ký số 100% trước khi xử lý dữ liệu
- Hỗ trợ chuyển tiếp an toàn từ backend sang frontend

## 8. INTEGRATION REQUIREMENTS
- Frontend app/payment-result/page.js


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Relying Solely on Return URL**: Return URL chỉ dùng để hiển thị giao diện cho khách; việc cập nhật trạng thái tài chính cốt lõi PHẢI dựa vào Webhook IPN để tránh trường hợp khách tắt trình duyệt giữa chừng.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Giao diện hiển thị đúng kết quả thành công với mã 00.
[ ] **AC-2**: Hiển thị lý do thất bại rõ ràng nếu mã lỗi khác 00.
[ ] **AC-3**: Chữ ký sai bị phát hiện và cảnh báo ngay lập tức.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm thử mở Return URL với mã 00 (thành công) và mã 24 (khách hủy giao dịch)

## 12. EXPECTED OUTPUT
- `backend/src/controllers/paymentController.js`: Hàm xử lý vnpayReturn
- `frontend/src/app/payment-result/page.js`: Trang kết quả thanh toán

## 13. COMPLETION REPORT
- Endpoint tiếp nhận Return URL và trang kết quả thanh toán VNPay hoàn thành
