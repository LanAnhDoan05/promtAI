# USER MASTER PROMPT #02: 02 CLOUDINARY ADMIN PRODUCT MANAGEMENT
> **Nguồn gốc:** Prompt chỉ đạo thực tế từ Người dùng (User Request) tại Step 247.
> **Độ dài gốc:** 11403 ký tự.
> **Mục đích trong thư viện:** Cung cấp toàn văn đặc tả nghiệp vụ, yêu cầu kỹ thuật và ràng buộc sản xuất thực tế mà người dùng đã trực tiếp chỉ đạo và kiểm chứng trong dự án Routine Web.

---

# FINAL TASK – ROUTINE WEB
## TÍCH HỢP CLOUDINARY + HOÀN THIỆN ADMIN PRODUCT MANAGEMENT

Bạn tiếp tục làm việc trên dự án Routine Web hiện tại.

Đây là giai đoạn hoàn thiện chức năng quản trị sản phẩm trước khi demo. Không xây dựng lại dự án, không làm lại những chức năng đã hoàn thành.

**Mục tiêu quan trọng nhất: Admin có thể thêm một sản phẩm hoàn chỉnh, tải ảnh lên Cloudinary, lưu vào MySQL và sản phẩm tự động xuất hiện chính xác trên website khách hàng.**

---

# I. BỐI CẢNH DỰ ÁN – GIỮ NGUYÊN CÁC CHỨC NĂNG ĐÃ HOÀN THÀNH

Dựa trên báo cáo `FINAL_DEMO_STATUS.md`, trạng thái dự án hiện tại:

### 1. Database MySQL

- Database: `defaultdb`.
- Tổng sản phẩm: 37.
- ACTIVE: 34.
- INACTIVE: 3.
- DRAFT: 0.
- Categories: 26.
- Stores: 25.
- Media files: 96.
- Tổng đường dẫn ảnh sản phẩm: 122.
- 37/37 sản phẩm có đầy đủ ảnh, giá và danh mục.

Không tự ý thay đổi các số liệu này.

Không tạo thêm sản phẩm thử nghiệm trên database thật khi chưa có bản sao lưu và sự cho phép riêng.

### 2. Gemini AI Agent

Các chức năng đã được báo cáo hoàn thành:

- `search_products`
- `get_product_details`
- `recommend_outfit`
- `replace_outfit_item`
- `get_available_sizes`

5 kịch bản Tool Calling đều PASS.

Đã xử lý lỗi Gemini HTTP 504, tối ưu context, giới hạn retry và cải thiện thông báo lỗi.

**Yêu cầu:**
- Không viết lại Gemini AI Agent.
- Không đổi model, timeout, fallback hoặc cơ chế Tool Calling đang hoạt động.
- Không sửa logic AI nếu không phát hiện lỗi thực tế.
- Sau khi thay đổi cấu trúc sản phẩm hoặc ảnh, chỉ kiểm tra khả năng tương thích giữa AI và catalog.
- Đảm bảo AI vẫn đọc dữ liệu thực tế từ MySQL.

### 3. Frontend và Backend

Các trang đã được kiểm tra HTTP 200:

- `/`
- `/search`
- `/product/p003`
- `/admin/products/new`
- `/smart-outfit/ai-stylist`

Backend chạy port 5001, Frontend chạy port 3000.

Giữ nguyên kiến trúc và cách khởi chạy hiện tại.

---

# II. NHIỆM VỤ 1 – TÍCH HỢP CLOUDINARY

### Thông tin Cloudinary

```env
CLOUDINARY_CLOUD_NAME=ubkdyrwp
CLOUDINARY_API_KEY=821468172265738
CLOUDINARY_API_SECRET=YOUR_NEW_ROTATED_SECRET
```

API Secret phải được thay bằng Secret mới do chủ dự án tạo lại sau khi Secret cũ bị lộ.

### Yêu cầu thực hiện

1. Kiểm tra Backend hiện tại đã có thư viện Cloudinary hay chưa.
2. Nếu chưa có, cài đặt SDK phù hợp với cấu trúc dự án.
3. Kiểm tra các file cấu hình môi trường.
4. Bổ sung 3 biến môi trường trên vào đúng file `.env` mà Backend sử dụng.
5. Không ghi đè các biến môi trường cũ.
6. Không làm mất Gemini API Key, MySQL credentials hoặc các cấu hình hiện tại.
7. Đảm bảo `.env` được Git ignore.
8. Cập nhật `.env.example` bằng giá trị mẫu, không có Secret thật.
9. Kiểm tra Backend đọc được cấu hình Cloudinary.
10. Kiểm tra kết nối bằng thao tác upload an toàn.

