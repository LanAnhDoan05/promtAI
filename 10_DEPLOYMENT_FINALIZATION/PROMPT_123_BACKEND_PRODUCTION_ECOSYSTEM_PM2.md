# PROMPT 123 – BACKEND PRODUCTION ECOSYSTEM & PROCESS MANAGER CONFIGURATION (PM2 / SYSTEMD)

## 1. ROLE
DevOps & Infrastructure Specialist

## 2. OBJECTIVE
Xây dựng cấu hình quản lý tiến trình backend cho môi trường Production sử dụng PM2 (ecosystem.config.js) hoặc Systemd: Tự động khởi động lại khi crash, quản lý log tập trung, cấu hình chế độ cụm (Cluster Mode) tận dụng đa nhân CPU, và giới hạn mức tiêu thụ RAM tối đa (max_memory_restart: 500M).


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_10_FINAL_HANDOVER_LOCK.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_10_FINAL_HANDOVER_LOCK.md)
> - [USER_MASTER_PROMPT_17_SYSTEM_STABILITY_FINAL_ACCEPTANCE.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_17_SYSTEM_STABILITY_FINAL_ACCEPTANCE.md)

## 3. CONTEXT
Trên máy chủ thực tế, backend Node.js phải hoạt động liên tục 24/7/365 và tự động phục hồi ngay lập tức nếu gặp sự cố bất ngờ.

## 4. PREREQUISITES
- PROMPT_121: Security Gateway
- PROMPT_031: Express Entrypoint

## 5. INPUTS
- Entrypoint bin/www và biến môi trường production

## 6. DETAILED TASKS
1. **Tạo file backend/ecosystem.config.js**:
   Cấu hình PM2: name: "routine-backend", script: "bin/www", instances: "max" hoặc 2, exec_mode: "cluster", env_production: { NODE_ENV: "production", PORT: 5001 }, max_memory_restart: "500M", error_file: "logs/err.log", out_file: "logs/out.log", merge_logs: true.

2. **Thiết Lập Tự Động Khởi Động Cùng Hệ Thống**:
   Cấu hình pm2 startup và pm2 save để tự khởi động lại dịch vụ khi máy chủ khởi động lại.

3. **Kịch Bản Khởi Động start.bat và run_all.bat Cho Windows / Linux**:
   Cung cấp script khởi động tự động kiểm tra cổng 5001 và 3000 trước khi nạp tiến trình.

## 7. TECHNICAL REQUIREMENTS
- PM2 ^5.3.0
- Cluster mode cân bằng tải round-robin nội bộ

## 8. INTEGRATION REQUIREMENTS
- Quản trị máy chủ triển khai


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Port Conflict**: Tự động giải phóng cổng hoặc cảnh báo nếu cổng 5001 đang bị tiến trình khác chiếm dụng.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: File ecosystem.config.js được cấu hình chuẩn production.
[ ] **AC-2**: PM2 khởi động ứng dụng thành công ở chế độ cluster.
[ ] **AC-3**: Tiến trình tự động khởi động lại nếu bị dừng bất ngờ.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Khởi động bằng pm2 start ecosystem.config.js --env production và kiểm tra pm2 status

## 12. EXPECTED OUTPUT
- `backend/ecosystem.config.js`: File cấu hình PM2 Production
- `start.bat`: Script khởi động tự động toàn bộ hệ thống

## 13. COMPLETION REPORT
- Cấu hình quản lý tiến trình Backend Production PM2 hoàn thành
