# PROMPT 097 – BI DASHBOARD RESPONSIVE TABLES OPTIMIZATION (SIDE-BY-SIDE & COMPACT COLUMNS)

## 1. ROLE
Frontend UI/UX Optimization Specialist

## 2. OBJECTIVE
Tối ưu hóa bố cục hai bảng thống kê trong trang AI BI: 1) "Sản Phẩm Bán Chạy & Tỷ Trọng Doanh Thu" và 2) "Sản Phẩm Được Quan Tâm & Tỷ Lệ Xem/Mua". Thiết lập hiển thị song song (Side-by-side) trên desktop không tràn ngang, phân bổ tỷ lệ chiều rộng cột hợp lý, cắt gọn tên sản phẩm (text-truncate), và xếp chồng dọc gọn gàng trên tablet/mobile.


> 💡 **THAM CHIẾU MASTER PROMPT GỐC TỪ NGƯỜI DÙNG:**
> - [USER_MASTER_PROMPT_05_AI_BUSINESS_INTELLIGENCE_AUDIT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_05_AI_BUSINESS_INTELLIGENCE_AUDIT.md)
> - [USER_MASTER_PROMPT_24_ADMIN_NOTIFICATION_CENTER.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_24_ADMIN_NOTIFICATION_CENTER.md)
> - [USER_MASTER_PROMPT_28_AI_BI_IMPLEMENTATION_AND_E2E_AUDIT.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_28_AI_BI_IMPLEMENTATION_AND_E2E_AUDIT.md)
> - [USER_MASTER_PROMPT_29_BI_DASHBOARD_TABLES_UI_OPTIMIZATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_29_BI_DASHBOARD_TABLES_UI_OPTIMIZATION.md)
> - ⭐ **Tài liệu tham chiếu trực tiếp:** [USER_MASTER_PROMPT_29_BI_DASHBOARD_TABLES_UI_OPTIMIZATION.md](../00_USER_PRODUCTION_MASTER_PROMPTS/USER_MASTER_PROMPT_29_BI_DASHBOARD_TABLES_UI_OPTIMIZATION.md)

## 3. CONTEXT
Hai bảng số liệu này trước đây gặp lỗi tràn khỏi màn hình, cột số bị cắt và không thích ứng tốt. Việc tối ưu layout mang lại trải nghiệm xem báo cáo mượt mà trên mọi độ phân giải từ 390px đến 1920px.

## 4. PREREQUISITES
- PROMPT_096: AI BI Module

## 5. INPUTS
- Component BiDashboardTables và CSS styles

## 6. DETAILED TASKS
1. **Tối ưu Layout Container bằng CSS Grid/Flexbox**:
   Cấu hình container: display: grid, grid-template-columns: repeat(auto-fit, minmax(480px, 1fr)), gap: 20px, width: 100%, min-width: 0.

2. **Tối ưu Chiều Rộng Cột và Cắt Gọn Tên (Ellipsis)**:
   Đặt table-layout: fixed. Cột Tên sản phẩm chiếm 40-45% với white-space: nowrap, overflow: hidden, text-overflow: ellipsis. Các cột số liệu (Giá, Đã bán, Doanh thu, Tỷ trọng) chiếm tỷ lệ phần trăm cố định.

3. **Tương thích Responsive Mobile & Tablet**:
   Khi màn hình < 1024px: chuyển 2 bảng xếp chồng dọc (1 cột). Bọc bảng trong khung có overflow-x: auto nhẹ nhàng để các cột không bao giờ bị cắt cụt.


### QUY CHUẨN TỐI ƯU GIAO DIỆN HAI BẢNG BI DASHBOARD (Theo USER_MASTER_PROMPT_29):
1. **Vấn đề đã xử lý trong thực tế:**
   - Hai bảng bị tràn container, cột bên phải bị cắt, tên sản phẩm chiếm quá nhiều diện tích.
   - Giải pháp: Cấu hình `table-layout: fixed`, gán `min-width: 0` cho container con trong Grid, phân bổ tỷ lệ phần trăm % chặt chẽ.
2. **Quy tắc hiển thị Desktop vs Mobile:**
   - Desktop (>= 1024px): Hai bảng hiển thị song song (grid 2 cột) không làm xuất hiện thanh cuộn ngang của Dashboard.
   - Tablet/Mobile (< 1024px): Hai bảng tự động xếp chồng (1 cột), bọc trong thẻ có `overflow-x: auto` chống cắt dữ liệu.


## 7. TECHNICAL REQUIREMENTS
- Zero horizontal page overflow trên Dashboard
- min-width: 0 trên flex/grid children để chống tràn flexbox

## 8. INTEGRATION REQUIREMENTS
- Tích hợp trực tiếp vào trang /admin/ai-bi

## 9. SAFETY CONSTRAINTS
- ⚠️ **Table Overflow Bleed**: Bảng không được đẩy thanh cuộn ngang xuất hiện trên toàn trang (toàn bộ trang Dashboard).

## 10. ACCEPTANCE CRITERIA
[ ] **AC-1**: Hai bảng hiển thị song song hoàn hảo trên desktop 1440px và 1920px.
[ ] **AC-2**: Không có cột số liệu nào bị cắt hay che khuất.
[ ] **AC-3**: Hiển thị trơn tru không tràn ngang trên cả mobile 390px.

## 11. TESTING REQUIREMENTS
1. **Tình huống kiểm thử 1**: Kiểm tra DevTools ở các kích thước: 390px, 768px, 1366px, 1920px

### CODE MINH HỌA TRIỂN KHAI CHUẨN HÓA:

```css
/* frontend/src/components/Admin/BiTablesSection.module.css */
.tablesGrid {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 20px;
  width: 100%;
  box-sizing: border-box;
}

.tableCard {
  background: #ffffff;
  border: 1px solid #e5e5e5;
  border-radius: 8px;
  padding: 16px;
  min-width: 0; /* QUAN TRỌNG: Ngăn chặn flex/grid item bị tràn */
  overflow: hidden;
}

.tableWrapper {
  width: 100%;
  overflow-x: auto;
}

.compactTable {
  width: 100%;
  table-layout: fixed; /* Cố định chiều rộng cột */
  border-collapse: collapse;
}

.colProduct {
  width: 42%;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis; /* Cắt gọn tên dài kèm dấu 3 chấm */
}

.colNumber {
  width: 19%;
  text-align: right;
  white-space: nowrap;
}

@media (max-width: 1024px) {
  .tablesGrid {
    grid-template-columns: 1fr; /* Xếp chồng 1 cột trên mobile/tablet */
  }
}
```


## 12. EXPECTED OUTPUT
- `frontend/src/components/Admin/BiTablesSection.jsx`: Component bảng thống kê tối ưu
- `frontend/src/components/Admin/BiTablesSection.module.css`: CSS Module tối ưu bảng

## 13. COMPLETION REPORT
- Tối ưu bố cục responsive hai bảng thống kê BI Dashboard hoàn thành
