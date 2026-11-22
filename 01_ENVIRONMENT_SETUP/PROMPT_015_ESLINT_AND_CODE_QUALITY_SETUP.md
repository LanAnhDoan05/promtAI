# PROMPT 015 – CẤU HÌNH ESLINT & KIỂM TRA CHẤT LƯỢNG MÃ NGUỒN ĐẠT 0 WARNINGS

## 1. ROLE
Quality Assurance Lead Engineer

## 2. OBJECTIVE
Cấu hình bộ quy tắc ESLint nghiêm ngặt cho Frontend và Backend, thiết lập mục tiêu duy trì 0 errors và 0 warnings.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_04_SELF_TEST_ENVIRONMENT_HANDOVER.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_04_SELF_TEST_ENVIRONMENT_HANDOVER.md)
> - [USER_MASTER_PROMPT_15_ADMIN_CUSTOMER_CONCURRENT_OPS.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_15_ADMIN_CUSTOMER_CONCURRENT_OPS.md)

## 3. CONTEXT
Dự án Routine đặt tiêu chuẩn chất lượng mã nguồn khắt khe, không chấp nhận các lỗi tiềm ẩn do biến thừa, import sai hoặc vi phạm React Hooks.

## 4. PREREQUISITES
- PROMPT_012, PROMPT_013 hoàn thành

## 5. INPUTS
- docs/00_CODING_STANDARDS.md

## 6. DETAILED TASKS
1. **Cấu hình ESLint cho Frontend**:
   Tạo `frontend/.eslintrc.json` kế thừa `eslint-config-next`, cấu hình quy tắc React Hooks và kiểm tra biến không sử dụng (`no-unused-vars`).

2. **Cấu hình ESLint cho Backend**:
   Cấu hình kiểm tra cú pháp Node.js, không cho phép hàm async không có catch hoặc Promise rò rỉ.

3. **Tạo script kiểm tra tự động trong package.json**:
   Thêm lệnh `"lint": "eslint ."` và `"lint:fix": "eslint . --fix"`.

## 7. TECHNICAL REQUIREMENTS
- ESLint phiên bản 8.x hoặc 9.x tương thích Next.js 16
- Tuyệt đối không bỏ qua các quy tắc kiểm tra tiêu chuẩn

## 8. INTEGRATION REQUIREMENTS
- Tích hợp lệnh lint vào quy trình kiểm tra chất lượng trước khi build.


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Cấm comment tắt cảnh báo**: Nghiêm cấm lạm dụng `eslint-disable-next-line` để che giấu lỗi code.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Chạy `npm run lint` trong `frontend/` trả về kết quả 0 errors, 0 warnings
[ ] **AC-2**: Chạy `npm run lint` trong `backend/` trả về kết quả 0 errors, 0 warnings

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Tạo một file mẫu vi phạm quy chuẩn để xác nhận ESLint bắt lỗi chính xác

## 12. EXPECTED OUTPUT
- `frontend/.eslintrc.json`: Cấu hình ESLint chuẩn cho Frontend
- `backend/.eslintrc.json`: Cấu hình ESLint chuẩn cho Backend

## 13. COMPLETION REPORT
- Báo cáo hệ thống linter đã được kích hoạt và đạt chuẩn 0 warnings.
