# USER MASTER PROMPT #09: 09 REAL DATA AND BUSINESS LOGIC
> **Nguồn gốc:** Prompt chỉ đạo thực tế từ Người dùng (User Request) tại Step 2790.
> **Độ dài gốc:** 18160 ký tự.
> **Mục đích trong thư viện:** Cung cấp toàn văn đặc tả nghiệp vụ, yêu cầu kỹ thuật và ràng buộc sản xuất thực tế mà người dùng đã trực tiếp chỉ đạo và kiểm chứng trong dự án Routine Web.

---

# FINAL PRODUCTION-LIKE DATA & BUSINESS LOGIC COMPLETION – ROUTINE WEB

**Vai trò:** Senior Full-stack Developer, E-commerce System Architect, Database Engineer, Business Analyst và QA Engineer.

**Dự án:** Routine Web.

**Mục tiêu:** Sau khi hoàn thành các đợt sửa lỗi và nghiệm thu kỹ thuật, hãy chuyển Routine Web sang trạng thái một website thương mại điện tử có dữ liệu và quy trình vận hành mô phỏng thực tế.

Tôi không muốn website chỉ có các tài khoản test, sản phẩm test và đơn hàng test đơn giản. Tôi muốn khi mở website, hệ thống thể hiện được hoạt động kinh doanh của một thương hiệu thời trang thực tế: có khách hàng, địa chỉ giao hàng, đơn hàng, doanh thu, thanh toán, vận chuyển, tồn kho, chăm sóc khách hàng và báo cáo quản trị.

Đồng thời, hãy kiểm toán toàn bộ nghiệp vụ thương mại điện tử để tìm ra những chức năng còn thiếu, chưa đúng hoặc chưa hoàn chỉnh.

**Yêu cầu quan trọng: Phải phân biệt dữ liệu mô phỏng với dữ liệu thật. Không được tự tạo thông tin cá nhân rồi tuyên bố đó là khách hàng thật. Không được xóa hoặc làm mất dữ liệu sản phẩm thật đang có.**

---

# PHẦN I. KIỂM KÊ VÀ LÀM SẠCH DỮ LIỆU KIỂM THỬ

## 1. Rà soát toàn bộ dữ liệu hiện có

Kiểm tra tất cả bảng trong Database:

- Users.
- Customers.
- Products.
- Categories.
- Product Images.
- Product Variants.
- Inventory.
- Orders.
- Order Items.
- Payments.
- Shipping.
- Addresses.
- Reviews.
- Wishlists.
- Carts.
- Coupons.
- Promotions.
- Stores.
- CRM.
- Các bảng liên quan khác.

Phân loại dữ liệu:

1. Dữ liệu nền tảng cần giữ.
2. Dữ liệu sản phẩm thật cần giữ.
3. Dữ liệu tài khoản quản trị cần giữ.
4. Dữ liệu nghiệp vụ có nguồn gốc xác thực.
5. Dữ liệu do các lần tự động kiểm thử tạo ra.
6. Dữ liệu demo hoặc dữ liệu mẫu cũ.
7. Dữ liệu không xác định được nguồn gốc.

Không được xóa dữ liệu chỉ dựa trên tên có chứa TEST hoặc DEMO nếu chưa xác định nguồn gốc và quan hệ dữ liệu.

## 2. Xóa dữ liệu tự kiểm thử

Sau khi xác định chính xác dữ liệu được tạo ra từ các lần kiểm thử:

- Xóa tài khoản Customer test không còn cần thiết.
- Xóa đơn hàng test.
- Xóa thanh toán test.
- Xóa giỏ hàng test.
- Xóa địa chỉ test.
- Xóa đánh giá test.
- Xóa các bản ghi giao dịch thử nghiệm.
- Xóa sản phẩm test được tạo riêng cho kiểm thử nếu tôi không yêu cầu giữ lại.
- Xóa dữ liệu phát sinh không còn cần thiết trong các bảng liên quan.

