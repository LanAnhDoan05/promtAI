# USER MASTER PROMPT #08: 08 FINAL REGRESSION AND HANDOVER
> **Nguồn gốc:** Prompt chỉ đạo thực tế từ Người dùng (User Request) tại Step 2702.
> **Độ dài gốc:** 18617 ký tự.
> **Mục đích trong thư viện:** Cung cấp toàn văn đặc tả nghiệp vụ, yêu cầu kỹ thuật và ràng buộc sản xuất thực tế mà người dùng đã trực tiếp chỉ đạo và kiểm chứng trong dự án Routine Web.

---

# FINAL MASTER PROMPT – COMPLETE ALL REMAINING FEATURES, FULL REGRESSION TESTING & FINAL HANDOVER – ROUTINE WEB

**Dự án:** Routine Web E-commerce  
**Phạm vi:** Toàn bộ hệ thống Frontend + Backend + Database + Admin + Customer Storefront + Gemini AI Stylist + AI Business Intelligence + các module liên quan.

**Mục tiêu:** Hoàn thiện toàn bộ chức năng còn thiếu, sửa tất cả lỗi đã phát hiện, kiểm thử toàn diện và bàn giao một phiên bản ổn định để tôi trực tiếp nghiệm thu thủ công trên trình duyệt.

Đây là đợt hoàn thiện cuối cùng trước khi tôi tự kiểm thử. Không được chỉ đưa ra kế hoạch, báo cáo hoặc chạy lại những bài test cũ. Bạn phải thực hiện trực tiếp trên source code và môi trường đang chạy.

# PHẦN I. NGUYÊN TẮC THỰC HIỆN

## 1. Kiểm tra lại toàn bộ trạng thái hiện tại

Trước khi sửa bất cứ thứ gì:

- Đọc cấu trúc toàn bộ dự án.
- Kiểm tra Git status và bảo toàn các thay đổi chưa commit.
- Đọc các báo cáo kiểm thử trước đó.
- Đọc báo cáo khôi phục ảnh `docs/PRODUCT_IMAGE_RECOVERY_REPORT.md` nếu đã được tạo.
- Kiểm tra những lỗi đã sửa và những lỗi còn tồn tại.
- Đối chiếu chức năng thực tế trong source code với yêu cầu dự án.
- Kiểm tra trạng thái Frontend, Backend, Database và các dịch vụ tích hợp.

Không được mặc định những nội dung Anti từng báo cáo PASS vẫn đang hoạt động. Phải kiểm tra lại trên phiên bản hiện tại.

## 2. Bảo vệ dữ liệu và cấu hình

Các quy định bắt buộc:

- Chỉ sử dụng `routine_test_db` cho thao tác tạo, sửa, xóa và kiểm thử dữ liệu.
- Không sửa, xóa hoặc ghi dữ liệu vào `defaultdb`.
- Không chạy lệnh xóa Database, reset Database hoặc migration phá hủy.
- Không làm mất dữ liệu hoặc thay đổi cấu trúc Database khi chưa có căn cứ và phương án an toàn.
- Không ghi đè các thay đổi Git của tôi.
- Không để lộ API Key, mật khẩu, JWT Secret hoặc thông tin kết nối.
- Không cấu hình lại, thay đổi hoặc tích hợp lại Cloudinary.
- Không chỉnh sửa Cloudinary API Key, API Secret, Cloud Name hoặc `.env` liên quan.
- Chỉ kiểm tra hoạt động của Cloudinary hiện có.
- Không thay đổi cấu hình Gemini nếu chưa xác định được lỗi.
- Không tự ý thay thế công nghệ hoặc viết lại toàn bộ dự án.

Nếu Backend đang kết nối sai Database, hãy dừng các thao tác ghi và báo rõ nguyên nhân. Không tự ý chuyển môi trường mà không xác nhận được cấu hình an toàn.

# PHẦN II. LẬP DANH SÁCH VÀ HOÀN THIỆN TOÀN BỘ CHỨC NĂNG

Trước tiên, lập danh sách đầy đủ các module và chức năng thực tế đang tồn tại trong dự án.

