# PROMPT 063 – USERCONTEXT & GLOBAL AUTHENTICATION STATE MANAGEMENT

## 1. ROLE
Frontend State Management Specialist

## 2. OBJECTIVE
Xây dựng UserContext quản lý trạng thái đăng nhập toàn cục của khách hàng: lưu trữ thông tin user profile, cờ isAuthenticated, hàm login, logout, cập nhật profile và tự động khôi phục phiên từ token khi tải lại trang.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_21_ADDRESS_VALIDATION_AI_CONSULTATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_21_ADDRESS_VALIDATION_AI_CONSULTATION.md)
> - [USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md)

## 3. CONTEXT
Trạng thái đăng nhập ảnh hưởng đến Header (hiển thị Avatar / Tên khách hàng hay nút Đăng nhập), giỏ hàng, danh sách yêu thích, và quyền truy cập vào trang Checkout / Profile.

## 4. PREREQUISITES
- PROMPT_061: Frontend API Client
- PROMPT_032: Backend Auth API

## 5. INPUTS
- API /api/v1/auth/me, /api/v1/auth/login, /api/v1/auth/logout

## 6. DETAILED TASKS
1. **Xây dựng UserContext và UserProvider**:
   Tạo context/UserContext.js với state: user (null hoặc object), loading (boolean), isAuthenticated (boolean).

2. **Xử lý Tự động Khôi phục Phiên (Auto-fetch Profile)**:
   Trong useEffect khởi tạo: kiểm tra token trong localStorage/cookie, nếu có gọi GET /api/v1/auth/me để cập nhật state user.

3. **Xây dựng hàm login và logout**:
   Hàm login(credentials): gọi API đăng nhập, lưu token, cập nhật state user. Hàm logout(): gọi API đăng xuất, dọn sạch cookie/token và chuyển hướng về trang chủ.

## 7. TECHNICAL REQUIREMENTS
- React createContext + useContext
- Custom hook useAuth() tiện dụng
- Khắc phục tình trạng chớp giao diện (flicker) bằng state loading ban đầu

## 8. INTEGRATION REQUIREMENTS
- Bao bọc trong RootLayout và cung cấp state cho toàn bộ ứng dụng


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Token Leakage in State**: Không lưu trữ token nhạy cảm trong state dễ bị trích xuất hoặc in ra console.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Đăng nhập thành công cập nhật ngay Header sang trạng thái tài khoản.
[ ] **AC-2**: F5 tải lại trang vẫn giữ nguyên trạng thái đăng nhập.
[ ] **AC-3**: Bấm đăng xuất xóa sạch phiên và trở về trang chủ.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm thử đăng nhập, F5 trang và đăng xuất

## 12. EXPECTED OUTPUT
- `frontend/src/context/UserContext.js`: Quản lý trạng thái xác thực toàn cục

## 13. COMPLETION REPORT
- UserContext và quản lý phiên đăng nhập toàn cục đã hoàn thành
