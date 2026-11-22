# PROMPT 045 – SMART OUTFIT GENERATION & STYLE RECOMMENDATION SERVICE

## 1. ROLE
AI / Fashion Recommendation Specialist

## 2. OBJECTIVE
Xây dựng API phối đồ thông minh (Smart Outfit): Lấy danh sách outfit theo phong cách/dịp mặc, gợi ý các món đồ đi kèm (Mix & Match) cho một sản phẩm cụ thể, và tính tổng giá combo ưu đãi.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_02_CLOUDINARY_ADMIN_PRODUCT_MANAGEMENT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_02_CLOUDINARY_ADMIN_PRODUCT_MANAGEMENT.md)
> - [USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md)
> - [USER_MASTER_PROMPT_25_PRODUCTION_UPGRADE_NOTIFICATION_HANDOFF.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_25_PRODUCTION_UPGRADE_NOTIFICATION_HANDOFF.md)

## 3. CONTEXT
Tính năng Smart Outfit của Routine giúp khách hàng phối đồ dễ dàng. Khi xem một chiếc quần tây, hệ thống tự động gợi ý áo sơ mi và phụ kiện thắt lưng phù hợp để tạo thành một outfit hoàn chỉnh.

## 4. PREREQUISITES
- PROMPT_025: Outfit Models
- PROMPT_035: Product Catalog API

## 5. INPUTS
- Style slug, Occasion (Đi làm, Dự tiệc, Đi chơi, Thu đông), hoặc Product ID

## 6. DETAILED TASKS
1. **Xây dựng OutfitService.getOutfits**:
   Lấy danh sách outfits có lọc theo style, occasion, gender; kèm theo các sản phẩm thành phần (TOP, BOTTOM, ACCESSORY).

2. **Xây dựng OutfitService.getOutfitRecommendationsForProduct**:
   Tìm các bộ outfit có chứa sản phẩm hiện tại, hoặc tự động tìm các sản phẩm bổ trợ (nếu xem áo TOP thì tìm quần BOTTOM cùng tone màu và phong cách).

3. **Tạo Endpoints trong api.js**:
   GET /api/v1/outfits, GET /api/v1/outfits/:slug, GET /api/v1/outfits/recommend/:productId.

## 7. TECHNICAL REQUIREMENTS
- Cấu trúc combo bao gồm ít nhất 2 sản phẩm (Áo + Quần)
- Hỗ trợ thêm toàn bộ outfit vào giỏ hàng trong 1 click

## 8. INTEGRATION REQUIREMENTS
- Frontend Smart Outfit page và trang chi tiết sản phẩm (PDP)


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Active Items Only**: Chỉ hiển thị các món đồ trong outfit đang có trạng thái ACTIVE và còn tồn kho.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: GET /api/v1/outfits trả về danh sách combo kèm chi tiết các sản phẩm thành phần.
[ ] **AC-2**: Gợi ý phối đồ cho sản phẩm trả về các món bổ trợ hợp lý.
[ ] **AC-3**: API phản hồi nhanh chóng dưới 100ms.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm thử lấy danh sách outfit theo dịp mặc "di-lam" và "thu-dong"

## 12. EXPECTED OUTPUT
- `backend/src/services/outfitService.js`: Dịch vụ phối đồ thời trang thông minh
- `backend/src/controllers/outfitController.js`: Controller Outfit

## 13. COMPLETION REPORT
- Dịch vụ phối đồ Smart Outfit đã hoàn thành
