# USER MASTER PROMPT #21: 21 ADDRESS VALIDATION AI CONSULTATION
> **Nguồn gốc:** Prompt chỉ đạo thực tế từ Người dùng (User Request) tại Step 8912.
> **Độ dài gốc:** 17530 ký tự.
> **Mục đích trong thư viện:** Cung cấp toàn văn đặc tả nghiệp vụ, yêu cầu kỹ thuật và ràng buộc sản xuất thực tế mà người dùng đã trực tiếp chỉ đạo và kiểm chứng trong dự án Routine Web.

---

# MASTER PROMPT – ROUTINE WEB: ADDRESS VALIDATION + UI/UX REFINEMENT + AI STYLIST CONSULTATION + END-TO-END ACCEPTANCE

Bạn đang tiếp tục phát triển dự án `routine-web-demo` hiện có.

Đây là một hệ thống thương mại điện tử thời trang Routine với:
- Frontend: Next.js 16, React 19.
- Backend: Node.js, Express REST API.
- Database: MySQL, Prisma ORM.
- AI: Google Gemini tích hợp AI Stylist.
- Hai giao diện chính: Customer Storefront và Admin Panel.

## I. NGUYÊN TẮC BẮT BUỘC

1. Không xây dựng lại dự án từ đầu.
2. Không tự ý xóa, thay thế hoặc viết lại các chức năng đang hoạt động tốt.
3. Không tạo database, bảng dữ liệu hoặc API trùng lặp khi hệ thống đã có thành phần tương ứng.
4. Kiểm tra kiến trúc, database schema, API, frontend, backend và các luồng nghiệp vụ hiện tại trước khi sửa.
5. Mọi chức năng phải sử dụng dữ liệu thật từ MySQL, không sử dụng dữ liệu giả, mock data hoặc hardcode để tạo cảm giác hoạt động.
6. Không làm hỏng các chức năng sản phẩm, giỏ hàng, đơn hàng, thanh toán, tài khoản, quản lý khách hàng và AI Stylist hiện có.
7. Mọi thay đổi database phải có migration an toàn, có phương án bảo toàn dữ liệu.
8. Không ghi đè dữ liệu thật, không xóa dữ liệu người dùng và đơn hàng.
9. Không đưa API Key, mật khẩu hoặc thông tin bí mật vào mã nguồn, log hay báo cáo.
10. Phải trực tiếp thực thi, kiểm thử và sửa lỗi. Không chỉ đưa ra kế hoạch hoặc hướng dẫn.

---

# PHẦN 1. SỬA TOÀN DIỆN LOGIC ĐỊA CHỈ GIAO HÀNG

## 1.1. Vấn đề hiện tại

Tại trang Checkout, khách hàng có thể nhập một địa chỉ bất kỳ và hệ thống vẫn chấp nhận.

Đây là lỗi nghiêm trọng vì địa chỉ không tồn tại hoặc không thể xác định vị trí vẫn được sử dụng để tạo đơn hàng.

Yêu cầu xây dựng lại quy trình xác thực địa chỉ giao hàng.

## 1.2. Xây dựng quy trình nhập địa chỉ chuẩn

Không cho phép khách hàng chỉ nhập một chuỗi văn bản tự do rồi mặc định xem đó là địa chỉ hợp lệ.

Địa chỉ phải được cấu thành từ các thành phần:

- Tỉnh/Thành phố.
- Phường/Xã.
- Địa chỉ chi tiết: số nhà, tên đường, ngõ, ngách, tòa nhà...

Sử dụng danh mục đơn vị hành chính Việt Nam hiện hành hoặc nguồn dữ liệu địa chỉ đáng tin cậy đã được tích hợp trong dự án.

Lưu ý: Phải sử dụng đúng mô hình đơn vị hành chính hiện hành, không mặc định bắt buộc khách hàng nhập quận/huyện theo cấu trúc cũ.

## 1.3. Quy tắc xác thực

Xây dựng validation ở cả Frontend và Backend.

Các trường hợp phải xử lý:

- Bỏ trống địa chỉ.
- Nhập toàn ký tự đặc biệt.
- Nhập toàn số hoặc nội dung vô nghĩa.
- Nhập tên tỉnh/thành phố không tồn tại.
- Nhập phường/xã không thuộc đơn vị hành chính đã chọn.
- Nhập địa chỉ không thể xác định được vị trí.
- Nhập địa chỉ thiếu thông tin cần thiết.
- Nhập địa chỉ hợp lệ nhưng có cách viết tắt, viết hoa, viết thường hoặc khoảng trắng khác nhau.

