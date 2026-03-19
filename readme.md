# 🌦️ Rain forecast using Big Data Analytics
Dự án phân tích dữ liệu lớn nhằm mục đích dự báo khả năng có mưa dựa trên các chỉ số thời tiết đa chiều. Dự án giải quyết bài toán xử lý tập dữ liệu có quy mô rất lớn (hơn 16 triệu dòng) bằng việc ứng dụng hệ thống tính toán phân tán **PySpark**, đồng thời xây dựng quy trình tiền xử lý (ETL pipeline) và kỹ nghệ đặc trưng (Feature Engineering) để tối ưu hóa cho các mô hình Học máy.
---

## 🚀 Công nghệ và Thư viện (Tech Stack)
- **Xử lý Big Data:** Apache Spark, PySpark (tối ưu hóa phân vùng và bộ nhớ với Spark DataFrame)
- **Ngôn ngữ & Môi trường:** Python 3.10, Java 17 (OpenJDK), JupyterLab
- **Phân tích & Học máy:** Pandas, Numpy, Scikit-learn, Imbalanced-learn

---

## 🧠 Quy trình Xử lý Dữ liệu (Data Pipeline)
Dữ liệu thô ban đầu bao gồm các thông tin chi tiết về khí hậu như: lượng mưa, áp suất khí quyển, nhiệt độ, độ ẩm, và tốc độ gió. Quy trình ETL được chia thành 4 bước tự động hóa chặt chẽ:

1. **Chuẩn hóa Dữ liệu (Data Cleaning):** - Đồng bộ hóa tên các đặc trưng đầu vào.
   - Trích xuất và định dạng lại các biến thời gian (Ngày, Tháng, Năm, Giờ) để phục vụ cho các phân tích theo mùa vụ.
2. **Xử lý Dữ liệu Khuyết (Handling Missing Values):**
   - Lọc và loại bỏ các ngày bị nhiễu hoàn toàn (hoàn toàn không có dữ liệu đo đạc).
   - Áp dụng các kỹ thuật nội suy chuỗi thời gian như `Forward Fill` (kéo giá trị quá khứ) và `Backward Fill` (lấy giá trị tương lai) thông qua `Window Functions` của Spark để đảm bảo tính liên tục của dữ liệu.
3. **Gán Nhãn Khách Quan (Labeling):**
   - Tính toán nhãn phân loại `rain_label` (1 = Có mưa, 0 = Không mưa) một cách tự động dựa trên lượng mưa thực tế (`prcp > 0`).
4. **Kỹ nghệ Đặc trưng (Feature Engineering):**
   - **Mã hóa chu kỳ thời gian (Cyclical Encoding):** Chuyển đổi các biến thời gian (Tháng, Giờ) thành các tọa độ hình học `sin` và `cos`. Điều này giúp mô hình Học máy nhận diện được tính chu kỳ của các hiện tượng thời tiết (ví dụ: tháng 12 và tháng 1 liền kề nhau) và giảm thiểu rủi ro quá khớp (overfitting).
   - Loại bỏ các đặc trưng định danh dư thừa để tinh gọn kích thước tập dữ liệu.

*Kết quả:* Tập dữ liệu sạch cuối cùng bao gồm 26 biến đặc trưng (Features) có giá trị cao nhất.

---

## 🛠️ Hướng dẫn Cài đặt (Installation)

Môi trường phát triển yêu cầu hệ điều hành Linux/Ubuntu. Vui lòng chạy các lệnh sau để thiết lập môi trường ảo và cài đặt các dependencies cần thiết:

```bash
python3 -m venv btl_env
source btl_env/bin/activate
sudo apt update
sudo apt install openjdk-17-jdk -y
export JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
export PATH=$JAVA_HOME/bin:$PATH

pip install pyspark

sudo apt install python3.10 python3.10-venv python3.10-dev
pip install pandas numpy scikit-learn imbalanced-learn
pip install --upgrade pip

pip install jupyterlab