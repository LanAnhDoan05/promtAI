# PROMPT 049 – GLOBAL DESIGN SYSTEM, CSS VARIABLES, TYPOGRAPHY & COLOR PALETTE

## 1. ROLE
Senior UI/UX Designer & Lead Frontend Engineer

## 2. OBJECTIVE
Thiết lập hệ thống thiết kế (Design System) chuẩn hóa cho thương hiệu Routine: Bảng màu tối giản hiện đại (đen #000000, trắng #ffffff, xám #f5f5f5, xám viền #e5e5e5, đỏ nhấn #e11b22), kiểu chữ (typography scale), CSS variables, và reset CSS.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_23_HERO_SLIDER_AND_BRAND_EXPERIENCE.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_23_HERO_SLIDER_AND_BRAND_EXPERIENCE.md)
> - [USER_MASTER_PROMPT_27_GLOBAL_BRANDING_AND_WARNING_AUDIT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_27_GLOBAL_BRANDING_AND_WARNING_AUDIT.md)

## 3. CONTEXT
Thương hiệu thời trang Routine mang phong cách tối giản, tinh tế, chuẩn mực. Toàn bộ giao diện cần nhất quán về khoảng cách (spacing system), bo góc (border radius 4px - 8px), bóng đổ (box shadow nhẹ) và màu sắc để tạo trải nghiệm cao cấp.

## 4. PREREQUISITES
- PROMPT_013: Next.js Frontend Bootstrap đã hoàn tất

## 5. INPUTS
- Quy chuẩn nhận diện thương hiệu Routine
- Thiết kế hệ thống typography và color palette

## 6. DETAILED TASKS
1. **Xây dựng file frontend/src/app/globals.css**:
   Khai báo các biến CSS root: --color-primary, --color-secondary, --color-background, --color-surface, --color-border, --color-text-main, --color-text-muted, --color-accent-red, --font-sans, --spacing-xs đến --spacing-xxl.

2. **Cấu hình Typography chuẩn với Next.js Font**:
   Cấu hình Google Font Inter hoặc font sans-serif tương đương với subset "latin", "vietnamese", tối ưu font-display swap để chống layout shift.

3. **Tạo CSS Utility Classes và Spacing System**:
   Xây dựng các lớp tiện ích container, flex-center, text-truncate, button-base, badge-base đồng nhất.

## 7. TECHNICAL REQUIREMENTS
- CSS Variables native, không dùng inline style rải rác
- Next/font tối ưu tải font cục bộ
- Chuẩn hóa kích thước màn hình responsive breakpoints: 390px, 768px, 1024px, 1366px, 1920px

## 8. INTEGRATION REQUIREMENTS
- Được import trực tiếp vào app/layout.js


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **CSS Specificity Wars**: Tránh dùng !important vô tội vạ, sử dụng CSS Modules cho từng component riêng biệt.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: File globals.css chứa đầy đủ bảng biến màu và typography.
[ ] **AC-2**: Màu sắc hiển thị đúng chuẩn thương hiệu Routine.
[ ] **AC-3**: Giao diện web tải không bị giật font chữ (zero FOUT/FOIT).

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm tra hiển thị text tiếng Việt có dấu không bị lỗi font trên mọi kích thước

## 12. EXPECTED OUTPUT
- `frontend/src/app/globals.css`: CSS Variables và quy chuẩn thiết kế toàn cục

## 13. COMPLETION REPORT
- Hệ thống Design System và CSS Variables toàn cục đã hoàn thành
