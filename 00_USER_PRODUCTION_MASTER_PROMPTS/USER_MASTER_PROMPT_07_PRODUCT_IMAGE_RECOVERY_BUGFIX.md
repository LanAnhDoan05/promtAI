# USER MASTER PROMPT #07: 07 PRODUCT IMAGE RECOVERY BUGFIX
> **Nguồn gốc:** Prompt chỉ đạo thực tế từ Người dùng (User Request) tại Step 2375.
> **Độ dài gốc:** 7489 ký tự.
> **Mục đích trong thư viện:** Cung cấp toàn văn đặc tả nghiệp vụ, yêu cầu kỹ thuật và ràng buộc sản xuất thực tế mà người dùng đã trực tiếp chỉ đạo và kiểm chứng trong dự án Routine Web.

---

# URGENT BUG FIX – KHÔI PHỤC TOÀN BỘ ẢNH SẢN PHẨM TRÊN ROUTINE WEB

## 1. MÔ TẢ LỖI

Hiện tại, trên giao diện trang chủ dành cho khách hàng, các sản phẩm không hiển thị ảnh sản phẩm thực tế.

Thay vào đó, website đang hiển thị hình đại diện mặc định (placeholder hình người).

Tình trạng này ảnh hưởng trực tiếp đến:
- Trang chủ Customer.
- Khả năng nhận diện sản phẩm.
- Trải nghiệm mua sắm.
- Khả năng xem và lựa chọn sản phẩm của khách hàng.

Tôi cung cấp ảnh chụp màn hình lỗi để bạn đối chiếu.

**Yêu cầu: Khôi phục ảnh sản phẩm thực tế cho toàn bộ sản phẩm trên website, không chỉ sửa một vài sản phẩm mẫu.**

## 2. KIỂM TRA NGUYÊN NHÂN TỪ GỐC

Không được tự suy đoán nguyên nhân và sửa ngẫu nhiên.

Hãy kiểm tra lần lượt các lớp:

### A. Database

- Kiểm tra các bảng sản phẩm và bảng lưu trữ hình ảnh.
- Kiểm tra trường image, images, imageUrl, thumbnail hoặc các trường thực tế đang được dự án sử dụng.
- Kiểm tra đường dẫn ảnh có bị null, rỗng hoặc sai định dạng không.
- Kiểm tra ảnh có liên kết đúng với productId không.
- Kiểm tra dữ liệu ảnh của sản phẩm ACTIVE.
- Kiểm tra các sản phẩm có nhiều ảnh và ảnh đại diện.
- Đối chiếu dữ liệu trong Database với dữ liệu được API trả về.

Không tự ý cập nhật hàng loạt hoặc xóa dữ liệu ảnh trong Database.

### B. Backend và API

Kiểm tra các API trả danh sách sản phẩm:

- API trang chủ.
- API danh mục.
- API tìm kiếm.
- API chi tiết sản phẩm.
- API sản phẩm liên quan.
- API sản phẩm bán chạy hoặc sản phẩm nổi bật nếu có.

Đảm bảo API trả đúng URL ảnh và không làm mất dữ liệu ảnh trong quá trình truy vấn, mapping hoặc serialize response.

Kiểm tra các trường hợp:
- API có dữ liệu ảnh nhưng Frontend không nhận được.
- API trả sai tên trường.
- API chỉ trả một ảnh trong khi sản phẩm có nhiều ảnh.
- API trả URL không đầy đủ.
- API trả URL cũ hoặc đường dẫn không còn tồn tại.

### C. Frontend

Kiểm tra toàn bộ logic hiển thị ảnh:

- Component ProductCard.
- Component ProductGrid.
- Component ProductDetail.
- Component danh sách sản phẩm trang chủ.
- Component danh mục.
- Component tìm kiếm.
- Component ảnh sản phẩm trong giỏ hàng.
- Các component hiển thị sản phẩm liên quan.

