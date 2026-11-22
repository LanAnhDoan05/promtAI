# LỘ TRÌNH THỰC THI TUẦN TỰ (EXECUTION ORDER & WORKFLOW)
## ROUTINE E-COMMERCE PLATFORM – 128 PROMPTS

Tài liệu này định nghĩa thứ tự thực thi nghiêm ngặt từ Prompt 001 đến Prompt 128, nêu rõ các chốt chặn kiểm duyệt (Approval Gates) và các bài kiểm thử bắt buộc tại từng giai đoạn.

---

### GIAI ĐOẠN 0: NỀN TẢNG DỰ ÁN & THIẾT KẾ KIẾN TRÚC (00_PROJECT_FOUNDATION)
| Thứ tự | Mã Prompt | Tên nhiệm vụ | Loại thực thi | Điều kiện tiên quyết |
| :---: | :---: | :--- | :---: | :--- |
| 1 | `PROMPT_001` | Khảo sát hệ thống Routine & Tính khả thi dự án | Bắt buộc | Thư mục dự án trống |
| 2 | `PROMPT_002` | Xây dựng Business Requirements Document (BRD) | Tuần tự | PROMPT_001 |
| 3 | `PROMPT_003` | Lập Software Requirements Specification (SRS) | Tuần tự | PROMPT_002 |
| 4 | `PROMPT_004` | Thiết kế kiến trúc tổng thể High-Level (C4 Model) | Tuần tự | PROMPT_003 |
| 5 | `PROMPT_005` | Thiết lập Coding Standards, Git Flow & Quy chuẩn mã | Độc lập | PROMPT_004 |
| 6 | `PROMPT_006` | Thiết kế đặc tả RESTful API Specification (OpenAPI) | Tuần tự | PROMPT_004 |
| 7 | `PROMPT_007` | Xây dựng chính sách an ninh & Bảo vệ dữ liệu | Tuần tự | PROMPT_004 |
| 8 | `PROMPT_008` | Thiết lập Data Dictionary & Quy tắc toàn vẹn | Tuần tự | PROMPT_003 |
| 9 | `PROMPT_009` | Thiết kế kiến trúc AI Stylist Agent & Grounding | Tuần tự | PROMPT_004 |
| 10 | `PROMPT_010` | 🛑 **GATEWAY 0:** Thẩm định hồ sơ Foundation & Phê duyệt | Chốt duyệt | PROMPT_001 -> 009 |

---

### GIAI ĐOẠN 1: THIẾT LẬP MÔI TRƯỜNG PHÁT TRIỂN (01_ENVIRONMENT_SETUP)
| Thứ tự | Mã Prompt | Tên nhiệm vụ | Loại thực thi | Điều kiện tiên quyết |
| :---: | :---: | :--- | :---: | :--- |
| 11 | `PROMPT_011` | Khởi tạo cấu trúc dự án Monorepo Frontend/Backend | Bắt buộc | PROMPT_010 |
| 12 | `PROMPT_012` | Cài đặt môi trường Node.js & Express Server 4.22 | Tuần tự | PROMPT_011 |
| 13 | `PROMPT_013` | Khởi tạo Next.js 16.4.3 (Turbopack, React 19.2.3) | Tuần tự | PROMPT_011 |
| 14 | `PROMPT_014` | Cấu hình biến môi trường an toàn (.env.example) | Tuần tự | PROMPT_012, 013 |
| 15 | `PROMPT_015` | Thiết lập ESLint & Kiểm tra chất lượng mã nguồn | Độc lập | PROMPT_012, 013 |
| 16 | `PROMPT_016` | Cấu hình lưu trữ media tĩnh & Assets hình ảnh | Độc lập | PROMPT_012, 013 |
| 17 | `PROMPT_017` | Cấu hình chạy song song Backend:5001 & Frontend:3000 | Tuần tự | PROMPT_012, 013, 014 |
| 18 | `PROMPT_018` | 🛑 **GATEWAY 1:** Kiểm tra sức khỏe môi trường (Health Check) | Chốt duyệt | PROMPT_011 -> 017 |

---

