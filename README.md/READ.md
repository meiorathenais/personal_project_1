# 📊 Retail Business Performance Analysis

---

## 🎯 Bối cảnh & Mục tiêu

Doanh nghiệp bán lẻ đang đối mặt với 03 thách thức cốt lõi cần được làm rõ bằng dữ liệu:

| # | Câu hỏi phân tích | Bảng dữ liệu liên quan |
|---|---|---|
| 1 | Xu hướng doanh thu 10 năm thay đổi như thế nào? | `sales`, `orders`, `customers`, `payments` |
| 2 | Chiến dịch khuyến mãi có thực sự tạo ra lợi nhuận? | `promotions`, `order_items`, `returns`, `web_traffic` |
| 3 | Tồn kho và chuỗi cung ứng vận hành hiệu quả đến đâu? | `inventory`, `shipments`, `products`, `geography` |

---

## 📁 Cấu trúc dự án

```
promo-effectiveness-analysis/
│
├── notebooks/
│   ├── 01_eda_data_quality.ipynb          # Khám phá & kiểm tra chất lượng 15 bảng
│   ├── 02_revenue_trend_analysis.ipynb    # Xu hướng doanh thu, AOV, khách hàng mới
│   ├── 03_promo_effectiveness.ipynb       # Đo lường hiệu quả chiến dịch khuyến mãi
│   └── 04_inventory_supply_chain.ipynb    # Tồn kho, lead-time, hoàn trả
│
├── data/
│   ├── raw/README.md                      # Mô tả dataset (file gốc không public)
│   └── processed/                         # Dữ liệu đã aggregate, sẵn sàng visualize
│
├── dashboard/                             # Export từ Power BI (.png / .pdf)
├── reports/                               # Báo cáo insights tổng hợp
├── assets/                                # Ảnh dùng trong README
│
├── .gitignore
├── requirements.txt
└── README.md
```

---

## 📦 Dataset

**13 bảng dữ liệu** | Giai đoạn: 2012–2022

| Nhóm | Bảng |
|---|---|
| Giao dịch | `sales`, `orders`, `order_items`, `payments` |
| Khách hàng | `customers`, `reviews`, `returns` |
| Sản phẩm & Tồn kho | `products`, `inventory`, `baseline` |
| Vận hành | `shipments`, `geography` |
| Marketing | `promotions`, `web_traffic` |
| Dự báo | `sample_submission` |

---

## 🔍 Key Findings

### 1. Xu hướng Doanh thu (2012–2022)

**📉 Tính mùa vụ và quy mô thu hẹp dần**
- Doanh thu tập trung mạnh vào **Quý II** (tháng 4–6), nhưng mức doanh thu tuyệt đối trong giai đoạn cao điểm **giảm rõ rệt qua các năm** — doanh nghiệp đang phụ thuộc vào một mùa bán hàng ngắn với quy mô ngày càng thu hẹp.

**📈 AOV tăng 40% nhưng tổng khách hàng giảm**
- AOV tăng từ ~22K (2013) lên ~32K (2022), tương đương **+40.44%** — nhóm khách hàng còn lại có xu hướng chi tiêu cao hơn trên mỗi đơn.
- Tuy nhiên, **số lượng khách hàng mới đạt đỉnh năm 2013 rồi giảm mạnh**; tỷ lệ quay lại trong 1–2 năm cũng suy giảm, đặc biệt sau 2018.

> 💡 **Insight:** Doanh nghiệp đang "bán ít hơn nhưng đắt hơn cho số ít khách trung thành" — mô hình không bền vững nếu không có chiến lược thu hút khách mới.

---

### 2. Hiệu quả Chiến dịch Khuyến mãi

**💸 Promo đang ăn vào lợi nhuận**
- Đơn **không promo**: Gross profit trung bình **+5K/đơn**
- Đơn **single promo**: Gross profit chuyển âm **−2K/đơn**
- Stack 2 promo có cải thiện nhẹ nhưng vẫn thấp hơn đáng kể so với không promo.

**📦 Promo không giải phóng được tồn kho**
- Tỷ lệ overstock nhóm **có promo: 78.1%** vs. không promo: **73.6%** — promo không chỉ thất bại trong việc giải phóng hàng tồn mà còn làm tình trạng tệ hơn.

