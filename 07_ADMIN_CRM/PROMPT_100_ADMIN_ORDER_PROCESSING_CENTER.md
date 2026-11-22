# PROMPT 100 – ADMIN ORDER PROCESSING CENTER, STATUS TRANSITIONS & SHIPPING LABEL PRINTING

## 1. ROLE
Frontend & Logistics Systems Specialist

## 2. OBJECTIVE
Xây dựng Trung tâm xử lý đơn hàng (app/admin/orders/page.js và app/admin/orders/[id]/page.js): Bộ lọc trạng thái đơn hàng (Tất cả, Chờ xử lý, Đã xác nhận, Đang giao, Đã giao, Đã hủy), nút chuyển trạng thái một chạm, chi tiết người nhận và danh sách sản phẩm, và tính năng in phiếu đóng gói/vận đơn (Shipping Label Print).


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_05_AI_BUSINESS_INTELLIGENCE_AUDIT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_05_AI_BUSINESS_INTELLIGENCE_AUDIT.md)
> - [USER_MASTER_PROMPT_24_ADMIN_NOTIFICATION_CENTER.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_24_ADMIN_NOTIFICATION_CENTER.md)
> - [USER_MASTER_PROMPT_28_AI_BI_IMPLEMENTATION_AND_E2E_AUDIT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_28_AI_BI_IMPLEMENTATION_AND_E2E_AUDIT.md)
> - [USER_MASTER_PROMPT_29_BI_DASHBOARD_TABLES_UI_OPTIMIZATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_29_BI_DASHBOARD_TABLES_UI_OPTIMIZATION.md)

## 3. CONTEXT
Nhân viên vận hành Routine sử dụng trang này hàng ngày để xác nhận đơn, in phiếu xuất kho giao cho shipper và theo dõi tiến độ giao hàng.

## 4. PREREQUISITES
- PROMPT_043: Order Lifecycle Service
- PROMPT_094: Admin Layout

## 5. INPUTS
- Order management APIs /api/v1/admin/orders

## 6. DETAILED TASKS
1. **Xây dựng Bảng Danh Sách Đơn Hàng Quản Trị**:
   Hiển thị: Mã đơn, Thời gian, Tên khách hàng & SĐT, Địa chỉ giao hàng, Phương thức thanh toán (COD/VNPAY), Tổng tiền, Trạng thái đơn, Trạng thái thanh toán.

2. **Xây dựng Trang Chi Tiết Đơn Hàng (Order Detail View)**:
   Xem chi tiết các sản phẩm, biến thể size/màu, tiền hàng, phí ship, mã giảm giá. Dropdown chuyển trạng thái tuân thủ đúng State Machine.

3. **Tính Năng In Phiếu Giao Hàng (Shipping Label)**:
   Mẫu in chuẩn A6/A5: Mã vạch/QR đơn hàng, thông tin người gửi Routine, thông tin người nhận, ghi chú giao hàng, danh sách sản phẩm và số tiền thu hộ COD. Nút "In phiếu giao hàng".

## 7. TECHNICAL REQUIREMENTS
- CSS Print media tối ưu cho máy in nhiệt và máy in A4/A5
- Realtime cập nhật khi có đơn hàng mới từ khách

## 8. INTEGRATION REQUIREMENTS
- Order Lifecycle Service và Realtime SSE

## 9. SAFETY CONSTRAINTS
- ⚠️ **Status Transition Validation**: Không cho phép chuyển nhảy cóc trạng thái trái quy tắc.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Chuyển trạng thái đơn hàng từ PENDING sang CONFIRMED thành công.
[ ] **AC-2**: Hủy đơn hàng tự động giải phóng tồn kho.
[ ] **AC-3**: Phiên in phiếu giao hàng mở ra đúng chuẩn kích thước.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Thực hiện chuyển trạng thái 1 đơn hàng qua tất cả các bước

## 12. EXPECTED OUTPUT
- `frontend/src/app/admin/orders/page.js`: Trang quản lý đơn hàng
- `frontend/src/components/Admin/ShippingLabelModal.jsx`: Component in phiếu giao hàng

## 13. COMPLETION REPORT
- Trung tâm xử lý đơn hàng và in phiếu giao hàng hoàn thành
