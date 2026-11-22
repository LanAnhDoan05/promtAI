# USER MASTER PROMPT #30: 30 FROM ZERO PROMPT LIBRARY SPECIFICATION
> **Nguồn gốc:** Prompt chỉ đạo thực tế từ Người dùng (User Request) tại Step 12577.
> **Độ dài gốc:** 11991 ký tự.
> **Mục đích trong thư viện:** Cung cấp toàn văn đặc tả nghiệp vụ, yêu cầu kỹ thuật và ràng buộc sản xuất thực tế mà người dùng đã trực tiếp chỉ đạo và kiểm chứng trong dự án Routine Web.

---

# MASTER TASK: BUILD A COMPLETE FROM-ZERO PROMPT LIBRARY FOR ROUTINE E-COMMERCE PLATFORM

## I. VAI TRÒ

Bạn là một đội ngũ chuyên gia cấp cao bao gồm:

- Principal Software Architect.
- Senior Full-stack Engineer.
- Database Architect.
- UI/UX Designer.
- E-commerce Business Analyst.
- AI Agent Engineer.
- Payment Integration Engineer.
- DevOps Engineer.
- Cybersecurity Engineer.
- QA Automation Engineer.
- Technical Documentation Specialist.

Nhiệm vụ của bạn KHÔNG PHẢI là trực tiếp xây dựng website.

Nhiệm vụ của bạn là nghiên cứu dự án Routine hiện tại và tạo ra một thư viện gồm TỐI THIỂU 100 PROMPT ĐỘC LẬP, CHI TIẾT, CÓ TRÌNH TỰ để một AI Agent khác có thể sử dụng chúng nhằm xây dựng lại toàn bộ dự án Routine từ con số 0.

## II. REFERENCE PROJECT

Repository tham chiếu:

https://github.com/LanAnhDoan05/routine-web-demo

Hãy nghiên cứu toàn bộ repository trước khi viết prompt.

Phải phân tích:

1. README.
2. Cấu trúc thư mục.
3. Frontend source code.
4. Backend source code.
5. Database schema.
6. Prisma models.
7. Prisma migrations.
8. API routes.
9. Controllers.
10. Services.
11. Components.
12. CSS và giao diện.
13. Assets và hình ảnh.
14. Authentication.
15. Authorization.
16. Gemini AI integration.
17. AI Stylist.
18. Smart Outfit.
19. Product retrieval.
20. Cart và Checkout.
21. Order Management.
22. VNPay integration.
23. Admin Portal.
24. Customer Service.
25. CRM.
26. Marketing Analytics.
27. Các báo cáo kỹ thuật và tài liệu có sẵn.

Không chỉ đọc README rồi tự suy đoán chức năng.

Phải dựa vào source code thực tế để xác định từng nghiệp vụ.

Nếu không truy cập được một file hoặc module, phải ghi nhận là chưa xác minh, không tự bịa nội dung.

## III. MỤC TIÊU CUỐI CÙNG

Tạo một thư viện prompt giúp AI Agent xây dựng một dự án Routine mới hoàn toàn, từ một thư mục trống, đến một hệ thống thương mại điện tử có đầy đủ Frontend, Backend, Database, AI Agent và Admin Portal.

Hệ thống mới phải tái tạo được các chức năng và nghiệp vụ đã xác minh trong dự án tham chiếu.

Không được chỉ tạo một website giao diện minh họa.

Phải hướng đến một hệ thống Full-stack thực sự có thể vận hành.

## IV. QUY TẮC TẠO PROMPT

1. Số lượng tối thiểu: 100 prompt riêng biệt.
2. Khuyến nghị: 105–120 prompt nếu phạm vi thực tế yêu cầu.
3. Mỗi prompt phải được lưu thành một file Markdown riêng.
4. Mỗi prompt phải có mục tiêu độc lập.
5. Mỗi prompt phải có đầu vào, công việc cụ thể, yêu cầu kỹ thuật và đầu ra.
6. Mỗi prompt phải có tiêu chí nghiệm thu.
7. Mỗi prompt phải nêu rõ những chức năng cũ hoặc thành phần không được phá vỡ.
8. Mỗi prompt phải chỉ rõ các dependency và công việc cần hoàn thành trước đó.
9. Không viết những prompt chung chung như "hãy hoàn thiện website".
10. Không chia một nhiệm vụ quá lớn thành một prompt duy nhất.
11. Không lặp lại cùng một nội dung ở nhiều prompt.
12. Không tạo prompt chỉ để tăng số lượng.
13. Mỗi prompt phải đủ chi tiết để một AI Agent khác có thể thực hiện mà không cần đoán ý định của người viết.

