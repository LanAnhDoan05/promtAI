# PROMPT 087 – PURCHASE INTENT DETECTION & LEAD SCORE EVALUATION ENGINE

## 1. ROLE
AI CRM & Growth Engineer

## 2. OBJECTIVE
Xây dựng thuật toán phát hiện ý định mua hàng (Purchase Intent) và chấm điểm khách hàng tiềm năng (Lead Scoring từ 0 đến 100): Tự động phát hiện các tín hiệu mua sắm mạnh mẽ (hỏi giá, hỏi khuyến mãi, hỏi giao hàng hỏa tốc, hỏi size còn không, để lại số điện thoại) để nâng điểm Lead Score và đánh dấu khách hàng tiềm năng trong CRM.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_01_AI_AGENT_AND_DEMO_COMPLETION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_01_AI_AGENT_AND_DEMO_COMPLETION.md)
> - [USER_MASTER_PROMPT_16_AI_STYLIST_AND_SALES_STANDARDS.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_16_AI_STYLIST_AND_SALES_STANDARDS.md)
> - [USER_MASTER_PROMPT_18_VNPAY_QR_AND_AI_HUMAN_HANDOFF.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_18_VNPAY_QR_AND_AI_HUMAN_HANDOFF.md)
> - [USER_MASTER_PROMPT_19_AI_CONTEXTUAL_CONVERSATION_FIX.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_19_AI_CONTEXTUAL_CONVERSATION_FIX.md)

## 3. CONTEXT
Khách hàng có Lead Score cao (> 70) là những người sẵn sàng mua hàng ngay. Hệ thống cần ưu tiên hiển thị những lead này trên bàn làm việc của nhân viên tư vấn để chốt đơn kịp thời.

## 4. PREREQUISITES
- PROMPT_083: Context Tracing
- PROMPT_026: AI Conversation Model

## 5. INPUTS
- Nội dung câu nói, số lượt chat, hành vi xem sản phẩm trong session

## 6. DETAILED TASKS
1. **Xây dựng Ma trận Điểm Tín Hiệu Mua Hàng**:
   +15 điểm khi hỏi size/chiều cao; +20 điểm khi hỏi giá/ship; +25 điểm khi hỏi khuyến mãi/voucher; +40 điểm khi để lại số điện thoại hoặc yêu cầu ship gấp.

2. **Cập nhật Lead Score vào Database Realtime**:
   Cập nhật trường leadScore và leadStatus (HOT nếu > 70, WARM nếu 40-70, COLD nếu < 40) vào bảng AiConversation.

3. **Tự động Kích Hoạt Cảnh Báo Khi Điểm Cao**:
   Nếu leadScore >= 75 và khách có số điện thoại: tự động chuyển cờ handoffRequired = true.

## 7. TECHNICAL REQUIREMENTS
- Chấm điểm phi tuyến tính dựa trên hành vi đa kênh
- Bảo mật thông tin số điện thoại khách hàng

## 8. INTEGRATION REQUIREMENTS
- Đồng bộ trực tiếp sang Admin CRM Consultation Desk


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Score Spikes on Spam**: Không cộng điểm lặp lại nếu người dùng gõ cùng 1 từ khóa nhiều lần.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Khách hàng hỏi size và để lại số điện thoại được chấm Lead Score > 75.
[ ] **AC-2**: Trạng thái chuyển sang HOT trong cơ sở dữ liệu.
[ ] **AC-3**: Admin nhận được thông báo lead tiềm năng ngay lập tức.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Mô phỏng cuộc trò chuyện với các tín hiệu mua hàng và kiểm tra điểm Lead Score

## 12. EXPECTED OUTPUT
- `backend/src/services/aiLeadScorer.js`: Động cơ chấm điểm khách hàng tiềm năng

## 13. COMPLETION REPORT
- Động cơ nhận diện ý định mua và chấm điểm Lead hoàn thành
