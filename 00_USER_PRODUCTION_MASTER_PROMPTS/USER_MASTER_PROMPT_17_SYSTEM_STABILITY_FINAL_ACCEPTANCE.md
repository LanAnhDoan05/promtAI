# USER MASTER PROMPT #17: 17 SYSTEM STABILITY FINAL ACCEPTANCE
> **Nguồn gốc:** Prompt chỉ đạo thực tế từ Người dùng (User Request) tại Step 7165.
> **Độ dài gốc:** 18287 ký tự.
> **Mục đích trong thư viện:** Cung cấp toàn văn đặc tả nghiệp vụ, yêu cầu kỹ thuật và ràng buộc sản xuất thực tế mà người dùng đã trực tiếp chỉ đạo và kiểm chứng trong dự án Routine Web.

---

# MASTER PROMPT: FINAL SYSTEM STABILITY & END-TO-END ACCEPTANCE – ROUTINE WEB

## MỤC TIÊU

Tiến hành kiểm tra, sửa lỗi và nghiệm thu toàn diện hệ thống Routine Web sau khi hoàn thiện các chức năng AI.

Mục tiêu là đảm bảo toàn bộ hệ thống hoạt động ổn định, liên thông, nhất quán dữ liệu và không phát sinh lỗi trong quá trình sử dụng thực tế.

Phạm vi kiểm tra bao gồm:

1. Frontend – giao diện người dùng.
2. Backend – API và xử lý nghiệp vụ.
3. Database – MySQL, Prisma và dữ liệu.
4. User – đăng ký, đăng nhập, hồ sơ, phân quyền.
5. Admin – quản trị sản phẩm, đơn hàng, khách hàng và các chức năng nội bộ.
6. Product – sản phẩm, danh mục, biến thể, giá và tồn kho.
7. Image – hình ảnh sản phẩm, ảnh biến thể, ảnh người dùng và hình ảnh giao diện.
8. Customer Storefront – toàn bộ trải nghiệm mua sắm.
9. Cart & Order – giỏ hàng, đặt hàng và quản lý đơn.
10. Payment & Shipping – thanh toán, phí vận chuyển và hóa đơn.
11. AI Agent – Gemini, AI Stylist, tư vấn bán hàng và Admin AI.
12. Real-time Synchronization – đồng bộ dữ liệu giữa Admin và Customer.
13. Security & Performance – bảo mật, tốc độ và khả năng vận hành.

**Đây là nhiệm vụ kiểm tra và ổn định hệ thống hiện tại, không phải xây dựng lại website.**

---

# PHẦN I. KIỂM TRA TỔNG THỂ KIẾN TRÚC

Trước khi chỉnh sửa, hãy kiểm tra toàn bộ dự án.

### 1. Frontend

- Kiểm tra cấu trúc React/Next.js.
- Kiểm tra các trang và routing.
- Kiểm tra component dùng chung.
- Kiểm tra trạng thái đăng nhập.
- Kiểm tra việc gọi API.
- Kiểm tra hiển thị dữ liệu.
- Kiểm tra responsive.
- Kiểm tra lỗi console.
- Kiểm tra các thành phần giao diện bị lỗi hoặc không hoạt động.

### 2. Backend

- Kiểm tra toàn bộ API.
- Kiểm tra middleware.
- Kiểm tra xác thực và phân quyền.
- Kiểm tra xử lý lỗi.
- Kiểm tra validation.
- Kiểm tra kết nối Database.
- Kiểm tra các nghiệp vụ liên quan đến sản phẩm, người dùng, đơn hàng và AI.

### 3. Database

- Kiểm tra MySQL.
- Kiểm tra Prisma Schema.
- Kiểm tra quan hệ giữa các bảng.
- Kiểm tra khóa chính, khóa ngoại.
- Kiểm tra dữ liệu bị thiếu hoặc không nhất quán.
- Kiểm tra các bản ghi trùng lặp.
- Kiểm tra dữ liệu mồ côi.
- Kiểm tra các trường dữ liệu bắt buộc.
- Kiểm tra tình trạng migration.

