# USER MASTER PROMPT #13: 13 MYSQL AI ADDRESS SHIPPING SYNC
> **Nguồn gốc:** Prompt chỉ đạo thực tế từ Người dùng (User Request) tại Step 3527.
> **Độ dài gốc:** 10411 ký tự.
> **Mục đích trong thư viện:** Cung cấp toàn văn đặc tả nghiệp vụ, yêu cầu kỹ thuật và ràng buộc sản xuất thực tế mà người dùng đã trực tiếp chỉ đạo và kiểm chứng trong dự án Routine Web.

---

# PROMPT ANTIGRAVITY: ĐỒNG BỘ SẢN PHẨM MYSQL – GEMINI AI – XÁC THỰC ĐỊA CHỈ – TÍNH PHÍ VẬN CHUYỂN

## I. MỤC TIÊU

Tiếp tục phát triển dự án Routine Web hiện tại.

Triển khai 2 nhóm chức năng:

1. Sản phẩm được bổ sung từ website Routine (trong phạm vi được phép sử dụng) phải được lưu thực tế vào MySQL và đồng bộ với website, Admin, Gemini AI.
2. Xây dựng quy trình AI hỗ trợ thu thập, xác thực địa chỉ giao hàng và tính phí vận chuyển thông qua các công cụ Backend.

Yêu cầu: Không tạo dữ liệu giả trên giao diện. Không để AI tự bịa thông tin sản phẩm, địa chỉ hoặc phí vận chuyển.

---

# PHẦN A. ĐỒNG BỘ SẢN PHẨM VÀO MYSQL

## 1. Kiểm tra cấu trúc hiện tại

Trước khi sửa code, kiểm tra:
- Database MySQL đang sử dụng.
- Prisma Schema.
- Product, ProductVariant, Category, ProductImage và các bảng liên quan.
- API thêm, sửa, xóa, hiển thị sản phẩm.
- Cơ chế lưu ảnh hiện tại.
- Các công cụ Gemini đang sử dụng để truy vấn sản phẩm.

Không tự ý thay đổi cấu trúc database nếu không cần thiết.

## 2. Lưu sản phẩm thực tế

Khi thu thập được sản phẩm hợp lệ từ nguồn được phép sử dụng:

- Tạo bản ghi sản phẩm trong MySQL.
- Lưu SKU duy nhất.
- Lưu tên, mô tả, giá, danh mục.
- Lưu ảnh đại diện và gallery.
- Lưu các biến thể màu sắc, kích cỡ.
- Lưu tồn kho theo cấu trúc hiện tại.
- Lưu trạng thái ACTIVE/INACTIVE phù hợp.
- Lưu nguồn dữ liệu và đánh dấu DEMO nếu là dữ liệu mô phỏng.

Phải sử dụng API và Prisma hiện có.

Không chỉ thêm sản phẩm vào một mảng dữ liệu frontend.

## 3. Đồng bộ đến Gemini AI

Kiểm tra các công cụ hiện có:
- search_products
- get_product_details
- recommend_outfit
- replace_outfit_item
- get_available_sizes

Điều chỉnh để các công cụ trên truy vấn dữ liệu mới nhất từ MySQL.

Yêu cầu:

- AI tìm được sản phẩm mới bằng tên và SKU.
- AI trả về đúng giá từ database.
- AI trả về đúng ảnh sản phẩm.
- AI nhận diện đúng màu sắc và kích cỡ.
- AI kiểm tra tồn kho từ dữ liệu thực tế.
- AI không giới thiệu sản phẩm INACTIVE hoặc đã bị ẩn.
- AI không tự tạo sản phẩm khi không tìm thấy.
- AI không sử dụng dữ liệu cache cũ sau khi sản phẩm được cập nhật.

Khi Admin thêm sản phẩm mới, Gemini phải có khả năng tìm thấy sản phẩm đó mà không cần huấn luyện lại mô hình.

