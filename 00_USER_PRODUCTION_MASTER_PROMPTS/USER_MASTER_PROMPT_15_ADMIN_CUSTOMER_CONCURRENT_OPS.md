# USER MASTER PROMPT #15: 15 ADMIN CUSTOMER CONCURRENT OPS
> **Nguồn gốc:** Prompt chỉ đạo thực tế từ Người dùng (User Request) tại Step 6060.
> **Độ dài gốc:** 11992 ký tự.
> **Mục đích trong thư viện:** Cung cấp toàn văn đặc tả nghiệp vụ, yêu cầu kỹ thuật và ràng buộc sản xuất thực tế mà người dùng đã trực tiếp chỉ đạo và kiểm chứng trong dự án Routine Web.

---

# PROMPT ANTIGRAVITY: TRIỂN KHAI HỆ THỐNG ADMIN – CUSTOMER HOẠT ĐỘNG ĐỒNG THỜI VÀ ĐỒNG BỘ DỮ LIỆU

## I. MỤC TIÊU

Nâng cấp Routine Web thành một hệ thống thương mại điện tử hoạt động đồng thời giữa:

**1. Giao diện Admin – Quản trị**
- Quản lý sản phẩm.
- Quản lý danh mục.
- Quản lý hình ảnh.
- Quản lý khách hàng.
- Quản lý đơn hàng.
- Quản lý thanh toán.
- Quản lý tồn kho.
- Quản lý phí vận chuyển.
- Theo dõi hoạt động kinh doanh.

**2. Giao diện Customer – Khách hàng**
- Khách vãng lai không cần đăng nhập.
- Khách hàng đăng ký và đăng nhập.
- Xem sản phẩm.
- Tìm kiếm và lọc sản phẩm.
- Xem chi tiết sản phẩm.
- Thêm giỏ hàng.
- Đặt hàng.
- Thanh toán.
- Theo dõi đơn hàng.
- Sử dụng Gemini AI Stylist.

Hai giao diện phải hoạt động đồng thời, sử dụng chung Backend API và một nguồn dữ liệu MySQL thống nhất.

Không xây dựng hai hệ thống dữ liệu độc lập.

## II. CÁCH CHẠY HỆ THỐNG

Khi khởi động dự án:

- Frontend chạy tại cổng 3000.
- Backend chạy tại cổng 5001.
- MySQL sử dụng kết nối đã cấu hình.
- Gemini AI sử dụng cấu hình hiện tại.

Cho phép mở đồng thời:

**Tab 1:** `http://localhost:3000/admin`

**Tab 2:** `http://localhost:3000/`

Tab 1 đăng nhập tài khoản Admin.

Tab 2 mở trang bán hàng với hai trường hợp:
- Khách vãng lai.
- Khách hàng đã đăng nhập.

Không yêu cầu chạy hai bản Frontend riêng biệt hoặc tạo hai database khác nhau.

Nếu dự án hiện tại sử dụng cấu trúc URL khác, hãy giữ nguyên cấu trúc đang hoạt động và báo lại URL thực tế.

## III. NGUYÊN TẮC ĐỒNG BỘ

Tất cả dữ liệu nghiệp vụ phải được xử lý theo luồng:

Admin/Customer → Backend API → MySQL → Backend trả dữ liệu mới → Các giao diện liên quan cập nhật.

Không sử dụng dữ liệu mẫu tĩnh để giả lập sự đồng bộ.

Không chỉ cập nhật giao diện bằng cách thay đổi state cục bộ mà không lưu dữ liệu vào database.

Mỗi thao tác ghi dữ liệu phải được Backend xác nhận thành công trước khi thông báo hoàn tất.

## IV. ĐỒNG BỘ ADMIN VÀ CUSTOMER

### 1. Quản lý sản phẩm

Khi Admin:
- Thêm sản phẩm.
- Sửa tên sản phẩm.
- Sửa giá.
- Thêm ảnh.
- Thêm màu sắc.
- Thêm kích cỡ.
- Thay đổi tồn kho.
- Ẩn hoặc hiện sản phẩm.
- Xóa mềm sản phẩm.

Customer phải nhận được dữ liệu cập nhật.

Ví dụ:
- Admin thêm áo sơ mi mới → khách tải lại trang chủ sẽ nhìn thấy.
- Admin thay giá → trang sản phẩm hiển thị giá mới.
- Admin thêm màu Beige → khách có thể chọn màu mới và xem ảnh tương ứng.
- Admin chuyển sản phẩm sang INACTIVE → khách không thể đặt mua sản phẩm đó.
- Admin hết hàng → khách nhìn thấy trạng thái hết hàng.