Không tự ý xóa hoặc thay đổi dữ liệu thật khi chưa có bản sao lưu và chưa xác định chính xác nguyên nhân.

### 4. Kiểm tra liên thông

Phải xác minh được luồng:

Frontend → Backend → Database → Backend → Frontend.

Đối với AI:

Frontend → Backend → Gemini → Tool Calling → Backend → MySQL → Gemini → Frontend.

Không được đánh giá hệ thống hoạt động bình thường chỉ dựa trên việc các server khởi động thành công.

---

# PHẦN II. KIỂM TRA VÀ SỬA TRIỆT ĐỂ LỖI HÌNH ẢNH

Đây là hạng mục ưu tiên đặc biệt.

Phải kiểm tra toàn bộ hệ thống hình ảnh, không chỉ riêng trang chủ.

## 1. Kiểm tra nguồn hình ảnh

Kiểm tra:
- URL hình ảnh trong MySQL.
- URL hình ảnh trong các biến thể sản phẩm.
- Đường dẫn hình ảnh trong API.
- Cấu trúc dữ liệu hình ảnh trả về từ Backend.
- Cấu hình hiển thị ảnh trong Frontend.
- Quy trình upload hình ảnh hiện tại.
- Các URL Cloudinary đang được sử dụng.
- Các đường dẫn ảnh nội bộ.
- Các ảnh có URL sai, không còn tồn tại hoặc không truy cập được.

Không thay đổi cấu hình Cloudinary, API Key, API Secret hoặc `.env`.

Chỉ kiểm tra và sửa lỗi sử dụng, lưu trữ, truy xuất và hiển thị hình ảnh theo cấu hình hiện có.

## 2. Kiểm tra toàn bộ vị trí hiển thị ảnh

Phải kiểm tra trực tiếp trên trình duyệt:

### Customer Storefront
- Banner trang chủ.
- Danh sách sản phẩm trang chủ.
- Ảnh sản phẩm trong từng danh mục.
- Kết quả tìm kiếm.
- Trang chi tiết sản phẩm.
- Ảnh theo từng màu sắc.
- Ảnh trong giỏ hàng.
- Ảnh trong trang thanh toán.
- Ảnh trong lịch sử đơn hàng.
- Ảnh trong danh sách sản phẩm yêu thích nếu có.
- Ảnh trong kết quả tư vấn AI.
- Ảnh trong outfit AI Stylist.

### Admin
- Danh sách sản phẩm.
- Trang thêm sản phẩm.
- Trang chỉnh sửa sản phẩm.
- Trang quản lý biến thể.
- Trang xem chi tiết sản phẩm.
- Trang quản lý đơn hàng.
- Trang quản lý khách hàng nếu có ảnh đại diện.
- Trang quản lý banner và nội dung giao diện nếu có.

### AI Agent
- AI trả đúng ảnh của sản phẩm được đề cập.
- Không lấy ảnh sản phẩm khác.
- Không tự tạo URL ảnh.
- Không sử dụng ảnh đã bị xóa hoặc không hợp lệ.
- Không trả về sản phẩm có ảnh bị lỗi khi có dữ liệu ảnh hợp lệ khác.

## 3. Kiểm tra chất lượng hình ảnh

Mỗi ảnh phải được kiểm tra:

- URL hợp lệ.
- Truy cập được.
- Trả về nội dung hình ảnh thực tế.
- Không bị lỗi 404, 403 hoặc lỗi máy chủ.
- Không bị ảnh trống.
- Không bị sai sản phẩm.
- Không bị biến dạng.
- Không bị kéo giãn sai tỷ lệ.
- Không bị cắt mất phần quan trọng.
- Không bị hiển thị ảnh thumbnail quá nhỏ ở vị trí cần ảnh lớn.
- Không bị trùng ảnh không hợp lý.
- Không bị lỗi khi tải chậm.

Kiểm tra cả kích thước ảnh gốc và ảnh hiển thị.

## 4. Quy chuẩn sửa lỗi hình ảnh

Nếu phát hiện lỗi:

