# PROMPT 104 – ADMIN STORE SETTINGS, SHIPPING RATES & SYSTEM CONFIGURATION

## 1. ROLE
Full-stack Systems Engineer

## 2. OBJECTIVE
Xây dựng trang Cài đặt hệ thống cửa hàng (app/admin/settings/page.js): Cấu hình thông tin thương hiệu (Tên cửa hàng, Hotline, Email, Địa chỉ kho tổng, Tọa độ latitude/longitude), chỉnh sửa bảng phí vận chuyển (shipping_rules: nấc km, cước cơ bản), và cấu hình ngưỡng miễn phí ship.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_05_AI_BUSINESS_INTELLIGENCE_AUDIT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_05_AI_BUSINESS_INTELLIGENCE_AUDIT.md)
> - [USER_MASTER_PROMPT_24_ADMIN_NOTIFICATION_CENTER.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_24_ADMIN_NOTIFICATION_CENTER.md)
> - [USER_MASTER_PROMPT_28_AI_BI_IMPLEMENTATION_AND_E2E_AUDIT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_28_AI_BI_IMPLEMENTATION_AND_E2E_AUDIT.md)
> - [USER_MASTER_PROMPT_29_BI_DASHBOARD_TABLES_UI_OPTIMIZATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_29_BI_DASHBOARD_TABLES_UI_OPTIMIZATION.md)

## 3. CONTEXT
Cho phép người quản trị dễ dàng thay đổi thông tin vận hành và chính sách giao hàng mà không cần phải can thiệp trực tiếp vào mã nguồn hay database.

## 4. PREREQUISITES
- PROMPT_027: StoreSetting Model
- PROMPT_040: Dynamic Shipping Service

## 5. INPUTS
- APIs GET /api/v1/admin/settings và PUT /api/v1/admin/settings

## 6. DETAILED TASKS
1. **Cấu hình Thông Tin Cửa Hàng & Kho Tổng**:
   Tên thương hiệu, địa chỉ kho xuất hàng chính, tọa độ GPS (phục vụ tính khoảng cách km cho mọi đơn hàng).

2. **Bảng Điều Chỉnh Biểu Phí Vận Chuyển (shipping_rules)**:
   Xem và chỉnh sửa trực tiếp 4 nấc khoảng cách km, cước cơ bản và cước mỗi km phụ thu.

3. **Cài đặt Ngưỡng Miễn Phí Vận Chuyển**:
   Thiết lập giá trị đơn hàng tối thiểu để được Freeship (mặc định 500.000đ).

## 7. TECHNICAL REQUIREMENTS
- Lưu trữ dạng key-value trong bảng StoreSetting
- Cập nhật có hiệu lực ngay lập tức cho các đơn hàng tiếp theo

## 8. INTEGRATION REQUIREMENTS
- ShippingService đọc trực tiếp từ các cài đặt này


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Zero Lat/Lng Validation**: Không cho phép để trống tọa độ kho tổng.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Thay đổi cước vận chuyển lưu thành công vào MySQL.
[ ] **AC-2**: Đơn hàng tính cước theo mức phí mới ngay sau khi lưu.
[ ] **AC-3**: Thông tin liên hệ cửa hàng cập nhật đồng bộ lên Footer.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Đổi mức cước nội thành từ 15k lên 20k và kiểm tra tính cước tại checkout

## 12. EXPECTED OUTPUT
- `frontend/src/app/admin/settings/page.js`: Trang cài đặt hệ thống

## 13. COMPLETION REPORT
- Trang cài đặt hệ thống và biểu phí vận chuyển hoàn thành
