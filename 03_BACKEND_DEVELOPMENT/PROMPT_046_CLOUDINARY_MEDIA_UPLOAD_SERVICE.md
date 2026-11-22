# PROMPT 046 – CLOUDINARY MEDIA UPLOAD, IMAGE OPTIMIZATION & MEDIAFILE RECORD SERVICE

## 1. ROLE
Backend Media & Storage Specialist

## 2. OBJECTIVE
Xây dựng dịch vụ tải lên và tối ưu hóa hình ảnh sản phẩm/banner qua Cloudinary SDK, hỗ trợ định dạng WebP, tự động điều chỉnh kích thước và lưu vết vào bảng MediaFile trong MySQL.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_02_CLOUDINARY_ADMIN_PRODUCT_MANAGEMENT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_02_CLOUDINARY_ADMIN_PRODUCT_MANAGEMENT.md)
> - [USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_14_SHIPPING_FEE_INVOICE_INTEGRATION.md)
> - [USER_MASTER_PROMPT_25_PRODUCTION_UPGRADE_NOTIFICATION_HANDOFF.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_25_PRODUCTION_UPGRADE_NOTIFICATION_HANDOFF.md)

## 3. CONTEXT
Hình ảnh thời trang đòi hỏi độ phân giải cao nhưng kích thước file phải nhỏ để website tải nhanh. Hệ thống tích hợp Cloudinary để tự động nén, chuyển đổi định dạng và trả về URL CDN an toàn.

## 4. PREREQUISITES
- PROMPT_031: Express HTTP Server Architecture

## 5. INPUTS
- Biến môi trường CLOUDINARY_CLOUD_NAME, CLOUDINARY_API_KEY, CLOUDINARY_API_SECRET
- File ảnh từ multipart/form-data

## 6. DETAILED TASKS
1. **Cấu hình Cloudinary SDK và Multer**:
   Tạo config/cloudinary.js khởi tạo Cloudinary v2. Cấu hình multer memoryStorage để nhận file tải lên từ client với giới hạn kích thước 5MB.

2. **Xây dựng UploadService.uploadImage**:
   Sử dụng stream upload đưa ảnh lên Cloudinary với thư mục "routine_fashion/products", áp dụng transform: quality: "auto", fetch_format: "webp", width: 1200, crop: "limit".

3. **Lưu vết vào bảng MediaFile trong Database**:
   Lưu publicId, url, secureUrl, format, bytes, width, height vào bảng MediaFile để quản lý tài nguyên.

4. **Tạo Endpoint POST /api/v1/media/upload**:
   Yêu cầu quyền ADMIN hoặc STAFF, nhận single file hoặc multiple files và trả về danh sách URLs.

## 7. TECHNICAL REQUIREMENTS
- cloudinary ^1.41.0
- multer ^1.4.5-lts.1
- Chỉ chấp nhận định dạng ảnh: JPEG, PNG, WEBP

## 8. INTEGRATION REQUIREMENTS
- Admin Product Form, Category Form, Banner Manager

## 9. SAFETY CONSTRAINTS
- ⚠️ **Malicious File Upload Prevention**: Kiểm tra mime type và magic bytes của file để ngăn chặn upload script độc hại.

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Upload ảnh thành công lên Cloudinary và nhận lại URL WebP.
[ ] **AC-2**: Bản ghi MediaFile được tạo đầy đủ trong database.
[ ] **AC-3**: Upload file không phải ảnh bị từ chối với lỗi 400.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm thử upload file ảnh JPEG và xác nhận file trên Cloudinary

## 12. EXPECTED OUTPUT
- `backend/src/config/cloudinary.js`: Cấu hình Cloudinary SDK
- `backend/src/services/mediaService.js`: Dịch vụ xử lý tải lên và tối ưu ảnh
- `backend/src/controllers/mediaController.js`: Controller tải lên media

## 13. COMPLETION REPORT
- Hệ thống tải lên và tối ưu hóa hình ảnh đám mây đã hoàn thành
