# USER MASTER PROMPT #11: 11 STOREFRONT DISPLAY STATISTICS
> **Nguồn gốc:** Prompt chỉ đạo thực tế từ Người dùng (User Request) tại Step 3079.
> **Độ dài gốc:** 6443 ký tự.
> **Mục đích trong thư viện:** Cung cấp toàn văn đặc tả nghiệp vụ, yêu cầu kỹ thuật và ràng buộc sản xuất thực tế mà người dùng đã trực tiếp chỉ đạo và kiểm chứng trong dự án Routine Web.

---

# FEATURE COMPLETION – PRODUCT COUNT & STOREFRONT DISPLAY STATISTICS

Hãy bổ sung chức năng thống kê số lượng sản phẩm trực quan cho toàn bộ hệ thống Routine Web, bao gồm Admin Product Management và Customer Storefront.

## 1. BỔ SUNG THỐNG KÊ TRÊN ADMIN – PRODUCTS

Tại trang `/admin/products`, phía trên khu vực tìm kiếm và bảng danh sách sản phẩm, bổ sung các thẻ thống kê:

1. **Tổng sản phẩm:** Tổng số sản phẩm trong Database.
2. **Đang trưng bày:** Số sản phẩm ACTIVE và đủ điều kiện hiển thị trên website khách hàng.
3. **Đang ẩn:** Số sản phẩm INACTIVE hoặc chưa được xuất bản.
4. **Hết hàng:** Số sản phẩm đang có tồn kho khả dụng bằng 0.
5. **Hiển thị trang chủ:** Số sản phẩm thực tế đủ điều kiện xuất hiện trong khu vực sản phẩm trên trang chủ.

Mỗi thẻ có:
- Tên chỉ số.
- Con số thực tế.
- Mô tả ngắn.
- Icon trực quan phù hợp.
- Giao diện đồng nhất với thiết kế Admin hiện tại.

Không làm thay đổi bố cục bảng sản phẩm hiện có.

## 2. THỐNG KÊ THEO BỘ LỌC

Ngay phía trên bảng Products, hiển thị:

- Đang hiển thị X / Y sản phẩm.
- X là số sản phẩm đang xuất hiện trong kết quả hiện tại.
- Y là tổng số sản phẩm phù hợp với bộ lọc hiện tại trước khi phân trang.

Khi Admin:
- Tìm kiếm sản phẩm.
- Lọc danh mục.
- Lọc giới tính.
- Lọc phong cách.
- Lọc trạng thái.
- Lọc tồn kho.
- Chuyển trang.

Các con số phải cập nhật chính xác theo dữ liệu mới.

Không lấy số dòng đang hiển thị trên một trang để làm tổng số sản phẩm.

## 3. THỐNG KÊ SẢN PHẨM TRÊN CUSTOMER STOREFRONT

Bổ sung số lượng sản phẩm trên các khu vực:

### Trang chủ
Tại mỗi khu vực trưng bày sản phẩm như:
- Sản phẩm mới.
- Sản phẩm nổi bật.
- Sản phẩm bán chạy.
- Sản phẩm khuyến mãi.
- Các bộ sưu tập sản phẩm.

Hiển thị số lượng thực tế, ví dụ:
- Sản phẩm nổi bật (12).
- Sản phẩm mới (8).
- Sản phẩm bán chạy (10).

Chỉ hiển thị số liệu nếu khu vực đó thực sự tồn tại và có dữ liệu.

### Trang danh mục
Hiển thị:
- Tổng số sản phẩm thuộc danh mục.
- Số sản phẩm đang được hiển thị.
- Kết quả cập nhật theo bộ lọc.

Ví dụ: `24 sản phẩm`.

### Trang tìm kiếm
Hiển thị:
- Tổng số kết quả phù hợp.
- Số sản phẩm đang hiển thị.
- Cập nhật theo từ khóa, bộ lọc và phân trang.

Ví dụ: `Tìm thấy 36 sản phẩm`.

### Các trang bộ sưu tập hoặc trang sản phẩm khác
Nếu có danh sách sản phẩm, hãy hiển thị số lượng phù hợp với thiết kế hiện tại.

## 4. QUY TẮC ĐẾM SẢN PHẨM

Đây là yêu cầu quan trọng nhất.

Phải thống nhất logic giữa Admin, Backend, Database và Customer:

- Tổng sản phẩm: đếm sản phẩm theo dữ liệu thực trong Database, không tính bản ghi đã xóa mềm.
- Sản phẩm đang trưng bày: chỉ tính sản phẩm ACTIVE, được phép xuất bản và đáp ứng điều kiện hiển thị của hệ thống.
- Sản phẩm trang chủ: chỉ đếm các sản phẩm thực sự đủ điều kiện xuất hiện trong từng khu vực trang chủ.
- Sản phẩm hết hàng: đếm theo tồn kho khả dụng, không suy luận từ số lượng tổng nếu hệ thống có cơ chế giữ hàng.
- Sản phẩm đang ẩn: không được tính vào số lượng sản phẩm khách hàng có thể mua.
- Sản phẩm hết hàng nhưng vẫn ACTIVE: phân biệt rõ giữa sản phẩm đang hiển thị và sản phẩm có thể mua.

