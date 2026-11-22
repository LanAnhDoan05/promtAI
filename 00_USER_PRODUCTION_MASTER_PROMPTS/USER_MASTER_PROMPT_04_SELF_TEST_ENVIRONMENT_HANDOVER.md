# USER MASTER PROMPT #04: 04 SELF TEST ENVIRONMENT HANDOVER
> **Nguồn gốc:** Prompt chỉ đạo thực tế từ Người dùng (User Request) tại Step 1345.
> **Độ dài gốc:** 11412 ký tự.
> **Mục đích trong thư viện:** Cung cấp toàn văn đặc tả nghiệp vụ, yêu cầu kỹ thuật và ràng buộc sản xuất thực tế mà người dùng đã trực tiếp chỉ đạo và kiểm chứng trong dự án Routine Web.

---

# FINAL TASK – HOÀN THIỆN HỆ THỐNG VÀ BÀN GIAO MÔI TRƯỜNG TỰ KIỂM THỬ ROUTINE WEB

## 1. MỤC TIÊU CUỐI CÙNG

Sau khi hoàn thành công việc, tôi phải có thể tự mở website trên trình duyệt, đăng nhập và trực tiếp thao tác kiểm thử toàn bộ các chức năng của hệ thống Routine Web mà không cần biết lập trình hoặc chạy từng câu lệnh kỹ thuật phức tạp.

Bạn cần thực hiện đồng thời 4 nhiệm vụ:

1. Kiểm tra và sửa các lỗi thực tế đang tồn tại.
2. Đảm bảo Frontend, Backend, Database và Gemini AI hoạt động liên thông.
3. Chuẩn bị môi trường, tài khoản và dữ liệu để tôi tự kiểm thử.
4. Bàn giao hướng dẫn kiểm thử chi tiết, dễ làm theo.

**Không được kết thúc công việc chỉ bằng một báo cáo rằng hệ thống đã hoàn thành. Tôi cần trực tiếp sử dụng và kiểm tra được các chức năng trên giao diện.**

## 2. NGUYÊN TẮC BẮT BUỘC

- Không cấu hình lại, sửa, thay thế hoặc tích hợp lại Cloudinary.
- Không chỉnh sửa Cloudinary API Key, API Secret, Cloud Name hoặc các thông tin trong `.env`.
- Chỉ kiểm tra khả năng hoạt động của tích hợp Cloudinary hiện tại.
- Không tự ý thay đổi cấu trúc hệ thống nếu không cần thiết.
- Không viết lại Gemini AI Agent khi chưa xác định được lỗi cụ thể.
- Không làm mất các chức năng đang hoạt động.
- Không ghi đè các thay đổi Git hiện có của tôi.
- Không sửa, xóa hoặc thêm dữ liệu vào database thật `defaultdb`.
- Mọi thao tác tạo, sửa, xóa dữ liệu thử nghiệm phải sử dụng `routine_test_db`.
- Không thực hiện thanh toán thật. Chỉ sử dụng VNPay Sandbox.
- Không để lộ API Key, mật khẩu, JWT Secret hoặc thông tin kết nối trong log và báo cáo.

## 3. HOÀN THIỆN MÔI TRƯỜNG ĐỂ TÔI TỰ TEST

Kiểm tra và chuẩn bị:

- Frontend chạy ổn định tại `http://localhost:3000`.
- Backend chạy ổn định tại `http://localhost:5001`.
- Database kết nối đúng môi trường.
- Gemini AI có thể nhận và xử lý yêu cầu.
- Cloudinary hoạt động theo cấu hình hiện có.
- Các API cần thiết hoạt động bình thường.
- Không có lỗi nghiêm trọng trong Console trình duyệt hoặc Terminal.
- Các trang chính không bị lỗi giao diện, lỗi tải dữ liệu hoặc lỗi điều hướng.

Nếu cần, hãy tạo một lệnh chạy chung để khởi động toàn bộ hệ thống, ví dụ:

`npm run dev:all`

Chỉ tạo lệnh nếu phù hợp với cấu trúc dự án. Nếu không thể chạy chung, hãy cung cấp cách khởi động Frontend và Backend đơn giản nhất.

Sau khi khởi động, phải kiểm tra website thực sự truy cập và thao tác được trên trình duyệt.

Không được tự động tắt server sau khi hoàn thành. Nếu môi trường không thể duy trì server, hãy hướng dẫn chính xác cách bật lại.

