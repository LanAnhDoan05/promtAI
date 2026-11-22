# USER MASTER PROMPT #22: 22 COMPREHENSIVE TECHNICAL AUDIT
> **Nguồn gốc:** Prompt chỉ đạo thực tế từ Người dùng (User Request) tại Step 9321.
> **Độ dài gốc:** 11492 ký tự.
> **Mục đích trong thư viện:** Cung cấp toàn văn đặc tả nghiệp vụ, yêu cầu kỹ thuật và ràng buộc sản xuất thực tế mà người dùng đã trực tiếp chỉ đạo và kiểm chứng trong dự án Routine Web.

---

# MASTER PROMPT – COMPREHENSIVE TECHNICAL AUDIT ROUTINE WEB
## Mục tiêu: Đánh giá toàn diện hệ thống trước khi chuyển sang Production

Bạn là một đội ngũ kỹ thuật cấp cao chịu trách nhiệm kiểm toán và chuẩn bị đưa một nền tảng thương mại điện tử thời trang vào vận hành thực tế.

Dự án: ROUTINE WEB  
Mô hình: Fashion E-commerce Platform  
Quy mô ban đầu: Small Business  
Định hướng: Production Deployment  
Kiến trúc hiện tại: Tiếp tục sử dụng và nâng cấp codebase hiện có, không mặc định viết lại từ đầu.

Hệ thống bao gồm:
1. Customer Frontend – Website dành cho khách hàng.
2. Admin Dashboard – Hệ thống quản trị doanh nghiệp.
3. Backend API – Xử lý nghiệp vụ và dữ liệu.
4. MySQL Database – Lưu trữ dữ liệu.
5. Gemini AI Stylist Agent – Trợ lý tư vấn thời trang.
6. Payment Integration – Thanh toán trực tuyến.
7. Các module liên quan: sản phẩm, kho, khách hàng, giỏ hàng, đơn hàng, tư vấn và thông báo.

---

# PHẦN A. QUY TẮC KIỂM TOÁN

Đây là nhiệm vụ AUDIT ONLY – READ ONLY.

TUYỆT ĐỐI KHÔNG:
- Chỉnh sửa, ghi đè hoặc xóa bất kỳ file code nào.
- Tự ý cài đặt lại toàn bộ dependencies.
- Tự ý thay đổi cấu trúc database hoặc chạy migration.
- Xóa dữ liệu, tài khoản, sản phẩm hoặc đơn hàng hiện có.
- Reset database hoặc tạo dữ liệu thử nghiệm.
- Thay đổi cấu hình môi trường.
- Công khai API key, mật khẩu, token hoặc thông tin kết nối.
- Tuyên bố một chức năng hoạt động tốt chỉ vì giao diện hiển thị bình thường.

ĐƯỢC PHÉP:
- Đọc toàn bộ source code.
- Đọc cấu trúc thư mục và các file cấu hình.
- Kiểm tra database schema và quan hệ giữa các bảng bằng thao tác chỉ đọc.
- Đọc API routes, controllers, services, middleware.
- Kiểm tra các lệnh khởi chạy và test hiện có.
- Chạy các bài kiểm thử không gây thay đổi dữ liệu.
- Kiểm tra log và các lỗi có thể quan sát được.
- Đối chiếu luồng dữ liệu giữa Frontend, Backend và Database.

Nếu một kiểm tra cần thao tác ghi dữ liệu hoặc có nguy cơ ảnh hưởng hệ thống, KHÔNG tự thực hiện. Hãy ghi rõ cần môi trường staging hoặc sự cho phép riêng.

Phải phân biệt rõ:
- VERIFIED: Đã kiểm tra và có bằng chứng.
- FAILED: Đã kiểm tra và phát hiện lỗi.
- NOT VERIFIED: Chưa đủ điều kiện kiểm tra.
- NOT IMPLEMENTED: Chức năng chưa được xây dựng.
- INFERRED: Nhận định từ source code nhưng chưa xác minh khi chạy thực tế.

---

# PHẦN B. KHẢO SÁT KIẾN TRÚC TỔNG THỂ