Đảm bảo xử lý Foreign Key và các quan hệ dữ liệu đúng thứ tự.

Không được xóa:
- 37 sản phẩm hiện có trong defaultdb nếu vẫn là dữ liệu cần giữ.
- Danh mục và hình ảnh sản phẩm hợp lệ.
- Tài khoản Admin đang được sử dụng.
- Dữ liệu nghiệp vụ có nguồn gốc thật.
- Các thông tin cấu hình hệ thống.

**Không được sử dụng TRUNCATE, DROP DATABASE hoặc xóa toàn bộ bảng để làm sạch dữ liệu.**

Trước khi xóa:
- Sao lưu Database.
- Xuất danh sách bản ghi dự kiến xóa.
- Đối chiếu số lượng bản ghi.
- Xác định chính xác môi trường Database.

Nếu không thể phân biệt chắc chắn bản ghi nào là dữ liệu test và bản ghi nào là dữ liệu thật, phải dừng xóa và báo cáo, không tự suy đoán.

## 3. Tách biệt môi trường

Tổ chức dữ liệu thành hai môi trường rõ ràng:

- Development/Test: phục vụ lập trình và kiểm thử.
- Demo/Business Simulation: phục vụ trình diễn website với dữ liệu mô phỏng vận hành thực tế.

Nếu chưa có môi trường Production thực sự, hãy tạo môi trường Demo riêng.

Không tự ý biến routine_test_db thành Database sản xuất.

Không ghi dữ liệu mô phỏng vào Database thật khi chưa được phê duyệt.

---

# PHẦN II. XÂY DỰNG BỘ DỮ LIỆU MÔ PHỎNG NHƯ MỘT WEBSITE ĐANG HOẠT ĐỘNG

Sau khi làm sạch dữ liệu test, hãy xây dựng một bộ dữ liệu mô phỏng có tính nhất quán.

## 1. Dữ liệu khách hàng

Tạo tập khách hàng mô phỏng với:

- Họ và tên tiếng Việt.
- Số điện thoại đúng định dạng Việt Nam.
- Email đúng định dạng.
- Giới tính nếu cần.
- Ngày sinh nếu cần.
- Địa chỉ giao hàng.
- Tỉnh/thành phố.
- Phường/xã.
- Thời điểm đăng ký.
- Lịch sử mua hàng.
- Tổng số đơn.
- Tổng giá trị mua.
- Trạng thái tài khoản.

Yêu cầu:
- Dữ liệu có tính đa dạng, tự nhiên.
- Không sử dụng thông tin cá nhân của người thật.
- Không sử dụng số điện thoại của cá nhân hoặc tổ chức không liên quan.
- Không gửi OTP, SMS, email hoặc thông báo tới số điện thoại/email mô phỏng.
- Không tạo tài khoản bằng thông tin có thể bị hiểu nhầm là khách hàng thật.
- Phải đánh dấu nguồn dữ liệu là SYNTHETIC/DEMO trong hệ thống quản trị.

Nếu sử dụng dữ liệu khách hàng thật được cung cấp từ nguồn hợp pháp, phải giữ nguyên nguồn gốc và quyền sử dụng; không tự tạo thêm thông tin cá nhân giả rồi trộn lẫn.

## 2. Dữ liệu đơn hàng

Tạo bộ đơn hàng mô phỏng có trạng thái đa dạng:

- PENDING.
- CONFIRMED.
- PROCESSING.
- READY_TO_SHIP.
- SHIPPING.
- DELIVERED.
- CANCELLED.
- RETURN_REQUESTED.
- RETURNED.
- REFUNDED.

Tên trạng thái có thể điều chỉnh theo quy ước hiện có trong source code.

Mỗi đơn hàng phải có:

- Mã đơn hàng duy nhất.
- Khách hàng.
- Số điện thoại nhận hàng.
- Địa chỉ giao hàng.
- Danh sách sản phẩm.
- Số lượng.
- Đơn giá tại thời điểm mua.
- Giá trị hàng hóa.
- Phí vận chuyển.
- Giảm giá.
- Tổng thanh toán.
- Phương thức thanh toán.
- Trạng thái thanh toán.
- Trạng thái giao hàng.
- Ngày tạo đơn.
- Lịch sử thay đổi trạng thái.

