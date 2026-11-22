# PROMPT 088 – HUMAN HANDOFF WORKFLOW & CONSULTATION NOTIFICATION TRIGGER

## 1. ROLE
AI Workflow & Realtime Engineer

## 2. OBJECTIVE
Xây dựng quy trình chuyển giao hội thoại từ AI sang Chuyên viên tư vấn (Human Handoff): Khi khách yêu cầu gặp người thật hoặc để lại số điện thoại, AI phản hồi lịch sự cam kết thời gian liên hệ, cập nhật trạng thái handoffRequired = true trong MySQL, và phát thông báo SSE tức thì đến Admin Portal.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_01_AI_AGENT_AND_DEMO_COMPLETION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_01_AI_AGENT_AND_DEMO_COMPLETION.md)
> - [USER_MASTER_PROMPT_16_AI_STYLIST_AND_SALES_STANDARDS.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_16_AI_STYLIST_AND_SALES_STANDARDS.md)
> - [USER_MASTER_PROMPT_18_VNPAY_QR_AND_AI_HUMAN_HANDOFF.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_18_VNPAY_QR_AND_AI_HUMAN_HANDOFF.md)
> - [USER_MASTER_PROMPT_19_AI_CONTEXTUAL_CONVERSATION_FIX.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_19_AI_CONTEXTUAL_CONVERSATION_FIX.md)

## 3. CONTEXT
AI không thể thay thế hoàn toàn con người trong các tình huống tư vấn cá nhân hóa cao cấp. Quy trình bàn giao liền mạch giúp nhân viên nắm bắt toàn bộ lịch sử tư vấn của AI trước đó để tiếp tục hỗ trợ khách hàng không bị gián đoạn.

## 4. PREREQUISITES
- PROMPT_087: Lead Scoring
- PROMPT_047: SSE Broadcaster

## 5. INPUTS
- SessionId, Tên khách hàng, Số điện thoại, Tóm tắt nhu cầu

## 6. DETAILED TASKS
1. **Xử lý Logic Chuyển Giao trong Backend**:
   Cập nhật AiConversation: handoffRequired = true, customerName, customerPhone, leadStatus = "CONSULTING". Tạo bản ghi Notification type = "AI_LEAD".

2. **Phát Sự Kiện Realtime SSE đến Admin**:
   Gọi realtimeService.notifyAiLeadHandoff({ conversationId, customerName, customerPhone, summary, leadScore }).

3. **Sinh Lời Thoại Chuyển Giao Ấm Áp của AI**:
   AI gửi tin nhắn: "Routine đã ghi nhận thông tin của Quý khách (SĐT: 09xx xxx xxx). Chuyên viên tư vấn thời trang của Routine sẽ liên hệ lại qua Zalo/Điện thoại trong vòng 5-10 phút để hỗ trợ chi tiết nhất!".

## 7. TECHNICAL REQUIREMENTS
- Thời gian phát hiện và đẩy thông báo SSE < 1 giây
- Tự động tóm tắt ngắn gọn nhu cầu (Summary) bằng Gemini

## 8. INTEGRATION REQUIREMENTS
- Admin Consultation Desk tiếp quản phiên chat

## 9. SAFETY CONSTRAINTS
- ⚠️ **Repeated Handoff Flood**: Chỉ gửi 1 thông báo SSE duy nhất cho mỗi phiên hội thoại trừ khi khách cập nhật thông tin mới.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Khách gửi "Gọi tư vấn cho tôi số 0912345678" kích hoạt ngay quy trình chuyển giao.
[ ] **AC-2**: Bảng điều khiển Admin nhận được thông báo âm thanh và pop-up realtime.
[ ] **AC-3**: Lịch sử tư vấn trước đó được tóm tắt rõ ràng.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm thử gửi số điện thoại trong chatbox và kiểm tra sự kiện SSE trên Admin

## 12. EXPECTED OUTPUT
- `backend/src/services/aiHandoffService.js`: Dịch vụ chuyển giao tư vấn viên

## 13. COMPLETION REPORT
- Quy trình Human Handoff và thông báo thời gian thực hoàn thành
