# PROMPT 009 – THIẾT KẾ KIẾN TRÚC AI STYLIST AGENT & RETRIEVAL ENGINE

## 1. ROLE
Principal AI Engineer

## 2. OBJECTIVE
Thiết kế sơ đồ kiến trúc chi tiết cho Trợ lý thời trang AI Stylist, cơ chế Database Grounding, quản lý ngữ cảnh đa lượt và chuyển giao tư vấn.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_06_FULL_SYSTEM_AUDIT_AND_OPTIMIZATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_06_FULL_SYSTEM_AUDIT_AND_OPTIMIZATION.md)
> - [USER_MASTER_PROMPT_22_COMPREHENSIVE_TECHNICAL_AUDIT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_22_COMPREHENSIVE_TECHNICAL_AUDIT.md)
> - [USER_MASTER_PROMPT_30_FROM_ZERO_PROMPT_LIBRARY_SPECIFICATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_30_FROM_ZERO_PROMPT_LIBRARY_SPECIFICATION.md)

## 3. CONTEXT
Khách hàng có nhu cầu tư vấn phối đồ tinh tế. AI Stylist phải đóng vai trò như một chuyên gia tư vấn tại showroom, hiểu tiếng Việt tự nhiên và gợi ý sản phẩm có sẵn trong kho.

## 4. PREREQUISITES
- PROMPT_004 hoàn thành

## 5. INPUTS
- docs/00_SYSTEM_ARCHITECTURE_DOCUMENT.md
- Tài liệu kỹ thuật Google Gemini API

## 6. DETAILED TASKS
1. **Thiết kế bộ xử lý NLP & Từ điển thời trang**:
   Xây dựng pipeline phân tích cú pháp tiếng Việt, tách thực thể (Màu, Size, Dáng, Dịp mặc, Ngân sách).

2. **Thiết kế Grounding Engine (Chống AI bịa đặt)**:
   Xây dựng thuật toán chuyển đổi yêu cầu khách hàng thành câu truy vấn MySQL thực tế, chỉ gợi ý hàng còn tồn kho.

3. **Thiết kế cơ chế Multi-turn & Human Handoff**:
   Duy trì ngữ cảnh qua `ai_conversations` và chuyển giao trạng thái sang nhân viên khi khách hàng có nhu cầu.

## 7. TECHNICAL REQUIREMENTS
- Thời gian phản hồi AI trung bình < 2.5 giây
- Cơ chế Fallback Rule Engine hoạt động ngay cả khi API Gemini mất mạng hoặc quá tải

## 8. INTEGRATION REQUIREMENTS
- Tích hợp liền mạch với cơ sở dữ liệu MySQL và bảng điều khiển Admin Leads.


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Chống Hallucination**: Tuyệt đối cấm AI tự tạo tên sản phẩm, giá bán, kích cỡ hoặc ảnh không tồn tại trong hệ thống.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Bản thiết kế kiến trúc AI Stylist Agent hoàn chỉnh
[ ] **AC-2**: Quy trình quản lý trạng thái hội thoại (State Machine) được đặc tả rõ ràng

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Mô phỏng 5 ca hội thoại phức tạp trên kịch bản thiết kế

## 12. EXPECTED OUTPUT
- `docs/00_AI_STYLIST_ARCHITECTURE_BLUEPRINT.md`: Bản vẽ kiến trúc phân hệ Trợ lý AI Stylist

## 13. COMPLETION REPORT
- Hoàn tất thẩm định thiết kế AI và chuyển giao tài liệu cho giai đoạn triển khai.
