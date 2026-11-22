# PROMPT 006 – THIẾT KẾ ĐẶC TẢ HỢP ĐỒNG RESTFUL API SPECIFICATION (OPENAPI)

## 1. ROLE
Backend API Architect

## 2. OBJECTIVE
Xây dựng bản đặc tả chi tiết toàn bộ các API Endpoints (OpenAPI / Swagger 3.0) của hệ thống Routine v1.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_06_FULL_SYSTEM_AUDIT_AND_OPTIMIZATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_06_FULL_SYSTEM_AUDIT_AND_OPTIMIZATION.md)
> - [USER_MASTER_PROMPT_22_COMPREHENSIVE_TECHNICAL_AUDIT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_22_COMPREHENSIVE_TECHNICAL_AUDIT.md)
> - [USER_MASTER_PROMPT_30_FROM_ZERO_PROMPT_LIBRARY_SPECIFICATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_30_FROM_ZERO_PROMPT_LIBRARY_SPECIFICATION.md)

## 3. CONTEXT
Bản hợp đồng API là cam kết giao tiếp giữa Frontend và Backend, giúp hai nhóm có thể phát triển song song mà không bị phụ thuộc.

## 4. PREREQUISITES
- PROMPT_004 hoàn thành

## 5. INPUTS
- docs/00_SOFTWARE_REQUIREMENT_SPECIFICATION.md

## 6. DETAILED TASKS
1. **Thiết kế Auth & Customer APIs**:
   Đặc tả `/api/v1/auth/*`, `/api/v1/customers/*`, `/api/v1/addresses/*`.

2. **Thiết kế Catalog & Order APIs**:
   Đặc tả `/api/v1/products/*`, `/api/v1/categories/*`, `/api/v1/cart/*`, `/api/v1/orders/*`.

3. **Thiết kế AI & Payment APIs**:
   Đặc tả `/api/v1/ai/chat`, `/api/v1/payment/create-payment-url`, `/api/v1/payment/vnpay-ipn`, `/api/v1/bi/analyze`.

## 7. TECHNICAL REQUIREMENTS
- Chuẩn RESTful HTTP status codes (200, 201, 400, 401, 403, 404, 500)
- Cấu trúc JSON phản hồi chuẩn hóa: `{ success: boolean, message: string, data: any, error: any }`

## 8. INTEGRATION REQUIREMENTS
- Frontend gọi API theo đúng schema JSON đã cam kết trong hợp đồng.


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Không trả thông tin nhạy cảm**: Tuyệt đối không trả về `password`, mã hash hoặc secret key trong response.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Bản đặc tả OpenAPI 3.0 hoàn chỉnh bao phủ 100% các endpoint của hệ thống
[ ] **AC-2**: Cấu trúc mã lỗi (Error Codes) được định nghĩa chi tiết

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Validate file đặc tả bằng Swagger CLI / Spectral Validator

## 12. EXPECTED OUTPUT
- `docs/00_API_SPECIFICATION_V1.yaml`: Đặc tả OpenAPI 3.0 của Routine Platform

## 13. COMPLETION REPORT
- Báo cáo hoàn tất ký duyệt hợp đồng API giữa các nhóm kỹ thuật.