Nếu có cache, phải có cơ chế xóa hoặc cập nhật cache khi Admin thêm, sửa, ẩn hoặc xóa sản phẩm.

## 4. Kiểm thử

Thực hiện tình huống:

1. Admin thêm một sản phẩm mới.
2. Kiểm tra sản phẩm có trong MySQL.
3. Kiểm tra sản phẩm xuất hiện trên website.
4. Yêu cầu Gemini tìm sản phẩm bằng tên.
5. Yêu cầu Gemini tìm sản phẩm bằng SKU.
6. Hỏi giá, màu sắc và kích cỡ.
7. Sửa giá trong Admin.
8. Kiểm tra Gemini trả về giá mới.
9. Chuyển sản phẩm sang INACTIVE.
10. Kiểm tra Gemini không còn giới thiệu sản phẩm đó như hàng đang bán.

---

# PHẦN B. AI HỖ TRỢ THU THẬP VÀ XÁC THỰC ĐỊA CHỈ

## 1. Xây dựng quy trình hội thoại

Khi khách hàng mua hàng và nhập địa chỉ, Gemini AI cần có khả năng:

- Tiếp nhận địa chỉ khách nhập tự nhiên.
- Nhận diện tỉnh/thành phố.
- Nhận diện phường/xã.
- Nhận diện số nhà, tên đường, tòa nhà hoặc khu dân cư.
- Phát hiện thông tin còn thiếu.
- Hỏi lại khách hàng để bổ sung.
- Tóm tắt địa chỉ đã chuẩn hóa.
- Yêu cầu khách xác nhận trước khi lưu.

Ví dụ:

Khách hàng: "Mình ở số 15 ngõ 20 Nguyễn Trãi, Hà Đông, Hà Nội."

AI cần phân tích thông tin đã có, kiểm tra xem còn thiếu phường/xã hay không.

Nếu chưa đủ dữ liệu, AI hỏi lại:

"Bạn cho mình xin thêm tên phường để xác nhận địa chỉ giao hàng chính xác nhé."

Không tự suy đoán phường/xã khi có nhiều khả năng.

## 2. Xác thực địa chỉ bằng Backend

Tạo hoặc sử dụng công cụ Backend để:

- Chuẩn hóa địa chỉ.
- Đối chiếu tỉnh/thành phố với danh mục hành chính.
- Đối chiếu phường/xã với danh mục hành chính hiện hành.
- Kiểm tra các trường bắt buộc.
- Phát hiện địa chỉ không hợp lệ hoặc không đủ thông tin.

Ưu tiên sử dụng danh mục hành chính được cập nhật và lưu trong database.

Nếu không xác định được địa chỉ, phải trả về trạng thái NEED_MORE_INFORMATION hoặc INVALID.

Không được thông báo địa chỉ hợp lệ chỉ vì AI hiểu được nội dung khách nhập.

Lưu ý: Xác thực địa chỉ hành chính không đồng nghĩa với xác minh địa chỉ giao hàng thực tế tồn tại hoặc có thể giao đến. Nếu không tích hợp dịch vụ vận chuyển, phải thông báo đúng giới hạn này.

## 3. Xây dựng công cụ AI gọi Backend

Tạo các công cụ phù hợp, có thể sử dụng các tên:

- normalize_customer_address
- validate_customer_address
- calculate_shipping_fee
- get_shipping_policy

Các công cụ phải có đầu vào và đầu ra rõ ràng.

Ví dụ đầu ra xác thực:

{
  "status": "VALID",
  "province": "...",
  "ward": "...",
  "street_address": "...",
  "formatted_address": "...",
  "missing_fields": []
}

Ví dụ khi thiếu thông tin:

{
  "status": "NEED_MORE_INFORMATION",
  "missing_fields": ["ward"],
  "message": "Thiếu thông tin phường/xã"
}

AI chỉ được thông báo địa chỉ đã được xác thực khi Backend trả về trạng thái VALID.

---

