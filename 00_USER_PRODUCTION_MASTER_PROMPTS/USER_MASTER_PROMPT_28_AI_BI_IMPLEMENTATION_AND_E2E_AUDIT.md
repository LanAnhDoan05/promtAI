# USER MASTER PROMPT #28: 28 AI BI IMPLEMENTATION AND E2E AUDIT
> **Nguồn gốc:** Prompt chỉ đạo thực tế từ Người dùng (User Request) tại Step 11986.
> **Độ dài gốc:** 22429 ký tự.
> **Mục đích trong thư viện:** Cung cấp toàn văn đặc tả nghiệp vụ, yêu cầu kỹ thuật và ràng buộc sản xuất thực tế mà người dùng đã trực tiếp chỉ đạo và kiểm chứng trong dự án Routine Web.

---

# MASTER PROMPT – IMPLEMENT AI BUSINESS INTELLIGENCE + FULL PROJECT END-TO-END AUDIT
## DỰ ÁN ROUTINE E-COMMERCE PLATFORM

**VAI TRÒ**

Bạn là Senior Full-stack Engineer, AI Engineer, Data Engineer, Software Architect và QA Automation Engineer chịu trách nhiệm triển khai, tích hợp và nghiệm thu hệ thống Routine E-commerce Platform.

Nhiệm vụ là phát triển hoàn chỉnh module AI Business Intelligence dành cho Admin, sau đó kiểm tra, tối ưu và nghiệm thu toàn bộ hệ thống Routine để đảm bảo tất cả chức năng Frontend, Backend, Database, AI Agent và các nghiệp vụ thương mại điện tử hoạt động chính xác, liên thông và ổn định.

Đây là nhiệm vụ triển khai trên dự án thực tế, không phải tạo bản demo, giao diện minh họa hoặc báo cáo giả lập.

---

# PHẦN 0. NGUYÊN TẮC BẮT BUỘC

Trước khi thực hiện, phải tuân thủ các nguyên tắc sau:

1. Đọc toàn bộ repository hiện tại, bao gồm cấu trúc thư mục, package, frontend, backend, database schema, migration, API, middleware, authentication, authorization, AI Agent, Gemini integration, Admin Portal, Customer Storefront, VNPay và các chức năng hiện có.

2. Xác định chính xác công nghệ đang sử dụng từ source code thực tế. Không tự suy đoán hoặc tự thay đổi framework, thư viện, phiên bản hay kiến trúc.

3. Không xây dựng lại website từ đầu. Không xóa hoặc thay thế các chức năng đang hoạt động nếu không có lý do kỹ thuật và phương án tương thích.

4. Tận dụng tối đa các module, service, API, component và database model hiện có. Chỉ bổ sung những phần thực sự thiếu.

5. Không sử dụng dữ liệu giả, dữ liệu hardcode hoặc số liệu tự tạo để thay thế dữ liệu kinh doanh thực tế.

6. Không để Gemini tự bịa doanh thu, số lượng sản phẩm bán ra, lượt truy cập, tồn kho, tỷ lệ chuyển đổi hoặc các chỉ số khác.

7. Mọi số liệu phân tích phải được truy xuất hoặc tính toán từ database và dữ liệu hoạt động thực tế.

8. Không đưa API key, secret key, mật khẩu database hoặc thông tin nhạy cảm vào frontend, source code công khai hoặc log.

9. Không tự ý xóa dữ liệu khách hàng, đơn hàng, sản phẩm hoặc dữ liệu lịch sử.

10. Không đánh dấu một chức năng là hoàn thành nếu chưa thực thi kiểm thử và có bằng chứng.

11. Không chỉ tạo báo cáo phân tích code. Phải trực tiếp sửa lỗi, triển khai phần còn thiếu, chạy ứng dụng và kiểm thử thực tế trong phạm vi được phép.

12. Không tự ý deploy production, thanh toán thật, commit hoặc push GitHub nếu chưa được cho phép.

---

# PHẦN A. TRIỂN KHAI AI BUSINESS INTELLIGENCE

## A1. MỤC TIÊU CHỨC NĂNG

Xây dựng một trợ lý AI phân tích kinh doanh dành riêng cho Admin Routine.