Kiểm tra:
- Frontend đang đọc đúng trường ảnh từ API chưa?
- Có bị sai mapping giữa image và images không?
- Có đang vô tình sử dụng placeholder thay cho ảnh thật không?
- Có lỗi Next.js Image hoặc cấu hình remote image không?
- Có lỗi lazy loading không?
- Có lỗi CSS khiến ảnh bị ẩn không?
- Có lỗi xử lý onError khiến tất cả ảnh chuyển về placeholder không?
- Có lỗi cache hoặc dữ liệu cũ không?

### D. Nguồn ảnh

Kiểm tra các nguồn ảnh hiện đang được dự án sử dụng:
- Cloudinary CDN.
- Các ảnh được lưu trong thư mục uploads.
- Các đường dẫn ảnh cũ trong Database.

Kiểm tra khả năng truy cập thực tế của từng URL ảnh.

Đối với Cloudinary:
- Chỉ kiểm tra URL ảnh hiện tại.
- Không thay đổi Cloudinary Cloud Name.
- Không sửa API Key hoặc API Secret.
- Không chỉnh sửa file .env.
- Không cấu hình lại hoặc tích hợp lại Cloudinary.

Nếu URL ảnh bị lỗi, hãy xác định chính xác nguyên nhân trước khi sửa.

## 3. KHÔI PHỤC ẢNH SẢN PHẨM

Sau khi xác định nguyên nhân, hãy sửa tận gốc.

Yêu cầu:

1. Khôi phục đúng ảnh tương ứng với từng sản phẩm.
2. Giữ nguyên tên, mã sản phẩm và thông tin sản phẩm.
3. Không lấy ngẫu nhiên ảnh của sản phẩm khác để thay thế.
4. Không sử dụng cùng một ảnh cho toàn bộ sản phẩm.
5. Không tạo dữ liệu ảnh giả.
6. Không xóa các ảnh hiện có.
7. Không tự ý thay đổi giá, danh mục, màu sắc, kích cỡ hoặc tồn kho.
8. Nếu một sản phẩm thực sự chưa có ảnh, phải ghi nhận rõ và chỉ hiển thị placeholder cho sản phẩm đó.

Nếu dữ liệu ảnh đang lưu sai đường dẫn, hãy khôi phục mapping đúng từ nguồn ảnh hiện có.

Nếu Frontend đang đọc sai trường dữ liệu, hãy sửa mapping tại component hoặc lớp xử lý dữ liệu phù hợp.

Nếu API làm mất dữ liệu ảnh, hãy sửa Backend.

Không chỉ sửa biểu hiện ở giao diện mà phải khắc phục nguyên nhân ở đúng tầng hệ thống.

## 4. KIỂM TRA TOÀN BỘ GIAO DIỆN CUSTOMER

Sau khi sửa, phải kiểm tra thực tế trên trình duyệt:

- Trang chủ.
- Danh sách sản phẩm.
- Danh mục.
- Tìm kiếm.
- Sản phẩm nổi bật.
- Sản phẩm bán chạy.
- Sản phẩm liên quan.
- Chi tiết sản phẩm.
- Giỏ hàng.
- Danh sách yêu thích nếu có.
- Các trang khác có hiển thị hình ảnh sản phẩm.

Đảm bảo:
- Ảnh hiển thị đúng sản phẩm.
- Không bị vỡ ảnh.
- Không bị kéo giãn hoặc méo tỷ lệ.
- Không bị cắt mất phần quan trọng của sản phẩm.
- Không xuất hiện placeholder khi sản phẩm đã có ảnh hợp lệ.
- Khi tải lại trang, ảnh vẫn hiển thị.
- Khi chuyển trang hoặc lọc sản phẩm, ảnh vẫn hoạt động.

Kiểm tra cả Desktop và Mobile.

## 5. KIỂM TRA SAU KHI ADMIN CẬP NHẬT ẢNH