Kiểm tra:
1. Cấu trúc toàn bộ dự án.
2. Công nghệ Frontend và Backend.
3. Framework, thư viện và phiên bản.
4. Cấu trúc module.
5. Cách Frontend kết nối Backend.
6. Cách Backend kết nối MySQL.
7. Cách quản lý biến môi trường.
8. Cách xác thực và phân quyền.
9. Cách xử lý lỗi.
10. Cách quản lý log.
11. Cách chạy development và production.
12. Các dependency lỗi thời hoặc có lỗ hổng đã biết.

Vẽ sơ đồ kiến trúc hệ thống hiện tại bằng Mermaid.

Không tự suy đoán kiến trúc nếu chưa tìm thấy bằng chứng.

---

# PHẦN C. KIỂM TOÁN FRONTEND

Kiểm tra Customer Frontend và Admin Dashboard riêng biệt.

Đối với từng module:
- Kiểm tra các trang và route.
- Kiểm tra component và trạng thái giao diện.
- Kiểm tra API được gọi.
- Kiểm tra xử lý loading, empty state và error state.
- Kiểm tra validation dữ liệu đầu vào.
- Kiểm tra responsive trên mobile và desktop.
- Kiểm tra lỗi console.
- Kiểm tra hình ảnh sản phẩm và đường dẫn ảnh.
- Kiểm tra các nút, biểu mẫu và thao tác có thực sự hoạt động.

Đặc biệt kiểm tra:
1. Trang chủ và danh sách sản phẩm.
2. Tìm kiếm, lọc và sắp xếp.
3. Chi tiết sản phẩm.
4. Màu sắc, kích thước và biến thể.
5. Giỏ hàng.
6. Đặt hàng.
7. Đăng ký, đăng nhập.
8. Hồ sơ khách hàng.
9. Lịch sử đơn hàng.
10. Admin quản lý sản phẩm.
11. Admin quản lý đơn hàng.
12. Admin quản lý khách hàng.
13. Admin quản lý kho.
14. Admin quản lý tư vấn và hội thoại.
15. Dashboard và báo cáo.

Phát hiện các chức năng chỉ có giao diện nhưng chưa kết nối Backend hoặc chưa lưu dữ liệu thật.

---

# PHẦN D. KIỂM TOÁN BACKEND VÀ API

Kiểm tra:
- API routes.
- Controllers.
- Services.
- Middleware.
- Authentication.
- Authorization.
- Request validation.
- Response format.
- Error handling.
- Database transactions.
- Các API bị trùng lặp hoặc không sử dụng.
- Các API không có kiểm tra quyền truy cập.

Với mỗi module, cần xác định:
1. API nào đã triển khai.
2. API nào đang hoạt động.
3. API nào thiếu.
4. API nào có lỗi.
5. API nào có nguy cơ truy cập trái phép.
6. API nào chưa xử lý tình huống bất thường.

Kiểm tra khả năng chống:
- SQL Injection.
- XSS.
- CSRF khi phù hợp với cơ chế xác thực.
- Broken Access Control.
- IDOR.
- Brute-force đăng nhập.
- Lộ thông tin nhạy cảm.
- Gửi request trùng lặp gây tạo dữ liệu hoặc giao dịch trùng.

---

# PHẦN E. KIỂM TOÁN MYSQL DATABASE

Kiểm tra cấu trúc database hiện tại.

Lập danh sách:
- Tên bảng.
- Các trường dữ liệu.
- Primary Key.
- Foreign Key.
- Index.
- Quan hệ giữa các bảng.
- Ràng buộc dữ liệu.
- Kiểu dữ liệu.
- Trường có khả năng bị NULL không hợp lý.
- Các bảng trùng lặp hoặc thiếu liên kết.

Kiểm tra nghiệp vụ:
1. Product và Product Variant.
2. Category.
3. Inventory.
4. User và Customer.
5. Cart và Cart Items.
6. Orders và Order Items.
7. Payment Transactions.
8. Addresses.
9. Promotions.
10. Reviews.
11. Conversations và Messages.
12. Notifications.
13. AI Conversation History.
14. Employee và Role/Permission.

Không mặc định rằng các bảng trên đều tồn tại. Hãy đối chiếu với database thực tế.

Đánh giá:
- Tính toàn vẹn dữ liệu.
- Khả năng xảy ra dữ liệu trùng.
- Quan hệ dữ liệu bị thiếu.
- Khả năng mất dữ liệu khi thao tác đồng thời.
- Khả năng backup và restore.
- Cơ chế transaction.
- Khả năng đồng bộ tồn kho và đơn hàng.

