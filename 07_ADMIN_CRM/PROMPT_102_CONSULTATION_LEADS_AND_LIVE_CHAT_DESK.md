# PROMPT 102 – CONSULTATION LEADS & LIVE CHAT REALTIME HANDOFF DESK (SSE)

## 1. ROLE
Realtime Systems & Customer Service Specialist

## 2. OBJECTIVE
Xây dựng Bàn trực tư vấn khách hàng (app/admin/consultations/page.js): Tiếp nhận ngay lập tức các Lead được AI Stylist chuyển giao (Handoff) qua kết nối Server-Sent Events (SSE), hiển thị danh sách khách hàng đang chờ tư vấn kèm điểm Lead Score (HOT, WARM), chuông thông báo âm thanh, xem toàn bộ lịch sử chat trước đó, và cho phép chuyên viên gửi tin nhắn trực tiếp tiếp quản phiên chat.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_05_AI_BUSINESS_INTELLIGENCE_AUDIT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_05_AI_BUSINESS_INTELLIGENCE_AUDIT.md)
> - [USER_MASTER_PROMPT_24_ADMIN_NOTIFICATION_CENTER.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_24_ADMIN_NOTIFICATION_CENTER.md)
> - [USER_MASTER_PROMPT_28_AI_BI_IMPLEMENTATION_AND_E2E_AUDIT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_28_AI_BI_IMPLEMENTATION_AND_E2E_AUDIT.md)
> - [USER_MASTER_PROMPT_29_BI_DASHBOARD_TABLES_UI_OPTIMIZATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_29_BI_DASHBOARD_TABLES_UI_OPTIMIZATION.md)

## 3. CONTEXT
Đây là mắt xích kết nối giữa trí tuệ nhân tạo và chuyên viên tư vấn con người. Nhân viên chăm sóc khách hàng có thể chốt đơn trực tiếp ngay khi khách hàng có nhu cầu cao nhất.

## 4. PREREQUISITES
- PROMPT_088: Handoff Workflow
- PROMPT_047: SSE Broadcaster

## 5. INPUTS
- SSE endpoint /api/v1/realtime và Consultation APIs

## 6. DETAILED TASKS
1. **Kết Nối SSE và Xử Lý Thông Báo Âm Thanh**:
   Mở EventSource tới /api/v1/realtime. Khi nhận sự kiện AI_LEAD: phát âm thanh thông báo nhẹ nhàng (bell chime), hiển thị Toast thông báo và đưa Lead mới lên đầu danh sách.

2. **Bảng Bàn Trực Tư Vấn (Consultation Desk)**:
   Danh sách các cuộc trò chuyện cần hỗ trợ: Tên khách, SĐT, Điểm Lead Score (ví dụ: 85/100 - HOT), Dịp mặc đang tìm, Trạng thái (MỚI, ĐANG TƯ VẤN, ĐÃ CHỐT ĐƠN).

3. **Khung Tiếp Quản Tin Nhắn (Live Chat Takeover)**:
   Bấm vào một Lead: nạp toàn bộ lịch sử trò chuyện giữa khách và AI Stylist. Khung nhập tin nhắn để chuyên viên gửi tin nhắn trực tiếp tới khách hàng (sender: "STAFF").

## 7. TECHNICAL REQUIREMENTS
- EventSource auto-reconnect khi mạng chập chờn
- Đánh dấu trạng thái "Đã tiếp nhận" để các nhân viên khác không vào trùng

## 8. INTEGRATION REQUIREMENTS
- Đồng bộ 2 chiều với cửa sổ chat của khách hàng

## 9. SAFETY CONSTRAINTS
- ⚠️ **Audio Autoplay Policy**: Chỉ phát âm thanh sau khi nhân viên đã có ít nhất một tương tác click chuột trên trang.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Khi khách bên ngoài để lại SĐT, bàn trực tư vấn nhận được thông báo trong < 1s.
[ ] **AC-2**: Chuyên viên xem được toàn bộ 5 lượt chat trước đó của AI và khách.
[ ] **AC-3**: Gửi tin nhắn phản hồi xuất hiện ngay trên màn hình chat của khách hàng.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Mở song song 2 trình duyệt (Storefront và Admin Desk) kiểm thử luồng chuyển giao realtime

## 12. EXPECTED OUTPUT
- `frontend/src/app/admin/consultations/page.js`: Bàn trực tư vấn khách hàng Realtime
- `frontend/src/components/Admin/LiveChatDesk.jsx`: Khung tiếp quản chat

## 13. COMPLETION REPORT
- Bàn trực tiếp nhận Lead và Live Chat Realtime hoàn thành
