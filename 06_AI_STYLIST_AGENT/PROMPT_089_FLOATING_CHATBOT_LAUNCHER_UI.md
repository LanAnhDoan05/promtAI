# PROMPT 089 – FLOATING AI STYLIST CHATBOT LAUNCHER & TRIGGER ANIMATIONS

## 1. ROLE
Frontend UI/Animation Specialist

## 2. OBJECTIVE
Xây dựng nút bấm nổi mở Trợ lý AI Stylist (Floating Chat Launcher) ở góc dưới bên phải màn hình: Nút tròn sang trọng với logo Routine AI lấp lánh (sparkles), hiệu ứng gợn sóng (pulse animation), bong bóng lời mời chào tự động xuất hiện sau 5 giây (Welcome Bubble: "Chào bạn! Cần Routine gợi ý phối đồ hôm nay không?"), và badge thông báo chưa đọc.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_01_AI_AGENT_AND_DEMO_COMPLETION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_01_AI_AGENT_AND_DEMO_COMPLETION.md)
> - [USER_MASTER_PROMPT_16_AI_STYLIST_AND_SALES_STANDARDS.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_16_AI_STYLIST_AND_SALES_STANDARDS.md)
> - [USER_MASTER_PROMPT_18_VNPAY_QR_AND_AI_HUMAN_HANDOFF.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_18_VNPAY_QR_AND_AI_HUMAN_HANDOFF.md)
> - [USER_MASTER_PROMPT_19_AI_CONTEXTUAL_CONVERSATION_FIX.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_19_AI_CONTEXTUAL_CONVERSATION_FIX.md)

## 3. CONTEXT
Nút khởi chạy cần thu hút sự chú ý một cách tinh tế mà không che khuất các nút thao tác mua hàng quan trọng trên di động.

## 4. PREREQUISITES
- PROMPT_050: RootLayout

## 5. INPUTS
- Thiết kế nút launcher phong cách Routine (đen viền vàng gold hoặc đỏ nhấn)

## 6. DETAILED TASKS
1. **Xây dựng Component AiStylistLauncher**:
   Vị trí cố định (fixed) bottom: 24px, right: 24px, z-index: 999. Nút tròn đường kính 56px với icon lấp lánh ánh kim.

2. **Bong Bóng Chào Mời Tự Động (Welcome Bubble)**:
   Sau 5 giây truy cập website lần đầu: bong bóng thoại nhỏ hiện lên bên cạnh nút với hiệu ứng fade-in-up và âm thanh nhẹ nhàng (tùy chọn). Có nút X nhỏ để đóng.

3. **Thao Tác Click Mở/Đóng Cửa Sổ Chat**:
   Bấm vào nút: chuyển đổi giữa icon Chatbot và icon Đóng (X), kích hoạt mở cửa sổ trò chuyện chính.

## 7. TECHNICAL REQUIREMENTS
- CSS Keyframe animation mượt mà 60fps
- Responsive: trên mobile thu nhỏ nhẹ và cách mép dưới 16px tránh che thanh điều hướng

## 8. INTEGRATION REQUIREMENTS
- Nhúng vào app/layout.js để hiển thị trên toàn bộ các trang


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Screen Obstruction**: Không che nút "Thêm vào giỏ" dính ở đáy màn hình trên mobile.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Nút nổi hiển thị đẹp mắt ở góc dưới phải.
[ ] **AC-2**: Bong bóng mời chào tự động hiện sau 5 giây.
[ ] **AC-3**: Bấm nút mở/đóng cửa sổ chat mượt mà.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm tra hiển thị nút launcher trên iPhone (390px) và màn hình desktop 1440px

## 12. EXPECTED OUTPUT
- `frontend/src/components/AiStylist/AiStylistLauncher.jsx`: Component nút mở chatbot
- `frontend/src/components/AiStylist/AiStylistLauncher.module.css`: CSS Module nút mở

## 13. COMPLETION REPORT
- Nút nổi khởi chạy AI Stylist và hoạt họa mời chào hoàn thành
