# PROMPT 036 – PRODUCT VARIANT, SKU & REALTIME STOCK INSPECTION API

## 1. ROLE
Backend API Developer

## 2. OBJECTIVE
Xây dựng API chi tiết sản phẩm thời trang theo slug, bao gồm danh sách biến thể, bảng chọn màu/size ma trận, số lượng tồn kho khả dụng thời gian thực và tự động tăng lượt xem (views).


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_02_CLOUDINARY_ADMIN_PRODUCT_MANAGEMENT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_02_CLOUDINARY_ADMIN_PRODUCT_MANAGEMENT.md)
> - [USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md)
> - [USER_MASTER_PROMPT_25_PRODUCTION_UPGRADE_NOTIFICATION_HANDOFF.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_25_PRODUCTION_UPGRADE_NOTIFICATION_HANDOFF.md)

## 3. CONTEXT
Trang chi tiết sản phẩm (PDP) cần toàn bộ thông tin mô tả chi tiết, bảng size guide, hình ảnh gallery, danh sách biến thể khả dụng, giá khuyến mãi và kiểm tra tồn kho chính xác để vô hiệu hóa các nút size hết hàng.

## 4. PREREQUISITES
- PROMPT_035: Product Catalog API

## 5. INPUTS
- Product slug hoặc id

## 6. DETAILED TASKS
1. **Xây dựng API getProductBySlug**:
   Truy vấn sản phẩm bao gồm Category, Variants, Reviews và Outfits liên quan. Tự động tăng trường views thêm 1 bằng prisma.product.update({ data: { views: { increment: 1 } } }).

2. **Xây dựng API kiểm tra tồn kho thời gian thực**:
   GET /api/v1/products/variants/:variantId/stock tính toán số lượng tồn kho khả dụng: AvailableStock = variant.stock - activeReservations.

3. **Xây dựng API gợi ý sản phẩm liên quan (Related Products)**:
   Lấy top 8 sản phẩm cùng danh mục hoặc cùng styleTag loại trừ chính sản phẩm đang xem.

## 7. TECHNICAL REQUIREMENTS
- Atomic increment cho lượt xem (views)
- Tính toán chính xác số lượng hàng đang bị khóa giữ bởi StockReservation còn hiệu lực

## 8. INTEGRATION REQUIREMENTS
- Frontend Product Detail Page và Cart variant selector gọi API này


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Active Status Check**: Nếu sản phẩm có status != "ACTIVE", chỉ ADMIN mới có quyền xem preview.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: GET /api/v1/products/:slug trả về toàn bộ dữ liệu sản phẩm, danh mục và mảng variants.
[ ] **AC-2**: Mỗi lần gọi API chi tiết thành công, trường views tăng đúng 1 đơn vị.
[ ] **AC-3**: Kiểm tra tồn kho trừ đi chính xác các khoản giữ kho active.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Gọi GET /api/v1/products/ao-so-mi-oxford-routine kiểm tra phản hồi chi tiết

## 12. EXPECTED OUTPUT
- `backend/src/services/productService.js`: Cập nhật thêm getProductBySlug và getRelatedProducts

## 13. COMPLETION REPORT
- API chi tiết sản phẩm và kiểm tra tồn kho thời gian thực đã hoàn thành