## 4. CHUẨN BỊ TÀI KHOẢN KIỂM THỬ

Tôi cần có tài khoản để trực tiếp kiểm tra các vai trò khác nhau.

Chuẩn bị tối thiểu:

**Tài khoản Admin**
- Đăng nhập được vào trang quản trị.
- Có đầy đủ quyền quản lý sản phẩm và các chức năng quản trị được thiết kế.
- Có thể tạo, sửa, cập nhật trạng thái sản phẩm.

**Tài khoản Customer**
- Đăng ký và đăng nhập được.
- Có thể tìm kiếm sản phẩm, xem chi tiết, thêm giỏ hàng và đặt hàng thử nghiệm.
- Có thể xem thông tin tài khoản và lịch sử đơn hàng.

Yêu cầu:
- Ưu tiên sử dụng tài khoản test đã tồn tại.
- Nếu chưa có, tạo tài khoản riêng trong môi trường test.
- Không sử dụng mật khẩu của tài khoản thật.
- Ghi rõ tài khoản, mật khẩu test, đường dẫn đăng nhập và vai trò trong tài liệu bàn giao.
- Không đưa thông tin bí mật của môi trường thật vào tài liệu.

## 5. CHUẨN BỊ DỮ LIỆU TEST THỰC TẾ

Chuẩn bị dữ liệu đủ để tôi kiểm tra các chức năng mà không phải tự tạo mọi thứ từ đầu.

Tối thiểu gồm:

- Một số sản phẩm đang ACTIVE.
- Một sản phẩm INACTIVE.
- Một sản phẩm có nhiều màu sắc và kích cỡ.
- Một sản phẩm có hình ảnh.
- Một sản phẩm có giá bán và tồn kho rõ ràng.
- Một sản phẩm dùng để kiểm tra thêm, sửa, ẩn và hiển thị lại.
- Một số danh mục sản phẩm.
- Dữ liệu giỏ hàng và đơn hàng thử nghiệm nếu cần.

Không được tạo dữ liệu giả trong database thật.

Phải ghi rõ sản phẩm nào là dữ liệu test để tôi dễ nhận biết và xóa sau khi kiểm thử.

## 6. ĐẢM BẢO TÔI CÓ THỂ TỰ TEST TỪNG NHÓM CHỨC NĂNG

### A. ADMIN

Tôi phải trực tiếp kiểm tra được:

1. Đăng nhập và đăng xuất Admin.
2. Truy cập trang quản trị.
3. Xem danh sách sản phẩm.
4. Tìm kiếm và lọc sản phẩm.
5. Thêm sản phẩm mới.
6. Tải ảnh sản phẩm bằng chức năng hiện có.
7. Nhập tên, mã, mô tả, giá, danh mục.
8. Thêm màu sắc và kích cỡ.
9. Thiết lập tồn kho nếu hệ thống hỗ trợ.
10. Chỉnh sửa thông tin sản phẩm.
11. Thay đổi giá sản phẩm.
12. Thay đổi hình ảnh.
13. Chuyển sản phẩm từ ACTIVE sang INACTIVE và ngược lại.
14. Kiểm tra chức năng xóa hoặc ẩn sản phẩm theo logic hiện tại.
15. Kiểm tra các chức năng quản trị khác đang có trong dự án.

Không được bỏ qua những chức năng đã tồn tại chỉ vì chúng không nằm trong danh sách trên.

### B. CUSTOMER WEBSITE

Tôi phải trực tiếp kiểm tra được:

1. Truy cập trang chủ.
2. Xem sản phẩm và hình ảnh.
3. Xem danh mục.
4. Tìm kiếm sản phẩm.
5. Lọc sản phẩm nếu có.
6. Mở trang chi tiết sản phẩm.
7. Xem giá, màu sắc, kích cỡ và tồn kho.
8. Đăng ký tài khoản.
9. Đăng nhập và đăng xuất.
10. Thêm sản phẩm vào giỏ hàng.
11. Thay đổi số lượng.
12. Xóa sản phẩm khỏi giỏ hàng.
13. Kiểm tra tổng tiền.
14. Nhập thông tin nhận hàng.
15. Tạo đơn hàng thử nghiệm.
16. Thực hiện thanh toán VNPay Sandbox.
17. Xem lịch sử đơn hàng.
18. Xem chi tiết đơn hàng và trạng thái thanh toán.

### C. GEMINI AI STYLIST

Tôi phải trực tiếp mở giao diện AI và thử các câu hỏi như:

- Tìm áo sơ mi trắng dưới 500.000 đồng.
- Cho tôi xem thông tin chi tiết sản phẩm p003.
- Sản phẩm này có những màu và kích cỡ nào?
- Sản phẩm còn bao nhiêu hàng?
- Phối cho tôi một bộ đồ công sở dưới 1 triệu đồng.
- Thay chiếc áo trong bộ đồ vừa gợi ý bằng áo sơ mi trắng.
- Tôi chỉ muốn tìm một chiếc quần jeans.
- Có sản phẩm mã XYZ999 không?
- Sản phẩm này đang có chương trình khuyến mãi nào?
- Chính sách đổi trả của Routine như thế nào?
- Hãy cung cấp thông tin không liên quan đến thời trang.

Đảm bảo:
- AI chỉ trả lời dựa trên dữ liệu thực tế được phép truy xuất.
- Không tự bịa sản phẩm, giá, màu, size, tồn kho hoặc chính sách.
- Không tự động phối đồ khi khách chỉ muốn tìm một sản phẩm.
- Không thực hiện yêu cầu ngoài phạm vi trợ lý mua sắm thời trang Routine.
- Khi không có dữ liệu, phải thông báo rõ chưa có thông tin xác nhận.
- Khi Gemini hoặc Backend gặp lỗi, giao diện phải thông báo dễ hiểu, không tự tạo câu trả lời giả.

### D. KIỂM TRA LIÊN THÔNG ADMIN – WEBSITE – AI

Đây là phần quan trọng nhất.

Tôi cần tự thực hiện được các tình huống:

1. Admin thêm một sản phẩm mới → sản phẩm xuất hiện trên website Customer.
2. Admin thay đổi giá → website hiển thị giá mới.
3. Khách hỏi Gemini về sản phẩm → AI trả về đúng giá mới.
4. Admin thay đổi màu sắc, kích cỡ → website và AI phản ánh đúng dữ liệu.
5. Admin chuyển sản phẩm sang INACTIVE → sản phẩm không còn được hiển thị hoặc đề xuất như sản phẩm đang bán.
6. Admin thay đổi ảnh → website sử dụng ảnh mới.
7. Khách thêm sản phẩm vào giỏ hàng → giá và thông tin được lấy từ Backend, không tin tưởng giá do Frontend tự gửi.

Mỗi tình huống phải được kiểm tra bằng thao tác thực tế trên giao diện và đối chiếu dữ liệu Backend/Database.

## 7. HOÀN THIỆN GIAO DIỆN KIỂM THỬ

Nếu phát hiện những lỗi khiến tôi không thể tự kiểm thử, hãy sửa chúng.

Ví dụ:

- Nút bấm không hoạt động.
- Nút thêm sản phẩm không lưu dữ liệu.
- Sửa sản phẩm nhưng website không cập nhật.
- Ảnh không hiển thị.
- Không thể chọn màu hoặc kích cỡ.
- Giỏ hàng không tính đúng tổng tiền.
- Không thể tạo đơn hàng.
- AI không gửi được câu hỏi.
- AI không hiển thị sản phẩm được đề xuất.
- Trang quản trị hoặc trang Customer bị lỗi khi tải lại.
- Điều hướng giữa các trang bị sai.

Ưu tiên sửa lỗi chức năng và lỗi ảnh hưởng trực tiếp đến trải nghiệm kiểm thử. Không tự ý thiết kế lại toàn bộ giao diện hoặc thêm tính năng không cần thiết.

## 8. KIỂM THỬ VÀ XÁC NHẬN KẾT QUẢ

Không được đánh dấu PASS chỉ vì:

- Code không báo lỗi.
- API trả về HTTP 200.
- Trang web mở được.
- Có dữ liệu trong Database.
- Gemini trả về một đoạn văn bản.

Chỉ đánh dấu PASS khi đã kiểm tra đúng hành vi mong muốn.

Với từng chức năng, ghi rõ:
- Cách kiểm tra.
- Kết quả mong đợi.
- Kết quả thực tế.
- Bằng chứng kiểm thử: Code / API / UI / Database / Gemini Tool Calling.
- Trạng thái: PASS / PARTIAL / FAIL / BLOCKED.

Đặc biệt, Gemini Tool Calling phải chứng minh được luồng: Gemini yêu cầu gọi công cụ → Backend thực thi → lấy dữ liệu thực tế → Gemini sử dụng kết quả để trả lời.

