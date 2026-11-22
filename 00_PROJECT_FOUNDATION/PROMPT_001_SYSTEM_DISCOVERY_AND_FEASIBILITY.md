# PROMPT 001 – KHẢO SÁT HỆ THỐNG ROUTINE & ĐÁNH GIÁ TÍNH KHẢ THI DỰ ÁN

## 1. ROLE
Principal System Analyst & Business Architect

## 2. OBJECTIVE
Khảo sát toàn diện mô hình kinh doanh bán lẻ thời trang của Routine, đánh giá tính khả thi kỹ thuật và xác lập phạm vi ranh giới hệ thống từ con số 0.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_06_FULL_SYSTEM_AUDIT_AND_OPTIMIZATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_06_FULL_SYSTEM_AUDIT_AND_OPTIMIZATION.md)
> - [USER_MASTER_PROMPT_22_COMPREHENSIVE_TECHNICAL_AUDIT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_22_COMPREHENSIVE_TECHNICAL_AUDIT.md)
> - [USER_MASTER_PROMPT_30_FROM_ZERO_PROMPT_LIBRARY_SPECIFICATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_30_FROM_ZERO_PROMPT_LIBRARY_SPECIFICATION.md)

## 3. CONTEXT
Routine là thương hiệu thời trang nam nữ đương đại hàng đầu tại Việt Nam. Dự án yêu cầu xây dựng lại nền tảng E-commerce đa kênh kết hợp Trợ lý thời trang AI Stylist và Hệ thống phân tích kinh doanh AI BI.

## 4. PREREQUISITES
- Khởi động dự án tại thư mục trống
- Đã tiếp nhận yêu cầu tổng quan từ Ban giám đốc

## 5. INPUTS
- Tài liệu nghiên cứu thương hiệu Routine
- Danh mục sản phẩm thời trang mẫu
- Báo cáo khảo sát người dùng

## 6. DETAILED TASKS
1. **Phân tích mô hình kinh doanh bán lẻ**:
   Xác định các dòng sản phẩm chủ lực (Men, Women, New Arrivals), chính sách giá, khuyến mãi và chuỗi cung ứng.

2. **Đánh giá tính khả thi công nghệ (Feasibility Study)**:
   Thẩm định stack công nghệ: Next.js 16 (App Router), Express.js, MySQL 8.0, Prisma ORM, Google Gemini 2.5 Flash và VNPAY.

3. **Xác lập ranh giới hệ thống (Scope & Boundaries)**:
   Vạch rõ phạm vi MVP bao gồm Storefront, AI Stylist, Checkout VNPay và Admin Portal.

## 7. TECHNICAL REQUIREMENTS
- Hệ thống phải hỗ trợ mô hình đa nền tảng (Responsive Desktop, Tablet, Mobile)
- Thời gian phản hồi API trung bình dưới 200ms
- Tương thích chuẩn thanh toán trực tuyến Ngân hàng Nhà nước Việt Nam

## 8. INTEGRATION REQUIREMENTS
- Kết nối các phân hệ Storefront, AI Stylist, Payment Gateway và Admin Portal thành một thể thống nhất.


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Phạm vi bất biến**: Không mở rộng sang mô hình Marketplace nhiều người bán (Multi-vendor) trong giai đoạn này.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Báo cáo khảo sát khả thi (Feasibility Study Report) được phê duyệt
[ ] **AC-2**: Sơ đồ ngữ cảnh hệ thống (System Context Diagram) được thống nhất

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Rà soát ma trận rủi ro kỹ thuật và phương án dự phòng

## 12. EXPECTED OUTPUT
- `docs/00_FEASIBILITY_REPORT.md`: Báo cáo tính khả thi và phạm vi dự án Routine

## 13. COMPLETION REPORT
- Xác nhận hoàn thành khảo sát và chuyển giao tài liệu cho giai đoạn đặc tả BRD.