Nếu khách đang mở website, ưu tiên cập nhật tự động mà không cần tải lại trang.

### 2. Quản lý đơn hàng

Khi khách đặt hàng:

Backend phải:
1. Xác thực khách hàng hoặc phiên mua hàng.
2. Kiểm tra sản phẩm và tồn kho.
3. Tính lại giá sản phẩm.
4. Tính giảm giá.
5. Xác thực địa chỉ.
6. Tính phí vận chuyển.
7. Tính tổng thanh toán.
8. Tạo đơn hàng trong MySQL.
9. Cập nhật tồn kho theo quy tắc hiện tại.
10. Phát sự kiện thông báo cho Admin.

Admin phải nhận được:
- Mã đơn hàng.
- Thời gian đặt.
- Tên khách hàng.
- Số điện thoại.
- Sản phẩm và số lượng.
- Tổng tiền hàng.
- Phí vận chuyển.
- Tổng thanh toán.
- Trạng thái đơn hàng.
- Trạng thái thanh toán.

Không tạo đơn hàng trùng khi khách nhấn nút đặt hàng nhiều lần.

### 3. Cập nhật trạng thái đơn hàng

Khi Admin:
- Xác nhận đơn.
- Chuẩn bị hàng.
- Đang giao hàng.
- Giao thành công.
- Hủy đơn.

Customer phải nhìn thấy trạng thái mới trong lịch sử đơn hàng.

Nếu khách đang mở trang theo dõi đơn hàng, ưu tiên cập nhật tự động.

### 4. Đồng bộ khách hàng

Khi khách đăng ký tài khoản:
- MySQL tạo khách hàng mới.
- Admin có thể nhìn thấy khách hàng trong danh sách.
- Thông tin tài khoản phải được liên kết đúng với đơn hàng.

Khách vãng lai:
- Có thể xem sản phẩm và mua hàng theo chính sách hiện tại.
- Không bắt buộc đăng nhập nếu hệ thống cho phép checkout dạng guest.
- Phải có mã phiên hoặc mã định danh giỏ hàng phù hợp.
- Khi đặt hàng phải lưu thông tin người nhận đầy đủ.
- Không tự tạo tài khoản giả cho khách vãng lai.

### 5. Đồng bộ tồn kho

Khi khách đặt mua:
- Backend kiểm tra tồn kho.
- Tránh bán vượt tồn kho khi nhiều khách cùng mua.
- Cập nhật số lượng sau khi đơn được ghi nhận theo quy tắc nghiệp vụ.
- Admin nhìn thấy tồn kho mới.
- Customer nhìn thấy tình trạng còn hàng mới.

Phải xử lý giao dịch database để tránh hai khách cùng mua sản phẩm cuối cùng.

Không trừ tồn kho hai lần khi callback thanh toán được gửi lặp lại.

## V. CƠ CHẾ CẬP NHẬT REAL-TIME

Kiểm tra công nghệ hiện tại trước khi triển khai.

Ưu tiên:
- Socket.IO nếu Backend hiện tại hỗ trợ tốt.
- Server-Sent Events nếu phù hợp với cấu trúc dự án.
- Polling có chu kỳ hợp lý làm phương án dự phòng.

Không tự ý cài nhiều công nghệ cùng lúc nếu không cần thiết.

Các sự kiện cần hỗ trợ:

| Sự kiện | Giao diện nhận thông báo |
|---|---|
| PRODUCT_CREATED | Customer, Admin |
| PRODUCT_UPDATED | Customer, Admin |
| PRODUCT_STATUS_CHANGED | Customer, Admin |
| STOCK_UPDATED | Customer, Admin |
| ORDER_CREATED | Admin |
| ORDER_STATUS_UPDATED | Customer, Admin |
| PAYMENT_CONFIRMED | Customer, Admin |
| CUSTOMER_REGISTERED | Admin |
| SHIPPING_FEE_UPDATED | Checkout, Admin |
| CATEGORY_UPDATED | Customer, Admin |

Yêu cầu:
- Cập nhật dữ liệu khi có sự kiện.
- Không tạo thông báo giả.
- Có xử lý kết nối lại khi mất mạng.
- Khi kết nối lại phải đồng bộ dữ liệu mới nhất.
- Có kiểm tra quyền truy cập khi gửi sự kiện.
- Không gửi thông tin cá nhân hoặc dữ liệu đơn hàng cho người không có quyền.
- Không cho khách hàng truy cập các sự kiện nội bộ dành riêng cho Admin.

Nếu Socket.IO hoặc SSE chưa phù hợp, có thể sử dụng polling và tự động tải lại dữ liệu liên quan.

