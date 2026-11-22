# PROMPT 086 – SMART OUTFIT RECOMMENDER (TOP + BOTTOM + ACCESSORY COORDINATION)

## 1. ROLE
AI Fashion Stylist Specialist

## 2. OBJECTIVE
Xây dựng thuật toán gợi ý phối đồ thông minh: Tự động ghép nối các món đồ thành combo hoàn chỉnh (Áo + Quần + Áo khoác/Phụ kiện) hài hòa về màu sắc (Color Harmony - phối tương phản hoặc tone sur tone) và phong cách, hiển thị thẻ combo kèm tổng giá và nút thêm tất cả vào giỏ hàng.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_01_AI_AGENT_AND_DEMO_COMPLETION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_01_AI_AGENT_AND_DEMO_COMPLETION.md)
> - [USER_MASTER_PROMPT_16_AI_STYLIST_AND_SALES_STANDARDS.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_16_AI_STYLIST_AND_SALES_STANDARDS.md)
> - [USER_MASTER_PROMPT_18_VNPAY_QR_AND_AI_HUMAN_HANDOFF.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_18_VNPAY_QR_AND_AI_HUMAN_HANDOFF.md)
> - [USER_MASTER_PROMPT_19_AI_CONTEXTUAL_CONVERSATION_FIX.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_19_AI_CONTEXTUAL_CONVERSATION_FIX.md)

## 3. CONTEXT
Khi khách hỏi: "Tư vấn cho mình set đồ đi phỏng vấn xin việc", AI không chỉ đưa ra 1 cái áo đơn lẻ mà sẽ phối: Áo sơ mi trắng regular fit + Quần tây đen slimfit + Thắt lưng da, tạo nên diện mạo chuyên nghiệp.

## 4. PREREQUISITES
- PROMPT_084: Grounding Service
- PROMPT_045: Outfit Service

## 5. INPUTS
- Occasion, Gender, Phong cách mong muốn của khách hàng

## 6. DETAILED TASKS
1. **Xây dựng Quy tắc Phối Màu Thời Trang (Color Matching Matrix)**:
   Bảng quy tắc phối màu chuẩn thời trang Routine: Đen đi với mọi màu; Trắng đi với Đen/Navy/Xám; Be/Kem đi với Nâu/Trắng/Xanh rêu. Tránh phối các màu xung đột.

2. **Thuật toán Phối Combo 3 Món (Top - Bottom - Accessory)**:
   Lấy 1 sản phẩm Top (Áo), tìm 1 sản phẩm Bottom (Quần) tương thích theo bảng quy tắc, và 1 phụ kiện hoặc Outerwear nếu thời tiết lạnh.

3. **Sinh Thẻ Gợi Ý Combo trong Phản Hồi AI**:
   Đính kèm mảng recommendedProductIds trong phản hồi để giao diện chat render các thẻ sản phẩm bấm mua được ngay.

## 7. TECHNICAL REQUIREMENTS
- Đảm bảo tất cả các món trong combo đều cùng size phù hợp với khách
- Tính tổng giá combo và hiển thị mức tiết kiệm nếu có

## 8. INTEGRATION REQUIREMENTS
- Kết nối giữa AI Chat UI và CartContext


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Style Clashing**: Không phối đồ thể thao với quần âu công sở sang trọng.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Gợi ý set đồ công sở gồm đủ Áo và Quần phù hợp.
[ ] **AC-2**: Phản hồi của AI kèm theo danh sách sản phẩm có thể click xem chi tiết.
[ ] **AC-3**: Màu sắc các món đồ trong combo phối hợp hài hòa.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm thử yêu cầu gợi ý phối đồ Thu Đông và kiểm tra tính hợp lý của combo

## 12. EXPECTED OUTPUT
- `backend/src/services/aiOutfitRecommender.js`: Động cơ phối đồ thời trang thông minh

## 13. COMPLETION REPORT
- Động cơ gợi ý phối đồ Smart Outfit cho AI Stylist hoàn thành
