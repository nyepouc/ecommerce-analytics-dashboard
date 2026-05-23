# 🛒 E-Commerce Analytics Dashboard

> Phân tích hành vi mua sắm và phân khúc khách hàng từ **541,909 giao dịch** của một nhà bán lẻ trực tuyến tại Anh, sử dụng **Python**, **SQL** và **Power BI**.

![Status](https://img.shields.io/badge/status-in--progress-yellow)
![Python](https://img.shields.io/badge/Python-3.10+-blue)
![SQL](https://img.shields.io/badge/SQL-MySQL%2FPostgreSQL-orange)
![PowerBI](https://img.shields.io/badge/Power%20BI-Desktop-yellow)
![License](https://img.shields.io/badge/license-MIT-green)

---

## 📌 Mục lục

- [Giới thiệu](#-giới-thiệu)
- [Mục tiêu phân tích](#-mục-tiêu-phân-tích)
- [Bộ dữ liệu](#-bộ-dữ-liệu)
- [Công cụ & Thư viện](#-công-cụ--thư-viện)
- [Cấu trúc thư mục](#-cấu-trúc-thư-mục)
- [Quy trình thực hiện](#-quy-trình-thực-hiện)
- [Kết quả chính & Insight](#-kết-quả-chính--insight)
- [Dashboard Power BI](#-dashboard-power-bi)
- [Cách chạy lại project](#-cách-chạy-lại-project)
- [Hạn chế & Hướng phát triển](#-hạn-chế--hướng-phát-triển)
- [Tác giả](#-tác-giả)

---

## 📖 Giới thiệu

Project này được thực hiện trong khuôn khổ môn **Trực quan hóa Dữ liệu**, với mục tiêu xây dựng một pipeline phân tích dữ liệu thương mại điện tử hoàn chỉnh: từ **thu thập – làm sạch – phân tích – trực quan hóa – đưa ra đề xuất kinh doanh**.

Dataset được sử dụng là **Online Retail Dataset** — ghi lại toàn bộ giao dịch của một công ty bán lẻ trực tuyến chuyên về quà tặng và đồ trang trí tại Vương quốc Anh, trong giai đoạn **01/12/2010 – 09/12/2011**.

---

## 🎯 Mục tiêu phân tích

Project trả lời 5 câu hỏi phân tích sau:

1. **Doanh thu & đơn hàng** phân bố như thế nào theo khu vực địa lý và ngành hàng?
2. **Chiết khấu** (proxy thông qua biến động `UnitPrice`) có ảnh hưởng đến doanh thu như thế nào?
3. **Tỷ lệ hoàn hàng** có liên quan gì đến loại sản phẩm hay quốc gia của khách?
4. **Phân khúc khách hàng** nào mang lại giá trị cao nhất? (Phân tích RFM + Clustering)
5. Từ các phân tích trên, đề xuất **chiến lược khuyến mãi và giữ chân khách hàng** ra sao?

---

## 📦 Bộ dữ liệu

| Thuộc tính | Giá trị |
|---|---|
| Nguồn | UCI Machine Learning Repository – Online Retail |
| Khoảng thời gian | 01/12/2010 → 09/12/2011 |
| Số dòng | 541,909 giao dịch |
| Số cột | 8 |
| Kích thước | ~45 MB |
| Số quốc gia | 38 (UK chiếm ~91%) |
| Số khách hàng | ~4,372 (sau làm sạch) |

### Mô tả cột

| Cột | Kiểu | Mô tả |
|---|---|---|
| `InvoiceNo` | string | Mã hóa đơn (bắt đầu bằng "C" = đơn hủy/hoàn) |
| `StockCode` | string | Mã sản phẩm |
| `Description` | string | Tên/mô tả sản phẩm |
| `Quantity` | int | Số lượng (âm = trả hàng) |
| `InvoiceDate` | datetime | Ngày giờ giao dịch |
| `UnitPrice` | float | Đơn giá (GBP) |
| `CustomerID` | int | Mã khách hàng (~25% bị thiếu) |
| `Country` | string | Quốc gia của khách |

### Vấn đề chất lượng dữ liệu đã xử lý

- 135,080 dòng (~25%) thiếu `CustomerID` → tách thành dataset phân tích riêng
- 10,624 đơn hoàn/hủy (`Quantity < 0`) → tách ra để phân tích return rate
- 2,517 dòng có `UnitPrice ≤ 0` → loại bỏ
- 1,454 dòng thiếu `Description` → loại bỏ
- Mã đặc biệt (`POST`, `M`, `BANK CHARGES`,...) → loại bỏ khỏi phân tích sản phẩm

---

## 🛠 Công cụ & Thư viện

### Python
- `pandas`, `numpy` — xử lý dữ liệu
- `matplotlib`, `seaborn`, `plotly` — trực quan hóa
- `scikit-learn` — K-Means clustering cho RFM
- `mlxtend` — Market Basket Analysis (Apriori)
- `jupyter` — notebook

### SQL
- MySQL / PostgreSQL (chọn 1)
- Window functions, CTE, CASE WHEN

### Power BI
- Power BI Desktop
- DAX measures
- Slicer, drillthrough, bookmark, tooltip tùy chỉnh

---

## 📁 Cấu trúc thư mục

```
ecommerce-analytics-dashboard/
│
├── data/
│   ├── raw/                    # Dữ liệu gốc (không commit lên Git)
│   │   └── E-Commerce_Data.csv
│   └── processed/              # Dữ liệu đã làm sạch
│       ├── cleaned_data.csv
│       ├── rfm_scores.csv
│       └── customer_segments.csv
│
├── notebooks/                  # Jupyter notebooks
│   ├── 01_data_cleaning.ipynb
│   ├── 02_eda_and_insights.ipynb
│   ├── 03_rfm_segmentation.ipynb
│   └── 04_market_basket_analysis.ipynb
│
├── sql/                        # SQL queries phân tích
│   ├── 01_create_schema.sql
│   ├── 02_revenue_analysis.sql
│   ├── 03_customer_rfm.sql
│   ├── 04_return_analysis.sql
│   └── 05_advanced_queries.sql
│
├── powerbi/                    # Dashboard Power BI
│   ├── ecommerce_dashboard.pbix
│   └── dax_measures.md
│
├── reports/                    # Báo cáo & slide
│   ├── final_report.pdf
│   └── presentation.pptx
│
├── images/                     # Screenshot dashboard, biểu đồ
│   ├── dashboard_overview.png
│   ├── customer_segments.png
│   └── revenue_trend.png
│
├── scripts/                    # Script Python tái sử dụng
│   └── data_loader.py
│
├── .gitignore
├── requirements.txt
└── README.md
```

---

## 🔄 Quy trình thực hiện

```mermaid
flowchart LR
    A[Raw CSV<br>541K rows] --> B[Python<br>Data Cleaning]
    B --> C[Cleaned Dataset]
    C --> D[SQL<br>Analysis]
    C --> E[Python<br>EDA + ML]
    D --> F[Power BI<br>Dashboard]
    E --> F
    F --> G[Insights &<br>Recommendations]
```

**Chi tiết các bước:**

1. **Data Cleaning** *(Python)* — Xử lý missing, loại outlier, tạo cột phái sinh (`Revenue`, `Year`, `Month`, `Hour`, `Category`), tách đơn hoàn ra dataset riêng.
2. **SQL Analysis** — Import dữ liệu đã làm sạch vào CSDL, viết queries trả lời các câu hỏi kinh doanh.
3. **EDA & Modeling** *(Python)* — Phân tích thời gian, phân khúc RFM, K-Means clustering, market basket analysis.
4. **Visualization** *(Power BI)* — Xây dashboard 5 trang tương tác.
5. **Reporting** — Tổng hợp insight thành báo cáo và slide trình bày.

---

## 💡 Kết quả chính & Insight

> *Phần này sẽ được cập nhật sau khi hoàn thành phân tích*

### 🔑 Top 5 Insights

1. *[Insight 1 — VD: 8% khách hàng (Champions) đóng góp 45% tổng doanh thu]*
2. *[Insight 2 — VD: Giờ vàng bán hàng là 10-14h các ngày trong tuần]*
3. *[Insight 3 — VD: Tháng 11-12 doanh thu tăng 180% do mùa Giáng sinh]*
4. *[Insight 4]*
5. *[Insight 5]*

### 📊 Đề xuất kinh doanh

- *[Đề xuất 1 — VD: Triển khai chương trình loyalty cho nhóm Champions]*
- *[Đề xuất 2]*
- *[Đề xuất 3]*

---

## 📊 Dashboard Power BI

> 🔗 **[Link Dashboard trực tuyến](https://app.powerbi.com/...)** *(sẽ cập nhật)*

### Trang 1: Executive Overview
![Dashboard Overview](images/dashboard_overview.png)

### Trang 2: Customer Segmentation
![Customer Segments](images/customer_segments.png)

### Trang 3: Sales Analysis
*(Screenshot sẽ được thêm sau)*

### Trang 4: Returns Analysis
*(Screenshot sẽ được thêm sau)*

### Trang 5: Recommendations
*(Screenshot sẽ được thêm sau)*

---

## 🚀 Cách chạy lại project

### Yêu cầu
- Python 3.10+
- MySQL hoặc PostgreSQL
- Power BI Desktop (chỉ trên Windows)

### Cài đặt

```bash
# Clone repo
git clone https://github.com/<your-username>/ecommerce-analytics-dashboard.git
cd ecommerce-analytics-dashboard

# Tạo môi trường ảo
python -m venv venv
source venv/bin/activate     # Linux/Mac
# venv\Scripts\activate      # Windows

# Cài thư viện
pip install -r requirements.txt

# Tải dataset gốc vào data/raw/ (xem README ở data/raw/)
```

### Chạy phân tích

```bash
# Bước 1: Data cleaning
jupyter notebook notebooks/01_data_cleaning.ipynb

# Bước 2: SQL analysis (sau khi import vào DB)
mysql -u user -p ecommerce_db < sql/01_create_schema.sql
mysql -u user -p ecommerce_db < sql/02_revenue_analysis.sql

# Bước 3: EDA và segmentation
jupyter notebook notebooks/02_eda_and_insights.ipynb
jupyter notebook notebooks/03_rfm_segmentation.ipynb

# Bước 4: Mở dashboard
# Mở file powerbi/ecommerce_dashboard.pbix bằng Power BI Desktop
```

---

## ⚠️ Hạn chế & Hướng phát triển

### Hạn chế của dataset
- **Không có cột `Profit` và `Discount`** — phải dùng proxy thông qua biến động `UnitPrice`
- **Không có thông tin giao hàng** (thời gian giao, phí ship) — không thể phân tích trực tiếp tác động giao hàng đến tỷ lệ hoàn
- **Không có demographic của khách hàng** (tuổi, giới tính) — chỉ có quốc gia
- Dữ liệu chỉ có **1 năm** — chưa đủ để phân tích xu hướng dài hạn

### Hướng phát triển
- [ ] Thêm dự đoán Customer Lifetime Value (CLV) bằng mô hình BG/NBD
- [ ] Xây dựng hệ thống recommendation dựa trên collaborative filtering
- [ ] Tự động hóa pipeline bằng Airflow
- [ ] Triển khai dashboard lên Power BI Service và schedule refresh

---

## 👤 Tác giả

**[Tên của bạn]**
- 🎓 Sinh viên ngành Khoa học Dữ liệu
- 📧 Email: your.email@example.com
- 💼 LinkedIn: [linkedin.com/in/your-profile](https://linkedin.com/in/your-profile)
- 🐙 GitHub: [@your-username](https://github.com/your-username)

---

## 📝 License

Project này được phát hành dưới giấy phép **MIT License** — xem file [LICENSE](LICENSE) để biết thêm chi tiết.

## 🙏 Acknowledgements

- Dataset: [UCI Machine Learning Repository – Online Retail](https://archive.ics.uci.edu/ml/datasets/online+retail)
- Giảng viên môn Trực quan hóa Dữ liệu
- Cộng đồng data science Việt Nam

---

⭐ *Nếu project này hữu ích cho bạn, hãy cho một star để ủng hộ nhé!*
