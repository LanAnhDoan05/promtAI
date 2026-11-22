# PROMPT 007 – XÂY DỰNG CHÍNH SÁCH AN NINH & BẢO VỆ DỮ LIỆU NGƯỜI DÙNG

## 1. ROLE
Lead Cybersecurity Engineer

## 2. OBJECTIVE
Thiết lập chính sách an ninh thông tin, phòng chống tấn công mạng và tuân thủ các quy định bảo vệ dữ liệu cá nhân.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_06_FULL_SYSTEM_AUDIT_AND_OPTIMIZATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_06_FULL_SYSTEM_AUDIT_AND_OPTIMIZATION.md)
> - [USER_MASTER_PROMPT_22_COMPREHENSIVE_TECHNICAL_AUDIT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_22_COMPREHENSIVE_TECHNICAL_AUDIT.md)
> - [USER_MASTER_PROMPT_30_FROM_ZERO_PROMPT_LIBRARY_SPECIFICATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_30_FROM_ZERO_PROMPT_LIBRARY_SPECIFICATION.md)

## 3. CONTEXT
Routine xử lý dữ liệu tài khoản, địa chỉ giao hàng và giao dịch thanh toán trực tuyến của khách hàng, đòi hỏi tiêu chuẩn bảo mật nghiêm ngặt.

## 4. PREREQUISITES
- PROMPT_004 hoàn thành

## 5. INPUTS
- docs/00_SYSTEM_ARCHITECTURE_DOCUMENT.md
- Quy định bảo mật OWASP Top 10

## 6. DETAILED TASKS
1. **Thiết kế cơ chế xác thực & Phân quyền**:
   Mã hóa mật khẩu bằng bcryptjs (salt rounds 10), token JWT có thời hạn và RBAC 3 lớp.

2. **Chính sách phòng vệ API**:
   Cấu hình Rate Limiting chống Brute-force/DDoS, CORS whitelist, HTTP Security Headers bằng Helmet.

3. **Chính sách bảo mật thanh toán VNPAY**:
   Bảo vệ Merchant Secret, kiểm tra chữ ký HMAC-SHA512 và xác thực số tiền trước khi duyệt đơn.

## 7. TECHNICAL REQUIREMENTS
- Tuân thủ chuẩn bảo mật thanh toán PCI-DSS áp dụng cho Merchant
- Mã hóa đường truyền toàn diện qua HTTPS / TLS 1.3

## 8. INTEGRATION REQUIREMENTS
- Áp dụng middleware bảo mật xuyên suốt Express pipeline.


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Cấm lưu thông tin thẻ ngân hàng**: Không được lưu số thẻ, mã CVV/CVC của khách hàng trên hệ thống Routine.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Tài liệu chính sách bảo mật hệ thống được phê duyệt
[ ] **AC-2**: Checklist bảo mật OWASP Top 10 hoàn tất

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Rà soát các kịch bản tấn công SQL Injection, XSS, CSRF và Brute-force

## 12. EXPECTED OUTPUT
- `docs/00_SECURITY_AND_COMPLIANCE_POLICY.md`: Chính sách an ninh thông tin và bảo vệ dữ liệu

## 13. COMPLETION REPORT
- Xác nhận ban hành chính sách an ninh cho toàn bộ hệ thống.