- Xác định lỗi xuất phát từ Database, Backend, URL, CDN hay Frontend.
- Sửa đúng nguyên nhân.
- Giữ nguyên dữ liệu hình ảnh hợp lệ.
- Không thay ảnh bằng hình ngẫu nhiên.
- Không dùng ảnh placeholder để che giấu lỗi thật.
- Không tự tạo hình ảnh giả để làm đầy danh sách sản phẩm.
- Không tự thay đổi URL hàng loạt nếu chưa xác minh nguồn ảnh.
- Không xóa sản phẩm chỉ vì ảnh đang lỗi.
- Nếu không tìm được ảnh hợp lệ, đánh dấu rõ sản phẩm cần bổ sung ảnh.

Đối với hình ảnh sản phẩm, phải đảm bảo ảnh chính, ảnh phụ và ảnh theo màu sắc được liên kết đúng với sản phẩm và biến thể tương ứng.

## 5. Kiểm tra chức năng upload ảnh

Thử nghiệm:
- Thêm sản phẩm mới kèm ảnh.
- Chỉnh sửa ảnh sản phẩm.
- Thêm ảnh phụ.
- Thay ảnh theo màu sắc.
- Xóa ảnh theo đúng quy trình.
- Tải lại trang.
- Đăng nhập tài khoản khác.
- Kiểm tra ảnh vẫn hiển thị chính xác.

Nếu upload thất bại, phải hiển thị lỗi cụ thể, không lưu URL giả hoặc tạo bản ghi hình ảnh không hợp lệ.

---

# PHẦN III. KIỂM TRA FRONTEND TOÀN DIỆN

Mở trực tiếp website và kiểm tra từng trang.

### Customer

- Trang chủ.
- Trang danh mục.
- Trang tìm kiếm.
- Trang chi tiết sản phẩm.
- Trang giỏ hàng.
- Trang thanh toán.
- Trang đăng ký.
- Trang đăng nhập.
- Trang tài khoản cá nhân.
- Trang lịch sử đơn hàng.
- Trang AI Stylist.
- Trang hỗ trợ tư vấn.
- Các trang chính sách.

### Admin

- Dashboard.
- Quản lý sản phẩm.
- Thêm sản phẩm.
- Chỉnh sửa sản phẩm.
- Quản lý danh mục.
- Quản lý biến thể.
- Quản lý tồn kho.
- Quản lý đơn hàng.
- Quản lý khách hàng.
- Quản lý tư vấn.
- AI Admin.
- Quản lý các nội dung khác nếu có.

### Tiêu chí giao diện

- Không có trang trắng.
- Không có component bị vỡ.
- Không có ảnh bị mất.
- Không có dữ liệu hiển thị sai.
- Không có nút bấm vô tác dụng.
- Không có form không gửi được.
- Không có lỗi điều hướng.
- Không có lỗi console nghiêm trọng.
- Không có lỗi responsive ảnh hưởng đến sử dụng.
- Loading, empty state và error state phải hoạt động đúng.

Mỗi trang cần được kiểm tra cả khi có dữ liệu, không có dữ liệu và khi API bị lỗi.

---

# PHẦN IV. KIỂM TRA BACKEND VÀ API

Kiểm tra toàn bộ các nhóm API hiện có.

### 1. User & Authentication
- Đăng ký.
- Đăng nhập.
- Đăng xuất.
- Xác thực phiên.
- Phân quyền.
- Cập nhật hồ sơ.
- Đổi mật khẩu.
- Kiểm soát quyền truy cập.

### 2. Product
- Lấy danh sách sản phẩm.
- Lấy chi tiết sản phẩm.
- Thêm sản phẩm.
- Sửa sản phẩm.
- Ẩn sản phẩm.
- Khôi phục sản phẩm nếu hỗ trợ.
- Xóa mềm.
- Lấy biến thể.
- Cập nhật giá.
- Cập nhật tồn kho.
- Tìm kiếm và lọc.
- Phân trang.

### 3. Cart & Order
- Thêm sản phẩm vào giỏ.
- Cập nhật số lượng.
- Xóa sản phẩm.
- Kiểm tra tồn kho.
- Tạo đơn hàng.
- Tính tổng tiền.
- Lưu địa chỉ.
- Lưu phí vận chuyển.
- Tra cứu đơn hàng.
- Cập nhật trạng thái theo quyền.

