# USER MASTER PROMPT #18: 18 VNPAY QR AND AI HUMAN HANDOFF
> **Nguồn gốc:** Prompt chỉ đạo thực tế từ Người dùng (User Request) tại Step 7401.
> **Độ dài gốc:** 16147 ký tự.
> **Mục đích trong thư viện:** Cung cấp toàn văn đặc tả nghiệp vụ, yêu cầu kỹ thuật và ràng buộc sản xuất thực tế mà người dùng đã trực tiếp chỉ đạo và kiểm chứng trong dự án Routine Web.

---

# PROMPT: SỬA LỖI QR THANH TOÁN VÀ HOÀN THIỆN AI CHATBOT CHUYỂN TIẾP CHUYÊN VIÊN – ROUTINE WEB

## I. MỤC TIÊU

Thực hiện trực tiếp trên dự án Routine Web hiện tại, tập trung vào hai hạng mục:

1. Khắc phục triệt để lỗi mã QR thanh toán không hiển thị trên giao diện khách hàng.
2. Nâng cấp AI Chatbot thành trợ lý tư vấn có quy trình chuyển tiếp sang chuyên viên sau 5 lượt trao đổi tư vấn.

Không xây dựng lại hệ thống từ đầu. Phải tận dụng Gemini AI, Backend, Database, hệ thống đơn hàng, thanh toán và giao diện Admin hiện có.

---

# II. HẠNG MỤC 1: SỬA LỖI QR THANH TOÁN KHÔNG HIỂN THỊ

## 1. Kiểm tra nguyên nhân

Kiểm tra toàn bộ luồng thanh toán hiện tại:

Frontend Checkout → Backend tạo yêu cầu thanh toán → Cổng thanh toán → Dữ liệu QR → Frontend hiển thị QR.

Kiểm tra các vấn đề:

- Backend có tạo đúng dữ liệu thanh toán không?
- API có trả về URL QR hoặc dữ liệu QR không?
- Frontend có nhận đúng dữ liệu từ API không?
- Thành phần hiển thị QR có hoạt động không?
- URL ảnh QR có truy cập được không?
- Dữ liệu QR có bị null, undefined hoặc sai định dạng không?
- Có lỗi CORS, CSP, mạng hoặc lỗi tải ảnh không?
- Có lỗi khi chuyển từ trang checkout sang trang thanh toán không?
- Có lỗi khi làm mới trang hoặc quay lại trang thanh toán không?
- Có lỗi do trạng thái đơn hàng hoặc trạng thái thanh toán không?

Không được chỉ thêm một ảnh QR tĩnh để che lỗi.

## 2. Xác định loại QR đang sử dụng

Kiểm tra chính xác hệ thống hiện tại đang sử dụng:

- QR do cổng thanh toán trả về.
- QR được tạo từ dữ liệu thanh toán.
- QR chuyển khoản ngân hàng.
- QR thuộc VNPay Sandbox hoặc phương thức khác.

Không tự ý thay đổi phương thức thanh toán hiện tại.

Nếu hệ thống đang dùng VNPay Sandbox, phải phân biệt rõ:
- URL thanh toán.
- Mã QR thanh toán nếu được nhà cung cấp hỗ trợ.
- Thông tin giao dịch.
- Callback xác nhận thanh toán.

Không được tự tạo QR giả rồi coi đó là giao dịch đã thanh toán.

Nếu phương thức hiện tại không cung cấp dữ liệu QR, phải báo cáo rõ và đề xuất cách tích hợp phù hợp, không tự nhận QR đã hoạt động.

## 3. Sửa lỗi hiển thị QR

Yêu cầu:

- QR phải hiển thị rõ ràng trên trang thanh toán.
- Không bị vỡ ảnh hoặc biến dạng.
- Không bị mất khi tải lại trang nếu giao dịch vẫn còn hiệu lực.
- Có trạng thái đang tạo mã QR.
- Có thông báo lỗi nếu không thể tạo hoặc tải QR.
- Có nút thử lại khi phù hợp.
- Có thông tin đơn hàng và số tiền thanh toán.
- Có hướng dẫn khách quét mã.
- Có trạng thái chờ thanh toán.
- Có trạng thái thanh toán thành công hoặc thất bại.