Admin có thể nhấn một nút để yêu cầu AI:

- Phân tích tình hình kinh doanh.
- Đánh giá doanh thu và hiệu suất sản phẩm.
- Phân tích nhu cầu khách hàng qua hành vi truy cập.
- Phát hiện các vấn đề trong hoạt động bán hàng.
- Đánh giá tình trạng tồn kho.
- Nhận diện cơ hội kinh doanh.
- Đưa ra các kiến nghị có căn cứ dữ liệu.
- Giải thích lý do và mức độ ưu tiên của từng kiến nghị.

Đây là cơ chế phân tích theo yêu cầu (On-demand AI Business Analysis), không bắt buộc tự động chạy mỗi khi Admin mở Dashboard.

Phải có một nút kích hoạt rõ ràng trên trang quản trị:

**"PHÂN TÍCH & ĐƯA RA KIẾN NGHỊ"**

Khi Admin nhấn nút, hệ thống thực hiện toàn bộ quy trình thu thập dữ liệu, tính toán chỉ số, phân tích và tạo báo cáo.

## A2. THU THẬP VÀ KIỂM TRA DỮ LIỆU KINH DOANH

Kiểm tra database hiện tại và xác định dữ liệu nào đã có, dữ liệu nào còn thiếu.

Bắt buộc xem xét các nhóm dữ liệu:

### 1. Dữ liệu bán hàng

- Tổng doanh thu.
- Doanh thu theo ngày, tuần, tháng.
- Số lượng đơn hàng.
- Số đơn hàng thành công.
- Số đơn hàng bị hủy.
- Số lượng sản phẩm bán ra.
- Giá trị đơn hàng trung bình.
- Sản phẩm bán chạy.
- Sản phẩm có doanh thu cao.
- Sản phẩm có doanh số giảm.
- Hiệu suất theo danh mục.

Chỉ tính doanh thu từ các đơn hàng đủ điều kiện theo trạng thái nghiệp vụ thực tế. Phải phân biệt đơn mới, chờ thanh toán, đã thanh toán, đang xử lý, đã giao, hoàn thành, hủy và hoàn tiền.

Không cộng các đơn hàng chưa thanh toán hoặc đã hủy vào doanh thu thực nhận.

Phải xác định quy tắc ghi nhận doanh thu phù hợp với quy trình đơn hàng của Routine và thống nhất giữa báo cáo AI với Dashboard quản trị.

### 2. Dữ liệu hành vi khách hàng

Kiểm tra hệ thống hiện tại có ghi nhận các sự kiện sau hay chưa:

- Product view: Khách hàng xem sản phẩm.
- Search: Khách hàng tìm kiếm sản phẩm.
- Category view: Khách hàng xem danh mục.
- Add to cart: Khách hàng thêm sản phẩm vào giỏ.
- Remove from cart: Khách hàng xóa sản phẩm khỏi giỏ.
- Begin checkout: Khách hàng bắt đầu thanh toán.
- Purchase: Khách hàng hoàn thành mua hàng.
- Wishlist: Khách hàng thêm sản phẩm yêu thích.

Nếu chưa có hệ thống tracking phù hợp, hãy triển khai bổ sung một cách có cấu trúc.

Yêu cầu:
- Ghi nhận chính xác product ID, event type, thời gian và thông tin phiên truy cập cần thiết.
- Có thể liên kết với tài khoản người dùng khi khách hàng đăng nhập.
- Khách chưa đăng nhập vẫn có thể được ghi nhận bằng session ID hoặc cơ chế ẩn danh phù hợp.
- Không thu thập thông tin cá nhân không cần thiết.
- Không ghi nhận sự kiện trùng lặp do một thao tác bị gửi nhiều lần.
- Không tạo lượt xem giả từ hoạt động của Admin, bot hoặc các request hệ thống.
- Có cơ chế hạn chế spam và tracking bất thường.
- Không làm ảnh hưởng tốc độ tải trang và trải nghiệm mua sắm.

Đặc biệt phải đảm bảo tracking không chỉ hoạt động trên giao diện mà dữ liệu thực sự được lưu vào database.

### 3. Dữ liệu tồn kho

