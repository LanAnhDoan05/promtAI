# PROMPT 004 – THIẾT KẾ KIẾN TRÚC HỆ THỐNG HIGH-LEVEL (C4 MODEL)

## 1. ROLE
Chief Enterprise Architect

## 2. OBJECTIVE
Xây dựng bản vẽ thiết kế kiến trúc toàn diện theo mô hình C4 (Context, Containers, Components, Code) cho Routine Platform.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_06_FULL_SYSTEM_AUDIT_AND_OPTIMIZATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_06_FULL_SYSTEM_AUDIT_AND_OPTIMIZATION.md)
> - [USER_MASTER_PROMPT_22_COMPREHENSIVE_TECHNICAL_AUDIT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_22_COMPREHENSIVE_TECHNICAL_AUDIT.md)
> - [USER_MASTER_PROMPT_30_FROM_ZERO_PROMPT_LIBRARY_SPECIFICATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_30_FROM_ZERO_PROMPT_LIBRARY_SPECIFICATION.md)

## 3. CONTEXT
Đảm bảo hệ thống có kiến trúc module hóa cao, tách biệt rõ ràng giữa Storefront, API Gateway/Express Backend, MySQL Database và Gemini AI Engine.

## 4. PREREQUISITES
- PROMPT_003 hoàn thành

## 5. INPUTS
- docs/00_SOFTWARE_REQUIREMENT_SPECIFICATION.md

## 6. DETAILED TASKS
1. **Thiết kế C4 Level 1 & Level 2**:
   Vẽ sơ đồ Context và Container thể hiện luồng giao tiếp giữa Next.js, Express, MySQL, VNPay và Gemini.

2. **Thiết kế kiến trúc phân tầng Backend**:
   Mô hình Controller - Service - Repository/Prisma - Database đảm bảo nguyên lý Clean Architecture.

3. **Thiết kế kiến trúc đồng bộ thời gian thực**:
   Xây dựng luồng Server-Sent Events (SSE) `/api/v1/realtime` để đẩy thông báo và live chat.

## 7. TECHNICAL REQUIREMENTS
- Giao thức HTTP/HTTPS RESTful chuẩn RFC 7231
- Sử dụng Mermaid.js để trực quan hóa toàn bộ sơ đồ kiến trúc trong tài liệu Markdown

## 8. INTEGRATION REQUIREMENTS
- Định nghĩa ranh giới kết nối giữa Micro-services hoặc Modular Monolith.


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Ngăn chặn Single Point of Failure (SPOF)**: Có cơ chế Fallback nếu dịch vụ AI Gemini hoặc cổng thanh toán bị gián đoạn.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Sơ đồ C4 Level 1, 2 và 3 được hoàn thành đầy đủ
[ ] **AC-2**: Kiến trúc đáp ứng đầy đủ các chỉ số NFR đã cam kết trong SRS

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Mô phỏng luồng dữ liệu end-to-end trên sơ đồ khối kiến trúc

## 12. EXPECTED OUTPUT
- `docs/00_SYSTEM_ARCHITECTURE_DOCUMENT.md`: Bản thiết kế kiến trúc C4 Model chi tiết

## 13. COMPLETION REPORT
- Hoàn tất thẩm định kiến trúc và chuyển giao cho nhóm quy chuẩn phát triển.
