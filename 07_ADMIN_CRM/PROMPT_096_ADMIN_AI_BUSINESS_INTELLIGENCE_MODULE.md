# PROMPT 096 – AI BUSINESS INTELLIGENCE (BI) MODULE: REVENUE, CONVERSION & AI RECOMMENDATIONS

## 1. ROLE
AI Data Scientist / Full-stack Developer

## 2. OBJECTIVE
Xây dựng module Phân tích kinh doanh thông minh bằng AI (app/admin/ai-bi/page.js): Nút "Chạy phân tích AI ngay" kích hoạt Gemini tổng hợp dữ liệu doanh số, tỷ lệ xem/mua, và sinh ra báo cáo chiến lược: Tóm tắt điều hành (Executive Summary), Đánh giá rủi ro tồn kho, và các Khuyến nghị hành động (Khuyến nghị giá, tiếp thị, bổ sung hàng).


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_05_AI_BUSINESS_INTELLIGENCE_AUDIT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_05_AI_BUSINESS_INTELLIGENCE_AUDIT.md)
> - [USER_MASTER_PROMPT_24_ADMIN_NOTIFICATION_CENTER.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_24_ADMIN_NOTIFICATION_CENTER.md)
> - [USER_MASTER_PROMPT_28_AI_BI_IMPLEMENTATION_AND_E2E_AUDIT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_28_AI_BI_IMPLEMENTATION_AND_E2E_AUDIT.md)
> - [USER_MASTER_PROMPT_29_BI_DASHBOARD_TABLES_UI_OPTIMIZATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_29_BI_DASHBOARD_TABLES_UI_OPTIMIZATION.md)
> - ⭐ **Tài liệu tham chiếu trực tiếp:** [USER_MASTER_PROMPT_28_AI_BI_IMPLEMENTATION_AND_E2E_AUDIT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_28_AI_BI_IMPLEMENTATION_AND_E2E_AUDIT.md)

## 3. CONTEXT
Routine tích hợp trí tuệ nhân tạo Gemini để đóng vai trò như một chuyên gia tư vấn chiến lược kinh doanh cho ban giám đốc, biến các con số thống kê khô khan thành các đề xuất hành động thực tiễn.

## 4. PREREQUISITES
- PROMPT_028: AI BI Models
- PROMPT_079: Gemini Client

## 5. INPUTS
- API POST /api/v1/admin/ai-bi/analyze và GET /api/v1/admin/ai-bi/latest

## 6. DETAILED TASKS
1. **Backend Aggregation Service cho BI**:
   Tính toán tổng doanh thu, số đơn, AOV (giá trị đơn trung bình), top 5 sản phẩm bán chạy, top 5 sản phẩm xem nhiều nhưng mua ít, tỷ lệ chuyển đổi.

2. **Gọi Gemini Sinh Khuyến Nghị Chiến Lược**:
   Cung cấp dữ liệu tổng hợp cho Gemini với System Prompt phân tích kinh doanh thời trang: Yêu cầu trả về báo cáo có cấu trúc JSON gồm: summary, risks, recommendations (title, priority, action, impact).

3. **Xây dựng Giao diện AI BI Dashboard**:
   Hiển thị bản tóm tắt điều hành của AI, các thẻ khuyến nghị phân loại theo mức độ ưu tiên (HIGH, MEDIUM, LOW), và các nút đánh dấu trạng thái "Đang thực hiện", "Hoàn thành".


### QUY CHUẨN KIẾN TRÚC AI BUSINESS INTELLIGENCE (Theo USER_MASTER_PROMPT_28):
1. **Nguyên tắc cốt lõi:**
   - KHÔNG sử dụng dữ liệu giả (fake data) hay hardcode số liệu doanh thu.
   - KHÔNG để Gemini tự bịa số liệu. Toàn bộ con số tài chính (Doanh thu, Đơn hàng, AOV, Tỷ trọng) PHẢI được tính toán từ MySQL trước khi truyền vào prompt Gemini.
   - Lưu trữ lịch sử phân tích vào 2 bảng: `AiBiReport` và `AiBiRecommendation`.
2. **Cấu trúc JSON trả về từ Gemini:**
   - Phải định dạng JSON Schema: `{ summary: string, risks: string, recommendations: Array<{ title, priority, action, impact }> }`.


## 7. TECHNICAL REQUIREMENTS
- Lưu trữ lịch sử báo cáo vào bảng AiBiReport và AiBiRecommendation
- Tránh gọi Gemini lặp lại nếu dữ liệu chưa thay đổi trong vòng 6 giờ

## 8. INTEGRATION REQUIREMENTS
- Admin Portal navigation và Database

## 9. SAFETY CONSTRAINTS
- ⚠️ **Zero Fictitious Numbers**: Tuyệt đối không để Gemini tự bịa số liệu doanh thu; toàn bộ con số phải lấy từ kết quả truy vấn MySQL thực tế.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Bấm "Chạy phân tích AI" sinh ra báo cáo phân tích chiến lược trong vòng 5 giây.
[ ] **AC-2**: Các khuyến nghị có tính ứng dụng cao cho ngành thời trang.
[ ] **AC-3**: Báo cáo được lưu trữ bền vững trong database.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kích hoạt phân tích AI và xác minh các khuyến nghị được lưu vào MySQL

## 12. EXPECTED OUTPUT
- `backend/src/services/aiBiService.js`: Dịch vụ phân tích kinh doanh bằng AI
- `frontend/src/app/admin/ai-bi/page.js`: Trang giao diện AI BI Dashboard

## 13. COMPLETION REPORT
- Module phân tích kinh doanh thông minh AI Business Intelligence hoàn thành
