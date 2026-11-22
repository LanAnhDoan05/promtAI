# PROMPT 034 – CATEGORY MANAGEMENT API & MULTI-LEVEL HIERARCHY CONTROLLER

## 1. ROLE
Backend API Developer

## 2. OBJECTIVE
Xây dựng API quản lý danh mục thời trang phân cấp (Parent - Child Hierarchy), hỗ trợ truy xuất cây danh mục dạng nested tree và CRUD danh mục cho Admin.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_02_CLOUDINARY_ADMIN_PRODUCT_MANAGEMENT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_02_CLOUDINARY_ADMIN_PRODUCT_MANAGEMENT.md)
> - [USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md)
> - [USER_MASTER_PROMPT_25_PRODUCTION_UPGRADE_NOTIFICATION_HANDOFF.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_25_PRODUCTION_UPGRADE_NOTIFICATION_HANDOFF.md)

## 3. CONTEXT
Danh mục Routine có cấu trúc phân cấp (ví dụ: Danh mục gốc "Nam" -> Danh mục con "Áo Nam" -> Danh mục cháu "Áo Sơ Mi Nam"). Client cần API lấy danh mục dạng phẳng hoặc dạng lồng nhau để hiển thị menu đa cấp.

## 4. PREREQUISITES
- PROMPT_031: Express HTTP Server Architecture
- PROMPT_021: Category Model

## 5. INPUTS
- Schema Category trong Prisma

## 6. DETAILED TASKS
1. **Xây dựng CategoryService**:
   Viết các hàm getCategoryTree(), getAllCategories(), getCategoryBySlug(), createCategory(), updateCategory(), deleteCategory(). Xây dựng thuật toán chuyển danh sách phẳng thành cây nested.

2. **Xây dựng CategoryController**:
   Tiếp nhận các HTTP request, validate dữ liệu đầu vào (name, slug, parentId, image) và gọi Service tương ứng.

3. **Đăng ký Routes trong api.js**:
   GET /api/v1/categories (public, lấy cây danh mục), GET /api/v1/categories/:slug (chi tiết danh mục), POST /api/v1/categories (Admin), PUT /api/v1/categories/:id (Admin), DELETE /api/v1/categories/:id (Admin).

## 7. TECHNICAL REQUIREMENTS
- Slug tự động chuẩn hóa từ tên tiếng Việt không dấu (ví dụ: "Áo Sơ Mi" -> "ao-so-mi")
- Hỗ trợ đếm số lượng sản phẩm trong từng danh mục

## 8. INTEGRATION REQUIREMENTS
- Frontend Header menu và Sidebar bộ lọc sản phẩm tiêu thụ API này


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Circular Reference**: Ngăn chặn một danh mục chọn chính nó hoặc con của nó làm parentId.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: GET /api/v1/categories trả về cây danh mục phân cấp đúng quan hệ cha - con.
[ ] **AC-2**: Tạo danh mục mới tự động sinh slug duy nhất.
[ ] **AC-3**: Chỉ ADMIN mới có quyền tạo/sửa/xóa danh mục.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Gọi GET /api/v1/categories kiểm tra cấu trúc tree JSON
2. **Tình huống kiểm thử 2**: Kiểm thử tạo danh mục trùng slug

## 12. EXPECTED OUTPUT
- `backend/src/services/categoryService.js`: Logic nghiệp vụ cây danh mục
- `backend/src/controllers/categoryController.js`: Controller tiếp nhận API danh mục

## 13. COMPLETION REPORT
- API danh mục phân cấp đa tầng đã hoàn thành và sẵn sàng phục vụ frontend
