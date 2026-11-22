# PROMPT 105 – PHASE 07 ADMIN PORTAL & CRM WORKFLOW AUDIT GATEWAY

## 1. ROLE
Principal System Architect / Lead Operations Auditor

## 2. OBJECTIVE
Thực hiện kiểm toán toàn diện toàn bộ 12 phân hệ Quản trị & CRM Phase 07: Bảo mật phiên Admin, Dashboard điều hành, Báo cáo AI BI, Tối ưu bảng biểu, Quản lý sản phẩm SKU, Xử lý đơn hàng, CRM khách hàng, Bàn trực Live Chat SSE, và ký duyệt Gateway 7.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_05_AI_BUSINESS_INTELLIGENCE_AUDIT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_05_AI_BUSINESS_INTELLIGENCE_AUDIT.md)
> - [USER_MASTER_PROMPT_24_ADMIN_NOTIFICATION_CENTER.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_24_ADMIN_NOTIFICATION_CENTER.md)
> - [USER_MASTER_PROMPT_28_AI_BI_IMPLEMENTATION_AND_E2E_AUDIT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_28_AI_BI_IMPLEMENTATION_AND_E2E_AUDIT.md)
> - [USER_MASTER_PROMPT_29_BI_DASHBOARD_TABLES_UI_OPTIMIZATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_29_BI_DASHBOARD_TABLES_UI_OPTIMIZATION.md)

## 3. CONTEXT
Gateway 7 xác nhận toàn bộ hệ thống quản trị nội bộ đã vận hành trơn tru, bảo mật và kết nối thông suốt với Customer Storefront trước khi tích hợp cổng thanh toán VNPay trong Phase 08.

## 4. PREREQUISITES
- PROMPT_094 đến PROMPT_104

## 5. INPUTS
- Toàn bộ các trang và chức năng trong phân hệ Admin

## 6. DETAILED TASKS
1. **Kiểm toán Phân Quyền và Bảo Mật Admin**:
   Kiểm tra chặn truy cập trái phép đối với các tài khoản không có quyền ADMIN.

2. **Kiểm tra Toàn Trình Xử Lý Đơn Hàng Admin**:
   Nhận đơn mới -> Chuyển trạng thái -> In phiếu giao hàng thành công.

3. **Kiểm tra Tính Năng AI BI và Bàn Trực Realtime**:
   Kích hoạt AI BI sinh báo cáo; kiểm tra âm thanh và thông báo SSE khi có Lead mới.

4. **Lập Báo cáo Nghiệm thu Gateway 7**:
   Xuất bản tài liệu USER_ADMIN_ACCEPTANCE_REPORT.md và ký phê duyệt chuyển giao sang Phase 08 VNPay Payment.

## 7. TECHNICAL REQUIREMENTS
- Tất cả các module quản trị phản hồi < 200ms
- Zero unhandled errors trong bảng điều khiển

## 8. INTEGRATION REQUIREMENTS
- Mở khóa triển khai Phase 08 (VNPay Payment Integration)


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Quality Gate Rule**: Bất kỳ lỗ hổng bảo mật nào cho phép vượt quyền vào trang Admin sẽ chặn Gateway 7.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: [ ] AC-1: Các phân hệ Admin hoạt động ổn định và chính xác.
[ ] **AC-2**: [ ] AC-2: Báo cáo AI BI và bàn trực Live Chat SSE vận hành thông suốt.
[ ] **AC-3**: [ ] AC-3: Hai bảng thống kê BI hiển thị hoàn hảo không tràn ngang.
[ ] **AC-4**: [ ] AC-4: Báo cáo nghiệm thu Gateway 7 được phê duyệt.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Duyệt qua tất cả các trang quản trị và kiểm tra chức năng CRUD

## 12. EXPECTED OUTPUT
- `docs/USER_ADMIN_ACCEPTANCE_REPORT.md`: Báo cáo nghiệm thu phân hệ Quản trị Admin và CRM

## 13. COMPLETION REPORT
- Ký duyệt Gateway 7: Cấp phép bắt đầu Phase 08 Payment VNPay
