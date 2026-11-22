# PROMPT 044 – CUSTOMER REVIEW, RATING & MEDIA ATTACHMENT API

## 1. ROLE
Backend API Developer

## 2. OBJECTIVE
Xây dựng API đánh giá sản phẩm (Review & Rating 1-5 sao), bình luận kèm hình ảnh thực tế và xác minh khách hàng đã mua sản phẩm (Verified Purchase).


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_02_CLOUDINARY_ADMIN_PRODUCT_MANAGEMENT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_02_CLOUDINARY_ADMIN_PRODUCT_MANAGEMENT.md)
> - [USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md)
> - [USER_MASTER_PROMPT_25_PRODUCTION_UPGRADE_NOTIFICATION_HANDOFF.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_25_PRODUCTION_UPGRADE_NOTIFICATION_HANDOFF.md)

## 3. CONTEXT
Đánh giá thực tế từ khách hàng là yếu tố then chốt tạo niềm tin mua sắm. Khách hàng đã nhận đơn (DELIVERED) có thể gửi đánh giá, chấm điểm sao, tải ảnh feedback và hiển thị trực tiếp trên trang chi tiết sản phẩm.

## 4. PREREQUISITES
- PROMPT_021: Product Model
- PROMPT_043: Order Service

## 5. INPUTS
- Product ID, User ID, Rating (1-5), Comment, Images array

## 6. DETAILED TASKS
1. **Xây dựng ReviewService.createReview**:
   Kiểm tra người dùng đã mua sản phẩm này trong một đơn hàng có trạng thái DELIVERED chưa (để gán cờ isVerifiedPurchase: true). Lưu bản ghi Review.

2. **Tính toán điểm đánh giá trung bình của sản phẩm**:
   Mỗi khi có review mới, tính toán lại rating trung bình và tổng số lượt đánh giá của sản phẩm.

3. **Cung cấp API GET /api/v1/products/:productId/reviews**:
   Lấy danh sách review có phân trang, lọc theo số sao (1-5 sao), kèm thông tin user và ảnh đính kèm.

## 7. TECHNICAL REQUIREMENTS
- Rating là số nguyên từ 1 đến 5
- Chống spam đánh giá ảo (mỗi user chỉ review 1 lần cho mỗi lượt mua)

## 8. INTEGRATION REQUIREMENTS
- Frontend PDP tab Đánh giá và Account trang Đơn hàng đã mua


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Profanity Filter**: Lọc các từ ngữ thô tục hoặc spam trong nội dung bình luận.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Tạo review thành công với rating 1-5 sao và lưu ảnh đính kèm.
[ ] **AC-2**: Gán cờ isVerifiedPurchase đúng cho khách hàng đã mua sản phẩm.
[ ] **AC-3**: API lấy danh sách đánh giá trả về đúng dữ liệu phân trang.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm thử gửi đánh giá từ tài khoản đã mua sản phẩm và tài khoản chưa mua

## 12. EXPECTED OUTPUT
- `backend/src/services/reviewService.js`: Dịch vụ xử lý đánh giá sản phẩm
- `backend/src/controllers/reviewController.js`: Controller đánh giá

## 13. COMPLETION REPORT
- API đánh giá và chấm điểm sản phẩm đã hoàn thành
