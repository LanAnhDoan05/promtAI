# USER MASTER PROMPT #20: 20 FINAL E2E INTEGRATION TEST
> **Nguồn gốc:** Prompt chỉ đạo thực tế từ Người dùng (User Request) tại Step 8473.
> **Độ dài gốc:** 9412 ký tự.
> **Mục đích trong thư viện:** Cung cấp toàn văn đặc tả nghiệp vụ, yêu cầu kỹ thuật và ràng buộc sản xuất thực tế mà người dùng đã trực tiếp chỉ đạo và kiểm chứng trong dự án Routine Web.

---

# PROMPT: FINAL END-TO-END INTEGRATION TEST & ACCEPTANCE – ROUTINE WEB

## 1. MỤC TIÊU

Sau khi hoàn thành các yêu cầu sửa lỗi và nâng cấp gần nhất, hãy thực hiện kiểm thử End-to-End toàn diện trên hệ thống Routine Web.

Mục tiêu là xác nhận toàn bộ Frontend, Backend, MySQL, Gemini AI Agent, trang Admin và các chức năng thanh toán hoạt động liên thông chính xác.

Không chỉ kiểm tra API hoặc đọc code rồi kết luận PASS. Phải thực hiện thao tác thực tế trên trình duyệt, kiểm tra dữ liệu Backend và MySQL để chứng minh kết quả.

Không tự ý phát triển thêm tính năng mới. Chỉ sửa lỗi được phát hiện trong quá trình kiểm thử và kiểm tra hồi quy sau khi sửa.

## 2. NGUYÊN TẮC KIỂM THỬ VÀ BẢO VỆ DỮ LIỆU

- Kiểm tra Git status trước khi sửa, bảo toàn các thay đổi chưa commit.
- Không thay đổi cấu hình Cloudinary, API key, API secret hoặc file .env.
- Không ghi, sửa, xóa dữ liệu trên MySQL `defaultdb`.
- Mọi thao tác tạo, sửa, xóa dữ liệu kiểm thử phải sử dụng `routine_test_db`.
- Không chạy DROP DATABASE, TRUNCATE, prisma migrate reset hoặc lệnh phá hủy dữ liệu.
- Không thực hiện thanh toán thật; chỉ sử dụng VNPay Sandbox hoặc môi trường kiểm thử tương đương.
- Không gửi SMS, OTP hoặc email thật cho dữ liệu kiểm thử.
- Không tạo dữ liệu khách hàng giả rồi trình bày như khách hàng thật.
- Không sửa dữ liệu để ép kết quả kiểm thử thành PASS.

## 3. KIỂM THỬ QR VÀ THANH TOÁN

Thực hiện đầy đủ luồng:

Khách hàng → Giỏ hàng → Checkout → Tính tổng tiền → Tạo đơn hàng → Chọn thanh toán → Hiển thị QR → Thanh toán Sandbox → Backend nhận callback → Cập nhật trạng thái đơn hàng → Admin nhìn thấy đơn hàng.

Kiểm tra:
1. QR có thực sự hiển thị trên giao diện không.
2. QR có đúng với dữ liệu thanh toán của đơn hàng không.
3. Mã đơn hàng, số tiền và thông tin thanh toán có khớp không.
4. Tổng thanh toán có bao gồm phí vận chuyển và giảm giá không.
5. Làm mới trang có làm mất hoặc tạo trùng đơn hàng không.
6. QR hết hạn có được xử lý chính xác không.
7. Thanh toán thành công và thất bại có cập nhật đúng trạng thái không.
8. Backend có xác thực chữ ký callback không.
9. Callback gửi lặp có bị ghi nhận thanh toán hai lần không.
10. Admin và khách hàng có nhận được trạng thái đơn hàng chính xác không.

Không được kết luận QR hoạt động chỉ vì có một ảnh QR hiển thị. Phải xác minh QR tương ứng với giao dịch thực tế trong môi trường Sandbox.

## 4. KIỂM THỬ AI CHATBOT DUY TRÌ NGỮ CẢNH

Thực hiện hội thoại thực tế trên giao diện khách hàng.

### Kịch bản A: Tìm kiếm nối tiếp

- Khách: Tìm áo len dưới 1 triệu.
- Khách: Có màu trắng không?
- Khách: Có size M không?
- Khách: Chất liệu cotton thì sao?
- Khách: Có mẫu nào khác không?

AI phải giữ đầy đủ các điều kiện trước đó và chỉ cập nhật khi khách thay đổi.

### Kịch bản B: Thay đổi điều kiện

- Tìm áo len dưới 1 triệu màu trắng.
- Đổi sang màu đen.
- Tăng ngân sách lên 1,5 triệu.
- Bỏ điều kiện màu sắc.

Kiểm tra AI cập nhật đúng từng điều kiện, không giữ nhầm bộ lọc cũ.

