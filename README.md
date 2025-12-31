# DỰ ĐOÁN GIÁ NHÀ TẠI CALIFORNIA
# 1.Giới thiệu đề tài

1.1 Bài toán

Bộ dữ liệu này được trích xuất từ cuộc Điều tra dân số năm 1990 của California, thường được sử dụng trong các bài toán Hồi quy (Regression) để dự đoán giá nhà trung bình.

Dự án này sử dụng các dữ liệu thống kê tổng hợp cho mỗi khối nhà (block group) để dự đoán biến mục tiêu: median_house_value (Giá trị nhà trung bình tính bằng 100,000 USD).

1.2 Mục tiêu


Thông qua bài toán này, sinh viên nhằm:

-Hiểu và vận dụng quy trình giải quyết một bài toán hồi quy thực tế

-Phân tích mối quan hệ giữa các đặc trưng đầu vào và giá nhà

-Đánh giá hiệu quả mô hình thông qua các chỉ số như RMSE và R²

2️. Giới thiệu bộ dữ liệu ( California Housing Dataset)

2.1 Nguồn dữ liệu

Bộ dữ liệu được lấy từ Kaggle:

🔗 California Housing Dataset https://www.kaggle.com/datasets/dhirajnirne/california-housing-data?utm_source=chatgpt.com

⚠️ Do dung lượng và điều khoản sử dụng của Kaggle, dữ liệu không được đưa lên GitHub. Hướng dẫn tải và sử dụng dữ liệu được trình bày trong file: data/README.md

2.2 Mô tả các thuộc tính dữ liệu

Bộ dữ liệu được trích xuất từ cuộc Điều tra Dân số California năm 1990, bao gồm các thông tin thống kê tổng hợp theo từng khối nhà (block group). Mỗi dòng dữ liệu đại diện cho một khu vực dân cư và phản ánh các đặc điểm về vị trí địa lý, nhà ở, dân số và điều kiện kinh tế – xã hội.

Bộ dữ liệu gồm 10 thuộc tính, trong đó có 9 thuộc tính đầu vào và 1 thuộc tính mục tiêu, cụ thể như sau:

Tên thuộc tính	Mô tả

longitude	Kinh độ địa lý của khu vực

latitude	Vĩ độ địa lý của khu vực

housing_median_age	Tuổi trung bình của các ngôi nhà trong khu vực

total_rooms	Tổng số phòng trong các hộ gia đình

total_bedrooms	Tổng số phòng ngủ trong các hộ gia đình

population	Tổng dân số của khu vực

households	Tổng số hộ gia đình

median_income	Thu nhập trung bình của các hộ gia đình (đã được chuẩn hóa)

median_house_value	Giá trị nhà trung bình của khu vực (đơn vị: USD)

ocean_proximity	Vị trí tương đối so với biển (biến phân loại)

Trong đó:

median_house_value là biến mục tiêu (target variable) dùng để dự đoán trong bài toán hồi quy

ocean_proximity là thuộc tính phân loại, thể hiện mức độ gần biển của khu vực (ví dụ: NEAR BAY, INLAND, NEAR OCEAN, …)

Các thuộc tính còn lại là biến số (numerical features)

Bộ dữ liệu được sử dụng phổ biến trong các bài toán học máy có giám sát, đặc biệt là bài toán hồi quy, nhằm phân tích mối quan hệ giữa các yếu tố địa lý – kinh tế – xã hội và giá trị nhà ở.
