# USER MASTER PROMPT #26: 26 EMBEDDED VNPAY DYNAMIC QR
> **Nguồn gốc:** Prompt chỉ đạo thực tế từ Người dùng (User Request) tại Step 10811.
> **Độ dài gốc:** 6244 ký tự.
> **Mục đích trong thư viện:** Cung cấp toàn văn đặc tả nghiệp vụ, yêu cầu kỹ thuật và ràng buộc sản xuất thực tế mà người dùng đã trực tiếp chỉ đạo và kiểm chứng trong dự án Routine Web.

---

# ROUTINE WEB – TASK PAYMENT 02
# EMBEDDED VNPAY QR – DYNAMIC ORDER PAYMENT

Bạn là Senior Payment Integration Engineer, chịu trách nhiệm nâng cấp hệ thống thanh toán Routine Web.

MỤC TIÊU:
Khách hàng có thể nhìn thấy mã QR thanh toán VNPAY ngay trên website Routine, không phải rời khỏi giao diện checkout.

## A. KIỂM TRA KIẾN TRÚC HIỆN TẠI

Sử dụng codebase hiện tại, không tạo dự án mới.

Công nghệ:
- Next.js 16.4.3.
- React 19.2.3.
- Express 4.22.3.
- Prisma 6.19.3.
- MySQL 8.0.
- VNPAY SDK 2.5.0.
- qrcode ^1.5.4.

Các thành phần cần kiểm tra:
- backend/src/services/vnpayService.js
- backend/src/controllers/paymentController.js
- backend/src/routes/api.js
- backend/prisma/schema.prisma
- Frontend Checkout.
- Frontend Payment Result.
- Các component QR hiện có.

API hiện tại:
- POST /api/v1/payment/create-payment-url
- GET /api/v1/payment/vnpay-return
- GET /api/v1/payment/vnpay-ipn
- POST /api/v1/payment/simulate

Không tự ý đổi tên hoặc xóa API đang được sử dụng.

## B. PHÂN BIỆT VNPAY QR VÀ VIETQR

Kiểm tra chính xác hai cơ chế:

1. VietQR:
- Được tạo bằng thư viện qrcode hiện tại.
- Có thể chứa số tiền và nội dung chuyển khoản.
- Không đồng nghĩa với giao dịch VNPAY Gateway.

2. VNPAY-QR:
- Phải được tạo thông qua phương thức tích hợp được VNPAY cấp quyền.
- Có mã giao dịch tương ứng.
- Có cơ chế xác nhận thanh toán từ VNPAY.

TUYỆT ĐỐI:
- Không dùng QR VietQR để giả làm VNPAY.
- Không dùng ảnh QR tĩnh.
- Không tự ghép chuỗi QR tùy ý.
- Không tự tạo QR từ payment URL nếu chưa xác minh đó là phương thức được VNPAY hỗ trợ.
- Không sử dụng API không chính thức.

## C. KIỂM TRA KHẢ NĂNG HIỂN THỊ QR TRỰC TIẾP

Đối chiếu tài liệu tích hợp VNPAY hiện tại và cấu hình Merchant.

Xác minh:
1. Merchant có được cấp quyền tạo VNPAY QR động qua API hay không.
2. Có endpoint tạo QR riêng hay không.
3. API có trả về QR string, QR image hoặc QR payload hay không.
4. Có mã giao dịch và thời hạn QR hay không.
5. Có API truy vấn trạng thái giao dịch hay không.
6. Có IPN/Webhook để xác nhận giao dịch hay không.
7. Có cho phép hiển thị QR trong website Merchant hay không.

Nếu chưa có tài liệu hoặc Merchant Credentials phù hợp, ghi rõ phần nào chưa xác minh được.

Không tự suy đoán endpoint hoặc response của VNPAY.

## D. TRIỂN KHAI VNPAY EMBEDDED QR

Chỉ triển khai sau khi xác minh được phương thức tích hợp chính thức.

Luồng:

1. Customer tạo đơn hàng.
2. Backend tính tổng thanh toán từ dữ liệu database.
3. Backend tạo Payment Transaction.
4. Backend yêu cầu VNPAY tạo QR động.
5. Backend nhận dữ liệu QR.
6. Frontend hiển thị QR ngay trong trang Routine.
7. Khách quét QR bằng ứng dụng ngân hàng hoặc ví được hỗ trợ.
8. VNPAY xác nhận giao dịch.
9. Backend xác minh chữ ký và số tiền.
10. Database cập nhật trạng thái PAID.
11. Frontend nhận trạng thái thành công.

Mỗi QR phải liên kết với đúng:
- orderId.
- transactionId.
- totalAmount.
- currency.
- paymentMethod.
- expirationTime.

