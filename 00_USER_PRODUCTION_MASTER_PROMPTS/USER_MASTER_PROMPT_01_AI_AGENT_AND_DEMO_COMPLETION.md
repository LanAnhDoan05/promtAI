# USER MASTER PROMPT #01: 01 AI AGENT AND DEMO COMPLETION
> **Nguồn gốc:** Prompt chỉ đạo thực tế từ Người dùng (User Request) tại Step 0.
> **Độ dài gốc:** 6652 ký tự.
> **Mục đích trong thư viện:** Cung cấp toàn văn đặc tả nghiệp vụ, yêu cầu kỹ thuật và ràng buộc sản xuất thực tế mà người dùng đã trực tiếp chỉ đạo và kiểm chứng trong dự án Routine Web.

---

# CONTINUE PROJECT – ROUTINE WEB + GEMINI AI AGENT
## GIAI ĐOẠN HOÀN THIỆN CUỐI VÀ CHUẨN BỊ DEMO

Bạn tiếp tục làm việc trên dự án Routine Web hiện tại.

Không tạo dự án mới.
Không xây dựng lại những chức năng đã hoàn thành.
Không chạy lại toàn bộ quy trình kiểm toán từ đầu.

Hãy đọc trạng thái dự án hiện tại, các báo cáo trong thư mục docs và kịch bản demo mới nhất do chủ dự án cung cấp.

## I. TRẠNG THÁI ĐÃ XÁC NHẬN

1. MySQL đã smoke test.
2. Frontend và Backend đã smoke test.
3. Không sử dụng dữ liệu giả để thay thế database.
4. GET /api/v1/health đã được kiểm tra.
5. GET /api/v1/stores đã được kiểm tra.
6. API Admin chưa đăng nhập trả HTTP 401 đúng yêu cầu.
7. Các Backend Tool đọc catalog MySQL đã được kiểm chứng.

Các kết quả catalog đã xác nhận:

- p003 – Classic White Shirt: 339.000đ.
- p003 có màu Black/White/Navy, size S–XL, tồn kho tổng 78.
- p027 – Silk Blend Blouse: 349.000đ.
- p005 – Straight Fit Jeans: 549.000đ.
- Phối p027 + p005: tổng 898.000đ.
- Thay p027 bằng p003: tổng 888.000đ.

Lưu ý: p003 hiện chỉ có tồn kho tổng, không có tồn kho riêng theo size. Không được suy diễn tồn kho từng size.

## II. NHIỆM VỤ 1 – KIỂM TRA LẠI DỮ LIỆU THẬT

Kiểm tra MySQL và xác định:

- Tổng số sản phẩm thực tế.
- Số sản phẩm đang hoạt động.
- Số danh mục.
- Số showroom.
- Số hình ảnh sản phẩm.
- Số sản phẩm có đầy đủ ảnh, giá và danh mục.

Có sự chênh lệch giữa báo cáo trước ghi 38 sản phẩm và báo cáo demo mới ghi 37 sản phẩm.

Phải tìm nguyên nhân và ghi nhận chính xác.

Không thêm hoặc xóa sản phẩm để điều chỉnh số liệu.

## III. NHIỆM VỤ 2 – XỬ LÝ GEMINI HTTP 504

Đây là nhiệm vụ ưu tiên cao nhất.

Hiện Gemini API trả HTTP 504.

Hãy kiểm tra:

1. Model Gemini đang được cấu hình.
2. API endpoint đang sử dụng.
3. SDK và phiên bản SDK.
4. Cấu hình timeout.
5. Cách gửi request.
6. Cách xử lý response.
7. Quota và giới hạn API nếu có thể xác minh.
8. Log lỗi Backend.
9. Khả năng lỗi do proxy hoặc mạng.
10. Khả năng lỗi do request quá lớn hoặc timeout.

Không tự ý đổi model theo phỏng đoán.

Hãy kiểm tra model có khả năng hỗ trợ Tool Calling và tương thích với API đang dùng.

Không hiển thị API Key.

Thực hiện phương án:

- Sửa cấu hình request nếu sai.
- Giảm dữ liệu gửi lên Gemini nếu quá lớn.
- Giới hạn số sản phẩm đưa vào context.
- Thiết lập timeout hợp lý.
- Có retry giới hạn đối với lỗi tạm thời.
- Có xử lý lỗi 429, 500, 502, 503, 504.
- Không retry vô hạn.
- Không trả nội dung giả khi Gemini thất bại.

Sau khi sửa, gọi Gemini thật và ghi nhận HTTP status, thời gian phản hồi và kết quả.

Nếu vẫn lỗi, phải xác định rõ nguyên nhân có thể chứng minh và báo cáo.

## IV. NHIỆM VỤ 3 – HOÀN THIỆN GEMINI TOOL CALLING

Các Backend Tools đã có kết quả smoke test.

Không viết lại nếu đang hoạt động tốt.

Kiểm tra và hoàn thiện khả năng Gemini tự quyết định gọi các công cụ:

1. search_products
2. get_product_details
3. recommend_outfit
4. replace_outfit_item
5. get_available_sizes