Nếu sử dụng dữ liệu QR dạng chuỗi, kiểm tra việc tạo ảnh QR ở Frontend hoặc Backend theo đúng định dạng và nguồn dữ liệu.

Nếu sử dụng URL QR, phải kiểm tra URL thực tế và phản hồi HTTP.

## 4. Kiểm tra tính chính xác thanh toán

Đối chiếu:

- Mã đơn hàng.
- Mã giao dịch.
- Số tiền.
- Nội dung thanh toán.
- Trạng thái thanh toán.
- Dữ liệu QR hoặc URL thanh toán.
- Dữ liệu trong Database.

Số tiền thanh toán phải khớp với hóa đơn:

Tổng thanh toán = Tiền hàng - Giảm giá + Phí vận chuyển.

Không được xác nhận thanh toán chỉ vì:
- QR đã hiển thị.
- Khách đã mở trang thanh toán.
- Khách thông báo đã chuyển tiền.
- API tạo URL thanh toán trả về HTTP 200.

Chỉ cập nhật thanh toán thành công khi Backend xác minh được callback hoặc trạng thái giao dịch hợp lệ theo cơ chế của nhà cung cấp.

Nếu sử dụng VNPay Sandbox, kiểm tra chữ ký callback, số tiền, mã đơn hàng và trạng thái giao dịch.

## 5. Kiểm thử bắt buộc

- Tạo đơn hàng và mở trang thanh toán.
- Kiểm tra QR xuất hiện.
- Quét QR bằng phương thức tương thích với môi trường Sandbox nếu có.
- Kiểm tra số tiền.
- Làm mới trang thanh toán.
- Kiểm tra giao dịch hết hạn.
- Kiểm tra thanh toán thất bại.
- Kiểm tra thanh toán thành công.
- Kiểm tra callback.
- Kiểm tra Admin nhìn thấy đúng trạng thái đơn hàng.
- Kiểm tra khách nhìn thấy đúng trạng thái thanh toán.

---

# III. HẠNG MỤC 2: CHUẨN HÓA AI CHATBOT THEO QUY TRÌNH 5 LƯỢT TƯ VẤN

## 1. Mục tiêu

AI Chatbot mặc định đảm nhận vai trò trợ lý tư vấn bán hàng trực tuyến.

AI phải:
- Hiểu nhu cầu khách hàng.
- Tìm kiếm sản phẩm.
- Liệt kê đầy đủ sản phẩm phù hợp.
- Tư vấn giá, chất liệu, màu sắc, kích cỡ và tồn kho.
- Hỗ trợ lựa chọn sản phẩm.
- Phối đồ khi khách yêu cầu.
- Hỗ trợ nhu cầu mua hàng.
- Chủ động đề nghị kết nối chuyên viên tư vấn sau 5 lượt trao đổi tư vấn.

Không được biến AI thành chatbot chỉ biết phối đồ.

## 2. Quy định đếm 5 lượt trao đổi

Định nghĩa rõ:

**Một lượt tư vấn của khách hàng = một tin nhắn hợp lệ do khách gửi trong cuộc trò chuyện với mục đích hỏi thông tin, tìm kiếm, lựa chọn hoặc yêu cầu AI hỗ trợ tư vấn mua sắm.**

Cách tính:

- Tin nhắn đầu tiên của khách: lượt 1.
- Tin nhắn thứ hai: lượt 2.
- Tin nhắn thứ ba: lượt 3.
- Tin nhắn thứ tư: lượt 4.
- Tin nhắn thứ năm: lượt 5.

Sau khi khách gửi tin nhắn tư vấn thứ 5 và AI đã phản hồi nội dung đó, hệ thống phải chủ động hỏi khách:

"Bạn đã được hỗ trợ tìm hiểu sản phẩm và lựa chọn trang phục. Bạn có muốn mình kết nối với chuyên viên tư vấn Routine để được hỗ trợ trực tiếp và chi tiết hơn không?"

Hiển thị hai lựa chọn:

- Có, kết nối chuyên viên tư vấn.
- Không, tôi muốn tiếp tục trao đổi với AI.

