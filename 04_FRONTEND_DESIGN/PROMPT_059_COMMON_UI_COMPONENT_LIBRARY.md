# PROMPT 059 – COMMON UI COMPONENTS (MODAL, TOAST, SKELETON, SPINNER, BADGE, PAGINATION)

## 1. ROLE
Frontend UI Systems Engineer

## 2. OBJECTIVE
Xây dựng bộ thư viện UI dùng chung (Reusable UI Components): Modal dialog, Toast notification, Skeleton loading placeholders, Loading spinner, Status badge, Pagination controls, và Accordion collapse.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_23_HERO_SLIDER_AND_BRAND_EXPERIENCE.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_23_HERO_SLIDER_AND_BRAND_EXPERIENCE.md)
> - [USER_MASTER_PROMPT_27_GLOBAL_BRANDING_AND_WARNING_AUDIT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_27_GLOBAL_BRANDING_AND_WARNING_AUDIT.md)

## 3. CONTEXT
Một hệ sinh thái Frontend chất lượng cao cần các linh kiện giao diện cơ sở được chuẩn hóa, có animation mượt mà, dễ sử dụng qua Props và đảm bảo nhất quán về trải nghiệm trên toàn bộ các trang.

## 4. PREREQUISITES
- PROMPT_049: Global Design System

## 5. INPUTS
- Quy chuẩn thiết kế component Routine

## 6. DETAILED TASKS
1. **Xây dựng Modal Component với Portal**:
   Sử dụng createPortal gắn vào document.body, hỗ trợ click ngoài đóng modal, phím ESC, animation fade-in mượt.

2. **Xây dựng Hệ thống Toast Notification**:
   Tạo ToastContext và ToastContainer hiển thị thông báo góc trên/dưới: success (xanh lá), error (đỏ), warning (vàng), info (đen/xám), tự biến mất sau 3s.

3. **Xây dựng Skeleton Loader và Loading Spinner**:
   SkeletonCard mô phỏng hình dạng sản phẩm khi đang tải dữ liệu để chống giật trang (Zero Cumulative Layout Shift). Spinner tròn xoay tối giản.

4. **Xây dựng Badge và Pagination Component**:
   Badge hiển thị trạng thái (Đã giao hàng, Đang xử lý, Chờ thanh toán). Pagination phân trang đầy đủ.

## 7. TECHNICAL REQUIREMENTS
- React 19 / Next.js tương thích hoàn toàn
- Không phụ thuộc thư viện UI cồng kềnh (thuần CSS Modules và React)

## 8. INTEGRATION REQUIREMENTS
- Được sử dụng trong tất cả các trang Storefront và Admin Portal


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Memory Leaks in Timers**: Xóa sạch các hàm setTimeout trong Toast khi component unmount.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Gọi toast.success("...") hiển thị thông báo đẹp mắt và biến mất sau 3 giây.
[ ] **AC-2**: Skeleton loaders hiển thị đúng kích thước khung hình sản phẩm khi đang fetch API.
[ ] **AC-3**: Modal khóa cuộn trang body khi mở và mở khóa khi đóng.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm thử hiển thị đồng thời nhiều Toast và đóng Modal bằng phím ESC

## 12. EXPECTED OUTPUT
- `frontend/src/components/UI/Modal.jsx`: Component Modal Portal
- `frontend/src/components/UI/Toast.jsx`: Hệ thống Toast thông báo
- `frontend/src/components/UI/Skeleton.jsx`: Placeholder khung xương tải trang

## 13. COMPLETION REPORT
- Bộ thư viện UI components dùng chung hoàn thành
