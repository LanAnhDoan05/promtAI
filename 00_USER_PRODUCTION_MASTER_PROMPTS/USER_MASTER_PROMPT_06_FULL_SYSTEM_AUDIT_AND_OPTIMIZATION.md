# USER MASTER PROMPT #06: 06 FULL SYSTEM AUDIT AND OPTIMIZATION
> **Nguồn gốc:** Prompt chỉ đạo thực tế từ Người dùng (User Request) tại Step 1674.
> **Độ dài gốc:** 17171 ký tự.
> **Mục đích trong thư viện:** Cung cấp toàn văn đặc tả nghiệp vụ, yêu cầu kỹ thuật và ràng buộc sản xuất thực tế mà người dùng đã trực tiếp chỉ đạo và kiểm chứng trong dự án Routine Web.

---

# MASTER PROMPT – FULL SYSTEM AUDIT, TESTING & OPTIMIZATION – ROUTINE WEB

**Dự án:** Routine Web E-commerce  
**Phạm vi:** Toàn bộ hệ thống Admin + Customer Storefront + Gemini AI Stylist + AI Business Intelligence + Backend API + Database.

## I. MỤC TIÊU TỔNG THỂ

Tôi yêu cầu bạn thực hiện một đợt kiểm thử và nghiệm thu toàn diện trên TOÀN BỘ dự án Routine Web.

Đây không phải nhiệm vụ chỉ kiểm tra các chức năng hoặc chạy lại những bài test có sẵn.

Bạn phải tự kiểm tra hệ thống đang chạy, trực tiếp thao tác trên trình duyệt, kiểm tra giao diện, trải nghiệm người dùng, luồng API, dữ liệu Database, quyền truy cập, khả năng đồng bộ và hoạt động của AI.

Sau khi phát hiện lỗi, hãy sửa lỗi, chạy lại các bài kiểm thử liên quan và kiểm tra hồi quy để đảm bảo việc sửa lỗi không làm hỏng những chức năng khác.

**Mục tiêu cuối cùng:** Website phải hoạt động ổn định, hiển thị chính xác, dữ liệu nhất quán, API hoạt động đúng, Database được sử dụng an toàn và toàn bộ luồng nghiệp vụ có thể thực hiện từ đầu đến cuối.

Không được đánh giá dự án hoàn thành chỉ dựa trên việc code không báo lỗi hoặc API trả về HTTP 200.

---

## II. NGUYÊN TẮC BẮT BUỘC TRƯỚC KHI KIỂM THỬ

1. Đọc cấu trúc toàn bộ dự án và xác định đầy đủ các module đang tồn tại.
2. Kiểm tra `git status` và bảo toàn mọi thay đổi chưa commit.
3. Kiểm tra cấu hình môi trường hiện tại, xác định chính xác Database mà Backend đang kết nối.
4. Phân biệt rõ môi trường test và môi trường thật.
5. Toàn bộ thao tác ghi, sửa, xóa, tạo đơn hàng và dữ liệu thử nghiệm phải sử dụng `routine_test_db`.
6. Tuyệt đối không ghi, sửa, xóa hoặc chạy migration phá hủy trên `defaultdb`.
7. Không chạy `DROP DATABASE`, `TRUNCATE`, `prisma migrate reset` hoặc lệnh có nguy cơ làm mất dữ liệu.
8. Không để lộ API Key, mật khẩu, JWT Secret hoặc thông tin kết nối Database.
9. Không thay đổi hoặc cấu hình lại Cloudinary. Chỉ kiểm tra tích hợp hiện có.
10. Không viết lại các module đang hoạt động nếu chưa có bằng chứng lỗi.
11. Không tự ý thay đổi giao diện, cấu trúc dữ liệu hoặc nghiệp vụ đã được triển khai đúng.
12. Không sử dụng dữ liệu giả để đánh dấu hệ thống đã kiểm thử thành công.

Nếu môi trường test không thể khởi động hoặc thiếu dữ liệu cần thiết, phải báo rõ nguyên nhân, không được tự nhận PASS.

---

# III. KIỂM THỬ TOÀN DIỆN GIAO DIỆN – UI/UX

Đây là phần bắt buộc phải trực tiếp mở trình duyệt và thao tác.

Không chỉ kiểm tra trang có mở được hay không mà phải kiểm tra toàn bộ thành phần hiển thị và khả năng sử dụng.

