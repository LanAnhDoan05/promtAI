# PROMPT 126 – CENTRALIZED LOGGING, ERROR TRACKING & PERFORMANCE MONITORING

## 1. ROLE
DevOps / Observability Engineer

## 2. OBJECTIVE
Thiết lập hệ thống ghi log tập trung (Centralized Logging) và giám sát hiệu năng: Cấu hình xoay vòng file log (log rotation) bằng winston hoặc morgan để file log không làm đầy ổ đĩa, theo dõi thời gian phản hồi API, tích hợp giám sát lỗi (Error Tracking) và cảnh báo khi tỷ lệ lỗi 500 vượt quá ngưỡng.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_10_FINAL_HANDOVER_LOCK.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_10_FINAL_HANDOVER_LOCK.md)
> - [USER_MASTER_PROMPT_17_SYSTEM_STABILITY_FINAL_ACCEPTANCE.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_17_SYSTEM_STABILITY_FINAL_ACCEPTANCE.md)

## 3. CONTEXT
Giám sát chủ động giúp đội ngũ kỹ thuật phát hiện và khắc phục sự cố trước khi khách hàng kịp phàn nàn.

## 4. PREREQUISITES
- PROMPT_031: Express HTTP Server
- PROMPT_123: PM2 Ecosystem

## 5. INPUTS
- Hạ tầng logging hiện tại

## 6. DETAILED TASKS
1. **Cấu hình Log Rotation cho Node.js**:
   Sử dụng winston-daily-rotate-file hoặc pm2-logrotate: giới hạn dung lượng mỗi file log tối đa 20MB, lưu tối đa 14 ngày, nén tự động dạng .gz.

2. **Chuẩn Hóa Cấu Trúc Log Định Dạng JSON**:
   Mỗi dòng log chứa: timestamp (ISO 8601), level (INFO, WARN, ERROR), message, requestId, durationMs, userId (nếu có).

3. **Endpoint Giám Sát Sức Khỏe Chi Tiết (Deep Health Check)**:
   Mở rộng GET /api/v1/health: Kiểm tra kết nối MySQL, kiểm tra dung lượng RAM sử dụng, kiểm tra trạng thái kết nối Gemini AI, và thời gian server đã hoạt động (uptime).

## 7. TECHNICAL REQUIREMENTS
- JSON formatted logs
- Health check trả về HTTP 200 nếu mọi dịch vụ sẵn sàng, trả về 503 nếu database sập

## 8. INTEGRATION REQUIREMENTS
- Tương thích các công cụ giám sát (Prometheus, Datadog, Grafana, CloudWatch)


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **PII Redaction in Logs**: Tự động làm mờ (mask) mật khẩu, số thẻ ngân hàng và thông tin cá nhân nhạy cảm trước khi ghi log.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: File log được xoay vòng tự động không gây tràn ổ đĩa.
[ ] **AC-2**: Không có mật khẩu hay token bị ghi vào log.
[ ] **AC-3**: Endpoint health check phản hồi trạng thái chi tiết của từng thành phần hệ thống.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Truy cập /api/v1/health và kiểm tra cấu trúc JSON phản hồi trạng thái các thành phần

## 12. EXPECTED OUTPUT
- `backend/src/utils/logger.js`: Module ghi log chuẩn hóa
- `backend/src/routes/healthRoutes.js`: Định tuyến kiểm tra sức khỏe hệ thống

## 13. COMPLETION REPORT
- Hệ thống ghi log tập trung và giám sát sức khỏe hoàn thành