Phân loại từng chức năng:

- Đã hoàn thiện và hoạt động.
- Đã triển khai nhưng còn lỗi.
- Chưa hoàn thiện.
- Chưa triển khai.
- Không thể kiểm thử do thiếu dữ liệu hoặc điều kiện.

Sau đó, xử lý tất cả chức năng thuộc phạm vi dự án theo thứ tự ưu tiên.

Không được bỏ sót chức năng đang tồn tại chỉ vì nó không xuất hiện trong danh sách bên dưới.

## 1. CUSTOMER STOREFRONT

Hoàn thiện và kiểm thử:

- Trang chủ.
- Header, Footer, Menu và điều hướng.
- Danh sách sản phẩm.
- Danh mục sản phẩm.
- Tìm kiếm theo tên, mã và slug.
- Bộ lọc.
- Sắp xếp.
- Phân trang.
- Sản phẩm nổi bật và bán chạy.
- Trang chi tiết sản phẩm.
- Hình ảnh sản phẩm.
- Màu sắc, kích cỡ và biến thể.
- Giá bán và giá khuyến mãi nếu có.
- Tồn kho và trạng thái sản phẩm.
- Sản phẩm liên quan.
- Yêu thích nếu có.
- Giỏ hàng.
- Thay đổi số lượng.
- Xóa sản phẩm khỏi giỏ hàng.
- Tính tổng tiền.
- Đăng ký.
- Đăng nhập.
- Đăng xuất.
- Quản lý thông tin tài khoản.
- Địa chỉ giao hàng nếu có.
- Checkout.
- Đặt hàng.
- Thanh toán VNPay Sandbox.
- Lịch sử đơn hàng.
- Chi tiết đơn hàng.
- Theo dõi trạng thái đơn hàng.

Đảm bảo các chức năng hoạt động thực tế, không chỉ có giao diện.

## 2. ADMIN

Rà soát và hoàn thiện toàn bộ các module Admin hiện có:

- Đăng nhập và phân quyền.
- Dashboard.
- Quản lý sản phẩm.
- Thêm, sửa, ẩn, hiện và xóa mềm sản phẩm.
- Quản lý hình ảnh.
- Quản lý danh mục.
- Quản lý màu sắc.
- Quản lý kích cỡ.
- Quản lý biến thể.
- Quản lý tồn kho.
- Quản lý đơn hàng.
- Quản lý khách hàng.
- Quản lý cửa hàng.
- Quản lý các nội dung khác nếu có.
- Báo cáo và thống kê.
- Các chức năng quản trị bổ sung trong dự án.

Đối với từng chức năng, phải kiểm tra đủ:

1. Giao diện.
2. Form và validation.
3. API.
4. Database.
5. Phản hồi sau thao tác.
6. Dữ liệu sau khi tải lại trang.

Không để xuất hiện nút bấm giả, nút không có hành động hoặc chức năng chỉ hoạt động trên Frontend nhưng không lưu dữ liệu.

## 3. KHÔI PHỤC VÀ ỔN ĐỊNH HỆ THỐNG HÌNH ẢNH

Ưu tiên hoàn thành lỗi mất ảnh sản phẩm đã được báo cáo.

Kiểm tra và đảm bảo:

- Ảnh sản phẩm trên trang chủ.
- Ảnh danh mục.
- Ảnh tìm kiếm.
- Ảnh chi tiết sản phẩm.
- Ảnh giỏ hàng.
- Ảnh sản phẩm liên quan.
- Ảnh trong Admin.
- Ảnh cập nhật từ Admin sang Customer.

Đối chiếu URL ảnh giữa Database, API và Frontend.

Mọi sản phẩm có ảnh hợp lệ phải hiển thị đúng ảnh tương ứng.

Không sử dụng ảnh ngẫu nhiên để thay thế ảnh sản phẩm. Không đánh dấu PASS khi chỉ hiển thị placeholder.

Nếu phát hiện sản phẩm thực sự thiếu ảnh, ghi rõ mã sản phẩm và tình trạng để xử lý riêng.