### GIAI ĐOẠN 2: THIẾT KẾ CƠ SỞ DỮ LIỆU PRISMA & MYSQL (02_DATABASE_ARCHITECTURE)
| Thứ tự | Mã Prompt | Tên nhiệm vụ | Loại thực thi | Điều kiện tiên quyết |
| :---: | :---: | :--- | :---: | :--- |
| 19 | `PROMPT_019` | Cấu hình Prisma CLI 6.19 & Kết nối MySQL 8.0 | Bắt buộc | PROMPT_018 |
| 20 | `PROMPT_020` | Thiết kế Model User & Role Phân quyền | Tuần tự | PROMPT_019 |
| 21 | `PROMPT_021` | Thiết kế Model Address & Shipping Rules | Tuần tự | PROMPT_020 |
| 22 | `PROMPT_022` | Thiết kế Model Category & Style thời trang | Tuần tự | PROMPT_019 |
| 23 | `PROMPT_023` | Thiết kế Model Product & ProductVariant (SKU) | Tuần tự | PROMPT_022 |
| 24 | `PROMPT_024` | Thiết kế Model Outfit & OutfitProduct (Smart Outfit) | Tuần tự | PROMPT_023 |
| 25 | `PROMPT_025` | Thiết kế Model Cart, CartItem, Wishlist & WishlistItem | Tuần tự | PROMPT_020, 023 |
| 26 | `PROMPT_026` | Thiết kế Model Order, OrderItem & StockReservation | Tuần tự | PROMPT_020, 023 |
| 27 | `PROMPT_027` | Thiết kế Model PaymentTransaction & Coupon | Tuần tự | PROMPT_026 |
| 28 | `PROMPT_028` | Thiết kế Model TrafficLog & StoreSetting | Tuần tự | PROMPT_019 |
| 29 | `PROMPT_029` | Thiết kế Model AiConversation, Notification & AI BI | Tuần tự | PROMPT_020, 026 |
| 30 | `PROMPT_030` | 🛑 **GATEWAY 2:** Chạy Migration & Nạp dữ liệu Seeding thực | Chốt duyệt | PROMPT_019 -> 029 |

---

### GIAI ĐOẠN 3: PHÁT TRIỂN BACKEND API SERVICES (03_BACKEND_DEVELOPMENT)
| Thứ tự | Mã Prompt | Tên nhiệm vụ | Loại thực thi | Điều kiện tiên quyết |
| :---: | :---: | :--- | :---: | :--- |
| 31 | `PROMPT_031` | Xây dựng Express Middleware Pipeline & Error Handler | Bắt buộc | PROMPT_030 |
| 32 | `PROMPT_032` | Xây dựng AuthService & JWT Stateless Authentication | Tuần tự | PROMPT_031 |
| 33 | `PROMPT_033` | Xây dựng RBAC Middleware (Admin & Customer Guards) | Tuần tự | PROMPT_032 |
| 34 | `PROMPT_034` | Xây dựng Category Service & API Endpoints | Tuần tự | PROMPT_031 |
| 35 | `PROMPT_035` | Xây dựng Product Catalog Service & Dynamic Filters | Tuần tự | PROMPT_034 |
| 36 | `PROMPT_036` | Xây dựng Full-text Search Service tiếng Việt | Tuần tự | PROMPT_035 |
| 37 | `PROMPT_037` | Xây dựng Cart Service (Hỗ trợ Guest & Customer) | Tuần tự | PROMPT_035 |
| 38 | `PROMPT_038` | Xây dựng Wishlist Service & API Endpoints | Tuần tự | PROMPT_032, 035 |
| 39 | `PROMPT_039` | Xây dựng Shipping Fee Calculation Service theo Tọa độ | Tuần tự | PROMPT_031 |
| 40 | `PROMPT_040` | Xây dựng Coupon Validation & Discount Service | Tuần tự | PROMPT_031 |
| 41 | `PROMPT_041` | Xây dựng Stock Reservation Service chống Overselling | Tuần tự | PROMPT_035 |
| 42 | `PROMPT_042` | Xây dựng Order Lifecycle Service & Quản lý đơn hàng | Tuần tự | PROMPT_037, 039, 040, 041 |
| 43 | `PROMPT_043` | Xây dựng Customer Profile & Address Book Service | Tuần tự | PROMPT_032 |
| 44 | `PROMPT_044` | Xây dựng Review & Rating Service cho khách hàng | Tuần tự | PROMPT_042 |
| 45 | `PROMPT_045` | Xây dựng Smart Outfit Service & Bộ phối thời trang | Tuần tự | PROMPT_035 |
| 46 | `PROMPT_046` | Xây dựng Media Upload Controller (Local & Cloudinary) | Độc lập | PROMPT_031 |
| 47 | `PROMPT_047` | Xây dựng Notification Service & SSE Realtime Stream | Tuần tự | PROMPT_042 |
| 48 | `PROMPT_048` | 🛑 **GATEWAY 3:** Kiểm thử toàn diện API Integration Suite | Chốt duyệt | PROMPT_031 -> 047 |