Thu thập:
- Số lượng tồn kho hiện tại.
- Sản phẩm sắp hết hàng.
- Sản phẩm hết hàng.
- Sản phẩm tồn kho lâu nhưng ít bán.
- Biến thể theo màu sắc và kích thước nếu hệ thống quản lý theo biến thể.
- Lịch sử thay đổi tồn kho nếu có.

Không tự tạo dữ liệu tồn kho để phục vụ AI.

## A3. DATA PROCESSING – XỬ LÝ VÀ TÍNH TOÁN DỮ LIỆU

Đây là bước quan trọng nhất.

Không gửi toàn bộ database trực tiếp cho Gemini.

Backend phải thực hiện:
1. Truy xuất các dữ liệu cần thiết.
2. Kiểm tra dữ liệu hợp lệ.
3. Loại bỏ bản ghi trùng lặp.
4. Xác định khoảng thời gian phân tích.
5. Tổng hợp các chỉ số.
6. Tính toán tỷ lệ và so sánh.
7. Tạo một bộ dữ liệu phân tích có cấu trúc.
8. Chuyển dữ liệu tổng hợp cho Gemini để diễn giải và đưa ra kiến nghị.

Các chỉ số cần tính toán:

- Revenue Growth Rate.
- Units Sold.
- Average Order Value.
- Product View Count.
- Search Count.
- Add-to-Cart Rate.
- Conversion Rate.
- Cart Abandonment Rate.
- Product Revenue Contribution.
- Stock Availability.
- View-to-Purchase Performance.

Phải định nghĩa rõ công thức, mẫu số, mẫu số hợp lệ, thời gian và cách xử lý trường hợp không có dữ liệu.

Ví dụ:

Conversion Rate = Số phiên mua hàng thành công / Tổng số phiên có thể xác định trong cùng phạm vi phân tích.

Không được tùy tiện lấy số đơn hàng chia cho lượt xem sản phẩm rồi gọi đó là tỷ lệ chuyển đổi nếu hai chỉ số không cùng phạm vi đo lường.

Nếu thiếu dữ liệu, phải hiển thị "Chưa đủ dữ liệu để đánh giá", không tự suy diễn.

## A4. AI BUSINESS ANALYSIS – PHÂN TÍCH KINH DOANH

Sử dụng Google Gemini theo cấu hình và cách tích hợp hiện có của dự án.

AI nhận dữ liệu tổng hợp từ Backend, thực hiện phân tích theo các nhóm sau:

### Nhóm 1: Sales Performance Analysis

Phân tích:
- Sản phẩm tạo doanh thu lớn nhất.
- Sản phẩm có số lượng bán cao nhất.
- Danh mục đóng góp doanh thu nhiều nhất.
- Sản phẩm có dấu hiệu giảm doanh số.
- Biến động doanh thu theo thời gian.

### Nhóm 2: Customer Demand Analysis

Phân tích:
- Sản phẩm được xem nhiều nhất.
- Sản phẩm được tìm kiếm nhiều nhất.
- Sản phẩm có nhiều lượt thêm giỏ hàng.
- Sản phẩm được quan tâm nhưng ít mua.
- Những danh mục khách hàng đang có nhu cầu cao.
- Nhu cầu tìm kiếm chưa được đáp ứng bởi danh mục hiện tại.

### Nhóm 3: Conversion Analysis

Phân tích:
- Sản phẩm có lượt xem cao nhưng ít đơn.
- Sản phẩm có nhiều lượt thêm giỏ nhưng không hoàn tất mua.
- Những điểm có thể gây cản trở quá trình mua hàng.
- Khả năng mất khách hàng trong hành trình mua sắm.

Không kết luận nguyên nhân chắc chắn chỉ dựa trên một chỉ số. Phải trình bày rõ đâu là dữ kiện và đâu là giả thuyết cần kiểm tra.

### Nhóm 4: Inventory Analysis

Phân tích:
- Sản phẩm bán nhanh nhưng tồn kho thấp.
- Sản phẩm tồn kho cao nhưng tiêu thụ chậm.
- Sản phẩm thường xuyên hết hàng.
- Sự chênh lệch giữa nhu cầu và khả năng cung ứng.

### Nhóm 5: Business Opportunity Analysis

