# PROMPT 024 – CART, CARTITEM, WISHLIST & WISHLISTITEM SESSION MODELS

## 1. ROLE
Database Architect

## 2. OBJECTIVE
Xây dựng mô hình cơ sở dữ liệu Giỏ hàng (Cart, CartItem) và Danh sách yêu thích (Wishlist, WishlistItem) hỗ trợ cả khách vãng lai (guest session) và khách hàng đã đăng nhập.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_09_REAL_DATA_AND_BUSINESS_LOGIC.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_09_REAL_DATA_AND_BUSINESS_LOGIC.md)
> - [USER_MASTER_PROMPT_13_MYSQL_AI_ADDRESS_SHIPPING_SYNC.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_13_MYSQL_AI_ADDRESS_SHIPPING_SYNC.md)
> - [USER_MASTER_PROMPT_12_ROUTINE_VN_CATALOG_SCRAPING.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_12_ROUTINE_VN_CATALOG_SCRAPING.md)

## 3. CONTEXT
Khách hàng có thể thêm sản phẩm vào giỏ hàng hoặc danh sách yêu thích trước hoặc sau khi đăng nhập. Mô hình cần hỗ trợ sessionId (chuỗi định danh session ẩn danh) và userId (khi đã login), tự động đồng bộ khi khách đăng nhập.

## 4. PREREQUISITES
- PROMPT_021: Category, Product & ProductVariant Models

## 5. INPUTS
- Luồng giỏ hàng và danh sách yêu thích của Routine

## 6. DETAILED TASKS
1. **Định nghĩa Model Cart và CartItem**:
   Cart: id, userId (Int? @unique), sessionId (String? @unique), createdAt, updatedAt. CartItem: id, cartId (Int), variantId (Int), quantity (Int @default(1)), createdAt, updatedAt. Unique index @@unique([cartId, variantId]).

2. **Định nghĩa Model Wishlist và WishlistItem**:
   Wishlist: id, userId (Int @unique), createdAt, updatedAt. WishlistItem: id, wishlistId (Int), productId (Int), createdAt. Unique index @@unique([wishlistId, productId]).

## 7. TECHNICAL REQUIREMENTS
- Mỗi user chỉ có 1 Cart và 1 Wishlist active
- Cascade delete khi xóa Cart thì xóa toàn bộ CartItem
- Index trên sessionId để truy vấn nhanh cho khách vãng lai

## 8. INTEGRATION REQUIREMENTS
- CartItem liên kết tới ProductVariant; WishlistItem liên kết tới Product


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Duplicate Item Prevention**: Unique constraint [cartId, variantId] ngăn trùng lặp mục trong giỏ, ép buộc cộng dồn quantity.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Models Cart, CartItem, Wishlist, WishlistItem được tạo trong schema.prisma.
[ ] **AC-2**: Unique constraints và foreign keys hợp lệ.
[ ] **AC-3**: npx prisma validate kiểm tra thành công.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Chạy npx prisma validate xác nhận cấu trúc giỏ hàng

## 12. EXPECTED OUTPUT
- `backend/prisma/schema.prisma`: Thêm Cart, CartItem, Wishlist, WishlistItem models

## 13. COMPLETION REPORT
- Mô hình giỏ hàng và danh sách yêu thích đã hoàn thành
