# PROMPT 075 – ORDER CONFIRMATION PAGE WITH PRINTABLE INVOICE & TRANSACTION SUMMARY

## 1. ROLE
Frontend UI Developer

## 2. OBJECTIVE
Xây dựng trang Xác nhận đặt hàng thành công (app/order-success/page.js): Hiển thị thông điệp cảm ơn mua sắm tại Routine, mã đơn hàng, ngày đặt, trạng thái thanh toán, chi tiết các món đồ đã mua, địa chỉ nhận hàng, hóa đơn điện tử có thể in (Printable Invoice), và nút "Tiếp tục mua sắm".


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_21_ADDRESS_VALIDATION_AI_CONSULTATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_21_ADDRESS_VALIDATION_AI_CONSULTATION.md)
> - [USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md)

## 3. CONTEXT
Trang xác nhận đơn hàng mang lại sự an tâm cho khách hàng sau khi thanh toán hoặc đặt cọc. Khách hàng có thể in hóa đơn hoặc lưu lại mã đơn để tra cứu.

## 4. PREREQUISITES
- PROMPT_074: Order Submission

## 5. INPUTS
- Mã đơn hàng orderCode từ URL query

## 6. DETAILED TASKS
1. **Tự động Nạp Thông Tin Đơn Hàng**:
   Gọi GET /api/v1/orders/:orderCode để lấy toàn bộ thông tin đơn hàng vừa tạo.

2. **Hiển thị Khung Thông Báo Thành Công**:
   Biểu tượng dấu tích xanh lớn, tiêu đề: "ĐẶT HÀNG THÀNH CÔNG!", thông báo: "Cảm ơn bạn đã lựa chọn thời trang Routine. Đơn hàng đang được chuẩn bị để đóng gói".

3. **Bảng Hóa Đơn Chi Tiết (Printable Invoice)**:
   Thiết kế mẫu hóa đơn mua sắm Routine thanh lịch: Mã đơn, Thời gian, Thông tin người nhận, Bảng sản phẩm, Tổng thanh toán. Nút "In hóa đơn" kích hoạt window.print() với CSS @media print tối ưu.

4. **Nút Điều Hướng Tiếp Tục**:
   Nút "Xem lịch sử đơn hàng" (tới /account/orders) và nút "Tiếp tục mua hàng" (về trang chủ).

## 7. TECHNICAL REQUIREMENTS
- CSS @media print ẩn Header, Footer và các nút bấm, chỉ in phần hóa đơn
- Xử lý trường hợp không tìm thấy mã đơn hàng

## 8. INTEGRATION REQUIREMENTS
- Nhận orderCode từ luồng Checkout hoặc VNPay Return


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Order Information Masking**: Không hiển thị thông tin thẻ ngân hàng hoặc dữ liệu bảo mật trên trang công khai.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Trang hiển thị đầy đủ thông tin đơn hàng vừa đặt.
[ ] **AC-2**: Bấm "In hóa đơn" mở cửa sổ in ấn đúng định dạng hóa đơn đẹp mắt.
[ ] **AC-3**: Mã đơn hàng và trạng thái thanh toán hiển thị chính xác.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Truy cập /order-success?code=ROUTINE-... kiểm tra hiển thị

## 12. EXPECTED OUTPUT
- `frontend/src/app/order-success/page.js`: Trang xác nhận đặt hàng thành công
- `frontend/src/components/Order/InvoicePrint.jsx`: Component hóa đơn in ấn

## 13. COMPLETION REPORT
- Trang xác nhận đơn hàng và in hóa đơn điện tử hoàn thành
