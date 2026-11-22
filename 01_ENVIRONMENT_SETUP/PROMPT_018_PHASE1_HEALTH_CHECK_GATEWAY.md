# PROMPT 018 – KIỂM TRA SỨC KHỎE MÔI TRƯỜNG & KÝ DUYỆT GATEWAY PHASE 1

## 1. ROLE
DevOps & Quality Assurance Lead

## 2. OBJECTIVE
Kiểm tra toàn diện tính sẵn sàng của môi trường phát triển Frontend và Backend, ký duyệt Gateway Phase 1 để mở khóa giai đoạn thiết kế Cơ sở dữ liệu.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_04_SELF_TEST_ENVIRONMENT_HANDOVER.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_04_SELF_TEST_ENVIRONMENT_HANDOVER.md)
> - [USER_MASTER_PROMPT_15_ADMIN_CUSTOMER_CONCURRENT_OPS.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_15_ADMIN_CUSTOMER_CONCURRENT_OPS.md)

## 3. CONTEXT
Đảm bảo môi trường phát triển sạch sẽ, không có lỗi cấu hình và tuân thủ các quy chuẩn kỹ thuật đã đề ra.

## 4. PREREQUISITES
- PROMPT_011 đến PROMPT_017 hoàn thành 100%

## 5. INPUTS
- Toàn bộ mã nguồn và cấu hình đã tạo trong Phase 01

## 6. DETAILED TASKS
1. **Kiểm tra trạng thái máy chủ Backend**:
   Gửi request kiểm tra `/api/v1/health`, kiểm tra log khởi động và việc nạp biến môi trường.

2. **Kiểm tra máy chủ Frontend Next.js**:
   Kiểm tra quá trình render SSR trang chủ trên cổng 3000, kiểm tra hiển thị hình ảnh tĩnh.

3. **Kiểm tra chất lượng mã nguồn (Lint Check)**:
   Chạy linter trên cả hai phân hệ, xác nhận đạt 0 errors và 0 warnings.

4. **Lập biên bản nghiệm thu Gateway Phase 1**:
   Lập báo cáo đánh giá và ký duyệt chuyển giao sang Phase 2.

## 7. TECHNICAL REQUIREMENTS
- Tất cả các bài kiểm tra sức khỏe phải đạt 100%
- Biên bản nghiệm thu ghi rõ phiên bản Node, Next.js, Express đã cài đặt

## 8. INTEGRATION REQUIREMENTS
- Thông báo cho nhóm Database Architect sẵn sàng cài đặt Prisma và MySQL.


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Cấm vượt rào**: Không tiến hành cài đặt Database nếu môi trường chạy thử nghiệm chưa ổn định.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Backend trả về HTTP 200 Healthy
[ ] **AC-2**: Frontend hiển thị giao diện mượt mà không có lỗi console
[ ] **AC-3**: ESLint đạt chuẩn 0 warnings trên toàn bộ dự án

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Thực thi kịch bản kiểm tra sức khỏe liên thông tự động

## 12. EXPECTED OUTPUT
- `docs/01_GATEWAY_PHASE1_SIGNOFF.md`: Biên bản nghiệm thu chính thức Giai đoạn 1

## 13. COMPLETION REPORT
- Ký duyệt đóng Giai đoạn 1 và mở khóa Giai đoạn 2 (02_DATABASE_ARCHITECTURE).