---

### GIAI ĐOẠN 4: THIẾT KẾ FRONTEND GIAO DIỆN & DESIGN SYSTEM (04_FRONTEND_DESIGN)
| Thứ tự | Mã Prompt | Tên nhiệm vụ | Loại thực thi | Điều kiện tiên quyết |
| :---: | :---: | :--- | :---: | :--- |
| 49 | `PROMPT_049` | Xây dựng Design System, Typography & Global CSS | Bắt buộc | PROMPT_018 |
| 50 | `PROMPT_050` | Xây dựng RootLayout & Các Context Providers toàn cục | Tuần tự | PROMPT_049 |
| 51 | `PROMPT_051` | Xây dựng Header Navbar chuẩn thương hiệu ROUTINE | Tuần tự | PROMPT_050 |
| 52 | `PROMPT_052` | Xây dựng Mobile Drawer Menu & Responsive Header | Tuần tự | PROMPT_051 |
| 53 | `PROMPT_053` | Xây dựng Footer tối giản & Khẳng định thương hiệu | Tuần tự | PROMPT_050 |
| 54 | `PROMPT_054` | Xây dựng Hero Slider trang chủ kết nối Database | Tuần tự | PROMPT_050 |
| 55 | `PROMPT_055` | Xây dựng ProductCard Component tối ưu hiển thị | Tuần tự | PROMPT_049 |
| 56 | `PROMPT_056` | Xây dựng Category Page (/category/[slug]) & Bộ lọc | Tuần tự | PROMPT_055 |
| 57 | `PROMPT_057` | Xây dựng Product Detail Page (/product/[id]) | Tuần tự | PROMPT_055 |
| 58 | `PROMPT_058` | Xây dựng Search Page (/search) & Gợi ý từ khóa | Tuần tự | PROMPT_055 |
| 59 | `PROMPT_059` | Xây dựng Smart Outfit Showcase Page (/smart-outfit) | Tuần tự | PROMPT_055 |
| 60 | `PROMPT_060` | Xây dựng Thư viện Common Components (Button, Modal, Toast)| Độc lập | PROMPT_049 |
| 61 | `PROMPT_061` | Tối ưu hóa Responsive trên 5 kích thước chuẩn | Tuần tự | PROMPT_051 -> 060 |
| 62 | `PROMPT_062` | 🛑 **GATEWAY 4:** Thẩm định thẩm mỹ UI & Đạt 0 ESLint Warnings| Chốt duyệt | PROMPT_049 -> 061 |

---

