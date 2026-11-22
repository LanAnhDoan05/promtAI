# PROMPT 010 – THẨM ĐỊNH HỒ SƠ FOUNDATION & PHÊ DUYỆT GATEWAY PHASE 0

## 1. ROLE
Program Director & Technical Audit Lead

## 2. OBJECTIVE
Thực hiện thanh tra, rà soát toàn bộ các tài liệu nền tảng đã lập từ Prompt 001 đến 009, ký duyệt nghiệm thu Gateway Phase 0 để kích hoạt Phase 1.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_06_FULL_SYSTEM_AUDIT_AND_OPTIMIZATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_06_FULL_SYSTEM_AUDIT_AND_OPTIMIZATION.md)
> - [USER_MASTER_PROMPT_22_COMPREHENSIVE_TECHNICAL_AUDIT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_22_COMPREHENSIVE_TECHNICAL_AUDIT.md)
> - [USER_MASTER_PROMPT_30_FROM_ZERO_PROMPT_LIBRARY_SPECIFICATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_30_FROM_ZERO_PROMPT_LIBRARY_SPECIFICATION.md)

## 3. CONTEXT
Gateway 0 là chốt chặn quan trọng nhất để đảm bảo dự án không bị sai lệch hướng đi hoặc thiếu hụt yêu cầu trước khi bắt tay vào code.

## 4. PREREQUISITES
- PROMPT_001 đến PROMPT_009 hoàn thành 100%

## 5. INPUTS
- Toàn bộ các tài liệu trong thư mục `docs/00_*`

## 6. DETAILED TASKS
1. **Thanh tra tính toàn vẹn của hồ sơ tài liệu**:
   Kiểm tra độ đầy đủ của Feasibility, BRD, SRS, Architecture, Coding Standards, API Spec, Security, Data Dictionary và AI Blueprint.

2. **Đối chiếu chéo (Cross-verification)**:
   Đảm bảo không có mâu thuẫn giữa yêu cầu nghiệp vụ trong BRD và thiết kế kỹ thuật trong SRS/Architecture.

3. **Lập biên bản nghiệm thu Gateway Phase 0**:
   Ghi nhận các điểm đạt, các lưu ý rủi ro và phát lệnh cho phép khởi tạo môi trường Phase 1.

## 7. TECHNICAL REQUIREMENTS
- Tất cả 9 tài liệu phải đầy đủ cấu trúc, không có nội dung trống
- Biên bản nghiệm thu lập theo biểu mẫu chuyển giao kỹ thuật chuyên nghiệp

## 8. INTEGRATION REQUIREMENTS
- Thông báo cho toàn thể nhóm phát triển sẵn sàng bước vào giai đoạn cài đặt môi trường.


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Cấm vượt rào**: Không được phép bắt đầu Phase 01 nếu biên bản Gateway 0 chưa được ký duyệt PASS.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Tất cả tiêu chí nghiệm thu của 9 prompt trước đó đạt trạng thái PASS
[ ] **AC-2**: Biên bản nghiệm thu GATEWAY 0 được phát hành chính thức

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Rà soát checklist kiểm định chất lượng tài liệu kiến trúc (100% pass)

## 12. EXPECTED OUTPUT
- `docs/00_GATEWAY_PHASE0_SIGNOFF.md`: Biên bản nghiệm thu chính thức Giai đoạn 0

## 13. COMPLETION REPORT
- Ký duyệt đóng Giai đoạn 0 và chính thức mở khóa Giai đoạn 1 (01_ENVIRONMENT_SETUP).
