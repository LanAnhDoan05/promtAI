# PROMPT 050 – NEXT.JS ROOTLAYOUT, METADATA, FAVICON & GLOBAL BRAND IDENTITY

## 1. ROLE
Frontend Architect

## 2. OBJECTIVE
Xây dựng RootLayout (app/layout.js) cho toàn bộ ứng dụng Next.js, cấu hình Metadata SEO, OpenGraph, favicon, thẻ viewport và bao bọc các Provider toàn cục (UserProvider, CartProvider, ToastProvider).


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_23_HERO_SLIDER_AND_BRAND_EXPERIENCE.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_23_HERO_SLIDER_AND_BRAND_EXPERIENCE.md)
> - [USER_MASTER_PROMPT_27_GLOBAL_BRANDING_AND_WARNING_AUDIT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_27_GLOBAL_BRANDING_AND_WARNING_AUDIT.md)

## 3. CONTEXT
RootLayout là khung xương của ứng dụng. Tất cả các trang đều kế thừa từ layout này, đảm bảo chuẩn hóa tên thương hiệu "Routine", chuẩn hóa SEO thẻ title/description và tối ưu hóa tải trang.

## 4. PREREQUISITES
- PROMPT_049: Global Design System

## 5. INPUTS
- Favicon Routine, thẻ meta SEO, logo thương hiệu

## 6. DETAILED TASKS
1. **Cấu hình Metadata tĩnh và động trong app/layout.js**:
   Thiết lập title template: "%s | Routine - Smart Fashion", description: "Thương hiệu thời trang Routine - Tự hào phong cách Việt hiện đại, tối giản và thanh lịch", openGraph, robots, viewport.

2. **Tích hợp Favicon và App Icons**:
   Đặt favicon.ico, apple-touch-icon.png vào frontend/public/ và cấu hình trong metadata.

3. **Bao bọc Providers**:
   Tổ chức cây Provider: UserProvider -> CartProvider -> WishlistProvider -> ToastProvider -> Header -> {children} -> Footer.

## 7. TECHNICAL REQUIREMENTS
- Next.js 16 App Router metadata specification
- HTML lang="vi"
- Viewport tag chuẩn hóa chống zoom ngoài ý muốn trên mobile

## 8. INTEGRATION REQUIREMENTS
- Bao bọc toàn bộ các trang trong thư mục app/


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Hydration Mismatch Prevention**: Đảm bảo cây DOM phía server và client đồng nhất, tránh rendered attributes không khớp.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Trang web hiển thị đúng favicon và tiêu đề trang có đuôi "| Routine - Smart Fashion".
[ ] **AC-2**: HTML có lang="vi" và meta viewport chuẩn mobile.
[ ] **AC-3**: Cây Provider không gặp lỗi React Context Hydration.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Mở trang chủ và kiểm tra tiêu đề tab trình duyệt và thẻ meta trong Page Source

## 12. EXPECTED OUTPUT
- `frontend/src/app/layout.js`: RootLayout của ứng dụng Next.js

## 13. COMPLETION REPORT
- RootLayout và chuẩn hóa thương hiệu toàn cục đã hoàn thành