## V. PHÂN CHIA CÁC GIAI ĐOẠN

Tạo các thư mục theo thứ tự:

### 00_PROJECT_FOUNDATION
Nghiên cứu yêu cầu, xác định nghiệp vụ, phân tích hệ thống tham chiếu, xây dựng Software Requirement Specification, Business Requirement Document, kiến trúc tổng thể, sơ đồ luồng nghiệp vụ, quy chuẩn coding.

### 01_ENVIRONMENT_SETUP
Khởi tạo dự án từ thư mục trống, cài đặt môi trường, Node.js, package manager, Next.js, React, Express, TypeScript hoặc JavaScript theo kiến trúc được xác minh, cấu hình môi trường, Git, Docker nếu cần, kết nối môi trường phát triển.

### 02_DATABASE_ARCHITECTURE
Thiết kế MySQL, Prisma, bảng User, Role, Permission, Product, Category, ProductVariant, ProductImage, Inventory, Cart, CartItem, Order, OrderItem, Payment, Coupon, Review, Wishlist, Conversation, Message, Lead, Media và các bảng khác được xác minh từ dự án tham chiếu.

Thiết kế quan hệ, khóa ngoại, unique constraints, index, migration và chiến lược dữ liệu.

### 03_BACKEND_DEVELOPMENT
Xây dựng Express Server, API architecture, Middleware, Authentication, Authorization, Validation, Error Handling, User API, Product API, Category API, Inventory API, Cart API, Order API, Review API, Coupon API, Upload API, Conversation API, Admin API.

Mỗi module cần có prompt xây dựng riêng.

### 04_FRONTEND_DESIGN
Khởi tạo Next.js, cấu trúc component, design system, typography, màu sắc, layout, header, footer, homepage, navigation, category page, product listing, product detail, responsive, search, filter, sorting, loading, empty states, error states.

Phải xây dựng giao diện thương mại điện tử thời trang chuyên nghiệp.

Không sử dụng phong cách UI tạo tự động bằng AI, không lạm dụng gradient, card bo tròn hoặc animation.

### 05_ECOMMERCE_FEATURES
Đăng ký, đăng nhập, OTP, hồ sơ khách hàng, tìm kiếm, danh mục, biến thể sản phẩm, màu sắc, kích thước, giỏ hàng Guest, giỏ hàng Customer, Wishlist, Checkout, Address Management, Voucher, Order Management, Order Tracking, Review, Inventory Management.

### 06_AI_STYLIST_AGENT
Đây là phân hệ đặc biệt quan trọng.

Phải chia thành nhiều prompt độc lập để xây dựng:

1. Gemini integration.
2. AI Agent architecture.
3. System instruction.
4. Intent detection.
5. Entity extraction.
6. Vietnamese natural language understanding.
7. Fashion thesaurus.
8. Product retrieval.
9. Database grounding.
10. RAG nếu phù hợp kiến trúc.
11. Context management.
12. Multi-turn conversation.
13. Budget filtering.
14. Color filtering.
15. Size filtering.
16. Product recommendation.
17. Outfit recommendation.
18. Smart Outfit.
19. Product cards.
20. Add-to-cart action.
21. Purchase intent detection.
22. Customer service handoff.
23. Human takeover.
24. Conversation persistence.
25. AI fallback.
26. Rate limiting.
27. AI testing and evaluation.

AI phải hiểu hội thoại có ngữ cảnh.

Ví dụ:

Khách: Tôi muốn áo len dưới 1 triệu.

Khách: Màu trắng.

Khách: Có size M không?

