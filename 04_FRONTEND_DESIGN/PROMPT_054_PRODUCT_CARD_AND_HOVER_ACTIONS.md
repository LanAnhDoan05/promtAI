# PROMPT 054 – PRODUCTCARD COMPONENT, HOVER ANIMATION, DISCOUNT BADGE & QUICK ACTIONS

## 1. ROLE
Frontend UI Specialist

## 2. OBJECTIVE
Xây dựng thẻ sản phẩm (ProductCard) tái sử dụng: Hiển thị ảnh chính và tự động đổi sang ảnh phụ khi hover, huy hiệu giảm giá (Sale Badge -XX%), nút yêu thích Wishlist nhanh, bảng chọn size nhanh (Quick Size Picker), tên sản phẩm và định dạng giá tiền Việt Nam (VNĐ).


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_23_HERO_SLIDER_AND_BRAND_EXPERIENCE.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_23_HERO_SLIDER_AND_BRAND_EXPERIENCE.md)
> - [USER_MASTER_PROMPT_27_GLOBAL_BRANDING_AND_WARNING_AUDIT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_27_GLOBAL_BRANDING_AND_WARNING_AUDIT.md)

## 3. CONTEXT
ProductCard là thành phần UI cốt lõi xuất hiện khắp website: Trang chủ, Danh mục, Gợi ý, Tìm kiếm, Outfits. Cần tối ưu hiệu năng render và mang lại trải nghiệm tương tác trực quan cao cấp.

## 4. PREREQUISITES
- PROMPT_049: Global Design System

## 5. INPUTS
- Đối tượng Product từ API bao gồm variants, images, salePrice, originalPrice

## 6. DETAILED TASKS
1. **Xây dựng Cấu trúc ProductCard**:
   Container ảnh tỷ lệ 3:4. Hiển thị ảnh chính (featuredImage). Khi hover chuyển sang ảnh thứ 2 trong mảng images với hiệu ứng fade nhẹ.

2. **Thêm Nút Yêu Thích và Huy Hiệu Giảm Giá**:
   Icon trái tim ở góc trên bên phải, đổi màu đỏ khi đã yêu thích. Huy hiệu nền đỏ "-20%" ở góc trên bên trái nếu có salePrice < originalPrice.

3. **Khu vực Quick Size Picker xuất hiện khi hover**:
   Thanh chọn nhanh kích thước (S, M, L, XL) trượt lên từ đáy ảnh, cho phép thêm nhanh vào giỏ hàng mà không cần vào trang chi tiết.

4. **Hiển thị Tên, Giá và Bảng màu tròn (Color Swatches)**:
   Tên sản phẩm tối đa 2 dòng (line-clamp-2). Giá khuyến mãi in đậm màu đỏ/đen, giá gốc gạch ngang màu xám. Các chấm tròn màu sắc đại diện cho các màu có sẵn.

## 7. TECHNICAL REQUIREMENTS
- Next/image tối ưu hóa
- Format tiền tệ: new Intl.NumberFormat("vi-VN", { style: "currency", currency: "VND" })
- Tối ưu re-render với React.memo

## 8. INTEGRATION REQUIREMENTS
- Gọi WishlistContext để toggle và CartContext để thêm nhanh

## 9. SAFETY CONSTRAINTS
- ⚠️ **Event Bubbling**: Ngăn chặn sự kiện click vào nút Wishlist hoặc Quick Size làm kích hoạt chuyển trang của thẻ cha Link.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: ProductCard đổi ảnh mượt mà khi rê chuột.
[ ] **AC-2**: Giá tiền hiển thị đúng chuẩn VNĐ (ví dụ: 399.000 ₫).
[ ] **AC-3**: Bấm trái tim thêm vào danh sách yêu thích tức thì không giật trang.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm tra hiển thị ProductCard trên cả desktop và mobile (trên mobile tắt hover, hiển thị nút thao tác rõ ràng)

## 12. EXPECTED OUTPUT
- `frontend/src/components/ProductCard/ProductCard.jsx`: Component Thẻ sản phẩm
- `frontend/src/components/ProductCard/ProductCard.module.css`: CSS Module Thẻ sản phẩm

## 13. COMPLETION REPORT
- Component ProductCard hoàn chỉnh với đầy đủ hiệu ứng tương tác
