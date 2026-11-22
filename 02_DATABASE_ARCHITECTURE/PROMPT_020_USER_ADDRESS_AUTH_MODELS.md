# PROMPT 020 – USER, ADDRESS & AUTHENTICATION DATABASE MODELS

## 1. ROLE
Database Architect

## 2. OBJECTIVE
Thiết kế và định nghĩa các Prisma Model cho User, Address, và các trường xác thực tài khoản, phân quyền (Role) với quan hệ 1-N chuẩn hóa.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_09_REAL_DATA_AND_BUSINESS_LOGIC.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_09_REAL_DATA_AND_BUSINESS_LOGIC.md)
> - [USER_MASTER_PROMPT_13_MYSQL_AI_ADDRESS_SHIPPING_SYNC.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_13_MYSQL_AI_ADDRESS_SHIPPING_SYNC.md)
> - [USER_MASTER_PROMPT_12_ROUTINE_VN_CATALOG_SCRAPING.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_12_ROUTINE_VN_CATALOG_SCRAPING.md)

## 3. CONTEXT
Khách hàng và Quản trị viên trong hệ thống Routine cần tài khoản để đăng nhập, quản lý sổ địa chỉ giao hàng và phân quyền truy cập. Mô hình User chứa thông tin cá nhân, phân quyền (CUSTOMER, ADMIN, STAFF), và liên kết với Address.

## 4. PREREQUISITES
- PROMPT_019: Prisma ORM Initialization & MySQL Connection

## 5. INPUTS
- Danh sách trường dữ liệu User, Address, Role từ tài liệu đặc tả Data Dictionary

## 6. DETAILED TASKS
1. **Định nghĩa Model User trong schema.prisma**:
   Thêm model User với id (Int, @id, @default(autoincrement)), email (@unique), password (String), fullName (String), phone (String?), role (String @default("CUSTOMER")), avatar (String?), status (String @default("ACTIVE")), createdAt, updatedAt.

2. **Định nghĩa Model Address trong schema.prisma**:
   Thêm model Address với id, userId (Int), receiverName, phone, addressLine, province, district, ward, latitude (Float?), longitude (Float?), isDefault (Boolean @default(false)), quan hệ user User @relation(fields: [userId], references: [id], onDelete: Cascade).

3. **Đánh chỉ mục Index cho hiệu năng tìm kiếm**:
   Tạo index trên email, phone, role cho bảng users; tạo index trên userId cho bảng addresses.

## 7. TECHNICAL REQUIREMENTS
- Quan hệ 1-N giữa User và Address với onDelete: Cascade
- Email phải unique và được index
- Mặc định role là CUSTOMER, status là ACTIVE

## 8. INTEGRATION REQUIREMENTS
- Model User liên kết tới các bảng Order, Cart, Wishlist, Review trong các bước tiếp theo


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Mật khẩu Hash**: Trường password phải lưu hash bcrypt, độ dài String(255) đảm bảo an toàn.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Model User và Address được định nghĩa chuẩn xác trong schema.prisma.
[ ] **AC-2**: Lệnh npx prisma validate xác nhận tính hợp lệ của schema.
[ ] **AC-3**: Đầy đủ các trường tọa độ latitude/longitude cho địa chỉ giao hàng.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm tra cú pháp schema.prisma bằng npx prisma validate

## 12. EXPECTED OUTPUT
- `backend/prisma/schema.prisma`: Bổ sung model User và Address

## 13. COMPLETION REPORT
- Đã thêm User và Address models vào schema
- Sẵn sàng tích hợp tiếp các model Danh mục và Sản phẩm
