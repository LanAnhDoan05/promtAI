# PROMPT 091 – MYSQL CONVERSATION PERSISTENCE & SESSION ARCHIVING

## 1. ROLE
Backend Data Persistence Specialist

## 2. OBJECTIVE
Xây dựng cơ chế lưu vết bền vững toàn bộ nội dung trò chuyện vào cơ sở dữ liệu MySQL: Lưu từng tin nhắn (AiConversationMessage), cập nhật thời gian phản hồi, lưu intent, lưu mảng ID sản phẩm gợi ý, và tự động liên kết với userId khi khách hàng đăng nhập.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_01_AI_AGENT_AND_DEMO_COMPLETION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_01_AI_AGENT_AND_DEMO_COMPLETION.md)
> - [USER_MASTER_PROMPT_16_AI_STYLIST_AND_SALES_STANDARDS.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_16_AI_STYLIST_AND_SALES_STANDARDS.md)
> - [USER_MASTER_PROMPT_18_VNPAY_QR_AND_AI_HUMAN_HANDOFF.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_18_VNPAY_QR_AND_AI_HUMAN_HANDOFF.md)
> - [USER_MASTER_PROMPT_19_AI_CONTEXTUAL_CONVERSATION_FIX.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_19_AI_CONTEXTUAL_CONVERSATION_FIX.md)

## 3. CONTEXT
Lưu trữ lịch sử chat phục vụ hai mục đích lớn: 1) Khách hàng không bị mất nội dung khi tải lại trang; 2) Đội ngũ Admin có thể đọc lại toàn bộ nội dung trao đổi khi khách hàng được chuyển giao (Handoff) để tiếp tục tư vấn chính xác.

## 4. PREREQUISITES
- PROMPT_026: AI Conversation Models
- PROMPT_083: Context Tracing

## 5. INPUTS
- Session ID, User ID (nếu có), Content, Sender (USER / AI / STAFF), Intent

## 6. DETAILED TASKS
1. **Xây dựng ConversationRepository**:
   Hàm saveMessage(conversationId, sender, content, intent, recommendedProductIds): thực hiện insert vào bảng AiConversationMessage.

2. **Hàm linkConversationToUser(sessionId, userId)**:
   Khi người dùng đăng nhập thành công: cập nhật trường userId cho bản ghi AiConversation có sessionId tương ứng.

3. **API Lấy Lịch Sử Phiên Chat**:
   GET /api/v1/ai/stylist/history?sessionId=... trả về toàn bộ tin nhắn cũ để client render lại khi mở chatbot.

## 7. TECHNICAL REQUIREMENTS
- Transactional safe writes
- Chỉ mục trên conversationId và createdAt để query lịch sử nhanh < 10ms

## 8. INTEGRATION REQUIREMENTS
- Được gọi ngầm mỗi khi có tin nhắn mới phát sinh trong aiStylistService


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Database Bloat**: Lập kế hoạch dọn dẹp các phiên chat vô danh (guest) không có hoạt động sau 90 ngày.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Mọi câu nói của khách và câu trả lời của AI đều được lưu vào MySQL.
[ ] **AC-2**: F5 tải lại trang nạp lại đầy đủ các tin nhắn cũ từ database.
[ ] **AC-3**: Đăng nhập tài khoản liên kết đúng cuộc trò chuyện vào người dùng đó.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Chat 3 câu, tải lại trang và kiểm tra các câu chat vẫn hiển thị nguyên vẹn

## 12. EXPECTED OUTPUT
- `backend/src/services/aiConversationService.js`: Dịch vụ lưu trữ hội thoại

## 13. COMPLETION REPORT
- Cơ chế lưu vết hội thoại bền vững trong MySQL hoàn thành
