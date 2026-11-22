# PROMPT 119 – CROSS-BROWSER & CROSS-DEVICE RESPONSIVE UI/UX VISUAL REGRESSION AUDIT

## 1. ROLE
UI/UX Quality Auditor / Visual Testing Specialist

## 2. OBJECTIVE
Thực hiện kiểm toán hồi quy hình ảnh (Visual Regression Audit) trên nhiều trình duyệt (Chrome, Firefox, Safari, Edge) và 5 kích thước màn hình chuẩn: So sánh ảnh chụp giao diện trước và sau, đảm bảo không có hiện tượng lệch pixel (pixel drift), không tràn chữ, không lệch hàng trên các bảng thống kê và thẻ sản phẩm.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_03_FULL_SYSTEM_ACCEPTANCE_TESTING.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_03_FULL_SYSTEM_ACCEPTANCE_TESTING.md)
> - [USER_MASTER_PROMPT_08_FINAL_REGRESSION_AND_HANDOVER.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_08_FINAL_REGRESSION_AND_HANDOVER.md)
> - [USER_MASTER_PROMPT_17_SYSTEM_STABILITY_FINAL_ACCEPTANCE.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_17_SYSTEM_STABILITY_FINAL_ACCEPTANCE.md)
> - [USER_MASTER_PROMPT_20_FINAL_E2E_INTEGRATION_TEST.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_20_FINAL_E2E_INTEGRATION_TEST.md)

## 3. CONTEXT
Đảm bảo giao diện Routine luôn giữ vững vẻ đẹp tối giản, chỉn chu trên mọi hệ điều hành (Windows, macOS, iOS, Android) và mọi loại trình duyệt.

## 4. PREREQUISITES
- PROMPT_060: Responsive Layout
- PROMPT_097: BI Tables Optimization

## 5. INPUTS
- Ảnh chụp màn hình chuẩn của các trang chính

## 6. DETAILED TASKS
1. **Kiểm toán Giao Diện trên Safari / WebKit**:
   Kiểm tra các hiệu ứng backdrop-filter (blur), flexbox gap, bo góc border-radius và font chữ tiếng Việt trên WebKit.

2. **Kiểm toán Giao Diện trên Firefox và Chromium**:
   Xác minh thanh cuộn custom scrollbar, CSS grid và các hiệu ứng hover chuyển động.

3. **Kiểm toán Độ Tương Thích Di Động (Mobile Touch & Safe Area)**:
   Kiểm tra safe-area-inset-bottom trên iPhone (tai thỏ / dynamic island), đảm bảo nút mua hàng dính không bị thanh điều hướng che.

## 7. TECHNICAL REQUIREMENTS
- Visual regression threshold < 0.1%
- Tương thích hoàn hảo 4 trình duyệt lớn nhất

## 8. INTEGRATION REQUIREMENTS
- Lưu trữ ảnh bằng chứng vào docs/screenshots/


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Horizontal Scrollbar on Mobile**: Tuyệt đối không để phát sinh thanh cuộn ngang ở bất kỳ trang nào trên màn hình 390px.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Giao diện hiển thị đồng nhất trên cả 4 trình duyệt.
[ ] **AC-2**: Bảng thống kê BI và ProductCard giữ vững tỷ lệ chuẩn.
[ ] **AC-3**: Nút bấm trên mobile bấm chạm dễ dàng và không bị che khuất.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Chụp ảnh so sánh màn hình tại 5 viewports và kiểm tra visual diff

## 12. EXPECTED OUTPUT
- `docs/FINAL_UI_UX_REPORT.md`: Báo cáo kiểm toán chất lượng giao diện và thị giác

## 13. COMPLETION REPORT
- Kiểm toán đa trình duyệt và hồi quy hình ảnh giao diện hoàn thành