Không in Secret ra terminal, log, báo cáo hoặc giao diện.

Nếu chưa có Secret mới, yêu cầu chủ dự án nhập Secret mới trực tiếp vào file `.env`, sau đó tiếp tục các phần không phụ thuộc vào Cloudinary.

---

# III. NHIỆM VỤ 2 – HOÀN THIỆN UPLOAD ẢNH CLOUDINARY

Đây là phần cần ưu tiên cao.

Kiểm tra toàn bộ luồng upload ảnh hiện tại và tích hợp Cloudinary thay vì tạo một hệ thống upload song song.

### Chức năng cần có

- Tải ảnh từ máy tính.
- Hiển thị ảnh xem trước.
- Tải nhiều ảnh cho một sản phẩm.
- Chọn ảnh đại diện.
- Thay thế ảnh.
- Xóa ảnh đã chọn trước khi lưu.
- Sắp xếp ảnh nếu giao diện hiện tại hỗ trợ.
- Hiển thị trạng thái upload.
- Báo lỗi rõ ràng khi upload thất bại.

### Xử lý Backend

- Xác thực loại file và dung lượng.
- Upload lên Cloudinary.
- Nhận `secure_url`, `public_id` và các thông tin cần thiết.
- Lưu URL ảnh vào cấu trúc database hiện tại.
- Đảm bảo ảnh không bị mất khi tải lại trang.
- Không lưu API Secret ở Frontend.
- Có cơ chế xử lý lỗi và tránh tạo dữ liệu ảnh không liên kết.

### Bảo toàn ảnh cũ

Hiện database có 96 bản ghi trong `media_files` và 122 đường dẫn ảnh sản phẩm.

Không được:
- Xóa ảnh cũ hàng loạt.
- Thay toàn bộ URL ảnh cũ một cách tự động.
- Làm mất ảnh đang hiển thị trên website.
- Chuyển đổi cấu trúc lưu ảnh nếu chưa kiểm tra khả năng tương thích.

Chỉ áp dụng Cloudinary cho ảnh mới hoặc ảnh được Admin chủ động cập nhật.

---

# IV. NHIỆM VỤ 3 – HOÀN THIỆN CHỨC NĂNG THÊM SẢN PHẨM ADMIN

Trang cần hoàn thiện:

`/admin/products/new`

Trước tiên kiểm tra schema Prisma và API hiện tại. Tái sử dụng các trường dữ liệu đang có.

### 1. Form thêm sản phẩm

Hoàn thiện các nhóm thông tin:

**Thông tin cơ bản**
- Tên sản phẩm.
- Mã sản phẩm.
- Slug.
- Mô tả.

**Phân loại**
- Danh mục.
- Loại sản phẩm.
- Nhãn hoặc bộ sưu tập nếu hệ thống có.

**Giá**
- Giá bán.
- Giá gốc.
- Giá khuyến mãi nếu có.

**Hình ảnh**
- Ảnh đại diện.
- Thư viện ảnh sản phẩm.
- Ảnh xem trước.
- Upload Cloudinary.

**Thuộc tính**
- Màu sắc.
- Kích thước.
- Chất liệu.
- Các thuộc tính khác đã tồn tại trong database.

**Kho hàng**
- Số lượng tồn kho.
- Trạng thái tồn kho.
- Mã SKU hoặc biến thể nếu hệ thống đang sử dụng.

**Trạng thái**
- ACTIVE.
- INACTIVE.
- DRAFT.

Không tự tạo thêm trường trùng lặp với schema hiện tại.

### 2. Yêu cầu trải nghiệm giao diện

- Giao diện gọn gàng, đồng bộ với trang Admin hiện tại.
- Có thể nhập dữ liệu thuận tiện.
- Các danh mục lấy từ database.
- Màu sắc và kích thước có thể thêm nhiều lựa chọn nếu mô hình hiện tại hỗ trợ.
- Có kiểm tra trường bắt buộc.
- Có kiểm tra giá và tồn kho.
- Có thông báo lỗi tại trường dữ liệu.
- Có nút Lưu sản phẩm và Hủy.
- Có trạng thái đang lưu.
- Không cho nhấn lưu liên tục gây trùng sản phẩm.

### 3. Quy trình lưu sản phẩm

Đảm bảo luồng sau hoạt động đầy đủ:

Admin nhập thông tin
→ Upload ảnh lên Cloudinary
→ Nhận URL ảnh
→ Kiểm tra dữ liệu
→ Lưu sản phẩm vào MySQL bằng Prisma
→ Lưu các biến thể và thuộc tính liên quan
→ Trả kết quả thành công
→ Cập nhật danh sách Admin
→ Sản phẩm xuất hiện trên website nếu ở trạng thái ACTIVE.

Sử dụng transaction khi cần để tránh dữ liệu sản phẩm và biến thể bị lưu dở dang.

Nếu upload ảnh thất bại, không được báo thêm sản phẩm thành công khi ảnh là trường bắt buộc.

---

# V. NHIỆM VỤ 4 – HOÀN THIỆN CÁC CHỨC NĂNG QUẢN TRỊ SẢN PHẨM

Kiểm tra và hoàn thiện các chức năng:

| Chức năng | Yêu cầu |
|---|---|
| Xem sản phẩm | Hiển thị đúng dữ liệu MySQL |
| Tìm kiếm | Tìm theo tên, mã sản phẩm |
| Lọc | Theo danh mục và trạng thái |
| Chi tiết | Xem đầy đủ thông tin sản phẩm |
| Thêm mới | Lưu sản phẩm và ảnh Cloudinary |
| Chỉnh sửa | Cập nhật thông tin sản phẩm |
| Thay ảnh | Upload ảnh mới và cập nhật URL |
| Ẩn/hiện | Điều khiển trạng thái ACTIVE/INACTIVE |
| Xóa | Theo cơ chế an toàn hiện tại |

Không làm lại chức năng đang chạy tốt.

Đặc biệt kiểm tra:
- Khi chỉnh sửa sản phẩm, ảnh cũ không bị mất ngoài ý muốn.
- Khi thay ảnh, ảnh mới được hiển thị chính xác.
- Khi ẩn sản phẩm, sản phẩm không còn xuất hiện công khai.
- Khi thay đổi giá, website hiển thị giá mới.
- Khi thay đổi màu sắc hoặc kích thước, trang chi tiết phản ánh đúng dữ liệu.

---

# VI. NHIỆM VỤ 5 – ĐỒNG BỘ SẢN PHẨM VỚI WEBSITE KHÁCH HÀNG

Đây là điều kiện nghiệm thu quan trọng nhất.

Sau khi Admin thêm sản phẩm:

1. Sản phẩm xuất hiện trong danh sách Admin.
2. Sản phẩm xuất hiện ở trang danh mục phù hợp.
3. Sản phẩm xuất hiện trong kết quả tìm kiếm.
4. Trang chi tiết sản phẩm hoạt động.
5. Ảnh Cloudinary hiển thị chính xác.
6. Giá bán hiển thị chính xác.
7. Màu sắc và kích thước hiển thị đúng.
8. Giỏ hàng có thể nhận diện sản phẩm mới.
9. Các chức năng AI truy xuất được sản phẩm mới nếu sản phẩm đủ điều kiện hiển thị.
10. Dữ liệu vẫn chính xác sau khi tải lại trang.

Kiểm tra cache, API và cơ chế revalidation hiện tại để tránh tình trạng database đã cập nhật nhưng giao diện vẫn hiển thị dữ liệu cũ.

Không tạo dữ liệu giả để làm sản phẩm xuất hiện trên giao diện.

---

# VII. NHIỆM VỤ 6 – BẢO VỆ DATABASE VÀ CODE HIỆN TẠI

Đây là yêu cầu bắt buộc.

- Giữ nguyên 37 sản phẩm hiện có.
- Không tự ý xóa 3 sản phẩm INACTIVE.
- Không tự ý thêm hoặc xóa danh mục.
- Không sửa tồn kho của sản phẩm thật.
- Không tạo đơn hàng giả.
- Không thay đổi thông tin sản phẩm thật để kiểm thử.
- Không chạy migration nguy hiểm.
- Không thay đổi cơ chế xác thực Admin.
- Không để API quản trị truy cập trái phép.
- Không để Secret xuất hiện trên GitHub.

Nếu cần kiểm thử thêm sản phẩm, hãy tạo database thử nghiệm riêng hoặc xin xác nhận trước khi ghi dữ liệu vào `defaultdb`.

Trước khi thay đổi code:
- Kiểm tra `git status`.
- Bảo vệ các thay đổi chưa commit.
- Không ghi đè code đang hoạt động.

---