Không tạo đơn hàng mà không có chi tiết đơn.

Không tạo đơn hàng có tổng tiền không khớp với các thành phần.

Không tạo đơn DELIVERED nhưng lại có trạng thái thanh toán PENDING nếu nghiệp vụ hiện tại không cho phép.

Không tạo dữ liệu thanh toán VNPay giả với chữ ký hoặc giao dịch thành công giả.

Các đơn hàng mô phỏng phải được đánh dấu rõ là DEMO và không được hiểu là giao dịch đã thu tiền thật.

## 3. Dữ liệu kinh doanh

Tạo bộ dữ liệu có tính liên kết để các chức năng quản trị có thể phân tích:

- Doanh thu theo ngày.
- Doanh thu theo tuần.
- Doanh thu theo tháng.
- Đơn hàng theo trạng thái.
- Sản phẩm bán chạy.
- Sản phẩm bán chậm.
- Tồn kho.
- Sản phẩm sắp hết hàng.
- Giá trị đơn hàng trung bình.
- Khách hàng mới.
- Khách hàng quay lại.
- Doanh thu theo danh mục.
- Doanh thu theo khu vực.

Dữ liệu mô phỏng phải được tạo theo cùng một bộ quy tắc và có thể truy xuất ngược tới đơn hàng chi tiết.

Không được tạo doanh thu bằng cách cộng những con số không tồn tại trong dữ liệu đơn hàng.

Dashboard, biểu đồ và AI phải đọc từ cùng nguồn dữ liệu thống nhất.

## 4. Số lượng dữ liệu đề xuất

Hãy đề xuất quy mô dữ liệu phù hợp với khả năng của dự án, không tạo dữ liệu quá lớn làm chậm hệ thống.

Có thể bắt đầu với:
- 30–50 khách hàng mô phỏng.
- 60–100 đơn hàng mô phỏng.
- 3–6 tháng dữ liệu lịch sử.
- Các trạng thái đơn hàng đa dạng.
- Các sản phẩm và biến thể liên kết với catalog hiện có.

Đây là dữ liệu mô phỏng để trình diễn, không được trình bày như doanh thu hoặc khách hàng thực tế.

---

# PHẦN III. HOÀN THIỆN TÍNH PHÍ VẬN CHUYỂN THEO VỊ TRÍ KHÔNG PHỤ THUỘC GOOGLE MAPS

Đây là nghiệp vụ cần được thiết kế và kiểm tra kỹ.

Hiện tại tôi chưa muốn phụ thuộc vào Google Maps API để tính khoảng cách và phí ship.

Hãy phân tích và lựa chọn phương án phù hợp với kiến trúc hiện tại.

## 1. Phương án mặc định: Tính phí theo khu vực giao hàng

Xây dựng hệ thống tính phí vận chuyển dựa trên:

- Tỉnh/thành phố.
- Quận/huyện nếu dữ liệu hành chính hiện tại hỗ trợ.
- Phường/xã.
- Khu vực nội thành.
- Khu vực ngoại thành.
- Khu vực tỉnh khác.
- Khu vực xa hoặc đặc biệt.

Không nhất thiết phải sử dụng tọa độ GPS hoặc Google Maps.

Xây dựng bảng cấu hình phí vận chuyển có thể quản trị:

- Khu vực.
- Tỉnh/thành phố.
- Phường/xã nếu cần.
- Phí vận chuyển cơ bản.
- Phí bổ sung.
- Ngưỡng miễn phí vận chuyển.
- Điều kiện áp dụng.
- Thời gian giao hàng dự kiến.
- Trạng thái áp dụng.

Admin có thể cập nhật bảng giá mà không cần sửa code.

## 2. Quy tắc tính phí

Thiết kế công thức:

Phí vận chuyển = Phí cơ bản theo khu vực + Phụ phí hợp lệ - Ưu đãi vận chuyển.

Ví dụ minh họa để thiết kế cấu hình ban đầu:

| Khu vực | Phí tham khảo |
|---|---:|
| Nội thành cùng khu vực kho | 20.000đ |
| Ngoại thành cùng khu vực kho | 30.000đ |
| Tỉnh/thành phố khác | 35.000đ |
| Khu vực xa | 45.000đ |

Đây chỉ là giá trị mẫu, không được tuyên bố là bảng giá của đơn vị vận chuyển thực tế.

Có thể cấu hình miễn phí vận chuyển khi:
- Đơn hàng đạt ngưỡng giá trị nhất định.
- Khách hàng sử dụng mã miễn phí vận chuyển hợp lệ.
- Chương trình khuyến mãi có điều kiện cụ thể.

Ngưỡng miễn phí vận chuyển phải được quản trị thay đổi được.

## 3. Quy trình checkout

Khi khách hàng nhập địa chỉ:

1. Chọn tỉnh/thành phố.
2. Chọn quận/huyện nếu hệ thống sử dụng cấp này.
3. Chọn phường/xã.
4. Nhập địa chỉ chi tiết.
5. Backend xác định khu vực.
6. Backend tính phí vận chuyển.
7. Frontend hiển thị phí ship.
8. Khách hàng nhìn thấy tổng tiền cuối cùng.
9. Khi tạo đơn, Backend tính lại phí ship.
10. Lưu phí vận chuyển tại thời điểm đặt đơn.

Không tin tưởng phí ship do Frontend gửi lên.

Không để khách hàng thay đổi request để tự giảm phí vận chuyển.

Nếu không xác định được địa chỉ hoặc khu vực, phải hiển thị thông báo và yêu cầu chọn lại, không tự áp dụng mức phí thấp nhất.

## 4. Kiến trúc dữ liệu

Kiểm tra và thiết kế các bảng phù hợp:

- ShippingZones.
- ShippingRates.
- ShippingMethods.
- ShippingFeeRules.
- ShippingAddresses.
- Shipments.
- ShippingStatusHistory.

Không tạo bảng trùng lặp nếu dự án đã có cấu trúc tương đương.

Đảm bảo lưu được phí ship của từng đơn hàng tại thời điểm đặt hàng. Khi Admin đổi bảng giá, đơn cũ không bị thay đổi.

## 5. Khả năng nâng cấp API vận chuyển

Thiết kế kiến trúc để sau này có thể tích hợp:

- GHN.
- GHTK.
- Viettel Post.
- Các đơn vị vận chuyển khác.

Nếu tích hợp API vận chuyển:
- Lấy báo giá thực tế.
- Kiểm tra địa chỉ hỗ trợ.
- Tạo vận đơn.
- Lấy mã vận đơn.
- Theo dõi trạng thái.
- Xử lý webhook/callback.

Không được giả lập API bên ngoài rồi tuyên bố đã tích hợp thành công.

Nếu hiện tại chưa có API Key hoặc tài khoản đơn vị vận chuyển, hãy hoàn thiện cơ chế tính phí theo khu vực và ghi rõ phần tích hợp thật đang chờ cấu hình.

## 6. Tính khoảng cách nếu không có Google Maps

Phân tích thêm các phương án:
- Tính phí theo khu vực hành chính.
- Dùng bảng khoảng cách cố định giữa kho và khu vực.
- Dùng dịch vụ định tuyến hoặc bản đồ khác nếu cần.

Không được dùng khoảng cách đường chim bay để tuyên bố là quãng đường giao hàng thực tế.

Nếu sử dụng OpenStreetMap hoặc dịch vụ định tuyến khác, phải kiểm tra giấy phép, giới hạn sử dụng và điều kiện vận hành.

Đưa ra khuyến nghị phù hợp nhất với quy mô Routine Web.

---

