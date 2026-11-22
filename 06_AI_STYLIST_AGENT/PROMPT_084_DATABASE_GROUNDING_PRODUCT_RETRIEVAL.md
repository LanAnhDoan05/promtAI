# PROMPT 084 – DATABASE GROUNDING: REALTIME MYSQL PRODUCT RETRIEVAL ENGINE

## 1. ROLE
AI / Data Integration Specialist

## 2. OBJECTIVE
Xây dựng động cơ neo dữ liệu thực tế (Database Grounding Engine): Truy xuất trực tiếp sản phẩm thật từ MySQL dựa trên các thực thể đã trích xuất, chỉ cung cấp cho Gemini các sản phẩm có thật, đang còn hàng (ACTIVE & stock > 0), có giá bán chính xác và ảnh thật của Routine.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_01_AI_AGENT_AND_DEMO_COMPLETION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_01_AI_AGENT_AND_DEMO_COMPLETION.md)
> - [USER_MASTER_PROMPT_16_AI_STYLIST_AND_SALES_STANDARDS.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_16_AI_STYLIST_AND_SALES_STANDARDS.md)
> - [USER_MASTER_PROMPT_18_VNPAY_QR_AND_AI_HUMAN_HANDOFF.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_18_VNPAY_QR_AND_AI_HUMAN_HANDOFF.md)
> - [USER_MASTER_PROMPT_19_AI_CONTEXTUAL_CONVERSATION_FIX.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_19_AI_CONTEXTUAL_CONVERSATION_FIX.md)
> - ⭐ **Tài liệu tham chiếu trực tiếp:** [USER_MASTER_PROMPT_16_AI_STYLIST_AND_SALES_STANDARDS.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_16_AI_STYLIST_AND_SALES_STANDARDS.md)

## 3. CONTEXT
Vấn đề lớn nhất của LLM là "ảo giác" (hallucination - tự bịa ra sản phẩm không có thật). Database Grounding đảm bảo 100% sản phẩm AI tư vấn cho khách đều mua được ngay trên website.

## 4. PREREQUISITES
- PROMPT_082: Entity Extraction
- PROMPT_035: Product Catalog Service

## 5. INPUTS
- Các thuộc tính lọc: categoryIds, colors, sizes, minPrice, maxPrice, styleTag

## 6. DETAILED TASKS
1. **Xây dựng Hàm retrieveGroundedProducts**:
   Truy vấn bảng Product kết hợp ProductVariant: lọc status = "ACTIVE", tồn kho stock > 0, khớp danh mục hoặc tên, sắp xếp theo độ liên quan hoặc lượt xem. Lấy tối đa 6 sản phẩm khớp nhất.

2. **Định dạng Dữ Liệu Neo (Grounding Context) Cho Gemini**:
   Chuyển thông tin sản phẩm thành chuỗi mô tả ngắn gọn: "[ID: 12] Áo Sơ Mi Oxford Dài Tay - Giá: 399.000đ - Màu: Trắng, Xanh - Size: S, M, L - Link: /products/ao-so-mi-oxford-dai-tay - Đặc điểm: Chất vải cotton thoáng mát, form regular fit".

3. **Ép Buộc Ràng Buộc Neo Trong Prompt**:
   Yêu cầu trong Prompt: "CHỈ ĐƯỢC tư vấn các sản phẩm nằm trong danh sách [GROUNDED_PRODUCTS] dưới đây. Khi nhắc đến sản phẩm, PHẢI ghi rõ ID, tên đầy đủ và giá bán chính xác. TUYỆT ĐỐI KHÔNG giới thiệu bất kỳ sản phẩm nào ngoài danh sách này".


### QUY CHUẨN DATABASE GROUNDING CHỐNG ẢO GIÁC (Theo USER_MASTER_PROMPT_16):
- 100% sản phẩm do AI Stylist tư vấn PHẢI xuất phát từ danh sách sản phẩm thật được truy vấn từ bảng `Product` và `ProductVariant` trong MySQL.
- Bắt buộc kiểm tra `status = "ACTIVE"` và `stock > 0`.
- Khi nhắc đến sản phẩm, AI phải trích dẫn đúng ID, Tên, Giá niêm yết và URL slug hợp lệ.
- TUYỆT ĐỐI KHÔNG giới thiệu sản phẩm không tồn tại trong catalog của Routine.


## 7. TECHNICAL REQUIREMENTS
- Prisma query tối ưu tốc độ < 30ms
- Chống ảo giác (Anti-hallucination) 100%

## 8. INTEGRATION REQUIREMENTS
- Nạp vào prompt gửi sang Gemini API

## 9. SAFETY CONSTRAINTS
- ⚠️ **Out-of-Stock Filter**: Sản phẩm hết hàng tuyệt đối không được đưa vào danh sách Grounding.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Mọi sản phẩm do AI gợi ý đều có ID thật và slug thật trong database.
[ ] **AC-2**: Giá bán trong câu trả lời của AI khớp 100% với giá trong database.
[ ] **AC-3**: Khi không tìm thấy sản phẩm nào trong kho, AI thành thật thông báo và gợi ý danh mục tương đương thay vì bịa đặt.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm thử với câu hỏi về sản phẩm không có trong kho và kiểm tra phản hồi của AI

## 12. EXPECTED OUTPUT
- `backend/src/services/aiGroundingService.js`: Dịch vụ neo dữ liệu sản phẩm thực tế

## 13. COMPLETION REPORT
- Động cơ neo dữ liệu MySQL chống ảo giác cho AI Stylist hoàn thành
