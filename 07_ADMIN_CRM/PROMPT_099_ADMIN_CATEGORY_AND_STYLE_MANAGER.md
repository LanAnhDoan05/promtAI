# PROMPT 099 – ADMIN CATEGORY & STYLE HIERARCHY MANAGER

## 1. ROLE
Frontend & Backend CRUD Specialist

## 2. OBJECTIVE
Xây dựng trang Quản lý danh mục và phong cách (app/admin/categories/page.js và app/admin/styles/page.js): Hiển thị cây danh mục phân cấp đa tầng (kéo thả hoặc chọn danh mục cha), thêm/sửa/xóa danh mục, và quản lý các phong cách phối đồ (Công sở, Dạo phố, Thu Đông).


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_05_AI_BUSINESS_INTELLIGENCE_AUDIT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_05_AI_BUSINESS_INTELLIGENCE_AUDIT.md)
> - [USER_MASTER_PROMPT_24_ADMIN_NOTIFICATION_CENTER.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_24_ADMIN_NOTIFICATION_CENTER.md)
> - [USER_MASTER_PROMPT_28_AI_BI_IMPLEMENTATION_AND_E2E_AUDIT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_28_AI_BI_IMPLEMENTATION_AND_E2E_AUDIT.md)
> - [USER_MASTER_PROMPT_29_BI_DASHBOARD_TABLES_UI_OPTIMIZATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_29_BI_DASHBOARD_TABLES_UI_OPTIMIZATION.md)

## 3. CONTEXT
Giúp ban quản trị dễ dàng cơ cấu lại cây phân loại thời trang và các phong cách theo mùa của Routine.

## 4. PREREQUISITES
- PROMPT_034: Category API
- PROMPT_045: Outfit Style Service

## 5. INPUTS
- Category and Style APIs

## 6. DETAILED TASKS
1. **Xây dựng Giao diện Quản lý Cây Danh Mục**:
   Hiển thị danh sách danh mục dạng lồng nhau (Tree view). Nút Thêm danh mục con, chỉnh sửa tên, ảnh đại diện danh mục.

2. **Xây dựng Quản lý Phong Cách Phối Đồ (Style Manager)**:
   Danh sách các phong cách thời trang, mô tả và hình ảnh đại diện phục vụ cho tính năng Smart Outfit.

## 7. TECHNICAL REQUIREMENTS
- Tự động sinh slug chuẩn SEO
- Kiểm tra không cho xóa danh mục nếu đang chứa sản phẩm

## 8. INTEGRATION REQUIREMENTS
- Admin Portal navigation


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Orphaned Products Prevention**: Chặn xóa danh mục nếu còn sản phẩm trực thuộc.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Tạo danh mục cha và danh mục con thành công.
[ ] **AC-2**: Chỉnh sửa tên danh mục cập nhật ngay cây phân cấp.
[ ] **AC-3**: Quản lý phong cách style hoạt động tốt.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm thử tạo danh mục con cấp 2 và kiểm tra cây hiển thị

## 12. EXPECTED OUTPUT
- `frontend/src/app/admin/categories/page.js`: Trang quản lý danh mục phân cấp

## 13. COMPLETION REPORT
- Quản lý danh mục phân cấp và phong cách thời trang hoàn thành