### Kịch bản C: Hỏi về sản phẩm cụ thể

- Tìm áo len dưới 1 triệu.
- Mẫu thứ hai có chất liệu gì?
- Mẫu đó còn size M không?
- Có màu khác không?

AI phải xác định đúng sản phẩm đang được đề cập và truy vấn đúng dữ liệu.

### Kịch bản D: Chuyển nhu cầu

- Tìm áo len dưới 1 triệu.
- Chuyển sang tìm quần jeans.
- Tìm áo sơ mi màu trắng.

AI phải nhận biết yêu cầu mới, không áp dụng nhầm loại sản phẩm cũ.

### Kịch bản E: Tính chính xác dữ liệu

Kiểm tra tối thiểu:
- Tên sản phẩm.
- Giá bán.
- Màu sắc.
- Size.
- Chất liệu.
- Tình trạng tồn kho.
- Hình ảnh.
- Sản phẩm còn kinh doanh hay đã ẩn.

Đối chiếu trực tiếp với MySQL và kết quả Backend.

Không được tự tạo thông tin khi dữ liệu không tồn tại.

## 5. KIỂM THỬ BỘ ĐẾM 5 LƯỢT VÀ CHUYỂN TIẾP CHUYÊN VIÊN

Thực hiện các trường hợp:

1. Khách hỏi 1 lượt: AI tiếp tục tư vấn bình thường.
2. Khách hỏi 2–4 lượt: AI tiếp tục duy trì ngữ cảnh.
3. Khách hỏi lượt thứ 5: AI hoàn thành câu trả lời rồi đề nghị kết nối chuyên viên.
4. Khách từ chối: AI tiếp tục tư vấn, không hỏi lặp lại liên tục.
5. Khách đồng ý: Backend tạo yêu cầu hỗ trợ thực tế.
6. Khách chủ động yêu cầu chuyên viên trước lượt thứ 5: Cho phép chuyển ngay.
7. Khách tải lại trang: Không mất lịch sử và bộ đếm.
8. Hai khách cùng sử dụng chatbot: Không nhầm lịch sử hoặc bộ đếm.
9. Tin nhắn lỗi, trùng hoặc tin nhắn từ AI: Không được tính thành lượt hỏi của khách.
10. Khách chuyển tiếp: Chuyên viên nhận được đầy đủ lịch sử và bộ lọc tìm kiếm hiện tại.

## 6. KIỂM THỬ TRANG QUẢN TRỊ VÀ THÔNG BÁO

Mở đồng thời hai tab:

- Tab 1: Website khách hàng.
- Tab 2: Trang quản trị Admin.

Kiểm tra:

- Khách đồng ý chuyển chuyên viên → Admin nhận thông báo.
- Yêu cầu tư vấn mới xuất hiện trong danh sách.
- Số lượng yêu cầu chưa xử lý tăng chính xác.
- Admin xem được lịch sử trò chuyện.
- Admin xem được thông tin sản phẩm khách quan tâm, ngân sách, màu sắc, size và nhu cầu.
- Admin có thể tiếp nhận hoặc phân công chuyên viên.
- Chuyên viên phản hồi → Khách nhận được tin nhắn.
- Khách phản hồi → Admin nhìn thấy tin nhắn mới.
- Trạng thái hội thoại được cập nhật chính xác.
- Không tạo nhiều yêu cầu trùng cho một lần đồng ý.
- Khi chuyên viên đang tư vấn, AI không tiếp tục trả lời chen ngang.

Kiểm tra cả trường hợp tải lại trang và mất kết nối tạm thời.

## 7. KIỂM THỬ ĐỒNG BỘ ADMIN – WEBSITE – AI

Thực hiện thao tác thật trên Admin và xác nhận kết quả ở Website và AI:

1. Thêm sản phẩm mới → Website hiển thị → AI tìm được.
2. Sửa giá → Website và AI cập nhật đúng.
3. Thêm màu sắc → Website và AI nhận diện được.
4. Thêm size → Website và AI nhận diện đúng.
5. Cập nhật tồn kho → Kết quả tư vấn phản ánh đúng.
6. Chuyển sản phẩm sang INACTIVE → Website và AI không tiếp tục giới thiệu như sản phẩm đang bán.
7. Cập nhật hình ảnh → Các giao diện hiển thị đúng ảnh.
8. Xóa mềm sản phẩm → Không còn xuất hiện trong kết quả tìm kiếm công khai.

Phải kiểm tra việc làm mới cache và đồng bộ dữ liệu, không chỉ kiểm tra giao diện sau khi tải lại trang.

## 8. KIỂM THỬ TOÀN BỘ HÀNH TRÌNH KHÁCH HÀNG

Thực hiện một hành trình mua hàng hoàn chỉnh:

