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

# 2️. Giới thiệu bộ dữ liệu ( California Housing Dataset)

2.1 Nguồn dữ liệu

Bộ dữ liệu được lấy từ Kaggle:

🔗 California Housing Dataset https://www.kaggle.com/datasets/dhirajnirne/california-housing-data?utm_source=chatgpt.com

⚠️ Do dung lượng và điều khoản sử dụng của Kaggle, dữ liệu không được đưa lên GitHub. Hướng dẫn tải và sử dụng dữ liệu được trình bày trong file: data/README.md

2.2 Mô tả các thuộc tính dữ liệu

Bộ dữ liệu được trích xuất từ cuộc Điều tra Dân số California năm 1990, bao gồm các thông tin thống kê tổng hợp theo từng khối nhà (block group). Mỗi dòng dữ liệu đại diện cho một khu vực dân cư và phản ánh các đặc điểm về vị trí địa lý, nhà ở, dân số và điều kiện kinh tế – xã hội.

Bộ dữ liệu gồm 10 thuộc tính, trong đó có 9 thuộc tính đầu vào và 1 thuộc tính mục tiêu, cụ thể như sau:

Tên thuộc tính:	Mô tả

-longitude:	Kinh độ địa lý của khu vực

-latitude:	Vĩ độ địa lý của khu vực

-housing_median_age:	Tuổi trung bình của các ngôi nhà trong khu vực

-total_rooms:	Tổng số phòng trong các hộ gia đình

-total_bedrooms:	Tổng số phòng ngủ trong các hộ gia đình

-population:	Tổng dân số của khu vực

-households:	Tổng số hộ gia đình

-median_income:	Thu nhập trung bình của các hộ gia đình (đã được chuẩn hóa)

-median_house_value:	Giá trị nhà trung bình của khu vực (đơn vị: USD)

-ocean_proximity:	Vị trí tương đối so với biển (biến phân loại)

Trong đó:

-median_house_value là biến mục tiêu (target variable) dùng để dự đoán trong bài toán hồi quy

-ocean_proximity là thuộc tính phân loại, thể hiện mức độ gần biển của khu vực (ví dụ: NEAR BAY, INLAND, NEAR OCEAN, …)

-Các thuộc tính còn lại là biến số (numerical features)

Bộ dữ liệu được sử dụng phổ biến trong các bài toán học máy có giám sát, đặc biệt là bài toán hồi quy, nhằm phân tích mối quan hệ giữa các yếu tố địa lý – kinh tế – xã hội và giá trị nhà ở.

# 3️. Tiền xử lý dữ liệu

Trước khi tiến hành huấn luyện các mô hình hồi quy (Linear Regression, SVR và Random Forest), bộ dữ liệu cần được tiền xử lý nhằm đảm bảo chất lượng dữ liệu, cải thiện hiệu quả huấn luyện và độ chính xác của mô hình. Các bước tiền xử lý được thực hiện như sau:

3.1. Kiểm tra và xử lý dữ liệu thiếu

Trong bộ dữ liệu California Housing, một số giá trị có thể bị thiếu, đặc biệt là thuộc tính total_bedrooms.
Để xử lý vấn đề này, phương pháp thay thế bằng giá trị trung bình (mean imputation) được sử dụng nhằm:

Giữ nguyên số lượng mẫu dữ liệu

Hạn chế ảnh hưởng tiêu cực đến phân phối dữ liệu

3.2. Tách biến đầu vào và biến mục tiêu

Biến đầu vào (X): bao gồm các thuộc tính địa lý, dân số, nhà ở và kinh tế – xã hội

Biến mục tiêu (y): median_house_value

Việc tách riêng biến mục tiêu giúp mô hình học được mối quan hệ giữa các đặc trưng đầu vào và giá nhà.

3.3. Xử lý biến phân loại ocean_proximity

Thuộc tính ocean_proximity là biến phân loại, không thể đưa trực tiếp vào các mô hình hồi quy.

Do đó, dữ liệu được mã hóa bằng phương pháp One-Hot Encoding, chuyển mỗi giá trị phân loại thành một vector nhị phân.

Cách tiếp cận này giúp mô hình:

Không áp đặt quan hệ thứ tự giả giữa các nhãn

Khai thác thông tin vị trí tương đối so với biển một cách hiệu quả

3.4. Chuẩn hóa dữ liệu (Feature Scaling)

Các thuộc tính số có thang đo rất khác nhau (ví dụ: median_income chỉ vài đơn vị, trong khi population có thể lên đến hàng nghìn).

Vì vậy, dữ liệu được chuẩn hóa (Standardization) để đưa về cùng thang đo với:

Trung bình bằng 0

Độ lệch chuẩn bằng 1

Bước này đặc biệt quan trọng đối với SVR và Linear Regression, giúp:

Tăng tốc độ hội tụ

Tránh hiện tượng đặc trưng có giá trị lớn chi phối mô hình

Lưu ý: Đối với Random Forest, việc chuẩn hóa không bắt buộc, tuy nhiên vẫn được thực hiện để đảm bảo tính nhất quán khi so sánh các mô hình.

3.5. Chia tập dữ liệu huấn luyện và kiểm tra

Dữ liệu được chia thành:

Tập huấn luyện (Training set): dùng để huấn luyện mô hình

Tập kiểm tra (Test set): dùng để đánh giá hiệu quả dự đoán

Việc chia dữ liệu giúp đánh giá khả năng tổng quát hóa (generalization) của mô hình trên dữ liệu chưa từng thấy.

3.6. Kiểm tra và xử lý ngoại lai (nếu có)

Một số thuộc tính như total_rooms, population có thể chứa các giá trị ngoại lai.

