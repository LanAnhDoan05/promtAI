# PROMPT 057 – LIVE SEARCH OVERLAY, AUTO-COMPLETE & SEARCH RESULTS PAGE

## 1. ROLE
Frontend Developer / Search UX Specialist

## 2. OBJECTIVE
Xây dựng giao diện tìm kiếm tức thì: Modal tìm kiếm mở ra khi bấm icon kính lúp trên Header, ô nhập từ khóa có debounce 300ms, gợi ý từ khóa thông minh, danh sách sản phẩm khớp nhanh (quick preview), và trang kết quả tìm kiếm đầy đủ (/search?q=...).


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_23_HERO_SLIDER_AND_BRAND_EXPERIENCE.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_23_HERO_SLIDER_AND_BRAND_EXPERIENCE.md)
> - [USER_MASTER_PROMPT_27_GLOBAL_BRANDING_AND_WARNING_AUDIT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_27_GLOBAL_BRANDING_AND_WARNING_AUDIT.md)

## 3. CONTEXT
Tìm kiếm nhanh giúp khách hàng tìm thấy đúng chiếc áo hoặc quần Routine mong muốn chỉ sau vài phím gõ. Modal tìm kiếm phủ mờ toàn màn hình tạo cảm giác tập trung và chuyên nghiệp.

## 4. PREREQUISITES
- PROMPT_051: Global Header
- PROMPT_037: Full-text Search API

## 5. INPUTS
- Từ khóa người dùng gõ vào ô tìm kiếm

## 6. DETAILED TASKS
1. **Xây dựng SearchModal Overlay**:
   Modal trượt xuống từ trên đỉnh với hiệu ứng mờ hậu cảnh (backdrop blur). Phím ESC hoặc nút X để đóng. Ô nhập từ khóa tự động focus.

2. **Xử lý Debounce và Gợi ý Tức thì**:
   Sử dụng custom hook useDebounce (300ms). Khi người dùng gõ, gọi API /api/v1/search/suggestions để hiển thị 5 từ khóa hot và 4 sản phẩm khớp nhất.

3. **Xây dựng Trang Kết quả Tìm kiếm (/search?q=...)**:
   Hiển thị: "Kết quả tìm kiếm cho '<từ khóa>': tìm thấy X sản phẩm", kèm lưới sản phẩm và bộ lọc tương tự trang danh mục.

## 7. TECHNICAL REQUIREMENTS
- Debounce chống gửi spam request khi gõ nhanh
- Highlight từ khóa khớp trong tên sản phẩm

## 8. INTEGRATION REQUIREMENTS
- Header kính lúp mở Modal; Router chuyển hướng tới /search khi nhấn Enter


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **XSS Injection Prevention**: Tuyệt đối không render từ khóa trực tiếp qua dangerouslySetInnerHTML mà không lọc an toàn.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Bấm kính lúp mở Search Modal ngay lập tức.
[ ] **AC-2**: Gõ từ khóa hiển thị gợi ý và sản phẩm xem nhanh trong vòng 300ms.
[ ] **AC-3**: Nhấn Enter chuyển đến trang kết quả tìm kiếm đầy đủ.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm thử tìm kiếm từ đồng nghĩa thời trang: gõ "ao phong" hiển thị kết quả "áo thun"

## 12. EXPECTED OUTPUT
- `frontend/src/components/Search/SearchModal.jsx`: Modal tìm kiếm nhanh
- `frontend/src/app/search/page.js`: Trang kết quả tìm kiếm đầy đủ

## 13. COMPLETION REPORT
- Giao diện tìm kiếm trực tiếp và trang kết quả tìm kiếm đã hoàn thành