Tìm kiếm:
- Danh mục có nhu cầu tăng.
- Sản phẩm có tiềm năng phát triển.
- Cơ hội tối ưu doanh thu.
- Cơ hội cải thiện tỷ lệ chuyển đổi.
- Cơ hội tối ưu tồn kho.
- Những vấn đề cần ưu tiên giải quyết.

## A5. AI BUSINESS RECOMMENDATION – ĐỀ XUẤT KIẾN NGHỊ KINH DOANH

Đây là đầu ra quan trọng nhất của module.

AI không được chỉ mô tả số liệu. AI phải chuyển kết quả phân tích thành những hành động cụ thể mà Admin có thể cân nhắc thực hiện.

Mỗi kiến nghị bắt buộc có:

1. Tên kiến nghị.
2. Nhóm vấn đề.
3. Mức độ ưu tiên: Cao / Trung bình / Thấp.
4. Vấn đề phát hiện.
5. Dữ liệu làm căn cứ.
6. Phân tích nguyên nhân có thể xảy ra.
7. Đề xuất hành động cụ thể.
8. Kết quả kỳ vọng.
9. Rủi ro hoặc điều kiện cần lưu ý.
10. Mức độ tin cậy hoặc giới hạn dữ liệu.

Các loại kiến nghị cần hỗ trợ:

**A. Kiến nghị về sản phẩm**
- Bổ sung sản phẩm.
- Tối ưu danh mục.
- Điều chỉnh cách trưng bày.
- Ưu tiên sản phẩm tiềm năng.

**B. Kiến nghị về tồn kho**
- Xem xét nhập thêm hàng.
- Ưu tiên kiểm tra sản phẩm sắp hết.
- Xử lý hàng tồn kho lâu.
- Điều chỉnh kế hoạch cung ứng.

**C. Kiến nghị về bán hàng**
- Tối ưu giá bán.
- Tối ưu hình ảnh và mô tả sản phẩm.
- Tối ưu trang chi tiết sản phẩm.
- Cải thiện quy trình thanh toán.
- Đề xuất chương trình khuyến mãi khi có đủ căn cứ.

**D. Kiến nghị về marketing**
- Tăng cường quảng bá sản phẩm có nhu cầu cao.
- Ưu tiên danh mục có tiềm năng.
- Tập trung nội dung vào nhóm sản phẩm được tìm kiếm nhiều.
- Đề xuất chiến dịch theo nhóm sản phẩm và hành vi khách hàng.

Không tự đặt ngân sách, doanh thu mục tiêu hoặc phần trăm tăng trưởng nếu không có dữ liệu và giả định rõ ràng.

AI chỉ đưa ra kiến nghị để Admin xem xét. Không tự động thay đổi giá, tồn kho, trạng thái sản phẩm, khuyến mãi hoặc ngân sách quảng cáo.

## A6. GIAO DIỆN AI BUSINESS INTELLIGENCE TRÊN ADMIN

Thiết kế giao diện chuyên nghiệp, đồng nhất với phong cách quản trị hiện có của Routine.

Không sử dụng giao diện AI tạo sẵn, gradient màu sắc quá mức, card bo góc quá nhiều hoặc cách bố trí mang cảm giác template AI.

Yêu cầu:

### Khu vực 1: Tổng quan phân tích

Hiển thị:
- Tiêu đề AI Business Intelligence.
- Mô tả chức năng.
- Thời gian phân tích.
- Thời điểm cập nhật dữ liệu.
- Trạng thái dữ liệu.
- Nút "Phân tích & đưa ra kiến nghị".

Cho phép chọn:
- 7 ngày gần nhất.
- 30 ngày gần nhất.
- 90 ngày gần nhất.
- Tháng hiện tại.
- Khoảng thời gian tùy chỉnh.

### Khu vực 2: Kết quả phân tích

Hiển thị các chỉ số và biểu đồ phù hợp:
- Doanh thu.
- Đơn hàng.
- Sản phẩm bán chạy.
- Sản phẩm được quan tâm.
- Lượt xem.
- Lượt thêm giỏ.
- Tỷ lệ chuyển đổi.
- Tình trạng tồn kho.

### Khu vực 3: Báo cáo kiến nghị

Trình bày từng kiến nghị riêng biệt.