Yêu cầu:

1. Không chỉ sử dụng regex để đánh giá địa chỉ.
2. Kết hợp danh mục hành chính, kiểm tra cấu trúc dữ liệu và dịch vụ xác định vị trí (geocoding) nếu dự án có tích hợp hoặc có thể sử dụng nguồn phù hợp.
3. Chuẩn hóa địa chỉ trước khi lưu.
4. Không tự động biến một địa chỉ không hợp lệ thành địa chỉ hợp lệ.
5. Không yêu cầu geocoding phải trả về số nhà chính xác tuyệt đối nếu nhà cung cấp không hỗ trợ mức độ chi tiết đó. Phải phân biệt vị trí đã xác minh, vị trí xác định một phần và vị trí chưa xác minh.
6. Có thông báo cụ thể để khách biết cần sửa phần nào.

Chỉ cho phép đặt hàng khi địa chỉ đạt tiêu chuẩn hợp lệ theo quy tắc đã thiết lập.

## 1.4. Đồng bộ địa chỉ với giao hàng

Kiểm tra sự liên kết giữa địa chỉ và hai phương thức giao hàng:

- Ship Tiêu Chuẩn – Viettel Post.
- Ship Hỏa Tốc – nhân viên cửa hàng.

Đảm bảo:
- Địa chỉ được xác thực trước khi tính phí giao hàng.
- Khoảng cách đến showroom được tính từ tọa độ địa chỉ hợp lệ.
- Không hiển thị khoảng cách giả.
- Không cho phép chọn giao hỏa tốc nếu địa chỉ nằm ngoài phạm vi phục vụ thực tế.
- Phí vận chuyển phải được tính chính xác theo quy tắc hiện tại.
- Khi khách thay đổi địa chỉ, phí ship, khoảng cách và phương thức giao hàng phải được cập nhật lại.

Không làm thay đổi chính sách giá vận chuyển hiện tại nếu không có căn cứ từ logic kinh doanh đã tồn tại.

## 1.5. Kiểm thử địa chỉ

Tạo bộ test gồm:

- Địa chỉ hợp lệ.
- Địa chỉ sai tỉnh/thành phố.
- Địa chỉ sai phường/xã.
- Địa chỉ nhập linh tinh.
- Địa chỉ chỉ có số.
- Địa chỉ thiếu thông tin.
- Địa chỉ có dấu và không dấu.
- Địa chỉ có cách viết tắt thông dụng.
- Địa chỉ thay đổi sau khi đã chọn phương thức giao hàng.

Không sử dụng dữ liệu test để tạo đơn hàng thật.

---

# PHẦN 2. NÂNG CẤP GIAO DIỆN WEBSITE THEO TIÊU CHUẨN THƯƠNG MẠI ĐIỆN TỬ CHUYÊN NGHIỆP

## 2.1. Vấn đề hiện tại

Một số khu vực giao diện có cảm giác được tạo tự động bởi AI:

- Bố cục các thẻ thông tin quá máy móc.
- Các khung nội dung và badge xuất hiện quá nhiều.
- Khoảng cách, kích thước chữ và tỷ lệ các thành phần thiếu đồng nhất.
- Một số khu vực chưa tạo được cảm giác của một thương hiệu thời trang thực tế.
- Chatbot AI Stylist chưa được tích hợp tự nhiên với trải nghiệm mua sắm.

## 2.2. Yêu cầu thiết kế lại

Thực hiện UI/UX refinement trên cả Customer Storefront và Admin Panel.

Định hướng:

- Phong cách thương mại điện tử thời trang hiện đại.
- Tối giản, tinh tế, có tính thương hiệu.
- Phân cấp thông tin rõ ràng.
- Typography đồng nhất.
- Khoảng trắng hợp lý.
- Màu sắc có chủ đích, nhất quán với nhận diện Routine hiện tại.
- Các nút thao tác rõ ràng, dễ sử dụng.
- Giao diện responsive trên desktop, tablet và mobile.

Không được:
- Tự ý thay đổi logo hoặc nhận diện thương hiệu.
- Lạm dụng gradient, shadow, border và các khung card.
- Lạm dụng emoji, badge, icon trang trí.
- Sử dụng các bố cục dashboard chung chung giống template AI.
- Làm giao diện đẹp hơn nhưng khiến thao tác thực tế khó sử dụng.
- Thay đổi chức năng chỉ để phù hợp với một thiết kế mới.

