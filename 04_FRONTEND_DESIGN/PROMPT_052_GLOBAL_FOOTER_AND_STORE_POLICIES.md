# PROMPT 052 – GLOBAL FOOTER, STORE INFORMATION, POLICIES & SOCIAL LINKS

## 1. ROLE
Frontend UI Developer

## 2. OBJECTIVE
Xây dựng Footer chân trang toàn cục: Thông tin thương hiệu Routine, hệ thống cửa hàng, chính sách đổi trả, bảo mật, vận chuyển, đăng ký nhận tin khuyến mãi (Newsletter) và liên kết mạng xã hội.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_23_HERO_SLIDER_AND_BRAND_EXPERIENCE.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_23_HERO_SLIDER_AND_BRAND_EXPERIENCE.md)
> - [USER_MASTER_PROMPT_27_GLOBAL_BRANDING_AND_WARNING_AUDIT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_27_GLOBAL_BRANDING_AND_WARNING_AUDIT.md)

## 3. CONTEXT
Footer cung cấp thông tin pháp lý, độ tin cậy và liên hệ cho thương hiệu. Giao diện chia thành 4 cột trên desktop và xếp chồng accordion trên mobile.

## 4. PREREQUISITES
- PROMPT_050: RootLayout

## 5. INPUTS
- Thông tin công ty Routine, địa chỉ cửa hàng, danh sách liên kết chính sách

## 6. DETAILED TASKS
1. **Xây dựng Cột 1: Thông tin Thương hiệu Routine**:
   Tên công ty, giấy phép kinh doanh, địa chỉ trụ sở chính, hotline hỗ trợ 1900 xxxx, email cskh@routine.vn.

2. **Xây dựng Cột 2 & 3: Về chúng tôi & Chính sách**:
   Liên kết tới các trang: Giới thiệu thương hiệu, Hệ thống cửa hàng, Chính sách bảo mật, Chính sách đổi trả 15 ngày, Hướng dẫn chọn size, Quy định giao hàng.

3. **Xây dựng Cột 4: Đăng ký Nhận Bản tin & Mạng xã hội**:
   Form nhập email nhận voucher chào mừng 10%, các icon mạng xã hội: Facebook, Instagram, TikTok, YouTube.

4. **Dòng bản quyền dưới cùng (Copyright bar)**:
   Dòng chữ: "© 2026 ROUTINE - All rights reserved. Tự hào thời trang Việt Nam".

## 7. TECHNICAL REQUIREMENTS
- CSS Grid/Flexbox responsive
- Semantic tag <footer>
- Chống tràn ngang trên màn hình 390px

## 8. INTEGRATION REQUIREMENTS
- Được đặt cố định ở cuối RootLayout


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Accessibility (a11y)**: Đảm bảo độ tương phản chữ trên nền tối đạt chuẩn WCAG AA.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Footer hiển thị đầy đủ 4 cột thông tin trên desktop và thu gọn gọn gàng trên mobile.
[ ] **AC-2**: Các liên kết chính sách trỏ đến đúng trang tương ứng.
[ ] **AC-3**: Form nhập email có validate định dạng email hợp lệ.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm tra Footer trên viewport 390px và 1440px

## 12. EXPECTED OUTPUT
- `frontend/src/components/Footer/Footer.jsx`: Component Footer chính
- `frontend/src/components/Footer/Footer.module.css`: CSS Module Footer

## 13. COMPLETION REPORT
- Chân trang Footer toàn cục Routine hoàn thành