Khách: Còn màu đen?

AI phải duy trì các điều kiện trước đó và chỉ cập nhật điều kiện mới.

AI không được tự tạo tên sản phẩm, giá, hình ảnh, size hoặc tồn kho.

Dữ liệu sản phẩm phải được truy xuất và xác minh từ Database.

### 07_ADMIN_CRM
Xây dựng Admin Authentication, Dashboard, Product Management, Category Management, Inventory Management, Order Management, Customer Management, Staff Management, Role Management, Conversation Management, Lead Management, Customer Service Chat, Analytics.

Phải có prompt riêng cho từng module.

Đặc biệt phải xây dựng luồng chat hai chiều giữa khách hàng và nhân viên.

### 08_PAYMENT_VNPAY
Chia riêng các prompt cho:
- Payment architecture.
- COD.
- VNPay Sandbox.
- Dynamic payment URL.
- Dynamic QR.
- HMAC-SHA512.
- Return URL.
- IPN.
- Signature verification.
- Payment state machine.
- Idempotency.
- Transaction management.
- Payment failure.
- Timeout.
- Payment testing.

Không được thiết kế hệ thống dựa trên QR tĩnh.

### 09_TESTING_SECURITY
Unit testing, Integration testing, API testing, E2E testing, Browser testing, AI testing, Payment testing, Database testing, Security testing, Authorization testing, Negative testing, Performance testing, Regression testing.

Phải có prompt kiểm thử toàn bộ hành trình từ khách hàng đến Admin.

### 10_DEPLOYMENT_FINALIZATION
Production build, Environment configuration, Docker nếu phù hợp, Deployment, Database migration, Backup, Logging, Monitoring, SEO, Performance, Documentation, Final acceptance.

## VI. CẤU TRÚC BẮT BUỘC CỦA MỖI PROMPT

Mỗi file prompt phải có cấu trúc:

# PROMPT XX – TÊN NHIỆM VỤ

## 1. ROLE
Vai trò AI Agent cần đảm nhiệm.

## 2. OBJECTIVE
Mục tiêu cụ thể.

## 3. CONTEXT
Bối cảnh dự án, kiến trúc và các module liên quan.

## 4. PREREQUISITES
Các prompt hoặc công việc phải hoàn thành trước.

## 5. INPUTS
Những file, dữ liệu, cấu hình và tài nguyên cần sử dụng.

## 6. DETAILED TASKS
Danh sách các công việc chi tiết cần thực hiện.

## 7. TECHNICAL REQUIREMENTS
Yêu cầu kỹ thuật, công nghệ, API, Database và quy tắc nghiệp vụ.

## 8. INTEGRATION REQUIREMENTS
Các module phải kết nối với nhau như thế nào.

## 9. SAFETY CONSTRAINTS
Những điều không được phép thực hiện.

## 10. ACCEPTANCE CRITERIA
Tiêu chí xác định hoàn thành.

## 11. TESTING REQUIREMENTS
Các tình huống phải kiểm thử.

## 12. EXPECTED OUTPUT
File, source code, tài liệu hoặc kết quả cần tạo.

## 13. COMPLETION REPORT
Yêu cầu AI Agent báo cáo sau khi thực hiện.

Mỗi prompt phải có nội dung đủ chi tiết để copy và sử dụng trực tiếp.

## VII. YÊU CẦU VỀ TÍNH LIÊN KẾT

Các prompt phải được sắp xếp theo dependency thực tế.

Ví dụ:

Không xây dựng Checkout trước khi có Product, Cart và Order.

Không xây dựng Product Retrieval trước khi có Product Database.

Không xây dựng AI Handoff trước khi có Conversation và Message.

Không xây dựng Dashboard trước khi có các nghiệp vụ tạo dữ liệu.

Không kiểm thử VNPay trước khi có Payment API.

Không triển khai Production trước khi có Security Audit và Migration Plan.

Tạo sơ đồ dependency để thể hiện thứ tự sử dụng.

## VIII. QUY CHUẨN CÔNG NGHỆ

Không được tự ý thay đổi công nghệ so với dự án tham chiếu.