## VI. THEO DÕI LƯỢT XEM VÀ HOẠT ĐỘNG KHÁCH HÀNG

Xây dựng chức năng thống kê hoạt động trên website để Admin có thể theo dõi:

- Tổng lượt truy cập.
- Số phiên truy cập.
- Lượt xem sản phẩm.
- Lượt xem danh mục.
- Lượt tìm kiếm.
- Lượt thêm vào giỏ hàng.
- Lượt bắt đầu thanh toán.
- Số đơn hàng được tạo.
- Tỷ lệ chuyển đổi.

Phân biệt rõ:
- Lượt xem trang.
- Lượt xem sản phẩm.
- Lượt thêm giỏ.
- Đơn hàng thực tế.
- Thanh toán thành công.

Không tính một lần tải lại trang thành một đơn hàng hoặc một khách hàng mới.

Khách vãng lai có thể được nhận diện bằng session ID hoặc mã định danh ẩn danh phù hợp.

Khách đăng nhập có thể liên kết hoạt động với tài khoản theo chính sách bảo mật.

Không ghi nhận hoặc hiển thị mật khẩu, thông tin thanh toán nhạy cảm hoặc dữ liệu không cần thiết.

Admin có thể xem thống kê tổng hợp và hoạt động gần đây, không mặc định được phép theo dõi mọi nội dung riêng tư của khách hàng.

## VII. DASHBOARD ADMIN CẬP NHẬT

Dashboard phải hiển thị dữ liệu lấy từ MySQL/API:

- Tổng số sản phẩm.
- Sản phẩm đang hiển thị.
- Sản phẩm hết hàng.
- Tổng khách hàng.
- Khách hàng mới.
- Tổng đơn hàng.
- Đơn hàng mới.
- Đơn hàng chờ xác nhận.
- Đơn hàng đã giao.
- Doanh thu.
- Thanh toán thành công.
- Lượt truy cập.
- Lượt xem sản phẩm.
- Lượt thêm giỏ hàng.

Khi khách đặt đơn hoặc có hoạt động mới:
- Số liệu tương ứng được cập nhật.
- Danh sách đơn hàng mới được cập nhật.
- Hiển thị thông báo trong Admin nếu có sự kiện mới.
- Có thời gian ghi nhận rõ ràng.

Phân biệt doanh thu đơn đã thanh toán và giá trị đơn hàng chưa thanh toán. Không cộng đơn hủy hoặc đơn thất bại vào doanh thu thực nhận.

## VIII. ĐỒNG BỘ GEMINI AI

Gemini AI phải truy vấn cùng catalog và trạng thái dữ liệu hiện tại.

Khi Admin thêm hoặc sửa sản phẩm:
- AI tìm thấy sản phẩm mới.
- AI sử dụng giá mới.
- AI sử dụng màu sắc và kích cỡ mới.
- AI không giới thiệu sản phẩm đã ẩn hoặc hết hàng như sản phẩm có thể mua.

Khi khách cần tư vấn:
- AI tìm sản phẩm từ MySQL thông qua Backend Tools.
- AI chỉ trả lời dựa trên dữ liệu được xác thực.
- AI không tự tạo giá, tồn kho, mã sản phẩm.

Khi khách yêu cầu đặt hàng:
- AI có thể hỗ trợ giải thích sản phẩm, địa chỉ và phí vận chuyển.
- Backend thực hiện các phép tính và ghi dữ liệu.
- AI không tự xác nhận thanh toán hoặc tự tạo trạng thái đơn hàng.

## IX. QUY TẮC BẢO MẬT VÀ PHÂN QUYỀN

- Admin và Customer sử dụng phiên đăng nhập riêng.
- Khách không được truy cập API quản trị.
- Khách chỉ được xem đơn hàng của chính mình.
- Khách vãng lai chỉ được truy cập dữ liệu thuộc phiên của họ theo thiết kế hiện tại.
- Admin phải xác thực quyền trước khi thực hiện thao tác quản trị.
- Không tin tưởng dữ liệu giá hoặc tổng tiền từ Frontend.
- Không để khách tự thay đổi trạng thái thanh toán.
- VNPay callback phải được xác minh chữ ký và tính hợp lệ.
- Không gửi dữ liệu cá nhân qua kênh thông báo công khai.
- Không làm lộ thông tin đăng nhập hoặc API key.

## X. KIỂM THỬ THỰC TẾ BẰNG HAI TAB

Không chỉ chạy unit test. Hãy mở trình duyệt và kiểm tra đồng thời.

### Kịch bản 1: Admin thêm sản phẩm

