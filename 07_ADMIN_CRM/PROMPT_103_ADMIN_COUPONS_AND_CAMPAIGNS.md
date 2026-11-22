# PROMPT 103 – ADMIN COUPON, PROMOTION & SEASONAL CAMPAIGN MANAGEMENT

## 1. ROLE
Frontend & Backend Promotion Specialist

## 2. OBJECTIVE
Xây dựng trang Quản lý mã giảm giá và chiến dịch khuyến mãi (app/admin/coupons/page.js): Danh sách các mã coupon, form tạo mã mới (Mã code, loại giảm % hoặc số tiền, giá trị đơn tối thiểu, mức giảm tối đa, giới hạn lượt dùng, thời gian bắt đầu/kết thúc), và theo dõi số lượt đã sử dụng.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_05_AI_BUSINESS_INTELLIGENCE_AUDIT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_05_AI_BUSINESS_INTELLIGENCE_AUDIT.md)
> - [USER_MASTER_PROMPT_24_ADMIN_NOTIFICATION_CENTER.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_24_ADMIN_NOTIFICATION_CENTER.md)
> - [USER_MASTER_PROMPT_28_AI_BI_IMPLEMENTATION_AND_E2E_AUDIT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_28_AI_BI_IMPLEMENTATION_AND_E2E_AUDIT.md)
> - [USER_MASTER_PROMPT_29_BI_DASHBOARD_TABLES_UI_OPTIMIZATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_29_BI_DASHBOARD_TABLES_UI_OPTIMIZATION.md)

## 3. CONTEXT
Giúp bộ phận tiếp thị Routine phát hành các mã khuyến mãi theo mùa (Flash Sale, Black Friday, Chào mừng BST Thu Đông) và kiểm soát ngân sách giảm giá an toàn.

## 4. PREREQUISITES
- PROMPT_041: Coupon Engine
- PROMPT_094: Admin Layout

## 5. INPUTS
- Coupon APIs trong /api/v1/admin/coupons

## 6. DETAILED TASKS
1. **Xây dựng Bảng Danh Sách Mã Khuyến Mãi**:
   Mã code, Loại giảm giá, Giá trị, Đơn tối thiểu, Số lượt đã dùng/Tổng giới hạn, Thời hạn hiệu lực, Trạng thái (Đang chạy, Hết hạn, Tạm dừng).

2. **Form Tạo Mới / Sửa Mã Giảm Giá**:
   Nhập mã (chữ hoa tự động), chọn loại (PERCENT hoặc FIXED), ngày bắt đầu/kết thúc với date picker, nút Bật/Tắt kích hoạt.

## 7. TECHNICAL REQUIREMENTS
- Validate ngày kết thúc phải lớn hơn ngày bắt đầu
- Code tự động viết hoa và loại bỏ dấu cách

## 8. INTEGRATION REQUIREMENTS
- Coupon Engine kiểm tra trực tiếp từ bảng này


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Discount Abuse Prevention**: Cảnh báo nếu nhân viên thiết lập mức giảm % > 50% hoặc số tiền quá lớn.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Tạo mã mới thành công và áp dụng được ngay trên trang checkout.
[ ] **AC-2**: Chỉnh sửa giới hạn lượt dùng hoạt động chính xác.
[ ] **AC-3**: Hết hạn tự động đổi trạng thái sang Hết hiệu lực.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Tạo một mã TEST20 giảm 20% và áp dụng thử trên storefront

## 12. EXPECTED OUTPUT
- `frontend/src/app/admin/coupons/page.js`: Trang quản lý mã giảm giá

## 13. COMPLETION REPORT
- Hệ thống quản lý mã giảm giá và chiến dịch khuyến mãi hoàn thành
