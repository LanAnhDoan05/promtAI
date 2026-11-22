# PROMPT 079 – GOOGLE GEMINI 2.5 FLASH CLIENT INITIALIZATION & API KEY ROTATION

## 1. ROLE
AI Systems Architect / Gemini Specialist

## 2. OBJECTIVE
Khởi tạo client Google Gemini 2.5 Flash / 1.5 Flash sử dụng @google/genai hoặc @google/generative-ai, cấu hình tham số generationConfig (temperature: 0.3 - 0.7, topP, topK), System Instruction đóng vai chuyên viên tư vấn thời trang Routine cao cấp, và cơ chế tự động xoay vòng API Key (API Key Rotation) khi gặp lỗi Rate Limit (HTTP 429).


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_01_AI_AGENT_AND_DEMO_COMPLETION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_01_AI_AGENT_AND_DEMO_COMPLETION.md)
> - [USER_MASTER_PROMPT_16_AI_STYLIST_AND_SALES_STANDARDS.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_16_AI_STYLIST_AND_SALES_STANDARDS.md)
> - [USER_MASTER_PROMPT_18_VNPAY_QR_AND_AI_HUMAN_HANDOFF.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_18_VNPAY_QR_AND_AI_HUMAN_HANDOFF.md)
> - [USER_MASTER_PROMPT_19_AI_CONTEXTUAL_CONVERSATION_FIX.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_19_AI_CONTEXTUAL_CONVERSATION_FIX.md)

## 3. CONTEXT
Trợ lý ảo AI Stylist là điểm nhấn công nghệ của Routine. Việc giao tiếp với Gemini cần độ ổn định cao, tránh gián đoạn dịch vụ khi một API key bị hết hạn ngạch hoặc quota.

## 4. PREREQUISITES
- PROMPT_014: Biến môi trường GEMINI_API_KEY
- PROMPT_031: Express Backend

## 5. INPUTS
- GEMINI_API_KEY hoặc danh sách key GEMINI_API_KEYS="key1,key2,key3"

## 6. DETAILED TASKS
1. **Xây dựng GeminiClient Singleton với Key Manager**:
   Tạo backend/src/config/gemini.js quản lý danh sách API key, hàm getActiveKey() tự động chuyển sang key kế tiếp khi nhận lỗi 429 ResourceExhausted.

2. **Thiết lập System Instruction chuẩn mực cho Routine Stylist**:
   Quy định Persona: "Bạn là Trợ lý Thời trang Độc quyền của Routine. Phong cách tư vấn: Tinh tế, lịch thiệp, am hiểu xu hướng thời trang hiện đại (Minimalism, Smart Casual, Thu Đông). Luôn dựa vào sản phẩm có sẵn trong catalog thực tế, tuyệt đối không bịa đặt sản phẩm không có thật".

3. **Cấu hình Model Parameters**:
   Cấu hình model: "gemini-2.5-flash" (fallback "gemini-1.5-flash"), temperature: 0.4 cho độ chính xác dữ liệu cao, maxOutputTokens: 1024.

## 7. TECHNICAL REQUIREMENTS
- @google/genai ^0.1.1 hoặc @google/generative-ai ^0.21.12
- Tự động retry với exponential backoff

## 8. INTEGRATION REQUIREMENTS
- Được sử dụng bởi aiStylistService và aiBiService

## 9. SAFETY CONSTRAINTS
- ⚠️ **Prompt Injection Defense**: Khử khuẩn đầu vào của người dùng, ngăn chặn việc phá vỡ Persona hoặc trích xuất System Prompt.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Khởi tạo Gemini client thành công, gửi tin nhắn kiểm thử nhận phản hồi hợp lệ.
[ ] **AC-2**: Khi giả lập lỗi 429, hệ thống tự động xoay vòng sang key dự phòng không làm rơi phiên của khách.
[ ] **AC-3**: Persona Routine Stylist giữ đúng giọng điệu lịch thiệp.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Chạy script test kết nối Gemini API và kiểm tra thời gian phản hồi

## 12. EXPECTED OUTPUT
- `backend/src/config/gemini.js`: Cấu hình kết nối và xoay vòng key Gemini

## 13. COMPLETION REPORT
- Khởi tạo và cấu hình client Gemini AI hoàn thành