# PHẦN C. AI HỖ TRỢ TÍNH PHÍ VẬN CHUYỂN

## 1. Xây dựng bảng phí vận chuyển

Tạo bảng cấu hình phí vận chuyển có thể quản lý từ Admin.

Có thể phân vùng:

- Nội thành.
- Ngoại thành.
- Các tỉnh/thành phố khác.
- Khu vực xa hoặc khó giao hàng.

Mức phí phải do Admin cấu hình, không tự đặt thành chính sách chính thức của Routine.

Nếu chưa có bảng phí chính thức, hãy tạo bảng phí DEMO có nhãn rõ ràng để phục vụ thuyết trình.

Không sử dụng Google Maps nếu chưa được cấu hình.

Không giả vờ đã tích hợp GHN, GHTK hoặc Viettel Post nếu chưa có API thực tế.

## 2. Quy trình tính phí

Khi khách hàng cung cấp địa chỉ:

1. AI tiếp nhận địa chỉ.
2. Backend chuẩn hóa và xác thực.
3. Backend xác định khu vực giao hàng.
4. Backend truy xuất bảng phí.
5. Backend tính phí vận chuyển.
6. AI giải thích kết quả cho khách.
7. Khách xác nhận đơn hàng.
8. Backend lưu phí vận chuyển vào đơn hàng.

Công thức:

Tổng thanh toán = Tổng tiền sản phẩm - Giảm giá + Phí vận chuyển.

Backend phải tự tính lại tổng tiền ở bước checkout, không lấy con số do AI hoặc frontend tự gửi lên làm căn cứ thanh toán.

## 3. Các trường hợp phải kiểm thử

- Địa chỉ đầy đủ và hợp lệ.
- Địa chỉ thiếu phường/xã.
- Địa chỉ sai tỉnh/thành.
- Địa chỉ có cách viết tắt.
- Địa chỉ có lỗi chính tả.
- Địa chỉ không xác định được khu vực.
- Địa chỉ thuộc khu vực có phí khác nhau.
- Khách thay đổi địa chỉ sau khi đã tính phí.
- Khách thay đổi giỏ hàng.
- Đơn hàng có áp dụng mã giảm giá.

Nếu địa chỉ thay đổi, phải tính lại phí ship.

Nếu không xác định được phí, không được tự đặt một mức phí bất kỳ. Hãy yêu cầu khách bổ sung thông tin hoặc thông báo cần nhân viên hỗ trợ.

---

# PHẦN D. TÍCH HỢP VÀO QUY TRÌNH ĐẶT HÀNG

Tích hợp vào giao diện giỏ hàng và checkout hiện tại.

Luồng trải nghiệm:

1. Khách thêm sản phẩm vào giỏ.
2. Khách chuyển sang thanh toán.
3. AI hỗ trợ thu thập địa chỉ nếu khách cần.
4. Backend xác thực địa chỉ.
5. Backend tính phí vận chuyển.
6. Website hiển thị chi tiết tiền hàng, giảm giá, phí ship và tổng thanh toán.
7. Khách xác nhận.
8. Backend tạo đơn hàng.
9. MySQL lưu địa chỉ, phí ship và tổng tiền tại thời điểm đặt hàng.
10. Admin xem được đơn hàng và phí vận chuyển.

Lưu ý:
- Khách hàng vẫn có thể nhập địa chỉ bằng biểu mẫu thông thường.
- AI là công cụ hỗ trợ, không bắt buộc khách phải trò chuyện mới đặt hàng được.
- Không tự động đặt hàng khi chưa có xác nhận của khách.
- Không để AI tự sửa địa chỉ đã lưu mà không có sự đồng ý của khách.

## Dữ liệu đơn hàng cần lưu

Sử dụng các trường phù hợp với cấu trúc hiện tại:

- customer_id
- recipient_name
- recipient_phone
- province
- ward
- street_address
- full_address
- shipping_zone
- shipping_fee
- subtotal
- discount_amount
- total_amount
- shipping_fee_rule_version
- address_validation_status

