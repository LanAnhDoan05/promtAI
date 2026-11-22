# PROMPT 078 – PHASE 05 END-TO-END CUSTOMER PURCHASE JOURNEY VERIFICATION GATEWAY

## 1. ROLE
Lead QA Automation Engineer / Principal Architect

## 2. OBJECTIVE
Thực hiện kiểm thử chấp nhận toàn trình (End-to-End Customer Purchase Journey) cho toàn bộ Phase 05: Đăng ký -> Nhận voucher chào mừng -> Duyệt sản phẩm -> Chọn size/màu -> Thêm giỏ hàng -> Áp mã giảm giá -> Điền địa chỉ tính phí ship -> Đặt hàng COD -> Nhận mã đơn và in hóa đơn -> Kiểm tra đơn hàng trong lịch sử, và ký duyệt Gateway 5.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_21_ADDRESS_VALIDATION_AI_CONSULTATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_21_ADDRESS_VALIDATION_AI_CONSULTATION.md)
> - [USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md)

## 3. CONTEXT
Gateway 5 là chốt chặn quan trọng nhất của phân hệ Thương mại điện tử B2C. Toàn bộ hành trình khách hàng từ lúc vào web đến khi hoàn tất đơn hàng phải trơn tru 100% không gặp bất kỳ lỗi logic hay giao diện nào.

## 4. PREREQUISITES
- PROMPT_063 đến PROMPT_077

## 5. INPUTS
- Toàn bộ các tính năng thương mại điện tử đã xây dựng

## 6. DETAILED TASKS
1. **Thực thi kịch bản E2E Mua hàng hoàn chỉnh**:
   1) Đăng ký tài khoản mới; 2) Nhận voucher WELCOME10; 3) Thêm 2 sản phẩm vào giỏ; 4) Áp dụng mã giảm giá; 5) Điền địa chỉ giao hàng và kiểm tra phí ship tự động; 6) Chọn phương thức COD; 7) Gửi đơn hàng; 8) Xác minh trang Order Success và in hóa đơn; 9) Vào /account/orders kiểm tra trạng thái đơn.

2. **Kiểm tra Khấu trừ Tồn kho và Voucher**:
   Kiểm tra database: số lượng tồn kho của 2 biến thể sản phẩm đã mua giảm đúng số lượng đặt, usedCount của mã giảm giá tăng thêm 1.

3. **Kiểm tra Xóa sạch Giỏ Hàng**:
   Xác minh giỏ hàng của user sau khi đặt hàng thành công đã trở về 0.

4. **Lập Báo cáo Nghiệm thu Gateway 5**:
   Xuất bản tài liệu ECOMMERCE_E2E_TEST_REPORT.md và ký phê duyệt chuyển giao sang Phase 06 AI Stylist Agent.

## 7. TECHNICAL REQUIREMENTS
- 100% các bước trong kịch bản E2E hoàn thành không lỗi
- Kiểm tra tính nhất quán số liệu trong MySQL database

## 8. INTEGRATION REQUIREMENTS
- Mở khóa triển khai Phase 06 (AI Stylist Agent & Gemini Integration)

## 9. SAFETY CONSTRAINTS
- ⚠️ **Quality Gate Rule**: Nếu có bất kỳ sai lệch nào về tiền tệ hoặc tồn kho, hủy quyền phê duyệt Gateway 5.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: [ ] AC-1: Hành trình mua hàng E2E hoàn tất trọn vẹn từ Đăng ký đến Đặt hàng.
[ ] **AC-2**: [ ] AC-2: Tồn kho sản phẩm và mã giảm giá được trừ chính xác trong MySQL.
[ ] **AC-3**: [ ] AC-3: Giỏ hàng được làm sạch sau khi tạo đơn thành công.
[ ] **AC-4**: [ ] AC-4: Báo cáo nghiệm thu Gateway 5 được phê duyệt.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Chạy kịch bản tự động hóa Playwright/Cypress hoặc kịch bản kiểm thử tích hợp toàn trình

## 12. EXPECTED OUTPUT
- `docs/ECOMMERCE_E2E_TEST_REPORT.md`: Báo cáo kiểm thử hành trình khách hàng toàn trình

## 13. COMPLETION REPORT
- Ký duyệt Gateway 5: Cấp phép bắt đầu Phase 06 AI Stylist Agent
