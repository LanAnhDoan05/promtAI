# PROMPT 021 – CATEGORY, PRODUCT & PRODUCTVARIANT MODELS WITH SKU UNIQUE INDEXES

## 1. ROLE
Database Architect

## 2. OBJECTIVE
Xây dựng mô hình dữ liệu danh mục phân cấp đa cấp (Category) và sản phẩm thời trang Routine với các biến thể (ProductVariant: màu sắc, kích thước, SKU, tồn kho, giá bán).


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_09_REAL_DATA_AND_BUSINESS_LOGIC.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_09_REAL_DATA_AND_BUSINESS_LOGIC.md)
> - [USER_MASTER_PROMPT_13_MYSQL_AI_ADDRESS_SHIPPING_SYNC.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_13_MYSQL_AI_ADDRESS_SHIPPING_SYNC.md)
> - [USER_MASTER_PROMPT_12_ROUTINE_VN_CATALOG_SCRAPING.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_12_ROUTINE_VN_CATALOG_SCRAPING.md)

## 3. CONTEXT
Ngành thời trang Routine có cấu trúc sản phẩm đa biến thể (Size S/M/L/XL, Màu Đen/Trắng/Be) và danh mục cha-con (Nam, Nữ, Phụ kiện -> Áo sơ mi, Quần tây...). Mỗi biến thể có mã SKU duy nhất và quản lý số lượng tồn kho riêng biệt.

## 4. PREREQUISITES
- PROMPT_020: User, Address & Authentication Database Models

## 5. INPUTS
- Cấu trúc sản phẩm thời trang Routine thực tế và taxonomy danh mục

## 6. DETAILED TASKS
1. **Định nghĩa Model Category**:
   Bao gồm id, name, slug (@unique), description, parentId (Int?, tự liên kết Category), image, status, createdAt, updatedAt.

2. **Định nghĩa Model Product**:
   Bao gồm id, name, slug (@unique), description, originalPrice (Decimal(12,2)), salePrice (Decimal(12,2)?), categoryId (Int), material (String?), fit (String?), styleTag (String?), featuredImage (String), images (Json?), status (String @default("ACTIVE")), views (Int @default(0)), createdAt, updatedAt.

3. **Định nghĩa Model ProductVariant**:
   Bao gồm id, productId (Int), color (String), colorHex (String?), size (String), sku (String @unique), price (Decimal(12,2)?), stock (Int @default(0)), image (String?), createdAt, updatedAt. Thiết lập unique index kép @@unique([productId, color, size]).

## 7. TECHNICAL REQUIREMENTS
- SKU phải duy nhất trên toàn hệ thống (@unique)
- Quan hệ Cascade delete từ Product sang ProductVariant
- Giá dùng kiểu Decimal(12,2) để tránh lỗi số thực
- Cấu hình @@index([categoryId]), @@index([status]), @@index([slug])

## 8. INTEGRATION REQUIREMENTS
- ProductVariant liên kết tới OrderItem, CartItem, StockReservation

## 9. SAFETY CONSTRAINTS
- ⚠️ **Stock Non-negative Constraint**: Tồn kho không được âm, kiểm soát ở mức logic ứng dụng và schema.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Model Category, Product, ProductVariant được bổ sung vào schema.prisma.
[ ] **AC-2**: Ràng buộc unique trên SKU và tổ hợp (productId, color, size) chính xác.
[ ] **AC-3**: npx prisma validate kiểm tra thành công.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Chạy npx prisma validate xác minh cấu trúc quan hệ Product và Variant

## 12. EXPECTED OUTPUT
- `backend/prisma/schema.prisma`: Thêm Category, Product, ProductVariant models

## 13. COMPLETION REPORT
- Mô hình sản phẩm thời trang Routine và danh mục phân cấp được định nghĩa hoàn chỉnh