### GIAI ĐOẠN 5: TÍCH HỢP NGHIỆP VỤ E-COMMERCE ĐẦY ĐỦ (05_ECOMMERCE_FEATURES)
| Thứ tự | Mã Prompt | Tên nhiệm vụ | Loại thực thi | Điều kiện tiên quyết |
| :---: | :---: | :--- | :---: | :--- |
| 63 | `PROMPT_063` | Xây dựng UserContext & Quản lý phiên xác thực | Bắt buộc | PROMPT_032, 050 |
| 64 | `PROMPT_064` | Xây dựng Luồng đăng ký tài khoản & OTP xác thực | Tuần tự | PROMPT_063 |
| 65 | `PROMPT_065` | Xây dựng Màn hình đăng nhập & Phân luồng vai trò | Tuần tự | PROMPT_063 |
| 66 | `PROMPT_066` | Xây dựng Luồng quên mật khẩu & Đặt lại mật khẩu | Tuần tự | PROMPT_064 |
| 67 | `PROMPT_067` | Xây dựng CartContext & Giỏ hàng Drawer trượt | Tuần tự | PROMPT_037, 050 |
| 68 | `PROMPT_068` | Xây dựng Trang chi tiết giỏ hàng (/cart) | Tuần tự | PROMPT_067 |
| 69 | `PROMPT_069` | Xây dựng WishlistContext & Trang sản phẩm yêu thích | Tuần tự | PROMPT_038, 050 |
| 70 | `PROMPT_070` | Xây dựng Checkout Bước 1: Địa chỉ & Tọa độ phí ship | Tuần tự | PROMPT_039, 068 |
| 71 | `PROMPT_071` | Xây dựng Checkout Bước 2: Nhập mã Voucher giảm giá | Tuần tự | PROMPT_040, 070 |
| 72 | `PROMPT_072` | Xây dựng Checkout Bước 3: Lựa chọn COD hoặc VNPay | Tuần tự | PROMPT_071 |
| 73 | `PROMPT_073` | Xây dựng Xử lý tạo đơn hàng & Khóa tạm tồn kho | Tuần tự | PROMPT_041, 042, 072 |
| 74 | `PROMPT_074` | Xây dựng Trang đặt hàng thành công (/checkout/success)| Tuần tự | PROMPT_073 |
| 75 | `PROMPT_075` | Xây dựng Trang lịch sử đơn hàng (/orders) | Tuần tự | PROMPT_074 |
| 76 | `PROMPT_076` | Xây dựng Trang quản lý hồ sơ cá nhân (/profile) | Tuần tự | PROMPT_043, 063 |
| 77 | `PROMPT_077` | Xây dựng Form đánh giá sản phẩm sau mua hàng | Tuần tự | PROMPT_044, 075 |
| 78 | `PROMPT_078` | 🛑 **GATEWAY 5:** Kiểm thử toàn diện Customer Journey E2E | Chốt duyệt | PROMPT_063 -> 077 |

---

### GIAI ĐOẠN 6: PHÂN HỆ TRỢ LÝ AI STYLIST THÔNG MINH (06_AI_STYLIST_AGENT)
| Thứ tự | Mã Prompt | Tên nhiệm vụ | Loại thực thi | Điều kiện tiên quyết |
| :---: | :---: | :--- | :---: | :--- |
| 79 | `PROMPT_079` | Cấu hình Google Gemini Client & Model Parameters | Bắt buộc | PROMPT_018 |
| 80 | `PROMPT_080` | Xây dựng Fashion Thesaurus & Từ điển thời trang | Tuần tự | PROMPT_079 |
| 81 | `PROMPT_081` | Xây dựng Intent Detection & Bộ định tuyến ý định | Tuần tự | PROMPT_080 |
| 82 | `PROMPT_082` | Xây dựng Entity Extraction (Màu, Size, Dáng, Dịp, Giá)| Tuần tự | PROMPT_081 |
| 83 | `PROMPT_083` | Xây dựng Multi-turn Context Management (Ngữ cảnh đa lượt)| Tuần tự | PROMPT_082 |
| 84 | `PROMPT_084` | Xây dựng Database Grounding Engine (Chống bịa dữ liệu)| Tuần tự | PROMPT_035, 083 |
| 85 | `PROMPT_085` | Xây dựng AI Tool Calling (Search, SKU Detail, Outfits)| Tuần tự | PROMPT_084 |
| 86 | `PROMPT_086` | Xây dựng Thuật toán phối đồ Smart Outfit Recommender | Tuần tự | PROMPT_045, 085 |
| 87 | `PROMPT_087` | Nhận diện ý định mua hàng & Kích hoạt Thêm Giỏ Hàng | Tuần tự | PROMPT_085 |
| 88 | `PROMPT_088` | Xây dựng Cơ chế phát hiện và chuyển giao Lead (Handoff)| Tuần tự | PROMPT_087 |
| 89 | `PROMPT_089` | Xây dựng Floating Widget AI Stylist trên Frontend | Tuần tự | PROMPT_050 |
| 90 | `PROMPT_090` | Xây dựng Giao diện Chat tương tác & Thẻ sản phẩm trực quan| Tuần tự | PROMPT_089 |
| 91 | `PROMPT_091` | Xây dựng Lưu trữ phiên hội thoại vào MySQL | Tuần tự | PROMPT_029, 090 |
| 92 | `PROMPT_092` | Xây dựng Rate-limiting & Fallback Heuristic Engine | Tuần tự | PROMPT_091 |
| 93 | `PROMPT_093` | 🛑 **GATEWAY 6:** Đánh giá độ chính xác AI qua 5 lượt hội thoại| Chốt duyệt | PROMPT_079 -> 092 |

