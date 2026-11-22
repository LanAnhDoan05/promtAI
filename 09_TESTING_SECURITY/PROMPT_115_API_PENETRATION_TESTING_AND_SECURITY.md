# PROMPT 115 – API PENETRATION TESTING, SQL INJECTION, XSS & RBAC 401/403 MATRIX

## 1. ROLE
Cybersecurity Engineer / Penetration Tester

## 2. OBJECTIVE
Thực hiện kiểm thử xâm nhập (Penetration Testing) và đánh giá bảo mật toàn diện: Quét lỗ hổng SQL Injection trên các tham số tìm kiếm, kiểm tra lọc XSS trên bình luận đánh giá và chatbox, kiểm thử ma trận phân quyền RBAC (xác minh chặn 100% các request không token hoặc token giả mạo vào route Admin với mã HTTP 401/403), và kiểm tra bảo vệ CSRF / CORS.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_03_FULL_SYSTEM_ACCEPTANCE_TESTING.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_03_FULL_SYSTEM_ACCEPTANCE_TESTING.md)
> - [USER_MASTER_PROMPT_08_FINAL_REGRESSION_AND_HANDOVER.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_08_FINAL_REGRESSION_AND_HANDOVER.md)
> - [USER_MASTER_PROMPT_17_SYSTEM_STABILITY_FINAL_ACCEPTANCE.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_17_SYSTEM_STABILITY_FINAL_ACCEPTANCE.md)
> - [USER_MASTER_PROMPT_20_FINAL_E2E_INTEGRATION_TEST.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_20_FINAL_E2E_INTEGRATION_TEST.md)

## 3. CONTEXT
Bảo mật là tiêu chuẩn sống còn của sàn thương mại điện tử Routine nhằm bảo vệ dữ liệu thông tin khách hàng và giao dịch tài chính.

## 4. PREREQUISITES
- PROMPT_033: RBAC Middleware
- PROMPT_094: Admin Portal

## 5. INPUTS
- Danh sách toàn bộ API endpoints của hệ thống

## 6. DETAILED TASKS
1. **Kiểm thử Lỗ Hổng SQL Injection**:
   Gửi các chuỗi tấn công SQLi: "' OR '1'='1", "1; DROP TABLE users;--", "UNION SELECT..." vào các ô tìm kiếm, query params và body. Xác nhận Prisma xử lý parameterized queries an toàn.

2. **Kiểm thử Tấn Công XSS (Cross-Site Scripting)**:
   Nhập các đoạn script: "<script>alert(1)</script>", "<img src=x onerror=alert(1)>" vào phần đánh giá sản phẩm, họ tên, chat tin nhắn. Xác nhận dữ liệu được escape sạch sẽ khi hiển thị.

3. **Kiểm thử Ma Trận Phân Quyền RBAC 401/403**:
   Quét 15 endpoint quản trị (/api/v1/admin/*) bằng: 1) Không có token (phải trả về 401); 2) Token khách hàng thường (phải trả về 403); 3) Token bị sửa đổi chữ ký (phải trả về 401).

## 7. TECHNICAL REQUIREMENTS
- Tuân thủ tiêu chuẩn OWASP Top 10
- Zero critical vulnerabilities

## 8. INTEGRATION REQUIREMENTS
- Tài liệu hóa các khuyến nghị vá lỗi bảo mật

## 9. SAFETY CONSTRAINTS
- ⚠️ **Safe Pen-testing**: Thực hiện kiểm thử an toàn không gây phá hủy dữ liệu.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: 100% các thử nghiệm SQL Injection và XSS đều bị vô hiệu hóa an toàn.
[ ] **AC-2**: Ma trận RBAC chặn đúng 100% các truy cập trái phép với mã 401/403.
[ ] **AC-3**: Báo cáo kiểm thử bảo mật không còn lỗ hổng mức High hoặc Critical.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Chạy script tự động quét bảo mật và kiểm tra mã trạng thái trả về

## 12. EXPECTED OUTPUT
- `docs/API_AUDIT_REPORT.md`: Báo cáo kiểm thử xâm nhập và bảo mật API

## 13. COMPLETION REPORT
- Kiểm thử bảo mật API và ma trận phân quyền RBAC hoàn thành