Trước hết hãy xác minh stack thực tế.

Các công nghệ cần xem xét gồm:

- Next.js.
- React.
- Node.js.
- Express.
- MySQL.
- Prisma.
- Google Gemini.
- VNPay.
- JWT.
- Bcrypt.
- CSS Modules.
- Các thư viện khác thực sự có trong dự án.

Nếu cần đề xuất thay đổi kiến trúc, phải tách riêng thành một đề xuất, không tự đưa thay đổi đó vào prompt tái tạo dự án.

## IX. QUY TẮC AN TOÀN

Các prompt phải yêu cầu Agent:

- Không hardcode dữ liệu nghiệp vụ.
- Không tạo dữ liệu giả trên Production.
- Không lưu secrets trong source code.
- Không tự ý xóa Database.
- Không reset Database.
- Không tự ý thay đổi thông tin kết nối.
- Không tự động deploy.
- Không tự động commit hoặc push.
- Không đánh dấu chức năng PASS khi chưa kiểm thử.
- Không sử dụng mock data thay cho API thật trong chức năng chính thức.
- Có xử lý lỗi cho mọi tích hợp bên ngoài.

## X. OUTPUT – ĐẦU RA BẮT BUỘC

Tạo một thư mục mới:

ROUTINE-FROM-ZERO-PROMPTS/

Bên trong phải có:

- 11 thư mục giai đoạn.
- Tối thiểu 100 file PROMPT_XXX.md.
- MASTER_PROMPT.md.
- EXECUTION_ORDER.md.
- PROJECT_REQUIREMENTS.md.
- ARCHITECTURE_OVERVIEW.md.
- PROMPT_DEPENDENCY_MAP.md.
- ACCEPTANCE_CRITERIA.md.

EXECUTION_ORDER.md phải chỉ rõ:
- Prompt nào chạy đầu tiên.
- Prompt nào có thể chạy độc lập.
- Prompt nào phụ thuộc prompt khác.
- Prompt nào cần phê duyệt trước khi thực hiện.
- Prompt nào cần kiểm thử trước khi chuyển bước.

## XI. KIỂM TRA CHẤT LƯỢNG THƯ VIỆN PROMPT

Sau khi tạo xong:

1. Đếm số lượng prompt.
2. Kiểm tra số thứ tự.
3. Kiểm tra file bị trùng.
4. Kiểm tra prompt bị thiếu nội dung.
5. Kiểm tra các dependency.
6. Kiểm tra sự phù hợp với repository.
7. Kiểm tra khả năng sử dụng độc lập.
8. Kiểm tra các yêu cầu nghiệm thu.
9. Kiểm tra sự nhất quán về công nghệ.
10. Đảm bảo tất cả prompt có thể copy trực tiếp để sử dụng.

Không tạo file prompt rỗng.

Không dùng một file chứa 100 prompt thay cho 100 file độc lập.

Không chỉ tạo danh sách tiêu đề.

## XII. GIỚI HẠN NHIỆM VỤ

ĐÂY LÀ NHIỆM VỤ TẠO THƯ VIỆN PROMPT, KHÔNG PHẢI NHIỆM VỤ XÂY DỰNG WEBSITE.

Chỉ được tạo và ghi các file tài liệu trong thư mục ROUTINE-FROM-ZERO-PROMPTS.

Không chỉnh sửa source code hiện tại.

Không thay đổi Database.

Không cài đặt thư viện.

Không chạy migration.

Không thay đổi cấu hình dự án.

Không xóa hoặc di chuyển file hiện có.

Không tạo website mới trong quá trình này.

Nếu nội dung quá lớn, hãy tạo từng giai đoạn, lưu file ngay sau khi hoàn thành từng nhóm để tránh mất dữ liệu.

Chỉ kết thúc khi thư viện có ít nhất 100 prompt đầy đủ, độc lập, có thứ tự và đã được kiểm tra chất lượng.

BẮT ĐẦU BẰNG VIỆC NGHIÊN CỨU REPOSITORY, SAU ĐÓ TẠO TOÀN BỘ THƯ VIỆN PROMPT THEO YÊU CẦU TRÊN.
