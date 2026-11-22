# PROMPT 058 – SMART OUTFIT INSPIRATION & MIX-AND-MATCH VISUAL SHOWCASE

## 1. ROLE
Frontend UI/UX Specialist

## 2. OBJECTIVE
Xây dựng trang Phối đồ thông minh (app/outfits/page.js): Khám phá các bộ trang phục phối sẵn theo phong cách (Công sở, Dạo phố, Thu Đông), xem từng món đồ trong combo (Áo + Quần + Phụ kiện), chọn size cho từng món và nút "Mua trọn bộ combo" thêm toàn bộ vào giỏ hàng.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_23_HERO_SLIDER_AND_BRAND_EXPERIENCE.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_23_HERO_SLIDER_AND_BRAND_EXPERIENCE.md)
> - [USER_MASTER_PROMPT_27_GLOBAL_BRANDING_AND_WARNING_AUDIT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_27_GLOBAL_BRANDING_AND_WARNING_AUDIT.md)

## 3. CONTEXT
Tính năng Smart Outfit tạo nên nét đặc trưng cho website Routine. Thay vì mua từng món rời rạc, khách hàng có thể xem người mẫu mặc nguyên set đồ, kiểm tra giá ưu đãi của combo và mua toàn bộ set chỉ trong 1 thao tác.

## 4. PREREQUISITES
- PROMPT_045: Smart Outfit API
- PROMPT_054: ProductCard

## 5. INPUTS
- Danh sách Outfits từ API /api/v1/outfits

## 6. DETAILED TASKS
1. **Xây dựng Thanh lọc Phong cách và Dịp mặc**:
   Bộ lọc tab: Tất cả, Công sở thanh lịch, Dạo phố năng động, Phong cách Thu Đông, Tối giản Minimalist.

2. **Xây dựng Thẻ hiển thị Bộ phối đồ (OutfitCard)**:
   Ảnh lớn chụp toàn thân người mẫu phối đồ. Bên cạnh hoặc bên dưới hiển thị danh sách các món đồ thành phần (Áo, Quần, Phụ kiện) kèm giá riêng và kích cỡ.

3. **Xây dựng Cơ chế Thêm trọn bộ Combo vào giỏ hàng**:
   Khung chọn size đồng thời cho từng món đồ trong bộ phối, hiển thị tổng giá trị combo và nút "MUA TRỌN BỘ COMBO".

## 7. TECHNICAL REQUIREMENTS
- Grid layout sang trọng, hình ảnh dọc tỷ lệ 4:5
- Thêm đồng thời nhiều item vào giỏ hàng qua CartContext

## 8. INTEGRATION REQUIREMENTS
- CartContext và OutfitService backend


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Partial Stock Failure Handling**: Nếu 1 trong các món đồ trong combo hết size, hiển thị cảnh báo rõ ràng cho món đồ đó.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Trang /outfits hiển thị danh sách các bộ đồ phối chuẩn thời trang Routine.
[ ] **AC-2**: Bấm vào một outfit hiển thị chi tiết các món cấu thành.
[ ] **AC-3**: Nút "Mua trọn bộ combo" thêm thành công tất cả món đồ đã chọn vào giỏ hàng.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm thử chọn size cho 3 món trong 1 combo và thêm vào giỏ hàng

## 12. EXPECTED OUTPUT
- `frontend/src/app/outfits/page.js`: Trang khám phá phối đồ Smart Outfit
- `frontend/src/components/Outfit/OutfitCard.jsx`: Thẻ hiển thị combo phối đồ

## 13. COMPLETION REPORT
- Trang phối đồ thời trang thông minh Smart Outfit hoàn thành