# PHẦN IV. HOÀN THIỆN NGHIỆP VỤ ĐƠN HÀNG VÀ VẬN HÀNH

Rà soát và hoàn thiện các chức năng:

## 1. Đặt hàng

- Kiểm tra tồn kho.
- Kiểm tra giá.
- Kiểm tra mã giảm giá.
- Tính phí vận chuyển.
- Tính tổng tiền.
- Lưu snapshot sản phẩm và giá.
- Tạo mã đơn hàng.
- Chống đặt hàng trùng.
- Kiểm tra giao dịch thanh toán.

## 2. Quản lý đơn hàng

Admin cần có thể:

- Xem danh sách.
- Tìm kiếm theo mã đơn.
- Lọc theo thời gian.
- Lọc theo trạng thái.
- Xem thông tin khách hàng.
- Xem sản phẩm.
- Xem phí vận chuyển.
- Xem thanh toán.
- Xác nhận đơn.
- Chuẩn bị hàng.
- Xác nhận giao cho đơn vị vận chuyển.
- Cập nhật mã vận đơn.
- Cập nhật trạng thái.
- Hủy đơn theo điều kiện.
- Xử lý hoàn hàng.
- Xử lý hoàn tiền theo nghiệp vụ được hỗ trợ.

Không cho phép thay đổi trạng thái tùy ý nếu không phù hợp với luồng đơn hàng.

## 3. Tồn kho

Kiểm tra:

- Tồn kho thực tế.
- Tồn kho khả dụng.
- Số lượng đã đặt.
- Số lượng đang giữ.
- Số lượng đã bán.
- Hoàn kho khi đơn bị hủy.
- Cập nhật tồn kho khi đơn giao thành công theo quy tắc nhất quán.
- Chống bán vượt tồn kho.
- Lịch sử nhập và xuất kho.

Không tự động điều chỉnh số lượng tồn kho chỉ để làm đẹp Dashboard.

## 4. Đổi trả và hoàn tiền

Kiểm tra và hoàn thiện:

- Yêu cầu đổi trả.
- Lý do đổi trả.
- Thời hạn đổi trả.
- Trạng thái yêu cầu.
- Quy trình Admin duyệt.
- Nhập lại kho nếu sản phẩm đủ điều kiện.
- Hoàn tiền nếu có thanh toán.
- Lưu lịch sử xử lý.

Không tự tạo chính sách đổi trả nếu chưa có chính sách được xác nhận. Đưa ra cấu hình để Admin có thể quản lý.

---

# PHẦN V. HOÀN THIỆN QUẢN TRỊ KINH DOANH VÀ AI

Rà soát các chức năng AI Business Intelligence riêng biệt với chatbot AI Stylist.

## 1. Báo cáo doanh thu

- Doanh thu gộp.
- Doanh thu thuần.
- Phí vận chuyển.
- Giảm giá.
- Số đơn hàng.
- Giá trị đơn hàng trung bình.
- Tỷ lệ hủy.
- Tỷ lệ hoàn hàng.
- So sánh theo thời gian.

Phải thống nhất cách tính doanh thu và loại trừ đơn hủy, đơn chưa thanh toán hoặc đơn chưa giao theo quy tắc được cấu hình.

Phân biệt doanh thu ghi nhận, doanh thu đã thanh toán và giá trị đơn hàng.

## 2. Kiến nghị nhập hàng

Phân tích:

- Tồn kho hiện tại.
- Lịch sử bán hàng.
- Tốc độ tiêu thụ.
- Số ngày tồn kho.
- Thời gian nhập hàng.
- Tồn kho an toàn.
- Mức độ biến động nhu cầu.

Đề xuất số lượng nhập dựa trên dữ liệu thực tế.

Mỗi kiến nghị phải hiển thị:
- Sản phẩm.
- Tồn kho hiện tại.
- Tốc độ bán.
- Dự báo nhu cầu.
- Số lượng đề xuất.
- Thời gian nên nhập.
- Lý do.
- Mức độ ưu tiên.
- Độ tin cậy hoặc giới hạn của dự báo.

