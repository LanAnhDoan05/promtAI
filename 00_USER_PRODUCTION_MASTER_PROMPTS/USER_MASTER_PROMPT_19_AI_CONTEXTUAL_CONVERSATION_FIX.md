# USER MASTER PROMPT #19: 19 AI CONTEXTUAL CONVERSATION FIX
> **Nguồn gốc:** Prompt chỉ đạo thực tế từ Người dùng (User Request) tại Step 7869.
> **Độ dài gốc:** 7843 ký tự.
> **Mục đích trong thư viện:** Cung cấp toàn văn đặc tả nghiệp vụ, yêu cầu kỹ thuật và ràng buộc sản xuất thực tế mà người dùng đã trực tiếp chỉ đạo và kiểm chứng trong dự án Routine Web.

---

# BỔ SUNG PROMPT: SỬA LỖI AI CHATBOT KHÔNG DUY TRÌ NGỮ CẢNH HỘI THOẠI – CONTEXTUAL CONVERSATION

## 1. MỤC TIÊU

Nâng cấp AI Chatbot Routine thành trợ lý tư vấn có khả năng ghi nhớ, duy trì và cập nhật ngữ cảnh xuyên suốt cuộc trò chuyện.

AI không được xem mỗi tin nhắn của khách là một yêu cầu độc lập.

Khi khách đặt câu hỏi tiếp theo, AI phải xác định câu hỏi đó đang:
- Bổ sung điều kiện cho yêu cầu trước.
- Thu hẹp danh sách sản phẩm.
- Thay đổi một tiêu chí tìm kiếm.
- Hỏi thêm thông tin về sản phẩm vừa được đề cập.
- Chuyển sang một nhu cầu hoàn toàn mới.
- Yêu cầu thực hiện hành động khác.

Phải tận dụng Gemini AI, hệ thống hội thoại và các công cụ truy vấn sản phẩm hiện tại. Không thay thế toàn bộ AI Agent.

## 2. XÂY DỰNG CƠ CHẾ DUY TRÌ NGỮ CẢNH

Mỗi cuộc trò chuyện phải duy trì một đối tượng ngữ cảnh tìm kiếm sản phẩm (Conversation Context).

Ví dụ cấu trúc:

- product_type: loại sản phẩm.
- budget_min: ngân sách tối thiểu.
- budget_max: ngân sách tối đa.
- color: màu sắc.
- size: kích cỡ.
- gender: đối tượng sử dụng nếu có.
- material: chất liệu.
- style: phong cách.
- occasion: dịp sử dụng.
- stock_status: tình trạng còn hàng.
- excluded_products: sản phẩm đã loại trừ.
- current_product_ids: danh sách sản phẩm đang được thảo luận.
- active_search_filters: các điều kiện tìm kiếm đang áp dụng.
- conversation_intent: mục đích hiện tại của khách.

Đây là các trường ngữ cảnh có thể mở rộng theo nhu cầu thực tế.

Không được tự điền các điều kiện mà khách chưa đề cập.

## 3. QUY TẮC HIỂU CÂU HỎI NỐI TIẾP

### Tình huống 1: Bổ sung điều kiện

Khách: "Tìm áo len dưới 1 triệu."

AI: Liệt kê các mẫu áo len dưới 1 triệu.

Khách: "Có màu trắng không?"

AI phải hiểu thành:

Tìm áo len + giá dưới 1 triệu + màu trắng.

Không được xóa điều kiện loại sản phẩm và ngân sách.

### Tình huống 2: Bổ sung nhiều điều kiện liên tiếp

Khách: "Tìm áo len dưới 1 triệu."

Khách tiếp: "Màu trắng nhé."

Khách tiếp: "Có size M không?"

Khách tiếp: "Chất liệu cotton thì sao?"

AI phải hiểu yêu cầu cuối cùng là:

Áo len + dưới 1 triệu + màu trắng + size M + chất liệu cotton.

Các điều kiện trước vẫn được giữ lại cho đến khi khách thay đổi hoặc xóa chúng.

### Tình huống 3: Thay đổi một điều kiện