## E. GIAO DIỆN THANH TOÁN ROUTINE

Thiết kế trang thanh toán chuyên nghiệp, tối giản.

Bố cục:

Bên trái:
- Mã QR thanh toán.
- Hướng dẫn quét mã.
- Danh sách phương thức thanh toán được hỗ trợ.

Bên phải:
- Mã đơn hàng.
- Tổng tiền sản phẩm.
- Phí vận chuyển.
- Giảm giá.
- Tổng tiền phải thanh toán.

Bên dưới:
- Trạng thái đang chờ thanh toán.
- Thời gian còn lại nếu giao dịch có thời hạn.
- Nút kiểm tra trạng thái.
- Nút hủy giao dịch nếu được hỗ trợ.

Trạng thái:
- Đang tạo giao dịch.
- Đang chờ thanh toán.
- Thanh toán thành công.
- Thanh toán thất bại.
- Giao dịch hết hạn.
- Giao dịch bị hủy.

Không tự chuyển sang thành công khi khách chỉ nhấn nút xác nhận hoặc quay lại website.

## F. XỬ LÝ BACKEND VÀ DATABASE

- Sử dụng transaction hiện có nếu phù hợp.
- Không tạo giao dịch trùng.
- Không cập nhật đơn hàng sai số tiền.
- Không cho phép thay đổi số tiền sau khi tạo giao dịch.
- Không cho phép thanh toán lại đơn hàng đã PAID.
- Có idempotency khi nhận IPN nhiều lần.
- Kiểm tra chữ ký từ VNPAY.
- Kiểm tra mã đơn hàng và mã giao dịch.
- Kiểm tra số tiền chính xác.
- Lưu đầy đủ lịch sử giao dịch.

Nếu cần thay đổi Prisma Schema, phải tạo migration an toàn, không reset database và không xóa lịch sử giao dịch.

## G. REALTIME PAYMENT STATUS

Tận dụng SSE hiện tại nếu phù hợp.

Khi VNPAY xác nhận thành công:
- Backend cập nhật Database.
- Phát sự kiện PAYMENT_UPDATED.
- Frontend tự động cập nhật giao diện.
- Hiển thị thanh toán thành công.
- Điều hướng đến trang xác nhận đơn hàng khi phù hợp.

Nếu SSE mất kết nối, Frontend phải có cơ chế truy vấn trạng thái thanh toán từ Backend.

Không để trạng thái thanh toán chỉ phụ thuộc vào Frontend.

## H. PHƯƠNG ÁN DỰ PHÒNG

Nếu Merchant hiện tại chưa được cấp API tạo QR trực tiếp:

- Không tự chế QR VNPAY.
- Không sử dụng QR VietQR thay thế nhưng ghi nhãn VNPAY.
- Giữ nguyên chức năng tạo payment URL hiện tại.
- Kiểm tra khả năng chuyển khách sang trang VNPAY với phương thức VNPAYQR.
- Thiết kế giao diện thông báo chuyển sang cổng thanh toán phù hợp.
- Chuẩn bị kiến trúc để tích hợp QR trực tiếp sau khi được VNPAY cấp quyền.

Không sử dụng iframe nếu chưa được VNPAY xác nhận hỗ trợ và cho phép nhúng.

## I. KIỂM THỬ

Sandbox:
1. Đơn hàng 100.000 VNĐ.
2. Đơn hàng 500.000 VNĐ.
3. Đơn hàng 1.130.000 VNĐ.
4. Kiểm tra đúng số tiền QR.
5. Thanh toán thành công.
6. Thanh toán thất bại.
7. Hết hạn giao dịch.
8. Quét QR hai lần.
9. Callback trùng.
10. Giả mạo số tiền.
11. Giả mạo chữ ký.
12. Refresh trang thanh toán.
13. Mất SSE và kết nối lại.

Chỉ đánh dấu PASS khi có bằng chứng thực tế.

## J. BÁO CÁO

Báo cáo riêng:
1. Cơ chế QR hiện tại của Routine.
2. Khả năng hỗ trợ Embedded VNPAY QR.
3. Tài liệu VNPAY đã đối chiếu.
4. Các API cần sử dụng.
5. File đã sửa.
6. Database đã thay đổi.
7. Test case.
8. Các điều kiện còn thiếu từ phía VNPAY.
9. Trạng thái sẵn sàng Production.

ƯU TIÊN:
Bảo đảm giao dịch đúng, tiền đúng, bảo mật đúng trước khi tối ưu giao diện.

Không triển khai giao dịch tiền thật. Chỉ sử dụng Sandbox trong giai đoạn này.
