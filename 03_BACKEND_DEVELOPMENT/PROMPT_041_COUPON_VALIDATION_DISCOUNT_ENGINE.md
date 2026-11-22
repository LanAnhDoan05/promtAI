# PROMPT 041 – COUPON VALIDATION, DISCOUNT CALCULATION & USAGE CONSTRAINT ENGINE

## 1. ROLE
Backend Business Logic Developer

## 2. OBJECTIVE
Xây dựng hệ thống kiểm tra và áp dụng mã giảm giá (Coupon/Voucher): kiểm tra thời hạn, giá trị đơn hàng tối thiểu, giới hạn lượt dùng, loại giảm giá (% hoặc số tiền cố định) và mức giảm tối đa.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_02_CLOUDINARY_ADMIN_PRODUCT_MANAGEMENT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_02_CLOUDINARY_ADMIN_PRODUCT_MANAGEMENT.md)
> - [USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md)
> - [USER_MASTER_PROMPT_25_PRODUCTION_UPGRADE_NOTIFICATION_HANDOFF.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_25_PRODUCTION_UPGRADE_NOTIFICATION_HANDOFF.md)

## 3. CONTEXT
Khách hàng có thể nhập mã khuyến mãi (như WELCOME10, ROUTINE2026) tại trang giỏ hàng hoặc thanh toán. Hệ thống cần kiểm tra chặt chẽ điều kiện để ngăn chặn lạm dụng mã giảm giá.

## 4. PREREQUISITES
- PROMPT_027: Coupon Model

## 5. INPUTS
- Mã coupon (code) và giá trị tạm tính của đơn hàng (subtotal)

## 6. DETAILED TASKS
1. **Xây dựng CouponService.validateAndCalculate**:
   Tìm coupon theo code (không phân biệt hoa thường). Kiểm tra: isActive === true, startDate <= now <= endDate, usedCount < usageLimit, subtotal >= minOrderValue. Nếu không thỏa mãn, trả về lỗi chi tiết.

2. **Tính toán Số tiền Giảm giá**:
   Nếu discountType === "PERCENT": discount = subtotal * (discountValue / 100). Áp dụng trần maxDiscount nếu có. Nếu discountType === "FIXED": discount = min(discountValue, subtotal).

3. **Tạo Endpoint POST /api/v1/coupons/apply**:
   Nhận { code, subtotal } và trả về { valid: true, coupon: { code, discountAmount, finalTotal } }.

## 7. TECHNICAL REQUIREMENTS
- Định dạng tiền tệ Decimal chuẩn xác
- Kiểm tra ranh giới ngày hết hạn chính xác đến từng giây

## 8. INTEGRATION REQUIREMENTS
- Checkout flow và Cart summary


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Discount Overflow**: Số tiền giảm giá không bao giờ được vượt quá giá trị đơn hàng (discountAmount <= subtotal).

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Áp dụng mã WELCOME10 giảm 10% chính xác trên đơn hàng đủ điều kiện.
[ ] **AC-2**: Nhập mã hết hạn hoặc chưa đạt giá trị tối thiểu trả về thông báo lỗi rõ ràng.
[ ] **AC-3**: Mã giảm phần trăm có maxDiscount không bao giờ giảm vượt mức trần quy định.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm thử áp dụng mã hợp lệ
2. **Tình huống kiểm thử 2**: Kiểm thử áp dụng mã với đơn hàng dưới mức minOrderValue

## 12. EXPECTED OUTPUT
- `backend/src/services/couponService.js`: Dịch vụ xử lý mã giảm giá
- `backend/src/controllers/couponController.js`: Controller mã giảm giá

## 13. COMPLETION REPORT
- Động cơ xử lý mã giảm giá Coupon đã hoàn thành