Cho phép Admin:
- Đọc chi tiết.
- Xem dữ liệu làm căn cứ.
- Xem thời gian phân tích.
- Đánh dấu đã xem.
- Đánh dấu đang xử lý.
- Đánh dấu đã hoàn thành.
- Lưu trữ kiến nghị.
- Xem lại các báo cáo phân tích trước đây.

Phải lưu báo cáo vào database để Admin có thể xem lại sau khi tải lại trang hoặc đăng xuất đăng nhập.

### Khu vực 4: Lịch sử phân tích

Mỗi lần Admin nhấn nút phân tích phải tạo một phiên phân tích riêng, có:
- ID báo cáo.
- Admin thực hiện.
- Thời điểm phân tích.
- Khoảng thời gian dữ liệu.
- Trạng thái xử lý.
- Kết quả phân tích.
- Danh sách kiến nghị.

Không ghi đè báo cáo cũ khi tạo báo cáo mới.

## A7. BACKEND, API VÀ DATABASE

Phải xây dựng theo kiến trúc hiện có.

Rà soát và bổ sung những thành phần cần thiết:
- Business analytics service.
- Data aggregation service.
- Customer behavior tracking service.
- Gemini business analysis service.
- Business recommendation service.
- Analysis report service.

Các API cần có tương ứng với kiến trúc dự án:

- Lấy dữ liệu tổng quan.
- Tạo yêu cầu phân tích.
- Lấy kết quả phân tích.
- Lấy lịch sử báo cáo.
- Xem chi tiết báo cáo.
- Cập nhật trạng thái kiến nghị.
- Lưu trữ báo cáo.

Thiết kế API có phân quyền Admin.

Database cần lưu trữ báo cáo, kiến nghị và lịch sử xử lý.

Yêu cầu:
- Có validation.
- Có pagination khi cần.
- Có xử lý lỗi.
- Có timeout.
- Có kiểm soát số lần gọi Gemini.
- Có giới hạn kích thước dữ liệu gửi đến AI.
- Có xử lý khi Gemini không phản hồi.
- Có cơ chế tránh tạo nhiều báo cáo trùng lặp khi Admin nhấn nút liên tục.
- Có log cần thiết để truy vết.

Nếu báo cáo được tạo bất đồng bộ, giao diện phải hiển thị trạng thái chờ xử lý, đang phân tích, hoàn thành hoặc thất bại.

## A8. CHẤT LƯỢNG VÀ TÍNH AN TOÀN CỦA AI

- Gemini chỉ được phân tích dữ liệu do Backend cung cấp.
- Không cho phép AI tự thực thi câu lệnh SQL tùy ý.
- Không cho phép AI truy cập trực tiếp database.
- Không để AI tự thay đổi dữ liệu nghiệp vụ.
- Không đưa thông tin cá nhân nhạy cảm vào prompt.
- Phải kiểm tra đầu ra AI theo schema.
- Phải xử lý phản hồi sai định dạng.
- Phải ngăn chặn prompt injection từ dữ liệu người dùng.
- Phải phân biệt dữ liệu thực tế, suy luận và kiến nghị.
- Không tạo kiến nghị khi không có căn cứ đủ tin cậy.

---

# PHẦN B. KIỂM TRA VÀ TỐI ƯU TOÀN BỘ ROUTINE E-COMMERCE PLATFORM

Sau khi hoàn thiện AI Business Intelligence, bắt buộc tiến hành kiểm tra tổng thể toàn dự án.

Không được chỉ kiểm tra module AI mới.

Mục tiêu là bảo đảm mọi chức năng hiện tại hoạt động bình thường sau khi tích hợp.

## B1. FRONTEND – CUSTOMER STOREFRONT

Kiểm tra thực tế:

1. Trang chủ.
2. Hiển thị sản phẩm.
3. Danh mục sản phẩm.
4. Tìm kiếm và lọc sản phẩm.
5. Chi tiết sản phẩm.
6. Hình ảnh sản phẩm.
7. Giá bán và biến thể.
8. Giỏ hàng.
9. Đặt hàng.
10. Thanh toán.
11. Lịch sử đơn hàng.
12. Hồ sơ khách hàng.
13. Đăng nhập và đăng ký.
14. Wishlist nếu có.
15. Đánh giá sản phẩm nếu có.
16. Responsive trên desktop, tablet và mobile.