**Lưu ý quan trọng về cách đếm:**

- Chỉ đếm tin nhắn tư vấn hợp lệ của khách.
- Không đếm tin nhắn do AI gửi.
- Không đếm tin nhắn của chuyên viên.
- Không đếm tin nhắn hệ thống.
- Không đếm các tin nhắn trống hoặc gửi lỗi.
- Không đếm thao tác bấm nút xem sản phẩm nếu không tạo tin nhắn.
- Không đếm tin nhắn kỹ thuật hoặc sự kiện hệ thống.
- Không tăng bộ đếm khi khách gửi lại cùng một tin do lỗi mạng hoặc gửi trùng request.

Không được hiểu 5 lượt là 5 tin nhắn tổng cộng của cả AI và khách.

## 3. Xử lý các nhóm yêu cầu

AI phải phân loại ý định:

### A. Tìm kiếm sản phẩm

Ví dụ:
- Tôi muốn tìm áo dưới 1 triệu.
- Có những mẫu quần jeans nào?
- Tìm áo sơ mi trắng.
- Có sản phẩm nào đang giảm giá không?

AI phải truy vấn MySQL thông qua Backend và liệt kê tất cả sản phẩm phù hợp.

Không tự phối đồ nếu khách chưa yêu cầu.

### B. Tư vấn sản phẩm

Ví dụ:
- Áo này chất liệu gì?
- Mẫu này có size M không?
- Tôi cao 1m70 nặng 65kg nên chọn size gì?
- Hai sản phẩm này khác nhau thế nào?

AI phải trả lời dựa trên dữ liệu có thật.

### C. Phối đồ

Chỉ gọi công cụ phối đồ khi khách yêu cầu rõ ràng.

Không tự động kích hoạt `recommend_outfit` khi khách chỉ muốn tìm kiếm sản phẩm.

### D. Hỗ trợ mua hàng

Ví dụ:
- Tôi muốn mua sản phẩm này.
- Tôi cần tư vấn kỹ hơn.
- Tôi muốn gặp nhân viên.
- Tôi cần hỗ trợ đặt hàng.

AI có thể đề nghị kết nối chuyên viên ngay khi khách thể hiện nhu cầu rõ ràng, không bắt buộc phải chờ đủ 5 lượt.

**Quy tắc ưu tiên:** Ngưỡng 5 lượt là thời điểm đề nghị kết nối mặc định, không phải rào cản ngăn khách gặp nhân viên sớm hơn.

## 4. Quy tắc sau khi khách trả lời câu hỏi chuyển tiếp

### Trường hợp 1: Khách đồng ý

Ví dụ: "Có", "Kết nối giúp tôi", "Tôi muốn gặp nhân viên".

Hệ thống phải:

1. Gửi yêu cầu chuyển tiếp tới Backend.
2. Tạo bản ghi yêu cầu tư vấn trong Database.
3. Gắn mã khách hàng hoặc phiên khách.
4. Gắn mã cuộc trò chuyện.
5. Lưu lịch sử trao đổi.
6. Lưu nhu cầu khách hàng.
7. Lưu số lượt tư vấn.
8. Lưu thời gian yêu cầu.
9. Đưa yêu cầu vào danh sách chờ của Admin.
10. Gửi thông báo trên trang quản trị.

AI phản hồi:

"Mình đã ghi nhận yêu cầu kết nối chuyên viên tư vấn. Bạn vui lòng chờ chuyên viên Routine tiếp nhận nhé!"

Chỉ hiển thị thông báo này khi Backend xác nhận tạo yêu cầu thành công.

### Trường hợp 2: Khách từ chối

Ví dụ: "Không", "Tôi muốn tiếp tục hỏi AI".

Hệ thống phải:

- Không tạo yêu cầu chuyển tiếp.
- Tiếp tục tư vấn bình thường.
- Không hỏi lặp lại ngay sau mỗi tin nhắn.
- Chỉ đề nghị lại khi có nhu cầu mới rõ ràng hoặc sau một khoảng trao đổi hợp lý.

Không được ép khách chuyển sang nhân viên.

### Trường hợp 3: Khách chưa trả lời rõ ràng

