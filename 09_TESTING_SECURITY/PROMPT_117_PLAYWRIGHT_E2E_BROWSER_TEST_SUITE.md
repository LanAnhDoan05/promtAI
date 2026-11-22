# PROMPT 117 – PLAYWRIGHT E2E BROWSER TEST SUITE (GUEST CHECKOUT, USER LOGIN, CART, VNPAY)

## 1. ROLE
Lead QA Automation Engineer

## 2. OBJECTIVE
Xây dựng bộ kịch bản kiểm thử tự động trên trình duyệt thật sử dụng Playwright: 1) Luồng khách vãng lai duyệt hàng, thêm giỏ và checkout; 2) Luồng đăng nhập, xem đơn hàng cũ; 3) Luồng thanh toán VNPay QR; 4) Luồng kiểm tra responsive trên giao diện di động và máy tính.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_03_FULL_SYSTEM_ACCEPTANCE_TESTING.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_03_FULL_SYSTEM_ACCEPTANCE_TESTING.md)
> - [USER_MASTER_PROMPT_08_FINAL_REGRESSION_AND_HANDOVER.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_08_FINAL_REGRESSION_AND_HANDOVER.md)
> - [USER_MASTER_PROMPT_17_SYSTEM_STABILITY_FINAL_ACCEPTANCE.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_17_SYSTEM_STABILITY_FINAL_ACCEPTANCE.md)
> - [USER_MASTER_PROMPT_20_FINAL_E2E_INTEGRATION_TEST.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_20_FINAL_E2E_INTEGRATION_TEST.md)

## 3. CONTEXT
Kiểm thử trình duyệt thật mô phỏng chính xác hành vi click, gõ chữ, cuộn trang của người dùng thực tế, phát hiện các lỗi giao diện và lỗi tương tác mà unit test không thể bắt được.

## 4. PREREQUISITES
- PROMPT_062: Frontend UI Sanity
- PROMPT_078: Customer Journey Gateway

## 5. INPUTS
- Playwright test framework cấu hình trong frontend/tests/e2e/

## 6. DETAILED TASKS
1. **Cài đặt và Cấu hình Playwright**:
   Cài đặt @playwright/test, cấu hình playwright.config.js với các thiết bị: Desktop Chrome, Desktop Safari, Mobile Chrome (Pixel 5), Mobile Safari (iPhone 12).

2. **Viết Test Case 1: Đăng Ký và Mua Hàng Trọn Trình**:
   Mở trang chủ -> Bấm Đăng ký -> Điền thông tin -> Vào trang sản phẩm -> Chọn màu/size -> Thêm giỏ -> Vào Checkout -> Điền địa chỉ -> Chọn COD -> Bấm Đặt hàng -> Kiểm tra trang thành công.

3. **Viết Test Case 2: Kiểm Tra Giỏ Hàng và Khuyến Mãi**:
   Thêm sản phẩm -> Vào trang /cart -> Nhập mã giảm giá -> Kiểm tra số tiền giảm -> Tăng giảm số lượng -> Xóa sản phẩm.

4. **Chụp Ảnh Màn Hình Tự Động (Visual Artifacts)**:
   Tự động chụp ảnh screenshot tại các bước quan trọng để làm bằng chứng nghiệm thu (Acceptance Evidence).

## 7. TECHNICAL REQUIREMENTS
- @playwright/test ^1.40.0
- Chạy headless hoặc headed mode
- Tự động ghi hình video khi test case thất bại

## 8. INTEGRATION REQUIREMENTS
- Tích hợp vào quy trình CI/CD

## 9. SAFETY CONSTRAINTS
- ⚠️ **Flaky Tests Prevention**: Sử dụng auto-waiting và web-first assertions của Playwright, tránh dùng waitForTimeout cứng.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Toàn bộ các test cases Playwright chạy qua thành công (Passed).
[ ] **AC-2**: Ảnh chụp màn hình các bước checkout được lưu đầy đủ.
[ ] **AC-3**: Không phát hiện lỗi layout hay nút bấm không click được.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Chạy npx playwright test và xuất báo cáo HTML report

## 12. EXPECTED OUTPUT
- `frontend/tests/e2e/checkout.spec.js`: Kịch bản Playwright E2E
- `docs/FINAL_E2E_TEST_REPORT.md`: Báo cáo kiểm thử trình duyệt thực tế

## 13. COMPLETION REPORT
- Bộ kịch bản kiểm thử trình duyệt Playwright E2E hoàn thành