## 1. Kiểm tra toàn bộ trang

Tự động rà soát các route trong dự án và phân loại:

- Trang chủ.
- Trang danh mục.
- Trang tìm kiếm.
- Trang chi tiết sản phẩm.
- Trang đăng ký, đăng nhập.
- Trang giỏ hàng.
- Trang thanh toán.
- Trang tài khoản khách hàng.
- Trang lịch sử đơn hàng.
- Trang AI Stylist.
- Các trang Admin.
- Trang Dashboard.
- Trang quản lý sản phẩm.
- Trang quản lý danh mục.
- Các trang quản trị khác.
- Khu vực AI Business Intelligence nếu đã triển khai.

Không bỏ qua các route hiện có trong source code.

## 2. Kiểm tra hiển thị

Trên từng trang, kiểm tra:

- Logo, hình ảnh và nội dung.
- Font chữ, kích thước chữ, màu sắc.
- Khoảng cách, căn lề và bố cục.
- Header, Footer, Sidebar, Navigation.
- Menu và các thành phần điều hướng.
- Card sản phẩm.
- Hình ảnh sản phẩm và tỷ lệ khung hình.
- Giá, trạng thái và thông tin sản phẩm.
- Nút bấm và biểu tượng.
- Form nhập liệu.
- Modal, dropdown, tab và bộ lọc.
- Bảng dữ liệu.
- Biểu đồ và thông tin Dashboard.
- Trạng thái loading.
- Trạng thái không có dữ liệu.
- Thông báo thành công và thất bại.
- Thông báo lỗi validation.

Phát hiện và sửa:
- Hình ảnh bị vỡ.
- Ảnh không tải được.
- Nội dung tràn khỏi khung.
- Thành phần bị chồng lên nhau.
- Nút bị che hoặc không thể bấm.
- Chữ bị cắt.
- Card sản phẩm không đồng đều.
- Biểu đồ không hiển thị đúng.
- Dữ liệu bị hiển thị sai định dạng.
- Trang trắng hoặc lỗi render.
- Giao diện thiếu nhất quán giữa các trang.

## 3. Responsive

Kiểm tra tối thiểu ở các kích thước:

- Desktop: 1440 × 900.
- Laptop: 1366 × 768.
- Tablet: 768 × 1024.
- Mobile: 390 × 844.
- Mobile nhỏ: 360 × 800.

Kiểm tra:
- Menu trên thiết bị di động.
- Bố cục sản phẩm.
- Giỏ hàng và thanh toán.
- Bảng Admin.
- Dashboard và biểu đồ.
- Khung chat AI.
- Các form và nút thao tác.

Không để xuất hiện cuộn ngang không cần thiết, nội dung bị mất hoặc nút không thể thao tác.

## 4. Trải nghiệm người dùng

Kiểm tra các luồng thao tác:

- Người dùng có biết phải bấm vào đâu không?
- Các nút có phản hồi rõ ràng không?
- Sau khi lưu dữ liệu, có thông báo xác nhận không?
- Khi gặp lỗi, người dùng có hiểu nguyên nhân không?
- Khi tải dữ liệu, có trạng thái loading không?
- Khi danh sách trống, có hướng dẫn phù hợp không?
- Khi quay lại hoặc tải lại trang, trạng thái có hợp lý không?

Không chỉ kiểm tra hình thức mà phải kiểm tra khả năng sử dụng thực tế.

---

# IV. KIỂM THỬ TOÀN BỘ CHỨC NĂNG VÀ LUỒNG NGHIỆP VỤ

## 1. Customer Storefront

Kiểm thử:

- Trang chủ và sản phẩm hiển thị.
- Danh mục và phân trang.
- Tìm kiếm theo tên, mã sản phẩm và slug.
- Bộ lọc, sắp xếp.
- Trang chi tiết sản phẩm.
- Hình ảnh, màu sắc, kích cỡ, giá và tồn kho.
- Đăng ký.
- Đăng nhập.
- Đăng xuất.
- Quản lý thông tin tài khoản.
- Giỏ hàng.
- Thay đổi số lượng.
- Xóa sản phẩm.
- Tính tổng tiền.
- Thông tin nhận hàng.
- Tạo đơn hàng.
- Thanh toán.
- Lịch sử đơn hàng.
- Chi tiết đơn hàng.
- Trạng thái đơn hàng và thanh toán.