Khách: "Tìm áo len dưới 1 triệu màu trắng."

Khách tiếp: "Thế màu đen thì sao?"

AI phải thay màu trắng bằng màu đen, nhưng giữ nguyên:
- Loại sản phẩm: áo len.
- Ngân sách: dưới 1 triệu.

Không được giữ đồng thời màu trắng và màu đen nếu khách đang yêu cầu thay thế màu.

### Tình huống 4: Nới rộng ngân sách

Khách: "Tìm áo len dưới 1 triệu màu trắng."

Khách tiếp: "Nếu tăng lên 1 triệu rưỡi thì sao?"

AI cập nhật ngân sách tối đa thành 1.500.000 đồng, giữ nguyên loại sản phẩm và màu trắng.

### Tình huống 5: Hỏi về sản phẩm vừa được đề cập

Khách: "Tìm áo len dưới 1 triệu."

AI: Liệt kê 5 sản phẩm phù hợp.

Khách: "Mẫu thứ hai chất liệu gì?"

AI phải xác định đúng sản phẩm thứ hai trong danh sách gần nhất và truy vấn thông tin chi tiết sản phẩm đó.

Không được hiểu thành tìm sản phẩm mới.

### Tình huống 6: Hỏi thêm về tồn kho

Khách: "Mẫu áo trắng đó còn size M không?"

AI phải truy vấn tồn kho của đúng sản phẩm và đúng biến thể size M, màu trắng.

Không được suy đoán tồn kho từ tổng số lượng sản phẩm.

### Tình huống 7: Khách chuyển sang nhu cầu mới

Khách: "Tìm áo len dưới 1 triệu."

Khách tiếp: "Bây giờ tìm quần jeans nhé."

AI phải xác định đây là yêu cầu tìm kiếm mới.

Cập nhật loại sản phẩm thành quần jeans. Không tiếp tục áp dụng điều kiện áo len.

Các điều kiện ngân sách, màu sắc hoặc kích cỡ chỉ được giữ lại nếu ngữ cảnh và cách diễn đạt cho thấy khách muốn tiếp tục sử dụng chúng.

Nếu không đủ căn cứ, AI cần hỏi lại một câu ngắn để xác nhận.

## 4. QUY TẮC XỬ LÝ NGỮ CẢNH

Trước khi gọi công cụ tìm kiếm sản phẩm, AI phải thực hiện:

1. Đọc lịch sử hội thoại liên quan.
2. Xác định yêu cầu hiện tại.
3. Xác định các điều kiện đang có.
4. Phân biệt điều kiện mới, điều kiện thay thế và điều kiện bị xóa.
5. Cập nhật Conversation Context.
6. Chuyển truy vấn đã hoàn thiện cho Backend.
7. Backend truy vấn MySQL theo toàn bộ điều kiện.
8. Gemini trình bày kết quả.

Không được chỉ gửi nội dung tin nhắn mới nhất vào công cụ tìm kiếm mà bỏ qua các điều kiện trước đó.

## 5. QUY TẮC TÌM KIẾM VÀ HIỂN THỊ SẢN PHẨM

Khi khách hỏi một tiêu chí bổ sung, AI phải lọc lại danh sách sản phẩm theo toàn bộ điều kiện còn hiệu lực.

Ví dụ:

| Lần hỏi | Điều kiện cần áp dụng |
|---|---|
| Tìm áo len dưới 1 triệu | Áo len, giá dưới 1 triệu |
| Màu trắng | Áo len, dưới 1 triệu, trắng |
| Size M | Áo len, dưới 1 triệu, trắng, size M |
| Chất liệu cotton | Áo len, dưới 1 triệu, trắng, size M, cotton |

Kết quả phải lấy từ dữ liệu MySQL thông qua Backend.

Không:
- Tự bịa sản phẩm.
- Tự bịa màu sắc.
- Tự bịa size.
- Tự bịa giá.
- Tự bịa tồn kho.
- Hiển thị sản phẩm không thỏa mãn điều kiện.
- Tự bỏ điều kiện cũ mà khách chưa thay đổi.

