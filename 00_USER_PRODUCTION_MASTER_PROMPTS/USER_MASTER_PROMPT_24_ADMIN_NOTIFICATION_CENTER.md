# USER MASTER PROMPT #24: 24 ADMIN NOTIFICATION CENTER
> **Nguồn gốc:** Prompt chỉ đạo thực tế từ Người dùng (User Request) tại Step 9746.
> **Độ dài gốc:** 6177 ký tự.
> **Mục đích trong thư viện:** Cung cấp toàn văn đặc tả nghiệp vụ, yêu cầu kỹ thuật và ràng buộc sản xuất thực tế mà người dùng đã trực tiếp chỉ đạo và kiểm chứng trong dự án Routine Web.

---

# TASK: FIX & COMPLETE ADMIN NOTIFICATION CENTER – ROUTINE WEB

Bạn là Senior Full-stack Engineer. Hãy kiểm tra và hoàn thiện toàn bộ chức năng thông báo trên Admin Dashboard của Routine Web.

## 1. HIỆN TRẠNG

Trên thanh Header Admin hiện có:
- Biểu tượng chuông thông báo.
- Chấm đỏ báo có thông báo.

Tuy nhiên, khi nhấn vào biểu tượng chuông, không có dropdown, popup hoặc danh sách thông báo nào hiển thị.

Đây là lỗi cần khắc phục triệt để.

## 2. KIỂM TRA NGUYÊN NHÂN TRƯỚC KHI SỬA

Kiểm tra toàn bộ luồng thông báo hiện tại:

Frontend:
- Admin Header.
- Notification Bell component.
- Dropdown/Notification Panel nếu đã tồn tại.
- State quản lý thông báo.
- Event click.
- API fetching.
- SSE EventSource.
- Cơ chế cập nhật số lượng thông báo chưa đọc.

Backend:
- Notification API.
- Notification Controller.
- Notification Service.
- Realtime Service.
- SSE endpoint /api/v1/realtime/stream.
- Các sự kiện ORDER_CREATED, PAYMENT_UPDATED, CONSULTATION_REQUESTED.
- Cơ chế lưu và truy xuất thông báo.
- Cơ chế xác định thông báo đã đọc/chưa đọc.

Database:
- Kiểm tra có bảng notifications hay chưa.
- Kiểm tra cấu trúc dữ liệu.
- Kiểm tra quan hệ với Admin hoặc người nhận.
- Kiểm tra trạng thái READ/UNREAD.
- Kiểm tra thời gian tạo và nội dung thông báo.

Không tự mặc định bảng hoặc API đã tồn tại. Phải đối chiếu source code và database thực tế.

## 3. HOÀN THIỆN GIAO DIỆN NOTIFICATION CENTER

Khi Admin nhấn vào biểu tượng chuông, phải hiển thị một dropdown thông báo chuyên nghiệp.

Các thành phần:

A. Header:
- Tiêu đề "Thông báo".
- Số lượng thông báo chưa đọc.
- Nút "Đánh dấu tất cả đã đọc".

B. Danh sách thông báo:

Mỗi thông báo cần có:
- Icon theo loại sự kiện.
- Tiêu đề.
- Nội dung ngắn.
- Thời gian phát sinh.
- Trạng thái đã đọc/chưa đọc.
- Hành động khi nhấn vào thông báo.

Phân loại:
- Đơn hàng mới.
- Thanh toán thành công.
- Thanh toán thất bại.
- Yêu cầu tư vấn mới.
- Khách hàng cần hỗ trợ.
- Cập nhật trạng thái đơn hàng.
- Các sự kiện quản trị quan trọng khác nếu hệ thống đang hỗ trợ.

C. Footer:
- Nút "Xem tất cả thông báo" nếu có trang thông báo riêng.

D. Các trạng thái giao diện:
- Có thông báo chưa đọc.
- Không có thông báo.
- Đang tải.
- Không tải được thông báo.
- Có thông báo mới.
- Dropdown không bị cắt hoặc che khuất bởi Header.

Thiết kế tối giản, phù hợp với giao diện Admin hiện tại của Routine. Không lạm dụng màu sắc, hiệu ứng hoặc card.

## 4. HOÀN THIỆN LOGIC THÔNG BÁO

Phải đảm bảo:

1. Khi có đơn hàng mới, Admin nhận được thông báo.
2. Khi có giao dịch thanh toán thành công, Admin nhận được thông báo.
3. Khi có giao dịch thanh toán thất bại, Admin nhận được thông báo phù hợp.
4. Khi khách hàng gửi yêu cầu chuyển tiếp tư vấn AI và đồng ý gặp chuyên viên, Admin nhận được thông báo.
5. Khi có sự kiện quan trọng khác, hệ thống tạo thông báo theo đúng nghiệp vụ.

