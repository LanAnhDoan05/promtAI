# PROMPT 122 – FRONTEND NEXT.JS PRODUCTION BUILD OPTIMIZATION (ALL 38 APP ROUTES)

## 1. ROLE
Lead DevOps / Frontend Build Specialist

## 2. OBJECTIVE
Thực thi tối ưu hóa biên dịch Production cho toàn bộ 38 routes của ứng dụng Next.js 16.4.3: Chạy npm run build, tối ưu hóa bundle size, loại bỏ dead code (tree shaking), tối ưu hóa Static Site Generation (SSG) cho các trang tĩnh, Incremental Static Regeneration (ISR) cho danh mục sản phẩm, và đảm bảo biên dịch 38 routes hoàn thành 100% không có lỗi chặn.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_10_FINAL_HANDOVER_LOCK.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_10_FINAL_HANDOVER_LOCK.md)
> - [USER_MASTER_PROMPT_17_SYSTEM_STABILITY_FINAL_ACCEPTANCE.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_17_SYSTEM_STABILITY_FINAL_ACCEPTANCE.md)

## 3. CONTEXT
Biên dịch Production chuẩn xác giúp trang web tải siêu tốc, giảm kích thước file JavaScript tải về trình duyệt và cải thiện điểm SEO Google Lighthouse lên mức tối đa.

## 4. PREREQUISITES
- PROMPT_121: Phase 09 Signoff Gateway

## 5. INPUTS
- Mã nguồn frontend trong frontend/src/

## 6. DETAILED TASKS
1. **Kiểm tra Cấu hình next.config.js**:
   Cấu hình images.remotePatterns (Cloudinary, local assets), compress: true, powerByHeader: false, tối ưu hóa compiler.

2. **Chạy Lệnh Biên Dịch Production**:
   Thực thi npm run build trong frontend. Xác nhận Next.js App Router biên dịch thành công tất cả 38 routes (trang chủ, danh mục, chi tiết, giỏ hàng, checkout, account, admin...).

3. **Phân Tích Kích Thước Bundle (Bundle Analyzer)**:
   Đảm bảo First Load JS Shared của mỗi trang dưới 150kB để thời gian tải trang ban đầu luôn dưới 1 giây.

## 7. TECHNICAL REQUIREMENTS
- Next.js 16.4.3 Turbopack production compilation
- Zero build failure (Exit code 0)
- Khuyến nghị nâng cấp Next.js khi môi trường yêu cầu bảo mật cao hơn

## 8. INTEGRATION REQUIREMENTS
- Thư mục build .next/ sẵn sàng cho npm start


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Build Time Environment Variables**: Đảm bảo các biến NEXT_PUBLIC_* đã được nạp đầy đủ trong quá trình build.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Lệnh npm run build hoàn thành thành công với mã thoát 0.
[ ] **AC-2**: Tất cả 38 routes hiển thị biểu tượng Static (○) hoặc Dynamic (ƒ) hợp lệ trong bảng tổng kết build.
[ ] **AC-3**: Chạy npm start khởi động server production mượt mà trên cổng 3000.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Chạy npm run build và kiểm tra log tổng kết kích thước của 38 routes

## 12. EXPECTED OUTPUT
- `frontend/.next/`: Thư mục build production hoàn chỉnh

## 13. COMPLETION REPORT
- Biên dịch và tối ưu hóa Production Frontend Next.js hoàn thành
