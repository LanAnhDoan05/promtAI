# USER MASTER PROMPT #12: 12 ROUTINE VN CATALOG SCRAPING
> **Nguồn gốc:** Prompt chỉ đạo thực tế từ Người dùng (User Request) tại Step 3385.
> **Độ dài gốc:** 7454 ký tự.
> **Mục đích trong thư viện:** Cung cấp toàn văn đặc tả nghiệp vụ, yêu cầu kỹ thuật và ràng buộc sản xuất thực tế mà người dùng đã trực tiếp chỉ đạo và kiểm chứng trong dự án Routine Web.

---

# PROMPT ANTIGRAVITY: TỰ ĐỘNG DUYỆT ROUTINE.VN, THU THẬP ẢNH VÀ BỔ SUNG SẢN PHẨM VÀO ROUTINE WEB

## I. MỤC TIÊU

Hãy trực tiếp sử dụng trình duyệt để truy cập website chính thức:

https://routine.vn/

Nhiệm vụ của bạn là duyệt website như một khách hàng thực tế, lần lượt truy cập các danh mục và trang chi tiết sản phẩm, thu thập thông tin cùng hình ảnh sản phẩm được phép sử dụng, sau đó bổ sung vào dự án Routine Web hiện tại.

Mục tiêu cuối cùng: hoàn thiện kho sản phẩm và hình ảnh trên website demo, giúp giao diện trông đầy đủ, phong phú và chuyên nghiệp hơn khi thuyết trình trên lớp.

Không chỉ đưa ra hướng dẫn. Hãy trực tiếp thực hiện các thao tác trong trình duyệt, code, database và kiểm thử.

## II. BƯỚC 1: TRUY CẬP VÀ DUYỆT WEBSITE ROUTINE

Mở trình duyệt và truy cập https://routine.vn/.

Thực hiện lần lượt:

1. Truy cập trang chủ.
2. Cuộn từ đầu đến cuối trang.
3. Mở danh mục Nam.
4. Mở danh mục Nữ.
5. Mở danh mục Trẻ em nếu có.
6. Tiếp tục duyệt các danh mục con.
7. Mở danh sách sản phẩm.
8. Chuyển qua các trang tiếp theo bằng phân trang hoặc nút xem thêm.
9. Mở từng trang chi tiết sản phẩm.
10. Quan sát các ảnh sản phẩm, màu sắc và thông tin chi tiết.

Không chỉ lấy các sản phẩm xuất hiện ở trang đầu tiên. Hãy tiếp tục duyệt các trang tiếp theo để thu thập được nhiều sản phẩm nhất có thể.

Ưu tiên các nhóm:
- Áo sơ mi.
- Áo thun.
- Áo polo.
- Áo khoác.
- Quần dài.
- Quần short.
- Quần jeans.
- Váy và đầm.
- Sản phẩm phụ kiện.
- Các nhóm sản phẩm nổi bật khác trên website.

Nếu website có bộ lọc theo giới tính, loại sản phẩm, màu sắc hoặc bộ sưu tập, hãy sử dụng để khám phá đầy đủ danh mục.

Nếu website yêu cầu đăng nhập, CAPTCHA hoặc có cơ chế bảo vệ, không tìm cách vượt qua. Chuyển sang thu thập những nội dung công khai có thể truy cập.

## III. BƯỚC 2: THU THẬP THÔNG TIN SẢN PHẨM

Với mỗi sản phẩm truy cập được, thu thập:

- Tên sản phẩm.
- Mã SKU.
- Giá bán.
- Giá gốc nếu có.
- Danh mục.
- Giới tính.
- Mô tả sản phẩm.
- Chất liệu.
- Kiểu dáng.
- Màu sắc.
- Kích cỡ.
- Các biến thể sản phẩm.
- URL trang sản phẩm.
- Danh sách ảnh sản phẩm.

Phải ghi nhận ảnh theo từng màu sắc, tránh trường hợp sản phẩm có nhiều màu nhưng tất cả card đều hiển thị một ảnh không tương ứng.