Không đếm biến thể size/màu thành sản phẩm riêng. Một sản phẩm có nhiều biến thể vẫn chỉ tính là một sản phẩm.

Không đếm trùng sản phẩm nếu sản phẩm xuất hiện ở nhiều danh mục hoặc nhiều khu vực.

## 5. BACKEND API VÀ DATABASE

Kiểm tra API hiện có trước khi triển khai.

Nếu cần, bổ sung endpoint thống kê phù hợp, ví dụ:

- GET `/api/v1/admin/products/statistics`
- GET `/api/v1/products/count`
- Hoặc mở rộng các API danh sách hiện tại để trả về metadata thống kê.

Response cần hỗ trợ:
- totalProducts.
- activeProducts.
- inactiveProducts.
- outOfStockProducts.
- homepageProducts.
- filteredTotal.
- currentPageCount.
- totalPages.

Tên trường có thể điều chỉnh theo quy ước hiện có.

Yêu cầu:
- Backend chịu trách nhiệm tính toán số lượng.
- Database là nguồn dữ liệu gốc.
- Phân quyền API Admin đúng.
- Customer chỉ được truy cập các thông tin thống kê công khai.
- Không trả dữ liệu quản trị hoặc sản phẩm ẩn cho Customer.
- Không tạo truy vấn N+1.
- Tối ưu truy vấn COUNT và điều kiện lọc.
- Không sử dụng dữ liệu giả hoặc số lượng hardcode.

## 6. ĐỒNG BỘ KHI DỮ LIỆU THAY ĐỔI

Khi Admin:
- Thêm sản phẩm.
- Sửa sản phẩm.
- Chuyển ACTIVE/INACTIVE.
- Xóa mềm.
- Sửa danh mục.
- Sửa tồn kho.
- Cập nhật sản phẩm nổi bật.
- Thay đổi điều kiện hiển thị trang chủ.

Các số liệu phải cập nhật theo dữ liệu mới sau khi thao tác thành công.

Kiểm tra cơ chế cache hiện có. Nếu có cache, phải xử lý invalidation/revalidation để tránh trường hợp Admin đã thay đổi sản phẩm nhưng Customer vẫn thấy số lượng cũ.

Không yêu cầu tải lại toàn bộ hệ thống nếu có thể cập nhật dữ liệu theo cơ chế hiện tại.

## 7. YÊU CẦU GIAO DIỆN

Thiết kế theo phong cách Admin Routine hiện tại:
- Gọn gàng.
- Dễ đọc.
- Các thẻ thống kê không quá lớn.
- Màu sắc phân biệt trạng thái hợp lý.
- Responsive.
- Không làm bảng Products bị thu hẹp hoặc tràn màn hình.

Phía Customer:
- Số lượng sản phẩm hiển thị tinh tế.
- Không làm rối giao diện trang chủ.
- Đồng nhất với thiết kế hiện tại.
- Không làm ảnh hưởng đến hình ảnh, bố cục và trải nghiệm mua sắm.

## 8. KIỂM THỬ BẮT BUỘC

Thực hiện kiểm thử trực tiếp:

1. Ghi nhận số sản phẩm ban đầu.
2. Thêm một sản phẩm ACTIVE.
3. Kiểm tra tổng sản phẩm tăng 1.
4. Kiểm tra số sản phẩm đang trưng bày tăng nếu đủ điều kiện.
5. Kiểm tra số lượng trang chủ nếu sản phẩm thuộc khu vực tương ứng.
6. Chuyển sản phẩm sang INACTIVE.
7. Kiểm tra sản phẩm không còn được tính là sản phẩm đang trưng bày.
8. Kiểm tra Customer không nhìn thấy sản phẩm ẩn.
9. Cập nhật tồn kho về 0.
10. Kiểm tra số sản phẩm hết hàng.
11. Khôi phục tồn kho.
12. Kiểm tra số liệu cập nhật.
13. Tìm kiếm và lọc sản phẩm.
14. Kiểm tra tổng kết quả không bị nhầm với số sản phẩm trên trang hiện tại.
15. Kiểm tra phân trang.
16. Đối chiếu số liệu trên giao diện với API và Database.

Tất cả thao tác ghi dữ liệu phải sử dụng Database Demo, không thay đổi Database thật.

## 9. BÀN GIAO

Sau khi hoàn thành, báo cáo:
- Các vị trí đã bổ sung số lượng sản phẩm.
- Công thức và điều kiện đếm.
- API sử dụng.
- Bảng Database liên quan.
- Kết quả kiểm thử.
- Ảnh chụp Admin Products và Customer Storefront sau khi hoàn thiện.

Không chỉ bổ sung giao diện hiển thị con số. Phải hoàn thiện đầy đủ luồng Database → Backend API → Frontend và bảo đảm số liệu chính xác.
