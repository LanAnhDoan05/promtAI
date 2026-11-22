# PROMPT 067 – CARTCONTEXT, PERSISTENT LOCALSTORAGE CART & QUANTITY MUTATION

## 1. ROLE
Frontend State Management Specialist

## 2. OBJECTIVE
Xây dựng CartContext quản lý giỏ hàng toàn cục: Đồng bộ giỏ hàng với Backend API, lưu bản sao cache trong localStorage để hiển thị tức thì, hỗ trợ thêm sản phẩm, cập nhật số lượng (+ / -) với debounce, xóa sản phẩm và tính toán tổng tiền tạm tính.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_21_ADDRESS_VALIDATION_AI_CONSULTATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_21_ADDRESS_VALIDATION_AI_CONSULTATION.md)
> - [USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md)

## 3. CONTEXT
Giỏ hàng cần phản hồi mượt mà và tức thì. Khi khách hàng nhấn tăng số lượng liên tục, giao diện cập nhật ngay lập tức (Optimistic UI Update) trong khi request đồng bộ ngầm với server được debounce để tránh nghẽn mạng.

## 4. PREREQUISITES
- PROMPT_038: Backend Cart API
- PROMPT_061: Frontend API Client

## 5. INPUTS
- Cart API endpoints: GET /cart, POST /cart/items, PUT /cart/items/:id, DELETE /cart/items/:id

## 6. DETAILED TASKS
1. **Xây dựng CartContext và CartProvider**:
   State quản lý: cart (items, totalQuantity, subtotal), loading (boolean). Tự động nạp giỏ hàng khi khởi tạo ứng dụng.

2. **Hàm addToCart(variantId, quantity)**:
   Gọi API thêm hàng, hiển thị Toast thông báo thành công, mở Drawer xem nhanh giỏ hàng hoặc cập nhật số lượng trên Header icon.

3. **Hàm updateQuantity(itemId, newQty) và removeFromCart(itemId)**:
   Cập nhật lạc quan (optimistic update) trên state, gửi API với debounce 300ms. Nếu API báo lỗi tồn kho thì hoàn tác (rollback) số lượng cũ và thông báo lỗi.

4. **Hàm clearCart()**:
   Dọn sạch giỏ hàng sau khi đặt hàng thành công.

## 7. TECHNICAL REQUIREMENTS
- Optimistic UI pattern cho trải nghiệm mua sắm nhanh chóng
- Đồng bộ session giữa các tab trình duyệt bằng storage event

## 8. INTEGRATION REQUIREMENTS
- Header cart icon, ProductCard quick add, PDP add to cart, Cart Page


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Stock Ceiling**: Không cho phép tăng số lượng vượt quá tồn kho khả dụng trả về từ server.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Thêm sản phẩm vào giỏ cập nhật ngay lập tức badge số lượng trên Header.
[ ] **AC-2**: Bấm tăng/giảm số lượng mượt mà và tính lại tổng tiền chính xác.
[ ] **AC-3**: Xóa sản phẩm cập nhật ngay giỏ hàng.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm thử thêm 3 sản phẩm khác nhau và tăng/giảm số lượng từng món

## 12. EXPECTED OUTPUT
- `frontend/src/context/CartContext.js`: Quản lý trạng thái giỏ hàng toàn cục

## 13. COMPLETION REPORT
- CartContext và cơ chế đồng bộ giỏ hàng thời gian thực hoàn thành
