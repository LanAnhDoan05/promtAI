# USER MASTER PROMPT #05: 05 AI BUSINESS INTELLIGENCE AUDIT
> **Nguồn gốc:** Prompt chỉ đạo thực tế từ Người dùng (User Request) tại Step 1432.
> **Độ dài gốc:** 6059 ký tự.
> **Mục đích trong thư viện:** Cung cấp toàn văn đặc tả nghiệp vụ, yêu cầu kỹ thuật và ràng buộc sản xuất thực tế mà người dùng đã trực tiếp chỉ đạo và kiểm chứng trong dự án Routine Web.

---

# AUDIT & COMPLETE AI BUSINESS INTELLIGENCE – ROUTINE WEB

Tôi cần kiểm tra và hoàn thiện hệ thống AI quản trị kinh doanh của Routine Web.

LƯU Ý: Chatbot Gemini AI Stylist hiện đã được báo cáo hoàn thành 10/10 kịch bản. Không được nhầm chatbot tư vấn thời trang với AI phân tích và hỗ trợ ra quyết định kinh doanh.

## 1. KIỂM TRA HIỆN TRẠNG

Trước tiên, hãy kiểm tra toàn bộ source code, Database, Backend và giao diện Admin để xác định các chức năng sau đã được triển khai thực tế hay chưa:

1. AI phân tích doanh thu.
2. AI phân tích sản phẩm bán chạy và bán chậm.
3. AI dự báo nhu cầu và kiến nghị nhập hàng.
4. AI đề xuất phân phối hàng hóa giữa các cửa hàng.
5. AI phân tích khách hàng và CRM.
6. AI đề xuất kế hoạch Marketing.
7. CRM Dashboard, Customer 360, phân khúc RFM, Loyalty và Marketing Automation.

Với mỗi chức năng, ghi rõ:
- Đã có giao diện chưa?
- Đã có API Backend chưa?
- Đã kết nối Database thật của môi trường test chưa?
- Đã có logic tính toán và phân tích chưa?
- Đã tích hợp Gemini AI chưa?
- Đã kiểm thử đầu cuối chưa?

Không được đánh dấu hoàn thành chỉ vì đã có một trang giao diện hoặc một nút bấm.

## 2. AI PHÂN TÍCH DOANH THU

Xây dựng hoặc hoàn thiện chức năng cho Admin:

- Xem tổng doanh thu theo ngày, tuần, tháng.
- So sánh doanh thu giữa các giai đoạn.
- Phân tích số lượng đơn hàng, giá trị đơn trung bình.
- Phân tích sản phẩm bán chạy và bán chậm.
- Phân tích doanh thu theo danh mục và cửa hàng nếu có dữ liệu.
- Phân tích lợi nhuận khi có dữ liệu giá vốn hợp lệ.

Gemini phải có khả năng đọc dữ liệu đã tổng hợp từ Backend và đưa ra nhận xét, nguyên nhân có căn cứ, xu hướng và kiến nghị.

Không tự bịa doanh thu, lợi nhuận hoặc nguyên nhân tăng giảm.

## 3. AI KIẾN NGHỊ NHẬP HÀNG

Dựa trên:
- Tồn kho hiện tại.
- Lịch sử bán hàng.
- Tốc độ tiêu thụ sản phẩm.
- Mùa vụ nếu có dữ liệu.
- Thời gian cung ứng nếu có dữ liệu.

AI đưa ra:
- Danh sách sản phẩm có nguy cơ hết hàng.
- Sản phẩm tồn kho lâu.
- Số lượng nhập đề xuất.
- Mức độ ưu tiên nhập hàng.
- Cơ sở và lý do của từng đề xuất.

Phải phân biệt rõ số liệu thực tế và số lượng dự báo. Nếu thiếu lịch sử bán hàng hoặc dữ liệu nhà cung cấp thì phải thông báo giới hạn, không tự tạo con số.

AI chỉ đưa ra kiến nghị, không tự động tạo đơn mua hàng hoặc thay đổi tồn kho.

## 4. AI PHÂN PHỐI HÀNG HÓA

Nếu Database có dữ liệu nhiều cửa hàng và tồn kho theo từng cửa hàng, xây dựng chức năng:

- So sánh tồn kho giữa các cửa hàng.
- Phát hiện cửa hàng thừa hàng và cửa hàng thiếu hàng.
- Đề xuất điều chuyển sản phẩm.
- Nêu số lượng đề xuất và căn cứ.
- Đánh giá tác động dự kiến.

Không được phân phối nếu không có dữ liệu tồn kho theo địa điểm. Không tự tạo số liệu cửa hàng hoặc tự thực hiện điều chuyển.

## 5. AI LẬP KẾ HOẠCH MARKETING

