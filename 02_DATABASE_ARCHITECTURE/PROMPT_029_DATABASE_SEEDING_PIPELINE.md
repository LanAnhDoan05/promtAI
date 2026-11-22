# PROMPT 029 – PRODUCTION DATABASE SEEDING PIPELINE (STANDARD CATALOG & STORE DATA)

## 1. ROLE
Data Engineer / Database Developer

## 2. OBJECTIVE
Xây dựng kịch bản nạp dữ liệu khởi tạo (Database Seeding) tự động và có thứ tự phụ thuộc, bao gồm Admin account, danh mục, sản phẩm thời trang mẫu, biến thể SKU, quy tắc vận chuyển và voucher chào mừng.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_09_REAL_DATA_AND_BUSINESS_LOGIC.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_09_REAL_DATA_AND_BUSINESS_LOGIC.md)
> - [USER_MASTER_PROMPT_13_MYSQL_AI_ADDRESS_SHIPPING_SYNC.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_13_MYSQL_AI_ADDRESS_SHIPPING_SYNC.md)
> - [USER_MASTER_PROMPT_12_ROUTINE_VN_CATALOG_SCRAPING.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_12_ROUTINE_VN_CATALOG_SCRAPING.md)

## 3. CONTEXT
Một hệ thống Routine từ con số 0 cần dữ liệu danh mục chuẩn (Nam, Nữ, Phụ kiện), sản phẩm áo quần thực tế, hình ảnh hợp lệ, tài khoản admin mặc định, và bảng phí ship để hệ thống có thể chạy thử ngay sau khi cài đặt.

## 4. PREREQUISITES
- PROMPT_028: Hoàn tất toàn bộ 29 models trong schema.prisma

## 5. INPUTS
- Danh mục sản phẩm Routine, thông tin tài khoản Admin, biểu phí ship

## 6. DETAILED TASKS
1. **Tạo file backend/prisma/seed.js**:
   Xây dựng script seed sử dụng PrismaClient với cơ chế idempotent (upsert) để có thể chạy nhiều lần mà không bị lỗi duplicate key.

2. **Tạo tài khoản Quản trị viên và Khách hàng mẫu**:
   Tạo tài khoản Admin (admin@routine.vn / mật khẩu bcrypt) và 1 tài khoản Customer mẫu có địa chỉ đầy đủ tọa độ.

3. **Tạo Danh mục thời trang và Sản phẩm mẫu**:
   Nạp danh mục Áo (Sơ mi, Thun, Khoác), Quần (Jeans, Kaki, Tây), Váy, Phụ kiện. Nạp các sản phẩm kèm biến thể màu sắc (Đen, Trắng, Be, Xanh) và kích thước (S, M, L, XL), gán SKU duy nhất.

4. **Nạp Quy tắc vận chuyển và Voucher**:
   Nạp 4 nấc khoảng cách trong shipping_rules (Nội thành < 5km: 15.000đ, 5-15km: 25.000đ, 15-30km: 35.000đ, Liên tỉnh > 30km: 45.000đ). Nạp voucher chào mừng WELCOME10.

5. **Cấu hình package.json scripts**:
   Thêm "prisma": { "seed": "node prisma/seed.js" } vào backend/package.json.

## 7. TECHNICAL REQUIREMENTS
- Sử dụng upsert hoặc kiểm tra count trước khi insert
- Mật khẩu mẫu phải được hash bằng bcryptjs
- Tọa độ cửa hàng mẫu Routine (ví dụ: Hà Nội hoặc TP.HCM) để phục vụ tính khoảng cách

## 8. INTEGRATION REQUIREMENTS
- Chạy được trực tiếp qua lệnh npx prisma db seed

## 9. SAFETY CONSTRAINTS
- ⚠️ **Data Loss Prevention**: Script seed không được drop table hoặc xóa dữ liệu trừ khi được chỉ định cờ --force.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: File backend/prisma/seed.js được viết hoàn chỉnh.
[ ] **AC-2**: Chạy npx prisma db seed hoàn thành trong thời gian < 10 giây không có lỗi.
[ ] **AC-3**: Kiểm tra database có đủ admin user, categories, products, variants, shipping_rules, coupons.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Chạy npx prisma db seed và kiểm tra số lượng bản ghi trả về qua SQL query

## 12. EXPECTED OUTPUT
- `backend/prisma/seed.js`: Kịch bản nạp dữ liệu mẫu Routine

## 13. COMPLETION REPORT
- Database đã được nạp đầy đủ dữ liệu mẫu chuẩn hóa để sẵn sàng phát triển API
