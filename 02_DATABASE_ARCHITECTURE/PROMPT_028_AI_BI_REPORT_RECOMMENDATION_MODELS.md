# PROMPT 028 – AI BI REPORT & AI BI RECOMMENDATION ANALYTIC MODELS

## 1. ROLE
Data Architect / AI BI Specialist

## 2. OBJECTIVE
Xây dựng mô hình cơ sở dữ liệu lưu trữ kết quả phân tích kinh doanh định kỳ và khuyến nghị chiến lược được tạo bởi Gemini AI (AiBiReport, AiBiRecommendation).


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_09_REAL_DATA_AND_BUSINESS_LOGIC.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_09_REAL_DATA_AND_BUSINESS_LOGIC.md)
> - [USER_MASTER_PROMPT_13_MYSQL_AI_ADDRESS_SHIPPING_SYNC.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_13_MYSQL_AI_ADDRESS_SHIPPING_SYNC.md)
> - [USER_MASTER_PROMPT_12_ROUTINE_VN_CATALOG_SCRAPING.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_12_ROUTINE_VN_CATALOG_SCRAPING.md)

## 3. CONTEXT
Module AI Business Intelligence của Admin định kỳ tổng hợp dữ liệu doanh thu, sản phẩm bán chạy, tỷ lệ chuyển đổi, và gọi Gemini để sinh ra các phân tích chuyên sâu (SWOT, tối ưu tồn kho, chiến dịch tiếp thị). Các bản ghi báo cáo cần được lưu trữ để Admin tra cứu theo thời gian.

## 4. PREREQUISITES
- PROMPT_022: Order Model
- PROMPT_026: AI Conversation Model

## 5. INPUTS
- Cấu trúc báo cáo AI BI của Routine

## 6. DETAILED TASKS
1. **Định nghĩa Model AiBiReport**:
   Bao gồm id, reportDate (DateTime), totalRevenue (Decimal), totalOrders (Int), averageOrderValue (Decimal), conversionRate (Float?), topSellingProducts (Json?), trafficMetrics (Json?), executiveSummary (Text), riskAssessment (Text?), status (String @default("COMPLETED")), createdAt, updatedAt.

2. **Định nghĩa Model AiBiRecommendation**:
   Bao gồm id, reportId (Int), category (INVENTORY, PRICING, MARKETING, STYLING), priority (HIGH, MEDIUM, LOW), title (String), description (Text), suggestedAction (Text), impactEstimate (String?), status (String @default("PENDING")), createdAt, updatedAt. Quan hệ report AiBiReport @relation(fields: [reportId], references: [id], onDelete: Cascade).

## 7. TECHNICAL REQUIREMENTS
- Trường JSON linh hoạt lưu topSellingProducts và metrics
- Index trên reportDate, status, priority

## 8. INTEGRATION REQUIREMENTS
- Backend AI BI Service tổng hợp dữ liệu và ghi vào bảng này; Admin AI BI Dashboard truy xuất hiển thị


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Data Integrity**: Không ghi đè số liệu lịch sử; mỗi lần phân tích tạo một reportId mới có timestamp.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Models AiBiReport và AiBiRecommendation được định nghĩa trong schema.prisma.
[ ] **AC-2**: Quan hệ 1-N giữa Report và Recommendation thiết lập với Cascade Delete.
[ ] **AC-3**: npx prisma validate kiểm tra thành công.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Chạy npx prisma validate xác nhận cấu trúc bảng AI BI

## 12. EXPECTED OUTPUT
- `backend/prisma/schema.prisma`: Thêm AiBiReport, AiBiRecommendation models

## 13. COMPLETION REPORT
- Hoàn tất toàn bộ 29 models Prisma trong schema.prisma của Routine