Không hiển thị dữ liệu cá nhân thật hoặc thông tin bí mật trong báo cáo.

---

# PHẦN F. KIỂM TOÁN NGHIỆP VỤ THƯƠNG MẠI ĐIỆN TỬ

Truy vết các quy trình sau:

LUỒNG 1 – SẢN PHẨM:
Admin tạo sản phẩm → Lưu Database → Hiển thị trên Website → Khách hàng xem sản phẩm.

LUỒNG 2 – TỒN KHO:
Admin cập nhật tồn kho → Database cập nhật → Website hiển thị chính xác số lượng và trạng thái còn hàng.

LUỒNG 3 – ĐẶT HÀNG:
Khách hàng chọn sản phẩm → Chọn biến thể → Giỏ hàng → Địa chỉ giao hàng → Đặt hàng → Database lưu đơn hàng.

LUỒNG 4 – THANH TOÁN:
Tạo giao dịch → Chuyển đến cổng thanh toán → Nhận kết quả → Xác minh phía Backend → Cập nhật trạng thái thanh toán và đơn hàng.

LUỒNG 5 – QUẢN LÝ ĐƠN:
Khách đặt hàng → Admin nhận đơn → Xác nhận → Xử lý → Giao hàng → Hoàn tất hoặc hủy đơn.

LUỒNG 6 – TƯ VẤN:
Khách hàng gửi yêu cầu tư vấn → Admin nhận thông báo → Nhân viên mở hội thoại → Phản hồi khách hàng → Hai bên tiếp tục trao đổi.

Với từng luồng, xác định điểm bắt đầu, điểm kết thúc, API, bảng dữ liệu và các lỗi có thể xảy ra.

---

# PHẦN G. KIỂM TOÁN GEMINI AI STYLIST AGENT

Kiểm tra:
1. Cách kết nối Gemini API.
2. Quản lý API Key.
3. System Instructions.
4. Cơ chế truy xuất dữ liệu sản phẩm.
5. Cơ chế xử lý lịch sử hội thoại.
6. Cơ chế ghi nhớ ngữ cảnh.
7. Cơ chế xử lý ý định mua hàng.
8. Cơ chế phối đồ.
9. Cơ chế chuyển tiếp chuyên viên.
10. Cơ chế đồng bộ hội thoại với Admin.
11. Cơ chế xử lý lỗi API và giới hạn sử dụng.
12. Chi phí và khả năng kiểm soát mức sử dụng AI.

Kiểm tra các tình huống:
- Khách hỏi áo len dưới 1 triệu.
- Khách tiếp tục hỏi màu trắng.
- AI phải hiểu vẫn đang tìm áo len dưới 1 triệu, màu trắng.
- AI phải lấy sản phẩm từ database, không tự bịa sản phẩm hoặc giá.
- Khách yêu cầu phối đồ thì AI mới thực hiện phối đồ.
- Khách chỉ hỏi thông tin thì không tự động phối đồ.
- Khi khách có nhu cầu mua hàng, AI có thể đề nghị chuyển cho chuyên viên.
- Khi khách đồng ý, hệ thống phải tạo hoặc chuyển tiếp hội thoại.
- Admin phải nhận được thông báo và xem được nội dung hội thoại.
- Nhân viên trả lời thì khách hàng phải nhận được phản hồi.

Không kết luận AI đạt yêu cầu nếu chưa kiểm tra được cả Frontend, Backend và dữ liệu hội thoại.

---

# PHẦN H. KIỂM TOÁN THANH TOÁN VÀ BẢO MẬT

Đánh giá khả năng tích hợp cổng thanh toán thực tế.

Kiểm tra:
- Cấu trúc payment service.
- Tạo payment request.
- Xác thực chữ ký.
- Callback/Webhook.
- Chống giả mạo trạng thái thanh toán.
- Chống xử lý giao dịch trùng.
- Xử lý giao dịch pending.
- Xử lý thanh toán thất bại.
- Xử lý hoàn tiền.
- Đối soát đơn hàng và giao dịch.

Đặc biệt:
Không được cho phép Frontend tự quyết định một đơn hàng đã thanh toán thành công.

