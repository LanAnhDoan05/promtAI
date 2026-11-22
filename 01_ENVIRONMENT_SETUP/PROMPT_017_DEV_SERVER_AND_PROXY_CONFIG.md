# PROMPT 017 – CẤU HÌNH CHẠY ĐỒNG THỜI BACKEND (5001) & FRONTEND (3000)

## 1. ROLE
DevOps & Tooling Engineer

## 2. OBJECTIVE
Cấu hình môi trường phát triển cục bộ, cho phép khởi động song song Backend Express (cổng 5001) và Frontend Next.js (cổng 3000) cùng file điều phối `start.bat`.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_04_SELF_TEST_ENVIRONMENT_HANDOVER.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_04_SELF_TEST_ENVIRONMENT_HANDOVER.md)
> - [USER_MASTER_PROMPT_15_ADMIN_CUSTOMER_CONCURRENT_OPS.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_15_ADMIN_CUSTOMER_CONCURRENT_OPS.md)

## 3. CONTEXT
Giúp lập trình viên và kiểm thử viên có thể khởi động toàn bộ hệ thống bằng một thao tác duy nhất mà không bị xung đột tiến trình.

## 4. PREREQUISITES
- PROMPT_012, PROMPT_013, PROMPT_014 hoàn thành

## 5. INPUTS
- backend/package.json
- frontend/package.json

## 6. DETAILED TASKS
1. **Tạo file script khởi động nhanh `start.bat`**:
   Tự động mở hai cửa sổ terminal riêng biệt: một chạy `backend (node bin/www)` và một chạy `frontend (npm run dev)`.

2. **Cấu hình CORS trong Express Backend**:
   Cho phép nguồn `http://localhost:3000` truy cập các tài nguyên API với đầy đủ headers và credentials.

3. **Xây dựng file thư viện gọi API `frontend/lib/api.js`**:
   Cấu hình hàm `fetchApi(endpoint, options)` tự động gắn Base URL và xử lý lỗi mạng tập trung.

## 7. TECHNICAL REQUIREMENTS
- Hỗ trợ môi trường dòng lệnh Windows PowerShell và Command Prompt
- Hàm `fetchApi` tự động chuyển đổi JSON và bắt mã lỗi HTTP (401, 403, 500)

## 8. INTEGRATION REQUIREMENTS
- Kết nối thông suốt hai chiều giữa cổng 3000 và 5001.


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Tránh kẹt tiến trình**: Có hướng dẫn rõ ràng cách giải phóng cổng nếu Node.js bị treo ngầm trên Windows.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Khởi động cả hai phân hệ thành công bằng lệnh chạy tự động
[ ] **AC-2**: Frontend gọi thử endpoint `/api/v1/health` của Backend nhận dữ liệu thành công

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm tra kết nối chéo giữa cổng 3000 và cổng 5001 qua fetch API

## 12. EXPECTED OUTPUT
- `start.bat`: Script khởi động tự động hệ thống trên Windows
- `frontend/lib/api.js`: Thư viện client gọi API tập trung

## 13. COMPLETION REPORT
- Xác nhận hai phân hệ đã kết nối liên thông thành công trong môi trường phát triển.