AI có thể hỏi lại một lần:

"Bạn muốn tiếp tục được AI hỗ trợ hay kết nối với chuyên viên tư vấn?"

Không tự động chuyển khi khách chưa đồng ý.

### Trường hợp 4: Khách yêu cầu chuyên viên trước lượt thứ 5

Phải ưu tiên yêu cầu của khách và tạo luồng chuyển tiếp ngay sau khi khách xác nhận.

Không bắt khách phải trao đổi đủ 5 lượt.

## 5. Trạng thái hội thoại

Xây dựng hoặc tận dụng các trạng thái hiện có:

- `AI_ACTIVE`: AI đang tư vấn.
- `HANDOFF_OFFERED`: AI đã đề nghị kết nối.
- `WAITING_CONFIRMATION`: Chờ khách xác nhận.
- `PENDING`: Đã tạo yêu cầu, chờ chuyên viên tiếp nhận.
- `ASSIGNED`: Đã có nhân viên phụ trách.
- `HUMAN_ACTIVE`: Chuyên viên đang tư vấn.
- `RESOLVED`: Đã xử lý xong.
- `CLOSED`: Cuộc trò chuyện đã đóng.

Không được tự chuyển trạng thái khi chưa có sự kiện tương ứng.

Khi chuyên viên tiếp nhận, phải chuyển luồng hội thoại sang chế độ chuyên viên quản lý.

AI không được tiếp tục trả lời chen vào trong khi chuyên viên đang trực tiếp xử lý, trừ khi hệ thống có cơ chế phối hợp rõ ràng.

## 6. Chuyển tiếp hội thoại giữa AI và chuyên viên

Khi khách đồng ý kết nối, cần bàn giao:

- Tên khách hàng nếu có.
- Mã khách hàng hoặc mã phiên.
- Thông tin liên hệ khách đã cung cấp.
- Nội dung hội thoại.
- Các sản phẩm đã tìm kiếm.
- Sản phẩm khách quan tâm.
- Ngân sách.
- Kích cỡ, màu sắc và tiêu chí lựa chọn.
- Nhu cầu mua hàng.
- Lý do chuyển tiếp.
- Số lượt trao đổi.
- Thời điểm chuyển tiếp.

Chuyên viên phải nhìn thấy đầy đủ lịch sử hội thoại để không phải hỏi khách lại từ đầu.

Tin nhắn cần phân biệt:
- Khách hàng.
- AI.
- Chuyên viên tư vấn.
- Hệ thống.

Sau khi chuyên viên tiếp nhận, hai bên phải trao đổi được trên cùng cuộc trò chuyện.

---

# IV. HẠNG MỤC 3: THÔNG BÁO TRÊN TRANG QUẢN TRỊ

## 1. Thông báo khi khách đồng ý kết nối

Khi Backend tạo yêu cầu tư vấn thành công, Admin phải nhận được thông báo.

Nội dung thông báo gồm:

- Có yêu cầu tư vấn mới.
- Tên hoặc mã khách hàng.
- Thời gian gửi yêu cầu.
- Lý do cần hỗ trợ.
- Sản phẩm khách đang quan tâm.
- Số lượt trao đổi với AI.
- Trạng thái chờ tiếp nhận.

Ví dụ:

"Khách hàng mới yêu cầu kết nối chuyên viên tư vấn. Khách đã trao đổi 5 lượt với AI và đang quan tâm đến sản phẩm áo sơ mi."

## 2. Giao diện quản trị

Tích hợp vào khu vực quản lý tư vấn hoặc hệ thống thông báo hiện có.

Cần có:

- Số lượng yêu cầu tư vấn chưa tiếp nhận.
- Danh sách yêu cầu mới.
- Thông tin khách hàng.
- Lịch sử hội thoại.
- Sản phẩm khách quan tâm.
- Nhu cầu khách hàng.
- Nút tiếp nhận tư vấn.
- Trạng thái xử lý.
- Nhân viên phụ trách.
- Thời gian tiếp nhận.
- Chức năng trả lời khách.

Có thể bổ sung bộ lọc:
- Chờ tiếp nhận.
- Đã phân công.
- Đang tư vấn.
- Đã giải quyết.

