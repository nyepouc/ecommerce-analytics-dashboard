# 🗄️ SQL Analysis

Toàn bộ phân tích SQL được tổ chức thành 5 file `.sql`, đánh số theo thứ tự thực thi.

## Yêu cầu

- MySQL 8.0+ hoặc PostgreSQL 13+
- Dữ liệu đã làm sạch từ notebook `01_data_cleaning.ipynb` (`data/processed/cleaned_data.csv`)

## Cách chạy

```bash
# MySQL
mysql -u root -p ecommerce_db < sql/01_create_schema.sql
mysql -u root -p ecommerce_db < sql/02_revenue_analysis.sql
# ... tương tự

# PostgreSQL
psql -U postgres -d ecommerce_db -f sql/01_create_schema.sql
```

## Danh sách file

### `01_create_schema.sql`
Tạo bảng `transactions`, định nghĩa kiểu dữ liệu, indexes cho hiệu suất truy vấn.

### `02_revenue_analysis.sql`
- Doanh thu theo tháng/quý/năm
- Top 10 quốc gia theo doanh thu
- Top 20 sản phẩm bán chạy
- Average Order Value (AOV) theo quốc gia

### `03_customer_rfm.sql`
- Tính Recency, Frequency, Monetary cho từng khách
- Phân chia score 1-5 bằng `NTILE()` window function
- Phân loại khách hàng theo điểm tổng hợp
- Customer Lifetime Value

### `04_return_analysis.sql`
- Tỷ lệ hoàn hàng theo sản phẩm
- Tỷ lệ hoàn theo quốc gia
- Mối quan hệ giữa giá và tỷ lệ hoàn

### `05_advanced_queries.sql`
- Cohort retention analysis
- Repeat customer rate theo tháng
- Phân tích giờ vàng bằng `EXTRACT(HOUR FROM ...)`
- Running total doanh thu

## Kỹ thuật SQL được sử dụng

✅ Common Table Expressions (CTE) với `WITH`  
✅ Window functions: `ROW_NUMBER()`, `RANK()`, `NTILE()`, `LAG()`, `LEAD()`  
✅ Aggregations với `GROUP BY ROLLUP`  
✅ `CASE WHEN` cho phân loại  
✅ Subqueries và derived tables  
✅ Date functions cho time-series analysis
