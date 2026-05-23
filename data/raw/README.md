# 📂 Raw Data

> ⚠️ **File dữ liệu gốc KHÔNG được commit lên Git** (đã thêm vào `.gitignore`).

## Cách tải dataset

Để chạy lại project, bạn cần tải dataset gốc và đặt vào thư mục này:

### Tùy chọn 1: Tải từ UCI
1. Truy cập: https://archive.ics.uci.edu/ml/datasets/online+retail
2. Tải file `Online Retail.xlsx`
3. Convert sang CSV và đổi tên thành `E-Commerce_Data.csv`
4. Đặt vào `data/raw/`

### Tùy chọn 2: Tải từ Kaggle
```bash
kaggle datasets download -d carrie1/ecommerce-data -p data/raw/
unzip data/raw/ecommerce-data.zip -d data/raw/
```

## Cấu trúc file mong đợi

```
data/raw/
└── E-Commerce_Data.csv     (~45 MB, 541,909 dòng, 8 cột)
```

## Schema

| Cột | Kiểu | Mô tả |
|---|---|---|
| InvoiceNo | string | Mã hóa đơn |
| StockCode | string | Mã sản phẩm |
| Description | string | Mô tả sản phẩm |
| Quantity | int | Số lượng |
| InvoiceDate | string | Ngày giờ giao dịch |
| UnitPrice | float | Đơn giá (GBP) |
| CustomerID | int | Mã khách hàng |
| Country | string | Quốc gia |