Xây dựng chức năng để Admin yêu cầu Gemini:

- Phân tích tình hình kinh doanh và nhóm sản phẩm cần thúc đẩy.
- Phân tích phân khúc khách hàng.
- Đề xuất khách hàng mục tiêu.
- Đề xuất mục tiêu chiến dịch.
- Đề xuất thông điệp, Big Idea và nội dung.
- Đề xuất kênh truyền thông.
- Đề xuất ngân sách và KPI.
- Xây dựng lịch triển khai.
- Đề xuất phương pháp đo lường hiệu quả.

Kế hoạch phải dựa trên dữ liệu kinh doanh và khách hàng thực tế có sẵn. Những thông tin chưa có dữ liệu phải được ghi là giả định hoặc đề xuất tham khảo, không trình bày như sự thật.

## 6. AI PHÂN TÍCH KHÁCH HÀNG – CRM

Kiểm tra và hoàn thiện:

- Customer 360.
- Phân khúc khách hàng theo RFM nếu đủ dữ liệu.
- Khách hàng mới, khách hàng quay lại.
- Giá trị đơn hàng trung bình.
- Tần suất mua hàng.
- Khách hàng có nguy cơ rời bỏ nếu đủ dữ liệu.
- Gợi ý chăm sóc và chương trình khách hàng thân thiết.
- Đo lường hiệu quả chiến dịch Marketing.

Bảo vệ dữ liệu cá nhân khách hàng, phân quyền truy cập và không đưa thông tin nhạy cảm vào phản hồi không cần thiết.

## 7. GIAO DIỆN ADMIN

Tạo một khu vực AI Business Intelligence riêng trong Admin, dễ tìm và dễ sử dụng.

Có thể tổ chức thành các mục:
- Tổng quan kinh doanh.
- Phân tích doanh thu.
- Dự báo và nhập hàng.
- Phân phối hàng hóa.
- Phân tích khách hàng.
- Kế hoạch Marketing.
- Trợ lý AI quản trị.

Giao diện cần có:
- Biểu đồ và số liệu trực quan.
- Bộ lọc thời gian.
- Bộ lọc cửa hàng và danh mục nếu dữ liệu hỗ trợ.
- Khu vực đặt câu hỏi cho AI.
- Kết quả phân tích có dẫn chứng số liệu.
- Các kiến nghị được phân loại theo mức độ ưu tiên.

Không thay thế hoặc phá vỡ trang Admin hiện tại.

## 8. NGUYÊN TẮC KỸ THUẬT

- Tái sử dụng Database, API và cấu trúc hiện có khi phù hợp.
- Không sửa Cloudinary hoặc cấu hình Cloudinary.
- Không thay đổi Gemini AI Stylist đang hoạt động nếu không cần thiết.
- Không sửa hoặc xóa dữ liệu thật trong `defaultdb`.
- Mọi kiểm thử ghi dữ liệu phải sử dụng `routine_test_db`.
- Không tự động nhập hàng, điều chuyển hàng hoặc chạy chiến dịch thật.
- Không bịa dữ liệu để làm biểu đồ đẹp.
- Phân biệt dữ liệu thực tế, dữ liệu dự báo và giả định.
- Không làm lộ API Key, thông tin đăng nhập hoặc dữ liệu khách hàng.

## 9. KIỂM THỬ VÀ BÀN GIAO

Kiểm thử từng chức năng từ giao diện Admin đến Backend, Database và Gemini.

Tạo dữ liệu kiểm thử có kiểm soát trong `routine_test_db` nếu cần.

Tạo tài liệu:
`docs/AI_BUSINESS_INTELLIGENCE_REPORT.md`

Báo cáo phải có:
1. Chức năng nào đã tồn tại trước khi thực hiện.
2. Chức năng nào cần xây dựng mới.
3. Chức năng nào đã hoàn thiện.
4. Chức năng nào chưa thể hoàn thiện do thiếu dữ liệu.
5. Bằng chứng kiểm thử thực tế.
6. Hướng dẫn Admin sử dụng từng chức năng.
7. Các câu hỏi mẫu để kiểm tra AI.
8. Những giới hạn và giả định của mô hình.

MỤC TIÊU CUỐI CÙNG:

Routine Web phải có hai nhóm AI độc lập nhưng có thể sử dụng chung dữ liệu sản phẩm và kinh doanh:

- Gemini AI Stylist: tư vấn và hỗ trợ khách hàng mua sắm.
- AI Business Intelligence: hỗ trợ Admin phân tích kinh doanh, doanh thu, tồn kho, nhập hàng, phân phối và lập kế hoạch Marketing.

Không được tuyên bố hoàn thành nếu mới chỉ tạo giao diện mà chưa có dữ liệu, logic và khả năng phân tích thực tế.