Việc phân tích phân phối dữ liệu (thông qua biểu đồ hoặc thống kê) được thực hiện để:

Xác định các giá trị bất thường

Đánh giá mức độ ảnh hưởng của ngoại lai đến mô hình

# 4️. Pipeline huấn luyện & dự đoán

Pipeline huấn luyện và dự đoán được xây dựng nhằm đảm bảo tính nhất quán, khả năng tái sử dụng và tránh rò rỉ dữ liệu (data leakage) trong toàn bộ quá trình xử lý và huấn luyện mô hình. Pipeline bao gồm các bước chính như sau:

Bước 1: Thu thập và làm sạch dữ liệu

Dữ liệu thô được nạp từ bộ dữ liệu California Housing, sau đó tiến hành:

Kiểm tra giá trị thiếu

Xử lý dữ liệu không hợp lệ

Chuẩn hóa định dạng dữ liệu

Bước 2: Tiền xử lý dữ liệu

Các bước tiền xử lý được áp dụng đồng nhất cho cả quá trình huấn luyện và dự đoán, bao gồm:

Điền giá trị thiếu cho các thuộc tính số

Mã hóa biến phân loại ocean_proximity bằng One-Hot Encoding

Chuẩn hóa các thuộc tính số bằng Standardization

Các bước này được tích hợp trực tiếp vào pipeline nhằm đảm bảo dữ liệu đầu vào luôn được xử lý theo cùng một quy trình.

Bước 3: Chia tập dữ liệu

Dữ liệu được chia thành:

Tập huấn luyện (Training set): dùng để học tham số mô hình

Tập kiểm tra (Test set): dùng để đánh giá hiệu năng mô hình

Việc chia dữ liệu giúp kiểm tra khả năng tổng quát hóa của mô hình.

Bước 4: Huấn luyện mô hình

Ba mô hình hồi quy được huấn luyện độc lập trong pipeline:

Linear Regression

Support Vector Regression (SVR)

Random Forest Regression

Mỗi mô hình được huấn luyện trên cùng tập dữ liệu đã tiền xử lý để đảm bảo tính công bằng trong so sánh.

Bước 5: Dự đoán

Sau khi huấn luyện, mô hình được sử dụng để:

Dự đoán giá trị median_house_value trên tập kiểm tra

So sánh giá trị dự đoán với giá trị thực tế

Bước 6: Đánh giá mô hình

Hiệu năng của các mô hình được đánh giá thông qua các chỉ số:

Root Mean Squared Error (RMSE)

Hệ số xác định R²

Các chỉ số này được sử dụng để lựa chọn mô hình dự đoán hiệu quả nhất.

5. Mô hình sử dụng

Trong nghiên cứu này, ba mô hình học máy có giám sát thuộc nhóm hồi quy (Regression) được lựa chọn để huấn luyện và so sánh hiệu quả dự đoán giá trị nhà trung bình (median_house_value). Các mô hình bao gồm:

5.1. Linear Regression

Hồi quy tuyến tính là mô hình cơ sở, giả định mối quan hệ tuyến tính giữa các biến đầu vào và biến mục tiêu. Mô hình tìm hàm tuyến tính tối ưu nhằm giảm thiểu sai số giữa giá trị dự đoán và giá trị thực tế.

Ưu điểm:

Dễ triển khai và diễn giải

Tốc độ huấn luyện nhanh

Phù hợp làm mô hình baseline

Hạn chế:

Khó mô hình hóa quan hệ phi tuyến

Nhạy cảm với ngoại lai và đa cộng tuyến

5.2. Support Vector Regression (SVR)

SVR là phần mở rộng của Support Vector Machine cho bài toán hồi quy. Mô hình tìm hàm dự đoán sao cho sai số nằm trong một ngưỡng ε cho phép và tối đa hóa biên an toàn.

Ưu điểm:

Khả năng học quan hệ phi tuyến thông qua kernel (ví dụ: RBF)

Hiệu quả với dữ liệu có chiều cao

Hạn chế:

Nhạy cảm với việc lựa chọn tham số

Chi phí tính toán cao với tập dữ liệu lớn

5.3. Random Forest Regression

Random Forest là mô hình tổ hợp, xây dựng nhiều cây quyết định hồi quy trên các tập dữ liệu con khác nhau và tổng hợp kết quả dự đoán.

Ưu điểm:

Xử lý tốt dữ liệu phi tuyến và tương tác đặc trưng

Ít bị overfitting hơn so với cây quyết định đơn lẻ

Ít yêu cầu tiền xử lý dữ liệu

Hạn chế:

Khó diễn giải

Tốn tài nguyên tính toán

5.4. Lý do lựa chọn mô hình

Việc sử dụng ba mô hình với mức độ phức tạp khác nhau nhằm:

So sánh hiệu quả giữa mô hình tuyến tính và phi tuyến

Đánh giá khả năng học đặc trưng của từng mô hình

Lựa chọn mô hình phù hợp nhất cho bài toán dự đoán giá nhà

# 6. Đánh giá mô hình

Hiệu năng của các mô hình hồi quy được đánh giá thông qua hai chỉ số chính là RMSE và R².

RMSE đo lường mức độ sai lệch trung bình giữa giá trị dự đoán và giá trị thực tế, trong đó giá trị RMSE càng nhỏ thì mô hình dự đoán càng chính xác.

R² thể hiện mức độ giải thích của mô hình đối với sự biến thiên của biến mục tiêu; giá trị R² càng gần 1 cho thấy mô hình càng phù hợp với dữ liệu.

Các mô hình được so sánh và lựa chọn dựa trên tiêu chí RMSE thấp nhất và R² cao nhất.
