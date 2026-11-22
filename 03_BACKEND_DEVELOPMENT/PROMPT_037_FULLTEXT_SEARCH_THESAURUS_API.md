# PROMPT 037 – FULL-TEXT SEARCH, FASHION THESAURUS & KEYWORD NORMALIZATION API

## 1. ROLE
Backend NLP & Search Specialist

## 2. OBJECTIVE
Xây dựng công cụ tìm kiếm sản phẩm thông minh tích hợp từ điển đồng nghĩa thời trang (Fashion Thesaurus), chuẩn hóa tiếng Việt không dấu và gợi ý từ khóa (Auto-complete).


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_02_CLOUDINARY_ADMIN_PRODUCT_MANAGEMENT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_02_CLOUDINARY_ADMIN_PRODUCT_MANAGEMENT.md)
> - [USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md)
> - [USER_MASTER_PROMPT_25_PRODUCTION_UPGRADE_NOTIFICATION_HANDOFF.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_25_PRODUCTION_UPGRADE_NOTIFICATION_HANDOFF.md)

## 3. CONTEXT
Khách hàng có thể tìm kiếm với các từ đồng nghĩa như "áo phông" -> "áo thun", "quần bò" -> "quần jeans", "sơ mi cộc tay" -> "sơ mi ngắn tay". Hệ thống cần mở rộng từ khóa trước khi truy vấn database để nâng cao tỷ lệ tìm thấy sản phẩm.

## 4. PREREQUISITES
- PROMPT_035: Product Catalog API

## 5. INPUTS
- File backend/src/utils/fashionThesaurus.js chứa bộ từ điển từ đồng nghĩa thời trang

## 6. DETAILED TASKS
1. **Xây dựng FashionThesaurus Utility**:
   Tạo từ điển ánh xạ các cụm từ đồng nghĩa phổ biến trong ngành thời trang Việt Nam, hàm expandKeywords(query) mở rộng chuỗi tìm kiếm.

2. **Xây dựng SearchService với chuẩn hóa tiếng Việt**:
   Tách từ, loại bỏ dấu (normalize Vietnamese text), tạo các điều kiện OR trên name, description, material, styleTag, category.name.

3. **Xây dựng API Auto-complete Gợi ý nhanh**:
   GET /api/v1/search/suggestions?q=... trả về top 5 từ khóa phổ biến và top 4 sản phẩm khớp nhất.

## 7. TECHNICAL REQUIREMENTS
- Chuẩn hóa Unicode tiếng Việt NFC
- Tìm kiếm không phân biệt hoa thường và không phân biệt có/không dấu
- Tốc độ gợi ý tức thì < 50ms

## 8. INTEGRATION REQUIREMENTS
- Frontend SearchBar Modal và Search Results Page gọi API này


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **SQL Injection Prevention**: Toàn bộ từ khóa tìm kiếm phải được escape hoặc truyền qua Prisma parameterized query.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Tìm kiếm từ "áo phông" trả về kết quả chứa cả "áo thun".
[ ] **AC-2**: Tìm kiếm không dấu "quan jean" trả về kết quả "Quần Jeans".
[ ] **AC-3**: Endpoint suggestions trả về mảng kết quả phù hợp.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm thử tìm kiếm với các từ đồng nghĩa khác nhau trong từ điển thời trang

## 12. EXPECTED OUTPUT
- `backend/src/utils/fashionThesaurus.js`: Bộ từ điển đồng nghĩa thời trang
- `backend/src/services/searchService.js`: Dịch vụ tìm kiếm mở rộng
- `backend/src/controllers/searchController.js`: Controller tìm kiếm

## 13. COMPLETION REPORT
- Hệ thống tìm kiếm thời trang thông minh đã hoàn thành
