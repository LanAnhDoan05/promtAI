# PROMPT 120 – REALTIME SSE CONCURRENCY & CONNECTION DROP RECOVERY TEST

## 1. ROLE
Realtime Systems Engineer

## 2. OBJECTIVE
Kiểm thử độ bền bỉ và khả năng tự phục hồi của kênh truyền thông Server-Sent Events (SSE): Giả lập 100 kết nối SSE đồng thời, mô phỏng tình huống rớt mạng đột ngột (network disconnect), xác minh client tự động kết nối lại (Auto-reconnect), không rò rỉ bộ nhớ (Zero Memory Leak) và sự kiện mới được phát đầy đủ đến toàn bộ các máy khách đang mở.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_03_FULL_SYSTEM_ACCEPTANCE_TESTING.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_03_FULL_SYSTEM_ACCEPTANCE_TESTING.md)
> - [USER_MASTER_PROMPT_08_FINAL_REGRESSION_AND_HANDOVER.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_08_FINAL_REGRESSION_AND_HANDOVER.md)
> - [USER_MASTER_PROMPT_17_SYSTEM_STABILITY_FINAL_ACCEPTANCE.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_17_SYSTEM_STABILITY_FINAL_ACCEPTANCE.md)
> - [USER_MASTER_PROMPT_20_FINAL_E2E_INTEGRATION_TEST.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_20_FINAL_E2E_INTEGRATION_TEST.md)

## 3. CONTEXT
Kênh SSE phục vụ thông báo đơn hàng và tiếp nhận Lead tư vấn. Hệ thống phải đảm bảo khi nhân viên mang laptop đi từ phòng này sang phòng khác (đổi mạng Wi-Fi), kết nối tự động khôi phục trong vòng 3 giây mà không cần F5 trang.

## 4. PREREQUISITES
- PROMPT_047: SSE Broadcaster
- PROMPT_102: Consultation Desk

## 5. INPUTS
- Endpoint SSE /api/v1/realtime

## 6. DETAILED TASKS
1. **Kiểm thử 100 Kết Nối SSE Đồng Thời**:
   Mở 100 kết nối client giả lập tới /api/v1/realtime, theo dõi dung lượng RAM của Node.js process (không tăng đột biến).

2. **Mô phỏng Đứt Kết Nối và Tự Động Kết Nối Lại**:
   Ngắt socket kết nối đột ngột từ phía server. Kiểm tra client Frontend tự động kích hoạt cơ chế thử lại sau 3 giây và duy trì trạng thái bình thường.

3. **Kiểm thử Phát Sự Kiện Đồng Loạt (Broadcast Test)**:
   Tạo 1 đơn hàng mới -> Xác nhận 100 client đều nhận được thông báo sự kiện NEW_ORDER trong vòng chưa đầy 500ms.

## 7. TECHNICAL REQUIREMENTS
- Heartbeat ping mỗi 30 giây để giữ kết nối qua các proxy/firewall
- Dọn sạch listener trong event emitter khi client ngắt kết nối

## 8. INTEGRATION REQUIREMENTS
- Admin Portal notification bell

## 9. SAFETY CONSTRAINTS
- ⚠️ **Max Listeners Exceeded Warning**: Cấu hình event emitter maxListeners hợp lý để không bị cảnh báo rò rỉ bộ nhớ.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: 100 kết nối duy trì ổn định không làm nghẽn server.
[ ] **AC-2**: Client tự động phục hồi kết nối thành công sau khi mạng gián đoạn.
[ ] **AC-3**: RAM của backend process duy trì ổn định không tăng phi mã.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Chạy script giả lập 50 kết nối SSE và kiểm tra phát sự kiện đồng loạt

## 12. EXPECTED OUTPUT
- `docs/ADMIN_CUSTOMER_REALTIME_SYNC_REPORT.md`: Báo cáo kiểm thử đồng bộ thời gian thực SSE

## 13. COMPLETION REPORT
- Kiểm thử chịu tải và tự phục hồi kết nối Server-Sent Events hoàn thành
