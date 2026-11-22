# USER MASTER PROMPT #25: 25 PRODUCTION UPGRADE NOTIFICATION HANDOFF
> **Nguồn gốc:** Prompt chỉ đạo thực tế từ Người dùng (User Request) tại Step 10157.
> **Độ dài gốc:** 7090 ký tự.
> **Mục đích trong thư viện:** Cung cấp toàn văn đặc tả nghiệp vụ, yêu cầu kỹ thuật và ràng buộc sản xuất thực tế mà người dùng đã trực tiếp chỉ đạo và kiểm chứng trong dự án Routine Web.

---

# ROUTINE WEB – PRODUCTION UPGRADE TASK 01
## COMPLETE ADMIN NOTIFICATION CENTER + AI HUMAN HANDOFF

Bạn đang tiếp tục phát triển codebase Routine Web hiện tại.

Đây là nhiệm vụ nâng cấp hệ thống đang tồn tại, không phải xây dựng một dự án mới.

TECH STACK ĐÃ ĐƯỢC KIỂM TOÁN:
- Frontend: Next.js 16.4.3, React 19.2.3.
- Backend: Node.js, Express.js 4.22.3.
- Database: MySQL 8.0, Prisma 6.19.3.
- Authentication: JWT.
- Realtime: Server-Sent Events.
- AI: Gemini SDK @google/genai.

CÁC FILE ĐÃ ĐƯỢC GHI NHẬN TRONG BÁO CÁO:
- frontend/app/admin/leads/page.jsx
- backend/src/services/conversationService.js
- backend/src/services/realtimeService.js
- backend/src/controllers/conversationController.js
- backend/src/routes/api.js

Hãy kiểm tra đường dẫn và cấu trúc thực tế trước khi can thiệp.

## PHẦN 1. KIỂM TRA NOTIFICATION DATA MODEL

Trước tiên, kiểm tra toàn bộ Prisma schema và database thực tế.

Xác định:
- Có bảng notifications hay chưa.
- Có API lấy danh sách thông báo hay chưa.
- Có API đánh dấu đã đọc hay chưa.
- Có API đánh dấu tất cả đã đọc hay chưa.
- SSE đang phát những event nào.
- Sự kiện có được lưu lại sau khi phát hay không.
- Thông báo có gắn với người nhận cụ thể hay không.

Nếu chưa có Notification Model, hãy thiết kế bổ sung phù hợp với kiến trúc hiện tại.

Đề xuất các trường:
- id
- recipientId
- type
- title
- message
- referenceType
- referenceId
- isRead
- createdAt
- updatedAt

Thiết lập quan hệ với User và các index cần thiết.

Không tạo bảng trùng nếu hệ thống đã có model tương đương.

Mọi thay đổi database phải thông qua Prisma Migration có kiểm soát. Không reset database, không xóa dữ liệu cũ.

## PHẦN 2. HOÀN THIỆN NOTIFICATION BACKEND

Xây dựng hoặc hoàn thiện các API tương ứng:

GET /api/v1/admin/notifications
GET /api/v1/admin/notifications/unread-count
PATCH /api/v1/admin/notifications/:id/read
PATCH /api/v1/admin/notifications/read-all

Tên endpoint có thể điều chỉnh theo quy chuẩn API hiện tại để tránh trùng lặp.

Yêu cầu:
- Chỉ Admin có quyền truy cập.
- Phân trang thông báo.
- Sắp xếp mới nhất trước.
- Lọc đã đọc/chưa đọc.
- Không trả về thông báo của người dùng khác.
- Cập nhật trạng thái đọc trên MySQL.
- Trả về response thống nhất theo response.js hiện tại.

## PHẦN 3. KẾT NỐI CÁC NGHIỆP VỤ SINH THÔNG BÁO

Tích hợp Notification Service vào các sự kiện thực tế.

A. ĐƠN HÀNG:
Khi khách hàng tạo đơn hàng thành công:
- Lưu đơn hàng.
- Lưu chi tiết đơn.
- Phát sinh thông báo cho Admin.
- Nội dung có mã đơn hàng và giá trị đơn hàng.
- Nhấn thông báo mở đúng trang chi tiết đơn.

B. THANH TOÁN:
Khi Backend xác minh thanh toán thành công:
- Tạo thông báo thanh toán thành công.
- Liên kết với đơn hàng.
- Không phát thông báo thành công chỉ dựa vào Frontend Return URL.

C. TƯ VẤN AI:
Khi khách hàng đồng ý yêu cầu gặp chuyên viên:
- Cập nhật trạng thái hội thoại thành LEAD_PENDING.
- Tạo thông báo CONSULTATION_REQUESTED.
- Liên kết với conversationId.
- Gửi sự kiện realtime đến Admin.
- Không tạo thông báo trùng khi khách nhấn nhiều lần hoặc SSE reconnect.

D. CÁC SỰ KIỆN KHÁC:
Chỉ triển khai những sự kiện thực sự có trong nghiệp vụ hiện tại.

Phải đảm bảo tạo dữ liệu thông báo và cập nhật trạng thái nghiệp vụ một cách nhất quán, ưu tiên transaction khi phù hợp.

## PHẦN 4. HOÀN THIỆN SSE

Tận dụng GET /api/v1/realtime/stream hiện có.

