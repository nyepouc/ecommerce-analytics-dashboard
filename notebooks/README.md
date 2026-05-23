# 📓 Jupyter Notebooks

Các notebook được đánh số theo thứ tự thực hiện. Chạy lần lượt từ `01` đến `04`.

## Danh sách notebook

### `01_data_cleaning.ipynb`
**Mục đích:** Làm sạch và chuẩn hóa dữ liệu thô.

**Các bước:**
- Đọc CSV với encoding phù hợp
- Khảo sát chất lượng dữ liệu (missing, outlier, kiểu dữ liệu)
- Tách đơn hủy/hoàn (InvoiceNo bắt đầu bằng "C")
- Loại bỏ giao dịch lỗi (Quantity ≤ 0, UnitPrice ≤ 0)
- Tạo cột phái sinh: `Revenue`, `Year`, `Month`, `Hour`, `DayOfWeek`, `Category`
- Export ra `data/processed/cleaned_data.csv`

**Output:** `data/processed/cleaned_data.csv`, `data/processed/cancellations.csv`

---

### `02_eda_and_insights.ipynb`
**Mục đích:** Phân tích thăm dò và phát hiện insight chính.

**Các phân tích:**
- Phân phối doanh thu, đơn hàng, khách hàng
- Time series: doanh thu theo ngày/tuần/tháng
- Heatmap giờ × ngày (giờ vàng)
- Top sản phẩm, top quốc gia
- Phân tích mùa vụ

---

### `03_rfm_segmentation.ipynb`
**Mục đích:** Phân khúc khách hàng bằng RFM và K-Means.

**Các bước:**
- Tính Recency, Frequency, Monetary cho từng khách
- Chia score 1-5 cho từng chỉ số
- K-Means clustering trên RFM scaled
- Đặt tên nhóm: Champions, Loyal, At Risk, Lost, New
- Phân tích đóng góp doanh thu của từng nhóm

**Output:** `data/processed/rfm_scores.csv`, `data/processed/customer_segments.csv`

---

### `04_market_basket_analysis.ipynb`
**Mục đích:** Phân tích sản phẩm thường mua cùng nhau.

**Các bước:**
- Tạo ma trận transaction × product
- Apriori algorithm tìm frequent itemsets
- Tính association rules (support, confidence, lift)
- Đề xuất bundle/cross-sell

---

## Cách chạy

```bash
# Cài jupyter
pip install jupyter

# Mở notebook
jupyter notebook
```