**📊 Hiệu quả chiến dịch rất thấp**
- Chỉ **~6%** đợt promo đạt hiệu quả tốt
- **54%** ở mức trung bình, **40%** kém hiệu quả
- Tỷ lệ kém hiệu quả **ổn định và cao liên tục nhiều năm** — không có cải thiện theo thời gian.

**🌐 Traffic không phân biệt được hành vi promo**
- Tất cả kênh traffic đều có tỷ lệ đơn có promo **85–88%**, đơn không promo chỉ **12–14%** — promo không tạo ra khác biệt có ý nghĩa theo nguồn traffic.

> 💡 **Insight:** Cấu trúc promo hiện tại đang làm giảm profitability mà không tạo ra hiệu ứng kích cầu thực sự. Cần xem xét lại cơ chế định giá và điều kiện áp dụng promo.

---

### 3. Vận hành & Chuỗi Cung ứng

**🔄 Inventory Turnover suy giảm mạnh**
- Turnover toàn doanh nghiệp giảm từ **300.14 (2012)** xuống **66.86 (2022)** — hiệu quả giải phóng tồn kho suy giảm nghiêm trọng.
- Phân hoá rõ giữa các category: **Streetwear & Outdoor** vượt xa median (115.1), trong khi **GenZ & Casual** rất thấp.

**↩️ Overstock đi kèm rủi ro hoàn trả cao**
- Nhóm sản phẩm overstock: trung bình **110.6 lượt trả/sản phẩm**
- Nhóm bình thường: chỉ **13.7** — chênh lệch 8 lần.

**🚚 Lead-time là điểm sáng duy nhất**
- Lead-time ổn định quanh **4.5 ngày**, phần lớn đơn giao trong **7 ngày** — chỉ số vận hành tích cực nhất của toàn hệ thống.

**⭐ Lý do hoàn trả và chất lượng**
- **Wrong size: 34.7%** — lý do hoàn trả lớn nhất
- **Defective: 20.3%**, Not as described: 17.7%
- Dù đánh giá 4–5 sao chiếm >70%, tỷ lệ hoàn trả cao ở nhóm overstock cho thấy vấn đề chất lượng tiềm ẩn.

> 💡 **Insight:** Tối ưu hoá size guide và kiểm soát chất lượng trước khi nhập hàng có thể giảm đáng kể chi phí hoàn trả.

---

## 🛠️ Tech Stack

| Công cụ | Mục đích |
|---|---|
| **Python** (Pandas, NumPy) | Xử lý & phân tích dữ liệu |
| **Matplotlib, Seaborn** | Visualisation trong notebook |
| **Power BI** | Interactive dashboard |
| **Jupyter Notebook** | Môi trường phân tích |
| **GitHub** | Version control & portfolio |

---

## 🚀 Hướng dẫn chạy

```bash
# 1. Clone repo
git clone https://github.com/meiorathenais/promo-effectiveness-analysis.git
cd promo-effectiveness-analysis

# 2. Cài đặt thư viện
pip install -r requirements.txt

# 3. Chạy notebook theo thứ tự
jupyter notebook notebooks/01_eda_data_quality.ipynb
```

> Chạy notebook theo thứ tự từ `01` → `04` để đảm bảo các bước tiền xử lý được thực hiện đúng trình tự.

---

## 📊 Dashboard Preview

*(Thêm ảnh chụp màn hình Power BI vào đây sau khi export)*

```
dashboard/
├── 01_revenue_overview.png
├── 02_promo_effectiveness.png
└── 03_inventory_supply_chain.png
```

---

## 📬 Liên hệ

**[Tên của bạn]**
- 📧 Email: pthaomy3112002@gmail.com
- 💼 LinkedIn: [linkedin.com/in/phamthaomy/](https://linkedin.com/in/phamthaomy)
- 🐙 GitHub: [github.com/meiorathenais](https://github.com/meiorathenais)

---

*Project này được thực hiện như một phần của portfolio cá nhân nhằm ứng dụng kỹ năng phân tích dữ liệu vào bài toán kinh doanh thực tế.*