### 4. Support
- Tạo cuộc trò chuyện.
- Gửi tin nhắn.
- Chuyển tiếp chuyên viên.
- Nhận yêu cầu tư vấn.
- Phân công nhân viên.
- Trả lời khách.
- Cập nhật trạng thái.

### 5. AI
- Kiểm tra Gemini API.
- Kiểm tra Tool Calling.
- Kiểm tra quyền công cụ.
- Kiểm tra dữ liệu trả về.
- Kiểm tra timeout.
- Kiểm tra fallback.
- Kiểm tra giới hạn truy vấn.
- Kiểm tra xử lý lỗi.

Không chỉ kiểm tra HTTP status. Phải xác minh nội dung phản hồi, dữ liệu Database và nghiệp vụ thực tế.

---

# PHẦN V. KIỂM TRA USER VÀ PHÂN QUYỀN

Phải kiểm tra tối thiểu các nhóm:

- Khách chưa đăng nhập.
- Khách đã đăng nhập.
- Nhân viên tư vấn.
- Quản trị viên.

Kiểm tra:
- Mỗi tài khoản chỉ được thực hiện đúng quyền.
- Khách không truy cập trang Admin.
- Khách không đọc dữ liệu người khác.
- Nhân viên không được truy cập chức năng ngoài quyền.
- Admin truy cập đúng các chức năng được cấp.
- AI không được vượt quyền của người đang sử dụng.
- Không bị mất phiên đăng nhập bất thường.
- Không xảy ra lỗi phân quyền sau khi refresh trang.

Kiểm tra cả thao tác trực tiếp trên giao diện và gọi API.

---

# PHẦN VI. KIỂM TRA ADMIN VÀ CUSTOMER ĐỒNG BỘ DỮ LIỆU

Mở đồng thời hai tab:

- Tab 1: Admin.
- Tab 2: Customer.

Thực hiện kiểm thử thực tế:

1. Admin thêm sản phẩm → Customer nhìn thấy sản phẩm.
2. Admin sửa tên sản phẩm → Customer cập nhật tên.
3. Admin sửa giá → Customer cập nhật giá.
4. Admin thay ảnh → Customer hiển thị ảnh mới.
5. Admin thêm màu sắc → Customer nhìn thấy màu mới.
6. Admin thêm kích cỡ → Customer nhìn thấy kích cỡ mới.
7. Admin cập nhật tồn kho → Customer cập nhật tình trạng hàng.
8. Admin ẩn sản phẩm → Customer không còn nhìn thấy.
9. Khách đặt hàng → Admin nhận được đơn mới.
10. Admin cập nhật trạng thái đơn → Customer nhìn thấy trạng thái mới.
11. Khách gửi yêu cầu tư vấn → Admin nhận được yêu cầu.
12. Nhân viên trả lời → Customer nhận được tin nhắn.

Kiểm tra cơ chế:
- Socket.IO.
- SSE.
- Polling.
- Cache.
- Revalidation.
- Các cơ chế đồng bộ hiện có.

Ưu tiên tận dụng hệ thống đang hoạt động. Không tạo thêm một cơ chế realtime khác nếu không cần thiết.

Nếu không thể cập nhật tức thời, phải đảm bảo cơ chế tải lại dữ liệu hoạt động chính xác và không hiển thị dữ liệu cũ kéo dài.

---

# PHẦN VII. KIỂM TRA AI AGENT SAU KHI CHUẨN HÓA

Kiểm tra tất cả chức năng AI đã được chuẩn hóa ở nhiệm vụ trước.

### Customer AI
- Tìm kiếm sản phẩm.
- Liệt kê đầy đủ kết quả.
- Tư vấn thông tin sản phẩm.
- Tư vấn size.
- So sánh sản phẩm.
- Phối đồ khi được yêu cầu.
- Không tự phối đồ khi khách chỉ tìm kiếm.
- Hỗ trợ giỏ hàng.
- Hỗ trợ đặt hàng.
- Hỗ trợ vận chuyển.
- Tra cứu đơn hàng.
- Chuyển chuyên viên.