Nếu không có kết quả, phải nói rõ không tìm thấy sản phẩm phù hợp với toàn bộ điều kiện hiện tại.

Có thể đề xuất khách nới lỏng một điều kiện, nhưng không tự ý thay đổi bộ lọc.

## 6. HIỂN THỊ ĐIỀU KIỆN ĐANG TÌM KIẾM

Khi phù hợp, hiển thị ngắn gọn các điều kiện hiện tại để khách dễ theo dõi.

Ví dụ:

Đang tìm kiếm:
- Loại sản phẩm: Áo len.
- Ngân sách: Dưới 1.000.000đ.
- Màu sắc: Trắng.
- Kích cỡ: M.

Nếu khách thay đổi màu sắc, phần điều kiện phải cập nhật tương ứng.

Có thể cung cấp chức năng xóa từng điều kiện nếu giao diện hiện tại hỗ trợ.

## 7. DUY TRÌ NGỮ CẢNH VÀ BỘ ĐẾM 5 LƯỢT

Conversation Context và bộ đếm 5 lượt tư vấn phải hoạt động độc lập nhưng cùng thuộc một cuộc trò chuyện.

- Mỗi khách có ngữ cảnh riêng.
- Không dùng chung ngữ cảnh giữa hai khách.
- Tải lại trang không làm mất ngữ cảnh.
- Các tin nhắn trùng không được xử lý hai lần.
- Khi chuyển cho chuyên viên, phải bàn giao cả ngữ cảnh tìm kiếm hiện tại.
- Chuyên viên phải biết khách đang tìm loại sản phẩm nào, ngân sách bao nhiêu, màu sắc, size và những sản phẩm đã xem.

Việc khách hỏi nối tiếp không được làm sai bộ đếm 5 lượt tư vấn.

## 8. KIỂM THỬ BẮT BUỘC

Thực hiện trực tiếp bằng hội thoại trên trình duyệt:

1. Áo len dưới 1 triệu → màu trắng.
2. Áo len dưới 1 triệu → màu trắng → size M.
3. Áo len dưới 1 triệu → màu trắng → đổi sang màu đen.
4. Áo len dưới 1 triệu → tăng ngân sách lên 1,5 triệu.
5. Áo len dưới 1 triệu → hỏi chất liệu mẫu thứ hai.
6. Áo len dưới 1 triệu → hỏi mẫu thứ hai còn size M không.
7. Áo len dưới 1 triệu → chuyển sang tìm quần jeans.
8. Áo len dưới 1 triệu → màu trắng → tải lại trang → hỏi size M.
9. Hai khách tìm kiếm song song với các điều kiện khác nhau.
10. Khách chuyển sang chuyên viên → chuyên viên nhìn thấy đầy đủ điều kiện tìm kiếm.
11. Khách hỏi một câu hoàn toàn mới → AI không áp dụng nhầm ngữ cảnh cũ.
12. Khách hỏi một câu mơ hồ → AI hỏi lại thay vì tự suy diễn.

Mỗi kịch bản phải kiểm tra:
- Cách AI hiểu câu hỏi.
- Conversation Context trước và sau khi cập nhật.
- Tham số Backend nhận được.
- Kết quả truy vấn MySQL.
- Sản phẩm AI hiển thị.
- Độ chính xác của câu trả lời.

## 9. ĐIỀU KIỆN HOÀN THÀNH

AI phải có khả năng tư vấn liên tục như một nhân viên bán hàng thực tế.

Khách không cần lặp lại toàn bộ yêu cầu ở mỗi tin nhắn.

Khi khách nói "màu trắng", AI hiểu đó là màu trắng của loại sản phẩm và bộ lọc đang được trao đổi.

Khi khách nói "đổi sang màu đen", AI chỉ thay đổi điều kiện màu sắc.

Khi khách nói "mẫu thứ hai", AI xác định đúng sản phẩm trong danh sách gần nhất.

Khi khách đổi nhu cầu, AI phải nhận biết và bắt đầu luồng tìm kiếm mới.

Tuyệt đối không để ngữ cảnh cũ làm sai kết quả của yêu cầu mới.