Kiểm tra bảo mật:
- Mật khẩu và session.
- JWT/cookie nếu có.
- Phân quyền Admin và nhân viên.
- Bảo vệ API.
- CORS.
- HTTPS readiness.
- Rate limiting.
- Upload hình ảnh.
- Bảo vệ thông tin cá nhân.
- Quản lý secret và environment variables.
- Backup và phục hồi dữ liệu.

Không tiết lộ giá trị của bất kỳ secret nào.

---

# PHẦN I. KIỂM TOÁN KHẢ NĂNG ĐƯA LÊN PRODUCTION

Đánh giá:
1. Có thể build Frontend production không?
2. Có thể chạy Backend production không?
3. Có cấu hình database production không?
4. Có cấu hình domain và HTTPS không?
5. Có quy trình triển khai không?
6. Có health check không?
7. Có logging và monitoring không?
8. Có backup tự động không?
9. Có quy trình rollback không?
10. Có cơ chế xử lý khi server ngừng hoạt động không?

Đánh giá khả năng phục vụ quy mô nhỏ ban đầu, nhưng không thiết kế theo hướng khó mở rộng.

Không tự ý deploy hoặc thay đổi server hiện tại.

---

# PHẦN J. YÊU CẦU BÁO CÁO CUỐI CÙNG

Sau khi hoàn tất kiểm toán, xuất báo cáo theo cấu trúc:

## 1. Executive Summary
Tóm tắt hiện trạng, mức độ sẵn sàng Production và các vấn đề nghiêm trọng.

## 2. Technology Stack
Bảng công nghệ thực tế đang sử dụng.

## 3. System Architecture
Sơ đồ Mermaid thể hiện toàn bộ hệ thống.

## 4. Module Audit Matrix
Bảng gồm:
- Module.
- Chức năng.
- Trạng thái.
- Bằng chứng.
- Mức độ hoàn thiện.
- Vấn đề phát hiện.

## 5. Database Audit
Báo cáo cấu trúc và các vấn đề về tính toàn vẹn dữ liệu.

## 6. API Audit
Danh sách API và các vấn đề phát hiện.

## 7. AI Agent Audit
Đánh giá riêng toàn bộ chức năng AI.

## 8. Payment & Security Audit
Đánh giá khả năng thanh toán thực tế và bảo mật.

## 9. Production Readiness
Đánh giá các điều kiện cần có trước khi triển khai.

## 10. Critical Issues
Phân loại:
- P0: Nghiêm trọng, có thể gây mất dữ liệu, lộ dữ liệu hoặc tổn thất tài chính.
- P1: Lỗi nghiêm trọng ảnh hưởng nghiệp vụ cốt lõi.
- P2: Lỗi ảnh hưởng chức năng hoặc trải nghiệm.
- P3: Cải thiện và tối ưu.

## 11. Upgrade Roadmap
Xây dựng thứ tự xử lý:
- Việc cần sửa ngay.
- Việc cần nâng cấp.
- Việc cần bổ sung.
- Việc cần kiểm thử.
- Việc cần chuẩn bị triển khai.

## 12. Production Readiness Scorecard
Chấm điểm từng nhóm theo thang 100, nhưng phải có tiêu chí và bằng chứng. Không chấm điểm tùy ý.

## 13. Final Recommendation
Kết luận:
- Có thể tiếp tục nâng cấp code hiện tại hay không?
- Module nào nên giữ?
- Module nào cần sửa?
- Module nào cần viết lại?
- Những điều kiện nào bắt buộc hoàn thành trước Production?

---

# YÊU CẦU QUAN TRỌNG NHẤT

Không được chỉ tạo một báo cáo chung chung dựa trên tên file hoặc suy đoán.

Phải kiểm tra source code thực tế, truy vết các luồng dữ liệu và sử dụng bằng chứng cụ thể như đường dẫn file, tên API, tên bảng, vị trí code hoặc kết quả kiểm thử.

Nếu không thể truy cập hoặc kiểm thử một thành phần, hãy ghi rõ NOT VERIFIED và giải thích lý do.

Sau khi hoàn thành, chỉ xuất báo cáo kiểm toán và đề xuất lộ trình.

KHÔNG tự động triển khai bất kỳ thay đổi nào cho đến khi nhận được yêu cầu tiếp theo.
