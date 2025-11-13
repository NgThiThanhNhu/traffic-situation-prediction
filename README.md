# traffic-situation-prediction
# Dự đoán Tình Trạng Giao Thông bằng Học Máy

## Giới thiệu
Đề tài tập trung vào **dự đoán tình trạng giao thông** (Traffic Situation Prediction) dựa trên dữ liệu ghi nhận thực tế gồm nhiều loại phương tiện qua từng khung giờ trong ngày.  
Mục tiêu là **xây dựng và so sánh nhiều mô hình học máy** nhằm dự đoán tình trạng giao thông (*low, normal, high, heavy...*) dựa vào số lượng xe cộ và thời gian trong ngày.

---

## Mô tả bộ dữ liệu

Bộ dữ liệu **`TrafficTwoMonth.csv`** gồm thông tin thu thập trong 2 tháng về lưu lượng giao thông, được ghi nhận theo từng khung thời gian 15 phút.

| Cột | Mô tả |
|-----|--------|
| **Time** | Thời gian ghi nhận (theo từng 15 phút) |
| **Date** | Ngày trong tháng |
| **Day of the week** | Thứ trong tuần (Monday, Tuesday, …) |
| **CarCount** | Số lượng ô tô được ghi nhận |
| **BikeCount** | Số lượng xe máy |
| **BusCount** | Số lượng xe buýt |
| **TruckCount** | Số lượng xe tải |
| **Total** | Tổng số phương tiện (tổng 4 loại trên) |
| **Traffic Situation** | Nhãn phân loại tình trạng giao thông (*low, normal, high, heavy, …*) — đây là **biến mục tiêu** cần dự đoán |

**Ví dụ mẫu dữ liệu:**

| Time | Date | Day of the week | CarCount | BikeCount | BusCount | TruckCount | Total | Traffic Situation |
|------|------|----------------|-----------|------------|-----------|-------------|--------|--------------------|
| 12:00:00 AM | 10 | Tuesday | 13 | 2 | 2 | 24 | 41 | normal |
| 4:00:00 AM | 10 | Tuesday | 82 | 7 | 3 | 10 | 102 | low |
| 4:30:00 AM | 10 | Tuesday | 89 | 10 | 2 | 10 | 111 | low |

---

## Các mô hình học máy sử dụng

| STT | Mô hình | Thư viện | Mô tả ngắn |
|-----|----------|-----------|------------|
| 1 | **Logistic Regression** | `scikit-learn` | Mô hình tuyến tính, dùng làm baseline |
| 2 | **Naive Bayes** | `GaussianNB` | Dựa trên xác suất Bayes, nhanh và đơn giản |
| 3 | **Decision Tree** | `DecisionTreeClassifier` | Phân loại bằng cách chia nhỏ dữ liệu theo thuộc tính |
| 4 | **Random Forest** | `RandomForestClassifier` | Trung bình kết quả của nhiều cây để tăng độ chính xác |
| 5 | **Gradient Boosting** | `GradientBoostingClassifier` | Học nối tiếp nhiều mô hình yếu để cải thiện kết quả |
| 6 | **AdaBoost** | `AdaBoostClassifier` | Boosting đơn giản, hiệu quả tốt |
| 7 | **Artificial Neural Network (ANN)** | `TensorFlow / Keras` | Mô hình phi tuyến học sâu, phù hợp cho dữ liệu phức tạp |

---

## Quy trình thực hiện

1. **Tiền xử lý dữ liệu**
   - Xử lý giá trị thiếu (nếu có)
   - Mã hóa dữ liệu phân loại (`Day of the week`, `Traffic Situation`)
   - Chuẩn hóa dữ liệu đầu vào (`StandardScaler` hoặc `MinMaxScaler`)

2. **Chia tập dữ liệu**
   - `train_test_split` (ví dụ: 80% train, 20% test)

3. **Huấn luyện mô hình**
   - Triển khai 7 mô hình kể trên
   - Tinh chỉnh siêu tham số (hyperparameters)

4. **Đánh giá mô hình**
   - Dựa trên các chỉ số:
     - `Accuracy`
     - `Precision`, `Recall`, `F1-score`
     - `Confusion Matrix`

5. **So sánh kết quả**
   - Đưa ra mô hình cho hiệu năng tốt nhất
   - Phân tích ưu – nhược điểm của từng mô hình

---

## Kết quả minh họa (ví dụ)

| Mô hình | Accuracy (%) | F1-score | Nhận xét |
|----------|---------------|----------|-----------|
| Logistic Regression | 82.5 | 0.81 | Cơ bản, nhanh |
| Naive Bayes | 78.9 | 0.77 | Giả định độc lập chưa phù hợp hoàn toàn |
| Decision Tree | 85.2 | 0.84 | Dễ hiểu nhưng dễ overfit |
| Random Forest | 88.6 | 0.87 | Ổn định, chính xác cao |
| Gradient Boosting | 89.1 | 0.88 | Hiệu quả, học chậm hơn |
| AdaBoost | 87.4 | 0.86 | Boosting đơn giản, kết quả tốt |
| ANN | **90.3** | **0.89** | Hiệu năng cao nhất |

---

## Thư viện sử dụng
- `pandas`, `numpy` – xử lý dữ liệu  
- `matplotlib`, `seaborn` – trực quan hóa  
- `scikit-learn` – huấn luyện mô hình học máy  
- `tensorflow`, `keras` – xây dựng mạng nơ-ron nhân tạo  
- `jupyter notebook` – môi trường thực thi và trình bày kết quả  

---

## Kết luận
- Dữ liệu giao thông có thể dự đoán hiệu quả bằng nhiều mô hình học máy khác nhau.  
- Các mô hình **Boosting** và **ANN** cho kết quả chính xác cao nhất.  
- Biến thời gian (*Time*) và tổng phương tiện (*Total*) có ảnh hưởng lớn đến dự đoán.  

---

> **Trường:** [Điền tên trường bạn nếu muốn]  
> 📅 **Thời gian thực hiện:** Học kỳ I – Năm học 2025  

---