Phí ship cần được lưu thành giá trị cố định tại thời điểm tạo đơn hàng. Không để việc thay đổi bảng phí sau này làm thay đổi đơn hàng cũ.

---

# PHẦN E. KIỂM THỬ LIÊN THÔNG

Thực hiện kiểm thử thực tế:

### Test 1: Sản phẩm và AI
Admin thêm sản phẩm → MySQL lưu → Website hiển thị → Gemini tìm thấy.

### Test 2: Thay đổi giá
Admin sửa giá → Database cập nhật → Website cập nhật → Gemini trả giá mới.

### Test 3: Địa chỉ đầy đủ
Khách nhập địa chỉ → AI phân tích → Backend xác thực → Trả về địa chỉ chuẩn hóa.

### Test 4: Địa chỉ thiếu thông tin
Khách nhập địa chỉ thiếu phường/xã → AI hỏi bổ sung → Khách cung cấp → Backend xác thực lại.

### Test 5: Tính phí ship
Địa chỉ hợp lệ → Backend tính phí → AI giải thích → Website hiển thị đúng phí.

### Test 6: Thay đổi địa chỉ
Khách đổi địa chỉ → Backend xác thực và tính lại phí.

### Test 7: Đặt hàng
Khách xác nhận → Backend tạo đơn → MySQL lưu chính xác địa chỉ, phí ship và tổng tiền.

### Test 8: Kiểm tra Admin
Admin xem được địa chỉ giao hàng, số điện thoại, phí vận chuyển và tổng đơn.

---

# PHẦN F. RÀNG BUỘC AN TOÀN

- Không sửa cấu hình Cloudinary.
- Không sửa `.env` hoặc API key.
- Không thay đổi thông tin kết nối MySQL.
- Không ghi dữ liệu thử nghiệm vào database `defaultdb`.
- Dùng `routine_test_db` cho các kiểm thử có ghi dữ liệu.
- Không xóa sản phẩm hoặc đơn hàng hợp lệ.
- Không DROP, TRUNCATE hoặc reset database.
- Không tạo đơn hàng thật hoặc thanh toán thật.
- Không để lộ thông tin khách hàng, mật khẩu hoặc API secret trong log.
- Không refactor toàn bộ hệ thống nếu không cần thiết.
- Giữ nguyên các chức năng hiện có đang hoạt động tốt.

Nếu cần cập nhật Prisma Schema, hãy kiểm tra migration và backup trước. Không tự ý thực hiện migration phá hủy dữ liệu.

---

# PHẦN G. BÁO CÁO NGHIỆM THU

Tạo file:

`docs/PRODUCT_AI_SHIPPING_INTEGRATION_REPORT.md`

Báo cáo phải có:

1. Các bảng MySQL đã sử dụng hoặc bổ sung.
2. Các API đã tạo hoặc cập nhật.
3. Các công cụ Gemini đã tích hợp.
4. Quy trình đồng bộ sản phẩm.
5. Quy trình AI thu thập địa chỉ.
6. Cách Backend xác thực địa chỉ.
7. Cách Backend tính phí vận chuyển.
8. Cách lưu phí ship vào đơn hàng.
9. Kết quả kiểm thử từng tình huống.
10. Ảnh chụp giao diện thực tế.
11. Các lỗi còn tồn tại.

Phân loại kết quả PASS / PARTIAL / FAIL / BLOCKED.

Mỗi trường hợp PASS phải có bằng chứng phù hợp: giao diện, API response và bản ghi MySQL khi cần.

**YÊU CẦU CUỐI:** Không chỉ hoàn thành code. Phải chứng minh được luồng hoạt động thực tế: MySQL → Backend → Website → Gemini AI và AI → Backend → xác thực địa chỉ → tính phí ship → MySQL. Không tuyên bố hoàn thành nếu mới chỉ kiểm tra code hoặc trả về HTTP 200.
