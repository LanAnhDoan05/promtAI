# PROMPT 016 – THIẾT LẬP PIPELINE QUẢN LÝ TÀI NGUYÊN TĨNH & MEDIA ASSETS

## 1. ROLE
Frontend Asset & UI Specialist

## 2. OBJECTIVE
Thiết lập thư mục tài nguyên tĩnh, cấu hình lưu trữ media, bộ sưu tập hình ảnh thời trang và cơ chế nạp ảnh placeholder an toàn.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_04_SELF_TEST_ENVIRONMENT_HANDOVER.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_04_SELF_TEST_ENVIRONMENT_HANDOVER.md)
> - [USER_MASTER_PROMPT_15_ADMIN_CUSTOMER_CONCURRENT_OPS.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_15_ADMIN_CUSTOMER_CONCURRENT_OPS.md)

## 3. CONTEXT
Một trang thương mại điện tử thời trang phụ thuộc lớn vào chất lượng và tốc độ tải hình ảnh sản phẩm, banner và lookbook.

## 4. PREREQUISITES
- PROMPT_013 hoàn thành

## 5. INPUTS
- Kho hình ảnh sản phẩm Routine thực tế

## 6. DETAILED TASKS
1. **Tạo cấu trúc thư mục media trong `frontend/public/`**:
   Khởi tạo `images/products/`, `images/banners/`, `images/categories/`, `images/icons/`.

2. **Tạo component `PlaceholderImage.jsx`**:
   Xây dựng component hiển thị ảnh dự phòng thanh lịch khi ảnh sản phẩm bị lỗi đường dẫn hoặc đang tải.

3. **Cấu hình tối ưu hóa định dạng Next.js Image**:
   Hỗ trợ định dạng WebP, AVIF và cấu hình kích thước linh hoạt tránh vỡ layout (CLS).

## 7. TECHNICAL REQUIREMENTS
- Hình ảnh định dạng tối ưu WebP hoặc JPG nén chất lượng cao
- Cơ chế fallback tự động không để xuất hiện khung ảnh vỡ trên giao diện

## 8. INTEGRATION REQUIREMENTS
- Tương thích với component `ProductCard` và `HeroSlider` trong Phase 04.


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Kiểm soát dung lượng**: Không đưa các file ảnh có kích thước vượt quá 2MB vào thư mục tĩnh của dự án.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Cấu trúc thư mục tài nguyên hoàn chỉnh trong `frontend/public/`
[ ] **AC-2**: Component `PlaceholderImage` hoạt động mượt mà khi ảnh chính bị lỗi

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Thử tải một URL ảnh hỏng để kiểm tra hiển thị ảnh dự phòng

## 12. EXPECTED OUTPUT
- `frontend/components/common/PlaceholderImage.jsx`: Component hiển thị ảnh dự phòng fallback

## 13. COMPLETION REPORT
- Báo cáo hoàn tất pipeline tài nguyên tĩnh và hình ảnh thời trang.
