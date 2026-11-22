# PROMPT 080 – VIETNAMESE FASHION THESAURUS & KEYWORD SEMANTIC MAPPING ENGINE

## 1. ROLE
NLP Engineer / Fashion Domain Specialist

## 2. OBJECTIVE
Xây dựng bộ từ điển đồng nghĩa thời trang (Fashion Thesaurus) và động cơ ánh xạ ngữ nghĩa tiếng Việt: Nhận diện các thuật ngữ thời trang đa dạng (áo cộc, áo phông, áo sơ mi tơ, quần âu, quần tây, quần bò, áo blazer, măng tô, tone be, tone pastel), chuẩn hóa về danh mục và đặc tính sản phẩm trong catalog Routine.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_01_AI_AGENT_AND_DEMO_COMPLETION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_01_AI_AGENT_AND_DEMO_COMPLETION.md)
> - [USER_MASTER_PROMPT_16_AI_STYLIST_AND_SALES_STANDARDS.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_16_AI_STYLIST_AND_SALES_STANDARDS.md)
> - [USER_MASTER_PROMPT_18_VNPAY_QR_AND_AI_HUMAN_HANDOFF.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_18_VNPAY_QR_AND_AI_HUMAN_HANDOFF.md)
> - [USER_MASTER_PROMPT_19_AI_CONTEXTUAL_CONVERSATION_FIX.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_19_AI_CONTEXTUAL_CONVERSATION_FIX.md)

## 3. CONTEXT
Khách hàng Việt Nam sử dụng ngôn ngữ địa phương và cách gọi phong phú. Động cơ ánh xạ giúp hiểu chính xác mong muốn của khách để làm tiền đề cho việc truy vấn database chuẩn xác.

## 4. PREREQUISITES
- PROMPT_079: Gemini Client

## 5. INPUTS
- Danh mục sản phẩm, bảng thuộc tính màu sắc, chất liệu và phong cách Routine

## 6. DETAILED TASKS
1. **Mở rộng Bộ Từ Điển Đồng Nghĩa backend/src/utils/fashionThesaurus.js**:
   Định nghĩa các nhóm từ: 1) Áo (Top): sơ mi, polo, thun, tee, khoác, jacket, hoodie, blazer; 2) Quần (Bottom): âu, tây, kaki, chino, bò, jean, shorts, culottes; 3) Màu sắc: be, kem, rêu, navy, đen, trắng, pastel; 4) Dịp mặc: đi làm, công sở, đi chơi, hẹn hò, dự tiệc, đi biển, thu đông.

2. **Xây dựng Thuật toán Chuẩn Hóa và Trích Xuất Ngữ Nghĩa**:
   Hàm parseFashionKeywords(text): chuẩn hóa tiếng Việt, tìm các từ khóa khớp trong từ điển và trả về mảng thuộc tính chuẩn hóa { categories, colors, occasions, styles }.

## 7. TECHNICAL REQUIREMENTS
- Xử lý tiếng Việt có dấu và không dấu
- Khớp từ ghép (compound words) như "áo sơ mi cộc tay", "quần tây ống suông"

## 8. INTEGRATION REQUIREMENTS
- Được gọi bởi AI Intent Router và Database Grounding Engine

## 9. SAFETY CONSTRAINTS
- ⚠️ **False Positive Mappings**: Không ánh xạ nhầm các từ ngữ thông thường thành từ khóa thời trang.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Cụm từ "tìm cho mình cái quần bò đi chơi" trích xuất được: category: "Quần Jeans", occasion: "Dạo phố".
[ ] **AC-2**: Cụm từ "áo cộc tay màu kem" trích xuất được: category: "Áo ngắn tay", color: "Be/Kem".
[ ] **AC-3**: Hàm xử lý phản hồi dưới 5ms.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Chạy unit test kiểm thử 20 mẫu câu hội thoại tiếng Việt điển hình

## 12. EXPECTED OUTPUT
- `backend/src/utils/fashionThesaurus.js`: Từ điển đồng nghĩa thời trang nâng cao

## 13. COMPLETION REPORT
- Động cơ ánh xạ ngữ nghĩa thời trang tiếng Việt hoàn thành
