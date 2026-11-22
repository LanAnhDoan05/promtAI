# PROMPT 114 – AUTOMATED BACKEND UNIT & INTEGRATION TEST SUITE (JEST / SUPERTEST)

## 1. ROLE
Senior QA Automation Engineer

## 2. OBJECTIVE
Xây dựng bộ kiểm thử tự động toàn diện cho tầng Backend sử dụng Jest và Supertest: Kiểm thử đơn vị (Unit Tests) cho các hàm tiện ích (Haversine distance, Fashion thesaurus, Coupon calculate, Password hash) và kiểm thử tích hợp (Integration Tests) cho 10 luồng API cốt lõi.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_03_FULL_SYSTEM_ACCEPTANCE_TESTING.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_03_FULL_SYSTEM_ACCEPTANCE_TESTING.md)
> - [USER_MASTER_PROMPT_08_FINAL_REGRESSION_AND_HANDOVER.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_08_FINAL_REGRESSION_AND_HANDOVER.md)
> - [USER_MASTER_PROMPT_17_SYSTEM_STABILITY_FINAL_ACCEPTANCE.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_17_SYSTEM_STABILITY_FINAL_ACCEPTANCE.md)
> - [USER_MASTER_PROMPT_20_FINAL_E2E_INTEGRATION_TEST.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_20_FINAL_E2E_INTEGRATION_TEST.md)

## 3. CONTEXT
Bộ test tự động đảm bảo khi có bất kỳ thay đổi mã nguồn nào trong tương lai, các chức năng nghiệp vụ cốt lõi không bao giờ bị lỗi hồi quy (Regression).

## 4. PREREQUISITES
- PROMPT_048: Backend API Suite
- PROMPT_030: Database Seed

## 5. INPUTS
- Toàn bộ mã nguồn backend trong backend/src/

## 6. DETAILED TASKS
1. **Cài đặt và Cấu hình Jest trong backend**:
   Cấu hình jest.config.js, thiết lập testEnvironment: "node", cấu hình setupFilesAfterEnv để kết nối test database an toàn.

2. **Viết Bộ Unit Tests cho Core Utils**:
   Viết test cho geoDistance.test.js (tính khoảng cách km), couponEngine.test.js (tính giảm giá % và max discount), fashionThesaurus.test.js (mở rộng từ đồng nghĩa).

3. **Viết Bộ Integration Tests cho API Routes**:
   Sử dụng supertest gửi HTTP request kiểm thử: Auth API (đăng ký, đăng nhập sai/đúng), Products API (lọc, phân trang), Cart API (thêm, cập nhật tồn kho).

## 7. TECHNICAL REQUIREMENTS
- Code coverage tối thiểu > 75% cho các dịch vụ cốt lõi
- Test suite thực thi độc lập không làm ô nhiễm database chính

## 8. INTEGRATION REQUIREMENTS
- Tích hợp vào npm test trong backend/package.json

## 9. SAFETY CONSTRAINTS
- ⚠️ **Production Database Guard**: Tuyệt đối không chạy bộ test trên Production Database (phải dùng test database riêng).

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Lệnh npm test trong backend chạy thành công 100% không có test case thất bại.
[ ] **AC-2**: Bao phủ đầy đủ các trường hợp biên (boundary cases) của tính toán tài chính.
[ ] **AC-3**: Thời gian chạy toàn bộ test suite < 30 giây.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Chạy npm test trong thư mục backend và ghi nhận kết quả

## 12. EXPECTED OUTPUT
- `backend/tests/unit/geoDistance.test.js`: Unit test tính khoảng cách
- `backend/tests/unit/coupon.test.js`: Unit test mã giảm giá
- `backend/tests/integration/auth.test.js`: Integration test xác thực

## 13. COMPLETION REPORT
- Bộ kiểm thử tự động Unit & Integration Tests hoàn thành