Không thay đổi cấu hình Cloudinary.

## 4. GEMINI AI STYLIST

Giữ nguyên hệ thống chatbot tư vấn thời trang đang hoạt động và hoàn thiện các lỗi còn tồn tại.

Kiểm tra:

- Tìm kiếm sản phẩm.
- Xem chi tiết sản phẩm.
- Tư vấn theo giá.
- Tư vấn màu sắc, kích cỡ.
- Kiểm tra tồn kho.
- Phối đồ.
- Thay thế sản phẩm trong set đồ.
- Tư vấn theo ngân sách.
- Lịch sử hội thoại.
- Ghi nhớ ngữ cảnh.
- Tool Calling.
- Hiển thị câu trả lời.
- Hiển thị sản phẩm đề xuất.
- Xử lý câu hỏi ngoài phạm vi.
- Chống Prompt Injection.
- Xử lý lỗi Gemini API.
- Xử lý lỗi Backend Tool.

Yêu cầu:
- Chỉ sử dụng thông tin sản phẩm thực tế.
- Không bịa giá, mã sản phẩm, màu sắc, kích cỡ, tồn kho hoặc chính sách.
- Không tự phối đồ khi khách chỉ muốn tìm một sản phẩm.
- Không đề xuất sản phẩm INACTIVE.
- Khi thiếu dữ liệu, phải thông báo rõ.
- Khi gặp lỗi, phải trả thông báo phù hợp, không tự tạo câu trả lời giả.

## 5. AI BUSINESS INTELLIGENCE

Đây là nhóm chức năng riêng biệt với Gemini AI Stylist.

Kiểm tra hiện trạng và hoàn thiện những chức năng thuộc phạm vi AI quản trị kinh doanh đã được yêu cầu trước đó.

### A. Phân tích doanh thu

- Tổng doanh thu theo ngày, tuần, tháng.
- So sánh các giai đoạn.
- Phân tích số lượng đơn.
- Giá trị đơn hàng trung bình.
- Sản phẩm bán chạy và bán chậm.
- Doanh thu theo danh mục.
- Doanh thu theo cửa hàng nếu có dữ liệu.
- Lợi nhuận nếu có dữ liệu giá vốn.

### B. Kiến nghị nhập hàng

- Tồn kho hiện tại.
- Tốc độ bán.
- Lịch sử tiêu thụ.
- Cảnh báo sắp hết hàng.
- Hàng tồn lâu.
- Số lượng nhập đề xuất.
- Lý do và cơ sở đề xuất.

### C. Phân phối hàng hóa

- So sánh tồn kho giữa cửa hàng.
- Phát hiện thiếu hàng và thừa hàng.
- Đề xuất điều chuyển.
- Đề xuất số lượng và địa điểm nhận hàng.

### D. AI Marketing

- Phân tích tình hình kinh doanh.
- Xác định nhóm khách hàng mục tiêu.
- Đề xuất sản phẩm cần thúc đẩy.
- Big Idea và thông điệp.
- Kênh truyền thông.
- Ngân sách.
- KPI.
- Lịch triển khai.
- Phương pháp đo lường.

### E. CRM

- Customer 360.
- Phân nhóm RFM nếu đủ dữ liệu.
- Khách hàng mới và khách hàng quay lại.
- Tần suất mua.
- Giá trị đơn hàng.
- Phân tích hành vi mua.
- Đề xuất chăm sóc khách hàng.
- Loyalty và Marketing Automation nếu đã nằm trong phạm vi triển khai.

Lưu ý đặc biệt:

- Phải xác định chức năng nào đã tồn tại và chức năng nào chưa được xây dựng.
- Không đánh dấu hoàn thành nếu chỉ có giao diện.
- Phải có API, dữ liệu và logic xử lý thực tế.
- Không bịa số liệu doanh thu, tồn kho hoặc khách hàng.
- Không tạo số liệu dự báo giả.
- Phải phân biệt dữ liệu thực tế, dự báo và giả định.
- Không tự động nhập hàng, điều chuyển hàng hoặc triển khai chiến dịch Marketing.