Phải kiểm tra cả trường hợp dữ liệu hợp lệ và không hợp lệ.

## 2. Admin

Kiểm thử toàn bộ chức năng đang có:

- Đăng nhập và phân quyền.
- Dashboard.
- Quản lý sản phẩm.
- Thêm sản phẩm.
- Sửa sản phẩm.
- Xóa mềm.
- Ẩn và hiện sản phẩm.
- Danh mục.
- Hình ảnh.
- Màu sắc.
- Kích cỡ.
- Biến thể.
- Tồn kho.
- Quản lý đơn hàng.
- Quản lý khách hàng.
- Quản lý cửa hàng.
- Báo cáo.
- Các module quản trị khác có trong dự án.

Kiểm tra mỗi nút bấm và hành động thực tế. Không chấp nhận giao diện có chức năng nhưng không kết nối API.

## 3. Kiểm thử liên thông

Tự thực hiện các luồng hoàn chỉnh:

**Luồng 1: Thêm sản phẩm**

Admin tạo sản phẩm → Backend nhận dữ liệu → Database lưu → Customer nhìn thấy sản phẩm → Gemini tìm kiếm được sản phẩm.

**Luồng 2: Cập nhật sản phẩm**

Admin thay đổi giá, ảnh, màu và kích cỡ → Database cập nhật → API trả dữ liệu mới → Customer hiển thị dữ liệu mới → Gemini trả lời theo dữ liệu mới.

**Luồng 3: Ẩn sản phẩm**

Admin chuyển INACTIVE → Customer không còn nhìn thấy sản phẩm như sản phẩm đang bán → Gemini không đề xuất sản phẩm đó.

**Luồng 4: Mua hàng**

Customer tìm sản phẩm → xem chi tiết → thêm giỏ hàng → checkout → Backend tính toán → tạo đơn → Database lưu → thanh toán Sandbox → cập nhật trạng thái đơn.

**Luồng 5: Quản lý đơn hàng**

Customer tạo đơn → Admin nhìn thấy đơn → Admin cập nhật trạng thái theo nghiệp vụ hiện có → Customer xem được trạng thái mới.

**Luồng 6: Đồng bộ dữ liệu**

Thực hiện cập nhật dữ liệu ở từng module và kiểm tra các module liên quan có nhận dữ liệu mới chính xác không.

---

# V. KIỂM THỬ TOÀN BỘ BACKEND VÀ API

Không chỉ chạy API smoke test. Hãy lập danh sách toàn bộ endpoint đang tồn tại trong Backend.

## 1. Rà soát API

Với từng API, ghi rõ:

- HTTP Method.
- Endpoint.
- Chức năng.
- Request parameters.
- Request body.
- Authentication.
- Authorization.
- Database liên quan.
- Response mong đợi.
- Mã trạng thái phù hợp.

Kiểm tra:
- API GET.
- API POST.
- API PUT/PATCH.
- API DELETE.
- API upload.
- API xác thực.
- API Admin.
- API Customer.
- API AI.
- API Dashboard và báo cáo.
- API thanh toán.
- API đơn hàng.

## 2. Kiểm tra các tình huống

- Request hợp lệ.
- Thiếu trường bắt buộc.
- Sai kiểu dữ liệu.
- Dữ liệu null.
- Dữ liệu rỗng.
- ID không tồn tại.
- Sản phẩm không tồn tại.
- Sản phẩm INACTIVE.
- Giá không hợp lệ.
- Số lượng âm.
- Tồn kho không đủ.
- Token hết hạn.
- Không có token.
- Customer gọi API Admin.
- User không có quyền truy cập.
- Request trùng lặp.
- Nhiều request đồng thời.
- Database mất kết nối.
- API phụ thuộc bên ngoài gặp lỗi.

## 3. Kiểm tra tính chính xác

- Backend phải validate dữ liệu.
- Không tin tưởng giá và tổng tiền do Frontend gửi.
- Không cho phép Customer tự nâng quyền.
- Không để lộ thông tin nội bộ.
- Không trả stack trace hoặc thông tin nhạy cảm cho người dùng.
- Không để một request lỗi làm sập toàn bộ server.
- Không để dữ liệu bị tạo trùng khi người dùng gửi lại request.

## 4. Hiệu năng API

