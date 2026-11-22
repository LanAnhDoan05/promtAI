# USER MASTER PROMPT #23: 23 HERO SLIDER AND BRAND EXPERIENCE
> **Nguồn gốc:** Prompt chỉ đạo thực tế từ Người dùng (User Request) tại Step 9478.
> **Độ dài gốc:** 6486 ký tự.
> **Mục đích trong thư viện:** Cung cấp toàn văn đặc tả nghiệp vụ, yêu cầu kỹ thuật và ràng buộc sản xuất thực tế mà người dùng đã trực tiếp chỉ đạo và kiểm chứng trong dự án Routine Web.

---

# TASK: FIX HOMEPAGE HERO, ACCOUNT DROPDOWN & BRAND EXPERIENCE – ROUTINE WEB

Bạn là Senior Frontend Engineer kiêm UI/UX Designer chịu trách nhiệm hoàn thiện giao diện thương mại điện tử Routine trước khi đưa vào Production.

Hãy trực tiếp kiểm tra và sửa giao diện đang chạy tại localhost:3000 theo ảnh chụp màn hình được cung cấp.

## I. NGUYÊN TẮC THỰC HIỆN

- Giữ nguyên kiến trúc Next.js, React và Backend hiện tại.
- Không viết lại toàn bộ trang chủ.
- Không tự ý thay đổi database hoặc xóa dữ liệu.
- Không làm hỏng các chức năng tìm kiếm, yêu thích, giỏ hàng, tài khoản.
- Không thay đổi nhận diện thương hiệu Routine một cách tùy tiện.
- Phải xác định đúng file và nguồn dữ liệu gây ra lỗi trước khi sửa.
- Không chỉ sửa giao diện ở một trạng thái mà bỏ qua các trạng thái đăng nhập khác.

## II. SỬA LỖI HERO SECTION – TRANG CHỦ

Hiện trạng:

Trên giao diện đang xuất hiện dòng:

HERO FROM CLOUD DATABA...

Đây là nội dung không phù hợp với website bán hàng thời trang thực tế.

Yêu cầu:

1. Truy tìm chính xác nguồn nội dung này:
   - Homepage component.
   - Hero Banner component.
   - Database hoặc Store Settings.
   - API trả về nội dung banner.
   - Nội dung mặc định hoặc fallback.
   - Các dữ liệu seed hoặc placeholder còn sót lại.

2. Xác định nguyên nhân tại sao nội dung kỹ thuật lại xuất hiện trên giao diện khách hàng.

3. Thay thế bằng nội dung thương hiệu thời trang Routine phù hợp với bộ sưu tập Thu Đông.

Nội dung định hướng:

- Eyebrow: ROUTINE THU ĐÔNG – SMART FASHION.
- Headline: THU ĐÔNG, ĐỊNH HÌNH PHONG CÁCH.
- Description: Khám phá những thiết kế thời trang hiện đại, tinh tế và linh hoạt cho phong cách mỗi ngày.

Có thể điều chỉnh câu chữ để phù hợp hơn với thiết kế, nhưng tuyệt đối không để xuất hiện nội dung kỹ thuật, tên biến, placeholder hoặc thông tin database trên giao diện khách hàng.

4. Xử lý responsive:
   - Tiêu đề không được tràn khỏi khung.
   - Không bị cắt chữ ở desktop.
   - Không bị chồng lấn khi xem trên điện thoại.
   - Tự động điều chỉnh kích thước chữ theo màn hình.
   - Nội dung phải nằm trong vùng an toàn của Hero.
   - Đảm bảo ảnh nền không che mất nội dung.

5. Điều chỉnh lớp phủ ảnh (Overlay):
   - Đảm bảo chữ dễ đọc.
   - Không làm ảnh tối quá mức.
   - Giữ được chất lượng ảnh thời trang.
   - Cân đối khoảng cách giữa eyebrow, headline và description.

## III. SỬA MENU TÀI KHOẢN

Hiện trạng:

Khi khách hàng chưa đăng nhập, nhấn biểu tượng tài khoản, dropdown hiển thị:

- Tài khoản.
- Chưa đăng nhập.
- Đăng nhập.
- Đăng ký tài khoản.
- Vào trang Quản trị (Admin).

Yêu cầu:

1. Không hiển thị mục "Vào trang Quản trị (Admin)" trong menu tài khoản của khách hàng chưa đăng nhập.

2. Với tài khoản CUSTOMER:
   - Hiển thị thông tin tài khoản.
   - Hồ sơ cá nhân.
   - Đơn hàng của tôi.
   - Sản phẩm yêu thích.
   - Đăng xuất.

3. Với người chưa đăng nhập:
   - Đăng nhập.
   - Đăng ký tài khoản.
   - Không hiển thị chức năng quản trị.

4. Với tài khoản ADMIN:
   - Có thể hiển thị đường dẫn quản trị trong giao diện tài khoản nếu phù hợp.
   - Chỉ tài khoản có role ADMIN hợp lệ mới được truy cập Admin Dashboard.