Nếu thiếu dữ liệu cần thiết, hãy hoàn thiện phần có thể kiểm chứng và ghi rõ giới hạn thay vì tạo kết quả không có căn cứ.

# PHẦN III. KIỂM THỬ TOÀN BỘ FRONTEND VÀ UI/UX

Trực tiếp sử dụng Browser Automation hoặc Playwright để mở và thao tác trên website.

Không chỉ đọc code để kết luận giao diện hoạt động.

## 1. Kiểm tra toàn bộ route

Tự động thu thập danh sách route từ dự án và kiểm tra tất cả trang có thể truy cập.

Phân loại:
- Route công khai.
- Route Customer.
- Route Admin.
- Route yêu cầu đăng nhập.
- Route không tồn tại.
- Route bị lỗi.

Kiểm tra:
- Không có trang trắng.
- Không có lỗi render.
- Không có lỗi điều hướng.
- Không có trang bị chuyển hướng sai.
- Không có nội dung hiển thị sai vai trò.

## 2. Kiểm tra giao diện

Kiểm tra toàn bộ:

- Logo và hình ảnh.
- Màu sắc.
- Font chữ.
- Khoảng cách.
- Căn lề.
- Card.
- Bảng.
- Form.
- Nút.
- Modal.
- Menu.
- Sidebar.
- Biểu đồ.
- Khung chatbot.
- Trạng thái loading.
- Trạng thái lỗi.
- Trạng thái không có dữ liệu.

Sửa lỗi tràn nội dung, chồng lấn, ảnh vỡ, chữ bị cắt, nút bị che và các lỗi hiển thị khác.

## 3. Kiểm tra Responsive

Thử nghiệm tối thiểu:

- 1440 × 900.
- 1366 × 768.
- 768 × 1024.
- 390 × 844.
- 360 × 800.

Kiểm tra Customer và Admin.

Không để:
- Cuộn ngang không cần thiết.
- Form vượt khỏi màn hình.
- Nút không bấm được.
- Bảng dữ liệu mất nội dung quan trọng.
- Chatbot bị che.
- Card sản phẩm biến dạng.
- Nội dung bị cắt.

# PHẦN IV. KIỂM THỬ BACKEND VÀ TOÀN BỘ API

Rà soát toàn bộ endpoint trong dự án.

Với từng API, kiểm tra:

- HTTP Method.
- Endpoint.
- Request.
- Response.
- Authentication.
- Authorization.
- Validation.
- Database.
- Xử lý lỗi.
- Thời gian phản hồi.

Kiểm tra các trường hợp:

- Request hợp lệ.
- Thiếu dữ liệu bắt buộc.
- Dữ liệu sai định dạng.
- ID không tồn tại.
- Token không hợp lệ.
- Token hết hạn.
- Customer truy cập API Admin.
- Truy cập trái phép.
- Request trùng lặp.
- Tồn kho không đủ.
- Database mất kết nối.
- Dịch vụ bên ngoài gặp lỗi.

Đảm bảo Backend không tin tưởng giá hoặc tổng tiền do Frontend tự gửi.

Không để lộ thông tin nội bộ, stack trace hoặc secrets.

# PHẦN V. KIỂM THỬ DATABASE

Kiểm tra toàn bộ Database và Prisma Schema.

Rà soát:

- Bảng dữ liệu.
- Primary Key.
- Foreign Key.
- Quan hệ giữa bảng.
- Index.
- Unique Constraint.
- Null và Default.
- Kiểu dữ liệu.
- Migration.
- Các trường hợp dữ liệu mồ côi.

Kiểm tra tính nhất quán:

- Sản phẩm và danh mục.
- Sản phẩm và hình ảnh.
- Sản phẩm và biến thể.
- Biến thể và tồn kho.
- Khách hàng và đơn hàng.
- Đơn hàng và chi tiết đơn.
- Đơn hàng và thanh toán.
- Giá sản phẩm và tổng tiền đơn hàng.
- Trạng thái đơn và trạng thái thanh toán.

Với từng thao tác CRUD:

1. Thực hiện thao tác trên giao diện.
2. Kiểm tra API.
3. Kiểm tra Database.
4. Tải lại trang.
5. Xác nhận dữ liệu vẫn chính xác.

Kiểm tra transaction và chống tạo đơn trùng, thanh toán callback trùng, cập nhật tồn kho sai.

# PHẦN VI. KIỂM THỬ CÁC LUỒNG E2E QUAN TRỌNG

Bắt buộc tự chạy các luồng hoàn chỉnh sau:

### Luồng 1: Admin tạo sản phẩm

Admin đăng nhập → thêm sản phẩm → thêm ảnh → nhập giá → danh mục → màu → size → tồn kho → lưu → Database nhận dữ liệu → Customer nhìn thấy sản phẩm.

### Luồng 2: Đồng bộ sản phẩm

Admin đổi giá → API cập nhật → Database lưu → Customer thấy giá mới → Gemini tìm thấy giá mới.

### Luồng 3: Ảnh sản phẩm

Admin cập nhật ảnh → Database lưu URL → API trả URL → trang chủ hiển thị ảnh mới → trang chi tiết hiển thị ảnh mới → tải lại trang vẫn còn ảnh.

### Luồng 4: Ẩn sản phẩm

Admin chuyển INACTIVE → sản phẩm không xuất hiện trong danh sách đang bán → không được AI đề xuất như sản phẩm đang bán.

### Luồng 5: Mua hàng

Customer đăng nhập → tìm sản phẩm → xem chi tiết → chọn biến thể → thêm giỏ → checkout → tạo đơn → thanh toán Sandbox → cập nhật trạng thái → xem lịch sử đơn.

### Luồng 6: Admin xử lý đơn hàng

Customer tạo đơn → Admin nhìn thấy → cập nhật trạng thái theo nghiệp vụ → Customer nhìn thấy trạng thái mới.

### Luồng 7: AI Stylist

Khách hỏi sản phẩm → Gemini gọi Tool → Backend truy xuất dữ liệu → Gemini trả lời đúng → hiển thị sản phẩm trên giao diện.

### Luồng 8: AI Business Intelligence

Admin chọn khoảng thời gian → Backend truy xuất dữ liệu → hệ thống tính toán → Gemini phân tích → giao diện hiển thị nhận xét và kiến nghị có căn cứ.

### Luồng 9: Kiểm thử phân quyền

Customer không được truy cập trang hoặc API Admin. Admin có thể sử dụng đúng chức năng theo quyền được cấp.

### Luồng 10: Kiểm thử lỗi

Mô phỏng các tình huống dữ liệu thiếu, API lỗi, Database lỗi hoặc dịch vụ AI không phản hồi. Đảm bảo hệ thống thông báo rõ ràng và không làm mất dữ liệu.

# PHẦN VII. KIỂM THỬ THANH TOÁN VÀ TÍCH HỢP BÊN NGOÀI

Kiểm tra:

- VNPay Sandbox tạo giao dịch.
- Kiểm tra chữ ký.
- Callback.
- Thanh toán thành công.
- Thanh toán thất bại.
- Giao dịch bị hủy.
- Callback lặp lại.
- Trạng thái đơn hàng.
- Tính nhất quán của dữ liệu thanh toán.

Chỉ sử dụng Sandbox, không phát sinh giao dịch thật.

Kiểm tra Cloudinary theo cấu hình hiện tại nhưng không thay đổi bất cứ thông tin cấu hình nào.

# PHẦN VIII. KIỂM THỬ HIỆU NĂNG, BẢO MẬT VÀ ĐỘ ỔN ĐỊNH

Kiểm tra:

- Thời gian tải trang.
- Thời gian phản hồi API.
- Truy vấn Database.
- Phân trang.
- Tìm kiếm.
- Lazy Loading.
- Hình ảnh.
- Gemini response time.
- Bộ nhớ và lỗi runtime.
- Console errors.
- Network errors.
- Backend logs.
- Frontend production build.

Kiểm tra bảo mật:

- Authentication.
- Authorization.
- JWT.
- Password hashing.
- SQL Injection.
- XSS.
- CORS.
- Rate limiting.
- Input validation.
- Upload validation.
- Truy cập dữ liệu người dùng khác.
- Prompt Injection.

Chỉ thực hiện kiểm thử trong môi trường an toàn.

# PHẦN IX. QUY TRÌNH SỬA LỖI VÀ KIỂM THỬ HỒI QUY

Mọi lỗi phải được xử lý theo quy trình:

1. Phát hiện và ghi nhận lỗi.
2. Xác định nguyên nhân gốc.
3. Xác định module bị ảnh hưởng.
4. Sửa đúng vị trí.
5. Chạy lại test chức năng bị lỗi.
6. Chạy regression test các module liên quan.
7. Kiểm tra giao diện thực tế.
8. Đối chiếu dữ liệu Database.
9. Cập nhật báo cáo.

Không sửa một lỗi nhưng làm hỏng chức năng khác.

Không tạo tính năng mới không nằm trong phạm vi dự án chỉ để tăng số lượng chức năng.

Nếu một chức năng chưa có, hãy đánh giá nó có nằm trong yêu cầu đã thống nhất hay không. Nếu có, hoàn thiện. Nếu không, không tự ý mở rộng phạm vi.

# PHẦN X. CHUẨN BỊ TRẠNG THÁI CUỐI CÙNG ĐỂ TÔI TỰ TEST

Đây là yêu cầu bàn giao đặc biệt quan trọng.

Sau khi hoàn thành toàn bộ quá trình:

## 1. Chuẩn bị môi trường

- Frontend khởi động được.
- Backend khởi động được.
- Database test kết nối đúng.
- Gemini hoạt động.
- Cloudinary hoạt động theo cấu hình hiện tại.
- Các API quan trọng hoạt động.
- Không có lỗi runtime nghiêm trọng.

Ưu tiên duy trì server hoạt động sau khi bàn giao.

Nếu môi trường không thể giữ server chạy, phải cung cấp cách khởi động đơn giản nhất bằng file `start.bat` hoặc lệnh chạy chung đã được kiểm tra thực tế.

## 2. Chuẩn bị tài khoản

Kiểm tra và cung cấp:
- Tài khoản Admin test.
- Tài khoản Customer test.
- Mật khẩu tương ứng.
- Trang đăng nhập.
- Quyền của từng tài khoản.

Không được cung cấp mật khẩu chưa xác nhận hoạt động.

## 3. Chuẩn bị dữ liệu test

Giữ lại những dữ liệu cần thiết để tôi tự nghiệm thu:

- Sản phẩm ACTIVE.
- Sản phẩm INACTIVE.
- Sản phẩm nhiều màu.
- Sản phẩm nhiều size.
- Sản phẩm có ảnh hợp lệ.
- Sản phẩm có tồn kho.
- Dữ liệu đơn hàng mẫu nếu cần.
- Dữ liệu CRM/Business Intelligence nếu các chức năng đã triển khai.

Dọn dẹp những dữ liệu thử nghiệm phát sinh không cần thiết trong quá trình tự động kiểm thử.

Chỉ dọn dữ liệu được xác định chắc chắn là dữ liệu do chính đợt kiểm thử tạo ra trong `routine_test_db`.

Không xóa tài khoản test hoặc dữ liệu mẫu cần thiết cho tôi.

## 4. Không thay đổi mã nguồn sau khi nghiệm thu

Sau khi hoàn thành kiểm thử hồi quy và tạo bản bàn giao:

- Không tự tiếp tục refactor.
- Không tự nâng cấp thư viện.
- Không thay đổi Database.
- Không thay đổi cấu hình môi trường.
- Không tự sửa thêm chức năng.
- Giữ nguyên phiên bản đã nghiệm thu để tôi tự kiểm thử.

Nếu sau đó phát hiện lỗi mới, ghi nhận và chờ tôi yêu cầu xử lý.

# PHẦN XI. TẠO TÀI LIỆU BÀN GIAO

Tạo và cập nhật:

