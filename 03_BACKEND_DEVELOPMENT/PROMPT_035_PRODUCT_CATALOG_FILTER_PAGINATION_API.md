# PROMPT 035 – PRODUCT CATALOG SERVICE, MULTI-FACET FILTERING & PAGINATION

## 1. ROLE
Senior Backend Engineer / Performance Specialist

## 2. OBJECTIVE
Xây dựng API truy xuất danh sách sản phẩm thời trang hỗ trợ lọc đa tiêu chí (danh mục, khoảng giá, màu sắc, kích thước, giới tính), sắp xếp (mới nhất, giá tăng/giảm, bán chạy, xem nhiều) và phân trang chuẩn hóa.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_02_CLOUDINARY_ADMIN_PRODUCT_MANAGEMENT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_02_CLOUDINARY_ADMIN_PRODUCT_MANAGEMENT.md)
> - [USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md)
> - [USER_MASTER_PROMPT_25_PRODUCTION_UPGRADE_NOTIFICATION_HANDOFF.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_25_PRODUCTION_UPGRADE_NOTIFICATION_HANDOFF.md)

## 3. CONTEXT
Trang danh sách sản phẩm (PLP) của Routine cần phục vụ hàng trăm sản phẩm với khả năng lọc tức thì mà vẫn giữ thời gian phản hồi dưới 100ms.

## 4. PREREQUISITES
- PROMPT_034: Category API
- PROMPT_021: Product & Variant Models

## 5. INPUTS
- Các tham số query: category, minPrice, maxPrice, color, size, sort, page, limit

## 6. DETAILED TASKS
1. **Xây dựng ProductService.getProducts**:
   Xây dựng mệnh đề Prisma where động dựa trên các bộ lọc: categoryId (bao gồm cả category con), salePrice/originalPrice gte/lte, variants.some với color in [...] và size in [...], status = ACTIVE.

2. **Xây dựng Logic Sắp xếp và Phân trang**:
   Hỗ trợ sắp xếp: "price_asc", "price_desc", "newest", "views", "bestseller". Thực hiện prisma.$transaction([count, findMany]) để trả về { data, pagination: { total, page, limit, totalPages } }.

3. **Xây dựng ProductController và Route**:
   GET /api/v1/products với đầy đủ query parameters.

## 7. TECHNICAL REQUIREMENTS
- Pagination metadata chuẩn: page, limit, total, totalPages, hasNext, hasPrev
- Sử dụng eager loading (include) variants và category
- Thời gian phản hồi truy vấn dưới 100ms

## 8. INTEGRATION REQUIREMENTS
- Frontend Product Listing Page kết nối trực tiếp với endpoint này

## 9. SAFETY CONSTRAINTS
- ⚠️ **Limit Cap**: Giới hạn limit tối đa không quá 100 sản phẩm/lần để tránh nghẽn RAM.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Lọc sản phẩm theo màu sắc hoặc kích thước trả về chính xác sản phẩm có biến thể tương ứng.
[ ] **AC-2**: Phân trang hoạt động chính xác khi thay đổi page và limit.
[ ] **AC-3**: Sắp xếp giá tăng dần / giảm dần hoạt động chính xác.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm thử gọi API lọc kết hợp: /api/v1/products?category=ao-nam&minPrice=200000&maxPrice=500000&color=black&page=1&limit=12

## 12. EXPECTED OUTPUT
- `backend/src/services/productService.js`: Logic nghiệp vụ truy vấn danh mục sản phẩm
- `backend/src/controllers/productController.js`: Controller sản phẩm

## 13. COMPLETION REPORT
- API duyệt danh mục sản phẩm phân trang và đa bộ lọc đã hoàn thành