### Admin AI
- Phân tích doanh thu.
- Phân tích đơn hàng.
- Phân tích sản phẩm.
- Phân tích tồn kho.
- Phân tích khách hàng.
- Đề xuất nhập hàng.
- Đề xuất Marketing.
- Hỗ trợ tư vấn khách hàng.

### Kiểm tra độ chính xác

Với mỗi yêu cầu:
1. Ghi lại câu hỏi.
2. Ghi nhận ý định được AI phân loại.
3. Ghi nhận Tool Calling.
4. Ghi nhận dữ liệu Backend trả về.
5. Đối chiếu với MySQL.
6. Ghi lại câu trả lời cuối cùng.
7. Đánh giá kết quả.

Không chấp nhận:
- AI tự bịa sản phẩm.
- AI tự bịa giá.
- AI tự bịa tồn kho.
- AI trả sai ảnh sản phẩm.
- AI tự xác nhận thanh toán.
- AI truy cập dữ liệu ngoài quyền.
- AI báo đã chuyển nhân viên nhưng không tạo yêu cầu thật.

---

# PHẦN VIII. KIỂM TRA NGHIỆP VỤ MUA HÀNG

Thực hiện một hành trình hoàn chỉnh:

1. Khách vào trang chủ.
2. Tìm sản phẩm.
3. Xem chi tiết sản phẩm.
4. Chọn màu sắc.
5. Chọn kích cỡ.
6. Kiểm tra tồn kho.
7. Thêm vào giỏ hàng.
8. Cập nhật số lượng.
9. Nhập thông tin giao hàng.
10. Backend kiểm tra địa chỉ.
11. Backend tính phí vận chuyển.
12. Hiển thị hóa đơn.
13. Tạo đơn hàng.
14. Thanh toán qua VNPay Sandbox nếu được cấu hình.
15. Backend xác thực callback và chữ ký.
16. Cập nhật trạng thái thanh toán.
17. Admin nhìn thấy đơn hàng.
18. Khách xem lịch sử đơn hàng.

Công thức:

Tổng thanh toán = Tiền hàng - Giảm giá + Phí vận chuyển.

Phải đối chiếu tổng tiền ở:
- Giỏ hàng.
- Checkout.
- Database.
- Admin.
- VNPay Sandbox.
- Hóa đơn khách hàng.

Không tạo giao dịch thật.

---

# PHẦN IX. KIỂM TRA DỮ LIỆU VÀ TÍNH NHẤT QUÁN

Kiểm tra các vấn đề:

- Sản phẩm không có danh mục.
- Sản phẩm không có ảnh hợp lệ.
- Sản phẩm không có giá.
- Biến thể không thuộc sản phẩm.
- Tồn kho âm hoặc sai.
- Đơn hàng không có khách hàng hợp lệ.
- Đơn hàng thiếu chi tiết.
- Tổng tiền đơn hàng sai.
- Phí vận chuyển không khớp hóa đơn.
- Ảnh bị mồ côi.
- Khách hàng trùng lặp không hợp lý.
- Bản ghi test bị trộn vào dữ liệu mô phỏng.
- Dữ liệu AI không khớp dữ liệu sản phẩm.

Phải phân biệt rõ:
- Dữ liệu sản phẩm.
- Dữ liệu khách hàng.
- Dữ liệu giao dịch thực tế.
- Dữ liệu mô phỏng DEMO.
- Dữ liệu kiểm thử TEST.

Không được tự nhận dữ liệu mô phỏng là giao dịch thật.

Không xóa dữ liệu chỉ vì nghi ngờ là dữ liệu test. Trước khi xử lý phải xác định nguồn gốc và có phương án sao lưu.

---

# PHẦN X. KIỂM TRA HIỆU NĂNG VÀ ĐỘ ỔN ĐỊNH

Kiểm tra:

- Tốc độ tải trang.
- Tốc độ tải ảnh.
- Tốc độ truy vấn Database.
- Thời gian phản hồi API.
- Lỗi gọi API liên tục.
- Rò rỉ bộ nhớ nếu có bằng chứng.
- Truy vấn trùng lặp.
- Lỗi tải lại dữ liệu.
- Cache không được cập nhật.
- Timeout Gemini.
- Xử lý khi mất kết nối.
- Khả năng phục hồi sau khi server khởi động lại.

