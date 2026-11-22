# PROMPT 012 – CÀI ĐẶT MÔI TRƯỜNG NODE.JS & EXPRESS SERVER 4.22

## 1. ROLE
Senior Backend Engineer

## 2. OBJECTIVE
Cài đặt môi trường chạy Node.js trong thư mục `backend/`, cài đặt Express 4.22.3 và cấu hình script khởi động `bin/www`.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_04_SELF_TEST_ENVIRONMENT_HANDOVER.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_04_SELF_TEST_ENVIRONMENT_HANDOVER.md)
> - [USER_MASTER_PROMPT_15_ADMIN_CUSTOMER_CONCURRENT_OPS.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_15_ADMIN_CUSTOMER_CONCURRENT_OPS.md)

## 3. CONTEXT
Phân hệ Backend cung cấp toàn bộ RESTful API, quản lý kết nối cơ sở dữ liệu và xử lý các dịch vụ nền tảng.

## 4. PREREQUISITES
- PROMPT_011 hoàn thành

## 5. INPUTS
- backend/package.json
- docs/00_SYSTEM_ARCHITECTURE_DOCUMENT.md

## 6. DETAILED TASKS
1. **Khởi tạo `package.json` cho Backend**:
   Cấu hình name `routine-backend`, version `1.0.0`, dependencies chuẩn xác: `express@^4.22.3`, `dotenv@^16.4.7`, `cors@^2.8.5`, `helmet@^8.0.0`, `morgan@^1.10.0`.

2. **Xây dựng file khởi chạy `backend/bin/www`**:
   Tạo HTTP Server Node.js lắng nghe trên cổng 5001, xử lý các sự kiện `onError` và `onListening`.

3. **Tạo ứng dụng Express chính `backend/src/app.js`**:
   Khởi tạo Express app, cấu hình body-parser (json, urlencoded) và route kiểm tra sức khỏe cơ bản `/api/v1/health`.

## 7. TECHNICAL REQUIREMENTS
- Express.js phiên bản 4.22.3 theo chuẩn CommonJS
- Mặc định lắng nghe trên cổng 5001 (hoặc lấy từ biến môi trường `PORT`)

## 8. INTEGRATION REQUIREMENTS
- Sẵn sàng tích hợp middleware bảo mật và cơ sở dữ liệu ở các prompt sau.


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Xử lý lỗi cổng**: Có cơ chế thông báo rõ ràng nếu cổng 5001 bị chiếm dụng bởi ứng dụng khác.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Chạy `npm install` thành công trong `backend/` không gặp lỗi
[ ] **AC-2**: Chạy `node bin/www` server khởi động và trả về HTTP 200 tại `/api/v1/health`

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Gửi request `GET http://localhost:5001/api/v1/health` xác nhận JSON trả về `{ success: true, message: "Routine Web Backend is operational" }`

## 12. EXPECTED OUTPUT
- `backend/package.json`: Cấu hình dependencies Backend
- `backend/bin/www`: Script khởi động HTTP Server Backend
- `backend/src/app.js`: File cấu hình ứng dụng Express chính

## 13. COMPLETION REPORT
- Báo cáo Backend khởi động thành công trên cổng 5001 và sẵn sàng tích hợp.
