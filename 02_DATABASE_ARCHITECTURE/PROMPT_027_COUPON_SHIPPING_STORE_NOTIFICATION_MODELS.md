# PROMPT 027 – COUPON, SHIPPINGRULES, STORESETTING & NOTIFICATION MODELS

## 1. ROLE
Database Architect

## 2. OBJECTIVE
Xây dựng mô hình dữ liệu cho Khuyến mãi (Coupon), Quy tắc tính phí ship theo khoảng cách (shipping_rules), Cấu hình hệ thống (StoreSetting) và Thông báo thời gian thực (Notification).


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_09_REAL_DATA_AND_BUSINESS_LOGIC.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_09_REAL_DATA_AND_BUSINESS_LOGIC.md)
> - [USER_MASTER_PROMPT_13_MYSQL_AI_ADDRESS_SHIPPING_SYNC.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_13_MYSQL_AI_ADDRESS_SHIPPING_SYNC.md)
> - [USER_MASTER_PROMPT_12_ROUTINE_VN_CATALOG_SCRAPING.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_12_ROUTINE_VN_CATALOG_SCRAPING.md)

## 3. CONTEXT
Các cấu hình vận hành của Routine gồm mã giảm giá (tiền mặt / %), bảng cước vận chuyển động theo khoảng cách km (shipping_rules), thông số thương hiệu/cửa hàng (StoreSetting), và danh sách thông báo quản trị (Notification: đơn hàng mới, lead AI cần tiếp quản).

## 4. PREREQUISITES
- PROMPT_022: Order Model

## 5. INPUTS
- Quy định phí vận chuyển, chính sách voucher Routine

## 6. DETAILED TASKS
1. **Định nghĩa Model Coupon**:
   Bao gồm id, code (String @unique), discountType (PERCENT, FIXED), discountValue (Decimal), minOrderValue (Decimal @default(0)), maxDiscount (Decimal?), usageLimit (Int?), usedCount (Int @default(0)), startDate (DateTime), endDate (DateTime), isActive (Boolean @default(true)), createdAt, updatedAt.

2. **Định nghĩa Model shipping_rules**:
   Bao gồm id, name (String), minDistance (Float), maxDistance (Float), baseFee (Decimal), perKmFee (Decimal @default(0)), estimatedDays (String), isActive (Boolean @default(true)), createdAt, updatedAt.

3. **Định nghĩa Model StoreSetting và Notification**:
   StoreSetting: id, key (String @unique), value (Text), description (String?), updatedAt. Notification: id, type (ORDER, AI_LEAD, SYSTEM), title (String), message (Text), referenceId (String?), isRead (Boolean @default(false)), createdAt.

## 7. TECHNICAL REQUIREMENTS
- Coupon code lưu chữ hoa, @unique
- Bảng shipping_rules ánh xạ chính xác tên bảng trong MySQL @@map("shipping_rules")
- Index trên Notification (isRead, createdAt, type)

## 8. INTEGRATION REQUIREMENTS
- Checkout Service đọc shipping_rules và Coupon; Admin Notification Desk đọc Notification

## 9. SAFETY CONSTRAINTS
- ⚠️ **Coupon Race Condition**: Trường usedCount phải tăng nguyên tử trong transaction để không vượt quá usageLimit.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Models Coupon, shipping_rules, StoreSetting, Notification được thêm vào schema.prisma.
[ ] **AC-2**: npx prisma validate kiểm tra thành công không có lỗi cấu trúc.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Chạy npx prisma validate xác nhận cấu trúc bảng bổ trợ

## 12. EXPECTED OUTPUT
- `backend/prisma/schema.prisma`: Thêm Coupon, shipping_rules, StoreSetting, Notification models

## 13. COMPLETION REPORT
- Hoàn tất các mô hình hỗ trợ thương mại điện tử và thông báo