- Tab 1 đăng nhập Admin.
- Tab 2 mở trang chủ Customer.
- Admin thêm sản phẩm mới.
- Kiểm tra MySQL.
- Kiểm tra Tab 2.
- Sản phẩm phải xuất hiện sau khi cập nhật tự động hoặc tải lại trang.

### Kịch bản 2: Admin sửa giá

- Tab 1 sửa giá sản phẩm.
- Tab 2 mở sản phẩm đó.
- Kiểm tra giá mới.
- Kiểm tra giỏ hàng và checkout không sử dụng giá cũ.

### Kịch bản 3: Khách đặt hàng

- Tab 2 đăng nhập khách hàng hoặc sử dụng chế độ khách vãng lai.
- Thêm sản phẩm vào giỏ.
- Nhập địa chỉ.
- Xác thực địa chỉ và tính phí ship.
- Xác nhận đơn hàng.
- Kiểm tra MySQL.
- Tab 1 phải nhận được đơn hàng mới.
- Dashboard phải cập nhật số đơn hàng tương ứng.

### Kịch bản 4: Admin thay đổi trạng thái đơn

- Tab 1 xác nhận đơn hàng.
- Tab 2 mở lịch sử đơn hàng.
- Kiểm tra trạng thái mới được cập nhật.

### Kịch bản 5: Khách đăng ký tài khoản

- Tab 2 đăng ký khách hàng mới.
- Tab 1 kiểm tra danh sách khách hàng.
- Kiểm tra bản ghi trong MySQL.

### Kịch bản 6: Admin ẩn sản phẩm

- Tab 1 chuyển sản phẩm sang INACTIVE.
- Tab 2 tải lại danh mục.
- Sản phẩm không còn được hiển thị hoặc đặt mua.
- Gemini không còn giới thiệu sản phẩm đó như hàng đang bán.

### Kịch bản 7: Hai khách mua cùng sản phẩm

- Mở hai phiên Customer độc lập.
- Cho cả hai cùng thử đặt sản phẩm có tồn kho thấp.
- Backend phải ngăn việc bán vượt tồn kho.
- Kiểm tra database không bị trừ tồn kho hai lần.

### Kịch bản 8: Mất kết nối

- Tạm ngắt kết nối real-time.
- Thực hiện thay đổi ở Admin.
- Khôi phục kết nối.
- Customer phải nhận được dữ liệu mới nhất.

## XI. RÀNG BUỘC

- Không thay đổi Cloudinary.
- Không sửa `.env`, API key hoặc API secret.
- Không đổi thông tin kết nối MySQL.
- Không ghi dữ liệu test vào `defaultdb`.
- Sử dụng `routine_test_db` cho các bài kiểm thử có ghi dữ liệu.
- Không xóa sản phẩm, khách hàng hoặc đơn hàng hợp lệ.
- Không DROP, TRUNCATE hoặc reset database.
- Không tạo thanh toán thật.
- Không tự ý thay đổi các chức năng đang hoạt động.
- Không refactor toàn bộ dự án nếu không cần thiết.
- Kiểm tra Git status trước khi chỉnh sửa và bảo toàn các thay đổi hiện có.

## XII. BÁO CÁO NGHIỆM THU

Tạo file:

`docs/ADMIN_CUSTOMER_REALTIME_SYNC_REPORT.md`

Báo cáo cần có:

1. Cách chạy đồng thời Admin và Customer.
2. URL thực tế của từng giao diện.
3. Các API đã kiểm tra hoặc cập nhật.
4. Các sự kiện real-time đã triển khai.
5. Các bảng MySQL liên quan.
6. Kết quả từng kịch bản kiểm thử.
7. Ảnh chụp hai tab hoạt động đồng thời.
8. Ảnh chụp Admin nhận đơn hàng mới.
9. Ảnh chụp Customer nhìn thấy sản phẩm vừa được Admin thêm.
10. Các lỗi còn tồn tại.

Mỗi kết quả PASS phải có bằng chứng phù hợp từ giao diện, API và MySQL.

**TIÊU CHÍ HOÀN THÀNH:**

Tôi có thể mở cùng lúc hai tab trình duyệt:
- Tab thứ nhất là Admin.
- Tab thứ hai là website bán hàng Customer.

Tôi thực hiện thao tác ở bất kỳ bên nào, dữ liệu nghiệp vụ liên quan phải được lưu vào MySQL và bên còn lại nhận được thay đổi phù hợp.

Không được chỉ tạo hiệu ứng thông báo giả hoặc dữ liệu demo tĩnh để minh họa sự đồng bộ.
