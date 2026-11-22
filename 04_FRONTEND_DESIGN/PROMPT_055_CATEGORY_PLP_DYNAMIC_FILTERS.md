# PROMPT 055 – CATEGORY & PRODUCT LISTING PAGE (PLP) WITH DYNAMIC FILTERS & SORTING

## 1. ROLE
Senior Frontend Developer

## 2. OBJECTIVE
Xây dựng trang danh mục sản phẩm (app/category/[slug]/page.js hoặc app/products/page.js): Thanh breadcrumb, tiêu đề danh mục, bộ lọc bên cạnh (Sidebar Filter: Danh mục con, Mức giá, Màu sắc, Kích cỡ), thanh công cụ sắp xếp (Mới nhất, Giá tăng/giảm, Bán chạy), lưới sản phẩm responsive và phân trang.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_23_HERO_SLIDER_AND_BRAND_EXPERIENCE.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_23_HERO_SLIDER_AND_BRAND_EXPERIENCE.md)
> - [USER_MASTER_PROMPT_27_GLOBAL_BRANDING_AND_WARNING_AUDIT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_27_GLOBAL_BRANDING_AND_WARNING_AUDIT.md)

## 3. CONTEXT
Khách hàng duyệt sắm qua trang danh mục. Bộ lọc cần đồng bộ trực tiếp với URL query parameters (?category=...&color=...&sort=...) để khách hàng có thể chia sẻ link hoặc bookmark kết quả tìm kiếm.

## 4. PREREQUISITES
- PROMPT_054: ProductCard Component
- PROMPT_035: Product Catalog API

## 5. INPUTS
- Slug danh mục từ route params và searchParams

## 6. DETAILED TASKS
1. **Xây dựng Breadcrumb và Header trang danh mục**:
   Đường dẫn phân cấp: Trang chủ > Đồ Nam > Áo Sơ Mi. Tiêu đề danh mục lớn cùng mô tả ngắn.

2. **Xây dựng Bộ lọc đa tiêu chí (Filter Sidebar)**:
   Khung lọc danh mục con, khoảng giá (radio hoặc slider), bảng màu sắc (Color circles), kích cỡ (Size buttons). Nút "Xóa tất cả bộ lọc".

3. **Xây dựng Thanh công cụ Sắp xếp và Đếm số lượng**:
   Hiển thị: "Hiển thị 24 trên 150 sản phẩm". Dropdown sắp xếp: Mới nhất, Bán chạy, Giá tăng dần, Giá giảm dần.

4. **Lưới hiển thị sản phẩm và Phân trang (Pagination)**:
   Grid layout: 4 cột trên desktop (>1200px), 3 cột trên tablet, 2 cột trên điện thoại (<768px). Bộ điều khiển trang 1, 2, 3... Trang tiếp / Trang trước.

## 7. TECHNICAL REQUIREMENTS
- Sử dụng next/navigation: useRouter, useSearchParams, usePathname
- Cập nhật URL không làm tải lại trang (shallow routing)

## 8. INTEGRATION REQUIREMENTS
- Gọi GET /api/v1/products với searchParams tương ứng

## 9. SAFETY CONSTRAINTS
- ⚠️ **Empty State Handling**: Khi bộ lọc không tìm thấy sản phẩm nào, hiển thị thông báo thân thiện và nút "Bỏ chọn bộ lọc".

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Chọn bộ lọc màu sắc cập nhật ngay lập tức danh sách sản phẩm và URL query.
[ ] **AC-2**: Lưới sản phẩm tự co giãn đẹp mắt trên mọi kích thước màn hình.
[ ] **AC-3**: Chuyển trang giữ nguyên các bộ lọc đã chọn.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm thử chọn nhiều bộ lọc cùng lúc: Áo Nam + Màu Đen + Size L + Giá tăng dần

## 12. EXPECTED OUTPUT
- `frontend/src/app/category/[slug]/page.js`: Trang danh mục sản phẩm
- `frontend/src/components/Category/FilterSidebar.jsx`: Khung bộ lọc
- `frontend/src/components/Category/Category.module.css`: CSS Module danh mục

## 13. COMPLETION REPORT
- Trang duyệt danh mục sản phẩm hoàn chỉnh với bộ lọc động và URL sync