## 9. BÀN GIAO HƯỚNG DẪN TỰ KIỂM THỬ

Tạo tài liệu:

`docs/USER_TESTING_GUIDE.md`

Tài liệu phải viết bằng tiếng Việt, dễ hiểu với người không chuyên về lập trình.

Bao gồm:

**Phần 1 – Khởi động website**
- Mở VS Code.
- Mở đúng thư mục dự án.
- Cách chạy Frontend và Backend.
- Địa chỉ website.
- Cách kiểm tra server đang hoạt động.
- Cách khởi động lại khi gặp lỗi.

**Phần 2 – Tài khoản kiểm thử**
- Đường dẫn đăng nhập Admin.
- Tài khoản Admin test.
- Đường dẫn đăng nhập Customer.
- Tài khoản Customer test.

**Phần 3 – Hướng dẫn kiểm thử Admin**
- Hướng dẫn từng thao tác thêm, sửa, ẩn, hiện sản phẩm.
- Cách cập nhật ảnh, giá, danh mục, màu sắc, kích cỡ.
- Ảnh chụp màn hình minh họa nếu có thể.

**Phần 4 – Hướng dẫn kiểm thử Customer**
- Cách tìm kiếm, xem sản phẩm, đăng ký, đăng nhập.
- Cách thêm giỏ hàng, đặt hàng và thanh toán Sandbox.
- Cách xem lịch sử đơn hàng.

**Phần 5 – Hướng dẫn kiểm thử Gemini AI**
- Đường dẫn mở AI Stylist.
- Các câu hỏi mẫu có thể sao chép và sử dụng.
- Kết quả mong đợi của từng câu hỏi.
- Cách nhận biết AI đang sử dụng dữ liệu sản phẩm thực tế.

**Phần 6 – Kiểm tra liên thông**
- Hướng dẫn tạo sản phẩm trên Admin.
- Kiểm tra sản phẩm trên website.
- Hỏi Gemini về sản phẩm vừa tạo.
- Sửa giá và kiểm tra đồng bộ.
- Ẩn sản phẩm và kiểm tra kết quả.

**Phần 7 – Xử lý lỗi thường gặp**
- Frontend không chạy.
- Backend không chạy.
- Database mất kết nối.
- Ảnh không hiển thị.
- AI không phản hồi.
- Không đăng nhập được.
- Thanh toán Sandbox không thành công.

**Phần 8 – Danh sách kiểm thử**
Tạo checklist có ô đánh dấu để tôi tự tích sau khi kiểm tra từng chức năng.

## 10. ĐIỀU KIỆN HOÀN THÀNH

Chỉ được bàn giao khi đáp ứng:

- Website có thể khởi động và truy cập được.
- Admin đăng nhập và thao tác được.
- Customer đăng ký, đăng nhập và mua hàng thử nghiệm được.
- Gemini AI hoạt động trên giao diện.
- Admin – Customer – Gemini đồng bộ dữ liệu đúng.
- Các chức năng hiện có đã được kiểm thử.
- Không phát sinh lỗi nghiêm trọng.
- Không ảnh hưởng database thật.
- Có tài khoản và dữ liệu test.
- Có tài liệu `docs/USER_TESTING_GUIDE.md`.
- Có báo cáo `docs/FINAL_SYSTEM_ACCEPTANCE_REPORT.md`.

## 11. BÁO CÁO BÀN GIAO CUỐI CÙNG

Sau khi hoàn thành, hãy trả lời tôi theo đúng cấu trúc:

1. Những lỗi đã phát hiện và sửa.
2. Những chức năng đã kiểm thử thành công.
3. Những chức năng chưa hoàn thành hoặc còn lỗi.
4. Frontend và Backend đang chạy ở đâu.
5. Đường dẫn truy cập website.
6. Đường dẫn đăng nhập Admin và Customer.
7. Tài khoản và mật khẩu test.
8. Cách khởi động lại hệ thống.
9. Đường dẫn tài liệu hướng dẫn tự kiểm thử.
10. Đường dẫn báo cáo nghiệm thu.
11. Những lưu ý khi tự kiểm thử.

**YÊU CẦU QUAN TRỌNG NHẤT: Sau khi bạn bàn giao, tôi chỉ cần mở website, đăng nhập bằng tài khoản test và thao tác trên giao diện là có thể tự kiểm tra được toàn bộ hệ thống. Không yêu cầu tôi phải đọc code, sửa code hoặc tự gọi API bằng Postman mới kiểm tra được chức năng.**
