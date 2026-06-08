# 🇻🇳 VN AIDEOM-VN

**AI-Driven Decision Optimization Model for Vietnam**
Mô hình ra quyết định phát triển kinh tế Việt Nam trong kỉ nguyên AI.

Dashboard Streamlit mô phỏng **12 bài toán ra quyết định** trên dữ liệu thực tế của Việt Nam giai đoạn 2020–2025, kết hợp tối ưu hóa (LP, MIP, đa mục tiêu, động, ngẫu nhiên) và học tăng cường.

> **Bài tập lớn:** Các mô hình ra quyết định
> **Sinh viên:** Vũ Công Minh — **MSV:** 23051329
> Trường Đại học Kinh tế, ĐHQGHN — Viện Quản trị kinh doanh

---

## 📌 Tính năng

- **Trang chủ** — tổng quan kinh tế Việt Nam 2024–2025 và 3 bộ dữ liệu gốc (vĩ mô / 10 ngành / 6 vùng).
- **12 bài tập**, mỗi bài trình bày theo logic: **Bối cảnh → Mô hình → Dữ liệu → Tính toán → Chính sách**.
- **Tham số tương tác** riêng cho từng bài ở thanh bên (sidebar).
- **Bài 12** tích hợp 6 module (M1–M6) thành hệ thống AIDEOM-VN hoàn chỉnh.

---

## 🗂️ Danh mục 12 bài

| Cấp độ | Bài | Nội dung | Kỹ thuật chính |
|--------|-----|----------|----------------|
| **Dễ** | Bài 1 | Hàm sản xuất Cobb-Douglas mở rộng (AI, số hóa) | `numpy`, `pandas` |
| | Bài 2 | LP phân bổ ngân sách 4 hạng mục đầu tư số | `scipy.optimize`, `pulp` |
| | Bài 3 | Chỉ số ưu tiên ngành Priorityᵢ (10 ngành) | `numpy`, `pandas` |
| **Trung bình** | Bài 4 | LP phân bổ ngân sách ngành-vùng (công bằng vùng miền) | `pulp` |
| | Bài 5 | MIP lựa chọn 15 dự án chuyển đổi số | `pulp` (CBC) |
| | Bài 6 | TOPSIS xếp hạng 6 vùng (Expert / Entropy / AHP) | `numpy` |
| **Khá khó** | Bài 7 | NSGA-II tối ưu 4 mục tiêu Pareto | `pymoo` |
| | Bài 8 | Tối ưu động liên thời gian 2026–2035 | `scipy.optimize` (SLSQP) |
| | Bài 9 | Tác động AI tới lao động (NetJob ròng) | `scipy.optimize` |
| **Khó** | Bài 10 | Quy hoạch ngẫu nhiên 2 giai đoạn (VSS, EVPI, robust) | `pyomo` + HiGHS |
| | Bài 11 | Q-learning chính sách kinh tế thích nghi (MDP 81 trạng thái) | `numpy` |
| | Bài 12 | Đồ án tích hợp AIDEOM-VN: 6 module, 5 kịch bản | `streamlit`, `matplotlib` |

---

## 📁 Cấu trúc thư mục

```
.
├── app.py                          # Ứng dụng Streamlit (toàn bộ 12 bài)
├── requirements.txt                # Danh sách thư viện
├── README.md                       # File này
├── vietnam_macro_2020_2025.csv     # Dữ liệu vĩ mô 2020–2025
├── vietnam_sectors_2024.csv        # Dữ liệu 10 ngành 2024
└── vietnam_regions_2024.csv        # Dữ liệu 6 vùng KT-XH 2024
```

> ⚠️ **Quan trọng:** 3 tệp CSV phải nằm **cùng thư mục** với `app.py` (app tự tìm trong thư mục hiện tại, `data/`, hoặc đường dẫn upload).

---

## 🚀 Cách 1 — Chạy trên máy (local)

Yêu cầu: **Python 3.10–3.12**

```bash
# 1. (Khuyến nghị) tạo môi trường ảo
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate

# 2. Cài thư viện
pip install -r requirements.txt

# 3. Chạy dashboard
streamlit run app.py
```

Ứng dụng mở tại `http://localhost:8501`.

---

## ☁️ Cách 2 — Deploy lên Streamlit Community Cloud (miễn phí)

1. **Tạo repository GitHub** và đẩy đủ 5 tệp lên (giữ nguyên cấu trúc thư mục ở trên):
   ```bash
   git init
   git add app.py requirements.txt README.md vietnam_*.csv
   git commit -m "AIDEOM-VN Streamlit app"
   git branch -M main
   git remote add origin https://github.com/<tên-bạn>/<tên-repo>.git
   git push -u origin main
   ```

2. Truy cập **https://share.streamlit.io** → đăng nhập bằng GitHub.

3. Bấm **"Create app"** → **"Deploy a public app from GitHub"** và điền:
   - **Repository:** `<tên-bạn>/<tên-repo>`
   - **Branch:** `main`
   - **Main file path:** `app.py`

4. Bấm **Deploy**. Lần đầu mất 3–5 phút để cài thư viện. Sau đó app có URL công khai dạng
   `https://<tên-repo>.streamlit.app`.

**Lưu ý khi deploy:**
- Mỗi lần `git push` lên branch `main`, Streamlit Cloud **tự build lại** app.
- Các bài nặng (Bài 7 NSGA-II, Bài 8 tối ưu động, Bài 11 Q-learning) dùng cache nên lần mở đầu tiên mất vài giây, sau đó nhanh.
- Bài 10 cần solver `highspy` (đã có trong `requirements.txt`). Nếu cloud không cài được, trang Bài 10 vẫn hiển thị kết quả tham chiếu thay vì làm sập app.

---

## 📊 Nguồn dữ liệu

Cục Thống kê quốc gia (NSO/GSO), Bộ Khoa học và Công nghệ (MoST), Bộ Thông tin và Truyền thông (MIC),
Bộ Kế hoạch và Đầu tư (MPI), World Bank, và báo cáo Global Innovation Index 2025 (WIPO).

*Lưu ý: số liệu trong CSV được làm tròn phục vụ mục đích học tập.*

---

## 📦 Thư viện sử dụng

`streamlit` · `numpy` · `pandas` · `scipy` · `matplotlib` · `pulp` · `pymoo` · `pyomo` · `highspy`

---

## 📄 Giấy phép

Dự án phục vụ mục đích học tập (bài tập lớn học phần Các mô hình ra quyết định).
