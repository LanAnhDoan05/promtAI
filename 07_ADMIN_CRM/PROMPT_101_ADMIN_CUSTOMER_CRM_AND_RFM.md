# PROMPT 101 – ADMIN CUSTOMER CRM, RFM SEGMENTATION & CUSTOMER LIFETIME VALUE (CLV)

## 1. ROLE
CRM & Marketing Technology Specialist

## 2. OBJECTIVE
Xây dựng phân hệ Quản lý quan hệ khách hàng (app/admin/customers/page.js): Danh sách khách hàng, thống kê số đơn đã mua, tổng chi tiêu (Customer Lifetime Value - CLV), phân nhóm khách hàng theo mô hình RFM (VIP, Tiềm năng, Mới, Nguy cơ rời bỏ), và lịch sử mua sắm của từng khách.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_05_AI_BUSINESS_INTELLIGENCE_AUDIT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_05_AI_BUSINESS_INTELLIGENCE_AUDIT.md)
> - [USER_MASTER_PROMPT_24_ADMIN_NOTIFICATION_CENTER.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_24_ADMIN_NOTIFICATION_CENTER.md)
> - [USER_MASTER_PROMPT_28_AI_BI_IMPLEMENTATION_AND_E2E_AUDIT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_28_AI_BI_IMPLEMENTATION_AND_E2E_AUDIT.md)
> - [USER_MASTER_PROMPT_29_BI_DASHBOARD_TABLES_UI_OPTIMIZATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_29_BI_DASHBOARD_TABLES_UI_OPTIMIZATION.md)

## 3. CONTEXT
Phân tích khách hàng giúp Routine chăm sóc khách hàng thân thiết tốt hơn và gửi các ưu đãi cá nhân hóa để tăng tỷ lệ quay lại mua hàng.

## 4. PREREQUISITES
- PROMPT_020: User Model
- PROMPT_043: Order Service

## 5. INPUTS
- APIs GET /api/v1/admin/customers

## 6. DETAILED TASKS
1. **Xây dựng Thuật Toán Phân Nhóm RFM**:
   Tính toán: Recency (ngày mua gần nhất), Frequency (tần suất mua đơn), Monetary (tổng số tiền chi tiêu). Gán phân nhóm: VIP (> 5 triệu, > 3 đơn), Tiềm năng (1-2 đơn), Nguy cơ rời bỏ (> 90 ngày chưa mua lại).

2. **Xây dựng Bảng Danh Sách Khách Hàng CRM**:
   Họ tên, Email, Số điện thoại, Ngày đăng ký, Tổng chi tiêu CLV, Huy hiệu nhóm RFM (VIP màu vàng, Tiềm năng màu xanh), số đơn hàng.

3. **Trang Hồ Sơ Khách Hàng Chi Tiết**:
   Xem toàn bộ lịch sử mua sắm, các sản phẩm ưa thích, sổ địa chỉ và lịch sử chat với AI Stylist.

## 7. TECHNICAL REQUIREMENTS
- Query tổng hợp SQL tối ưu nhóm theo userId
- Xuất danh sách khách hàng ra file Excel/CSV

## 8. INTEGRATION REQUIREMENTS
- Admin Portal navigation


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Customer Data Privacy**: Ẩn một phần số điện thoại hoặc email đối với tài khoản staff chỉ có quyền đọc hạn chế.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Bảng khách hàng hiển thị đúng tổng chi tiêu và số đơn của từng người.
[ ] **AC-2**: Phân nhóm RFM hiển thị trực quan các khách hàng VIP.
[ ] **AC-3**: Xem được chi tiết lịch sử đơn hàng của từng khách.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm tra tính toán CLV của một khách hàng có 2 đơn hàng

## 12. EXPECTED OUTPUT
- `frontend/src/app/admin/customers/page.js`: Trang quản lý khách hàng CRM

## 13. COMPLETION REPORT
- Phân hệ quản lý khách hàng CRM và phân nhóm RFM hoàn thành