Đo:
- Thời gian phản hồi.
- API có truy vấn thừa không.
- API có tải quá nhiều dữ liệu không.
- Phân trang có hoạt động đúng không.
- Các endpoint có truy vấn N+1 không.
- Các request có bị timeout không.

Ghi lại số liệu thực tế, không tự tạo kết quả.

---

# VI. KIỂM THỬ DATABASE VÀ TÍNH TOÀN VẸN DỮ LIỆU

Đây là phần đặc biệt quan trọng.

## 1. Rà soát cấu trúc Database

Kiểm tra:

- Các bảng.
- Các trường dữ liệu.
- Primary Key.
- Foreign Key.
- Quan hệ giữa các bảng.
- Unique Constraint.
- Index.
- Kiểu dữ liệu.
- Giá trị mặc định.
- Nullable.
- Migration.
- Prisma Schema.

Đối chiếu cấu trúc thực tế với logic trong Backend.

## 2. Kiểm tra dữ liệu

Kiểm tra:
- Sản phẩm có danh mục hợp lệ.
- Giá sản phẩm hợp lệ.
- Biến thể liên kết đúng sản phẩm.
- Ảnh liên kết đúng sản phẩm.
- Đơn hàng liên kết đúng khách hàng.
- Chi tiết đơn hàng có sản phẩm hợp lệ.
- Tổng tiền đơn hàng nhất quán.
- Tồn kho không bị âm.
- Không xuất hiện dữ liệu mồ côi.
- Không tạo bản ghi trùng ngoài dự kiến.
- Trạng thái đơn hàng hợp lệ.
- Trạng thái thanh toán nhất quán.

## 3. Kiểm tra CRUD

Với từng module có CRUD, thực hiện:

- Create.
- Read.
- Update.
- Delete hoặc Soft Delete.

Sau mỗi thao tác:
1. Kiểm tra response API.
2. Kiểm tra dữ liệu Database.
3. Kiểm tra giao diện.
4. Tải lại trang.
5. Xác nhận dữ liệu vẫn chính xác.

## 4. Kiểm tra transaction và đồng thời

Kiểm tra các tình huống:

- Hai khách cùng mua sản phẩm có tồn kho thấp.
- Khách gửi nhiều request tạo đơn.
- Thanh toán callback lặp lại.
- Cập nhật sản phẩm trong lúc khách đang mua.
- Tạo đơn thất bại giữa quy trình.
- Cập nhật tồn kho thất bại.

Đảm bảo transaction, tính nhất quán và chống xử lý trùng phù hợp với thiết kế hiện tại.

## 5. Database Isolation

Bắt buộc xác nhận:

- Backend hiện kết nối `routine_test_db`.
- Các bài kiểm thử ghi dữ liệu không chạy trên `defaultdb`.
- Không có lệnh hoặc script tự động ghi vào Database thật.
- Không thay đổi dữ liệu ban đầu trong `defaultdb`.

Lưu lại thông tin xác nhận môi trường nhưng tuyệt đối không ghi mật khẩu hoặc chuỗi kết nối đầy đủ vào báo cáo.

---

# VII. KIỂM THỬ GEMINI AI VÀ AI BUSINESS INTELLIGENCE

Phải phân biệt rõ hai hệ thống AI.

## A. Gemini AI Stylist

Kiểm tra:

- Tìm kiếm sản phẩm.
- Chi tiết sản phẩm.
- Màu sắc và kích cỡ.
- Tồn kho.
- Phối đồ.
- Thay thế sản phẩm.
- Tư vấn theo ngân sách.
- Lịch sử hội thoại.
- Khả năng sử dụng tool.
- Chống Prompt Injection.
- Xử lý câu hỏi ngoài phạm vi.
- Xử lý lỗi API Gemini.
- Không bịa dữ liệu.

Phải chứng minh được Tool Calling thực sự đi qua Backend và dữ liệu Database.

## B. AI Business Intelligence

Kiểm tra hiện trạng và mức độ triển khai của:

1. Phân tích doanh thu.
2. Phân tích đơn hàng.
3. Phân tích sản phẩm bán chạy và bán chậm.
4. Dự báo nhu cầu.
5. Kiến nghị nhập hàng.
6. Phân phối hàng giữa cửa hàng.
7. Phân tích khách hàng.
8. Customer 360.
9. RFM.
10. Kiến nghị Marketing.
11. Kế hoạch chiến dịch.
12. KPI và ngân sách.

