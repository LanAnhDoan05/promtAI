# PROMPT 003 – LẬP SOFTWARE REQUIREMENTS SPECIFICATION (SRS) CHUẨN IEEE 830

## 1. ROLE
Principal Software Architect

## 2. OBJECTIVE
Chuyển đổi các yêu cầu nghiệp vụ trong BRD thành tài liệu Đặc tả Yêu cầu Kỹ thuật Phần mềm (SRS) chuẩn hóa IEEE 830.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_06_FULL_SYSTEM_AUDIT_AND_OPTIMIZATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_06_FULL_SYSTEM_AUDIT_AND_OPTIMIZATION.md)
> - [USER_MASTER_PROMPT_22_COMPREHENSIVE_TECHNICAL_AUDIT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_22_COMPREHENSIVE_TECHNICAL_AUDIT.md)
> - [USER_MASTER_PROMPT_30_FROM_ZERO_PROMPT_LIBRARY_SPECIFICATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_30_FROM_ZERO_PROMPT_LIBRARY_SPECIFICATION.md)

## 3. CONTEXT
SRS định nghĩa chi tiết các yêu cầu chức năng (Functional Requirements) và phi chức năng (Non-Functional Requirements) làm cơ sở triển khai kỹ thuật.

## 4. PREREQUISITES
- PROMPT_002 hoàn thành

## 5. INPUTS
- docs/00_BUSINESS_REQUIREMENTS_DOCUMENT.md

## 6. DETAILED TASKS
1. **Đặc tả yêu cầu chức năng (FR)**:
   Liệt kê và phân rã chi tiết 50+ chức năng từ Frontend, Backend, AI Agent đến Admin CRM.

2. **Đặc tả yêu cầu phi chức năng (NFR)**:
   Xác định các chỉ số SLA: Khả năng chịu tải (500 CCU), bảo mật (OWASP Top 10), hiệu năng (<1.5s LCP) và độ khả dụng (99.9%).

3. **Xây dựng ma trận truy vết (Traceability Matrix)**:
   Ánh xạ từng yêu cầu nghiệp vụ sang từng yêu cầu phần mềm tương ứng.

## 7. TECHNICAL REQUIREMENTS
- Cấu trúc tài liệu tuân thủ chuẩn IEEE Std 830-1998
- Mỗi yêu cầu chức năng phải có mã định danh duy nhất (ví dụ: FR-AUTH-01, FR-PROD-02)

## 8. INTEGRATION REQUIREMENTS
- Đảm bảo mọi module kỹ thuật được quy định rõ ràng giao diện và định dạng trao đổi dữ liệu JSON.


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Tính rõ ràng**: Không sử dụng các từ ngữ mơ hồ như "nhanh", "dễ dùng", "đẹp" mà phải có tiêu chí đo lường cụ thể.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Tài liệu SRS được thẩm định đạt 100% độ bao phủ các Use Case của BRD
[ ] **AC-2**: Ma trận truy vết yêu cầu (Requirement Traceability Matrix) hoàn tất

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Rà soát tính nhất quán và kiểm tra xung đột giữa các yêu cầu chức năng

## 12. EXPECTED OUTPUT
- `docs/00_SOFTWARE_REQUIREMENT_SPECIFICATION.md`: Tài liệu SRS chuẩn IEEE 830

## 13. COMPLETION REPORT
- Báo cáo nghiệm thu SRS và chuyển giao cho nhóm thiết kế kiến trúc hệ thống.
