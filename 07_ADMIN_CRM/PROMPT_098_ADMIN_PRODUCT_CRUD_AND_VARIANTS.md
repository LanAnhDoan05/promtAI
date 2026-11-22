# PROMPT 098 – ADMIN PRODUCT CATALOG CRUD, IMAGE UPLOAD & VARIANT MATRIX MANAGEMENT

## 1. ROLE
Frontend & Backend CRUD Specialist

## 2. OBJECTIVE
Xây dựng trang Quản lý sản phẩm thời trang (app/admin/products/page.js): Danh sách sản phẩm có tìm kiếm/lọc, form Thêm mới / Sửa sản phẩm (Tên, Slug, Mô tả, Danh mục, Chất liệu, Form dáng, Giá niêm yết, Giá khuyến mãi), tải nhiều ảnh lên Cloudinary, và ma trận quản lý biến thể (Variant Matrix: thêm/sửa Màu sắc, Kích cỡ S/M/L/XL, mã SKU tự động và số lượng tồn kho từng loại).


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_05_AI_BUSINESS_INTELLIGENCE_AUDIT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_05_AI_BUSINESS_INTELLIGENCE_AUDIT.md)
> - [USER_MASTER_PROMPT_24_ADMIN_NOTIFICATION_CENTER.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_24_ADMIN_NOTIFICATION_CENTER.md)
> - [USER_MASTER_PROMPT_28_AI_BI_IMPLEMENTATION_AND_E2E_AUDIT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_28_AI_BI_IMPLEMENTATION_AND_E2E_AUDIT.md)
> - [USER_MASTER_PROMPT_29_BI_DASHBOARD_TABLES_UI_OPTIMIZATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_29_BI_DASHBOARD_TABLES_UI_OPTIMIZATION.md)

## 3. CONTEXT
Quản trị viên cần công cụ linh hoạt để nhập liệu và quản lý hàng trăm mẫu quần áo Routine kèm theo nhiều biến thể kích thước và màu sắc khác nhau.

## 4. PREREQUISITES
- PROMPT_035: Product Service
- PROMPT_046: Cloudinary Upload

## 5. INPUTS
- Product và ProductVariant APIs trong /api/v1/admin/products

## 6. DETAILED TASKS
1. **Xây dựng Bảng Danh Sách Sản Phẩm Quản Trị**:
   Hiển thị: Ảnh đại diện, Tên sản phẩm, Danh mục, Giá bán, Tổng tồn kho các biến thể, Trạng thái (ACTIVE / INACTIVE), Lượt xem, và các nút Thao tác (Sửa, Đổi trạng thái, Xóa).

2. **Xây dựng Form Thêm Mới / Chỉnh Sửa Sản Phẩm**:
   Form 2 cột chuyên nghiệp: Cột chính nhập thông tin sản phẩm và upload gallery ảnh; Cột phụ chọn danh mục, gắn styleTag, và thiết lập trạng thái.

3. **Bảng Ma Trận Biến Thể SKU (Variant Matrix Table)**:
   Cho phép bấm "Thêm biến thể", chọn màu và size. Tự động sinh mã SKU theo quy tắc: [SLUG]-[COLOR]-[SIZE]. Nhập số lượng tồn kho và giá riêng cho biến thể nếu có.

## 7. TECHNICAL REQUIREMENTS
- Xử lý transaction khi lưu sản phẩm và danh sách biến thể đồng thời
- Tải ảnh trực tiếp lên Cloudinary và preview trước khi lưu

## 8. INTEGRATION REQUIREMENTS
- Admin Portal và Backend Product Controller

## 9. SAFETY CONSTRAINTS
- ⚠️ **Cascade Delete Safety**: Không cho phép xóa cứng sản phẩm nếu đã có trong đơn hàng cũ (chuyển sang INACTIVE thay vì DELETE).

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Thêm mới sản phẩm thời trang kèm 4 biến thể SKU thành công.
[ ] **AC-2**: Chỉnh sửa thông tin và cập nhật tồn kho biến thể chính xác.
[ ] **AC-3**: Tải ảnh lên Cloudinary hoạt động mượt mà.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Tạo một sản phẩm áo khoác mẫu với 2 màu và 3 size kiểm tra lưu vào database

## 12. EXPECTED OUTPUT
- `frontend/src/app/admin/products/page.js`: Trang danh sách sản phẩm quản trị
- `frontend/src/app/admin/products/[id]/page.js`: Trang chỉnh sửa sản phẩm và ma trận SKU

## 13. COMPLETION REPORT
- Hệ thống quản lý sản phẩm và ma trận biến thể SKU hoàn thành
