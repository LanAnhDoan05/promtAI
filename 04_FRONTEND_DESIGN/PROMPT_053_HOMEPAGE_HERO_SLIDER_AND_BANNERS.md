# PROMPT 053 – HOMEPAGE HERO BANNER SLIDER & PROMOTIONAL SECTION

## 1. ROLE
Frontend UI/UX Specialist

## 2. OBJECTIVE
Xây dựng Hero Banner Slider tự động chuyển slide trên trang chủ với hình ảnh thời trang chất lượng cao, khẩu hiệu mùa mới, nút kêu gọi hành động (Call to Action - "Khám phá ngay", "Mua sắm BST Thu Đông"), và dải banner danh mục nổi bật.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_23_HERO_SLIDER_AND_BRAND_EXPERIENCE.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_23_HERO_SLIDER_AND_BRAND_EXPERIENCE.md)
> - [USER_MASTER_PROMPT_27_GLOBAL_BRANDING_AND_WARNING_AUDIT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_27_GLOBAL_BRANDING_AND_WARNING_AUDIT.md)

## 3. CONTEXT
Trang chủ là bộ mặt thương mại của Routine. Hero Banner cần gây ấn tượng thị giác mạnh mẽ, hỗ trợ vuốt chạm trên mobile (touch swipe), nút mũi tên điều hướng, thanh phân trang dots và hiệu ứng chuyển cảnh mượt mà.

## 4. PREREQUISITES
- PROMPT_049: Global Design System

## 5. INPUTS
- Danh sách ảnh banner chiến dịch Thu Đông từ backend hoặc public assets

## 6. DETAILED TASKS
1. **Xây dựng Component HeroSlider**:
   Hỗ trợ mảng banners với autoplay 5 giây, dừng khi hover, nút Next/Prev tròn tinh tế, chỉ số dots điều hướng bên dưới.

2. **Tối ưu hình ảnh Hero Banner với Next/Image**:
   Sử dụng priority={true} cho slide đầu tiên để tối ưu điểm LCP (Largest Contentful Paint), hỗ trợ tỷ lệ khung hình 16:9 desktop và 4:5 mobile.

3. **Xây dựng Dải Banner Danh Mục Nổi Bật (Featured Categories)**:
   Lưới 3 ô banner lớn dẫn tới: Đồ Nam, Đồ Nữ, Smart Outfit Phối đồ.

## 7. TECHNICAL REQUIREMENTS
- Tự xây dựng slider nhẹ nhàng hoặc dùng Swiper / CSS scroll-snap mượt mà
- Zero layout shift (CLS = 0) nhờ kích thước ảnh cố định tỷ lệ

## 8. INTEGRATION REQUIREMENTS
- Đặt tại vị trí đầu tiên của frontend/src/app/page.js


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Heavy Asset Loading**: Chỉ tải ảnh có độ phân giải tối ưu, chuyển định dạng WebP để không làm chậm trang chủ.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Slider tự động chuyển sau mỗi 5s, hoạt động trơn tru khi click nút hoặc vuốt trên điện thoại.
[ ] **AC-2**: Slide đầu tiên tải nhanh không giật layout.
[ ] **AC-3**: Các nút CTA liên kết chính xác tới danh mục tương ứng.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm tra hoạt động vuốt cảm ứng trên giả lập thiết bị di động

## 12. EXPECTED OUTPUT
- `frontend/src/components/Home/HeroSlider.jsx`: Component Hero Slider
- `frontend/src/components/Home/HeroSlider.module.css`: CSS Module Slider

## 13. COMPLETION REPORT
- Hero Banner Slider và khu vực banner chiến dịch trang chủ đã hoàn thành
