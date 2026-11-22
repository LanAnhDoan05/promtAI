# PROMPT 095 – ADMIN EXECUTIVE DASHBOARD WITH KEY METRICS & REVENUE TRENDS

## 1. ROLE
Frontend Data Visualization Specialist

## 2. OBJECTIVE
Xây dựng Dashboard điều hành tổng quan (app/admin/dashboard/page.js): 4 thẻ chỉ số KPI then chốt (Tổng doanh thu, Tổng đơn hàng, Khách hàng mới, Tỷ lệ chuyển đổi), biểu đồ xu hướng doanh thu theo ngày/tháng, bảng 5 đơn hàng mới nhất và danh sách cảnh báo tồn kho sắp hết.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_05_AI_BUSINESS_INTELLIGENCE_AUDIT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_05_AI_BUSINESS_INTELLIGENCE_AUDIT.md)
> - [USER_MASTER_PROMPT_24_ADMIN_NOTIFICATION_CENTER.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_24_ADMIN_NOTIFICATION_CENTER.md)
> - [USER_MASTER_PROMPT_28_AI_BI_IMPLEMENTATION_AND_E2E_AUDIT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_28_AI_BI_IMPLEMENTATION_AND_E2E_AUDIT.md)
> - [USER_MASTER_PROMPT_29_BI_DASHBOARD_TABLES_UI_OPTIMIZATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_29_BI_DASHBOARD_TABLES_UI_OPTIMIZATION.md)

## 3. CONTEXT
Dashboard là nơi người điều hành nắm bắt sức khỏe tài chính và hoạt động kinh doanh của Routine trong nháy mắt mỗi sáng mở máy làm việc.

## 4. PREREQUISITES
- PROMPT_094: Admin Layout
- PROMPT_043: Order Service

## 5. INPUTS
- API GET /api/v1/admin/dashboard/stats

## 6. DETAILED TASKS
1. **Xây dựng 4 Thẻ Chỉ Số KPI (Metric Cards)**:
   1) Doanh thu hôm nay/tháng này (+X% so với kỳ trước); 2) Số đơn hàng mới; 3) Khách hàng mới đăng ký; 4) Tồn kho cần bổ sung.

2. **Biểu Đồ Doanh Thu Thời Gian Thực (Revenue Chart)**:
   Biểu đồ đường/cột thể hiện doanh thu 7 ngày hoặc 30 ngày gần nhất (sử dụng Chart.js hoặc SVG tinh gọn).

3. **Bảng 5 Đơn Hàng Mới Nhất và Cảnh Báo Tồn Kho**:
   Bảng đơn hàng vừa đặt cần duyệt; Bảng các biến thể SKU có tồn kho <= 3 sản phẩm để nhân viên kho nhập hàng bổ sung.

## 7. TECHNICAL REQUIREMENTS
- Format số liệu tiền tệ VNĐ và tỷ lệ % chuẩn xác
- Tự động làm mới dữ liệu sau mỗi 60 giây hoặc khi có sự kiện SSE

## 8. INTEGRATION REQUIREMENTS
- Admin Dashboard API backend


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Performance on Large Dataset**: Chỉ số KPI phải được tính toán từ các câu lệnh query tổng hợp tối ưu, không load toàn bộ bảng Order vào RAM.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Dashboard hiển thị đúng doanh thu và số lượng đơn hàng thực tế trong MySQL.
[ ] **AC-2**: Biểu đồ trực quan, co giãn đẹp mắt trên các kích thước màn hình.
[ ] **AC-3**: Bấm vào đơn hàng mới chuyển nhanh sang trang chi tiết đơn.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm tra khớp số liệu giữa Dashboard và database

## 12. EXPECTED OUTPUT
- `frontend/src/app/admin/dashboard/page.js`: Trang tổng quan quản trị
- `frontend/src/components/Admin/MetricCard.jsx`: Component thẻ chỉ số

## 13. COMPLETION REPORT
- Dashboard điều hành tổng quan Routine hoàn thành
