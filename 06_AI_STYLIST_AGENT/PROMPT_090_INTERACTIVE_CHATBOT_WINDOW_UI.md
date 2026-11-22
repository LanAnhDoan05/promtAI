# PROMPT 090 – INTERACTIVE CHATBOT WINDOW, MESSAGE STREAM & PRODUCT SUGGESTION CARDS

## 1. ROLE
Frontend Chat UI Specialist

## 2. OBJECTIVE
Xây dựng cửa sổ trò chuyện tương tác AI Stylist (Chatbot Window): Khung chat kích thước chuẩn (rộng 380px, cao 520px trên desktop; toàn màn hình trên mobile), luồng tin nhắn hiển thị theo thời gian thực (typing indicator, stream chữ gõ từng ký tự), các câu hỏi gợi ý nhanh (Quick Prompts: "Gợi ý đồ đi làm", "Tư vấn chọn size", "Set đồ Thu Đông mới nhất"), và các thẻ sản phẩm xem nhanh đính kèm trong tin nhắn.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_01_AI_AGENT_AND_DEMO_COMPLETION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_01_AI_AGENT_AND_DEMO_COMPLETION.md)
> - [USER_MASTER_PROMPT_16_AI_STYLIST_AND_SALES_STANDARDS.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_16_AI_STYLIST_AND_SALES_STANDARDS.md)
> - [USER_MASTER_PROMPT_18_VNPAY_QR_AND_AI_HUMAN_HANDOFF.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_18_VNPAY_QR_AND_AI_HUMAN_HANDOFF.md)
> - [USER_MASTER_PROMPT_19_AI_CONTEXTUAL_CONVERSATION_FIX.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_19_AI_CONTEXTUAL_CONVERSATION_FIX.md)

## 3. CONTEXT
Giao diện chat là nơi khách hàng trực tiếp trải nghiệm sự thông minh của AI. Thẻ sản phẩm hiển thị ngay trong bong bóng chat cho phép khách bấm xem nhanh, chọn size và thêm vào giỏ hàng ngay lập tức.

## 4. PREREQUISITES
- PROMPT_089: Floating Launcher
- PROMPT_085: AI Tools

## 5. INPUTS
- API POST /api/v1/ai/stylist/chat

## 6. DETAILED TASKS
1. **Xây dựng Khung Cửa Sổ Chat (Chat Window)**:
   Header: Logo Routine AI, tên "Trợ lý Routine Stylist", nút thu nhỏ, nút làm mới phiên chat. Body: cuộn tin nhắn tự động xuống đáy khi có tin mới. Footer: ô nhập text, nút gửi, icon micro (tùy chọn).

2. **Các Nút Gợi Ý Nhanh (Quick Action Pills)**:
   Dải các nút gợi ý bấm nhanh: "Phối đồ Thu Đông", "Đồ công sở thanh lịch", "Tư vấn chọn size", "Gặp chuyên viên tư vấn". Bấm vào tự động gửi câu hỏi.

3. **Render Thẻ Sản Phẩm Đính Kèm (Embedded Product Cards)**:
   Khi AI trả về recommendedProductIds: hiển thị thanh cuộn ngang các thẻ sản phẩm nhỏ (ảnh, tên, giá, nút "Xem ngay" mở PDP hoặc popup).

4. **Hiệu ứng Gõ Chữ (Typing Indicator & Streaming)**:
   Hiển thị 3 dấu chấm nhảy (bouncing dots) khi AI đang xử lý, và hiệu ứng hiển thị chữ dần dần như người thật đang trả lời.

## 7. TECHNICAL REQUIREMENTS
- Auto scroll to bottom (smooth behavior)
- Hỗ trợ Markdown cơ bản (in đậm, danh sách gạch đầu dòng)

## 8. INTEGRATION REQUIREMENTS
- CartContext để thêm sản phẩm trực tiếp từ ô chat

## 9. SAFETY CONSTRAINTS
- ⚠️ **Scroll Lock Issue**: Cuộn tin nhắn bên trong cửa sổ chat không làm cuộn trang web phía sau trên mobile.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Cửa sổ chat mở trơn tru, hiển thị lời chào mở đầu.
[ ] **AC-2**: Nhập câu hỏi nhận được phản hồi nhanh chóng có hiệu ứng gõ chữ.
[ ] **AC-3**: Các thẻ sản phẩm hiển thị ảnh rõ nét và bấm vào xem được chi tiết.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Thực hiện gửi 3 câu hỏi liên tiếp và kiểm tra cuộn tự động và thẻ sản phẩm

## 12. EXPECTED OUTPUT
- `frontend/src/components/AiStylist/AiStylistWindow.jsx`: Component cửa sổ chat chính
- `frontend/src/components/AiStylist/ChatMessage.jsx`: Component từng bong bóng tin nhắn
- `frontend/src/components/AiStylist/AiStylistWindow.module.css`: CSS Module cửa sổ chat

## 13. COMPLETION REPORT
- Cửa sổ chat tương tác AI Stylist và thẻ sản phẩm hoàn thành
