# USER MASTER PROMPT #27: 27 GLOBAL BRANDING AND WARNING AUDIT
> **Nguồn gốc:** Prompt chỉ đạo thực tế từ Người dùng (User Request) tại Step 10979.
> **Độ dài gốc:** 5847 ký tự.
> **Mục đích trong thư viện:** Cung cấp toàn văn đặc tả nghiệp vụ, yêu cầu kỹ thuật và ràng buộc sản xuất thực tế mà người dùng đã trực tiếp chỉ đạo và kiểm chứng trong dự án Routine Web.

---

# TASK: GLOBAL BRANDING UPDATE – ROUTINE THU ĐÔNG + FULL WARNING AUDIT

**Dự án:** ROUTINE E-COMMERCE PLATFORM  
**Mục tiêu:** Chuẩn hóa nhận diện thương hiệu thành "Routine Thu Đông" trên toàn bộ giao diện website và kiểm tra, xử lý 88 cảnh báo hiện có.

## PHẦN A – TÌM KIẾM VÀ CHUẨN HÓA TÊN THƯƠNG HIỆU

### 1. Quét toàn bộ dự án

Tìm tất cả vị trí xuất hiện của các cụm:
- Routine
- ROUTINE
- routine
- Routine Fashion
- Các cách viết khác có chứa tên thương hiệu Routine.

Phạm vi tìm kiếm bao gồm:
- Frontend: trang chủ, header, footer, menu, banner, nội dung sản phẩm, trang chi tiết, giỏ hàng, thanh toán, tài khoản khách hàng.
- Backend: email gửi khách hàng, thông báo, nội dung phản hồi API có hiển thị ra giao diện.
- Admin: tiêu đề trang, dashboard, thông báo, giao diện quản trị nếu có nội dung nhận diện thương hiệu.
- Metadata: SEO title, description, Open Graph, favicon metadata và nội dung chia sẻ.
- Các file cấu hình nội dung và dữ liệu mẫu có liên quan đến nội dung hiển thị.

### 2. Quy tắc thay đổi

Đổi tên thương hiệu hiển thị cho người dùng từ:

"Routine" → "Routine Thu Đông"

Yêu cầu:
- Viết đúng chính tả, đúng kiểu chữ và thống nhất toàn website.
- Không thay thế một phần từ không liên quan.
- Không tạo ra các cụm lặp như "Routine Thu Đông Thu Đông".
- Không thay đổi tên thương hiệu trong các ngữ cảnh không phải nội dung hiển thị nếu có nguy cơ gây lỗi.

### 3. Những thành phần tuyệt đối không tự ý đổi

Không tự động thay thế trong:
- Tên biến, tên hàm, tên class, tên component.
- Tên bảng, cột database, Prisma model và quan hệ.
- API endpoint, route, URL, domain.
- Tên thư mục, tên file và đường dẫn import.
- Package name, dependency, script chạy dự án.
- Environment variables, credentials, khóa API.
- Dữ liệu lịch sử đơn hàng, giao dịch và tài khoản khách hàng.
- Các định danh kỹ thuật đang được Frontend và Backend sử dụng chung.

Nếu phát hiện những trường hợp trên, chỉ báo cáo và đề xuất phương án riêng, không tự ý đổi.

## PHẦN B – KIỂM TRA VÀ XỬ LÝ 88 WARNINGS

### 1. Xác định chính xác nguồn cảnh báo

Không mặc định 88 cảnh báo đều thuộc cùng một loại.

Hãy chạy các công cụ kiểm tra phù hợp với dự án hiện tại:
- Frontend: ESLint, TypeScript (nếu đang sử dụng), Next.js build.
- Backend: ESLint, kiểm tra cú pháp và các bài test hiện có.
- Prisma: kiểm tra schema và trạng thái đồng bộ.
- Các công cụ kiểm tra khác đang được cấu hình trong package.json.

Đọc toàn bộ kết quả và xác định:
- File phát sinh cảnh báo.
- Dòng code liên quan.
- Nội dung cảnh báo.
- Nguyên nhân.
- Mức độ ảnh hưởng.
- Khả năng gây lỗi khi chạy thực tế.

### 2. Phân loại

Chia cảnh báo thành:

A. Cần sửa:
- Biến hoặc import không sử dụng.
- Dependency trong React Hook chưa đầy đủ gây lỗi logic.
- Sai kiểu dữ liệu.
- Xử lý bất đồng bộ không an toàn.
- Thiếu kiểm tra lỗi.
- Vấn đề bảo mật.
- Lỗi accessibility ảnh hưởng đến khả năng sử dụng.
- Các vấn đề có nguy cơ gây lỗi thực tế.

B. Có thể sửa:
- Cách viết code chưa tối ưu.
- Cảnh báo deprecated có phương án thay thế tương thích.
- Các vấn đề hiệu năng có căn cứ.

C. Có thể giữ lại:
- Cảnh báo từ thư viện bên thứ ba.
- Cảnh báo không ảnh hưởng chức năng.
- Cảnh báo cần thay đổi kiến trúc lớn mới xử lý được.
- Cảnh báo do cấu hình hoặc môi trường không thể kiểm soát an toàn.

### 3. Nguyên tắc sửa

- Ưu tiên sửa tận gốc nguyên nhân.
- Không tắt ESLint hoặc TypeScript để làm biến mất cảnh báo.
- Không sử dụng eslint-disable, ts-ignore hoặc ép kiểu any chỉ để che cảnh báo.
- Không xóa chức năng đang hoạt động.
- Không thay đổi nghiệp vụ đơn hàng, thanh toán VNPAY, tồn kho, đăng nhập, phân quyền, AI Stylist và tư vấn viên nếu không thực sự cần thiết.
- Không nâng cấp hàng loạt dependency khi chưa đánh giá tính tương thích.
- Không reset database, không xóa dữ liệu và không chạy script seed/cleanup.
- Không sửa những phần code không liên quan chỉ để giảm số lượng cảnh báo.

## PHẦN C – KIỂM THỬ SAU KHI SỬA

Sau khi cập nhật thương hiệu và xử lý cảnh báo:

1. Chạy lại toàn bộ công cụ đã phát hiện 88 cảnh báo.
2. So sánh số lượng Errors và Warnings trước/sau.
3. Chạy Frontend build.
4. Chạy Backend và kiểm tra API.
5. Kiểm tra Prisma và kết nối MySQL.
6. Kiểm tra giao diện desktop và mobile.
7. Xác minh tên "Routine Thu Đông" hiển thị nhất quán.
8. Kiểm tra các chức năng quan trọng:
   - Đăng ký, đăng nhập, phân quyền.
   - Hiển thị sản phẩm và hình ảnh.
   - Tìm kiếm, lọc và giỏ hàng.
   - Tạo đơn hàng.
   - Thanh toán VNPAY Sandbox.
   - AI Stylist và chuyển tiếp hội thoại sang nhân viên tư vấn.
   - Thông báo quản trị và realtime.
   - Quản lý sản phẩm, đơn hàng trong Admin.

Không được tuyên bố PASS nếu chưa thực sự chạy kiểm thử.

## PHẦN D – BÁO CÁO KẾT QUẢ

Xuất báo cáo gồm:

1. Tổng số vị trí chứa tên Routine đã tìm thấy.
2. Số vị trí đã đổi thành Routine Thu Đông.
3. Các vị trí được giữ nguyên vì là định danh kỹ thuật.
4. Bảng 88 cảnh báo ban đầu: phân loại và nguyên nhân.
5. Danh sách cảnh báo đã sửa.
6. Danh sách cảnh báo còn lại và lý do.
7. Số Errors/Warnings sau khi sửa.
8. Kết quả Frontend Build, Backend, Prisma và các bài kiểm thử.
9. Danh sách file đã thay đổi.
10. Những vấn đề còn tồn tại cần xử lý tiếp.

**ĐIỀU KIỆN HOÀN THÀNH:**

Website sử dụng tên hiển thị "Routine Thu Đông" nhất quán; không làm hỏng các định danh kỹ thuật; các lỗi và cảnh báo quan trọng được xử lý; những cảnh báo còn lại được giải thích rõ ràng.

Không xóa dữ liệu, không viết lại dự án từ đầu, không tự ý thay đổi kiến trúc và không báo cáo kết quả giả lập.
