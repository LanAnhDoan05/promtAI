# PROMPT 108 – EMBEDDED DYNAMIC VNPAY QR CODE ON CHECKOUT PAGE

## 1. ROLE
Senior Payment & Frontend Engineer

## 2. OBJECTIVE
Xây dựng cơ chế hiển thị mã QR thanh toán động nhúng trực tiếp ngay trên trang Checkout (Embedded VNPay QR): Khách hàng không cần rời khỏi website Routine, mã QR động được sinh từ URL thanh toán chuẩn VNPay, đồng hồ đếm ngược 15 phút, và cơ chế tự động thăm dò (polling hoặc SSE) kiểm tra trạng thái thanh toán thành công để chuyển trang tức thì.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_18_VNPAY_QR_AND_AI_HUMAN_HANDOFF.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_18_VNPAY_QR_AND_AI_HUMAN_HANDOFF.md)
> - [USER_MASTER_PROMPT_26_EMBEDDED_VNPAY_DYNAMIC_QR.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_26_EMBEDDED_VNPAY_DYNAMIC_QR.md)
> - ⭐ **Tài liệu tham chiếu trực tiếp:** [USER_MASTER_PROMPT_26_EMBEDDED_VNPAY_DYNAMIC_QR.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_26_EMBEDDED_VNPAY_DYNAMIC_QR.md)

## 3. CONTEXT
Trải nghiệm thanh toán nhúng QR trực tiếp giúp khách hàng chỉ cần mở app ngân hàng (Vietcombank, MB, Techcombank...) quét mã ngay trên màn hình máy tính mà không bị chuyển hướng sang trang ngoài, tối ưu tỷ lệ chuyển đổi đơn hàng.

## 4. PREREQUISITES
- PROMPT_107: Dynamic VNPay URL
- PROMPT_074: Order Submission

## 5. INPUTS
- Payment URL từ API và mã đơn hàng orderCode

## 6. DETAILED TASKS
1. **Tạo Mã QR Động Phía Frontend (sử dụng qrcode)**:
   Cài đặt thư viện qrcode (^1.5.4). Khi nhận được paymentUrl từ backend, chuyển đổi thành DataURL hình ảnh QR hiển thị trên thẻ <canvas> hoặc <img>.

2. **Thiết Kế Khung Embedded VNPay QR Sang Trọng**:
   Khung viền Routine tinh tế: Logo VNPAY-QR chính thức, mã QR ở giữa, dòng chữ "Quét mã bằng ứng dụng Ngân hàng hoặc Ví VNPAY", thông tin số tiền cần thanh toán và mã đơn hàng.

3. **Đồng Hồ Đếm Ngược 15 Phút (Countdown Timer)**:
   Hiển thị thời gian hiệu lực còn lại: 14:59, 14:58... Khi hết giờ, làm mờ mã QR và hiển thị nút "Tạo lại mã QR mới".

4. **Cơ Chế Tự Động Nhận Diện Thanh Toán Thành Công (Auto-detect)**:
   Frontend kích hoạt thăm dò nhẹ (polling mỗi 3 giây gọi GET /api/v1/payment/check-status/:orderCode) hoặc lắng nghe sự kiện SSE. Khi phát hiện đơn hàng đã chuyển sang PAID, tự động hiển thị hiệu ứng thành công và chuyển sang /order-success.


### PHÂN BIỆT RÕ RÀNG VNPAY-QR VÀ VIETQR (Theo chỉ thị từ USER_MASTER_PROMPT_26):
1. **VietQR (Chuyển khoản thường):**
   - Được tạo bằng thư viện qrcode dựa trên định dạng NAPAS (số tài khoản ngân hàng, mã ngân hàng, nội dung chuyển khoản).
   - KHÔNG liên kết phiên thanh toán với VNPay Gateway.
   - Không có Webhook IPN tự động xác nhận từ ngân hàng về cổng.
2. **VNPAY-QR (Cổng thanh toán chính thức):**
   - Phải được tạo từ URL thanh toán có chữ ký số HMAC-SHA512 do backend sinh qua cổng VNPay.
   - Có mã giao dịch tương ứng (vnp_TxnRef) và được VNPay quản lý vòng đời.
   - Có cơ chế xác nhận thanh toán tự động qua Webhook IPN và Return URL.
   - TUYỆT ĐỐI KHÔNG dùng ảnh QR tĩnh, không tự ghép chuỗi QR tùy ý giả làm VNPAY.


