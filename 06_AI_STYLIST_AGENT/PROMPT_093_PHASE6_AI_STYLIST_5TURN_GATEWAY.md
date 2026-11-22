# PROMPT 093 – PHASE 06 AI STYLIST 5-TURN CONVERSATION & GROUNDING VERIFICATION GATEWAY

## 1. ROLE
Principal AI Architect / Lead QA Auditor

## 2. OBJECTIVE
Thực hiện kiểm thử nghiệm thu toàn diện hệ thống AI Stylist theo kịch bản 5 lượt (5-Turn Conversation Workflow): Turn 1 Chào hỏi & Nêu dịp mặc -> Turn 2 Tư vấn Size & Chiều cao -> Turn 3 Gợi ý Set đồ Grounding thực tế -> Turn 4 Hỏi Khuyến mãi & Giá -> Turn 5 Để lại SĐT & Kích hoạt Human Handoff SSE, và ký duyệt Gateway 6.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_01_AI_AGENT_AND_DEMO_COMPLETION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_01_AI_AGENT_AND_DEMO_COMPLETION.md)
> - [USER_MASTER_PROMPT_16_AI_STYLIST_AND_SALES_STANDARDS.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_16_AI_STYLIST_AND_SALES_STANDARDS.md)
> - [USER_MASTER_PROMPT_18_VNPAY_QR_AND_AI_HUMAN_HANDOFF.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_18_VNPAY_QR_AND_AI_HUMAN_HANDOFF.md)
> - [USER_MASTER_PROMPT_19_AI_CONTEXTUAL_CONVERSATION_FIX.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_19_AI_CONTEXTUAL_CONVERSATION_FIX.md)

## 3. CONTEXT
Gateway 6 kiểm chứng toàn bộ chu trình thông minh của AI: từ thấu hiểu ngôn ngữ tự nhiên, trích xuất thực thể, tra cứu dữ liệu thực tế không ảo giác, đến chuyển giao khách hàng tiềm năng cho nhân viên.

## 4. PREREQUISITES
- PROMPT_079 đến PROMPT_092

## 5. INPUTS
- Kịch bản kiểm thử 5-turn chuẩn hóa của Routine

## 6. DETAILED TASKS
1. **Thực thi Kịch bản 5 Lượt Hội Thoại Chuẩn**:
   Turn 1: "Chào Routine, mình cần tìm đồ đi làm lịch sự". Turn 2: "Mình cao 1m73, nặng 67kg thì mặc size gì vừa?". Turn 3: "Phối cho mình một set sơ mi và quần tây tone be". Turn 4: "Set này có áp được mã WELCOME10 không?". Turn 5: "Tư vấn thêm cho mình qua số 0988123456 nhé".

2. **Kiểm toán Độ Chính Xác Dữ Liệu Grounding**:
   Xác minh các sản phẩm được gợi ý ở Turn 3 có thật trong MySQL, còn tồn kho, và đúng size L được khuyến nghị ở Turn 2.

3. **Kiểm tra Chuyển Giao Human Handoff và SSE**:
   Xác minh ở Turn 5: AiConversation chuyển handoffRequired = true, SĐT được lưu, và Admin Portal nhận được thông báo SSE.

4. **Lập Báo cáo Nghiệm thu Gateway 6**:
   Xuất bản tài liệu AI_FIVE_TURN_HANDOFF_E2E_REPORT.md và ký phê duyệt chuyển giao sang Phase 07 Admin CRM.

## 7. TECHNICAL REQUIREMENTS
- Đạt 100% tiêu chí kịch bản 5-turn
- Thời gian phản hồi mỗi turn < 3 giây

## 8. INTEGRATION REQUIREMENTS
- Mở khóa triển khai Phase 07 (Admin Portal & CRM Management)

## 9. SAFETY CONSTRAINTS
- ⚠️ **Quality Gate Rule**: Nếu có bất kỳ sản phẩm ảo giác (hallucination) nào xuất hiện trong 5 turn, hủy quyền phê duyệt Gateway 6.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: [ ] AC-1: Hội thoại 5 lượt hoàn tất trọn vẹn, giữ vững ngữ cảnh liền mạch.
[ ] **AC-2**: [ ] AC-2: 100% sản phẩm gợi ý là sản phẩm có thật từ MySQL database.
[ ] **AC-3**: [ ] AC-3: Sự kiện chuyển giao nhân viên phát sóng SSE thành công đến Admin.
[ ] **AC-4**: [ ] AC-4: Báo cáo nghiệm thu Gateway 6 được phê duyệt.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Chạy script tự động hóa kiểm thử 5 lượt chat và lắng nghe SSE socket

## 12. EXPECTED OUTPUT
- `docs/AI_FIVE_TURN_HANDOFF_E2E_REPORT.md`: Báo cáo nghiệm thu chu trình AI 5 lượt toàn diện

## 13. COMPLETION REPORT
- Ký duyệt Gateway 6: Cấp phép bắt đầu Phase 07 Admin CRM