Kiểm tra các lỗi phổ biến:
- 400.
- 401.
- 403.
- 404.
- 409.
- 422.
- 429.
- 500.
- 502.
- 503.
- 504.

Không được tùy tiện tăng timeout hoặc retry vô hạn để che giấu lỗi gốc.

---

# PHẦN XI. QUY TRÌNH THỰC HIỆN SỬA LỖI

Thực hiện theo thứ tự:

### Giai đoạn 1 – Audit

- Kiểm tra toàn bộ Frontend.
- Kiểm tra toàn bộ Backend.
- Kiểm tra Database.
- Kiểm tra hình ảnh.
- Kiểm tra User và Admin.
- Kiểm tra AI Agent.
- Kiểm tra liên thông.
- Lập danh sách lỗi.

Phân loại:
- CRITICAL: Làm hệ thống không thể sử dụng hoặc có nguy cơ mất dữ liệu/bảo mật.
- HIGH: Lỗi nghiệp vụ quan trọng.
- MEDIUM: Lỗi ảnh hưởng một phần chức năng.
- LOW: Lỗi giao diện nhỏ.

### Giai đoạn 2 – Xác định nguyên nhân

Mỗi lỗi phải xác định:
- Vị trí phát sinh.
- Nguyên nhân.
- Phạm vi ảnh hưởng.
- Dữ liệu liên quan.
- Phương án sửa.

Không sửa theo kiểu thử ngẫu nhiên.

### Giai đoạn 3 – Sửa lỗi

Ưu tiên:
1. Lỗi bảo mật và dữ liệu.
2. Lỗi Database và Backend.
3. Lỗi hình ảnh.
4. Lỗi liên thông Frontend – Backend.
5. Lỗi nghiệp vụ.
6. Lỗi AI.
7. Lỗi giao diện và hiệu năng.

Không refactor toàn bộ dự án khi chỉ cần sửa một lỗi cụ thể.

### Giai đoạn 4 – Regression Testing

Sau mỗi lần sửa:
- Chạy lại kiểm thử chức năng liên quan.
- Kiểm tra các chức năng phụ thuộc.
- Kiểm tra các chức năng cũ.
- Đảm bảo không phát sinh lỗi mới.

### Giai đoạn 5 – Final Acceptance

Kiểm tra lại toàn bộ hệ thống trên trình duyệt và đối chiếu Database.

---

# PHẦN XII. BẰNG CHỨNG VÀ BÁO CÁO NGHIỆM THU

Tạo các tài liệu:

1. `docs/FINAL_SYSTEM_STABILITY_AUDIT.md`
2. `docs/FRONTEND_ACCEPTANCE_REPORT.md`
3. `docs/BACKEND_API_ACCEPTANCE_REPORT.md`
4. `docs/DATABASE_INTEGRITY_REPORT.md`
5. `docs/IMAGE_ASSET_AUDIT_REPORT.md`
6. `docs/USER_ADMIN_ACCEPTANCE_REPORT.md`
7. `docs/ADMIN_CUSTOMER_SYNC_REPORT.md`
8. `docs/AI_AGENT_ACCEPTANCE_REPORT.md`
9. `docs/ECOMMERCE_E2E_TEST_REPORT.md`
10. `docs/FINAL_SYSTEM_ACCEPTANCE_REPORT.md`

Mỗi báo cáo phải thể hiện:

- Chức năng được kiểm tra.
- Kết quả mong đợi.
- Kết quả thực tế.
- Trạng thái PASS / FAIL / BLOCKED / NOT TESTED.
- Bằng chứng kiểm thử.
- Lỗi phát hiện.
- Nguyên nhân.
- Cách khắc phục.
- Kết quả kiểm thử lại.

Bằng chứng phải phân biệt rõ:

1. Code review.
2. Unit test.
3. API integration test.
4. Database verification.
5. Browser UI test.
6. End-to-end test.
7. Gemini Tool Calling thực tế.

