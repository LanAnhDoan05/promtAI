# PROMPT 051 – GLOBAL HEADER NAVIGATION, DROPDOWN MENUS & MOBILE DRAWER MENU

## 1. ROLE
Senior Frontend Developer / UI Specialist

## 2. OBJECTIVE
Xây dựng Header điều hướng toàn cục dính (sticky header) với logo ROUTINE, thanh điều hướng danh mục đa cấp (Mega Menu dropdown), nút tìm kiếm, icon giỏ hàng có số lượng badge, icon tài khoản và Mobile Drawer menu trượt mượt mà.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_23_HERO_SLIDER_AND_BRAND_EXPERIENCE.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_23_HERO_SLIDER_AND_BRAND_EXPERIENCE.md)
> - [USER_MASTER_PROMPT_27_GLOBAL_BRANDING_AND_WARNING_AUDIT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_27_GLOBAL_BRANDING_AND_WARNING_AUDIT.md)

## 3. CONTEXT
Header là thành phần giao diện xuất hiện ở mọi trang, cần thích ứng hoàn hảo từ màn hình điện thoại 390px đến màn hình 1920px. Trên desktop, khi hover danh mục sẽ mở menu phụ; trên mobile chuyển thành nút hamburger mở thanh trượt bên cạnh.

## 4. PREREQUISITES
- PROMPT_050: RootLayout

## 5. INPUTS
- Cây danh mục từ API /api/v1/categories
- Logo SVG Routine

## 6. DETAILED TASKS
1. **Xây dựng Desktop Header**:
   Tạo components/Header/Header.jsx với logo chữ in hoa "ROUTINE", menu chính (Nam, Nữ, Phụ kiện, Smart Outfit, Bộ sưu tập mới, Sale), hỗ trợ hover mở dropdown danh mục con.

2. **Xây dựng Quick Action Icons**:
   Nút kính lúp mở Search Modal, icon trái tim Wishlist kèm badge số lượng, icon túi xách Giỏ hàng kèm badge số lượng realtime, icon User mở menu tài khoản.

3. **Xây dựng Mobile Drawer Navigation**:
   Tạo nút Hamburger (3 vạch). Khi bấm, mở thanh trượt Drawer từ trái qua với hiệu ứng trượt êm ái, hỗ trợ accordion mở rộng danh mục con, hiển thị hotline hỗ trợ và liên kết đăng nhập.

4. **Hiệu ứng Sticky và Co giãn khi Cuộn trang**:
   Khi cuộn trang xuống, Header thu nhỏ nhẹ chiều cao (transition 0.3s) và có đổ bóng nhẹ phía dưới.

## 7. TECHNICAL REQUIREMENTS
- CSS Modules: Header.module.css
- Tránh chặn cuộn trang body khi đóng Drawer
- Hiển thị chính xác logo thương hiệu ROUTINE

## 8. INTEGRATION REQUIREMENTS
- Đọc cartCount từ CartContext, user từ UserContext, wishlistCount từ WishlistContext

## 9. SAFETY CONSTRAINTS
- ⚠️ **Z-index Clashing**: Đảm bảo Header có z-index: 1000 để nằm trên nội dung trang nhưng nằm dưới Toast/Modal khi cần.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Header hiển thị logo ROUTINE rõ nét, dropdown menu hoạt động mượt mà khi hover.
[ ] **AC-2**: Trên màn hình mobile 390px, thanh hamburger mở Drawer trơn tru và bấm đóng bình thường.
[ ] **AC-3**: Badge số lượng giỏ hàng cập nhật ngay khi thêm sản phẩm.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm thử responsive Header trên các kích thước: 390px, 768px, 1024px, 1440px

## 12. EXPECTED OUTPUT
- `frontend/src/components/Header/Header.jsx`: Component Header chính
- `frontend/src/components/Header/Header.module.css`: CSS Module Header
- `frontend/src/components/Header/MobileMenu.jsx`: Thanh trượt menu di động

## 13. COMPLETION REPORT
- Header toàn cục và Mobile Drawer hoàn thành chuẩn nhận diện Routine
