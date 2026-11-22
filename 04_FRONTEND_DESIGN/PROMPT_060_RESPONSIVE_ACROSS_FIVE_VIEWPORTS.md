# PROMPT 060 – RESPONSIVE LAYOUT ACROSS 5 VIEWPORTS (390PX, 768PX, 1024PX, 1366PX, 1920PX)

## 1. ROLE
Frontend Responsive & QA Specialist

## 2. OBJECTIVE
Kiểm toán và hoàn thiện khả năng hiển thị tương thích tuyệt đối (Pixel-perfect Responsive) trên 5 kích thước màn hình chuẩn: Mobile nhỏ (390px), Tablet dọc (768px), Tablet ngang / Laptop nhỏ (1024px), Desktop phổ thông (1366px), và Màn hình lớn (1920px).


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_23_HERO_SLIDER_AND_BRAND_EXPERIENCE.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_23_HERO_SLIDER_AND_BRAND_EXPERIENCE.md)
> - [USER_MASTER_PROMPT_27_GLOBAL_BRANDING_AND_WARNING_AUDIT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_27_GLOBAL_BRANDING_AND_WARNING_AUDIT.md)

## 3. CONTEXT
Người dùng mua sắm quần áo Routine trên nhiều loại thiết bị (iPhone, iPad, MacBook, PC). Không được có hiện tượng tràn chiều ngang (horizontal overflow scroll), vỡ chữ, đè nút hoặc layout co cụm bất hợp lý.

## 4. PREREQUISITES
- PROMPT_051 đến PROMPT_059

## 5. INPUTS
- Danh sách 5 viewports tiêu chuẩn kiểm thử

## 6. DETAILED TASKS
1. **Kiểm tra và tinh chỉnh Viewport Mobile 390px**:
   Đảm bảo Header thu thành hamburger, ProductCard xếp 2 cột cân đối, padding cạnh 12px, cỡ chữ tối thiểu 14px cho văn bản đọc, không xuất hiện thanh cuộn ngang của trang.

2. **Kiểm tra và tinh chỉnh Viewport Tablet 768px & 1024px**:
   Lưới sản phẩm 3 cột, Filter chuyển thành nút bấm bật sidebar (drawer filter), khoảng cách padding 24px.

3. **Kiểm tra và tinh chỉnh Viewport Desktop 1366px & 1920px**:
   Giới hạn chiều rộng tối đa (max-width: 1440px) căn giữa màn hình cho container, lưới sản phẩm 4 cột, dropdown mega menu mở rộng đầy đủ.

## 7. TECHNICAL REQUIREMENTS
- CSS Media Queries chuẩn: min-width / max-width
- overflow-x: hidden trên body/html để ngăn tràn ngang vô tình

## 8. INTEGRATION REQUIREMENTS
- Áp dụng xuyên suốt toàn bộ các trang frontend


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Touch Target Size**: Các nút bấm trên mobile phải có kích thước tối thiểu 44x44px để chạm bấm dễ dàng.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Không có bất kỳ thanh cuộn ngang nào xuất hiện ở độ phân giải 390px.
[ ] **AC-2**: Các hình ảnh sản phẩm giữ đúng tỷ lệ khung hình không bị méo.
[ ] **AC-3**: Chữ và nút bấm hiển thị rõ ràng trên cả 5 kích thước màn hình.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Sử dụng DevTools kiểm tra trang chủ và trang danh mục ở 5 kích thước: 390px, 768px, 1024px, 1366px, 1920px

## 12. EXPECTED OUTPUT
- `frontend/src/app/responsive.css`: Các quy tắc media query bổ trợ toàn cục

## 13. COMPLETION REPORT
- Kiểm toán và tối ưu hiển thị Responsive trên 5 viewports hoàn thành
