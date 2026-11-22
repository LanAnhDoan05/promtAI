# PROMPT 116 – DATABASE REFERENTIAL INTEGRITY, CONCURRENCY & DEADLOCK STRESS TEST

## 1. ROLE
Database Reliability Engineer

## 2. OBJECTIVE
Thực hiện kiểm thử áp lực đồng thời (Concurrency Stress Test) và kiểm tra toàn vẹn cơ sở dữ liệu: Mô phỏng 20 luồng đồng thời cùng đặt mua 1 chiếc áo cuối cùng trong kho để xác minh cơ chế StockReservation không bị bán vượt tồn kho (Zero Overselling), kiểm tra khóa giao dịch không xảy ra Deadlock, và kiểm toán tính toàn vẹn tham chiếu khóa ngoại.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_03_FULL_SYSTEM_ACCEPTANCE_TESTING.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_03_FULL_SYSTEM_ACCEPTANCE_TESTING.md)
> - [USER_MASTER_PROMPT_08_FINAL_REGRESSION_AND_HANDOVER.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_08_FINAL_REGRESSION_AND_HANDOVER.md)
> - [USER_MASTER_PROMPT_17_SYSTEM_STABILITY_FINAL_ACCEPTANCE.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_17_SYSTEM_STABILITY_FINAL_ACCEPTANCE.md)
> - [USER_MASTER_PROMPT_20_FINAL_E2E_INTEGRATION_TEST.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_20_FINAL_E2E_INTEGRATION_TEST.md)

## 3. CONTEXT
Trong các sự kiện Flash Sale lớn, hàng nghìn khách hàng có thể cùng tranh mua một món đồ giảm giá sốc. Hệ thống cơ sở dữ liệu phải giữ vững tính nhất quán tuyệt đối dưới tải cao.

## 4. PREREQUISITES
- PROMPT_042: Stock Reservation
- PROMPT_022: Order Transaction

## 5. INPUTS
- Script kiểm thử đồng thời Node.js đa luồng

## 6. DETAILED TASKS
1. **Mô phỏng Đặt Hàng Đồng Thời (Race Condition Test)**:
   Thiết lập 1 biến thể SKU có stock = 1. Gửi đồng thời 20 request tạo đơn hàng trong cùng 1 phần nghìn giây.

2. **Xác Minh Kết Quả Tồn Kho và Đơn Hàng**:
   Xác nhận chỉ có duy nhất 1 đơn hàng tạo thành công và giữ được hàng; 19 đơn hàng còn lại nhận được thông báo "Sản phẩm đã hết hàng". Tồn kho cuối cùng chính xác bằng 0, không bị âm.

3. **Kiểm tra Deadlock và Transaction Timeout**:
   Xác minh không có lỗi MySQL Deadlock 1213 xuất hiện trong log server nhờ thứ tự truy vấn tài nguyên nhất quán.

## 7. TECHNICAL REQUIREMENTS
- Prisma transaction isolation level chuẩn
- Tồn kho khả dụng không bao giờ < 0

## 8. INTEGRATION REQUIREMENTS
- Database MySQL 8.0

## 9. SAFETY CONSTRAINTS
- ⚠️ **Connection Exhaustion during Spike**: Cấu hình connection_limit hợp lý trong DATABASE_URL để server không sập khi có nhiều luồng đồng thời.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Không xảy ra hiện tượng overselling (bán âm kho) dưới mọi tình huống đồng thời.
[ ] **AC-2**: Không xảy ra deadlock làm crash server.
[ ] **AC-3**: Dữ liệu khóa ngoại và bảng nối toàn vẹn 100%.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Chạy script stress test đồng thời 20 luồng và kiểm tra bản ghi MySQL sau khi chạy

## 12. EXPECTED OUTPUT
- `docs/DATABASE_INTEGRITY_REPORT.md`: Báo cáo kiểm thử toàn vẹn và chịu tải database

## 13. COMPLETION REPORT
- Kiểm thử toàn vẹn dữ liệu và chịu tải đồng thời hoàn thành xuất sắc
