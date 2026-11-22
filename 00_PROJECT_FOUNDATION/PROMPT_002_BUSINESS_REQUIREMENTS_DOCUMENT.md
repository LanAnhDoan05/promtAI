# PROMPT 002 – XÂY DỰNG BUSINESS REQUIREMENTS DOCUMENT (BRD)

## 1. ROLE
Lead E-Commerce Business Analyst

## 2. OBJECTIVE
Soạn thảo tài liệu Yêu cầu Nghiệp vụ (BRD) chi tiết hóa toàn bộ các luồng kinh doanh của Routine Platform.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_06_FULL_SYSTEM_AUDIT_AND_OPTIMIZATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_06_FULL_SYSTEM_AUDIT_AND_OPTIMIZATION.md)
> - [USER_MASTER_PROMPT_22_COMPREHENSIVE_TECHNICAL_AUDIT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_22_COMPREHENSIVE_TECHNICAL_AUDIT.md)
> - [USER_MASTER_PROMPT_30_FROM_ZERO_PROMPT_LIBRARY_SPECIFICATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_30_FROM_ZERO_PROMPT_LIBRARY_SPECIFICATION.md)

## 3. CONTEXT
BRD là kim chỉ nam cho các đội ngũ phát triển, kiểm thử và vận hành hiểu rõ từng quy trình nghiệp vụ mua bán, thanh toán và quản trị.

## 4. PREREQUISITES
- PROMPT_001 hoàn thành

## 5. INPUTS
- docs/00_FEASIBILITY_REPORT.md
- Quy trình vận hành kho và bán lẻ Routine

## 6. DETAILED TASKS
1. **Đặc tả nghiệp vụ Khách hàng (Storefront)**:
   Đặc tả luồng xem catalog, tìm kiếm, lọc thuộc tính (size, màu), giỏ hàng, đặt hàng và quản lý tài khoản.

2. **Đặc tả nghiệp vụ Trợ lý AI Stylist**:
   Quy định các kịch bản tư vấn phối đồ, tra cứu size, phát hiện ý định mua hàng và quy trình chuyển giao sang nhân viên tư vấn.

3. **Đặc tả nghiệp vụ Thanh toán & Quản trị**:
   Quy định luồng thanh toán COD/VNPay, xử lý đơn hàng, quản lý kho, CRM khách hàng và phân tích AI BI.

## 7. TECHNICAL REQUIREMENTS
- Định dạng tài liệu theo chuẩn IIBA (International Institute of Business Analysis)
- Các ca sử dụng (Use Cases) phải có sơ đồ luồng dữ liệu (Flowcharts) trực quan

## 8. INTEGRATION REQUIREMENTS
- Liên kết các phòng ban: Marketing, Bán hàng, Kho vận, Chăm sóc khách hàng và Kế toán.


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Tính khả thi nghiệp vụ**: Không đưa vào các yêu cầu vượt quá năng lực xử lý của hệ thống đơn lẻ.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Tài liệu BRD hoàn chỉnh với tối thiểu 15 Use Cases cốt lõi
[ ] **AC-2**: Toàn bộ các bên liên quan ký duyệt bàn giao

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Thực hiện Walkthrough Review toàn bộ kịch bản mua hàng cùng đại diện nghiệp vụ

## 12. EXPECTED OUTPUT
- `docs/00_BUSINESS_REQUIREMENTS_DOCUMENT.md`: Tài liệu BRD hoàn chỉnh của Routine Platform

## 13. COMPLETION REPORT
- Xác nhận bàn giao BRD cho đội ngũ kiến trúc phần mềm xây dựng SRS.