## 3. Thông báo thời gian thực

Tận dụng cơ chế Socket.IO, SSE hoặc hệ thống cập nhật thời gian thực hiện có.

Khi khách xác nhận kết nối:

- Admin đang mở trang phải nhận được thông báo.
- Số lượng yêu cầu chờ tăng chính xác.
- Danh sách tư vấn cập nhật.
- Không cần đăng xuất hoặc tải lại toàn bộ trang.

Nếu chưa có kết nối thời gian thực, sử dụng cơ chế polling phù hợp và báo cáo rõ.

Không tạo thông báo giả lập chỉ bằng dữ liệu Frontend.

---

# V. HẠNG MỤC 4: LƯU TRỮ VÀ ĐỒNG BỘ DỮ LIỆU

Mỗi cuộc trò chuyện phải có mã định danh riêng.

Bộ đếm 5 lượt phải được lưu ở Backend hoặc Database, không chỉ lưu trong React state hoặc localStorage.

Yêu cầu:

- Bộ đếm được duy trì khi khách tải lại trang.
- Không mất số lượt khi chuyển thiết bị nếu khách đã đăng nhập.
- Phiên khách vãng lai phải có định danh phiên ổn định.
- Không cộng trùng tin nhắn.
- Không trộn dữ liệu giữa khách hàng.
- Khi tạo yêu cầu tư vấn, lưu snapshot lịch sử tại thời điểm bàn giao.
- Khi chuyên viên tiếp tục trả lời, lịch sử được nối tiếp.

Nếu khách đã chuyển sang chuyên viên, không tiếp tục đếm lượt tư vấn AI trong cùng giai đoạn nhân viên đang xử lý.

Nếu cuộc trò chuyện được mở lại với AI sau khi kết thúc tư vấn, phải áp dụng quy tắc reset hoặc bắt đầu chu kỳ tư vấn mới theo trạng thái hội thoại, không tự xóa lịch sử cũ.

---

# VI. HẠNG MỤC 5: KIỂM THỬ BẮT BUỘC

## A. QR thanh toán

1. Tạo đơn hàng mới.
2. Mở trang thanh toán.
3. Kiểm tra QR hiển thị.
4. Kiểm tra nội dung QR hoặc URL QR.
5. Kiểm tra số tiền.
6. Tải lại trang.
7. Kiểm tra QR khi giao dịch còn hiệu lực.
8. Kiểm tra QR hết hạn.
9. Kiểm tra thanh toán thất bại.
10. Kiểm tra callback thành công.
11. Đối chiếu trạng thái đơn hàng ở Admin.
12. Đối chiếu trạng thái thanh toán ở Database.

## B. AI Chatbot – Bộ đếm 5 lượt

1. Khách gửi câu hỏi thứ nhất → bộ đếm 1.
2. Khách gửi câu hỏi thứ hai → bộ đếm 2.
3. Khách gửi câu hỏi thứ ba → bộ đếm 3.
4. Khách gửi câu hỏi thứ tư → bộ đếm 4.
5. Khách gửi câu hỏi thứ năm → AI hỏi khách có muốn kết nối chuyên viên không.
6. Tin nhắn của AI không làm tăng bộ đếm.
7. Tin nhắn của chuyên viên không làm tăng bộ đếm.
8. Tin nhắn hệ thống không làm tăng bộ đếm.
9. Khách từ chối → tiếp tục tư vấn, không hỏi lặp liên tục.
10. Khách đồng ý → tạo yêu cầu thật.
11. Khách yêu cầu nhân viên ở lượt thứ nhất → vẫn được kết nối.
12. Khách tải lại trang → bộ đếm không bị mất.
13. Hai khách khác nhau → bộ đếm độc lập.
14. Tin nhắn gửi trùng do mạng → không tăng hai lần.

## C. Admin nhận thông báo