Đặc biệt:
- Không để ảnh sản phẩm bị mất.
- Không hiển thị sản phẩm đã bị xóa hoặc không còn được kinh doanh.
- Không hiển thị giá sai.
- Không để sản phẩm được thêm mới từ Admin nhưng không xuất hiện trên giao diện khách hàng.
- Không để giao diện bị vỡ khi dữ liệu thay đổi.
- Không có lỗi console nghiêm trọng.

## B2. ADMIN PORTAL

Kiểm tra:

1. Đăng nhập Admin.
2. Phân quyền Admin.
3. Dashboard.
4. Quản lý sản phẩm.
5. Thêm sản phẩm.
6. Sửa sản phẩm.
7. Xóa hoặc ẩn sản phẩm.
8. Upload hình ảnh.
9. Quản lý danh mục.
10. Quản lý giá và biến thể.
11. Quản lý tồn kho.
12. Quản lý đơn hàng.
13. Quản lý khách hàng.
14. Quản lý thông báo.
15. Quản lý tư vấn và hội thoại.
16. Quản lý AI Business Intelligence.
17. Báo cáo và thống kê.

Đảm bảo dữ liệu Admin thay đổi phải đồng bộ đúng với Customer Storefront.

## B3. AI STYLIST AGENT

Kiểm thử thực tế:

1. AI hiểu câu hỏi tự nhiên.
2. AI tìm sản phẩm theo giá.
3. AI tìm theo màu sắc.
4. AI tìm theo kích cỡ.
5. AI tìm theo danh mục.
6. AI kết hợp nhiều điều kiện.
7. AI duy trì ngữ cảnh nhiều lượt.
8. AI không tự tạo thông tin sản phẩm.
9. AI trả lời dựa trên dữ liệu thực tế.
10. AI tư vấn phối đồ.
11. AI xử lý khi không có sản phẩm phù hợp.
12. AI xử lý khi sản phẩm hết hàng.
13. AI nhận diện nhu cầu chuyển nhân viên.
14. AI chuyển hội thoại sang Admin.
15. Nhân viên có thể tiếp nhận và trả lời.
16. Tin nhắn được lưu và đồng bộ hai chiều.
17. AI không tiếp tục trả lời khi nhân viên đang xử lý hội thoại nếu thiết kế hiện tại yêu cầu tạm dừng.

## B4. PAYMENT – VNPAY

Kiểm tra:
- Tạo đơn hàng.
- Tạo yêu cầu thanh toán.
- Sinh QR động theo đúng đơn hàng.
- Hiển thị QR.
- Số tiền thanh toán.
- Mã giao dịch.
- Kiểm tra chữ ký.
- Xác thực callback.
- Xử lý thanh toán thành công.
- Xử lý thanh toán thất bại.
- Hủy giao dịch.
- Callback trùng lặp.
- Đối soát trạng thái thanh toán và đơn hàng.
- Không ghi nhận thanh toán thành công khi chưa xác minh hợp lệ.

Sử dụng Sandbox, không thực hiện giao dịch thật.

Đảm bảo không thể thay đổi số tiền thanh toán từ frontend để thanh toán sai giá trị.

## B5. DATABASE VÀ BACKEND

Kiểm tra:

- Kết nối MySQL.
- Prisma schema và migration.
- Quan hệ giữa các bảng.
- API request/response.
- Validation dữ liệu.
- Authentication.
- Authorization.
- Error handling.
- Transaction.
- Tính toàn vẹn dữ liệu.
- Tránh dữ liệu trùng lặp.
- Tối ưu truy vấn.
- Phân quyền Admin và khách hàng.
- Bảo vệ dữ liệu cá nhân.
- Không có API quan trọng chỉ chạy bằng dữ liệu giả.

Đặc biệt kiểm tra việc thêm, sửa, xóa dữ liệu từ Frontend có thực sự cập nhật vào Database và được phản ánh trên các giao diện liên quan hay không.

## B6. AI BUSINESS INTELLIGENCE

Kiểm tra riêng toàn bộ luồng:

1. Admin nhấn nút phân tích.
2. Backend lấy dữ liệu thật.
3. Hệ thống tính toán chỉ số.
4. Gemini nhận dữ liệu tổng hợp.
5. Gemini trả kết quả đúng cấu trúc.
6. Backend xác thực kết quả.
7. Báo cáo được lưu database.
8. Admin xem được báo cáo.
9. Admin xem được căn cứ của từng kiến nghị.
10. Admin cập nhật trạng thái kiến nghị.
11. Admin xem lại lịch sử báo cáo.
12. Báo cáo không thay đổi dữ liệu kinh doanh khi chưa được Admin cho phép.

## B7. TESTING – KIỂM THỬ LIÊN THÔNG END-TO-END

Không chỉ chạy lint hoặc build rồi kết luận hệ thống hoạt động tốt.

Phải thực hiện kiểm thử thực tế theo các kịch bản:

**Kịch bản 1 – Sản phẩm**

Admin thêm sản phẩm → Database lưu thành công → Customer Storefront hiển thị → AI Stylist tìm được sản phẩm → AI Business Intelligence ghi nhận sản phẩm trong dữ liệu phân tích.

**Kịch bản 2 – Đơn hàng**

Khách hàng chọn sản phẩm → Thêm vào giỏ → Đặt hàng → Thanh toán Sandbox → Backend cập nhật đơn hàng → Dashboard cập nhật số liệu doanh thu theo quy tắc ghi nhận.

**Kịch bản 3 – Hành vi khách hàng**

Khách hàng xem sản phẩm → Tìm kiếm → Thêm giỏ → Thanh toán → Hệ thống ghi nhận sự kiện → AI Business Intelligence sử dụng được dữ liệu để phân tích.

**Kịch bản 4 – AI Stylist**

Khách hàng hỏi sản phẩm → AI tìm kiếm → Khách hỏi tiếp về màu sắc → AI duy trì ngữ cảnh → Khách yêu cầu nhân viên → Admin nhận được hội thoại và tiếp nhận.

**Kịch bản 5 – AI Business Intelligence**

Admin chọn thời gian → Nhấn nút phân tích → AI tổng hợp dữ liệu → Tạo kiến nghị → Lưu báo cáo → Admin xem và cập nhật trạng thái.

**Kịch bản 6 – Kiểm soát dữ liệu**

Thử các trường hợp:
- Database không có dữ liệu.
- Dữ liệu thiếu.
- Sản phẩm đã xóa.
- Sản phẩm hết hàng.
- Đơn hàng bị hủy.
- Thanh toán thất bại.
- API timeout.
- Gemini lỗi.
- Admin không đủ quyền.
- Khách hàng cố truy cập API quản trị.

Hệ thống phải xử lý đúng và không bị crash.

## B8. SECURITY VÀ PERFORMANCE

Kiểm tra:
- Không lộ thông tin bí mật.
- Không truy cập trái phép API Admin.
- Không SQL injection.
- Không XSS.
- Không để người dùng sửa dữ liệu của tài khoản khác.
- Kiểm soát upload file.
- Kiểm soát request bất thường.
- Tránh gọi AI liên tục gây phát sinh chi phí.
- Tránh query database quá nặng.
- Tối ưu ảnh và tải dữ liệu.
- Kiểm soát lỗi frontend/backend.
- Không có vòng lặp request hoặc lỗi nghiêm trọng khi tải trang.

---

# PHẦN C. QUY TRÌNH THỰC HIỆN BẮT BUỘC

Không thực hiện tất cả một cách thiếu kiểm soát.

Chia thành các giai đoạn:

**GIAI ĐOẠN 1 – AUDIT SOURCE CODE**
- Đọc repository.
- Xác định kiến trúc.
- Xác định chức năng hiện có.
- Xác định lỗi và phần thiếu.
- Xây dựng danh sách công việc.

**GIAI ĐOẠN 2 – DATA FOUNDATION**
- Kiểm tra dữ liệu bán hàng.
- Kiểm tra tracking.
- Bổ sung tracking còn thiếu.
- Xây dựng các truy vấn tổng hợp.
- Kiểm thử độ chính xác số liệu.

