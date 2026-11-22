# PROMPT 062 – PHASE 04 FRONTEND UI SANITY & VISUAL POLISH GATEWAY

## 1. ROLE
Principal UI/UX Architect / QA Lead

## 2. OBJECTIVE
Thực hiện kiểm tra nghiệm thu chất lượng giao diện toàn bộ Phase 04: Thẩm mỹ thương hiệu Routine, độ mượt của hoạt họa, không lỗi console React, và ký duyệt Gateway 4.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_23_HERO_SLIDER_AND_BRAND_EXPERIENCE.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_23_HERO_SLIDER_AND_BRAND_EXPERIENCE.md)
> - [USER_MASTER_PROMPT_27_GLOBAL_BRANDING_AND_WARNING_AUDIT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_27_GLOBAL_BRANDING_AND_WARNING_AUDIT.md)

## 3. CONTEXT
Gateway 4 xác nhận tầng giao diện và hệ thống components đã hoàn thiện chuẩn mực trước khi tích hợp các nghiệp vụ mua hàng chi tiết trong Phase 05.

## 4. PREREQUISITES
- PROMPT_049 đến PROMPT_061

## 5. INPUTS
- Toàn bộ các components và trang giao diện trong frontend/src/

## 6. DETAILED TASKS
1. **Kiểm toán Nhận diện Thương hiệu Toàn diện**:
   Kiểm tra tên thương hiệu "Routine", logo ROUTINE in hoa, favicon, màu sắc chủ đạo đen-trắng-đỏ trên tất cả các trang.

2. **Kiểm tra Console Logs và Cảnh báo React**:
   Xác minh không có lỗi Hydration Mismatch, không có lỗi missing key trong mảng map(), không có lỗi thẻ lồng sai quy cách (như <p> trong <p>).

3. **Kiểm toán Hiệu năng Tải trang (Core Web Vitals)**:
   Kiểm tra điểm CLS (Cumulative Layout Shift) = 0, FCP < 1.5s trên môi trường local.

4. **Lập Báo cáo Nghiệm thu Gateway 4**:
   Xuất bản tài liệu FRONTEND_ACCEPTANCE_REPORT.md và ký phê duyệt chuyển giao sang Phase 05 E-commerce Features.

## 7. TECHNICAL REQUIREMENTS
- Zero critical UI bugs
- Chuẩn nhận diện thương hiệu Routine

## 8. INTEGRATION REQUIREMENTS
- Mở khóa triển khai Phase 05 (E-commerce Features)


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Quality Gate Rule**: Bất kỳ lỗi vỡ layout nào trên mobile 390px đều không được thông qua Gateway 4.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: [ ] AC-1: Giao diện Header, Footer, Homepage, PLP, PDP, Outfits hoàn thiện đẹp mắt.
[ ] **AC-2**: [ ] AC-2: Đạt chuẩn responsive trên 5 viewports không tràn ngang.
[ ] **AC-3**: [ ] AC-3: Không có lỗi React console đỏ.
[ ] **AC-4**: [ ] AC-4: Báo cáo nghiệm thu Gateway 4 được phê duyệt.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Mở DevTools kiểm tra console trang chủ và duyệt qua 3 trang danh mục không có lỗi đỏ

## 12. EXPECTED OUTPUT
- `docs/FRONTEND_ACCEPTANCE_REPORT.md`: Báo cáo nghiệm thu chất lượng giao diện Frontend

## 13. COMPLETION REPORT
- Ký duyệt Gateway 4: Cấp phép bắt đầu Phase 05 E-commerce Features
