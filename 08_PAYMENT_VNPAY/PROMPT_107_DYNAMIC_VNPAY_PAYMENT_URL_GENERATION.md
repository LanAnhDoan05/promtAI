# PROMPT 107 – DYNAMIC VNPAY PAYMENT URL GENERATION WITH HMAC-SHA512 CHECKSUM

## 1. ROLE
Payment Integration Engineer

## 2. OBJECTIVE
Xây dựng API tạo URL thanh toán động: POST /api/v1/payment/create-payment-url nhận { orderId, bankCode, language }. Thực hiện sắp xếp từ điển (Alphabetical Sort) các tham số vnp_*, tạo chuỗi dữ liệu ký (signData), tính toán vnp_SecureHash và ghép thành URL chuyển hướng chính thức tới cổng VNPay.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_18_VNPAY_QR_AND_AI_HUMAN_HANDOFF.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_18_VNPAY_QR_AND_AI_HUMAN_HANDOFF.md)
> - [USER_MASTER_PROMPT_26_EMBEDDED_VNPAY_DYNAMIC_QR.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_26_EMBEDDED_VNPAY_DYNAMIC_QR.md)

## 3. CONTEXT
Khi khách hàng chọn thanh toán qua VNPay và bấm Đặt hàng, hệ thống cần sinh một URL thanh toán có chữ ký số hợp lệ trong vòng chưa đầy 50ms để khách hàng chuyển tiếp sang giao diện thanh toán của ngân hàng.

## 4. PREREQUISITES
- PROMPT_106: VNPay Config
- PROMPT_043: Order Service

## 5. INPUTS
- orderId, amount (số tiền VNĐ nhân 100 theo quy định VNPay), ipAddr, locale

## 6. DETAILED TASKS
1. **Thu thập và Chuẩn hóa Tham số VNPay**:
   Tạo đối tượng tham số: vnp_Version="2.1.0", vnp_Command="pay", vnp_TmnCode, vnp_Amount=amount*100, vnp_CurrCode="VND", vnp_TxnRef=orderCode, vnp_OrderInfo="Thanh toan don hang Routine " + orderCode, vnp_OrderType="billpayment", vnp_Locale=locale||"vn", vnp_ReturnUrl, vnp_IpAddr, vnp_CreateDate=YYYYMMDDHHmmss.

2. **Thuật toán Sắp xếp Từ điển (Alphabetical Key Sort)**:
   Sắp xếp tất cả các key theo thứ tự a-z, mã hóa URI component (encodeURIComponent) đúng chuẩn trước khi ghép chuỗi signData.

3. **Tạo Chữ Ký Số và Trả Về URL Thanh Toán**:
   Băm chuỗi bằng HMAC-SHA512 với HashSecret, gắn thêm &vnp_SecureHash=... và lưu một bản ghi PaymentTransaction status = "PENDING". Trả về JSON { success: true, paymentUrl: "..." }.

## 7. TECHNICAL REQUIREMENTS
- Quy tắc VNPay: vnp_Amount phải nhân với 100 (ví dụ 100.000đ gửi 10000000)
- Thời gian tạo URL < 30ms

## 8. INTEGRATION REQUIREMENTS
- Frontend Checkout gọi API này khi khách chọn thanh toán VNPay

## 9. SAFETY CONSTRAINTS
- ⚠️ **Amount Tampering Prevention**: Số tiền amount PHẢI được lấy từ bản ghi Order trong cơ sở dữ liệu, tuyệt đối không lấy từ body của request client gửi lên.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: API trả về paymentUrl hợp lệ bắt đầu bằng https://sandbox.vnpayment.vn/...
[ ] **AC-2**: Chữ ký vnp_SecureHash khớp với thuật toán kiểm tra của VNPay.
[ ] **AC-3**: Bản ghi PaymentTransaction được tạo với trạng thái PENDING.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Gọi POST /api/v1/payment/create-payment-url với đơn hàng mẫu và mở URL trên trình duyệt

## 12. EXPECTED OUTPUT
- `backend/src/services/vnpayService.js`: Dịch vụ sinh URL thanh toán VNPay
- `backend/src/controllers/paymentController.js`: Controller thanh toán

## 13. COMPLETION REPORT
- API tạo URL thanh toán VNPay động kèm chữ ký số an toàn hoàn thành
