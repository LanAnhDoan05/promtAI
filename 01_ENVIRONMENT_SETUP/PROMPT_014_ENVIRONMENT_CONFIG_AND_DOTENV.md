# PROMPT 014 – THIẾT LẬP HỆ THỐNG BIẾN MÔI TRƯỜNG AN TOÀN (.ENV.EXAMPLE)

## 1. ROLE
DevOps & Security Specialist

## 2. OBJECTIVE
Xây dựng cấu trúc quản lý biến môi trường an toàn cho cả Backend và Frontend, cung cấp các file `.env.example` chuẩn mẫu.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_04_SELF_TEST_ENVIRONMENT_HANDOVER.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_04_SELF_TEST_ENVIRONMENT_HANDOVER.md)
> - [USER_MASTER_PROMPT_15_ADMIN_CUSTOMER_CONCURRENT_OPS.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_15_ADMIN_CUSTOMER_CONCURRENT_OPS.md)

## 3. CONTEXT
Bảo vệ các thông tin nhạy cảm: thông tin kết nối MySQL, khóa bí mật JWT, API Key Google Gemini và Merchant Key VNPAY.

## 4. PREREQUISITES
- PROMPT_012, PROMPT_013 hoàn thành

## 5. INPUTS
- docs/00_SECURITY_AND_COMPLIANCE_POLICY.md

## 6. DETAILED TASKS
1. **Tạo `backend/.env.example`**:
   Khai báo các biến mẫu: `PORT=5001`, `DATABASE_URL=mysql://user:pass@localhost:3306/routine_test_db`, `JWT_SECRET`, `GEMINI_API_KEY`, `VNP_TMN_CODE`, `VNP_HASH_SECRET`, `VNP_URL`.

2. **Tạo `frontend/.env.example`**:
   Khai báo biến mẫu: `NEXT_PUBLIC_API_URL=http://localhost:5001/api/v1`.

3. **Cấu hình nạp biến môi trường trong mã nguồn**:
   Sử dụng `dotenv` tại dòng đầu tiên của `backend/bin/www` và `backend/src/app.js`.

## 7. TECHNICAL REQUIREMENTS
- Bắt buộc kiểm tra sự tồn tại của các biến môi trường thiết yếu khi server khởi động (Fail-fast mechanism)

## 8. INTEGRATION REQUIREMENTS
- Frontend giao tiếp với Backend thông qua biến môi trường `NEXT_PUBLIC_API_URL`.


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Không commit file `.env` thật**: Đảm bảo file `.env` được liệt kê trong `.gitignore`.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: File `.env.example` được tạo đầy đủ ở cả `backend/` và `frontend/`
[ ] **AC-2**: Server hiển thị cảnh báo nếu thiếu các biến môi trường quan trọng

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Thử khởi động server khi thiếu file `.env` để kiểm tra cơ chế cảnh báo lỗi

## 12. EXPECTED OUTPUT
- `backend/.env.example`: Biến môi trường mẫu cho Backend
- `frontend/.env.example`: Biến môi trường mẫu cho Frontend

## 13. COMPLETION REPORT
- Hoàn tất cấu hình biến môi trường an toàn cho toàn hệ thống.
