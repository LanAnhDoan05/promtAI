# PROMPT 069 – CUSTOMER WISHLIST PAGE WITH ONE-CLICK ADD TO CART

## 1. ROLE
Frontend UI Developer

## 2. OBJECTIVE
Xây dựng trang Danh sách yêu thích của khách hàng (app/wishlist/page.js): Hiển thị lưới các sản phẩm đã lưu, nút xóa khỏi danh sách yêu thích, nút "Thêm vào giỏ hàng" nhanh cho từng sản phẩm và nút "Thêm tất cả vào giỏ hàng".


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_21_ADDRESS_VALIDATION_AI_CONSULTATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_21_ADDRESS_VALIDATION_AI_CONSULTATION.md)
> - [USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md)

## 3. CONTEXT
Trang Wishlist giúp khách hàng lưu lại các mẫu quần áo thời trang Routine ưa thích để theo dõi giảm giá hoặc mua sắm dần.

## 4. PREREQUISITES
- PROMPT_039: Backend Wishlist API
- PROMPT_054: ProductCard

## 5. INPUTS
- Danh sách sản phẩm yêu thích từ WishlistContext

## 6. DETAILED TASKS
1. **Xây dựng Giao diện Lưới Sản Phẩm Yêu Thích**:
   Hiển thị lưới 4 cột (desktop) hoặc 2 cột (mobile) các ProductCard có sẵn trong danh sách yêu thích.

2. **Nút Thao Tác Nhanh cho từng Sản phẩm**:
   Nút "Chọn size & Thêm giỏ" mở popup chọn size nhanh, thêm vào giỏ và có tùy chọn xóa khỏi Wishlist.

3. **Giao diện Danh sách Trống (Empty Wishlist)**:
   Khi chưa có sản phẩm nào, hiển thị biểu tượng trái tim rỗng và nút "Khám phá sản phẩm mới".

## 7. TECHNICAL REQUIREMENTS
- Đồng bộ trạng thái Wishlist thời gian thực với backend

## 8. INTEGRATION REQUIREMENTS
- WishlistContext, CartContext


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Auth Guard**: Bảo vệ trang bằng ProtectedRoute, yêu cầu đăng nhập để xem danh sách cá nhân.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Trang hiển thị chính xác các sản phẩm mà khách hàng đã bấm yêu thích.
[ ] **AC-2**: Bấm bỏ yêu thích xóa ngay sản phẩm khỏi lưới.
[ ] **AC-3**: Thêm sản phẩm từ Wishlist vào giỏ hàng thành công.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Thêm 2 sản phẩm vào yêu thích, truy cập /wishlist và kiểm tra hiển thị

## 12. EXPECTED OUTPUT
- `frontend/src/app/wishlist/page.js`: Trang danh sách yêu thích

## 13. COMPLETION REPORT
- Trang danh sách yêu thích Wishlist hoàn thành