Không dùng kết quả của một loại kiểm thử để khẳng định các loại khác đã thành công.

Đối với hình ảnh, cần có danh sách:
- Tổng số ảnh được kiểm tra.
- Số ảnh hợp lệ.
- Số ảnh lỗi.
- Số ảnh đã sửa.
- Số ảnh cần bổ sung.
- Các vị trí đã kiểm tra trên giao diện.

---

# PHẦN XIII. ĐIỀU KIỆN AN TOÀN BẮT BUỘC

- Không thay đổi Cloudinary hoặc cấu hình `.env`.
- Không yêu cầu người dùng gửi API Key hoặc mật khẩu.
- Không ghi dữ liệu thử nghiệm vào MySQL `defaultdb`.
- Sử dụng `routine_test_db` cho các kiểm thử có ghi dữ liệu.
- Không xóa dữ liệu thật.
- Không chạy `DROP DATABASE`, `TRUNCATE`, `prisma migrate reset` hoặc migration phá hủy dữ liệu.
- Không tạo thanh toán thật.
- Không gửi SMS, OTP hoặc email thật đến dữ liệu thử nghiệm.
- Không thay đổi cấu trúc dữ liệu lớn nếu chưa đánh giá tác động và sao lưu.
- Kiểm tra `git status` trước khi chỉnh sửa.
- Bảo toàn tất cả thay đổi chưa commit.
- Không tự động thay thế ảnh hợp lệ bằng ảnh không rõ nguồn.
- Không sử dụng dữ liệu giả để che lỗi hệ thống.
- Không đánh dấu PASS khi chưa có bằng chứng thực tế.

Nếu một chức năng bị BLOCKED vì thiếu quyền, cấu hình hoặc dữ liệu, phải báo cáo rõ nguyên nhân thay vì tự nhận đã kiểm thử thành công.

---

# XIV. TIÊU CHUẨN HOÀN THÀNH

Hệ thống chỉ được nghiệm thu khi:

- Frontend hoạt động ổn định.
- Backend hoạt động ổn định.
- Database không có lỗi toàn vẹn nghiêm trọng.
- User và Admin hoạt động đúng quyền.
- Quản lý sản phẩm và đơn hàng hoạt động.
- Hình ảnh hiển thị chính xác trên toàn bộ các trang.
- Upload và cập nhật ảnh hoạt động đúng.
- Customer và Admin đồng bộ dữ liệu.
- AI Agent hoạt động đúng quy chuẩn.
- AI Stylist không tự phối đồ khi khách chưa yêu cầu.
- AI tư vấn dựa trên dữ liệu thật.
- Chuyển tiếp chuyên viên hoạt động hai chiều.
- Giỏ hàng, đơn hàng, thanh toán Sandbox và vận chuyển tính đúng.
- Không có lỗi CRITICAL hoặc HIGH chưa được xử lý.
- Các lỗi đã sửa đều được kiểm thử lại.
- Có báo cáo nghiệm thu và bằng chứng.

**YÊU CẦU CUỐI CÙNG:**

Hãy thực hiện kiểm tra và sửa lỗi trực tiếp trên dự án hiện tại.

Không chỉ đưa ra danh sách đề xuất. Hãy thực sự chạy hệ thống, mở trình duyệt, thao tác các chức năng, kiểm tra API, đối chiếu MySQL và kiểm tra hình ảnh.

Ưu tiên giải quyết triệt để lỗi hình ảnh và các lỗi liên thông dữ liệu.

Không được hy sinh tính toàn vẹn dữ liệu để làm cho giao diện trông có vẻ hoạt động tốt.

Kết thúc công việc, hãy đưa ra đánh giá trung thực về mức độ sẵn sàng của Routine Web, những gì đã kiểm chứng, những gì chưa thể kiểm chứng và các vấn đề còn tồn tại.

Mục tiêu cuối cùng là một website thương mại điện tử có thể trình diễn và vận hành xuyên suốt từ Admin đến Customer, từ Database đến AI Agent, không bị lỗi hình ảnh, không sai dữ liệu và không có chức năng chỉ hoạt động trên giao diện giả lập.