5. Kiểm tra cả hai lớp bảo vệ:
   - Frontend: Ẩn các mục điều hướng không có quyền.
   - Backend: Xác thực và phân quyền thực tế cho mọi API quản trị.

6. Không được chỉ ẩn nút Admin bằng CSS hoặc điều kiện giao diện trong khi vẫn cho phép khách hàng truy cập trực tiếp đường dẫn /admin.

7. Đảm bảo không xảy ra lỗi rò rỉ phiên đăng nhập giữa Customer và Admin.

## IV. NÂNG CẤP THIẾT KẾ HEADER

Giữ phong cách tối giản hiện tại của Routine nhưng cải thiện tính chuyên nghiệp.

Yêu cầu:
- Logo/Wordmark chính giữa cân đối.
- Menu hamburger bên trái.
- Các biểu tượng tìm kiếm, yêu thích, giỏ hàng và tài khoản bên phải.
- Kích thước icon đồng nhất.
- Khoảng cách giữa các icon hợp lý.
- Dropdown tài khoản có chiều rộng và khoảng cách phù hợp.
- Không bị lệch vị trí khi mở dropdown.
- Có trạng thái hover, focus và click rõ ràng.
- Không che khuất những thành phần quan trọng của Hero.
- Responsive trên desktop, tablet và mobile.

Không tự ý thêm quá nhiều hiệu ứng, gradient, bo góc hoặc các thành phần trang trí không cần thiết.

## V. QUY CHUẨN THIẾT KẾ DOANH NGHIỆP

Website phải mang cảm giác của một thương hiệu thời trang đang hoạt động thực tế.

Ưu tiên:
- Typography rõ ràng, có phân cấp.
- Khoảng trắng hợp lý.
- Ảnh thời trang chất lượng cao.
- Bố cục có chủ đích.
- Màu sắc nhất quán.
- Hạn chế hiệu ứng chuyển động.
- Nội dung ngắn gọn, đúng ngôn ngữ thương hiệu.
- Không sử dụng các nội dung chung chung kiểu AI tạo tự động.

Không:
- Tạo thêm card hoặc box không cần thiết.
- Lạm dụng glassmorphism.
- Lạm dụng shadow.
- Sử dụng gradient tùy tiện.
- Đưa các cụm từ kỹ thuật lên giao diện người dùng.
- Tự ý thay đổi những phần đang hoạt động tốt.

## VI. KIỂM THỬ SAU KHI SỬA

Phải kiểm tra trực tiếp tại localhost:3000.

TEST CASE 1 – Khách chưa đăng nhập:
- Truy cập trang chủ.
- Mở menu tài khoản.
- Kiểm tra không còn mục Admin.
- Đăng nhập và đăng ký vẫn hoạt động.

TEST CASE 2 – Khách hàng CUSTOMER:
- Đăng nhập.
- Mở menu tài khoản.
- Kiểm tra đúng thông tin khách hàng.
- Kiểm tra hồ sơ và lịch sử đơn hàng.
- Không được xuất hiện quyền quản trị.

TEST CASE 3 – Tài khoản ADMIN:
- Đăng nhập Admin.
- Kiểm tra đường dẫn quản trị.
- Truy cập Admin Dashboard thành công.
- Kiểm tra các API quản trị vẫn hoạt động.

TEST CASE 4 – Bảo mật:
- Đăng xuất.
- Thử truy cập trực tiếp /admin.
- Thử gọi API quản trị khi không có quyền.
- Đảm bảo hệ thống từ chối truy cập.

TEST CASE 5 – Hero Section:
- Không còn nội dung HERO FROM CLOUD DATABASE.
- Không có placeholder kỹ thuật.
- Không tràn hoặc cắt chữ.
- Ảnh hiển thị đúng.
- Nội dung đẹp trên desktop và mobile.

TEST CASE 6 – Responsive:
Kiểm tra tối thiểu ở các kích thước:
- 1440px.
- 1280px.
- 768px.
- 390px.

## VII. BÁO CÁO SAU KHI HOÀN THÀNH

Xuất báo cáo:
1. Nguyên nhân từng lỗi.
2. Danh sách file đã sửa.
3. Những thay đổi giao diện.
4. Những thay đổi logic phân quyền.
5. Kết quả từng test case.
6. Những vấn đề chưa thể khắc phục.

Chỉ báo cáo PASS khi đã kiểm thử thực tế.

Không được tự nhận hoàn thành nếu mới chỉ sửa code mà chưa kiểm tra giao diện đang chạy.

MỤC TIÊU CUỐI CÙNG:

Hoàn thiện trang chủ Routine với giao diện thời trang chuyên nghiệp, nội dung thương hiệu chính xác, menu tài khoản đúng quyền hạn và sẵn sàng tiếp tục nâng cấp lên môi trường Production.
