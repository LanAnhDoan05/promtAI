# PROMPT 092 – AI SAFETY GUARDRAILS, ANTI-HALLUCINATION & RATE-LIMITING FALLBACK RULES

## 1. ROLE
AI Safety & Security Engineer

## 2. OBJECTIVE
Thiết lập hàng rào an toàn cho AI (AI Safety Guardrails): Chặn các câu hỏi không liên quan đến thời trang/Routine (chính trị, tôn giáo, đối thủ cạnh tranh), ngăn chặn kỹ thuật bẻ khóa prompt (Jailbreak / Prompt Injection), giới hạn tần suất gửi tin (Rate Limiting: tối đa 20 tin/phút/IP), và cơ chế Fallback bằng luật cứng (Rule Engine) khi Gemini API gặp sự cố hoặc mất mạng.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_01_AI_AGENT_AND_DEMO_COMPLETION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_01_AI_AGENT_AND_DEMO_COMPLETION.md)
> - [USER_MASTER_PROMPT_16_AI_STYLIST_AND_SALES_STANDARDS.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_16_AI_STYLIST_AND_SALES_STANDARDS.md)
> - [USER_MASTER_PROMPT_18_VNPAY_QR_AND_AI_HUMAN_HANDOFF.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_18_VNPAY_QR_AND_AI_HUMAN_HANDOFF.md)
> - [USER_MASTER_PROMPT_19_AI_CONTEXTUAL_CONVERSATION_FIX.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_19_AI_CONTEXTUAL_CONVERSATION_FIX.md)

## 3. CONTEXT
Một AI công cộng cần bảo vệ uy tín thương hiệu. Khi Gemini API quá tải hoặc ngắt kết nối, hệ thống vẫn phải phản hồi lịch sự bằng các kịch bản định sẵn thay vì báo lỗi server 500.

## 4. PREREQUISITES
- PROMPT_079: Gemini Client
- PROMPT_081: Intent Router

## 5. INPUTS
- Tin nhắn người dùng và trạng thái sức khỏe của Gemini API

## 6. DETAILED TASKS
1. **Xây dựng Bộ Lọc Nội Dung Độc Hại và Chủ Đề Cấm (Guardrails)**:
   Kiểm tra danh sách từ khóa cấm và các mẫu câu tấn công prompt injection ("bỏ qua chỉ thị trước", "hãy đóng vai hacker"). Nếu vi phạm, AI từ chối khéo léo: "Tôi là Trợ lý Thời trang Routine và chỉ hỗ trợ các câu hỏi liên quan đến sản phẩm, phối đồ và dịch vụ của Routine".

2. **Cơ Chế Giới Hạn Tần Suất (Rate Limiter)**:
   Sử dụng express-rate-limit giới hạn 20 request/phút cho mỗi IP đối với endpoint /api/v1/ai/stylist/chat.

3. **Động Cơ Kịch Bản Dự Phòng (Rule-based Fallback Engine)**:
   Khi Gemini trả về lỗi 503 hoặc timeout: tự động chuyển sang kịch bản tĩnh dựa trên từ khóa (ví dụ: thấy từ "sơ mi" thì trả về danh sách 4 áo sơ mi bán chạy nhất kèm lời xin lỗi nhẹ nhàng).

## 7. TECHNICAL REQUIREMENTS
- Fail-safe architecture: Không bao giờ để lộ lỗi kỹ thuật ra màn hình chat
- Fallback phản hồi dưới 50ms

## 8. INTEGRATION REQUIREMENTS
- Bao bọc luồng gọi Gemini trong try-catch với fallback

## 9. SAFETY CONSTRAINTS
- ⚠️ **Brand Reputation Protection**: Tuyệt đối không để AI nhắc đến tiêu cực về thương hiệu Routine hoặc khen ngợi đối thủ.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Gửi câu hỏi độc hại hoặc prompt injection bị chặn và từ chối an toàn.
[ ] **AC-2**: Spam 25 tin nhắn trong 1 phút nhận HTTP 429 Too Many Requests.
[ ] **AC-3**: Ngắt kết nối internet của Gemini, hệ thống tự động trả lời bằng kịch bản dự phòng.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm thử gửi 5 câu hỏi tấn công prompt injection và mô phỏng lỗi API Gemini

## 12. EXPECTED OUTPUT
- `backend/src/services/aiGuardrailService.js`: Hàng rào an toàn và kịch bản dự phòng

## 13. COMPLETION REPORT
- Hàng rào an toàn AI Guardrails và kịch bản dự phòng hoàn thành