Thực hiện một luồng kiểm thử:

1. Admin mở một sản phẩm đang có.
2. Cập nhật ảnh bằng chức năng hiện tại.
3. Lưu sản phẩm.
4. Kiểm tra Database lưu đúng URL ảnh.
5. Kiểm tra API trả URL mới.
6. Mở trang chủ Customer.
7. Xác nhận sản phẩm hiển thị ảnh mới.
8. Mở trang chi tiết sản phẩm.
9. Xác nhận ảnh chi tiết cũng được cập nhật.
10. Tải lại trình duyệt để kiểm tra dữ liệu vẫn chính xác.

Không sửa hoặc cấu hình lại Cloudinary trong quá trình kiểm thử.

## 6. KIỂM THỬ TỰ ĐỘNG VÀ ĐỐI CHIẾU

Hãy tạo một bài kiểm thử để rà soát toàn bộ sản phẩm đang ACTIVE.

Với mỗi sản phẩm, ghi nhận:

- Product ID.
- Product Name.
- Image URL trong Database.
- Image URL API trả về.
- Image URL Frontend sử dụng.
- HTTP status của ảnh nếu kiểm tra được.
- Ảnh có thực sự hiển thị trên trình duyệt không.

Phân loại:
- PASS: Ảnh đúng sản phẩm và hiển thị được.
- FAIL: Có ảnh trong Database nhưng không hiển thị.
- MISSING: Sản phẩm thực sự chưa có ảnh.
- INVALID URL: Đường dẫn ảnh không truy cập được.
- WRONG MAPPING: Ảnh không thuộc sản phẩm tương ứng.

Không được đánh dấu PASS chỉ vì Database có URL ảnh.

## 7. AN TOÀN DỮ LIỆU

- Chỉ sử dụng routine_test_db cho mọi thao tác ghi thử nghiệm.
- Không sửa hoặc xóa dữ liệu trong defaultdb.
- Không thực hiện migration phá hủy.
- Không thay đổi cấu hình Cloudinary.
- Không ghi lộ thông tin bảo mật.
- Không làm ảnh hưởng các chức năng Admin, Customer và Gemini AI đang hoạt động.

## 8. BÁO CÁO SAU KHI SỬA

Tạo tài liệu:

`docs/PRODUCT_IMAGE_RECOVERY_REPORT.md`

Báo cáo gồm:

1. Nguyên nhân chính xác gây mất ảnh.
2. File và component đã sửa.
3. API liên quan đã sửa.
4. Tình trạng dữ liệu ảnh trong Database.
5. Tổng số sản phẩm ACTIVE đã kiểm tra.
6. Số ảnh hiển thị thành công.
7. Số ảnh bị lỗi.
8. Số sản phẩm thực sự thiếu ảnh.
9. Ảnh chụp màn hình trước và sau khi sửa.
10. Kết quả kiểm thử trang chủ, danh mục, tìm kiếm, chi tiết sản phẩm và giỏ hàng.

## 9. ĐIỀU KIỆN HOÀN THÀNH

Chỉ được kết thúc khi:

- Ảnh sản phẩm thực tế đã xuất hiện trở lại trên trang chủ.
- Toàn bộ sản phẩm ACTIVE có ảnh hợp lệ đều hiển thị đúng.
- Ảnh đúng với từng sản phẩm.
- Không còn lỗi mapping ảnh.
- Các trang Customer liên quan đều hiển thị ảnh chính xác.
- Ảnh vẫn hiển thị sau khi tải lại trang.
- Chức năng Admin cập nhật ảnh vẫn hoạt động.
- Không ảnh hưởng Database thật và các chức năng khác.

**ƯU TIÊN CAO NHẤT: Hãy trực tiếp mở trình duyệt, kiểm tra trang chủ và xác nhận ảnh sản phẩm đã hiển thị trở lại. Không chỉ sửa code rồi báo hoàn thành.**
