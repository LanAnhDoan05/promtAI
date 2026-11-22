# PROMPT 085 – GEMINI FUNCTION CALLING / TOOL DEFINITION FOR CATALOG SEARCH

## 1. ROLE
AI Tool Integration Specialist

## 2. OBJECTIVE
Xây dựng cơ chế Gọi Hàm (Function Calling / Tool Calling) cho Gemini: Định nghĩa các công cụ search_routine_catalog, check_size_availability, get_outfit_combo và handle_consultation_handoff trong khai báo tools của Gemini API.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_01_AI_AGENT_AND_DEMO_COMPLETION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_01_AI_AGENT_AND_DEMO_COMPLETION.md)
> - [USER_MASTER_PROMPT_16_AI_STYLIST_AND_SALES_STANDARDS.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_16_AI_STYLIST_AND_SALES_STANDARDS.md)
> - [USER_MASTER_PROMPT_18_VNPAY_QR_AND_AI_HUMAN_HANDOFF.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_18_VNPAY_QR_AND_AI_HUMAN_HANDOFF.md)
> - [USER_MASTER_PROMPT_19_AI_CONTEXTUAL_CONVERSATION_FIX.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_19_AI_CONTEXTUAL_CONVERSATION_FIX.md)

## 3. CONTEXT
Function Calling cho phép Gemini tự quyết định khi nào cần tra cứu kho hàng hoặc chuyển giao nhân viên, trả về tên hàm và tham số chuẩn JSON để backend thực thi truy vấn an toàn.

## 4. PREREQUISITES
- PROMPT_079: Gemini Client
- PROMPT_084: Grounding Service

## 5. INPUTS
- Đặc tả Schema các function tools theo chuẩn OpenAPI

## 6. DETAILED TASKS
1. **Khai báo Function search_routine_catalog**:
   Parameters: query (string), category (string), color (string), maxPrice (number), occasion (string). Mô tả: "Tìm kiếm danh sách sản phẩm quần áo Routine thực tế trong kho".

2. **Khai báo Function check_size_availability**:
   Parameters: productId (number), height (number), weight (number). Mô tả: "Tư vấn kích thước (size S, M, L, XL) và kiểm tra còn hàng cho khách hàng".

3. **Khai báo Function trigger_human_handoff**:
   Parameters: customerName (string), customerPhone (string), reason (string), summary (string). Mô tả: "Chuyển giao khách hàng cho chuyên viên tư vấn Routine khi có nhu cầu cao hoặc yêu cầu trực tiếp".

4. **Vòng lặp Thực Thi Tool và Phản Hồi Kết Quả**:
   Khi Gemini trả về functionCall: backend gọi hàm tương ứng, nhận kết quả JSON và gửi lại cho Gemini (functionResponse) để sinh câu trả lời tự nhiên cuối cùng.

## 7. TECHNICAL REQUIREMENTS
- Gemini Function Calling API chuẩn
- Xử lý timeout khi tool chạy quá 5 giây

## 8. INTEGRATION REQUIREMENTS
- Được nhúng vào aiStylistService

## 9. SAFETY CONSTRAINTS
- ⚠️ **Tool Parameter Validation**: Validate chặt chẽ các tham số đầu vào do Gemini sinh ra trước khi chạy câu lệnh database.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Gemini tự động gọi search_routine_catalog khi khách hỏi tìm áo/quần.
[ ] **AC-2**: Gemini gọi trigger_human_handoff khi khách để lại số điện thoại.
[ ] **AC-3**: Vòng lặp Tool Call hoàn thành mượt mà trong < 2.5 giây.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Gửi câu hỏi "Tôi muốn tìm áo sơ mi trắng dưới 400k" và kiểm tra Gemini gọi đúng function tool

## 12. EXPECTED OUTPUT
- `backend/src/services/aiTools.js`: Định nghĩa và xử lý công cụ Function Calling

## 13. COMPLETION REPORT
- Hệ thống Function Calling và công cụ tra cứu thông minh cho AI hoàn thành
