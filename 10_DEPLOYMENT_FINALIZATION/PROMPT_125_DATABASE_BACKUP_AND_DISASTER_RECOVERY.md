# PROMPT 125 – AUTOMATED DATABASE BACKUP, MIGRATION & DISASTER RECOVERY PLAN

## 1. ROLE
Database Administrator / Site Reliability Engineer

## 2. OBJECTIVE
Xây dựng kế hoạch sao lưu cơ sở dữ liệu tự động (Automated Backup) và phục hồi thảm họa (Disaster Recovery): Kịch bản mysqldump tự động sao lưu hàng ngày lúc 02:00 sáng, nén file .sql.gz, lưu trữ phân phiên bản (giữ 7 ngày gần nhất), và quy trình phục hồi cơ sở dữ liệu từng bước khi gặp sự cố phần cứng.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_10_FINAL_HANDOVER_LOCK.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_10_FINAL_HANDOVER_LOCK.md)
> - [USER_MASTER_PROMPT_17_SYSTEM_STABILITY_FINAL_ACCEPTANCE.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_17_SYSTEM_STABILITY_FINAL_ACCEPTANCE.md)

## 3. CONTEXT
Dữ liệu đơn hàng, khách hàng và giao dịch tài chính là tài sản vô giá của Routine. Một kế hoạch sao lưu và phục hồi thảm họa vững chắc giúp khôi phục hệ thống trong vòng 15 phút nếu xảy ra sự cố máy chủ.

## 4. PREREQUISITES
- PROMPT_030: Database Architecture

## 5. INPUTS
- Thông tin kết nối MySQL và đường dẫn lưu trữ bản sao lưu

## 6. DETAILED TASKS
1. **Viết Script Sao Lưu Tự Động backend/scripts/backup_database.sh (và .bat)**:
   Sử dụng mysqldump với cờ: --single-transaction --quick --routines. Đặt tên file theo ngày: routine_backup_YYYYMMDD_HHMMSS.sql.gz. Tự động xóa các file sao lưu cũ hơn 7 ngày.

2. **Thiết Lập Lịch Chạy Định Kỳ (Cron / Windows Task Scheduler)**:
   Cấu hình cronjob: 0 2 * * * chạy kịch bản sao lưu vào 2h sáng mỗi ngày.

3. **Quy Trình Phục Hồi Thảm Họa (Disaster Recovery Runbook)**:
   Tài liệu hướng dẫn khôi phục từng bước: Giải nén file backup -> Tạo database mới -> Nạp lại dữ liệu bằng mysql < file.sql -> Chạy npx prisma migrate deploy để cập nhật các migration mới nhất.

## 7. TECHNICAL REQUIREMENTS
- Sao lưu không làm khóa bảng (non-locking backup với --single-transaction)
- Thời gian phục hồi RTO < 15 phút, điểm phục hồi RPO < 24 giờ

## 8. INTEGRATION REQUIREMENTS
- Kịch bản vận hành máy chủ


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Offsite Storage Rule**: Bản sao lưu nên được đẩy lên Cloud Storage (S3 / Google Cloud Storage) để an toàn nếu máy chủ chính bị hỏng ổ cứng.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Chạy script backup tạo ra file nén .sql.gz hoàn chỉnh và kiểm tra giải nén thành công.
[ ] **AC-2**: Kịch bản phục hồi khôi phục đầy đủ 29 bảng dữ liệu nguyên vẹn.
[ ] **AC-3**: Tài liệu quy trình phục hồi thảm họa rõ ràng, dễ thao tác.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Thực hiện thử nghiệm sao lưu và khôi phục vào một database thử nghiệm

## 12. EXPECTED OUTPUT
- `backend/scripts/backup_db.bat`: Script sao lưu database trên Windows
- `docs/DISASTER_RECOVERY_RUNBOOK.md`: Quy trình phục hồi thảm họa chi tiết

## 13. COMPLETION REPORT
- Kế hoạch sao lưu tự động và phục hồi thảm họa cơ sở dữ liệu hoàn thành
