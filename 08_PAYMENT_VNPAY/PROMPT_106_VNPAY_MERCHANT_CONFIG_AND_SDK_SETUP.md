# PROMPT 106 – VNPAY MERCHANT CREDENTIALS, ENVIRONMENT CONFIGURATION & SDK 2.5.0 SETUP

## 1. ROLE
Payment Systems Architect / Senior Backend Engineer

## 2. OBJECTIVE
Cấu hình thông số tích hợp cổng thanh toán VNPay SDK 2.5.0 trong backend/.env: vnp_TmnCode (Mã định danh Merchant), vnp_HashSecret (Chuỗi bí mật tạo chữ ký HMAC-SHA512), vnp_Url (Endpoint Sandbox / Production), vnp_ReturnUrl (URL trả kết quả cho khách hàng), và xây dựng module vnpayConfig.js chuẩn hóa.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_18_VNPAY_QR_AND_AI_HUMAN_HANDOFF.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_18_VNPAY_QR_AND_AI_HUMAN_HANDOFF.md)
> - [USER_MASTER_PROMPT_26_EMBEDDED_VNPAY_DYNAMIC_QR.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_26_EMBEDDED_VNPAY_DYNAMIC_QR.md)

## 3. CONTEXT
Cổng thanh toán VNPay là phương thức thanh toán trực tuyến chính của Routine. Mọi thông số kết nối cần được bảo mật và cấu hình tập trung để sẵn sàng cho cả môi trường kiểm thử Sandbox và môi trường Production thực tế.

## 4. PREREQUISITES
- PROMPT_014: Biến môi trường .env
- PROMPT_023: PaymentTransaction Model

## 5. INPUTS
- Thông tin tài khoản Merchant VNPay Sandbox

## 6. DETAILED TASKS
1. **Khai báo Biến Môi Trường trong backend/.env**:
   Cấu hình: VNP_TMN_CODE, VNP_HASH_SECRET, VNP_URL="https://sandbox.vnpayment.vn/paymentv2/vpcpay.html", VNP_RETURN_URL="http://localhost:3000/payment-result".

2. **Xây dựng Module backend/src/config/vnpay.js**:
   Export cấu hình chuẩn, kiểm tra các biến môi trường bắt buộc khi server khởi động. Nếu thiếu VNP_HASH_SECRET thì cảnh báo lỗi ngay lập tức.

3. **Cài đặt Thư viện và Helper Chữ Ký Số HMAC-SHA512**:
   Sử dụng crypto native của Node.js để tính toán mã băm sha512: crypto.createHmac("sha512", secret).update(Buffer.from(signData, "utf-8")).digest("hex").

## 7. TECHNICAL REQUIREMENTS
- Thuật toán chữ ký số HMAC-SHA512
- Thư viện vnpay ^2.5.0 hoặc triển khai native chuẩn quy chuẩn VNPay

## 8. INTEGRATION REQUIREMENTS
- Được sử dụng bởi vnpayService và paymentController


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Secret Exposure Prevention**: Tuyệt đối không gửi VNP_HASH_SECRET về phía client hoặc commit vào git repo.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Module cấu hình VNPay nạp đúng các tham số merchant.
[ ] **AC-2**: Hàm tạo chữ ký số HMAC-SHA512 cho ra kết quả băm chính xác.
[ ] **AC-3**: Server không bị crash khi cấu hình hợp lệ.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Chạy unit test kiểm tra hàm hash HMAC-SHA512 với chuỗi mẫu của VNPay

## 12. EXPECTED OUTPUT
- `backend/src/config/vnpay.js`: Cấu hình kết nối Merchant VNPay
- `backend/src/utils/vnpayHelper.js`: Hàm tính toán chữ ký số và sắp xếp tham số

## 13. COMPLETION REPORT
- Cấu hình thông số Merchant và thiết lập SDK VNPay hoàn thành
