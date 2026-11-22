# PROMPT 030 – PHASE 02 DATABASE INTEGRITY & FOREIGN KEY AUDIT GATEWAY

## 1. ROLE
Principal Database Architect / QA Auditor

## 2. OBJECTIVE
Thực hiện kiểm toán toàn diện tầng cơ sở dữ liệu Phase 02: kiểm tra 29 models, khóa ngoại, ràng buộc unique, hiệu năng index và cấp phê duyệt nghiệm thu Gateway 2.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_09_REAL_DATA_AND_BUSINESS_LOGIC.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_09_REAL_DATA_AND_BUSINESS_LOGIC.md)
> - [USER_MASTER_PROMPT_13_MYSQL_AI_ADDRESS_SHIPPING_SYNC.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_13_MYSQL_AI_ADDRESS_SHIPPING_SYNC.md)
> - [USER_MASTER_PROMPT_12_ROUTINE_VN_CATALOG_SCRAPING.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_12_ROUTINE_VN_CATALOG_SCRAPING.md)

## 3. CONTEXT
Gateway 2 là chốt chặn quan trọng trước khi bắt đầu lập trình Backend Core (Phase 03). Mọi thiếu sót về kiểu dữ liệu (Decimal vs Float), chỉ mục tìm kiếm hoặc khóa ngoại sẽ gây lỗi cascade nghiêm trọng ở các giai đoạn sau nếu không được phát hiện tại đây.

## 4. PREREQUISITES
- PROMPT_019 đến PROMPT_029

## 5. INPUTS
- Toàn bộ schema.prisma và kết quả chạy seed

## 6. DETAILED TASKS
1. **Kiểm toán toàn bộ 29 Prisma Models**:
   Xác minh sự hiện diện và tính chính xác của đủ 29 models: User, Address, Category, Product, ProductVariant, Order, OrderItem, StockReservation, PaymentTransaction, Cart, CartItem, Wishlist, WishlistItem, Outfit, OutfitProduct, Style, AiConversation, AiConversationMessage, Coupon, shipping_rules, StoreSetting, Notification, AiBiReport, AiBiRecommendation, TrafficLog, MediaFile, SizeGuide, Store, ...

2. **Kiểm tra Ràng buộc Khóa Ngoại và Cascade Rules**:
   Xác minh các quan hệ 1-N, N-N, các cờ onDelete (Cascade khi xóa cha hoặc Restrict khi có ràng buộc tài chính).

3. **Kiểm toán Kiểu Dữ Liệu Tài Chính**:
   Đảm bảo tất cả các trường tiền tệ (price, originalPrice, salePrice, subtotal, shippingFee, discountAmount, totalAmount) sử dụng Decimal(12,2).

4. **Lập Báo cáo Nghiệm thu Gateway 2**:
   Tổng hợp checklist nghiệm thu, ghi nhận các chỉ số và ký phê duyệt chuyển giao sang Phase 03.

## 7. TECHNICAL REQUIREMENTS
- Đủ 29 models hợp lệ
- 100% foreign key relationships được xác thực
- Zero syntax error trong schema.prisma

## 8. INTEGRATION REQUIREMENTS
- Là điều kiện tiên quyết bắt buộc để mở khóa Phase 03 (Backend Core Development)

## 9. SAFETY CONSTRAINTS
- ⚠️ **Quality Gate Rule**: Không cho phép tiến hành Phase 03 nếu còn bất kỳ model nào bị thiếu hoặc sai lệch kiểu dữ liệu.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: [ ] AC-1: Schema.prisma chứa đủ 29 models theo đặc tả hệ thống Routine.
[ ] **AC-2**: [ ] AC-2: Lệnh npx prisma validate hoàn thành với mã thoát 0.
[ ] **AC-3**: [ ] AC-3: Dữ liệu seed nạp thành công vào MySQL.
[ ] **AC-4**: [ ] AC-4: Báo cáo kiểm toán Phase 02 được phê duyệt.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Chạy npx prisma validate
2. **Tình huống kiểm thử 2**: Chạy script đếm tổng số bảng và foreign keys trong cơ sở dữ liệu MySQL

## 12. EXPECTED OUTPUT
- `docs/DATABASE_INTEGRITY_REPORT.md`: Báo cáo kiểm toán chất lượng tầng cơ sở dữ liệu

## 13. COMPLETION REPORT
- Ký duyệt Gateway 2: Cấp phép bắt đầu Phase 03 Backend Development