## 2.3. Tối ưu chatbot AI Stylist

Rà soát giao diện chatbot hiện tại.

Yêu cầu:

- Khung chat gọn, tự nhiên, không che khuất nội dung mua sắm.
- Phân biệt rõ tin nhắn khách hàng và AI Stylist.
- Hiển thị sản phẩm bằng hình ảnh thật từ database.
- Hiển thị giá, tên sản phẩm và thông tin sản phẩm chính xác.
- Các nút gợi ý câu hỏi phải liên quan đến ngữ cảnh hội thoại.
- Nút mở rộng/thu nhỏ chatbot hoạt động bình thường.
- Không hiển thị quá nhiều khung nội dung không cần thiết.
- Khi chuyển sang tư vấn viên, phải hiển thị trạng thái kết nối rõ ràng.

Đặc biệt, không được tự động phối đồ khi khách chỉ hỏi thông tin sản phẩm. Chỉ thực hiện phối đồ khi khách yêu cầu.

---

# PHẦN 3. HOÀN THIỆN HỆ THỐNG AI STYLIST KẾT NỐI CHUYÊN VIÊN TƯ VẤN

Đây là phần ưu tiên cao nhất.

## 3.1. Lỗi hiện tại

Khách hàng đang sử dụng AI Stylist và nhấn nút yêu cầu kết nối chuyên viên tư vấn.

Chatbot trả lời:

"Mình đã ghi nhận yêu cầu kết nối chuyên viên tư vấn. Bạn vui lòng chờ chuyên viên Routine tiếp nhận nhé!"

Tuy nhiên:
- Trang quản trị không nhận được thông báo tương ứng.
- Mục AI Stylist Leads không hiển thị hoặc không cập nhật hội thoại mới.
- Chuyên viên không nhìn thấy nội dung hội thoại của khách.
- Không có quy trình tiếp nhận và phản hồi khách hàng hoàn chỉnh.

Như vậy, thông báo của AI hiện tại chưa chứng minh rằng yêu cầu đã được lưu và chuyển đến nhân viên.

Phải sửa toàn bộ quy trình này.

## 3.2. Xây dựng quy trình kết nối hoàn chỉnh

Luồng nghiệp vụ bắt buộc:

BƯỚC 1 – KHÁCH YÊU CẦU TƯ VẤN

Khi khách hàng nhấn "Nhắn tin với chuyên viên tư vấn":

- Tạo yêu cầu tư vấn thực tế.
- Ghi nhận thời điểm yêu cầu.
- Ghi nhận khách hàng đang đăng nhập hay khách vãng lai.
- Ghi nhận thông tin tài khoản hoặc session khách vãng lai.
- Ghi nhận nội dung hội thoại trước khi chuyển giao.
- Ghi nhận sản phẩm khách quan tâm.
- Ghi nhận ngân sách, size, màu sắc và nhu cầu nếu AI đã thu thập được.
- Ghi nhận nguồn yêu cầu từ AI Stylist.

Không được làm mất lịch sử trò chuyện trước đó.

BƯỚC 2 – LƯU VÀO DATABASE

Kiểm tra schema hiện tại và tái sử dụng các bảng phù hợp.

Nếu cần bổ sung, xây dựng đầy đủ quan hệ dữ liệu cho:

- Consultation Request / Lead.
- Conversation.
- Conversation Message.
- Staff Assignment.
- Notification.

Không tạo bảng trùng lặp nếu dự án đã có cấu trúc tương ứng.

Yêu cầu:
- Dữ liệu phải được lưu vào MySQL.
- Có mã định danh duy nhất cho từng yêu cầu và cuộc hội thoại.
- Có quan hệ giữa khách hàng, yêu cầu tư vấn và hội thoại.
- Đảm bảo dữ liệu không bị mất khi tải lại trang hoặc đăng xuất.
- Có cơ chế tránh tạo yêu cầu trùng lặp khi khách nhấn nút nhiều lần.
- Lưu thời gian tạo và cập nhật.

Việc tạo yêu cầu và hội thoại ban đầu phải được xử lý nhất quán, tránh tình trạng chỉ tạo Lead nhưng không có Conversation.

BƯỚC 3 – THÔNG BÁO TRÊN ADMIN PANEL

Khi có yêu cầu tư vấn mới:

- Thông báo phải xuất hiện tại biểu tượng chuông trên Admin Panel.
- Tăng số lượng thông báo chưa đọc.
- Có thông tin khách hàng và thời gian yêu cầu.
- Có thể nhấn thông báo để mở đúng yêu cầu tư vấn.
- Cập nhật trạng thái đã đọc/chưa đọc.
- Không tạo thông báo giả lập chỉ bằng dữ liệu frontend.

Ưu tiên sử dụng WebSocket hoặc cơ chế realtime hiện có.

Nếu dự án chưa có WebSocket, có thể triển khai polling có kiểm soát làm phương án tương thích.

BƯỚC 4 – HIỂN THỊ TẠI AI STYLIST LEADS

Khi quản trị viên mở mục AI Stylist Leads:

Phải nhìn thấy yêu cầu mới ngay sau khi hệ thống cập nhật.

Mỗi yêu cầu phải hiển thị:

- Tên khách hàng hoặc Khách vãng lai.
- Số điện thoại nếu khách đã cung cấp.
- Trạng thái yêu cầu.
- Thời gian gửi yêu cầu.
- Nội dung hội thoại gần nhất.
- Sản phẩm khách đang quan tâm.
- Điểm Purchase Intent nếu hệ thống đã tính.
- Ngân sách nếu khách đã đề cập.
- Nhu cầu và thông tin đã được AI thu thập.

Không tự suy diễn thông tin khách hàng khi dữ liệu chưa có.

BƯỚC 5 – CHUYÊN VIÊN TIẾP NHẬN VÀ TƯ VẤN

Khi nhân viên nhấn tiếp nhận:

- Cập nhật trạng thái yêu cầu.
- Ghi nhận nhân viên phụ trách.
- Hiển thị trạng thái đang tư vấn.
- Mở giao diện hội thoại thực tế.
- Hiển thị toàn bộ lịch sử trò chuyện giữa khách và AI trước khi chuyển giao.
- Cho phép nhân viên gửi tin nhắn cho khách.
- Khách nhận được tin nhắn ngay trên giao diện chatbot hoặc giao diện hội thoại phù hợp.
- Khách có thể phản hồi và nhân viên nhìn thấy phản hồi đó.

Không chỉ hiển thị nội dung hội thoại tĩnh.

Phải có cơ chế gửi và nhận tin nhắn hai chiều thực tế.

BƯỚC 6 – HOÀN TẤT TƯ VẤN

Xây dựng trạng thái rõ ràng:

- Chờ tiếp nhận.
- Đang tư vấn.
- Đã hoàn tất.
- Đã đóng.

Nhân viên có thể:
- Tiếp nhận yêu cầu.
- Tiếp tục hội thoại.
- Đóng yêu cầu khi hoàn thành.
- Xem lại lịch sử tư vấn.

Không được tự động đóng yêu cầu khi khách vừa gửi yêu cầu tư vấn.

## 3.3. Yêu cầu riêng đối với khách vãng lai

Đây là tình huống cần đặc biệt chú ý.

Hệ thống hiện có khách hàng đăng nhập và khách vãng lai.

Nếu khách vãng lai yêu cầu tư vấn:
- Không bắt buộc khách đăng nhập chỉ để chuyển sang tư vấn viên nếu chính sách hiện tại không yêu cầu.
- Tạo định danh session ổn định.
- Gắn hội thoại với session đó.
- Không nhầm lẫn hai khách vãng lai khác nhau.
- Khi khách tải lại trang, hội thoại vẫn được khôi phục nếu session còn hiệu lực.
- Khi nhân viên phản hồi, đúng khách hàng phải nhận được tin nhắn.

Nếu cần thu thập số điện thoại, phải thực hiện theo luồng nhập thông tin hợp lý, không tự tạo số điện thoại giả.

## 3.4. Đồng bộ AI và chuyên viên tư vấn

Khi khách đã chuyển sang tư vấn viên:

- AI phải biết yêu cầu đang được nhân viên tiếp nhận.
- Không tiếp tục trả lời như thể đang tư vấn độc lập nếu nhân viên đang xử lý.
- Có thể thông báo khách đang chờ nhân viên phản hồi.
- Không tạo thêm Lead mới mỗi khi khách gửi tin nhắn.
- Không mất ngữ cảnh hội thoại.
- Không để tin nhắn AI và nhân viên bị đảo lộn thứ tự.

Nếu khách quay lại sử dụng AI sau khi yêu cầu tư vấn đã đóng, phải xử lý theo trạng thái nghiệp vụ phù hợp.

---