Nếu thiếu dữ liệu lịch sử, phải ghi rõ chưa đủ dữ liệu.

## 3. Phân phối hàng hóa

Đối với các cửa hàng hoặc kho:

- So sánh tồn kho.
- Phát hiện thiếu hàng.
- Phát hiện hàng tồn lâu.
- Đề xuất điều chuyển.
- Đề xuất số lượng.
- Nêu rõ kho xuất và kho nhận.

Không tự động tạo phiếu điều chuyển nếu chưa được Admin phê duyệt.

## 4. AI Marketing

Đề xuất kế hoạch Marketing dựa trên dữ liệu:

- Doanh thu.
- Sản phẩm.
- Khách hàng.
- Mùa vụ.
- Lịch sử bán hàng.
- Hiệu quả chương trình trước đó nếu có.

Kết quả cần có:
- Vấn đề kinh doanh.
- Cơ hội.
- Khách hàng mục tiêu.
- Sản phẩm cần thúc đẩy.
- Insight.
- Big Idea.
- Key Message.
- Kênh truyền thông.
- Ngân sách đề xuất.
- KPI.
- Lịch triển khai.
- Cách đo lường.

Phải phân biệt số liệu lịch sử và giả định lập kế hoạch.

Không tự động chi ngân sách quảng cáo hoặc triển khai chiến dịch.

---

# PHẦN VI. KIỂM TOÁN TOÀN DIỆN WEBSITE – TÌM NHỮNG NGHIỆP VỤ CÒN THIẾU

Không giới hạn việc kiểm tra ở các chức năng đã được liệt kê.

Hãy đóng vai một chuyên gia đánh giá hệ thống thương mại điện tử và rà soát các nhóm sau:

1. Quản lý sản phẩm.
2. Quản lý danh mục.
3. Quản lý biến thể.
4. Quản lý tồn kho.
5. Quản lý kho và cửa hàng.
6. Quản lý khách hàng.
7. Quản lý tài khoản và phân quyền.
8. Quản lý giỏ hàng.
9. Quản lý đơn hàng.
10. Quản lý thanh toán.
11. Quản lý vận chuyển.
12. Quản lý phí ship.
13. Quản lý mã giảm giá.
14. Quản lý khuyến mãi.
15. Đổi trả và hoàn tiền.
16. Đánh giá sản phẩm.
17. Danh sách yêu thích.
18. Chăm sóc khách hàng.
19. CRM.
20. Báo cáo doanh thu.
21. Phân tích tồn kho.
22. Dự báo nhập hàng.
23. Điều phối hàng hóa.
24. AI Stylist.
25. AI Business Intelligence.
26. AI Marketing.
27. SEO.
28. Responsive.
29. Bảo mật.
30. Hiệu năng.
31. Sao lưu và phục hồi.
32. Logging và giám sát hệ thống.

Với mỗi nhóm, hãy đánh giá:

- Đã triển khai chưa?
- Đã có giao diện chưa?
- Đã có API chưa?
- Đã kết nối Database chưa?
- Đã kiểm thử chưa?
- Có hoạt động đúng nghiệp vụ không?
- Có thiếu logic quan trọng không?
- Có cần hoàn thiện không?

Phân loại mức độ:

- CRITICAL: Có thể gây mất dữ liệu, sai tiền, sai thanh toán hoặc lộ thông tin.
- HIGH: Làm hỏng luồng mua hàng hoặc nghiệp vụ cốt lõi.
- MEDIUM: Chức năng chưa hoàn chỉnh hoặc trải nghiệm còn hạn chế.
- LOW: Cải thiện giao diện và tiện ích.

Ưu tiên sửa CRITICAL và HIGH trước.

Không tự ý mở rộng phạm vi bằng các tính năng không cần thiết.

---

# PHẦN VII. KIỂM THỬ SAU KHI HOÀN THIỆN

Thực hiện kiểm thử lại trên giao diện thực tế:

1. Admin đăng nhập.
2. Admin xem Dashboard.
3. Admin quản lý sản phẩm.
4. Admin quản lý khách hàng.
5. Admin quản lý đơn hàng.
6. Admin xem báo cáo doanh thu.
7. Admin xem kiến nghị nhập hàng.
8. Admin xem kiến nghị phân phối.
9. Admin tạo kế hoạch Marketing.
10. Customer đăng ký.
11. Customer đăng nhập.
12. Customer tìm kiếm sản phẩm.
13. Customer xem ảnh và chi tiết.
14. Customer chọn biến thể.
15. Customer thêm giỏ hàng.
16. Customer nhập địa chỉ.
17. Hệ thống tính phí ship.
18. Customer kiểm tra tổng tiền.
19. Customer đặt hàng.
20. Customer thanh toán Sandbox.
21. Admin xử lý đơn.
22. Customer xem trạng thái đơn.
23. Customer gửi yêu cầu đổi trả nếu chức năng được triển khai.
24. Gemini AI Stylist tư vấn.
25. AI Business Intelligence phân tích dữ liệu.

Đối chiếu dữ liệu giữa Frontend, API và Database.

Không đánh dấu PASS chỉ dựa vào việc trang tải được hoặc API trả HTTP 200.

---

# PHẦN VIII. BÀN GIAO CUỐI CÙNG

Tạo các tài liệu:

- `docs/FINAL_DATA_CLEANUP_REPORT.md`
- `docs/DEMO_DATA_DICTIONARY.md`
- `docs/SHIPPING_FEE_DESIGN.md`
- `docs/ECOMMERCE_BUSINESS_AUDIT.md`
- `docs/FINAL_BUSINESS_LOGIC_REPORT.md`
- `docs/FINAL_MANUAL_ACCEPTANCE_GUIDE.md`

Báo cáo rõ:

1. Những dữ liệu test nào đã xóa.
2. Những dữ liệu nào được giữ.
3. Tổng số khách hàng mô phỏng.
4. Tổng số đơn hàng mô phỏng.
5. Tổng số sản phẩm.
6. Tổng số giao dịch mô phỏng.
7. Cách phân biệt dữ liệu thật và mô phỏng.
8. Công thức tính phí vận chuyển.
9. Cách Admin quản lý bảng giá ship.
10. Các chức năng nghiệp vụ đã hoàn thiện.
11. Các chức năng còn thiếu.
12. Các chức năng cần tài khoản/API bên ngoài.
13. Kết quả kiểm thử cuối cùng.
14. Tài khoản đăng nhập để tôi nghiệm thu.
15. Cách khởi động website.

## ĐIỀU KIỆN BÀN GIAO

Tôi cần nhận được một website:

- Có dữ liệu mô phỏng phong phú và nhất quán.
- Không còn dữ liệu tự kiểm thử cũ không cần thiết.
- Có khách hàng và đơn hàng mô phỏng giống tình huống kinh doanh thật.
- Có phí vận chuyển theo địa chỉ.
- Có quy trình mua hàng và xử lý đơn hàng.
- Có báo cáo doanh thu lấy từ dữ liệu đơn hàng.
- Có kiến nghị nhập hàng và phân phối dựa trên dữ liệu.
- Có AI Stylist hoạt động đúng.
- Có AI Business Intelligence hoạt động đúng trong phạm vi dữ liệu hỗ trợ.
- Có giao diện Admin và Customer hoàn chỉnh.
- Có dữ liệu để tôi trực tiếp kiểm tra.

**Không được tuyên bố website đã vận hành thực tế nếu chưa có khách hàng, giao dịch và dữ liệu kinh doanh thật. Đây là môi trường Demo mô phỏng vận hành thực tế.**

**Không tự động chuyển sang Production, không xóa Database thật và không phát sinh giao dịch thật.**

Hãy thực hiện tuần tự, có backup, có bằng chứng và chỉ báo cáo hoàn thành khi toàn bộ điều kiện nghiệm thu đã được xác minh.