**GIAI ĐOẠN 3 – AI BUSINESS INTELLIGENCE**
- Xây dựng backend.
- Tích hợp Gemini.
- Xây dựng giao diện.
- Lưu lịch sử phân tích.
- Xây dựng kiến nghị.
- Kiểm thử chức năng.

**GIAI ĐOẠN 4 – FULL SYSTEM AUDIT**
- Kiểm tra Frontend.
- Kiểm tra Backend.
- Kiểm tra Database.
- Kiểm tra AI Stylist.
- Kiểm tra Admin.
- Kiểm tra VNPay.
- Kiểm tra các chức năng khác.

**GIAI ĐOẠN 5 – INTEGRATION TEST**
- Kiểm thử các luồng liên thông.
- Sửa các lỗi phát hiện được.
- Chạy lại các bài test liên quan.
- Đánh giá khả năng vận hành thực tế.

**GIAI ĐOẠN 6 – FINAL ACCEPTANCE**
- Build toàn dự án.
- Chạy lint và kiểm tra kiểu dữ liệu nếu có.
- Chạy test tự động.
- Kiểm thử trực tiếp trên trình duyệt.
- Kiểm tra API.
- Kiểm tra Database.
- Tổng hợp bằng chứng.

Nếu phát hiện lỗi, phải sửa và kiểm thử lại. Không chỉ liệt kê lỗi rồi dừng lại.

---

# PHẦN D. TIÊU CHUẨN NGHIỆM THU

Chỉ được đánh dấu PASS khi có bằng chứng kiểm thử.

Báo cáo cuối cùng phải có các nội dung:

1. Kiến trúc hệ thống thực tế.
2. Công nghệ sử dụng.
3. Các module đã kiểm tra.
4. Các chức năng đã triển khai.
5. Các lỗi đã phát hiện.
6. Các lỗi đã sửa.
7. Các chức năng đã kiểm thử thành công.
8. Các chức năng chưa hoàn thiện.
9. Các chức năng bị chặn bởi thiếu API key, môi trường hoặc quyền truy cập.
10. Kết quả build.
11. Kết quả lint.
12. Kết quả test.
13. Kết quả kiểm thử liên thông.
14. Các vấn đề còn tồn tại.
15. Hướng xử lý tiếp theo.

Tạo bảng nghiệm thu:

| Module | Kiểm tra | Kết quả | Bằng chứng |
|---|---|---|---|
| Customer Storefront | UI + API + Database | PASS/FAIL/BLOCKED | Log/Test |
| Admin Portal | CRUD + Permission | PASS/FAIL/BLOCKED | Log/Test |
| AI Stylist | Context + Product Retrieval | PASS/FAIL/BLOCKED | Test case |
| AI Handoff | Chat + Notification | PASS/FAIL/BLOCKED | Test case |
| AI Business Intelligence | Data + Analysis + Recommendation | PASS/FAIL/BLOCKED | Report |
| VNPay | QR + Callback + Signature | PASS/FAIL/BLOCKED | Sandbox |
| Database | Integrity + Migration | PASS/FAIL/BLOCKED | Test |
| Security | Authorization + Validation | PASS/FAIL/BLOCKED | Test |
| Integration | End-to-End | PASS/FAIL/BLOCKED | Test case |

Không được dùng PASS nếu chỉ mới kiểm tra giao diện.

Không được dùng PASS nếu chưa kiểm tra dữ liệu thực tế.

Không được dùng PASS nếu chức năng chỉ hoạt động trên mock data.

Không được che giấu lỗi hoặc ghi nhận hoàn thành khi còn lỗi nghiêm trọng.

**YÊU CẦU CUỐI CÙNG:**

Hãy trực tiếp triển khai AI Business Intelligence và thực hiện kiểm tra, tối ưu toàn bộ Routine E-commerce Platform theo các yêu cầu trên.

Ưu tiên tính đúng đắn của dữ liệu, độ ổn định, khả năng liên thông và chất lượng vận hành thực tế hơn việc hoàn thành nhanh hoặc tạo ra một giao diện đẹp nhưng không có chức năng.

Chỉ kết thúc khi đã thực hiện toàn bộ những gì có thể kiểm thử trong môi trường hiện tại và cung cấp báo cáo nghiệm thu trung thực, có bằng chứng cụ thể.
