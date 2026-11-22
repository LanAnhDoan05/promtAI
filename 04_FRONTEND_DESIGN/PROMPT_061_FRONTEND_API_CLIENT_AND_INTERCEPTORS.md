# PROMPT 061 – FRONTEND STATE MANAGEMENT, CLIENT COOKIE HANDLING & API INTERCEPTOR

## 1. ROLE
Senior Frontend Engineer

## 2. OBJECTIVE
Xây dựng module HTTP Client (Axios hoặc Fetch wrapper) tập trung tại frontend/src/utils/api.js: Tự động gắn Bearer Token vào header, xử lý làm mới token (Token Refresh) khi nhận HTTP 401, và chuẩn hóa xử lý lỗi mạng.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_23_HERO_SLIDER_AND_BRAND_EXPERIENCE.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_23_HERO_SLIDER_AND_BRAND_EXPERIENCE.md)
> - [USER_MASTER_PROMPT_27_GLOBAL_BRANDING_AND_WARNING_AUDIT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_27_GLOBAL_BRANDING_AND_WARNING_AUDIT.md)

## 3. CONTEXT
Mọi giao tiếp giữa Frontend Next.js và Backend Express đều thông qua API Client này. Cần cơ chế tự động thử lại (retry) và chuyển hướng đăng nhập khi phiên làm việc hết hạn để người dùng không bị gián đoạn thao tác.

## 4. PREREQUISITES
- PROMPT_031: Express Backend
- PROMPT_032: JWT Auth

## 5. INPUTS
- NEXT_PUBLIC_API_URL môi trường

## 6. DETAILED TASKS
1. **Tạo apiClient instance với Base URL**:
   Cấu hình baseURL = process.env.NEXT_PUBLIC_API_URL || "http://localhost:5001/api/v1", timeout: 15000, withCredentials: true.

2. **Xây dựng Request Interceptor**:
   Tự động lấy accessToken từ cookie/localStorage và đính kèm vào Authorization: Bearer <token>. Tự động đính kèm X-Session-Id nếu là khách vãng lai.

3. **Xây dựng Response Interceptor và Auto-Refresh Token**:
   Nếu response trả về 401 Unauthorized và chưa retry: gọi POST /api/v1/auth/refresh để lấy token mới, sau đó gửi lại request ban đầu. Nếu refresh thất bại, xóa token và chuyển hướng tới /login.

## 7. TECHNICAL REQUIREMENTS
- Xử lý queue các request đồng thời khi đang chờ refresh token để không gọi refresh nhiều lần
- Chuẩn hóa cấu trúc lỗi trả về cho UI dễ dàng hiển thị Toast

## 8. INTEGRATION REQUIREMENTS
- Tất cả các dịch vụ gọi API phía frontend đều import từ utils/api.js


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Infinite Refresh Loop**: Phải có cờ _retry để ngăn chặn vòng lặp vô tận khi endpoint refresh trả về 401.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Mọi request gửi đi đều tự động có header Authorization hợp lệ nếu đã đăng nhập.
[ ] **AC-2**: Khi accessToken hết hạn, hệ thống tự làm mới token ngầm mà người dùng không nhận ra.
[ ] **AC-3**: Lỗi mạng được chuyển thành thông báo tiếng Việt dễ hiểu.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Mô phỏng token hết hạn và kiểm tra request tự động phục hồi thành công

## 12. EXPECTED OUTPUT
- `frontend/src/utils/api.js`: HTTP API Client trung tâm với interceptors

## 13. COMPLETION REPORT
- Module giao tiếp API phía frontend hoàn thành