1. `docs/FINAL_PROJECT_COMPLETION_REPORT.md`
2. `docs/FINAL_E2E_TEST_REPORT.md`
3. `docs/FINAL_UI_UX_REPORT.md`
4. `docs/FINAL_API_REPORT.md`
5. `docs/FINAL_DATABASE_REPORT.md`
6. `docs/FINAL_AI_REPORT.md`
7. `docs/FINAL_MANUAL_TESTING_GUIDE.md`

Trong tài liệu phải có:

- Danh sách chức năng.
- Trạng thái triển khai.
- Trạng thái kiểm thử.
- Lỗi phát hiện.
- Lỗi đã sửa.
- Lỗi còn tồn tại.
- Ảnh chụp giao diện.
- API và kết quả kiểm thử.
- Bằng chứng Database.
- Bằng chứng E2E.
- Các chức năng chưa triển khai.
- Hướng dẫn tự kiểm thử.

Tất cả tài liệu viết bằng tiếng Việt, dễ hiểu và có thể sử dụng trực tiếp.

# PHẦN XII. TIÊU CHUẨN NGHIỆM THU

Chỉ được báo cáo hoàn thành khi đáp ứng:

- Toàn bộ module đã được rà soát.
- Tất cả chức năng thuộc phạm vi đã được kiểm tra.
- Không còn lỗi CRITICAL.
- Không còn lỗi HIGH chưa xử lý.
- Lỗi MEDIUM và LOW còn lại được liệt kê rõ.
- Các luồng E2E quan trọng hoạt động.
- Ảnh sản phẩm hiển thị đúng.
- UI/UX không có lỗi nghiêm trọng.
- Responsive hoạt động.
- API đúng.
- Database đúng.
- Dữ liệu nhất quán.
- Admin và Customer hoạt động.
- Gemini AI Stylist hoạt động.
- AI Business Intelligence được đánh giá đúng trạng thái.
- Thanh toán Sandbox được kiểm tra.
- Không ảnh hưởng Database thật.
- Có tài khoản và dữ liệu để tôi tự test.
- Có tài liệu hướng dẫn bàn giao.

Không được cố đạt 100% PASS bằng cách bỏ qua những chức năng chưa hoàn thành.

# PHẦN XIII. BÁO CÁO KẾT QUẢ CHO TÔI

Khi hoàn tất, trả lời đúng cấu trúc:

1. Tổng số module đã rà soát.
2. Tổng số chức năng đã kiểm thử.
3. Tổng số route đã kiểm tra.
4. Tổng số API đã kiểm tra.
5. Kết quả kiểm thử UI/UX.
6. Kết quả Responsive.
7. Kết quả Database.
8. Kết quả Admin.
9. Kết quả Customer.
10. Kết quả hình ảnh sản phẩm.
11. Kết quả Gemini AI Stylist.
12. Kết quả AI Business Intelligence.
13. Kết quả VNPay Sandbox.
14. Tổng số lỗi phát hiện.
15. Số lỗi đã sửa.
16. Số lỗi còn tồn tại.
17. Những chức năng chưa triển khai.
18. Những chức năng không thể kiểm thử và lý do.
19. Địa chỉ Frontend và Backend.
20. Tài khoản Admin và Customer test.
21. Cách khởi động hệ thống.
22. Đường dẫn tất cả báo cáo.
23. Các bước tôi cần làm để tự nghiệm thu.

**YÊU CẦU CUỐI CÙNG:**

Hãy tự thực hiện toàn bộ quá trình hoàn thiện, kiểm thử và sửa lỗi trong một đợt làm việc có kiểm soát.

Không dừng lại ở việc phân tích hoặc đưa ra danh sách việc cần làm.

Không tuyên bố hoàn thành khi chưa có bằng chứng thực tế.

Sau khi hoàn thành, hãy để hệ thống ở trạng thái ổn định, giữ nguyên dữ liệu test cần thiết, duy trì môi trường chạy nếu có thể và bàn giao cho tôi tự kiểm thử thủ công trên giao diện.

Tôi muốn đây là phiên bản hoàn thiện cuối cùng trước khi nghiệm thu, không phải một báo cáo tiến độ trung gian.
