# PROMPT 118 – AI STYLIST 5-TURN CONVERSATION QUALITY & GROUNDING ACCURACY TEST

## 1. ROLE
AI Evaluation & QA Specialist

## 2. OBJECTIVE
Thực hiện đánh giá định lượng chất lượng của trợ lý AI Stylist: Kiểm tra tỷ lệ không ảo giác (Zero-Hallucination Rate > 99%), độ chính xác trích xuất thực thể (> 95%), tính mạch lạc qua 5 lượt trò chuyện liên tiếp, và tỷ lệ chuyển giao Human Handoff thành công khi có số điện thoại.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_03_FULL_SYSTEM_ACCEPTANCE_TESTING.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_03_FULL_SYSTEM_ACCEPTANCE_TESTING.md)
> - [USER_MASTER_PROMPT_08_FINAL_REGRESSION_AND_HANDOVER.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_08_FINAL_REGRESSION_AND_HANDOVER.md)
> - [USER_MASTER_PROMPT_17_SYSTEM_STABILITY_FINAL_ACCEPTANCE.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_17_SYSTEM_STABILITY_FINAL_ACCEPTANCE.md)
> - [USER_MASTER_PROMPT_20_FINAL_E2E_INTEGRATION_TEST.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_20_FINAL_E2E_INTEGRATION_TEST.md)

## 3. CONTEXT
Đánh giá AI đòi hỏi bộ tiêu chí khắt khe để đảm bảo trợ lý thời trang của Routine luôn tư vấn đúng sản phẩm, đúng giá, đúng kích thước và mang lại cảm giác thân thiện, chuyên nghiệp cho khách hàng.

## 4. PREREQUISITES
- PROMPT_093: AI 5-Turn Gateway

## 5. INPUTS
- Bộ 20 kịch bản hội thoại đa dạng (Hỏi size, hỏi màu, hỏi phối đồ tiệc, hỏi đồ đông, hỏi khuyến mãi)

## 6. DETAILED TASKS
1. **Kiểm toán Độ Chính Xác Sản Phẩm Gợi Ý (Grounding Audit)**:
   Đối chiếu mọi sản phẩm được AI đề xuất trong 20 kịch bản với bảng Product trong MySQL. Xác minh 100% ID sản phẩm tồn tại, tên sản phẩm chính xác và giá tiền khớp hoàn toàn.

2. **Đánh Giá Tư Vấn Size Chuẩn Xác (Size Recommendation Eval)**:
   Kiểm tra với các thông số: 1m70 65kg (Size M/L), 1m80 78kg (Size XL), 1m58 48kg (Size S). Xác nhận AI tư vấn size khớp với bảng Size Guide của Routine.

3. **Đánh Giá Tốc Độ Phản Hồi và Tỷ Lệ Lỗi**:
   Đo lường thời gian phản hồi trung bình (P95 latency < 2.5s) và tỷ lệ lỗi mạng khi gọi Gemini API.

## 7. TECHNICAL REQUIREMENTS
- Bộ tiêu chí đánh giá AI Accuracy Framework chuẩn
- Tỷ lệ ảo giác (Hallucination Rate) = 0%

## 8. INTEGRATION REQUIREMENTS
- AI Stylist Service

## 9. SAFETY CONSTRAINTS
- ⚠️ **Zero Tolerance on Fake Stock**: Bất kỳ gợi ý nào về sản phẩm đã hết hàng hoặc sai giá đều bị tính là vi phạm chất lượng.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Tỷ lệ chính xác thông tin sản phẩm đạt 100%.
[ ] **AC-2**: Tư vấn size phù hợp chính xác theo số đo chuẩn.
[ ] **AC-3**: Thời gian phản hồi trung bình dưới 2.5 giây.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Chạy script tự động gửi 20 kịch bản test và đối chiếu kết quả phản hồi với database

## 12. EXPECTED OUTPUT
- `docs/AI_ACCURACY_SECURITY_STANDARD.md`: Báo cáo đánh giá chất lượng và độ chính xác AI

## 13. COMPLETION REPORT
- Đánh giá chất lượng hội thoại và độ chính xác dữ liệu của AI Stylist hoàn thành