Quy trình bắt buộc:

User Request
→ Gemini phân tích ý định
→ Gemini chọn Tool
→ Backend thực thi Tool
→ Backend truy vấn MySQL
→ Trả kết quả cho Gemini
→ Gemini tổng hợp
→ Frontend hiển thị.

Không được chỉ trả kết quả từ các hàm Backend rồi gọi đó là Gemini Tool Calling.

Phải ghi log:
- Tool được Gemini yêu cầu.
- Tham số.
- Kết quả Backend.
- Phản hồi cuối cùng.

Không ghi API Key hoặc dữ liệu bí mật vào log.

## V. NHIỆM VỤ 4 – KIỂM THỬ 5 KỊCH BẢN

Kịch bản 1:

"Tìm cho tôi áo sơ mi trắng dưới 500.000 đồng."

Yêu cầu:
- Gọi search_products.
- Tìm được p003.
- Không trả T-shirt thay cho áo sơ mi.
- Giá đúng 339.000đ.

Kịch bản 2:

"Lấy thông tin chi tiết và size của sản phẩm này."

Yêu cầu:
- Gọi get_product_details.
- Hiển thị màu và size chính xác.
- Không suy diễn tồn kho theo size.

Kịch bản 3:

"Phối cho tôi một bộ đồ đi làm dưới 1 triệu."

Yêu cầu:
- Gọi recommend_outfit.
- Sử dụng dữ liệu thật.
- Tổng giá không vượt 1 triệu.
- Kiểm tra tồn kho.

Kịch bản 4:

"Thay chiếc áo vừa rồi bằng áo sơ mi trắng."

Yêu cầu:
- Gọi replace_outfit_item.
- Giữ nguyên quần p005.
- Thay áo bằng p003.
- Tổng giá phải tính lại thành 888.000đ nếu các sản phẩm và giá không thay đổi.

Kịch bản 5:

"Tôi chỉ muốn xem quần jeans."

Yêu cầu:
- Chỉ gọi công cụ tìm kiếm phù hợp.
- Không tự phối đồ.

Mỗi tình huống phải ghi kết quả PASS hoặc FAIL.

Nếu Gemini không hoạt động thì không được đánh dấu PASS cho phần Gemini Tool Calling.

## VI. NHIỆM VỤ 5 – KIỂM TRA GIAO DIỆN DEMO

Kiểm tra:

- Trang chủ.
- Trang sản phẩm.
- Chi tiết sản phẩm.
- Form Admin thêm sản phẩm.
- Giao diện AI Stylist.
- Hiển thị ảnh và giá.
- Hiển thị câu trả lời của AI.
- Trạng thái loading.
- Trạng thái lỗi khi Gemini không phản hồi.

Đặc biệt, khi Gemini trả HTTP 504, giao diện phải hiển thị thông báo thân thiện, không bị treo hoặc hiển thị câu trả lời giả.

## VII. NHIỆM VỤ 6 – BẢO VỆ DATABASE VÀ ADMIN

Chủ dự án chưa cấp phép ghi dữ liệu thử nghiệm vào database thật.

Do đó:

- Không tạo sản phẩm thử nghiệm.
- Không sửa sản phẩm thật.
- Không xóa sản phẩm.
- Không thay đổi tồn kho.
- Không thực hiện đơn hàng thật.

Chỉ kiểm tra form và API theo cách không ghi dữ liệu.

Nếu muốn kiểm thử CRUD, đề xuất môi trường database test riêng.

Chỉ được thực hiện khi có backup đầy đủ bao gồm cả LONGBLOB và chủ dự án cho phép.

## VIII. NHIỆM VỤ 7 – BÁO CÁO

Tạo file:

docs/FINAL_DEMO_STATUS.md

Bao gồm:

1. Trạng thái dự án.
2. Số liệu MySQL thực tế.
3. Nguyên nhân chênh lệch số sản phẩm.
4. Nguyên nhân Gemini 504.
5. Những thay đổi đã thực hiện.
6. Các Tools đã kiểm chứng.
7. Kết quả 5 kịch bản.
8. Bằng chứng Gemini thực sự gọi Tool.
9. Các chức năng chưa hoàn thành.
10. Các lỗi còn tồn tại.
11. Hướng xử lý tiếp theo.
12. Kịch bản demo cuối cùng.

Phân loại:
- PASS: Đã kiểm chứng thực tế.
- PARTIAL: Hoạt động một phần.
- FAIL: Chưa hoạt động.
- BLOCKED: Không thể thực hiện do điều kiện bên ngoài.

Không được báo cáo thành công khi chỉ mới viết code.

## IX. QUY TẮC THỰC THI

Ưu tiên xử lý Gemini HTTP 504 và Tool Calling trước.

Không sửa các chức năng Backend đã hoạt động nếu không có lý do cụ thể.

Không tiếp tục tối ưu những phần không ảnh hưởng đến demo.

Tận dụng tối đa cấu trúc hiện có.

Sau khi hoàn thành, cập nhật báo cáo và gửi tóm tắt trực tiếp trong cửa sổ chat.

Bắt đầu thực hiện ngay.
