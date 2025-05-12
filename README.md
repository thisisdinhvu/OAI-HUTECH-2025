Dưới đây là phiên bản viết lại cho **lưu loát, mạch lạc và trình bày chuyên nghiệp hơn**, phù hợp để đặt ở README:

---

# 🌟 OAI HUTECH 2025 – Mushroom Image Classification Challenge

Đây là repository chứa **source code giải pháp** cho cuộc thi **Mushroom Image Classification** do **Hội Tin học TP.HCM (HCA)** phối hợp với **Trường Đại học HUTECH** tổ chức.

---

## 🚀 Vòng Bán Kết (Semi-Final Solution)

### 🧪 Data Preprocessing & Augmentation

Qua quá trình quan sát dữ liệu ban đầu, nhóm nhận thấy rằng việc sử dụng trực tiếp ảnh gốc kích thước **32×32** không đem lại kết quả tối ưu trên các kiến trúc CNN. Vì vậy, chúng em áp dụng **Image Super-Resolution (ISR)** để tăng kích thước ảnh lên **64×64**, giúp mô hình học tốt hơn các đặc trưng.

<div align="center">
    <img src="https://github.com/thisisdinhvu/OAI-HUTECH-2025/blob/main/src/semi-final/ISR.png" alt="ISR Image" width="700"/>
</div> 

Bên cạnh đó, nhóm nhận thấy **class 2** bị ảnh hưởng bởi **background sặc sỡ**, làm giảm độ chính xác. Để khắc phục, với mỗi ảnh màu, chúng em tạo thêm một phiên bản **ảnh xám**, nhằm giúp mô hình tập trung vào hình dạng, đường nét nấm, giảm sự phụ thuộc vào màu nền — nhưng vẫn giữ lại ảnh màu để học thêm đặc trưng màu sắc.

<div align="center">
  <img src="https://github.com/thisisdinhvu/OAI-HUTECH-2025/blob/main/src/semi-final/COLOR-XAM.png" alt="Color vs Gray Image" width="700"/>
</div> 

---

### 🧠 Training & Evaluation

Nhóm lựa chọn mô hình **EfficientNetV2S** do nhẹ, phù hợp với tập dữ liệu nhỏ (chỉ 1400 ảnh huấn luyện từ BTC) và vẫn đạt hiệu suất tốt. Sau khi huấn luyện, kết quả đạt **91% accuracy** trên tập public test — xếp hạng **12** toàn quốc và được mời vào vòng chung kết.

Mô hình đã cải thiện đáng kể hiệu suất phân loại **class 2**, từ **90/150** lên **124/150** mẫu chính xác.

<div align="center">
  <img src="https://github.com/thisisdinhvu/OAI-HUTECH-2025/blob/main/src/semi-final/EVAL.jpg" alt="Confusion Matrix" width="700"/>
</div> 

---

## 🏆 Vòng Chung Kết (Final Solution)

### 📊 Data Preprocessing & Augmentation

Từ kinh nghiệm vòng trước, nhóm quyết định resize ảnh lên kích thước **96×96** (hoạt động tốt hơn với CNN), sử dụng **BICUBIC interpolation**. Ngoài ra, áp dụng thêm các kỹ thuật augmentation nâng cao như:

* `RandomResizedCrop`
* `RandomHorizontalFlip`
* `RandomRotation`
* `ColorJitter`
* `RandomPerspective`
* `Normalize` (trên 3 kênh RGB)

---

### 🧠 Training & Ensemble

Tại vòng chung kết, nhóm áp dụng kỹ thuật **ensemble** hai mô hình mạnh:

* `EfficientNetV2-L`
* `ConvNeXt-Large`

Hai mô hình này được dùng để **trích xuất đặc trưng**, sau đó **nối đặc trưng (concat)** lại. Thay vì dùng một lớp linear đơn giản để dự đoán, chúng em áp dụng **KAN (Kolmogorov–Arnold Networks)** để tổng hợp đặc trưng và đưa ra dự đoán chính xác hơn.

<div align="center">
  <img src="https://github.com/thisisdinhvu/OAI-HUTECH-2025/blob/main/src/final/effv2l_convL_kan_ensemble.png" alt="Model Architecture" width="700"/>
</div> 

---

### 📈 Kết quả

Mô hình đạt được **98% accuracy** và xếp **hạng 9 toàn giải** trong vòng chung kết cuộc thi.

<div align="center">
  <img src="https://github.com/thisisdinhvu/OAI-HUTECH-2025/blob/main/src/final/ranking.png" alt="Leaderboard" width="700"/>
</div> 

---

