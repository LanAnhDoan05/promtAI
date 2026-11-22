# PROMPT 039 – WISHLIST MANAGEMENT API & TOGGLE OPERATIONS

## 1. ROLE
Backend API Developer

## 2. OBJECTIVE
Xây dựng API quản lý danh sách sản phẩm yêu thích (Wishlist): kiểm tra trạng thái yêu thích, thêm/xóa dạng toggle, và lấy danh sách sản phẩm yêu thích của người dùng.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_02_CLOUDINARY_ADMIN_PRODUCT_MANAGEMENT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_02_CLOUDINARY_ADMIN_PRODUCT_MANAGEMENT.md)
> - [USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md)
> - [USER_MASTER_PROMPT_25_PRODUCTION_UPGRADE_NOTIFICATION_HANDOFF.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_25_PRODUCTION_UPGRADE_NOTIFICATION_HANDOFF.md)

## 3. CONTEXT
Khách hàng có thể lưu các mẫu quần áo ưa thích vào Wishlist để theo dõi hoặc mua sau. API cần hỗ trợ thao tác toggle nhanh từ nút hình trái tim trên ProductCard.

## 4. PREREQUISITES
- PROMPT_024: Wishlist Model
- PROMPT_033: RBAC Middleware

## 5. INPUTS
- User ID từ Token và Product ID

## 6. DETAILED TASKS
1. **Xây dựng WishlistService.toggleWishlist**:
   Kiểm tra nếu sản phẩm đã có trong Wishlist của User thì xóa bỏ; nếu chưa có thì thêm mới. Trả về trạng thái boolean isWishlisted.

2. **Xây dựng API getWishlist**:
   Trả về toàn bộ sản phẩm trong Wishlist của người dùng hiện tại kèm theo giá bán, biến thể và trạng thái còn hàng.

3. **Đăng ký Route và Controller**:
   POST /api/v1/wishlist/toggle, GET /api/v1/wishlist. Yêu cầu đăng nhập (authenticate middleware).

## 7. TECHNICAL REQUIREMENTS
- Atomic toggle operation
- Chỉ người dùng đã đăng nhập mới có Wishlist cá nhân

## 8. INTEGRATION REQUIREMENTS
- ProductCard heart icon và trang Wishlist frontend


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **User Isolation**: Chỉ cho phép người dùng truy cập và chỉnh sửa Wishlist của chính mình.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Bấm toggle lần đầu thêm sản phẩm vào Wishlist (isWishlisted: true).
[ ] **AC-2**: Bấm toggle lần hai xóa sản phẩm khỏi Wishlist (isWishlisted: false).
[ ] **AC-3**: Lấy danh sách trả về đúng các sản phẩm đã yêu thích.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm thử toggle thêm và xóa sản phẩm yêu thích qua Postman

## 12. EXPECTED OUTPUT
- `backend/src/services/wishlistService.js`: Dịch vụ danh sách yêu thích
- `backend/src/controllers/wishlistController.js`: Controller Wishlist

## 13. COMPLETION REPORT
- API danh sách yêu thích Wishlist đã hoàn thành