1. Truy cập trang chủ.
2. Tìm kiếm sản phẩm.
3. Sử dụng AI Stylist để tư vấn.
4. Lọc sản phẩm bằng hội thoại liên tiếp.
5. Xem chi tiết sản phẩm.
6. Chọn màu sắc và size.
7. Thêm vào giỏ hàng.
8. Đăng nhập hoặc đăng ký.
9. Nhập thông tin giao hàng.
10. Kiểm tra tính hợp lệ địa chỉ theo dữ liệu Backend hỗ trợ.
11. Tính phí vận chuyển.
12. Kiểm tra tổng tiền trên hóa đơn.
13. Đặt hàng.
14. Thanh toán Sandbox.
15. Xem lịch sử và trạng thái đơn hàng.
16. Admin tiếp nhận và xử lý đơn hàng.

Đối chiếu dữ liệu đơn hàng giữa giao diện khách hàng, Backend và MySQL.

## 9. KIỂM THỬ GIAO DIỆN VÀ KỸ THUẬT

Kiểm tra trực tiếp:
- Trang chủ.
- Danh mục sản phẩm.
- Tìm kiếm.
- Chi tiết sản phẩm.
- Giỏ hàng.
- Checkout.
- QR thanh toán.
- AI Stylist.
- Đăng nhập và đăng ký.
- Lịch sử đơn hàng.
- Quản trị sản phẩm.
- Quản trị đơn hàng.
- Quản trị khách hàng.
- Quản trị yêu cầu tư vấn.

Kiểm tra:
- Không có ảnh bị lỗi hoặc ảnh không đúng sản phẩm.
- Không có nút bấm không hoạt động.
- Không có dữ liệu hiển thị sai.
- Không có lỗi JavaScript nghiêm trọng.
- Không có API lỗi trong các luồng chính.
- Không có lỗi phân quyền.
- Không để lộ dữ liệu nhạy cảm.
- Không tạo đơn hàng hoặc yêu cầu tư vấn trùng lặp.
- Không để AI truy cập dữ liệu ngoài quyền hạn.

## 10. QUY ĐỊNH BÁO CÁO KẾT QUẢ

Tạo báo cáo:

- `docs/FINAL_END_TO_END_ACCEPTANCE_REPORT.md`
- `docs/QR_PAYMENT_E2E_TEST_REPORT.md`
- `docs/AI_CONTEXTUAL_CONVERSATION_E2E_REPORT.md`
- `docs/AI_FIVE_TURN_HANDOFF_E2E_REPORT.md`
- `docs/ADMIN_CUSTOMER_REALTIME_E2E_REPORT.md`
- `docs/FINAL_REGRESSION_TEST_REPORT.md`

Báo cáo tổng hợp cần có:

| Hạng mục | Tổng test | PASS | FAIL | BLOCKED |
|---|---:|---:|---:|---:|
| QR và thanh toán | | | | |
| AI duy trì ngữ cảnh | | | | |
| Bộ đếm 5 lượt | | | | |
| Chuyển tiếp chuyên viên | | | | |
| Admin và thông báo | | | | |
| Đồng bộ Admin – Website – AI | | | | |
| Hành trình mua hàng | | | | |
| Giao diện và kỹ thuật | | | | |

Với mỗi lỗi, ghi rõ:
- Mô tả lỗi.
- Nguyên nhân.
- File/API/Database liên quan.
- Cách khắc phục.
- Kết quả kiểm thử lại.

Mỗi kết quả phải ghi rõ bằng chứng thuộc loại nào:
- Code Review.
- API Test.
- Browser UI Test.
- Database Verification.
- Gemini Live Tool Calling.
- Sandbox Payment Callback.

Không được đánh đồng việc kiểm tra code với việc kiểm thử giao diện thực tế.

## 11. ĐIỀU KIỆN NGHIỆM THU CUỐI CÙNG

Chỉ kết luận READY FOR DEMO khi:

- Các luồng chính đều PASS.
- QR hiển thị và thanh toán Sandbox được xác minh.
- AI hiểu chính xác các câu hỏi nối tiếp.
- AI không mất ngữ cảnh khi tải lại trang.
- Bộ đếm 5 lượt hoạt động đúng.
- Chuyển tiếp chuyên viên tạo yêu cầu thật trong Backend và Admin nhận được.
- Admin và khách hàng trao đổi hai chiều được.
- Sản phẩm, giá, màu, size, tồn kho và hình ảnh đồng bộ chính xác.
- Không có lỗi nghiêm trọng về bảo mật, dữ liệu hoặc thanh toán.

Nếu còn lỗi BLOCKED hoặc FAIL ảnh hưởng đến luồng chính, phải ghi rõ và không được tự kết luận hệ thống đã nghiệm thu hoàn toàn.

Cuối cùng, cung cấp hướng dẫn kiểm thử thủ công từng bước để tôi có thể tự trình diễn trước giảng viên.
