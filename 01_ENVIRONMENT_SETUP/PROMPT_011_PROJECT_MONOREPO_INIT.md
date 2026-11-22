# PROMPT 011 – KHỞI TẠO CẤU TRÚC DỰ ÁN MONOREPO FRONTEND & BACKEND

## 1. ROLE
Lead DevOps Engineer

## 2. OBJECTIVE
Khởi tạo cấu trúc thư mục dự án sạch sẽ từ thư mục gốc, phân tách rõ ràng hai phân hệ `frontend/` và `backend/`.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_04_SELF_TEST_ENVIRONMENT_HANDOVER.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_04_SELF_TEST_ENVIRONMENT_HANDOVER.md)
> - [USER_MASTER_PROMPT_15_ADMIN_CUSTOMER_CONCURRENT_OPS.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_15_ADMIN_CUSTOMER_CONCURRENT_OPS.md)

## 3. CONTEXT
Routine Platform được tổ chức theo cấu trúc monorepo phân tầng giúp quản lý mã nguồn tập trung nhưng đảm bảo tính độc lập hoàn toàn khi thực thi.

## 4. PREREQUISITES
- PROMPT_010 (Gateway 0) hoàn thành

## 5. INPUTS
- Quy chuẩn cấu trúc thư mục trong `docs/00_CODING_STANDARDS.md`

## 6. DETAILED TASKS
1. **Tạo cấu trúc thư mục gốc**:
   Khởi tạo thư mục `frontend/`, `backend/`, `docs/`, `scripts/`.

2. **Khởi tạo Git Repository & .gitignore**:
   Thiết lập `.gitignore` chuẩn tại thư mục gốc loại trừ `node_modules`, `.next`, `.env`, build artifacts.

3. **Tạo README.md tổng quan dự án**:
   Soạn thảo tài liệu hướng dẫn cấu trúc dự án, yêu cầu Node.js (>= 18.x) và cách cài đặt ban đầu.

## 7. TECHNICAL REQUIREMENTS
- Node.js phiên bản LTS (Khuyến nghị Node.js v20+ hoặc v24)
- Hệ thống tệp tương thích đa nền tảng (Windows, macOS, Linux)

## 8. INTEGRATION REQUIREMENTS
- Đảm bảo hai thư mục frontend và backend không bị xung đột dependencies.


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Không lồng thư mục thừa**: Tránh tạo cấu trúc thư mục trùng tên lồng nhau.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Thư mục `frontend/` và `backend/` được khởi tạo thành công
[ ] **AC-2**: File `.gitignore` hoạt động chuẩn xác, không commit file rác

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Chạy `git status` xác nhận cây thư mục sạch sẽ

## 12. EXPECTED OUTPUT
- `.gitignore`: Quy tắc loại trừ file cho Git
- `README.md`: Tài liệu tổng quan dự án Routine

## 13. COMPLETION REPORT
- Báo cáo hoàn thành cấu trúc thư mục và chuyển sang cài đặt Backend.
