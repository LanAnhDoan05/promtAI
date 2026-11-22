# PROMPT 068 – INTERACTIVE SHOPPING CART PAGE WITH ORDER SUMMARY & COUPON INPUT

## 1. ROLE
Frontend UI/UX Specialist

## 2. OBJECTIVE
Xây dựng trang Giỏ hàng chi tiết (app/cart/page.js): Bảng danh sách sản phẩm (ảnh, tên, màu, size, đơn giá, bộ đếm số lượng, nút xóa), ô nhập mã giảm giá (Coupon Input) có nút áp dụng tức thì, khung tóm tắt đơn hàng (Tạm tính, Giảm giá, Ước tính phí vận chuyển, Tổng thanh toán) và nút "Tiến hành Thanh toán".


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_21_ADDRESS_VALIDATION_AI_CONSULTATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_21_ADDRESS_VALIDATION_AI_CONSULTATION.md)
> - [USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md)

## 3. CONTEXT
Trang giỏ hàng là bước đệm then chốt trước khi thanh toán. Cần hiển thị rõ ràng chính sách "Miễn phí vận chuyển cho đơn từ 500k" và thanh tiến độ (Free shipping progress bar) để kích thích khách hàng mua thêm.

## 4. PREREQUISITES
- PROMPT_067: CartContext
- PROMPT_041: Coupon Engine

## 5. INPUTS
- Dữ liệu giỏ hàng từ CartContext

## 6. DETAILED TASKS
1. **Xây dựng Thanh Tiến Độ Miễn Phí Vận Chuyển**:
   Hiển thị: "Mua thêm X.000đ để được MIỄN PHÍ VẬN CHUYỂN", thanh tiến độ phần trăm % lấp đầy theo giá trị tạm tính.

2. **Bảng Danh Sách Sản Phẩm trong Giỏ**:
   Hiển thị rõ ảnh thumbnail, tên sản phẩm có link về PDP, phân loại Màu/Size, đơn giá, bộ tăng giảm số lượng (+ / -) và icon thùng rác xóa món đồ.

3. **Khung Áp Dụng Mã Khuyến Mãi (Coupon Box)**:
   Ô nhập mã voucher (như WELCOME10), nút "Áp dụng". Khi áp dụng thành công, hiển thị dòng giảm giá màu xanh và tag mã đã áp dụng kèm nút hủy.

4. **Khung Tóm Tắt Đơn Hàng (Order Summary Card)**:
   Cột phải dính (sticky): Tạm tính, Giảm giá voucher, Tổng tiền dự tính, nút lớn màu đen "TIẾN HÀNH THANH TOÁN" dẫn tới /checkout.

## 7. TECHNICAL REQUIREMENTS
- Thiết kế responsive 2 cột desktop, 1 cột mobile
- Trạng thái giỏ hàng trống (Empty Cart) với hình ảnh minh họa và nút "Tiếp tục mua sắm"

## 8. INTEGRATION REQUIREMENTS
- CartContext và Router chuyển hướng sang /checkout


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Empty Checkout Prevention**: Vô hiệu hóa nút Thanh toán nếu giỏ hàng trống hoặc có sản phẩm bị hết hàng.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Trang giỏ hàng hiển thị đầy đủ danh sách món đồ đã chọn.
[ ] **AC-2**: Nhập mã WELCOME10 giảm giá thành công và cập nhật lại tổng tiền.
[ ] **AC-3**: Bấm "Tiến hành thanh toán" chuyển hướng đúng sang trang /checkout.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm thử nhập mã giảm giá hợp lệ và mã giảm giá không hợp lệ

## 12. EXPECTED OUTPUT
- `frontend/src/app/cart/page.js`: Trang giỏ hàng đầy đủ
- `frontend/src/components/Cart/CartSummary.jsx`: Khung tóm tắt đơn hàng

## 13. COMPLETION REPORT
- Trang giỏ hàng tương tác và áp dụng khuyến mãi hoàn thành
