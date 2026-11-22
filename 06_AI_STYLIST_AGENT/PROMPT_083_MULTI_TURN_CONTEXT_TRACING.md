# PROMPT 083 – MULTI-TURN CONTEXT MANAGEMENT & CONVERSATION HISTORY TRACING

## 1. ROLE
AI Conversational Engineer

## 2. OBJECTIVE
Xây dựng cơ chế quản lý ngữ cảnh đa lượt (Multi-turn Context Management): Theo dõi lịch sử hội thoại lên đến 10 lượt gần nhất, ghi nhớ sở thích đã nêu ở các câu trước (ví dụ: đã chọn áo ở turn 1, turn 2 hỏi "quần nào hợp với áo đó?" thì AI tự hiểu là quần phối với chiếc áo ở turn 1), và duy trì sessionId qua cookie/header.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_01_AI_AGENT_AND_DEMO_COMPLETION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_01_AI_AGENT_AND_DEMO_COMPLETION.md)
> - [USER_MASTER_PROMPT_16_AI_STYLIST_AND_SALES_STANDARDS.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_16_AI_STYLIST_AND_SALES_STANDARDS.md)
> - [USER_MASTER_PROMPT_18_VNPAY_QR_AND_AI_HUMAN_HANDOFF.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_18_VNPAY_QR_AND_AI_HUMAN_HANDOFF.md)
> - [USER_MASTER_PROMPT_19_AI_CONTEXTUAL_CONVERSATION_FIX.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_19_AI_CONTEXTUAL_CONVERSATION_FIX.md)

## 3. CONTEXT
Một trợ lý ảo xuất sắc không trả lời rời rạc từng câu mà phải ghi nhớ dòng chảy câu chuyện của khách hàng để đưa ra tư vấn liền mạch như một stylist con người.

## 4. PREREQUISITES
- PROMPT_026: AI Conversation Model
- PROMPT_082: Entity Extraction

## 5. INPUTS
- SessionId, tin nhắn mới và lịch sử hội thoại từ MySQL

## 6. DETAILED TASKS
1. **Xây dựng ConversationContextManager**:
   Tìm hoặc tạo bản ghi AiConversation trong database theo sessionId. Nạp danh sách tin nhắn cũ sắp xếp theo thời gian (tối đa 10 tin gần nhất).

2. **Định dạng Lịch Sử Gửi Sang Gemini API**:
   Chuyển đổi các tin nhắn thành mảng contents chuẩn của Gemini: { role: "user" | "model", parts: [{ text }] }.

3. **Kỹ thuật Context Summarization & State Merging**:
   Gộp các thuộc tính đã nhận diện ở các turn trước (ví dụ: customerPhone, preferredStyle, budget) vào trạng thái phiên làm việc hiện tại.

## 7. TECHNICAL REQUIREMENTS
- Giới hạn token ngữ cảnh để không vượt context window
- SessionId đồng bộ giữa client và server qua localStorage / cookie

## 8. INTEGRATION REQUIREMENTS
- Được sử dụng trong luồng chính của aiStylistService

## 9. SAFETY CONSTRAINTS
- ⚠️ **Session Hijacking Prevention**: Đảm bảo sessionId ngẫu nhiên có độ dài đủ lớn (UUID v4).

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Hội thoại 5 lượt liên tiếp giữ đúng ngữ cảnh (khách hỏi "còn màu khác không?" AI hiểu là hỏi sản phẩm ở câu trước).
[ ] **AC-2**: Lịch sử được lưu đầy đủ vào MySQL bảng AiConversationMessage.
[ ] **AC-3**: Tải lại trang vẫn giữ nguyên lịch sử trò chuyện trong phiên.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Thực hiện kịch bản test 5 lượt trò chuyện liên tiếp và kiểm tra bộ nhớ ngữ cảnh

## 12. EXPECTED OUTPUT
- `backend/src/services/aiContextManager.js`: Quản lý ngữ cảnh đa lượt hội thoại

## 13. COMPLETION REPORT
- Cơ chế quản lý ngữ cảnh đa lượt hội thoại hoàn thành
