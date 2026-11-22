# PROMPT 094 – ADMIN PORTAL AUTHENTICATION, SESSION SECURITY & PROTECTED LAYOUT

## 1. ROLE
Frontend Architect / Admin Systems Specialist

## 2. OBJECTIVE
Xây dựng cấu trúc cổng Quản trị viên (Admin Portal) tại /admin: Đăng nhập quản trị riêng biệt, kiểm tra quyền nghiêm ngặt (chỉ cho phép Role ADMIN hoặc STAFF), thanh điều hướng Sidebar quản trị (Dashboard, Sản phẩm, Danh mục, Đơn hàng, Khách hàng, Tư vấn Leads, Khuyến mãi, Cài đặt), Header quản trị với chuông thông báo SSE thời gian thực và nút Đăng xuất.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_05_AI_BUSINESS_INTELLIGENCE_AUDIT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_05_AI_BUSINESS_INTELLIGENCE_AUDIT.md)
> - [USER_MASTER_PROMPT_24_ADMIN_NOTIFICATION_CENTER.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_24_ADMIN_NOTIFICATION_CENTER.md)
> - [USER_MASTER_PROMPT_28_AI_BI_IMPLEMENTATION_AND_E2E_AUDIT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_28_AI_BI_IMPLEMENTATION_AND_E2E_AUDIT.md)
> - [USER_MASTER_PROMPT_29_BI_DASHBOARD_TABLES_UI_OPTIMIZATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_29_BI_DASHBOARD_TABLES_UI_OPTIMIZATION.md)

## 3. CONTEXT
Khu vực quản trị là trung tâm điều hành toàn bộ sàn thương mại điện tử Routine. Cần layout chuyên nghiệp, tông màu tối giản sang trọng, bảo mật cao và tiện dụng cho nhân viên vận hành.

## 4. PREREQUISITES
- PROMPT_033: RBAC Middleware
- PROMPT_061: Frontend API Client

## 5. INPUTS
- Tài khoản admin mặc định: admin@routine.vn

## 6. DETAILED TASKS
1. **Xây dựng AdminLayout (app/admin/layout.js)**:
   Kiểm tra role người dùng: nếu không phải ADMIN/STAFF, lập tức chuyển hướng về /login hoặc trang 403 Forbidden. Cấu trúc 2 cột: Sidebar cố định bên trái (260px) và Nội dung chính co giãn bên phải.

2. **Xây dựng Admin Sidebar Điều Hướng**:
   Menu các phân hệ: 1) Dashboard Tổng quan; 2) Phân tích AI BI; 3) Quản lý Sản phẩm & Biến thể; 4) Danh mục & Phong cách; 5) Đơn hàng; 6) Khách hàng CRM; 7) Bàn trực Tư vấn Lead (Live Chat); 8) Mã giảm giá; 9) Cài đặt hệ thống.

3. **Xây dựng Admin Header**:
   Hiển thị tiêu đề trang hiện tại, chuông thông báo realtime với badge số thông báo chưa đọc, thông tin Admin đăng nhập và nút Đăng xuất an toàn.

## 7. TECHNICAL REQUIREMENTS
- Bảo vệ nghiêm ngặt bằng Next.js middleware hoặc layout guard
- Lưu trạng thái thu gọn Sidebar (collapsed/expanded) vào localStorage

## 8. INTEGRATION REQUIREMENTS
- Bao bọc tất cả các trang con trong app/admin/*

## 9. SAFETY CONSTRAINTS
- ⚠️ **Session Hijacking in Admin**: Tự động đăng xuất quản trị viên nếu không có thao tác sau 60 phút.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Đăng nhập tài khoản admin truy cập /admin thành công.
[ ] **AC-2**: Tài khoản khách hàng thông thường truy cập /admin bị chặn với thông báo không có quyền.
[ ] **AC-3**: Sidebar điều hướng chính xác giữa tất cả các phân hệ quản trị.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Thử đăng nhập tài khoản thường và truy cập /admin để xác minh bảo vệ

## 12. EXPECTED OUTPUT
- `frontend/src/app/admin/layout.js`: Layout quản trị viên bảo vệ
- `frontend/src/components/Admin/AdminSidebar.jsx`: Sidebar quản trị
- `frontend/src/components/Admin/AdminHeader.jsx`: Header quản trị

## 13. COMPLETION REPORT
- Khung quản trị Admin Portal và bảo mật phiên hoàn thành