# VIII. NHIỆM VỤ 7 – KIỂM THỬ VÀ NGHIỆM THU

Thực hiện theo các nhóm sau:

### Test A – Cloudinary
- Kết nối Cloudinary thành công.
- Upload ảnh thành công.
- URL ảnh truy cập được.
- Ảnh không mất sau khi tải lại.

### Test B – Thêm sản phẩm
- Form hiển thị đầy đủ.
- Validation hoạt động.
- Upload nhiều ảnh hoạt động nếu được hỗ trợ.
- Lưu dữ liệu đúng vào MySQL.
- Không tạo bản ghi trùng.

### Test C – Website
- Sản phẩm xuất hiện ở danh mục.
- Tìm kiếm được sản phẩm.
- Trang chi tiết hoạt động.
- Ảnh, giá, màu sắc và kích thước chính xác.
- Giỏ hàng nhận sản phẩm.

### Test D – Chỉnh sửa
- Sửa tên và giá.
- Thay ảnh.
- Thay đổi trạng thái.
- Kiểm tra dữ liệu sau khi tải lại.

### Test E – Hồi quy
- Trang chủ.
- Tìm kiếm.
- Chi tiết sản phẩm cũ.
- Giỏ hàng.
- Admin.
- AI Stylist.
- Gemini Tool Calling.

Các thao tác ghi dữ liệu phải sử dụng database thử nghiệm hoặc được chủ dự án phê duyệt sau khi có backup đầy đủ.

Nếu chưa thể kiểm thử trên database thật, ghi rõ BLOCKED, không tự nhận PASS.

---

# IX. TỐI ƯU TOKEN VÀ THỜI GIAN

Không phân tích lại toàn bộ dự án nếu không cần thiết.

Thứ tự ưu tiên:

1. Kiểm tra code quản lý sản phẩm hiện tại.
2. Tích hợp Cloudinary.
3. Hoàn thiện upload ảnh.
4. Hoàn thiện thêm sản phẩm.
5. Hoàn thiện chỉnh sửa sản phẩm.
6. Đồng bộ ra giao diện khách hàng.
7. Kiểm thử và sửa lỗi.
8. Báo cáo.

Quy tắc:
- Chỉ đọc file có liên quan.
- Không tạo component/API trùng lặp.
- Không refactor ngoài phạm vi.
- Không làm lại Gemini.
- Không giải thích dài trong quá trình triển khai.
- Tập trung sửa lỗi và chạy kiểm thử.
- Nếu gặp lỗi, tìm nguyên nhân gốc và sửa trực tiếp.
- Ưu tiên hoàn thành MVP ổn định thay vì thêm tính năng không cần thiết.

---

# X. BÁO CÁO HOÀN THÀNH

Tạo file:

`docs/ADMIN_CLOUDINARY_COMPLETION_REPORT.md`

Nội dung:

1. Trạng thái tích hợp Cloudinary.
2. Các biến môi trường đã cấu hình (chỉ ghi tên biến).
3. Các file đã sửa.
4. Các API đã sửa hoặc bổ sung.
5. Trạng thái upload ảnh.
6. Trạng thái thêm sản phẩm.
7. Trạng thái chỉnh sửa sản phẩm.
8. Trạng thái đồng bộ dữ liệu ra website.
9. Kết quả kiểm thử.
10. Những lỗi còn tồn tại.
11. Những việc cần chủ dự án thực hiện.

Phân loại:
- PASS: Đã chạy và kiểm chứng thành công.
- PARTIAL: Đã triển khai nhưng chưa kiểm chứng đầy đủ.
- FAIL: Đã kiểm thử nhưng không hoạt động.
- BLOCKED: Thiếu quyền hoặc điều kiện để kiểm thử.

Không ghi Secret hoặc thông tin đăng nhập vào báo cáo.

## ĐIỀU KIỆN HOÀN THÀNH CUỐI CÙNG

Chỉ được xác nhận hoàn thành khi chứng minh được quy trình:

**Admin nhập sản phẩm → Upload ảnh Cloudinary → Lưu MySQL → Sản phẩm xuất hiện trên Admin → Sản phẩm hiển thị trên website → Khách hàng xem được chi tiết sản phẩm.**

Giữ nguyên toàn bộ dữ liệu sản phẩm hiện có và các chức năng Gemini AI Agent đã hoàn thành.

Hãy trực tiếp triển khai, kiểm thử và báo cáo kết quả. Không chỉ đưa ra hướng dẫn hoặc code mẫu.
