# PROMPT 019 – PRISMA ORM INITIALIZATION & MYSQL 8.0 CONNECTION

## 1. ROLE
Senior Database Engineer / Prisma Specialist

## 2. OBJECTIVE
Khởi tạo cấu trúc Prisma ORM 6.19.3 trong thư mục backend, kết nối an toàn với cơ sở dữ liệu MySQL 8.0 qua biến môi trường DATABASE_URL.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_09_REAL_DATA_AND_BUSINESS_LOGIC.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_09_REAL_DATA_AND_BUSINESS_LOGIC.md)
> - [USER_MASTER_PROMPT_13_MYSQL_AI_ADDRESS_SHIPPING_SYNC.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_13_MYSQL_AI_ADDRESS_SHIPPING_SYNC.md)
> - [USER_MASTER_PROMPT_12_ROUTINE_VN_CATALOG_SCRAPING.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_12_ROUTINE_VN_CATALOG_SCRAPING.md)

## 3. CONTEXT
Dự án Routine sử dụng kiến trúc MySQL 8.0 quan hệ chuẩn và Prisma ORM 6.19.3. Bước đầu tiên của tầng dữ liệu là khởi tạo Prisma CLI, cấu hình datasource MySQL, provider client và kiểm tra kết nối kết nối thành công đến database.

## 4. PREREQUISITES
- PROMPT_012: Node.js Express Backend Bootstrap đã hoàn thành
- PROMPT_014: Cấu hình biến môi trường DATABASE_URL trong backend/.env hợp lệ
- Cơ sở dữ liệu MySQL 8.0 đang hoạt động trên cổng 3306

## 5. INPUTS
- Biến môi trường DATABASE_URL="mysql://root:password@localhost:3306/routine_db"
- Tài liệu schema MySQL của Routine

## 6. DETAILED TASKS
1. **Khởi tạo Prisma trong backend**:
   Chạy lệnh npx prisma init trong thư mục backend để tạo thư mục prisma/ và file schema.prisma chuẩn.

2. **Cấu hình Datasource và Client Generator**:
   Cấu hình datasource db với provider = "mysql" và url = env("DATABASE_URL"). Cấu hình generator client với provider = "prisma-client-js".

3. **Tạo Singleton Prisma Client Wrapper**:
   Xây dựng file backend/src/config/prisma.js hoặc src/prisma.js khởi tạo new PrismaClient() với log query/error trong môi trường development, ngăn chặn khởi tạo nhiều instance.

4. **Kiểm tra kết nối Database Ping**:
   Viết script kiểm tra ping database bằng prisma.$connect() và prisma.$queryRaw`SELECT 1` để đảm bảo kết nối thông suốt.

## 7. TECHNICAL REQUIREMENTS
- Prisma version: ^6.19.3
- Provider: mysql
- Singleton pattern cho PrismaClient
- Không hardcode mật khẩu hay connection string

## 8. INTEGRATION REQUIREMENTS
- Backend Express server import prisma từ src/config/prisma.js
- Tự động ngắt kết nối (graceful disconnect) khi process nhận SIGINT/SIGTERM

## 9. SAFETY CONSTRAINTS
- ⚠️ **Connection Pool Exhaustion**: Phải dùng singleton instance để tránh cạn kiệt connection pool trong MySQL.
- ⚠️ **Windows DLL File Lock**: Khi chạy npx prisma generate, đảm bảo tiến trình backend đang tạm dừng nếu gặp lỗi EBUSY/file lock.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: File backend/prisma/schema.prisma được tạo với datasource mysql và client generator.
[ ] **AC-2**: Module backend/src/config/prisma.js export instance PrismaClient chuẩn singleton.
[ ] **AC-3**: Lệnh npx prisma validate trả về kết quả schema valid.
[ ] **AC-4**: Script kiểm thử ping kết nối MySQL thành công không gặp lỗi kết nối.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Chạy npx prisma validate kiểm tra tính đúng đắn của schema.prisma
2. **Tình huống kiểm thử 2**: Chạy node -e "const p = require('./src/config/prisma'); p.$connect().then(()=>console.log('Connected')).finally(()=>p.$disconnect())"

## 12. EXPECTED OUTPUT
- `backend/prisma/schema.prisma`: File schema Prisma ban đầu
- `backend/src/config/prisma.js`: Prisma Client singleton instance

## 13. COMPLETION REPORT
- Xác nhận kết nối MySQL 8.0 thành công
- Cấu hình Prisma CLI sẵn sàng cho các bước migration mô hình dữ liệu tiếp theo