---

### GIAI ĐOẠN 7: ADMIN PORTAL, CRM & BUSINESS INTELLIGENCE (07_ADMIN_CRM)
| Thứ tự | Mã Prompt | Tên nhiệm vụ | Loại thực thi | Điều kiện tiên quyết |
| :---: | :---: | :--- | :---: | :--- |
| 94 | `PROMPT_094` | Xây dựng Admin Auth & Khung giao diện AdminLayout | Bắt buộc | PROMPT_033, 050 |
| 95 | `PROMPT_095` | Xây dựng Admin Dashboard & Chỉ số KPI thời gian thực | Tuần tự | PROMPT_094 |
| 96 | `PROMPT_096` | Xây dựng Phân hệ AI Business Intelligence (/admin/ai-bi)| Tuần tự | PROMPT_095 |
| 97 | `PROMPT_097` | Tối ưu hóa 2 Bảng thống kê BI Dashboard Đa màn hình | Tuần tự | PROMPT_096 |
| 98 | `PROMPT_098` | Xây dựng Quản lý Sản phẩm & Biến thể SKU (/admin/products)| Tuần tự | PROMPT_094 |
| 99 | `PROMPT_099` | Xây dựng Quản lý Danh mục & Phong cách (/admin/categories)| Tuần tự | PROMPT_094 |
| 100 | `PROMPT_100` | Xây dựng Quản lý Đơn hàng & Duyệt trạng thái (/admin/orders)| Tuần tự | PROMPT_042, 094 |
| 101 | `PROMPT_101` | Xây dựng Quản lý Khách hàng & Phân hạng RFM (/admin/customers)| Tuần tự | PROMPT_094 |
| 102 | `PROMPT_102` | Xây dựng Quản lý Handoff Leads (/admin/leads) | Tuần tự | PROMPT_088, 094 |
| 103 | `PROMPT_103` | Xây dựng Realtime Live Chat Chuyên viên tiếp quản lead | Tuần tự | PROMPT_047, 102 |
| 104 | `PROMPT_104` | Xây dựng Quản lý Vouchers & Banners (/admin/vouchers) | Tuần tự | PROMPT_094 |
| 105 | `PROMPT_105` | 🛑 **GATEWAY 7:** Kiểm thử vận hành đồng bộ Admin Portal & CRM | Chốt duyệt | PROMPT_094 -> 104 |

---

