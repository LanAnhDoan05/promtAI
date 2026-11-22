# PROMPT 038 – CART MANAGEMENT SERVICE, VARIANT MERGING & GUEST SESSION SYNC

## 1. ROLE
Backend API Developer

## 2. OBJECTIVE
Xây dựng API quản lý giỏ hàng toàn diện: Thêm vào giỏ, cập nhật số lượng, xóa mục, và cơ chế tự động gộp giỏ hàng khách vãng lai (Session Cart) vào tài khoản người dùng khi đăng nhập.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_02_CLOUDINARY_ADMIN_PRODUCT_MANAGEMENT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_02_CLOUDINARY_ADMIN_PRODUCT_MANAGEMENT.md)
> - [USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md)
> - [USER_MASTER_PROMPT_25_PRODUCTION_UPGRADE_NOTIFICATION_HANDOFF.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_25_PRODUCTION_UPGRADE_NOTIFICATION_HANDOFF.md)

## 3. CONTEXT
Khách hàng có thể lướt web và thêm sản phẩm vào giỏ hàng khi chưa đăng nhập. Khi họ đăng nhập, hệ thống phải tự động gộp các sản phẩm từ sessionId sang userId mà không làm mất hàng.

## 4. PREREQUISITES
- PROMPT_024: Cart Model
- PROMPT_032: Auth Service

## 5. INPUTS
- Session ID (từ cookie hoặc header) hoặc User ID (từ Bearer Token)

## 6. DETAILED TASKS
1. **Xây dựng CartService.getCart**:
   Tìm hoặc tạo Cart theo userId hoặc sessionId. Nạp kèm danh sách CartItem, ProductVariant, và Product (tên, ảnh, giá bán, tồn kho hiện tại).

2. **Xây dựng Thao tác Thêm / Sửa / Xóa mục giỏ hàng**:
   Thêm mục: kiểm tra variantId và số lượng yêu cầu so với tồn kho khả dụng. Nếu đã tồn tại trong giỏ thì tăng số lượng. Cập nhật số lượng: kiểm tra tồn kho. Xóa mục khỏi giỏ.

3. **Xây dựng Logic Gộp Giỏ Hàng (Merge Carts)**:
   Khi người dùng đăng nhập có truyền sessionId: chuyển toàn bộ CartItem từ Session Cart sang User Cart. Nếu trùng variantId thì cộng dồn số lượng. Xóa Session Cart cũ.

## 7. TECHNICAL REQUIREMENTS
- Đảm bảo số lượng trong giỏ không vượt quá tồn kho khả dụng của variant
- Trả về tổng số lượng mục (cartCount) và tạm tính (subtotal)

## 8. INTEGRATION REQUIREMENTS
- Frontend CartContext và Header Cart Badge kết nối API này

## 9. SAFETY CONSTRAINTS
- ⚠️ **Cart Price Tampering**: Giá của sản phẩm trong giỏ luôn được lấy từ Product/Variant trong database, không lấy từ client payload.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Khách thêm sản phẩm vào giỏ thành công, phản hồi trả về đầy đủ chi tiết biến thể và tổng tiền.
[ ] **AC-2**: Cập nhật số lượng quá tồn kho trả về lỗi HTTP 400 kèm thông báo số lượng tối đa.
[ ] **AC-3**: Đăng nhập gộp thành công giỏ hàng ẩn danh vào tài khoản.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm thử thêm sản phẩm vào giỏ với vai trò khách vãng lai
2. **Tình huống kiểm thử 2**: Kiểm thử đăng nhập và xác minh giỏ hàng được gộp chính xác

## 12. EXPECTED OUTPUT
- `backend/src/services/cartService.js`: Dịch vụ xử lý giỏ hàng và gộp session
- `backend/src/controllers/cartController.js`: Controller giỏ hàng

## 13. COMPLETION REPORT
- API quản lý giỏ hàng đa phiên đã hoàn thành
