# PROMPT 026 – AI CONVERSATION, MESSAGE & CONSULTATION LEAD MODELS

## 1. ROLE
AI System Architect / Database Engineer

## 2. OBJECTIVE
Xây dựng mô hình cơ sở dữ liệu lưu trữ phiên hội thoại đa lượt (AiConversation), lịch sử tin nhắn (AiConversationMessage), và hồ sơ lead tư vấn khách hàng (Consultation Lead).


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_09_REAL_DATA_AND_BUSINESS_LOGIC.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_09_REAL_DATA_AND_BUSINESS_LOGIC.md)
> - [USER_MASTER_PROMPT_13_MYSQL_AI_ADDRESS_SHIPPING_SYNC.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_13_MYSQL_AI_ADDRESS_SHIPPING_SYNC.md)
> - [USER_MASTER_PROMPT_12_ROUTINE_VN_CATALOG_SCRAPING.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_12_ROUTINE_VN_CATALOG_SCRAPING.md)

## 3. CONTEXT
Trợ lý AI Stylist hỗ trợ tư vấn thời trang đa lượt và tự động nhận diện nhu cầu mua sắm. Nếu khách hàng có nhu cầu cao hoặc yêu cầu gặp chuyên viên, hệ thống lưu trữ toàn bộ ngữ cảnh hội thoại, số điện thoại, ghi chú và kích hoạt trạng thái handoff (chuyển giao) cho Admin/Staff.

## 4. PREREQUISITES
- PROMPT_020: User, Address Models

## 5. INPUTS
- Quy trình tư vấn AI 5-turn và chuyển giao Handoff của Routine

## 6. DETAILED TASKS
1. **Định nghĩa Model AiConversation**:
   Bao gồm id, sessionId (String @unique), userId (Int?), customerName (String?), customerPhone (String?), occasion (String?), budget (Decimal?), stylePreference (String?), leadStatus (String @default("NEW") - NEW, CONSULTING, CONVERTED, CLOSED), handoffRequired (Boolean @default(false)), agentNotes (Text?), createdAt, updatedAt.

2. **Định nghĩa Model AiConversationMessage**:
   Bao gồm id, conversationId (Int), sender (String - USER, AI, STAFF), content (Text), recommendedProductIds (Json?), intent (String?), createdAt.

## 7. TECHNICAL REQUIREMENTS
- sessionId là chuỗi UUID/Token duy nhất để theo dõi phiên chat
- Cascade delete từ AiConversation sang AiConversationMessage
- Index trên sessionId, userId, leadStatus, handoffRequired, createdAt

## 8. INTEGRATION REQUIREMENTS
- AI Stylist Service ghi nhận tin nhắn; Admin CRM đọc danh sách Lead và tiếp quản chat qua SSE


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Privacy & Content Sanitize**: Nội dung tin nhắn cần hỗ trợ lưu trữ chuỗi an toàn, mã hóa số điện thoại nếu cần.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Models AiConversation và AiConversationMessage được tạo chuẩn xác trong schema.prisma.
[ ] **AC-2**: Các trường nhận diện lead (phone, budget, occasion, handoffRequired) đầy đủ.
[ ] **AC-3**: npx prisma validate kiểm tra thành công.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Chạy npx prisma validate xác nhận cấu trúc bảng AI Conversation

## 12. EXPECTED OUTPUT
- `backend/prisma/schema.prisma`: Thêm AiConversation và AiConversationMessage models

## 13. COMPLETION REPORT
- Mô hình hội thoại AI Stylist và Lead CRM hoàn thành