### GIAI ĐOẠN 8: CỔNG THANH TOÁN VNPAY & EMBEDDED QR (08_PAYMENT_VNPAY)
| Thứ tự | Mã Prompt | Tên nhiệm vụ | Loại thực thi | Điều kiện tiên quyết |
| :---: | :---: | :--- | :---: | :--- |
| 106 | `PROMPT_106` | Thiết lập kiến trúc VNPAY Gateway & Nạp Merchant Config | Bắt buộc | PROMPT_018 |
| 107 | `PROMPT_107` | Xây dựng Tạo URL thanh toán động kèm HMAC-SHA512 | Tuần tự | PROMPT_106 |
| 108 | `PROMPT_108` | Xây dựng Embedded Dynamic VNPAY QR Code trên Checkout | Tuần tự | PROMPT_107 |
| 109 | `PROMPT_109` | Xây dựng Xử lý Return URL (/api/v1/payment/vnpay-return) | Tuần tự | PROMPT_107 |
| 110 | `PROMPT_110` | Xây dựng IPN Webhook Server-to-Server & Cập nhật PAID | Tuần tự | PROMPT_109 |
| 111 | `PROMPT_111` | Xây dựng Cơ chế Idempotency & Bảng Transaction Log | Tuần tự | PROMPT_110 |
| 112 | `PROMPT_112` | Xây dựng Luồng xử lý Giao dịch Thất bại, Timeout & Hủy | Tuần tự | PROMPT_110 |
| 113 | `PROMPT_113` | 🛑 **GATEWAY 8:** Kiểm thử tự động VNPAY Sandbox thanh toán | Chốt duyệt | PROMPT_106 -> 112 |

---

### GIAI ĐOẠN 9: KIỂM THỬ TỰ ĐỘNG & BẢO MẬT HỆ THỐNG (09_TESTING_SECURITY)
| Thứ tự | Mã Prompt | Tên nhiệm vụ | Loại thực thi | Điều kiện tiên quyết |
| :---: | :---: | :--- | :---: | :--- |
| 114 | `PROMPT_114` | Xây dựng Bộ Unit & Integration Test hàm nghiệp vụ lõi | Bắt buộc | PROMPT_048 |
| 115 | `PROMPT_115` | Kiểm thử bảo mật API & Phòng chống SQLi/XSS/RBAC 401 | Tuần tự | PROMPT_114 |
| 116 | `PROMPT_116` | Kiểm thử toàn vẹn Database & Ràng buộc Transaction | Tuần tự | PROMPT_114 |
| 117 | `PROMPT_117` | Xây dựng Kịch bản Playwright E2E toàn bộ hành trình | Tuần tự | PROMPT_078, 105, 113 |
| 118 | `PROMPT_118` | Kiểm thử hồi quy AI Agent qua 5 lượt ngữ cảnh liên tiếp| Tuần tự | PROMPT_093 |
| 119 | `PROMPT_119` | Kiểm thử Responsive UI/UX trên 5 độ phân giải chuẩn | Tuần tự | PROMPT_097 |
| 120 | `PROMPT_120` | Kiểm thử Concurrency & Đồng bộ Realtime SSE đa phiên | Tuần tự | PROMPT_103 |
| 121 | `PROMPT_121` | 🛑 **GATEWAY 9:** Biên bản thẩm định an ninh & Nghiệm thu QA | Chốt duyệt | PROMPT_114 -> 120 |

---

### GIAI ĐOẠN 10: TRIỂN KHAI PRODUCTION & CHUYỂN GIAO (10_DEPLOYMENT_FINALIZATION)
| Thứ tự | Mã Prompt | Tên nhiệm vụ | Loại thực thi | Điều kiện tiên quyết |
| :---: | :---: | :--- | :---: | :--- |
| 122 | `PROMPT_122` | Biên dịch Next.js Production Build (Đủ 38 Routes) | Bắt buộc | PROMPT_121 |
| 123 | `PROMPT_123` | Đóng gói Dockerfile & docker-compose.yml toàn hệ thống | Tuần tự | PROMPT_122 |
| 124 | `PROMPT_124` | Xây dựng Quy trình Migration & Backup Database định kỳ | Tuần tự | PROMPT_123 |
| 125 | `PROMPT_125` | Cấu hình Giám sát hệ thống (Monitoring) & Centralized Log | Tuần tự | PROMPT_123 |
| 126 | `PROMPT_126` | Tối ưu hóa SEO OpenGraph, Sitemap & Core Web Vitals | Tuần tự | PROMPT_122 |
| 127 | `PROMPT_127` | Soạn thảo Sổ tay vận hành dành cho Quản trị viên & CSKH | Tuần tự | PROMPT_105 |
| 128 | `PROMPT_128` | 🛑 **GATEWAY 10:** Lập Biên bản nghiệm thu & Bàn giao Go-Live | Nghiệm thu cuối | PROMPT_001 -> 127 |