Nếu chưa triển khai, phải đánh dấu NOT IMPLEMENTED hoặc PARTIAL. Không được tạo báo cáo giả rằng những chức năng này đã hoàn thành.

Với các chức năng đã có, kiểm tra dữ liệu đầu vào, công thức tính toán, API, giao diện và kết quả AI.

AI phải phân biệt:
- Số liệu thực tế.
- Số liệu dự báo.
- Giả định.
- Kiến nghị.

Không tự động thay đổi tồn kho, nhập hàng hoặc triển khai chiến dịch Marketing.

---

# VIII. KIỂM THỬ BẢO MẬT

Rà soát các vấn đề:

- Authentication.
- Authorization.
- JWT.
- Password Hashing.
- SQL Injection.
- XSS.
- CSRF nếu có liên quan.
- CORS.
- Rate Limiting.
- Input Validation.
- Upload File Validation.
- Quyền truy cập dữ liệu.
- Lộ thông tin qua API.
- Lộ secrets trong code hoặc log.
- Prompt Injection.
- Truy cập trái phép vào API Admin.
- Truy cập dữ liệu đơn hàng của người khác.

Chỉ kiểm thử trong môi trường test, không thực hiện tấn công phá hoại.

---

# IX. KIỂM THỬ HIỆU NĂNG VÀ ĐỘ ỔN ĐỊNH

Kiểm tra:

- Thời gian tải trang.
- Thời gian tải danh sách sản phẩm.
- Thời gian tìm kiếm.
- Thời gian mở chi tiết sản phẩm.
- Thời gian phản hồi AI.
- Khả năng tải ảnh.
- Khả năng xử lý nhiều request.
- Khả năng phục hồi khi API lỗi.
- Memory leak nếu có dấu hiệu.
- Console errors.
- Network errors.
- Backend logs.
- Frontend build.
- Production build.

Thực hiện kiểm thử tải ở mức phù hợp với môi trường test. Không tạo tải quá mức lên Database thật hoặc dịch vụ bên ngoài.

---

# X. TỰ ĐỘNG HÓA KIỂM THỬ VÀ SỬA LỖI

Bạn cần sử dụng các công cụ phù hợp với dự án:

- Browser automation/Playwright để thao tác giao diện.
- API testing để kiểm tra Backend.
- Prisma/SQL để kiểm tra Database.
- Unit test và Integration test.
- Console và Network inspection.
- Screenshot để lưu bằng chứng giao diện.

Nếu đã có test framework, ưu tiên sử dụng framework hiện tại.

Không chỉ chạy test có sẵn. Phải xây dựng thêm test cho những luồng quan trọng còn thiếu.

Với từng lỗi:
1. Ghi nhận lỗi.
2. Xác định nguyên nhân.
3. Sửa đúng module.
4. Chạy lại test lỗi.
5. Chạy regression test cho các chức năng liên quan.
6. Chụp bằng chứng sau khi sửa.

Không sửa hàng loạt hoặc refactor toàn dự án không cần thiết.

---

# XI. TIÊU CHUẨN ĐÁNH GIÁ

Sử dụng các trạng thái:

- PASS: Đã kiểm thử và có bằng chứng đạt.
- PARTIAL: Đã triển khai nhưng chưa hoàn chỉnh.
- FAIL: Đã kiểm thử và không đạt.
- BLOCKED: Không thể kiểm thử do thiếu điều kiện.
- NOT IMPLEMENTED: Chưa có chức năng.

Phân loại mức độ lỗi:

- CRITICAL: Ảnh hưởng bảo mật, dữ liệu hoặc toàn bộ hệ thống.
- HIGH: Luồng nghiệp vụ quan trọng không hoạt động.
- MEDIUM: Chức năng có lỗi nhưng có cách sử dụng thay thế.
- LOW: Lỗi giao diện hoặc trải nghiệm nhỏ.

Không được:
- Đánh dấu PASS chỉ dựa trên code review.
- Đánh dấu PASS chỉ dựa trên HTTP 200.
- Tự tạo kết quả kiểm thử.
- Bỏ qua những chức năng chưa triển khai.
- Che giấu lỗi để đạt tỷ lệ 100%.

---

# XII. TÀI LIỆU BÀN GIAO

