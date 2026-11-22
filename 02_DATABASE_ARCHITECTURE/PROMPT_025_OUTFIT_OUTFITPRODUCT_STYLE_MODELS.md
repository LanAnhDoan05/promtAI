# PROMPT 025 – OUTFIT, OUTFITPRODUCT & STYLE MODELS FOR SMART MIX & MATCH

## 1. ROLE
AI / Data Modeling Engineer

## 2. OBJECTIVE
Xây dựng mô hình dữ liệu cho tính năng Gợi ý phối đồ thông minh (Smart Outfit) và Phong cách thời trang (Style, Outfit, OutfitProduct).


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_09_REAL_DATA_AND_BUSINESS_LOGIC.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_09_REAL_DATA_AND_BUSINESS_LOGIC.md)
> - [USER_MASTER_PROMPT_13_MYSQL_AI_ADDRESS_SHIPPING_SYNC.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_13_MYSQL_AI_ADDRESS_SHIPPING_SYNC.md)
> - [USER_MASTER_PROMPT_12_ROUTINE_VN_CATALOG_SCRAPING.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_12_ROUTINE_VN_CATALOG_SCRAPING.md)

## 3. CONTEXT
Routine nổi bật với tính năng phối đồ (Mix & Match) cho phép gợi ý combo hoàn chỉnh (Áo sơ mi + Quần âu + Áo khoác/Phụ kiện). Mô hình cần liên kết các sản phẩm theo phong cách (Công sở, Dạo phố, Thu Đông, Minimalist) để AI Stylist và trang Smart Outfit truy xuất.

## 4. PREREQUISITES
- PROMPT_021: Category, Product & ProductVariant Models

## 5. INPUTS
- Cơ cấu phối đồ và catalog phong cách thời trang của Routine

## 6. DETAILED TASKS
1. **Định nghĩa Model Style**:
   Bao gồm id, name, slug (@unique), description, image, createdAt, updatedAt.

2. **Định nghĩa Model Outfit**:
   Bao gồm id, title, slug (@unique), description, styleId (Int?), occasion (String?), gender (String?), image (String?), isActive (Boolean @default(true)), views (Int @default(0)), createdAt, updatedAt.

3. **Định nghĩa Model OutfitProduct (Bảng nối n-n)**:
   Bao gồm id, outfitId (Int), productId (Int), role (String? ví dụ: TOP, BOTTOM, OUTERWEAR, ACCESSORY), isMain (Boolean @default(false)), sortOrder (Int @default(0)). Unique index @@unique([outfitId, productId]).

## 7. TECHNICAL REQUIREMENTS
- Hỗ trợ phân loại role thành phần trang phục (TOP, BOTTOM, OUTERWEAR, ACCESSORY)
- Quan hệ Cascade delete khi xóa Outfit
- Index trên styleId, occasion, gender

## 8. INTEGRATION REQUIREMENTS
- Smart Outfit Service và Gemini AI Stylist grounding query từ bảng này


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Data Integrity**: Đảm bảo mọi productId trong OutfitProduct đều tồn tại và đang active.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Models Style, Outfit, OutfitProduct được thêm vào schema.prisma.
[ ] **AC-2**: Unique index [outfitId, productId] được thiết lập.
[ ] **AC-3**: npx prisma validate kiểm tra thành công.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Chạy npx prisma validate xác nhận cấu trúc bảng outfit

## 12. EXPECTED OUTPUT
- `backend/prisma/schema.prisma`: Thêm Style, Outfit, OutfitProduct models

## 13. COMPLETION REPORT
- Đã định nghĩa hoàn chỉnh mô hình Outfit và phối đồ thời trang
