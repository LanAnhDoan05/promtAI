# PROMPT 124 – DOCKERIZATION & MULTI-CONTAINER COMPOSE SETUP (MYSQL, EXPRESS, NEXT.JS)

## 1. ROLE
DevOps / Cloud Architecture Specialist

## 2. OBJECTIVE
Đóng gói toàn bộ hệ thống Routine vào các container Docker độc lập và điều phối bằng docker-compose.yml: 1) Container database MySQL 8.0 với volume dữ liệu bền vững; 2) Container backend Node.js Express với multi-stage build tối ưu; 3) Container frontend Next.js với standalone output; mạng nội bộ an toàn và health check định kỳ.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_10_FINAL_HANDOVER_LOCK.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_10_FINAL_HANDOVER_LOCK.md)
> - [USER_MASTER_PROMPT_17_SYSTEM_STABILITY_FINAL_ACCEPTANCE.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_17_SYSTEM_STABILITY_FINAL_ACCEPTANCE.md)

## 3. CONTEXT
Dockerization giúp đóng gói toàn bộ môi trường chạy, cho phép triển khai hệ thống Routine lên bất kỳ hạ tầng đám mây nào (AWS, GCP, DigitalOcean, VPS cá nhân) chỉ với một câu lệnh duy nhất: docker compose up -d.

## 4. PREREQUISITES
- PROMPT_122: Frontend Build
- PROMPT_123: Backend Ecosystem

## 5. INPUTS
- Cấu trúc monorepo của Routine

## 6. DETAILED TASKS
1. **Viết Dockerfile cho Backend**:
   Sử dụng base image node:18-alpine, multi-stage build: stage 1 cài dependencies và npx prisma generate; stage 2 copy code và chạy bin/www với non-root user (node).

2. **Viết Dockerfile cho Frontend**:
   Sử dụng output: "standalone" trong next.config.js. Base image node:18-alpine, copy .next/standalone, .next/static và public, expose cổng 3000.

3. **Viết docker-compose.yml Điều Phối 3 Dịch Vụ**:
   Định nghĩa services: mysql (port 3306, volume mysql_data), backend (depends_on mysql healthy, port 5001), frontend (depends_on backend, port 3000). Mạng bridge routine-network.

## 7. TECHNICAL REQUIREMENTS
- Docker Compose v2 specification
- Dung lượng image tối ưu < 200MB nhờ Alpine Linux
- Non-root user đảm bảo an toàn bảo mật container

## 8. INTEGRATION REQUIREMENTS
- Tương thích môi trường Linux và Windows Docker Desktop


### HƯỚNG DẪN THI CÔNG CHI TIẾT DÀNH CHO AI AGENT:
- **Kiểm soát mã nguồn:** Đảm bảo đọc kỹ file đích trước khi chỉnh sửa. Không sử dụng mock data hoặc dữ liệu giả lập.
- **Tính toán tiền tệ:** Luôn sử dụng kiểu dữ liệu số nguyên VNĐ hoặc Decimal(12,2), không làm tròn sai số trong quá trình cộng dồn phí vận chuyển và mã giảm giá.
- **Ràng buộc an toàn:** Xử lý đầy đủ các trường hợp biên (boundary cases): rớt mạng, mã coupon hết hạn, giỏ hàng trống, biến thể hết tồn kho trong lúc đang checkout.
- **Chuẩn phong cách Routine:** Giao diện tối giản hiện đại (đen, trắng, xám, đỏ điểm xuyết). Typography sắc nét, hỗ trợ tiếng Việt đầy đủ dấu Unicode NFC.

## 9. SAFETY CONSTRAINTS
- ⚠️ **Persistent Storage Rule**: Bắt buộc phải gắn volume cho cơ sở dữ liệu MySQL để không bị mất dữ liệu khi restart container.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Chạy docker compose build xây dựng thành công cả 3 images.
[ ] **AC-2**: Chạy docker compose up -d khởi động toàn bộ hệ thống trong vòng 60 giây.
[ ] **AC-3**: Truy cập được website trên localhost:3000 và backend trên localhost:5001.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm tra cú pháp docker compose config và kiểm tra khởi động container

## 12. EXPECTED OUTPUT
- `backend/Dockerfile`: Dockerfile cho Backend Express
- `frontend/Dockerfile`: Dockerfile cho Frontend Next.js
- `docker-compose.yml`: Tập tin điều phối cụm dịch vụ Docker

## 13. COMPLETION REPORT
- Đóng gói Container Docker và điều phối Docker Compose hoàn thành