# PHẦN 4. RÀ SOÁT TOÀN BỘ API, DATABASE VÀ CƠ CHẾ ĐỒNG BỘ

Không được chỉ sửa giao diện.

Kiểm tra toàn bộ liên kết:

Customer Frontend → Backend API → MySQL → Admin Frontend.

Đặc biệt kiểm tra:

1. API tạo yêu cầu tư vấn.
2. API lấy danh sách yêu cầu.
3. API xem chi tiết hội thoại.
4. API gửi tin nhắn từ khách.
5. API gửi tin nhắn từ chuyên viên.
6. API cập nhật trạng thái.
7. API phân công nhân viên.
8. API lấy và cập nhật thông báo.
9. Cơ chế đồng bộ tin nhắn realtime.
10. Cơ chế khôi phục session khách vãng lai.

Tất cả phải có:
- Validation.
- Authentication/Authorization phù hợp.
- Xử lý lỗi.
- Kiểm tra quyền nhân viên.
- Chống gửi tin nhắn trùng.
- Đảm bảo thứ tự tin nhắn.
- Không để khách hàng truy cập hội thoại của người khác.
- Không để API trả về thành công khi thao tác database thất bại.

---

# PHẦN 5. KIỂM THỬ END-TO-END TOÀN HỆ THỐNG

Không được kết luận hoàn thành chỉ vì frontend hiển thị đúng.

Phải trực tiếp chạy hệ thống và thực hiện các kịch bản sau.

## TEST 1 – ĐỊA CHỈ GIAO HÀNG

- Nhập địa chỉ hợp lệ.
- Nhập địa chỉ sai.
- Nhập địa chỉ linh tinh.
- Thay đổi địa chỉ sau khi chọn giao hàng.
- Kiểm tra phí ship và khoảng cách.
- Thử đặt hàng khi địa chỉ chưa hợp lệ.

Điều kiện đạt: Địa chỉ sai không thể vượt qua bước xác thực và không thể tạo đơn hàng.

## TEST 2 – KHÁCH VÃNG LAI YÊU CẦU TƯ VẤN

1. Mở website ở giao diện khách hàng.
2. Mở AI Stylist.
3. Trao đổi về một sản phẩm cụ thể.
4. Nhấn kết nối chuyên viên.
5. Kiểm tra dữ liệu đã được lưu vào MySQL.
6. Mở Admin Panel.
7. Kiểm tra thông báo mới.
8. Mở AI Stylist Leads.
9. Mở đúng yêu cầu tư vấn.
10. Kiểm tra lịch sử trò chuyện.

Điều kiện đạt: Yêu cầu xuất hiện ở cả Customer và Admin với cùng một mã định danh.

## TEST 3 – CHUYÊN VIÊN TRẢ LỜI KHÁCH

1. Nhân viên tiếp nhận yêu cầu.
2. Gửi một tin nhắn từ Admin.
3. Kiểm tra tin nhắn hiển thị trên Customer.
4. Khách phản hồi.
5. Kiểm tra tin nhắn xuất hiện trên Admin.
6. Tải lại cả hai giao diện.
7. Kiểm tra lịch sử hội thoại.

Điều kiện đạt: Hai bên gửi và nhận tin nhắn thực tế, không mất dữ liệu.

## TEST 4 – KHÁCH HÀNG ĐÃ ĐĂNG NHẬP

Lặp lại quy trình tư vấn với tài khoản khách hàng đã đăng nhập.

Kiểm tra liên kết chính xác giữa:
- Tài khoản.
- Hồ sơ khách hàng.
- Yêu cầu tư vấn.
- Hội thoại.
- Tin nhắn.

## TEST 5 – KIỂM TRA GIAO DIỆN

Kiểm tra các màn hình:
- Trang chủ.
- Chi tiết sản phẩm.
- Giỏ hàng.
- Checkout.
- AI Stylist.
- AI Stylist Leads.
- Giao diện hội thoại Admin.
- Thông báo Admin.
- Quản lý đơn hàng.

Đảm bảo giao diện không vỡ trên desktop và mobile.

## TEST 6 – REGRESSION TEST

Kiểm tra lại các chức năng cũ:

