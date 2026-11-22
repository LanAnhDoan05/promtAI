# PROMPT 081 – AI INTENT CLASSIFICATION & RULE-BASED ROUTER (GREETING, OUTFIT, SIZE, HAND-OFF)

## 1. ROLE
AI Conversational Designer / Backend Engineer

## 2. OBJECTIVE
Xây dựng bộ phân loại ý định (Intent Classification) và định tuyến thông minh (Intent Router): Phân loại câu nói của khách vào các nhóm ý định chính: GREETING (chào hỏi), OUTFIT_RECOMMENDATION (tư vấn phối đồ), PRODUCT_SEARCH (tìm sản phẩm cụ thể), SIZE_ADVICE (tư vấn size/chiều cao cân nặng), ORDER_STATUS (tra cứu đơn hàng), HUMAN_HANDOFF (yêu cầu gặp người thật), và CHITCHAT.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_01_AI_AGENT_AND_DEMO_COMPLETION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_01_AI_AGENT_AND_DEMO_COMPLETION.md)
> - [USER_MASTER_PROMPT_16_AI_STYLIST_AND_SALES_STANDARDS.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_16_AI_STYLIST_AND_SALES_STANDARDS.md)
> - [USER_MASTER_PROMPT_18_VNPAY_QR_AND_AI_HUMAN_HANDOFF.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_18_VNPAY_QR_AND_AI_HUMAN_HANDOFF.md)
> - [USER_MASTER_PROMPT_19_AI_CONTEXTUAL_CONVERSATION_FIX.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_19_AI_CONTEXTUAL_CONVERSATION_FIX.md)

## 3. CONTEXT
Việc định tuyến đúng ý định giúp tối ưu tài nguyên và tốc độ phản hồi: Với câu chào hỏi đơn giản, hệ thống phản hồi tức thì bằng rule-based; với yêu cầu phối đồ phức tạp, chuyển sang gọi Gemini kết hợp Grounding Database.

## 4. PREREQUISITES
- PROMPT_080: Fashion Thesaurus

## 5. INPUTS
- Nội dung tin nhắn khách hàng và lịch sử hội thoại gần nhất

## 6. DETAILED TASKS
1. **Xây dựng Rule-based Regex và Keyword Matcher**:
   Nhận diện nhanh các ý định phổ biến: Gặp người thật ("nhân viên", "tư vấn viên", "gặp người", "hotline"); Chào hỏi ("xin chào", "hello", "hi"); Tra cứu đơn ("đơn hàng", "mã vận đơn", "giao đến đâu").

2. **Sử dụng Gemini Zero-shot Intent Classifier cho các câu phức tạp**:
   Nếu rule-based không chắc chắn: gọi prompt phân loại gọn nhẹ trả về JSON { intent: string, confidence: float }.

3. **Điều phối luồng xử lý (Action Dispatcher)**:
   Định tuyến đến service tương ứng dựa trên intent được phân loại.

## 7. TECHNICAL REQUIREMENTS
- Hybrid approach: Rule-based (tốc độ cao < 1ms) + LLM-based (cho câu linh hoạt)
- Độ chính xác phân loại > 95%

## 8. INTEGRATION REQUIREMENTS
- Module đầu tiên tiếp nhận tin nhắn trong aiStylistService

## 9. SAFETY CONSTRAINTS
- ⚠️ **Handoff Priority**: Ý định HUMAN_HANDOFF phải có độ ưu tiên cao nhất, lập tức kích hoạt thông báo chuyển giao.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Câu "Tôi muốn gặp nhân viên trực tiếp" phân loại chính xác intent HUMAN_HANDOFF.
[ ] **AC-2**: Câu "Cao 1m75 nặng 68kg mặc size gì" phân loại chính xác intent SIZE_ADVICE.
[ ] **AC-3**: Câu "Phối đồ đi đám cưới sang trọng" phân loại chính xác intent OUTFIT_RECOMMENDATION.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Chạy bộ 30 câu test cases kiểm thử ma trận phân loại ý định

## 12. EXPECTED OUTPUT
- `backend/src/services/aiIntentRouter.js`: Bộ định tuyến ý định hội thoại

## 13. COMPLETION REPORT
- Bộ phân loại ý định hội thoại và định tuyến thông minh hoàn thành
