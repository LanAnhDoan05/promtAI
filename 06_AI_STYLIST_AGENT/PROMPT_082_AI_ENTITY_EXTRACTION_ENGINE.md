# PROMPT 082 – ENTITY EXTRACTION ENGINE (OCCASION, GENDER, BUDGET, CATEGORY, COLOR, SIZE)

## 1. ROLE
AI NLP Engineer

## 2. OBJECTIVE
Xây dựng động cơ trích xuất thực thể (Named Entity Extraction): Tự động rút trích các tham số mua sắm quan trọng từ tin nhắn người dùng: Giới tính (Nam, Nữ), Dịp mặc (Đi làm, Tiệc, Dạo phố, Thu Đông), Ngân sách (dưới 500k, 1 triệu, tầm trung), Danh mục đồ (Áo sơ mi, Quần tây), Màu sắc (Đen, Be), Chiều cao/Cân nặng (1m70, 65kg).


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_01_AI_AGENT_AND_DEMO_COMPLETION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_01_AI_AGENT_AND_DEMO_COMPLETION.md)
> - [USER_MASTER_PROMPT_16_AI_STYLIST_AND_SALES_STANDARDS.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_16_AI_STYLIST_AND_SALES_STANDARDS.md)
> - [USER_MASTER_PROMPT_18_VNPAY_QR_AND_AI_HUMAN_HANDOFF.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_18_VNPAY_QR_AND_AI_HUMAN_HANDOFF.md)
> - [USER_MASTER_PROMPT_19_AI_CONTEXTUAL_CONVERSATION_FIX.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_19_AI_CONTEXTUAL_CONVERSATION_FIX.md)

## 3. CONTEXT
Các thực thể này là điều kiện đầu vào (filter criteria) để truy vấn chính xác danh mục sản phẩm trong cơ sở dữ liệu MySQL của Routine.

## 4. PREREQUISITES
- PROMPT_081: AI Intent Router

## 5. INPUTS
- Câu thoại của người dùng

## 6. DETAILED TASKS
1. **Trích xuất Chiều cao, Cân nặng và Size**:
   Sử dụng regex thông minh bắt các mẫu: "1m\d{2}", "\d{2,3}kg", "nặng \d{2}", "cao \d{2,3}", "size [smlxSMLX]+".

2. **Trích xuất Khoảng Giá và Ngân Sách (Budget)**:
   Bắt các mẫu: "dưới \d+k", "tầm \d+ triệu", "khoảng \d+ trăm", chuyển đổi thành số nguyên VNĐ (ví dụ: "dưới 500k" -> maxPrice = 500000).

3. **Kết hợp Prompt Structured Output của Gemini**:
   Yêu cầu Gemini trích xuất dạng JSON Schema chuẩn: { gender, occasion, category, color, size, height, weight, minPrice, maxPrice }.

## 7. TECHNICAL REQUIREMENTS
- Gemini response_mime_type: "application/json"
- Tự động tích lũy thực thể qua các lượt nói (entity persistence qua các turn)

## 8. INTEGRATION REQUIREMENTS
- Dữ liệu thực thể được truyền trực tiếp vào Database Grounding Engine


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Hallucinated Entities**: Loại bỏ các thực thể không liên quan đến thời trang.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Câu "Em muốn tìm set đồ đi làm tầm 1 triệu màu be" trích xuất chính xác: occasion: "Đi làm", maxPrice: 1000000, color: "Be".
[ ] **AC-2**: Thực thể được cấu trúc thành đối tượng JSON rõ ràng.
[ ] **AC-3**: Xử lý linh hoạt các cách viết tắt (k, tr, củ, lit).

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm thử trích xuất trên 15 câu thoại có cấu trúc phức tạp

## 12. EXPECTED OUTPUT
- `backend/src/services/aiEntityExtractor.js`: Động cơ trích xuất thực thể thời trang

## 13. COMPLETION REPORT
- Hệ thống trích xuất thực thể thời trang Routine hoàn thành
