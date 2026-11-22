# PROMPT 008 – THIẾT LẬP DATA DICTIONARY & QUY TẮC TOÀN VẸN CƠ SỞ DỮ LIỆU

## 1. ROLE
Lead Database Architect

## 2. OBJECTIVE
Xây dựng từ điển dữ liệu (Data Dictionary) định nghĩa chi tiết từng bảng, từng cột, kiểu dữ liệu và ràng buộc toàn vẹn quan hệ.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_06_FULL_SYSTEM_AUDIT_AND_OPTIMIZATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_06_FULL_SYSTEM_AUDIT_AND_OPTIMIZATION.md)
> - [USER_MASTER_PROMPT_22_COMPREHENSIVE_TECHNICAL_AUDIT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_22_COMPREHENSIVE_TECHNICAL_AUDIT.md)
> - [USER_MASTER_PROMPT_30_FROM_ZERO_PROMPT_LIBRARY_SPECIFICATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_30_FROM_ZERO_PROMPT_LIBRARY_SPECIFICATION.md)

## 3. CONTEXT
Đảm bảo cơ sở dữ liệu MySQL của Routine được thiết kế chuẩn hóa 3NF, không dư thừa, hỗ trợ truy vấn hiệu năng cao và toàn vẹn dữ liệu giao dịch.

## 4. PREREQUISITES
- PROMPT_003 hoàn thành

## 5. INPUTS
- docs/00_SOFTWARE_REQUIREMENT_SPECIFICATION.md

## 6. DETAILED TASKS
1. **Đặc tả 29 bảng dữ liệu**:
   Định nghĩa chi tiết các thực thể: User, Product, Variant, Order, Payment, Cart, TrafficLog, AI BI...

2. **Thiết kế ràng buộc toàn vẹn**:
   Xác định khóa chính, khóa ngoại (ON DELETE CASCADE / RESTRICT), chỉ mục (Indexes) và ràng buộc Unique.

3. **Quy tắc định danh & Kiểu dữ liệu**:
   Quy định tiền tố ID tự sinh (`ord-`, `p-`, `var-`, `tl-`), kiểu dữ liệu tiền tệ `DECIMAL(12,2)` / `Int`.

## 7. TECHNICAL REQUIREMENTS
- Chuẩn hóa cơ sở dữ liệu đạt dạng chuẩn 3NF (Third Normal Form)
- Hỗ trợ đầy đủ bộ ký tự `utf8mb4` cho tiếng Việt có dấu

## 8. INTEGRATION REQUIREMENTS
- Đồng bộ 100% với file schema Prisma ORM trong Phase 02.


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Toàn vẹn đơn hàng**: Không cho phép xóa cứng (Hard Delete) các đơn hàng và giao dịch thanh toán đã hoàn thành.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Tài liệu Data Dictionary bao phủ đầy đủ 29 thực thể của Routine
[ ] **AC-2**: Ma trận quan hệ thực thể (ERD Matrix) được thẩm định

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm tra tính nhất quán kiểu dữ liệu giữa các bảng liên kết khóa ngoại

## 12. EXPECTED OUTPUT
- `docs/00_DATA_DICTIONARY.md`: Từ điển dữ liệu và quy tắc toàn vẹn nghiệp vụ

## 13. COMPLETION REPORT
- Chuyển giao tài liệu Data Dictionary cho giai đoạn thiết kế Prisma Schema.