Tạo các tài liệu:

1. `docs/FULL_SYSTEM_AUDIT_REPORT.md`
   - Tổng quan hệ thống.
   - Phạm vi đã kiểm tra.
   - Danh sách module.
   - Kết quả từng nhóm test.
   - Lỗi phát hiện và sửa.
   - Các vấn đề còn tồn đọng.

2. `docs/UI_UX_AUDIT_REPORT.md`
   - Danh sách route.
   - Kết quả kiểm tra hiển thị.
   - Responsive.
   - Ảnh chụp trước và sau sửa.
   - Các vấn đề UI/UX.

3. `docs/API_AUDIT_REPORT.md`
   - Danh sách API.
   - Kết quả từng endpoint.
   - Validation.
   - Authorization.
   - Hiệu năng.

4. `docs/DATABASE_AUDIT_REPORT.md`
   - Cấu trúc bảng.
   - Quan hệ dữ liệu.
   - CRUD.
   - Tính toàn vẹn.
   - Transaction.
   - Database isolation.

5. `docs/AI_AUDIT_REPORT.md`
   - Gemini AI Stylist.
   - AI Business Intelligence.
   - Tool Calling.
   - Độ chính xác.
   - Giới hạn dữ liệu.
   - Kết quả kiểm thử.

6. `docs/BUG_FIX_REPORT.md`
   - Danh sách lỗi.
   - Nguyên nhân.
   - Cách sửa.
   - Kết quả kiểm thử lại.

7. `docs/FINAL_ACCEPTANCE_CHECKLIST.md`
   - Checklist nghiệm thu toàn bộ dự án.

---

# XIII. ĐIỀU KIỆN BÀN GIAO CUỐI CÙNG

Sau khi hoàn thành, hãy đảm bảo:

1. Website có thể chạy và thao tác bình thường.
2. Toàn bộ route quan trọng hoạt động.
3. Giao diện hiển thị đúng trên Desktop, Tablet và Mobile.
4. Các nút và form thực hiện đúng chức năng.
5. Frontend và Backend liên thông.
6. API hoạt động đúng.
7. Database được sử dụng đúng và an toàn.
8. Dữ liệu không bị sai lệch giữa API, Database và giao diện.
9. Các luồng Admin và Customer hoạt động đầu cuối.
10. Gemini AI Stylist hoạt động đúng.
11. AI Business Intelligence được đánh giá đúng trạng thái thực tế.
12. Không còn lỗi CRITICAL và HIGH chưa xử lý.
13. Những lỗi MEDIUM và LOW còn tồn tại phải được liệt kê rõ.
14. Không làm ảnh hưởng dữ liệu thật.
15. Người dùng có thể tự khởi động và kiểm thử hệ thống.

## XIV. BÁO CÁO TRỰC TIẾP CHO TÔI

Sau khi hoàn thành, hãy trả lời:

1. Tổng số trang đã kiểm thử.
2. Tổng số thành phần giao diện đã kiểm tra.
3. Kết quả Responsive.
4. Tổng số API đã kiểm thử.
5. Kết quả Database.
6. Tổng số luồng nghiệp vụ đã kiểm thử.
7. Kết quả Gemini AI Stylist.
8. Kết quả AI Business Intelligence.
9. Số lỗi phát hiện.
10. Số lỗi đã sửa.
11. Số lỗi còn tồn tại.
12. Những chức năng chưa được triển khai.
13. Những nội dung không thể kiểm thử và nguyên nhân.
14. Đường dẫn các báo cáo và bằng chứng.
15. Hướng dẫn tôi tự kiểm tra sau khi bàn giao.

**YÊU CẦU CUỐI CÙNG:**

Hãy thực hiện công việc thực tế trên dự án, không chỉ đưa ra kế hoạch hoặc danh sách đề xuất.

Ưu tiên kiểm thử toàn diện, phát hiện lỗi thật, sửa lỗi có kiểm soát và chứng minh kết quả bằng bằng chứng thực tế.

Không tự ý xây thêm tính năng ngoài phạm vi khi chưa được yêu cầu. Không hy sinh tính ổn định của hệ thống để đạt số lượng chức năng hoặc tỷ lệ PASS cao.

Chỉ tuyên bố hoàn thành khi đã có kết quả kiểm thử thực tế và tài liệu bàn giao đầy đủ.
