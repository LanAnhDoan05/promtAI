# PROMPT 056 – PRODUCT DETAIL PAGE (PDP), IMAGE GALLERY, SIZE/COLOR VARIANT PICKER

## 1. ROLE
Senior Frontend Developer / UX Designer

## 2. OBJECTIVE
Xây dựng trang chi tiết sản phẩm (app/products/[slug]/page.js): Bộ sưu tập ảnh (Image Gallery kèm thumbnail và zoom ảnh), bộ chọn biến thể Màu sắc và Kích thước ma trận, kiểm tra tồn kho thời gian thực, nút Thêm vào giỏ hàng, Mua ngay, Bảng hướng dẫn chọn size (Size Guide popup), thông tin chất liệu và danh sách đánh giá.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_23_HERO_SLIDER_AND_BRAND_EXPERIENCE.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_23_HERO_SLIDER_AND_BRAND_EXPERIENCE.md)
> - [USER_MASTER_PROMPT_27_GLOBAL_BRANDING_AND_WARNING_AUDIT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_27_GLOBAL_BRANDING_AND_WARNING_AUDIT.md)

## 3. CONTEXT
PDP là trang quyết định chuyển đổi mua hàng (Conversion Rate). Mọi thao tác chọn màu, chọn size phải mượt mà, phản hồi ngay trạng thái còn/hết hàng và cập nhật ảnh tương ứng với màu được chọn.

## 4. PREREQUISITES
- PROMPT_054: ProductCard Component
- PROMPT_036: Product Detail API

## 5. INPUTS
- Product slug từ URL params

## 6. DETAILED TASKS
1. **Xây dựng Bộ sưu tập ảnh (Image Gallery)**:
   Cột trái hiển thị dải ảnh thu nhỏ (thumbnails). Khung ảnh chính lớn hỗ trợ rê chuột phóng to (zoom preview). Khi chọn màu khác, tự động cuộn đến ảnh của màu đó.

2. **Xây dựng Bộ chọn Màu sắc và Kích thước**:
   Nút chọn màu có tên màu và vòng màu sắc. Nút chọn size (S, M, L, XL), gạch chéo và làm mờ các size đã hết hàng trong kho. Hiển thị thông báo "Chỉ còn X sản phẩm" nếu tồn kho < 5.

3. **Bộ đếm số lượng và Nút Mua Hàng**:
   Nút tăng giảm số lượng (+ / -) không vượt quá tồn kho. Nút "THÊM VÀO GIỎ HÀNG" (viền đen) và nút "MUA NGAY" (nền đen chữ trắng).

4. **Tích hợp Size Guide Modal và Accordion chi tiết**:
   Nút "Bảng hướng dẫn chọn size" mở modal bảng thông số đo (Chiều cao, Cân nặng, Vòng ngực, Vòng eo). Các khối accordion thu gọn: Mô tả chi tiết, Chất liệu & Cách bảo quản, Chính sách đổi trả.

## 7. TECHNICAL REQUIREMENTS
- State quản lý selectedColor, selectedSize, selectedVariant, quantity
- Kiểm tra tồn kho thời gian thực trước khi cho phép bấm nút thêm giỏ

## 8. INTEGRATION REQUIREMENTS
- CartContext để thêm sản phẩm; ReviewSection để hiển thị đánh giá

## 9. SAFETY CONSTRAINTS
- ⚠️ **Unselected Variant Prevention**: Nếu khách chưa chọn size mà bấm Thêm giỏ, hiển thị thông báo yêu cầu chọn size cụ thể.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Chọn màu sắc tự động cập nhật danh sách size khả dụng của màu đó.
[ ] **AC-2**: Bấm thêm vào giỏ hàng hiển thị thông báo thành công và cập nhật badge giỏ hàng.
[ ] **AC-3**: Size Guide modal mở ra hiển thị bảng số đo chính xác.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm thử chọn biến thể hết hàng xác minh nút Thêm giỏ bị vô hiệu hóa

## 12. EXPECTED OUTPUT
- `frontend/src/app/products/[slug]/page.js`: Trang chi tiết sản phẩm
- `frontend/src/components/ProductDetail/ImageGallery.jsx`: Bộ sưu tập ảnh
- `frontend/src/components/ProductDetail/SizeGuideModal.jsx`: Modal hướng dẫn chọn size

## 13. COMPLETION REPORT
- Trang chi tiết sản phẩm thời trang Routine hoàn thành
