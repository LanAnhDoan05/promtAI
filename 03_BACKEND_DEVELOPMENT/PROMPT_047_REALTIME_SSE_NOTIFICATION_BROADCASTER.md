# PROMPT 047 – SERVER-SENT EVENTS (SSE) REALTIME NOTIFICATION & EVENT BROADCASTER

## 1. ROLE
Backend Realtime Systems Engineer

## 2. OBJECTIVE
Xây dựng kênh truyền thông thời gian thực sử dụng Server-Sent Events (SSE) tại endpoint /api/v1/realtime để đồng bộ thông báo đơn hàng mới, biến động tồn kho và tin nhắn tư vấn AI Lead đến Admin Portal.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_02_CLOUDINARY_ADMIN_PRODUCT_MANAGEMENT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_02_CLOUDINARY_ADMIN_PRODUCT_MANAGEMENT.md)
> - [USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md)
> - [USER_MASTER_PROMPT_25_PRODUCTION_UPGRADE_NOTIFICATION_HANDOFF.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_25_PRODUCTION_UPGRADE_NOTIFICATION_HANDOFF.md)

## 3. CONTEXT
Ban quản trị Routine cần nhận thông báo tức thì khi có đơn hàng mới hoặc khi trợ lý AI Stylist chuyển giao (handoff) một khách hàng cần tư vấn trực tiếp, mà không cần phải tải lại trang hoặc dùng WebSocket phức tạp.

## 4. PREREQUISITES
- PROMPT_031: Express HTTP Server Architecture
- PROMPT_027: Notification Model

## 5. INPUTS
- HTTP connection duy trì với header text/event-stream

## 6. DETAILED TASKS
1. **Xây dựng RealtimeService quản lý danh sách Client kết nối**:
   Tạo Map lưu trữ các kết nối SSE đang mở: addClient(id, res), removeClient(id), broadcast(eventType, data), sendToUser(userId, eventType, data).

2. **Tạo Endpoint SSE GET /api/v1/realtime**:
   Thiết lập headers: Content-Type: "text/event-stream", Cache-Control: "no-cache", Connection: "keep-alive". Gửi ping định kỳ 30 giây để duy trì kết nối.

3. **Xây dựng cơ chế phát sự kiện từ các Service khác**:
   Tạo hàm notifyNewOrder(order), notifyAiLeadHandoff(lead), notifyStockAlert(variant) để các service khác gọi khi có biến động dữ liệu.

## 7. TECHNICAL REQUIREMENTS
- Chuẩn SSE: "event: <name>\ndata: <json>\n\n"
- Xử lý ngắt kết nối (res.on("close")) sạch sẽ để không rò rỉ bộ nhớ (Memory Leak)

## 8. INTEGRATION REQUIREMENTS
- Admin Header notification bell và Consultation Leads desk lắng nghe SSE này

## 9. SAFETY CONSTRAINTS
- ⚠️ **Connection Exhaustion**: Giới hạn số lượng kết nối đồng thời từ cùng 1 IP để chống DoS.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Kết nối GET /api/v1/realtime duy trì thông suốt không bị ngắt quãng.
[ ] **AC-2**: Khi có đơn hàng mới tạo, client SSE nhận được sự kiện NEW_ORDER trong < 1 giây.
[ ] **AC-3**: Client ngắt kết nối được xóa sạch khỏi bộ nhớ server.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Mở kết nối cURL tới /api/v1/realtime và kích hoạt tạo đơn hàng để xem stream dữ liệu

## 12. EXPECTED OUTPUT
- `backend/src/services/realtimeService.js`: Dịch vụ phát sóng SSE thời gian thực
- `backend/src/controllers/realtimeController.js`: Controller quản lý kết nối SSE

## 13. COMPLETION REPORT
- Hệ thống thông báo thời gian thực Server-Sent Events đã hoàn thành