Không tự suy đoán giá, chất liệu, SKU, kích cỡ hoặc thông tin chưa có trên website.

## IV. BƯỚC 3: THU THẬP VÀ LƯU ẢNH SẢN PHẨM

Đối với mỗi sản phẩm, cần xác định:

1. Ảnh đại diện.
2. Ảnh mặt trước.
3. Ảnh mặt sau nếu có.
4. Ảnh chi tiết chất liệu hoặc thiết kế.
5. Ảnh theo từng màu sắc.
6. Các ảnh bổ sung trong gallery.

Yêu cầu:

- Ưu tiên ảnh có độ phân giải cao.
- Không lấy thumbnail 80x100 hoặc ảnh quá nhỏ làm ảnh đại diện.
- Giữ nguyên tỷ lệ và chất lượng ảnh.
- Không tự tạo ảnh giả để thay thế ảnh sản phẩm thật.
- Không tải ảnh trùng lặp.
- Lưu tên file có SKU và màu sắc để dễ quản lý.
- Chỉ tải và sử dụng tài nguyên trong phạm vi được phép; không vượt cơ chế bảo vệ hoặc giới hạn truy cập của website.

Nếu có quyền sử dụng tài nguyên, lưu ảnh vào hệ thống lưu trữ hiện có của dự án. Nếu chưa có quyền, lưu danh sách URL tham khảo và đánh dấu cần được cấp quyền trước khi đưa vào website công khai.

**LƯU Ý QUAN TRỌNG:**
Không thay đổi cấu hình Cloudinary, không sửa `.env`, không thay API key hoặc API secret. Tận dụng hệ thống lưu ảnh hiện tại nếu cần và được phép sử dụng.

## V. BƯỚC 4: ĐỐI CHIẾU VỚI DATABASE HIỆN TẠI

Trước khi thêm sản phẩm, kiểm tra database.

Đối chiếu theo thứ tự:
1. SKU.
2. Tên sản phẩm.
3. Các biến thể.
4. Màu sắc.

Phân loại thành:

- Sản phẩm đã tồn tại và đầy đủ ảnh.
- Sản phẩm đã tồn tại nhưng thiếu ảnh.
- Sản phẩm đã tồn tại nhưng thiếu ảnh theo màu.
- Sản phẩm chưa tồn tại.
- Sản phẩm trùng hoặc có nguy cơ trùng dữ liệu.

Cách xử lý:

- Nếu sản phẩm đã có và thiếu ảnh: bổ sung ảnh còn thiếu.
- Nếu sản phẩm đã có nhưng sai ảnh: chỉ thay ảnh khi xác định đúng sản phẩm và có quyền sử dụng ảnh thay thế.
- Nếu sản phẩm chưa có: tạo sản phẩm mới.
- Nếu có SKU trùng: tuyệt đối không tạo bản ghi mới.
- Không xóa sản phẩm hiện tại chỉ vì sản phẩm đó không xuất hiện trên website nguồn.

## VI. BƯỚC 5: BỔ SUNG SẢN PHẨM VÀO ROUTINE WEB

Thực hiện bổ sung vào database và giao diện hiện tại.

Mỗi sản phẩm mới phải có:
- Tên sản phẩm.
- SKU duy nhất.
- Giá bán.
- Danh mục.
- Mô tả.
- Hình ảnh đại diện.
- Gallery ảnh.
- Màu sắc.
- Kích cỡ.
- Biến thể tương ứng.
- Trạng thái hiển thị phù hợp.

Đảm bảo sản phẩm được đồng bộ đến:

1. Trang chủ.
2. Trang danh mục.
3. Trang danh sách sản phẩm.
4. Trang tìm kiếm.
5. Trang chi tiết.
6. Khu vực sản phẩm liên quan.
7. Admin quản lý sản phẩm.
8. Gemini AI Stylist.

Không tạo dữ liệu frontend giả lập. Sản phẩm phải được lưu và truy xuất từ database thông qua API hiện tại.

