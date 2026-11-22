# USER MASTER PROMPT #14: 14 SHIPPING FEE INVOICE INTEGRATION
> **Nguồn gốc:** Prompt chỉ đạo thực tế từ Người dùng (User Request) tại Step 3817.
> **Độ dài gốc:** 3555 ký tự.
> **Mục đích trong thư viện:** Cung cấp toàn văn đặc tả nghiệp vụ, yêu cầu kỹ thuật và ràng buộc sản xuất thực tế mà người dùng đã trực tiếp chỉ đạo và kiểm chứng trong dự án Routine Web.

---

## PHẦN BỔ SUNG: TÍNH PHÍ SHIP VÀO HÓA ĐƠN THANH TOÁN

### 1. Hiển thị chi tiết hóa đơn tại Checkout

Sau khi AI hỗ trợ xác thực địa chỉ và Backend tính phí vận chuyển, website phải hiển thị hóa đơn chi tiết cho khách hàng trước khi xác nhận đặt hàng.

Các khoản cần hiển thị:

- Tổng tiền sản phẩm.
- Giảm giá sản phẩm (nếu có).
- Mã giảm giá (nếu có).
- Phí vận chuyển.
- Tổng thanh toán cuối cùng.

Công thức bắt buộc:

**Tổng thanh toán = Tổng tiền sản phẩm - Tổng giảm giá + Phí vận chuyển.**

Ví dụ minh họa:

| Nội dung | Số tiền |
|---|---:|
| Tổng tiền sản phẩm | 898.000đ |
| Giảm giá | -50.000đ |
| Phí vận chuyển | +30.000đ |
| **Tổng thanh toán** | **878.000đ** |

Đây là dữ liệu minh họa, không phải bảng phí chính thức.

### 2. Đồng bộ phí ship với thanh toán

Backend phải là nơi tính toán và xác nhận số tiền cuối cùng.

Khi khách hàng nhấn thanh toán:

1. Backend lấy lại giá sản phẩm từ MySQL.
2. Kiểm tra số lượng và tồn kho.
3. Tính lại tổng tiền hàng.
4. Kiểm tra mã giảm giá.
5. Xác thực địa chỉ giao hàng.
6. Tính lại phí vận chuyển.
7. Cộng phí ship vào tổng thanh toán.
8. Tạo đơn hàng với số tiền chính xác.
9. Truyền đúng tổng thanh toán sang cổng thanh toán VNPay Sandbox hiện có.

Không sử dụng tổng tiền do Frontend hoặc AI tự gửi lên làm căn cứ thanh toán.

### 3. Đồng bộ với VNPay Sandbox

Đảm bảo số tiền gửi sang VNPay là:

**Số tiền thanh toán VNPay = Tổng tiền sản phẩm - Giảm giá + Phí vận chuyển.**

Kiểm tra:
- Số tiền trên trang Checkout.
- Số tiền trong bản ghi đơn hàng MySQL.
- Số tiền trên URL/giao dịch VNPay Sandbox.
- Số tiền trong kết quả callback sau thanh toán.

Bốn giá trị phải khớp nhau.

Không chỉ tạo được URL thanh toán là coi như hoàn thành. Phải kiểm thử cả callback, chữ ký và trạng thái thanh toán.

### 4. Lưu hóa đơn trong MySQL

Đảm bảo đơn hàng lưu được:

- subtotal: Tổng tiền sản phẩm.
- discount_amount: Tổng giảm giá.
- shipping_fee: Phí vận chuyển.
- total_amount: Tổng thanh toán cuối cùng.
- shipping_address: Địa chỉ giao hàng.
- shipping_zone: Khu vực giao hàng.
- shipping_fee_rule_version: Phiên bản bảng phí được áp dụng.

Phải lưu phí vận chuyển tại thời điểm đặt hàng để khi Admin thay đổi bảng phí, hóa đơn cũ không bị thay đổi.

### 5. Đồng bộ hóa đơn ở các giao diện

**Khách hàng:**
- Xem hóa đơn trước thanh toán.
- Xem tổng tiền đã bao gồm phí ship.
- Xem chi tiết phí ship trong lịch sử đơn hàng.
- Xem lại hóa đơn sau khi đặt hàng.

**Admin:**
- Xem tổng tiền hàng.
- Xem giảm giá.
- Xem phí vận chuyển.
- Xem tổng thanh toán.
- Xem địa chỉ giao hàng.
- Không được làm thay đổi hóa đơn cũ khi cập nhật bảng phí.

**AI:**
- Có thể giải thích cách tính phí ship.
- Có thể thông báo tổng thanh toán đã được Backend xác nhận.
- Không tự thay đổi giá trị hóa đơn.
- Không tự xác nhận thanh toán thành công.

### 6. Kiểm thử bắt buộc

Thực hiện ít nhất các trường hợp:

1. Đơn hàng không có mã giảm giá.
2. Đơn hàng có mã giảm giá.
3. Đơn hàng có phí ship khác nhau theo khu vực.
4. Khách thay đổi địa chỉ trước thanh toán.
5. Khách thay đổi sản phẩm hoặc số lượng.
6. Thanh toán qua VNPay Sandbox.
7. VNPay trả về thanh toán thành công.
8. VNPay trả về thanh toán thất bại hoặc khách hủy.
9. Khách xem lại hóa đơn trong lịch sử đơn hàng.

Đối chiếu số tiền giữa Checkout, Backend, MySQL và VNPay Sandbox.

**Tiêu chí nghiệm thu:** Không có trường hợp nào phí ship bị bỏ sót, bị cộng hai lần hoặc không được tính vào tổng thanh toán cuối cùng.