Luồng yêu cầu:

Business Event
→ Notification Service
→ MySQL
→ SSE Event
→ Admin Frontend
→ Notification Bell cập nhật.

Yêu cầu:
- Reconnect khi mất kết nối.
- Không nhân đôi thông báo.
- Không làm mất thông báo khi Admin offline.
- Khi kết nối lại, Frontend lấy dữ liệu từ Database.
- Xác thực Admin trước khi mở SSE.
- Không phát dữ liệu nội bộ cho Customer.
- Có xử lý heartbeat và đóng kết nối đúng cách.

Với quy mô nhỏ, có thể tiếp tục dùng SSE lưu kết nối trong RAM như kiến trúc hiện tại. Chưa cần triển khai Redis nếu chưa chạy nhiều Backend instance.

## PHẦN 5. HOÀN THIỆN GIAO DIỆN ADMIN NOTIFICATION CENTER

Khi nhấn biểu tượng chuông ở Header Admin, phải mở dropdown thông báo.

Thiết kế:
- Tiêu đề Thông báo.
- Số thông báo chưa đọc.
- Danh sách thông báo mới nhất.
- Icon theo từng loại sự kiện.
- Tiêu đề và nội dung.
- Thời gian.
- Trạng thái đọc/chưa đọc.
- Đánh dấu tất cả đã đọc.
- Xem tất cả nếu hệ thống có trang riêng.

Các trạng thái:
- Loading.
- Empty.
- Error.
- Loaded.
- New notification.

Không sử dụng dữ liệu giả lập.

Không để dropdown bị che hoặc cắt bởi Header, viewport hoặc các container cha.

## PHẦN 6. HOÀN THIỆN AI HUMAN HANDOFF

Đây là phần bắt buộc phải kiểm thử liên thông.

Luồng:

Customer
→ Gemini AI Stylist
→ Nhận diện nhu cầu gặp chuyên viên
→ Đề nghị chuyển tiếp
→ Customer đồng ý
→ LEAD_PENDING
→ Admin nhận thông báo
→ Mở đúng hội thoại
→ Nhân viên tiếp quản
→ Nhắn tin trực tiếp với khách
→ Customer nhận phản hồi.

Kiểm tra:
- conversationId.
- customerId.
- Trạng thái hội thoại.
- Tin nhắn cũ.
- Tin nhắn mới.
- Người gửi.
- Thời gian gửi.
- Cơ chế phân biệt tin nhắn AI và chuyên viên.

Không được chỉ chuyển trạng thái giao diện thành HUMAN_TAKEOVER mà không cập nhật Backend.

Khi nhân viên gửi tin nhắn:
- Lưu vào database.
- Liên kết đúng conversation.
- Phát realtime cho khách.
- Không làm mất lịch sử hội thoại.
- AI không tự động chen vào khi chuyên viên đang tiếp quản, trừ khi có quy trình bàn giao lại rõ ràng.

Nếu khách tiếp tục gửi tin nhắn khi nhân viên offline, phải lưu lại để nhân viên xử lý sau.

## PHẦN 7. END-TO-END TEST

Kiểm thử trên staging hoặc môi trường có dữ liệu test riêng.

TEST 1:
Admin nhấn chuông, dropdown mở.

TEST 2:
Tạo đơn hàng mới, Admin nhận thông báo.

TEST 3:
Khách đồng ý chuyển tiếp tư vấn AI, Admin nhận thông báo.

TEST 4:
Nhấn thông báo tư vấn, mở đúng conversationId.

TEST 5:
Nhân viên phản hồi, khách nhận được tin nhắn.

TEST 6:
Đánh dấu đã đọc, database cập nhật chính xác.

TEST 7:
Reload trang, thông báo vẫn tồn tại.

TEST 8:
Ngắt SSE, kết nối lại, không mất hoặc trùng thông báo.

TEST 9:
Customer gọi API Admin Notification, Backend từ chối.

TEST 10:
Hai Admin hoặc nhân viên có quyền phù hợp không được xem dữ liệu ngoài phạm vi phân quyền.

## PHẦN 8. NGUYÊN TẮC TRIỂN KHAI

- Giữ nguyên các module không liên quan.
- Không thay đổi dữ liệu sản phẩm, khách hàng và đơn hàng hiện có.
- Không xóa lịch sử hội thoại.
- Không reset database.
- Không tạo dữ liệu giả để báo cáo PASS.
- Không tự triển khai lên Production.
- Không thay đổi cấu hình thanh toán thật.

## PHẦN 9. BÁO CÁO NGHIỆM THU

Báo cáo:
1. Nguyên nhân Notification Center không hoạt động.
2. Cấu trúc Database trước và sau.
3. API được bổ sung hoặc sửa.
4. File Frontend và Backend được thay đổi.
5. Luồng SSE.
6. Luồng AI Handoff.
7. Kết quả 10 test case.
8. Những vấn đề chưa giải quyết.
9. Khả năng vận hành của module sau nâng cấp.

Chỉ báo cáo PASS khi đã kiểm thử thực tế.

MỤC TIÊU:
Hoàn thiện Notification Center và AI Human Handoff thành một quy trình chăm sóc khách hàng thực tế, đồng bộ giữa Customer Frontend, Admin Dashboard, Backend và MySQL.