Không tự đặt tồn kho là có hàng nếu chưa có dữ liệu. Với sản phẩm phục vụ demo, nếu cần tồn kho giả lập, phải đánh dấu rõ là dữ liệu DEMO.

## VII. BƯỚC 6: HOÀN THIỆN GIAO DIỆN PRODUCT CARD

Sau khi bổ sung, kiểm tra từng product card.

Mỗi card cần:
- Ảnh đại diện rõ nét.
- Tên sản phẩm.
- Giá bán.
- Giá khuyến mại nếu có.
- Màu sắc nếu có.
- Hiệu ứng khi di chuột.
- Liên kết đúng đến trang chi tiết.

Đảm bảo:
- Các card đồng đều về kích thước.
- Ảnh không bị méo.
- Không có ảnh bị vỡ.
- Không có ảnh sai màu sản phẩm.
- Không có sản phẩm trùng lặp.
- Giao diện đẹp trên desktop và mobile.

## VIII. BƯỚC 7: KIỂM THỬ

Sau khi hoàn thành, trực tiếp chạy website và kiểm tra:

1. Sản phẩm mới có xuất hiện trên trang chủ không?
2. Sản phẩm có xuất hiện đúng danh mục không?
3. Ảnh có tải thành công không?
4. Chọn màu có đổi đúng ảnh không?
5. Mở chi tiết có đúng sản phẩm không?
6. Tìm kiếm theo tên và SKU có hoạt động không?
7. Admin có quản lý được sản phẩm vừa thêm không?
8. Gemini AI có tìm kiếm và giới thiệu đúng sản phẩm không?
9. Số lượng sản phẩm trên Admin có cập nhật không?
10. Không có dữ liệu sản phẩm cũ bị mất hoặc ghi đè ngoài ý muốn.

## IX. QUY ĐỊNH AN TOÀN

- Không sửa cấu hình Cloudinary.
- Không sửa `.env`.
- Không để lộ thông tin đăng nhập hoặc API key.
- Không xóa dữ liệu sản phẩm hợp lệ.
- Không chạy DROP DATABASE, TRUNCATE hoặc reset database.
- Không ghi dữ liệu thử nghiệm vào database `defaultdb`.
- Nếu cần thêm dữ liệu demo, chỉ sử dụng database demo/test.
- Không tự ý thay đổi chức năng đang hoạt động tốt.
- Không refactor toàn bộ dự án.
- Không tự nhận rằng ảnh đã được tải và lưu thành công nếu chưa kiểm tra file thực tế.
- Không sử dụng tài nguyên hình ảnh khi chưa có quyền phù hợp.

## X. BÁO CÁO SAU KHI HOÀN THÀNH

Tạo file:

`docs/ROUTINE_PRODUCT_IMPORT_REPORT.md`

Báo cáo gồm:

| Chỉ số | Kết quả |
|---|---|
| Số danh mục đã duyệt | |
| Số trang sản phẩm đã duyệt | |
| Số sản phẩm đã thu thập thông tin | |
| Số sản phẩm mới bổ sung | |
| Số sản phẩm cũ được bổ sung ảnh | |
| Số ảnh đã lưu thành công | |
| Số ảnh chưa thể sử dụng do quyền truy cập/quyền sử dụng | |
| Số sản phẩm còn thiếu dữ liệu | |
| Số lỗi phát sinh | |

Đính kèm:
- Danh sách SKU đã thêm.
- Danh sách sản phẩm đã cập nhật ảnh.
- Danh sách ảnh bị lỗi.
- Ảnh chụp giao diện trước và sau.
- Kết quả kiểm thử trên trang chủ, danh mục, chi tiết và Admin.

**YÊU CẦU THỰC HIỆN:** Hãy thực hiện tuần tự từ bước 1 đến bước 10. Không dừng lại ở việc lập kế hoạch. Nếu một thao tác không thực hiện được, ghi rõ nguyên nhân, tiếp tục các phần còn lại có thể thực hiện và không tự ý phá vỡ dữ liệu hiện tại.
