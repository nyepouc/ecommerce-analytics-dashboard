# 📊 Power BI Dashboard

## File chính

- **`ecommerce_dashboard.pbix`** — File Power BI Desktop chứa toàn bộ dashboard
- **`dax_measures.md`** — Tài liệu các DAX measures đã viết

## Yêu cầu

- **Power BI Desktop** (miễn phí từ Microsoft Store hoặc [powerbi.microsoft.com](https://powerbi.microsoft.com/desktop/))
- Chỉ chạy được trên **Windows** (hoặc Mac qua máy ảo)

## Cấu trúc dashboard

### 📄 Trang 1: Executive Overview
- KPI cards: Total Revenue, Orders, Customers, AOV, YoY Growth
- Line chart: Doanh thu theo thời gian
- Map: Doanh thu theo quốc gia
- Slicer: thời gian, quốc gia

### 📄 Trang 2: Sales Analysis
- Top 10 sản phẩm theo doanh thu (bar chart)
- Top 10 quốc gia (loại trừ UK)
- Heatmap: Giờ × Ngày trong tuần
- Donut chart: Tỷ trọng theo Category

### 📄 Trang 3: Customer Segmentation (RFM)
- Treemap: Các phân khúc khách
- Scatter plot: Frequency × Monetary, kích thước theo Recency
- KPI từng segment
- Drillthrough vào từng segment

### 📄 Trang 4: Returns & Cancellation
- Return rate tổng quan
- Top sản phẩm bị hoàn nhiều nhất
- Tỷ lệ hoàn theo quốc gia
- Xu hướng theo thời gian

### 📄 Trang 5: Recommendations
- Tóm tắt insight chính
- Đề xuất hành động cụ thể
- Roadmap triển khai

## Data source

Dashboard kết nối tới:
- `data/processed/cleaned_data.csv` — bảng fact giao dịch
- `data/processed/customer_segments.csv` — bảng dim khách hàng

## Cách publish lên Power BI Service

1. Sign in vào Power BI Desktop bằng tài khoản Microsoft
2. File → Publish → Chọn workspace
3. Vào https://app.powerbi.com → Share → Get link
4. Lưu link vào README chính
