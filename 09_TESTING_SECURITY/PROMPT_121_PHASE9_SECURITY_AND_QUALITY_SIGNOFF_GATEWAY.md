# PROMPT 121 – PHASE 09 FINAL SYSTEM SECURITY, QUALITY & STABILITY SIGNOFF GATEWAY

## 1. ROLE
Chief Technology Officer / Principal QA Architect

## 2. OBJECTIVE
Thực hiện đánh giá tổng kết và ký phê duyệt chứng chỉ chất lượng & an toàn toàn hệ thống (Gateway 9): Tổng hợp kết quả từ toàn bộ 7 phân hệ kiểm thử (Unit test, Penetration test, Concurrency test, Playwright E2E, AI Accuracy, Responsive UI, SSE Stress), đảm bảo zero critical bug, zero security breach, và ký phê duyệt chuyển giao sang Phase 10 Triển khai thực tế.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_03_FULL_SYSTEM_ACCEPTANCE_TESTING.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_03_FULL_SYSTEM_ACCEPTANCE_TESTING.md)
> - [USER_MASTER_PROMPT_08_FINAL_REGRESSION_AND_HANDOVER.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_08_FINAL_REGRESSION_AND_HANDOVER.md)
> - [USER_MASTER_PROMPT_17_SYSTEM_STABILITY_FINAL_ACCEPTANCE.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_17_SYSTEM_STABILITY_FINAL_ACCEPTANCE.md)
> - [USER_MASTER_PROMPT_20_FINAL_E2E_INTEGRATION_TEST.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_20_FINAL_E2E_INTEGRATION_TEST.md)

## 3. CONTEXT
Gateway 9 là bước kiểm tra nghiêm ngặt cuối cùng trước khi đưa hệ thống lên môi trường Production. Không một dòng code nào có lỗ hổng bảo mật hoặc lỗi nghiêm trọng được phép đi qua chốt chặn này.

## 4. PREREQUISITES
- PROMPT_114 đến PROMPT_120

## 5. INPUTS
- Tất cả các báo cáo kiểm thử và chứng chỉ nghiệm thu từ Phase 00 đến Phase 09

## 6. DETAILED TASKS
1. **Kiểm toán Tổng Thể 100% Tiêu Chí Chất Lượng**:
   Kiểm tra bảng checklist 50+ mục tiêu kỹ thuật: Tính đúng đắn của dữ liệu, bảo mật API, hiệu năng tải trang, giao dịch VNPay, và độ thông minh của AI.

2. **Kiểm tra Tình Trạng Cảnh Báo và Lỗi Mã Nguồn**:
   Xác nhận mã nguồn không có lỗi biên dịch (0 error), các cảnh báo đã được kiểm soát và ghi nhận lý do an toàn.

3. **Ký Phê Duyệt Báo Cáo Nghiệm Thu Gateway 9**:
   Xuất bản tài liệu FINAL_SYSTEM_STABILITY_AUDIT.md và ký phê duyệt chính thức cho phép bắt đầu Phase 10 Deployment Finalization.

## 7. TECHNICAL REQUIREMENTS
- Zero Blocking Issues
- 100% Gateways từ 0 đến 8 đã được thông qua hợp lệ

## 8. INTEGRATION REQUIREMENTS
- Mở khóa triển khai Phase 10 (Deployment & Production Go-Live)

## 9. SAFETY CONSTRAINTS
- ⚠️ **Final Quality Gate Rule**: Nếu còn bất kỳ bài kiểm tra nào thất bại chưa được khắc phục, từ chối cấp phép chuyển giao.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: [ ] AC-1: Toàn bộ các bộ kiểm thử tự động, bảo mật và hiệu năng vượt qua thành công.
[ ] **AC-2**: [ ] AC-2: Hệ thống chứng minh tính ổn định dưới tải cao và không có lỗi rò rỉ bộ nhớ.
[ ] **AC-3**: [ ] AC-3: Báo cáo nghiệm thu an toàn và ổn định hệ thống được phê duyệt.
[ ] **AC-4**: [ ] AC-4: Ký duyệt Gateway 9 thành công.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Duyệt toàn bộ kết quả kiểm thử tự động và ký biên bản nghiệm thu

## 12. EXPECTED OUTPUT
- `docs/FINAL_SYSTEM_STABILITY_AUDIT.md`: Báo cáo kiểm toán độ ổn định và an toàn toàn hệ thống

## 13. COMPLETION REPORT
- Ký duyệt Gateway 9: Cấp phép bắt đầu Phase 10 Deployment & Production Go-Live
