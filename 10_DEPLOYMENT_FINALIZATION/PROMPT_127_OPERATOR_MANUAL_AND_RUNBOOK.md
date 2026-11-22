# PROMPT 127 – SYSTEM OPERATOR MANUAL, RUNBOOK & TROUBLESHOOTING GUIDE

## 1. ROLE
Lead Technical Documentation Specialist

## 2. OBJECTIVE
Biên soạn Bộ tài liệu hướng dẫn vận hành hệ thống (Operator Manual), Sổ tay xử lý sự cố (Troubleshooting Runbook) và Cẩm nang sử dụng cho Quản trị viên: Hướng dẫn khởi động/dừng hệ thống, hướng dẫn thêm sản phẩm mới và quản lý kho, hướng dẫn xử lý đơn hàng và đối soát VNPay, hướng dẫn sử dụng bàn trực AI Live Chat, và bảng tra cứu cách khắc phục 10 sự cố thường gặp nhất.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_10_FINAL_HANDOVER_LOCK.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_10_FINAL_HANDOVER_LOCK.md)
> - [USER_MASTER_PROMPT_17_SYSTEM_STABILITY_FINAL_ACCEPTANCE.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_17_SYSTEM_STABILITY_FINAL_ACCEPTANCE.md)

## 3. CONTEXT
Tài liệu hướng dẫn hoàn chỉnh giúp đội ngũ vận hành, chăm sóc khách hàng và các kỹ sư mới có thể tiếp quản và vận hành website Routine một cách độc lập mà không cần sự có mặt của đội ngũ phát triển ban đầu.

## 4. PREREQUISITES
- PROMPT_001 đến PROMPT_126

## 5. INPUTS
- Toàn bộ quy trình vận hành và tài liệu kỹ thuật của Routine

## 6. DETAILED TASKS
1. **Biên soạn Hướng Dẫn Vận Hành Kỹ Thuật (System Runbook)**:
   Các lệnh khởi động, dừng, xem log, sao lưu, phục hồi database, cách xoay vòng API key Gemini khi hết quota.

2. **Biên soạn Cẩm Nang Quản Trị Viên (Admin User Guide)**:
   Quy trình nhập sản phẩm biến thể SKU, quy trình duyệt đơn và in phiếu giao hàng, quy trình tiếp nhận Lead tư vấn AI.

3. **Bảng Tra Cứu Xử Lý 10 Sự Cố Thường Gặp (Troubleshooting Matrix)**:
   1) Cổng thanh toán báo sai chữ ký số; 2) Không cập nhật được tồn kho; 3) Khách hàng không nhận được email/OTP; 4) AI phản hồi chậm; 5) Lỗi Prisma file lock trên Windows (dừng backend trước khi generate); ...

## 7. TECHNICAL REQUIREMENTS
- Định dạng Markdown chuẩn hóa, mục lục liên kết rõ ràng
- Chụp ảnh minh họa từng bước thao tác

## 8. INTEGRATION REQUIREMENTS
- Lưu trong thư mục docs/ của dự án


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Clear Escalation Path**: Ghi rõ số điện thoại và thông tin liên hệ của đầu mối kỹ thuật khi gặp sự cố nghiêm trọng cấp 1.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Tài liệu hướng dẫn vận hành chi tiết, mạch lạc và đầy đủ thông tin.
[ ] **AC-2**: Bao gồm bảng hướng dẫn xử lý sự cố Prisma file lock trên Windows.
[ ] **AC-3**: Bất kỳ kỹ sư mới nào đọc tài liệu đều có thể vận hành được hệ thống.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm tra đọc và làm theo các bước trong tài liệu đảm bảo không có bước nào bị thiếu

## 12. EXPECTED OUTPUT
- `docs/OPERATOR_MANUAL_AND_RUNBOOK.md`: Sổ tay hướng dẫn vận hành và xử lý sự cố
- `docs/USER_TESTING_GUIDE.md`: Hướng dẫn kiểm thử và sử dụng dành cho người dùng

## 13. COMPLETION REPORT
- Bộ tài liệu hướng dẫn vận hành và sổ tay xử lý sự cố hoàn thành
