# USER MASTER PROMPT #29: 29 BI DASHBOARD TABLES UI OPTIMIZATION
> **Nguồn gốc:** Prompt chỉ đạo thực tế từ Người dùng (User Request) tại Step 12457.
> **Độ dài gốc:** 7085 ký tự.
> **Mục đích trong thư viện:** Cung cấp toàn văn đặc tả nghiệp vụ, yêu cầu kỹ thuật và ràng buộc sản xuất thực tế mà người dùng đã trực tiếp chỉ đạo và kiểm chứng trong dự án Routine Web.

---

# TASK: FIX & OPTIMIZE BUSINESS INTELLIGENCE DASHBOARD TABLE UI
## ROUTINE E-COMMERCE PLATFORM

### 1. VẤN ĐỀ HIỆN TẠI

Kiểm tra giao diện Dashboard phân tích kinh doanh trong Admin Portal, đặc biệt hai khu vực:

1. **Sản Phẩm Bán Chạy & Tỷ Trọng Doanh Thu**
2. **Sản Phẩm Được Quan Tâm & Tỷ Lệ Xem/Mua**

Giao diện hiện tại đang gặp các vấn đề:

- Bảng có chiều rộng vượt quá khung chứa.
- Các cột bên phải bị tràn và bị cắt khỏi màn hình.
- Tên sản phẩm chiếm quá nhiều diện tích.
- Các cột số liệu không được phân bổ chiều rộng hợp lý.
- Hai bảng không hiển thị đầy đủ nội dung trong khu vực Dashboard.
- Giao diện chưa thích ứng tốt với kích thước màn hình khác nhau.

Yêu cầu sửa trực tiếp trên source code hiện tại, xác định chính xác component, CSS và cấu trúc layout gây ra lỗi. Không tạo một giao diện demo thay thế.

### 2. TỐI ƯU LAYOUT TỔNG THỂ

Giữ hai bảng thống kê nằm cạnh nhau trên desktop nếu không gian cho phép.

Yêu cầu:

- Hai khung thống kê phải nằm gọn trong vùng nội dung Dashboard.
- Không được vượt quá chiều rộng của parent container.
- Sử dụng layout Grid hoặc Flexbox phù hợp.
- Thiết lập `min-width: 0` cho các phần tử con cần co giãn.
- Kiểm tra `width`, `max-width`, `min-width`, `flex`, `grid-template-columns` và `box-sizing`.
- Không sử dụng chiều rộng cố định quá lớn khiến bảng tràn khỏi màn hình.
- Khoảng cách giữa hai khung phải đồng nhất.
- Padding trong khung được cân đối.
- Tiêu đề không bị tràn hoặc xuống dòng bất hợp lý.

Desktop:
- Hai bảng hiển thị song song.
- Chiều rộng hai bảng được phân bổ hợp lý.
- Không xuất hiện thanh cuộn ngang của toàn bộ Dashboard.

Tablet:
- Cho phép hai bảng co giãn hoặc chuyển thành hai hàng tùy theo chiều rộng thực tế.

Mobile:
- Hai bảng xếp thành một cột.
- Không ép hai bảng hiển thị cạnh nhau trên màn hình nhỏ.

### 3. THIẾT KẾ LẠI BẢNG SẢN PHẨM BÁN CHẠY

Tiêu đề: **Sản Phẩm Bán Chạy & Tỷ Trọng Doanh Thu**

Các cột cần giữ:

| Cột | Nội dung |
|---|---|
| Sản phẩm | Tên sản phẩm |
| Đã bán | Số lượng bán |
| Doanh thu | Tổng doanh thu |
| Tỷ trọng | Tỷ trọng doanh thu |

Yêu cầu thiết kế:

- Cột tên sản phẩm được phép co giãn và chiếm phần diện tích lớn nhất.
- Tên sản phẩm dài được hiển thị tối đa 2 dòng hoặc ellipsis có tooltip xem đầy đủ.
- Không để tên sản phẩm đẩy các cột số liệu ra khỏi khung.
- Cột số lượng bán căn chỉnh thống nhất.
- Cột doanh thu căn chỉnh dễ đọc, sử dụng định dạng tiền Việt Nam.
- Cột tỷ trọng hiển thị rõ ràng bằng phần trăm.
- Có thể dùng progress indicator nhỏ bên cạnh tỷ trọng nếu phù hợp với thiết kế hiện tại.
- Các hàng có chiều cao đồng nhất.
- Đường phân cách hàng mảnh, không quá đậm.
- Header và nội dung phải thẳng hàng chính xác.

### 4. THIẾT KẾ LẠI BẢNG SẢN PHẨM ĐƯỢC QUAN TÂM

Tiêu đề: **Sản Phẩm Được Quan Tâm & Tỷ Lệ Xem/Mua**

Các cột cần giữ theo dữ liệu hiện có:

| Cột | Nội dung |
|---|---|
| Sản phẩm | Tên sản phẩm |
| Lượt xem | Số lượt xem |
| Lượt mua | Số lượt mua |
| Tỷ lệ xem/mua | Tỷ lệ chuyển đổi tương ứng nếu đã có dữ liệu hợp lệ |

Yêu cầu:

- Cột sản phẩm chiếm phần chiều rộng lớn nhất.
- Các cột số liệu có chiều rộng phù hợp với nội dung.
- Không để các cột bị cắt.
- Định dạng số liệu đồng nhất.
- Hiển thị tỷ lệ theo phần trăm nếu dữ liệu và công thức đã được xác định.
- Khi không có lượt xem hoặc không đủ dữ liệu, hiển thị trạng thái phù hợp thay vì tự tạo tỷ lệ.
- Có tooltip nếu cần giải thích chỉ số.

Lưu ý: Phải kiểm tra chính xác cấu trúc dữ liệu hiện tại. Không tự ý thay đổi ý nghĩa của cột hoặc công thức tính toán.

### 5. XỬ LÝ TRƯỜNG HỢP BẢNG CẦN NHIỀU CHIỀU RỘNG

Ưu tiên giải pháp responsive và phân bổ cột hợp lý để toàn bộ dữ liệu có thể đọc được.

Nếu trên một số màn hình nhỏ bảng vẫn không đủ chiều rộng:

- Chỉ cho phép cuộn ngang bên trong vùng bảng.
- Không làm toàn bộ trang Dashboard cuộn ngang.
- Thanh cuộn phải thuộc đúng khu vực bảng.
- Có thể cố định cột tên sản phẩm khi cuộn ngang nếu phù hợp.
- Header và nội dung phải cuộn đồng bộ.
- Không cắt mất dữ liệu hoặc ẩn các cột quan trọng một cách âm thầm.

Không sử dụng `overflow: hidden` để che phần bảng bị tràn và coi đó là đã sửa lỗi.

### 6. TỐI ƯU UI/UX

Giữ phong cách quản trị chuyên nghiệp của Routine.

Không:
- Tự ý thay đổi bộ nhận diện thương hiệu.
- Sử dụng gradient màu sắc không cần thiết.
- Tạo quá nhiều card hoặc hiệu ứng.
- Thêm animation gây mất tập trung.
- Làm giao diện giống template AI tạo sẵn.
- Tăng kích thước chữ hoặc padding quá mức.
- Làm mất các thông tin thống kê hiện tại.

Cần:
- Typography rõ ràng.
- Tiêu đề bảng có thứ bậc phù hợp.
- Căn chỉnh số liệu nhất quán.
- Khoảng cách giữa các thành phần cân đối.
- Màu sắc tỷ trọng và trạng thái dễ nhận biết.
- Giao diện thống nhất với các khu vực Admin khác.

### 7. BẢO TOÀN DỮ LIỆU VÀ CHỨC NĂNG

Đây là yêu cầu bắt buộc.

Không được chỉ sửa giao diện mà làm sai dữ liệu.

Phải đảm bảo:

- Tên sản phẩm lấy từ database.
- Số lượng bán lấy từ dữ liệu đơn hàng hợp lệ.
- Doanh thu tính theo quy tắc ghi nhận doanh thu của hệ thống.
- Tỷ trọng doanh thu được tính chính xác.
- Lượt xem được lấy từ hệ thống tracking thực tế.
- Lượt mua được lấy từ dữ liệu đơn hàng phù hợp.
- Không sử dụng dữ liệu hardcode.
- Không tạo sản phẩm giả để lấp đầy bảng.
- Không thay đổi API hoặc database nếu không cần thiết.

Nếu phát hiện số liệu đang sai, phải xác định nguyên nhân và báo cáo riêng, không tự sửa công thức theo suy đoán.

### 8. KIỂM THỬ RESPONSIVE VÀ NGHIỆM THU

Sau khi sửa, phải chạy website và kiểm tra trực tiếp ít nhất các kích thước sau:

- Desktop rộng: 1920px.
- Desktop tiêu chuẩn: 1440px.
- Laptop: 1366px.
- Tablet: 768px.
- Mobile: 390px.

Kiểm tra:

1. Hai bảng không tràn khỏi khung.
2. Tất cả tiêu đề cột đều hiển thị.
3. Các giá trị số liệu không bị cắt.
4. Tên sản phẩm dài được xử lý đúng.
5. Không xuất hiện horizontal overflow ở toàn bộ Dashboard.
6. Nếu có cuộn ngang, chỉ vùng bảng được cuộn.
7. Hai bảng không chồng lấn lên nhau.
8. Giao diện không bị vỡ khi dữ liệu có nhiều ký tự.
9. Các bảng vẫn hiển thị đúng khi dữ liệu thay đổi.
10. Các chức năng tải dữ liệu, lọc và phân trang hiện có vẫn hoạt động.

Chạy lại các kiểm tra build, lint và test phù hợp với dự án.

### 9. YÊU CẦU BÁO CÁO HOÀN THÀNH

Sau khi triển khai, báo cáo:

- Component và file CSS đã chỉnh sửa.
- Nguyên nhân chính gây tràn bảng.
- Giải pháp layout đã áp dụng.
- Các kích thước màn hình đã kiểm thử.
- Kết quả kiểm thử dữ liệu.
- Kết quả build và lint.
- Các lỗi còn tồn tại nếu có.

Chỉ báo PASS khi đã chạy giao diện thực tế và xác nhận không còn lỗi tràn, cắt nội dung hoặc lệch cột.

**MỤC TIÊU CUỐI CÙNG:** Hai bảng thống kê phải hiển thị chuyên nghiệp, cân đối, đọc được toàn bộ dữ liệu, không tràn khỏi Dashboard trên desktop và thích ứng tốt trên tablet/mobile. Giữ nguyên nghiệp vụ, dữ liệu và kiến trúc hiện tại của Routine.