Thông báo phải được lưu trữ bền vững trong Database, không chỉ tồn tại trong RAM hoặc state của Frontend.

Không tạo thông báo giả lập để làm giao diện có vẻ hoạt động.

## 5. HOÀN THIỆN REALTIME SSE

Tận dụng hệ thống SSE hiện có tại:

GET /api/v1/realtime/stream

Kiểm tra và hoàn thiện cơ chế:

Backend phát sinh sự kiện
→ Notification Service lưu thông báo vào Database
→ Realtime Service phát sự kiện SSE
→ Admin Frontend nhận sự kiện
→ Notification Bell cập nhật số lượng chưa đọc
→ Dropdown hiển thị thông báo mới.

Yêu cầu:
- Không cần tải lại trang để nhận thông báo mới.
- Không tạo thông báo trùng khi SSE tự kết nối lại.
- Có cơ chế reconnect khi mất kết nối.
- Có xác thực quyền Admin đối với luồng thông báo.
- Không để khách hàng truy cập được thông báo nội bộ của Admin.
- Khi tải lại trang, thông báo cũ vẫn còn.
- Số lượng chưa đọc phải được đồng bộ với Database.

Nếu SSE hiện tại đã hỗ trợ một phần thì tận dụng, không viết lại toàn bộ.

## 6. XỬ LÝ CÁC THAO TÁC

Khi Admin nhấn vào một thông báo:

- Đánh dấu thông báo đó đã đọc.
- Cập nhật số lượng chưa đọc ngay lập tức.
- Điều hướng đến đúng chức năng liên quan.

Ví dụ:

Đơn hàng mới:
→ Mở trang quản lý đơn hàng.
→ Có thể mở trực tiếp chi tiết đơn tương ứng.

Yêu cầu tư vấn:
→ Mở trang Admin Leads.
→ Tự động chọn đúng khách hàng và hội thoại.
→ Nhân viên có thể tiếp tục nhắn tin.

Thanh toán:
→ Mở chi tiết đơn hàng và trạng thái giao dịch.

Nút "Đánh dấu tất cả đã đọc":
→ Cập nhật trạng thái trên Database.
→ Đồng bộ lại số lượng chưa đọc.

## 7. KIỂM TRA BẢO MẬT

- Chỉ Admin được quyền xem Notification Center của Admin.
- CUSTOMER không được truy cập API thông báo nội bộ.
- Không tin tưởng role do Frontend tự gửi lên.
- Backend phải xác thực JWT và role thực tế.
- Không để người dùng truy cập thông báo của người khác bằng cách thay ID.
- Không đưa thông tin thanh toán nhạy cảm vào nội dung thông báo.

## 8. KIỂM THỬ END-TO-END

Thực hiện các test case:

TEST 1:
Admin nhấn chuông.
→ Dropdown hiển thị bình thường.

TEST 2:
Có đơn hàng mới.
→ Admin nhận thông báo realtime.

TEST 3:
Có khách hàng yêu cầu tư vấn AI.
→ Admin nhận thông báo.
→ Nhấn thông báo mở đúng hội thoại.

TEST 4:
Admin đánh dấu một thông báo đã đọc.
→ Trạng thái được lưu Database.
→ Số lượng chưa đọc giảm chính xác.

TEST 5:
Admin đánh dấu tất cả đã đọc.
→ Tất cả thông báo được cập nhật.

TEST 6:
Admin tải lại trang.
→ Thông báo vẫn được giữ nguyên.

TEST 7:
Mất kết nối rồi kết nối lại SSE.
→ Không bị mất hoặc nhân đôi thông báo.

TEST 8:
Customer cố truy cập API Notification Admin.
→ Backend từ chối.

TEST 9:
Không có thông báo.
→ Hiển thị trạng thái rỗng chuyên nghiệp, không để dropdown trống bất thường.

## 9. BÁO CÁO NGHIỆM THU

Sau khi hoàn thành, báo cáo:
- Nguyên nhân lỗi ban đầu.
- File Frontend đã sửa.
- File Backend đã sửa.
- API đã bổ sung hoặc chỉnh sửa.
- Database đã thay đổi (nếu có).
- Cơ chế SSE đã hoàn thiện.
- Kết quả 9 test case.
- Những phần chưa kiểm chứng được.

Không tự tạo dữ liệu giả và không báo PASS nếu chưa thực sự kiểm thử.

MỤC TIÊU:
Biến biểu tượng chuông hiện tại thành một Notification Center hoàn chỉnh, hoạt động realtime, lưu trữ bền vững, bảo mật và liên kết trực tiếp với các nghiệp vụ của Routine Web.