- Đăng ký, đăng nhập, đăng xuất.
- Hiển thị sản phẩm.
- Tìm kiếm và lọc sản phẩm.
- Chi tiết sản phẩm.
- Chọn size và màu sắc.
- Kiểm tra tồn kho.
- Thêm vào giỏ hàng.
- Cập nhật giỏ hàng.
- Voucher.
- Thanh toán.
- Tạo đơn hàng.
- Theo dõi đơn hàng.
- Quản lý sản phẩm Admin.
- Quản lý khách hàng.
- Quản lý đơn hàng.
- AI Stylist tìm kiếm và tư vấn sản phẩm.
- Hiển thị ảnh sản phẩm.
- Các chức năng quản trị hiện có.

Không được làm hỏng các luồng đã hoạt động.

---

# PHẦN 6. TIÊU CHUẨN NGHIỆM THU

Sau khi thực hiện, phải cung cấp báo cáo nghiệm thu thực tế.

Báo cáo gồm:

## A. Tổng hợp thay đổi

- Những lỗi đã tìm thấy.
- Nguyên nhân gốc rễ.
- File Frontend đã sửa.
- File Backend đã sửa.
- Database schema hoặc migration đã thay đổi.
- API được bổ sung hoặc chỉnh sửa.
- Các thành phần UI/UX được cải tiến.

## B. Kết quả kiểm thử

Tạo bảng:

| Hạng mục | Kết quả | Bằng chứng |
|---|---|---|
| Xác thực địa chỉ | PASS/FAIL | Kết quả test |
| Tính phí giao hàng | PASS/FAIL | Kết quả test |
| Tạo yêu cầu tư vấn | PASS/FAIL | Database |
| Admin nhận thông báo | PASS/FAIL | Giao diện Admin |
| Admin nhận hội thoại | PASS/FAIL | Ảnh thực tế |
| Nhân viên gửi tin nhắn | PASS/FAIL | Hội thoại hai chiều |
| Khách nhận phản hồi | PASS/FAIL | Giao diện Customer |
| Khôi phục lịch sử chat | PASS/FAIL | Kết quả reload |
| Khách vãng lai | PASS/FAIL | Kết quả test |
| Khách đăng nhập | PASS/FAIL | Kết quả test |
| Regression test | PASS/FAIL | Báo cáo |

## C. Điều kiện hoàn thành

Chỉ được tuyên bố hệ thống hoàn thành khi:

1. Không còn lỗi nghiêm trọng hoặc lỗi chặn luồng mua hàng.
2. Địa chỉ không hợp lệ không thể tạo đơn.
3. Khách yêu cầu tư vấn thì Admin thực sự nhận được yêu cầu.
4. Admin xem được hội thoại trước khi tiếp nhận.
5. Nhân viên và khách nhắn tin hai chiều được.
6. Tin nhắn và trạng thái được lưu trong MySQL.
7. Thông báo được đồng bộ chính xác.
8. Các chức năng cũ vẫn hoạt động.
9. Không có dữ liệu test rác trong database thật.
10. Các kịch bản E2E đã được chạy và có bằng chứng.

Nếu có hạng mục chưa hoàn thành, phải ghi rõ:
- Nguyên nhân.
- File hoặc API đang gặp vấn đề.
- Công việc còn thiếu.
- Hướng xử lý tiếp theo.

TUYỆT ĐỐI KHÔNG báo PASS khi chỉ mới kiểm tra bằng cách đọc code hoặc nhìn giao diện.

---

# CÁCH TRIỂN KHAI

Thực hiện theo 4 giai đoạn:

**Giai đoạn 1:** Audit toàn bộ hệ thống, xác định nguyên nhân lỗi và lập danh sách file cần sửa.

**Giai đoạn 2:** Sửa validation địa chỉ và hoàn thiện quy trình AI Stylist chuyển giao chuyên viên.

**Giai đoạn 3:** Hoàn thiện giao diện Customer/Admin và đồng bộ các chức năng liên quan.

**Giai đoạn 4:** Chạy E2E, regression test, sửa các lỗi phát sinh và lập báo cáo nghiệm thu.

Sau mỗi giai đoạn phải báo cáo:
- Đã thực hiện những gì.
- Những file nào đã thay đổi.
- Kết quả chạy thực tế.
- Những lỗi còn tồn tại.

Ưu tiên bảo toàn dữ liệu, tính đúng đắn nghiệp vụ và khả năng vận hành thực tế.

Mục tiêu cuối cùng: Biến Routine từ một website demo có các chức năng riêng lẻ thành một hệ thống thương mại điện tử hoạt động liên thông thực sự, trong đó khách hàng, AI Stylist, chuyên viên tư vấn, Admin, Backend và MySQL cùng vận hành nhất quán.
