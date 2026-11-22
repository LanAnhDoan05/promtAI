# PROMPT 040 – DYNAMIC SHIPPING FEE CALCULATION & COORDINATE DISTANCE SERVICE

## 1. ROLE
Backend Geolocation & Logistics Engineer

## 2. OBJECTIVE
Xây dựng thuật toán tính khoảng cách địa lý (Haversine Formula) giữa kho hàng trung tâm của Routine và địa chỉ giao hàng của khách để tính phí vận chuyển động dựa trên bảng shipping_rules.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_02_CLOUDINARY_ADMIN_PRODUCT_MANAGEMENT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_02_CLOUDINARY_ADMIN_PRODUCT_MANAGEMENT.md)
> - [USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md)
> - [USER_MASTER_PROMPT_25_PRODUCTION_UPGRADE_NOTIFICATION_HANDOFF.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_25_PRODUCTION_UPGRADE_NOTIFICATION_HANDOFF.md)
> - ⭐ **Tài liệu tham chiếu trực tiếp:** [USER_MASTER_PROMPT_13_MYSQL_AI_ADDRESS_SHIPPING_SYNC.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_13_MYSQL_AI_ADDRESS_SHIPPING_SYNC.md)

## 3. CONTEXT
Routine áp dụng chính sách tính phí vận chuyển thông minh theo khoảng cách thực tế (km) tính từ kho tổng đến tọa độ (latitude, longitude) địa chỉ nhận hàng của khách. Nếu không có tọa độ chính xác, hệ thống tính theo tỉnh/thành phố quy chuẩn.

## 4. PREREQUISITES
- PROMPT_027: shipping_rules Model
- PROMPT_020: Address Model

## 5. INPUTS
- Tọa độ kho Routine gốc (STORE_LAT, STORE_LNG)
- Tọa độ hoặc Tỉnh/Thành của khách hàng

## 6. DETAILED TASKS
1. **Xây dựng hàm tính khoảng cách Haversine**:
   Tạo utils/geoDistance.js tính khoảng cách đường chim bay giữa hai cặp tọa độ (lat1, lon1) và (lat2, lon2) theo đơn vị km, có hệ số hiệu chỉnh cung đường thực tế (nhân hệ số 1.25).

2. **Xây dựng ShippingService.calculateFee**:
   Truy vấn bảng shipping_rules đang active. So khớp khoảng cách km vào dải [minDistance, maxDistance] để lấy cước cơ bản (baseFee) và cước phụ thu mỗi km (perKmFee).

3. **Hỗ trợ tính theo Tỉnh/Thành phố fallback**:
   Nếu địa chỉ chưa có tọa độ, tra cứu khoảng cách ước lượng theo bảng tọa độ trung tâm 63 tỉnh thành Việt Nam.

4. **Tạo Endpoint POST /api/v1/shipping/calculate**:
   Nhận { addressId, province, latitude, longitude } và trả về { distanceKm, shippingFee, estimatedDays, ruleName }.


### CÔNG THỨC HAVERSINE TÍNH KHOẢNG CÁCH VẬN CHUYỂN (Theo USER_MASTER_PROMPT_13):
- Kho tổng Routine đặt tại Hà Nội hoặc TP.HCM với tọa độ gốc (STORE_LAT, STORE_LNG).
- Công thức Haversine:
  ```javascript
  function calculateDistanceKm(lat1, lon1, lat2, lon2) {
    const R = 6371; // Ban kinh Trai Dat (km)
    const dLat = (lat2 - lat1) * Math.PI / 180;
    const dLon = (lon2 - lon1) * Math.PI / 180;
    const a = Math.sin(dLat/2) * Math.sin(dLat/2) +
              Math.cos(lat1 * Math.PI / 180) * Math.cos(lat2 * Math.PI / 180) *
              Math.sin(dLon/2) * Math.sin(dLon/2);
    const c = 2 * Math.atan2(Math.sqrt(a), Math.sqrt(1-a));
    return parseFloat((R * c * 1.25).toFixed(1)); // 1.25 la he so duong bo thuc te
  }
  ```
- Tra cứu bảng `shipping_rules` để xác định mức cước: Nội thành (< 5km), Cận nội thành (5-15km), Ngoại thành (15-30km), Liên tỉnh (> 30km).


## 7. TECHNICAL REQUIREMENTS
- Haversine formula chính xác với bán kính Trái Đất R = 6371 km
- Lấy quy tắc cước từ MySQL bảng shipping_rules
- Fallback an toàn nếu thiếu tọa độ

## 8. INTEGRATION REQUIREMENTS
- Frontend Checkout Step 1 và Order Service gọi để lấy phí ship

## 9. SAFETY CONSTRAINTS
- ⚠️ **Invalid Coordinates**: Kiểm tra tọa độ hợp lệ (-90 <= lat <= 90, -180 <= lng <= 180).

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Địa chỉ nội thành cách kho 3km trả về đúng mức cước nội thành (15.000đ).
[ ] **AC-2**: Địa chỉ liên tỉnh cách kho 100km trả về đúng mức cước liên tỉnh.
[ ] **AC-3**: Trả về đầy đủ số ngày giao hàng ước tính (estimatedDays).

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm thử tính phí với tọa độ nội thành Hà Nội
2. **Tình huống kiểm thử 2**: Kiểm thử tính phí với tỉnh xa (Cà Mau, Đà Nẵng)

## 12. EXPECTED OUTPUT
- `backend/src/utils/geoDistance.js`: Công thức tính khoảng cách địa lý
- `backend/src/services/shippingService.js`: Dịch vụ tính phí vận chuyển động
- `backend/src/controllers/shippingController.js`: Controller vận chuyển

## 13. COMPLETION REPORT
- Hệ thống tính cước vận chuyển động theo khoảng cách đã hoàn thành
