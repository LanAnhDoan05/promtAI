# PROMPT 048 – PHASE 03 BACKEND API TEST SUITE & INTEGRATION VERIFICATION GATEWAY

## 1. ROLE
Principal QA Engineer / Lead Backend Architect

## 2. OBJECTIVE
Thực hiện kiểm thử tích hợp tự động toàn diện cho tất cả 18 API module của Phase 03, kiểm tra phân quyền RBAC, mã trạng thái HTTP, và ký duyệt nghiệm thu Gateway 3.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_02_CLOUDINARY_ADMIN_PRODUCT_MANAGEMENT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_02_CLOUDINARY_ADMIN_PRODUCT_MANAGEMENT.md)
> - [USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md)
> - [USER_MASTER_PROMPT_25_PRODUCTION_UPGRADE_NOTIFICATION_HANDOFF.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_25_PRODUCTION_UPGRADE_NOTIFICATION_HANDOFF.md)

## 3. CONTEXT
Gateway 3 là điểm chốt chặn kỹ thuật bắt buộc để xác nhận tầng Backend đã hoàn toàn độc lập, mạnh mẽ và sẵn sàng kết nối với Frontend. Mọi API phải trả về dữ liệu đúng chuẩn hợp đồng RESTful trước khi bước vào thiết kế giao diện.

## 4. PREREQUISITES
- PROMPT_031 đến PROMPT_047

## 5. INPUTS
- Toàn bộ các routes, controllers, services trong backend/src/

## 6. DETAILED TASKS
1. **Kiểm thử Khói (Smoke Test) toàn bộ Endpoints**:
   Chạy bộ test kiểm tra 20+ endpoint chính: Health, Auth, Categories, Products, Search, Cart, Wishlist, Shipping, Coupons, Orders, Reviews, Outfits, Realtime.

2. **Kiểm thử Ma trận Phân quyền RBAC**:
   Kiểm tra 401/403 trên các route Admin và xác thực quyền sở hữu dữ liệu người dùng.

3. **Kiểm thử Tải và Phản hồi**:
   Đo lường thời gian phản hồi trung bình của các API chính, đảm bảo < 150ms.

4. **Lập Báo cáo Nghiệm thu Gateway 3**:
   Xuất bản tài liệu BACKEND_API_ACCEPTANCE_REPORT.md ghi nhận kết quả và ký phê duyệt chuyển giao sang Phase 04 Frontend Design.

## 7. TECHNICAL REQUIREMENTS
- 100% test cases vượt qua không lỗi
- Chuẩn hóa cấu trúc phản hồi { success: true, data: ... } hoặc { success: false, message: ... }

## 8. INTEGRATION REQUIREMENTS
- Cấp phép mở khóa Phase 04 (Frontend Design & Component System)


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Quality Gate Rule**: Bất kỳ lỗi 500 Unhandled Exception nào cũng sẽ chặn quyền vượt qua Gateway 3.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: [ ] AC-1: Toàn bộ các route backend hoạt động ổn định trên cổng 5001.
[ ] **AC-2**: [ ] AC-2: Xác thực JWT và phân quyền RBAC được kiểm thử an toàn.
[ ] **AC-3**: [ ] AC-3: Quy trình tạo đơn và tính phí ship hoạt động chính xác.
[ ] **AC-4**: [ ] AC-4: Báo cáo nghiệm thu Gateway 3 được phê duyệt.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Chạy script kiểm thử tích hợp API tự động với 25+ assertions

## 12. EXPECTED OUTPUT
- `docs/BACKEND_API_ACCEPTANCE_REPORT.md`: Báo cáo nghiệm thu chất lượng tầng Backend API

## 13. COMPLETION REPORT
- Ký duyệt Gateway 3: Cấp phép bắt đầu Phase 04 Frontend Design
