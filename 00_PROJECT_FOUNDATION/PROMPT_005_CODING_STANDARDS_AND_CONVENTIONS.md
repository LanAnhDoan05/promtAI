# PROMPT 005 – XÂY DỰNG QUY CHUẨN CODING STANDARDS & GIT FLOW

## 1. ROLE
Lead DevOps & Code Quality Architect

## 2. OBJECTIVE
Thiết lập bộ quy chuẩn lập trình, phong cách viết mã (Coding Conventions), cấu hình Git Flow và chiến lược rẽ nhánh cho toàn dự án.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_06_FULL_SYSTEM_AUDIT_AND_OPTIMIZATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_06_FULL_SYSTEM_AUDIT_AND_OPTIMIZATION.md)
> - [USER_MASTER_PROMPT_22_COMPREHENSIVE_TECHNICAL_AUDIT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_22_COMPREHENSIVE_TECHNICAL_AUDIT.md)
> - [USER_MASTER_PROMPT_30_FROM_ZERO_PROMPT_LIBRARY_SPECIFICATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_30_FROM_ZERO_PROMPT_LIBRARY_SPECIFICATION.md)

## 3. CONTEXT
Đảm bảo toàn bộ mã nguồn Frontend và Backend đồng nhất, dễ bảo trì, tuân thủ nguyên tắc Clean Code và quy chuẩn ESLint 0 errors, 0 warnings.

## 4. PREREQUISITES
- PROMPT_004 hoàn thành

## 5. INPUTS
- docs/00_SYSTEM_ARCHITECTURE_DOCUMENT.md

## 6. DETAILED TASKS
1. **Quy chuẩn đặt tên (Naming Conventions)**:
   Quy định chuẩn camelCase cho biến/hàm, PascalCase cho React component, kebab-case cho CSS modules và file routes.

2. **Quy chuẩn Git Flow & Commit Lint**:
   Áp dụng Conventional Commits (`feat:`, `fix:`, `docs:`, `refactor:`, `test:`), quy định nhánh `main`, `develop` và feature branches.

3. **Chính sách quản lý lỗi & Zero Warning**:
   Tuyệt đối cấm sử dụng comment vô hiệu hóa linter (`@ts-ignore`, `eslint-disable`).

## 7. TECHNICAL REQUIREMENTS
- Cấu hình Prettier chuẩn (2 spaces, single quotes, semi: true)
- Quy định cấu trúc thư mục module hóa rõ ràng

## 8. INTEGRATION REQUIREMENTS
- Tích hợp linter hooks trước khi commit.


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Cấm đẩy Secrets vào Git**: Bắt buộc kiểm tra `.gitignore` không bao gồm file `.env`, `node_modules` hay chứng chỉ mật.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Tài liệu quy chuẩn lập trình được ban hành
[ ] **AC-2**: File `.editorconfig` và mẫu `.gitignore` được cấu hình chuẩn xác

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm tra định dạng commit thử nghiệm theo chuẩn Conventional Commits

## 12. EXPECTED OUTPUT
- `docs/00_CODING_STANDARDS.md`: Tài liệu quy chuẩn phát triển và quản trị mã nguồn

## 13. COMPLETION REPORT
- Xác nhận ban hành quy chuẩn cho toàn bộ các thành viên phát triển.
