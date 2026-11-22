# PROMPT 076 – CUSTOMER ORDER HISTORY & REALTIME TRACKING TIMELINE

## 1. ROLE
Frontend UI/UX Specialist

## 2. OBJECTIVE
Xây dựng trang Lịch sử đơn hàng của khách hàng (app/account/orders/page.js): Danh sách các đơn hàng đã đặt (phân loại tab: Tất cả, Chờ xử lý, Đang giao, Đã giao, Đã hủy), dòng thời gian theo dõi tiến độ giao hàng (Tracking Timeline: Đặt đơn -> Xác nhận -> Đang đóng gói -> Đang giao -> Hoàn thành), và nút "Hủy đơn" (nếu đơn còn ở trạng thái Chờ xử lý).


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_21_ADDRESS_VALIDATION_AI_CONSULTATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_21_ADDRESS_VALIDATION_AI_CONSULTATION.md)
> - [USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md)

## 3. CONTEXT
Khách hàng cần theo dõi sát sao đơn hàng của mình đang ở giai đoạn nào. Dòng thời gian trực quan giúp khách biết rõ thời điểm dự kiến nhận hàng.

## 4. PREREQUISITES
- PROMPT_043: Order Lifecycle Service
- PROMPT_063: UserContext

## 5. INPUTS
- Danh sách đơn hàng của User từ API /api/v1/orders

## 6. DETAILED TASKS
1. **Xây dựng Thanh Phân Loại Trạng Thái Đơn Hàng (Tabs)**:
   Các tab: Tất cả, Chờ xác nhận, Đang xử lý, Đang vận chuyển, Đã giao hàng, Đã hủy.

2. **Thẻ Hiển Thị Đơn Hàng (Order Card)**:
   Mã đơn, ngày đặt, danh sách sản phẩm thu gọn, tổng số tiền, huy hiệu trạng thái (status badge). Nút "Xem chi tiết" mở trang /account/orders/[id].

3. **Dòng Thời Gian Theo Dõi (Tracking Timeline)**:
   Thanh tiến trình 5 bước với các mốc trạng thái kèm ngày giờ cập nhật cụ thể.

4. **Hành Động Hủy Đơn Hàng (Cancel Order)**:
   Nếu trạng thái là PENDING: hiển thị nút "Hủy đơn hàng". Bấm vào mở modal xác nhận lý do hủy, gọi API hủy đơn và cập nhật lại giao diện.

## 7. TECHNICAL REQUIREMENTS
- Protected route yêu cầu đăng nhập
- Realtime cập nhật trạng thái khi shipper đổi tiến độ

## 8. INTEGRATION REQUIREMENTS
- Tài khoản cá nhân /account và OrderService backend


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Unauthorized Order Cancellation**: Khách hàng chỉ có thể hủy đơn của chính mình khi đơn chưa chuyển sang trạng thái SHIPPING.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Khách xem được toàn bộ danh sách đơn hàng cá nhân đã từng mua.
[ ] **AC-2**: Dòng thời gian hiển thị đúng mốc trạng thái hiện tại của đơn.
[ ] **AC-3**: Hủy đơn hàng pending thành công và hoàn trả tồn kho.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm thử tạo đơn hàng mới và thực hiện thao tác hủy đơn từ trang lịch sử

## 12. EXPECTED OUTPUT
- `frontend/src/app/account/orders/page.js`: Trang lịch sử đơn hàng
- `frontend/src/components/Account/OrderTimeline.jsx`: Dòng thời gian trạng thái đơn

## 13. COMPLETION REPORT
- Trang lịch sử đơn hàng và theo dõi tiến độ giao hàng hoàn thành