15. Khách đồng ý chuyển chuyên viên.
16. Admin nhận thông báo.
17. Bộ đếm yêu cầu chờ tăng đúng một đơn vị.
18. Admin mở yêu cầu và xem lịch sử.
19. Admin tiếp nhận.
20. Khách nhìn thấy trạng thái đã tiếp nhận.
21. Nhân viên gửi tin nhắn.
22. Khách nhận được tin nhắn.
23. Khách phản hồi.
24. Nhân viên nhìn thấy phản hồi.
25. Admin đóng yêu cầu.
26. Trạng thái hai bên được đồng bộ.

## D. Kiểm tra hồi quy

27. Tìm kiếm sản phẩm vẫn hoạt động.
28. Danh sách sản phẩm vẫn hiển thị đủ.
29. AI không tự phối đồ khi khách chưa yêu cầu.
30. Công cụ Gemini hiện có vẫn hoạt động.
31. Admin vẫn quản lý được sản phẩm và đơn hàng.
32. Các chức năng cũ không bị ảnh hưởng.

---

# VII. QUY ĐỊNH TRIỂN KHAI AN TOÀN

- Giữ nguyên Gemini AI hiện tại.
- Không thay đổi Cloudinary hoặc `.env`.
- Không sửa API Key hoặc Secret.
- Không ghi dữ liệu thử nghiệm vào MySQL `defaultdb`.
- Sử dụng `routine_test_db` cho các kiểm thử ghi dữ liệu.
- Không xóa dữ liệu thật.
- Không chạy `DROP DATABASE`, `TRUNCATE` hoặc `prisma migrate reset`.
- Không tạo thanh toán thật.
- Sử dụng môi trường Sandbox cho thanh toán.
- Không giả lập giao dịch thành công.
- Kiểm tra `git status` trước khi sửa.
- Bảo toàn các thay đổi chưa commit.
- Chỉ sửa các thành phần có lỗi hoặc thiếu chức năng.
- Không refactor toàn bộ dự án khi không cần thiết.

Nếu cần thay đổi Database, phải kiểm tra Schema hiện tại, tạo migration an toàn và xác minh khả năng rollback. Không được phá hủy dữ liệu hiện có.

---

# VIII. BÁO CÁO NGHIỆM THU

Tạo các file:

1. `docs/PAYMENT_QR_FIX_REPORT.md`
2. `docs/AI_CHATBOT_FIVE_TURN_WORKFLOW.md`
3. `docs/AI_HUMAN_HANDOFF_REPORT.md`
4. `docs/ADMIN_CONSULTATION_NOTIFICATION_REPORT.md`
5. `docs/FINAL_QR_AND_AI_ACCEPTANCE_REPORT.md`

Báo cáo phải có:

- Nguyên nhân lỗi QR.
- Cách khắc phục.
- Phương thức QR thực tế đang sử dụng.
- Bằng chứng QR hiển thị trên trình duyệt.
- Kết quả kiểm tra giao dịch Sandbox.
- Cách đếm 5 lượt.
- Cách xử lý khách đồng ý hoặc từ chối.
- Bằng chứng yêu cầu tư vấn được lưu vào Database.
- Bằng chứng Admin nhận thông báo.
- Bằng chứng chuyên viên trả lời khách.
- Kết quả từng kịch bản PASS / FAIL / BLOCKED.
- Những lỗi còn tồn tại.

Không được báo cáo PASS chỉ vì API trả về HTTP 200.

**KẾT QUẢ CUỐI CÙNG MONG MUỐN:**

1. QR thanh toán hiển thị đúng, hoạt động đúng với phương thức thanh toán hiện có và không làm sai trạng thái giao dịch.
2. AI Chatbot tư vấn khách hàng theo đúng ý định.
3. Sau 5 lượt tư vấn của khách, AI chủ động hỏi khách có muốn kết nối chuyên viên hay không.
4. Khách có thể yêu cầu chuyên viên sớm hơn 5 lượt.
5. Khi khách đồng ý, Admin nhận thông báo thực tế.
6. Chuyên viên tiếp nhận và trò chuyện hai chiều với khách.
7. Toàn bộ lịch sử và trạng thái được lưu trong Database.
8. Các chức năng hiện tại vẫn hoạt động bình thường.

Hãy trực tiếp triển khai, chạy kiểm thử trên trình duyệt, đối chiếu API và Database, sau đó báo cáo kết quả trung thực.
