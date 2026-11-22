# USER MASTER PROMPT #10: 10 FINAL HANDOVER LOCK
> **Nguồn gốc:** Prompt chỉ đạo thực tế từ Người dùng (User Request) tại Step 3022.
> **Độ dài gốc:** 2022 ký tự.
> **Mục đích trong thư viện:** Cung cấp toàn văn đặc tả nghiệp vụ, yêu cầu kỹ thuật và ràng buộc sản xuất thực tế mà người dùng đã trực tiếp chỉ đạo và kiểm chứng trong dự án Routine Web.

---

# FINAL HANDOVER LOCK – ROUTINE WEB

Sau khi hoàn thành toàn bộ công việc trước đó, hãy thực hiện bước bàn giao cuối cùng để tôi trực tiếp kiểm thử thủ công.

**1. Xác nhận trạng thái hệ thống**
- Kiểm tra Frontend và Backend đang hoạt động.
- Xác nhận Database đang kết nối đúng môi trường Demo.
- Kiểm tra Gemini AI, API, hình ảnh và các tích hợp hiện có.
- Xác nhận không còn lỗi CRITICAL hoặc HIGH chưa được báo cáo.

**2. Bảo toàn dữ liệu**
- Giữ nguyên bộ dữ liệu Demo đã chuẩn bị.
- Không tiếp tục xóa tài khoản, khách hàng, sản phẩm hoặc đơn hàng.
- Không xóa dữ liệu mô phỏng cần thiết cho việc kiểm thử.
- Không ghi dữ liệu vào Database thật.
- Không thay đổi cấu hình Cloudinary, Gemini hoặc các file môi trường.

**3. Khóa trạng thái phát triển**
- Không tự động sửa code hoặc refactor tiếp.
- Không chạy các tác vụ tự động có thể làm thay đổi dữ liệu.
- Không tự động tạo thêm khách hàng, đơn hàng hoặc giao dịch.
- Không chạy migration hoặc cập nhật cấu trúc Database.
- Giữ nguyên phiên bản hiện tại để tôi nghiệm thu.

**4. Chuẩn bị truy cập**
Cung cấp chính xác:
- Địa chỉ website Customer.
- Địa chỉ Admin.
- Tài khoản Admin.
- Tài khoản Customer.
- Cách khởi động lại hệ thống.
- Trạng thái kết nối Database.
- Danh sách sản phẩm và đơn hàng Demo có sẵn.
- Các tính năng có thể kiểm thử.
- Các tính năng chưa hoàn thiện hoặc cần API bên ngoài.

**5. Kiểm tra khả năng tự nghiệm thu**
Mở trình duyệt và xác nhận tôi có thể:
- Đăng nhập Admin.
- Đăng nhập Customer.
- Xem sản phẩm.
- Thao tác quản lý sản phẩm.
- Thực hiện mua hàng.
- Kiểm tra phí vận chuyển.
- Kiểm tra đơn hàng.
- Sử dụng Gemini AI Stylist.
- Xem báo cáo kinh doanh và các chức năng AI quản trị đã triển khai.

**6. Kết thúc**
Sau khi xác nhận tất cả nội dung trên, dừng mọi hoạt động phát triển tự động và bàn giao hệ thống.

Không tuyên bố chức năng đã hoàn thiện nếu chưa có bằng chứng kiểm tra thực tế.