## 7. TECHNICAL REQUIREMENTS
- Thư viện qrcode ^1.5.4
- Tuyệt đối không dùng ảnh QR tĩnh hoặc VietQR tự tạo không có liên kết giao dịch cổng

## 8. INTEGRATION REQUIREMENTS
- Tích hợp trực tiếp vào component Checkout Payment Result

## 9. SAFETY CONSTRAINTS
- ⚠️ **Fake QR Defense**: Đảm bảo QR sinh từ paymentUrl chính thống có mã giao dịch duy nhất của VNPay.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Mã QR hiển thị rõ nét ngay tại trang checkout sau khi bấm đặt hàng qua VNPay.
[ ] **AC-2**: Đồng hồ đếm ngược chạy chính xác từng giây.
[ ] **AC-3**: Quét thanh toán thành công trên app ngân hàng thì website tự động chuyển trang sau 1-2 giây.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm thử hiển thị mã QR và mô phỏng giao dịch thành công để kiểm tra tự động chuyển trang

### CODE MINH HỌA TRIỂN KHAI CHUẨN HÓA:

```javascript
// frontend/src/components/Checkout/EmbeddedVnpayQr.jsx
import React, { useState, useEffect } from 'react';
import QRCode from 'qrcode';

export default function EmbeddedVnpayQr({ paymentUrl, orderCode, amount, onPaymentSuccess }) {
  const [qrSrc, setQrSrc] = useState('');
  const [timeLeft, setTimeLeft] = useState(900); // 15 phut = 900s
  const [isExpired, setIsExpired] = useState(false);

  useEffect(() => {
    if (paymentUrl) {
      QRCode.toDataURL(paymentUrl, {
        width: 280,
        margin: 2,
        color: { dark: '#000000', light: '#ffffff' }
      }).then(url => setQrSrc(url));
    }
  }, [paymentUrl]);

  // Countdown timer
  useEffect(() => {
    if (timeLeft <= 0) {
      setIsExpired(true);
      return;
    }
    const timer = setInterval(() => setTimeLeft(prev => prev - 1), 1000);
    return () => clearInterval(timer);
  }, [timeLeft]);

  // Polling check status
  useEffect(() => {
    if (isExpired || !orderCode) return;
    const pollInterval = setInterval(async () => {
      try {
        const res = await fetch(`/api/v1/payment/check-status/${orderCode}`);
        const data = await res.json();
        if (data.success && data.paymentStatus === 'PAID') {
          clearInterval(pollInterval);
          onPaymentSuccess(data);
        }
      } catch (err) {
        console.error('Polling error:', err);
      }
    }, 3000);

    return () => clearInterval(pollInterval);
  }, [orderCode, isExpired, onPaymentSuccess]);

  const formatTime = (secs) => {
    const m = Math.floor(secs / 60);
    const s = secs % 60;
    return `${m}:${s < 10 ? '0' : ''}${s}`;
  };

  return (
    <div className="vnpay-qr-container border p-4 text-center rounded bg-white shadow-sm">
      <div className="vnpay-badge mb-3">
        <span className="font-bold text-red-600 text-lg">VNPAY-QR</span>
      </div>
      {qrSrc && !isExpired ? (
        <div className="qr-wrapper flex justify-center mb-3">
          <img src={qrSrc} alt="VNPay Dynamic QR" className="w-64 h-64 border rounded" />
        </div>
      ) : isExpired ? (
        <div className="expired-notice p-6 bg-gray-100 rounded text-red-500 font-semibold mb-3">
          Mã QR đã hết hạn (15 phút). Vui lòng tạo lại mã mới.
        </div>
      ) : (
        <div className="loading p-6">Đang khởi tạo mã QR thanh toán an toàn...</div>
      )}
      <div className="timer text-sm text-gray-600 mb-2">
        Thời gian hiệu lực còn lại: <strong className="text-red-500">{formatTime(timeLeft)}</strong>
      </div>
      <div className="order-info text-xs text-gray-500 border-t pt-2">
        Mã đơn hàng: <span className="font-mono font-semibold">{orderCode}</span> | Số tiền: <span className="font-semibold text-black">{new Intl.NumberFormat('vi-VN', { style: 'currency', currency: 'VND' }).format(amount)}</span>
      </div>
    </div>
  );
}
```


## 12. EXPECTED OUTPUT
- `frontend/src/components/Checkout/EmbeddedVnpayQr.jsx`: Component nhúng mã QR thanh toán động

## 13. COMPLETION REPORT
- Tính năng nhúng mã QR thanh toán VNPay động tại checkout hoàn thành
