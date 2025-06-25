
# TUẦN 1 LAP 1
# Bài Tập Xử Lý Ảnh Cơ Bản với OpenCV

Đây là bài tập các script Python sử dụng thư viện OpenCV để thực hiện một số tác vụ xử lý ảnh cơ bản. Mỗi script giải quyết một bài toán cụ thể.


## Công cụ sử dụng

*   **Python 3:** Ngôn ngữ lập trình chính.
*   **OpenCV (cv2):** Thư viện cốt lõi cho các tác vụ thị giác máy tính, bao gồm:
    *   Đọc và ghi file ảnh (PNG, JPG, JPEG, BMP).
    *   Áp dụng các bộ lọc ảnh (Trung bình, Gaussian, Trung vị).
    *   Thực hiện phát hiện biên (Canny, Sobel, Laplacian).
    *   Chuyển đổi giữa các không gian màu (ví dụ: BGR sang HSV, BGR sang Grayscale).
    *   Tách và ghép các kênh màu của ảnh.
*   **Matplotlib (pyplot):** Dùng để hiển thị hình ảnh gốc và các kết quả xử lý một cách trực quan trong các cửa sổ riêng biệt.
*   **NumPy:** Hỗ trợ các phép toán ma trận và mảng hiệu suất cao, cần thiết cho việc xử lý dữ liệu ảnh (ví dụ: xáo trộn kênh màu, các phép toán của OpenCV).
*   **Pathlib:** Cung cấp một cách làm việc với đường dẫn tệp và thư mục một cách hiện đại, dễ đọc và an toàn hơn so với module `os.path` truyền thống.


## Tuần 1

### Bài 1: Tách và lưu ảnh theo từng kênh màu (R, G, B)
*   **Mục đích:** Nạp một ảnh màu, tách thành 3 kênh màu gốc (Blue, Green, Red) và lưu mỗi kênh thành một ảnh riêng biệt. Các kênh không được chọn sẽ được tô đen.
*   **Cách hoạt động:**
    1.  Đọc ảnh đầu vào (`bird.png`).
    2.  Tách ảnh thành 3 kênh màu B, G, R.
    3.  Tạo một mảng zero có cùng kích thước với một kênh màu.
    4.  Ghép kênh Red với hai mảng zero để tạo ảnh chỉ có màu đỏ, lưu lại.
    5.  Ghép kênh Green với hai mảng zero để tạo ảnh chỉ có màu xanh lá, lưu lại.
    6.  Ghép kênh Blue với hai mảng zero để tạo ảnh chỉ có màu xanh dương, lưu lại.
*   **Kết quả:**
    *   `output_img/red_image.png`
    *   `output_img/green_image.png`
    *   `output_img/blue_image.png`

---

### Bài 2: Hoán đổi các kênh màu
*   **Mục đích:** Nạp một ảnh màu và tạo ra các ảnh mới bằng cách hoán đổi vị trí của các cặp kênh màu (ví dụ: Red và Green, Green và Blue, Blue và Red).
*   **Cách hoạt động:**
    1.  Đọc ảnh đầu vào (`bird.png`).
    2.  Tạo bản sao của ảnh gốc cho mỗi lần hoán đổi.
    3.  Hoán đổi kênh Red và Green: `img[:, :, [1, 2]] = img[:, :, [2, 1]]` (OpenCV đọc BGR, nên 2 là Red, 1 là Green). Lưu ảnh.
    4.  Hoán đổi kênh Green và Blue: `img[:, :, [0, 1]] = img[:, :, [1, 0]]` (0 là Blue, 1 là Green). Lưu ảnh.
    5.  Hoán đổi kênh Blue và Red: `img[:, :, [0, 2]] = img[:, :, [2, 0]]` (0 là Blue, 2 là Red). Lưu ảnh.
*   **Kết quả:**
    *   `output_swapped_colors/swap_rg.png`
    *   `output_swapped_colors/swap_gb.png`
    *   `output_swapped_colors/swap_br.png`

---

### Bài 3: Chuyển sang hệ màu HSV và lưu ảnh theo từng kênh (H, S, V)
*   **Mục đích:** Nạp một ảnh, chuyển đổi sang không gian màu HSV, sau đó hiển thị và lưu riêng từng kênh Hue (H), Saturation (S), và Value (V) dưới dạng ảnh màu có thể quan sát được.
*   **Cách hoạt động:**
    1.  Đọc ảnh đầu vào (`bird.png`).
    2.  Chuyển ảnh từ BGR sang HSV.
    3.  Tách thành 3 kênh H, S, V.
    4.  Để hiển thị kênh Hue: Tạo ảnh mới bằng cách giữ nguyên kênh H, đặt S và V ở giá trị tối đa (255). Chuyển ngược lại BGR và lưu.
    5.  Để hiển thị kênh Saturation: Tạo ảnh mới bằng cách giữ nguyên kênh S, đặt H ở một giá trị cố định (ví dụ 90 - màu lục lam) và V ở giá trị tối đa. Chuyển ngược lại BGR và lưu.
    6.  Để hiển thị kênh Value: Tạo ảnh mới bằng cách giữ nguyên kênh V, đặt H ở một giá trị cố định (ví dụ 90) và S ở giá trị tối đa. Chuyển ngược lại BGR và lưu.
*   **Kết quả:**
    *   `output_hsv_images/hue_channel.png`
    *   `output_hsv_images/saturation_channel.png`
    *   `output_hsv_images/value_channel.png`

---

### Bài 4: Chỉnh sửa kênh H và V trong không gian màu HSV
*   **Mục đích:** Nạp một ảnh, chuyển sang hệ màu HSV, thay đổi giá trị kênh Hue (H) thành 1/3 giá trị gốc và kênh Value (V) thành 3/4 giá trị gốc. Sau đó, lưu ảnh kết quả.
*   **Cách hoạt động:**
    1.  Đọc ảnh đầu vào (`bird.png`)
    2.  Chuyển ảnh từ BGR sang HSV
    3.  Tách thành 3 kênh H, S, V
    4.  Tính `H_new = H / 3`. Đảm bảo giá trị H_new nằm trong khoảng [0, 179] (do OpenCV quy định)
    5.  Tính `V_new = V * 0.75`. Đảm bảo giá trị V_new nằm trong khoảng [0, 255]
    6.  Giữ nguyên kênh S
    7.  Ghép các kênh H_new, S, V_new lại thành ảnh HSV mới
    8.  Chuyển ảnh HSV đã chỉnh sửa về lại BGR và lưu
*   **Kết quả:**
    *   `output_modified_hsv/modified_hsv_image.png`

---

### Bài 5: Áp dụng bộ lọc trung bình (Mean Filter) cho tất cả ảnh trong thư mục
*   **Mục đích:** Duyệt qua tất cả các file ảnh (png, jpg, jpeg, bmp) trong một thư mục gốc (và các thư mục con của nó), áp dụng bộ lọc trung bình (làm mờ) cho mỗi ảnh và lưu kết quả vào một cấu trúc thư mục tương ứng
*   **Cách hoạt động:**
    1.  Xác định thư mục đầu vào (`input_root`, mặc định là thư mục hiện tại `./`) và thư mục đầu ra (`output_root`).
    2.  Sử dụng `os.walk` để duyệt qua tất cả các file và thư mục con trong `input_root`
    3.  Với mỗi file ảnh tìm được:
        a.  Đọc ảnh
        b.  Áp dụng bộ lọc trung bình `cv2.blur()` với kích thước kernel (ví dụ: 5x5)
        c.  Tạo cấu trúc thư mục tương ứng trong `output_root`
        d.  Lưu ảnh đã lọc với tiền tố `mean_` vào thư mục đầu ra
*   **Kết quả:**
    *   Các ảnh đã được lọc sẽ được lưu trong thư mục `Exercise_mean_filtered/`, giữ nguyên cấu trúc thư mục con của thư mục đầu vào. Tên file sẽ có dạng `mean_<tên_file_gốc>`

---
## Tuần 2

### Bài 6: Lọc Ảnh (Image Filtering)

*   **Chức năng:** Áp dụng ba loại bộ lọc làm mịn/khử nhiễu cơ bản lên ảnh:
    1.  **Mean Filter (Lọc trung bình):** Làm mịn ảnh bằng cách lấy trung bình giá trị pixel trong một cửa sổ kernel
    2.  **Gaussian Filter (Lọc Gaussian):** Làm mịn ảnh bằng cách sử dụng hàm Gaussian, giảm nhiễu hiệu quả hơn Mean Filter và giữ lại các biên tốt hơn
    3.  **Median Filter (Lọc trung vị):** Loại bỏ nhiễu "muối tiêu" (salt-and-pepper noise) hiệu quả bằng cách lấy giá trị trung vị của các pixel trong cửa sổ kernel
*   **Đầu ra:** Ảnh đã lọc được lưu vào các thư mục con: `filtered_mean`, `filtered_gaussian`, `filtered_median`

### Bài 7: Phát hiện Biên (Edge Detection)

*   **Chức năng:** Sau khi khử nhiễu sơ bộ bằng Median Filter và chuyển ảnh sang thang độ xám, script áp dụng ba thuật toán phát hiện biên phổ biến:
    1.  **Canny:** Một thuật toán phát hiện biên đa giai đoạn, cho kết quả biên mảnh và liên tục
    2.  **Sobel:** Sử dụng đạo hàm bậc nhất để tìm các điểm có sự thay đổi cường độ lớn, làm nổi bật các biên ngang và dọc
    3.  **Laplacian:** Sử dụng đạo hàm bậc hai để phát hiện các vùng có sự thay đổi cường độ nhanh
*   **Đầu ra:** Ảnh chứa các biên được phát hiện được lưu vào thư mục `edge_detected_images`

### Bài 8: Xáo trộn Kênh màu RGB (RGB Channel Randomization)

*   **Chức năng:**
    1.  Khử nhiễu ảnh bằng Median Filter.
    2.  Tách ảnh BGR (Blue, Green, Red - thứ tự kênh mặc định của OpenCV) thành ba kênh màu riêng biệt
    3.  Xáo trộn thứ tự của ba kênh này một cách ngẫu nhiên
    4.  Ghép các kênh đã xáo trộn lại thành một ảnh mới, tạo ra hiệu ứng màu sắc kỳ lạ
*   **Đầu ra:** Ảnh với các kênh màu RGB đã bị xáo trộn được lưu vào thư mục `color_randomized_images`

### Bài 9: Xáo trộn Kênh màu HSV (HSV Channel Randomization)

*   **Chức năng:**
    1.  Khử nhiễu ảnh bằng Median Filter
    2.  Chuyển ảnh từ không gian màu BGR sang HSV (Hue, Saturation, Value)
    3.  Tách ảnh HSV thành ba kênh H, S, V
    4.  Xáo trộn thứ tự của ba kênh này một cách ngẫu nhiên
    5.  Ghép các kênh HSV đã xáo trộn lại và chuyển ngược ảnh về không gian màu BGR
*   **Đầu ra:** Ảnh với các kênh HSV đã bị xáo trộn (sau đó chuyển về BGR) được lưu vào thư mục `hsv_randomized_images`
<!-- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ -->
                                       # LAP2
# Mục lục
# Tổng quan

# Mô tả Scripts và Hàm

# Bài 1: Biến đổi Điểm và Cân bằng Histogram
# Bài 2: Xử lý Ảnh trong Miền Tần số
# Bài 3: Kết hợp Shuffle Kênh Màu và Lọc Tần số Ngẫu nhiên
# Bài 4: Xử lý Tuần tự: Shuffle Màu, Lọc Tần số và Lọc Không gian
# Thư viện sử dụng

# Tổng quan
# Dự án này bao gồm bốn script Python, mỗi script tập trung vào các khía cạnh khác nhau của xử lý ảnh:

# Bài 1: Thực hiện các phép biến đổi cường độ cơ bản như đảo ảnh, hiệu chỉnh gamma, biến đổi log, cân bằng histogram và giãn tương phản trên một ảnh đầu vào.
# Bài 2: Áp dụng các kỹ thuật xử lý trong miền tần số, bao gồm Biến đổi Fourier Nhanh (FFT) để xem phổ biên độ, và các bộ lọc Butterworth thông thấp/thông cao. Xử lý nhiều ảnh từ một thư mục.
# Bài 3: Kết hợp việc xáo trộn (shuffle) các kênh màu RGB của ảnh, sau đó chuyển sang ảnh xám và áp dụng một bộ lọc tần số được chọn ngẫu nhiên (FFT spectrum, Butterworth low/high-pass).
# Bài 4: Mở rộng Bài 3 bằng cách thêm một bước lọc không gian (Min hoặc Max filter) sau khi đã áp dụng bộ lọc tần số cho ảnh đã được xáo trộn kênh màu và chuyển xám.
# Thư viện sử dụng
# NumPy (numpy):

# Mục đích: Thư viện nền tảng cho tính toán khoa học trong Python. Được sử dụng rộng rãi để làm việc với mảng đa chiều (đại diện cho ảnh), thực hiện các phép toán số học hiệu quả, và các thao tác trên ma trận.
# Sử dụng trong dự án: Biểu diễn ảnh dưới dạng mảng NumPy, thực hiện các phép tính FFT, tạo mặt nạ lọc, và các phép toán pixel.
# Pillow (PIL.Image, PIL.ImageFilter):

# Mục đích: Là một "ngã ba thân thiện" của Thư viện Ảnh Python (PIL). Nó cung cấp khả năng mở, thao tác và lưu nhiều định dạng file ảnh khác nhau. ImageFilter chứa các bộ lọc ảnh tích hợp sẵn.
# Sử dụng trong dự án: Đọc ảnh từ file, chuyển đổi không gian màu (ví dụ: RGB sang ảnh xám 'L'), lưu ảnh đã xử lý, xáo trộn kênh màu, và áp dụng các bộ lọc không gian như Min/Max filter (trong Bài 4).
# Matplotlib (matplotlib.pyplot):

# Mục đích: Thư viện vẽ đồ thị 2D toàn diện, tạo ra các hình ảnh chất lượng xuất bản ở nhiều định dạng.
# Sử dụng trong dự án: Hiển thị ảnh gốc và ảnh kết quả sau khi xử lý.
# OpenCV-Python (cv2):

# Mục đích: Thư viện mã nguồn mở về thị giác máy tính và học máy, cung cấp một loạt các thuật toán và công cụ.
# Sử dụng trong dự án: Chủ yếu được sử dụng trong Bài 1 cho chức năng cân bằng histogram (cv2.equalizeHist).
# os:

# Mục đích: Module tích hợp sẵn của Python, cung cấp một cách sử dụng các chức năng phụ thuộc vào hệ điều hành như đọc hoặc ghi vào hệ thống tệp.
# Sử dụng trong dự án: Kiểm tra sự tồn tại của file/thư mục, tạo thư mục, lấy tên file từ đường dẫn.
# pathlib (pathlib.Path):

# Mục đích: Module tích hợp sẵn (từ Python 3.4+), cung cấp các lớp biểu diễn đường dẫn hệ thống tệp với ngữ nghĩa phù hợp cho các hệ điều hành khác nhau (cách tiếp cận hướng đối tượng hơn so với os.path).
# Sử dụng trong dự án: Xây dựng đường dẫn file, kiểm tra sự tồn tại, tạo thư mục, và duyệt file trong thư mục (trong Bài 2, 3, 4).
# random:

# Mục đích: Module tích hợp sẵn của Python để tạo ra các số giả ngẫu nhiên.
# Sử dụng trong dự án: Xáo trộn ngẫu nhiên các kênh màu (Bài 3, 4) và chọn ngẫu nhiên một phép biến đổi từ danh sách (Bài 3, 4).
# typing:

# Mục đích: Module tích hợp sẵn của Python, hỗ trợ type hints, giúp cải thiện khả năng đọc và kiểm tra tĩnh cho code.
# Sử dụng trong dự án: Khai báo kiểu dữ liệu cho các tham số hàm và giá trị trả về (ví dụ: Callable, Tuple, List, np.ndarray).

<!-- --------------------------------------------------------------------------------------- -->
# TUẦN 3
# Image Processing Exercises
## Công cụ và thư viện sử dụng

- **Python 3.x**: Ngôn ngữ lập trình chính.
- **OpenCV (cv2)**: Thư viện xử lý ảnh mạnh mẽ, dùng cho đọc, biến đổi, nội suy ảnh.
- **NumPy**: Xử lý ma trận và tính toán số học nhanh.
- **Matplotlib**: Hiển thị ảnh trong notebook.
- **SciPy**: Sử dụng cho nội suy ảnh trong bài 1 (map_coordinates).
- **ipywidgets**: Tạo menu tương tác trong Jupyter Notebook (bài 5).
- **os**: Quản lý file và thư mục.

---

## Mô tả các bài tập

### Bài 1: Tịnh tiến và hiệu ứng sóng trên ảnh quả kiwi
- Đọc ảnh quả kiwi.
- Tịnh tiến ảnh 50 pixel sang phải, 30 pixel xuống dưới.
- Áp dụng hiệu ứng sóng (wave effect) bằng biến đổi tọa độ với hàm sin.
- Lưu ảnh kết quả.

### Bài 2: Đổi màu gradient và ghép ảnh quả đu đủ và dưa hấu
- Đọc ảnh đu đủ và dưa hấu.
- Tạo gradient màu đỏ → xanh lá cho đu đủ, vàng → tím cho dưa hấu.
- Áp dụng gradient lên ảnh giữ hình dạng quả.
- Ghép hai quả lên nền trong suốt.
- Lưu ảnh PNG kết quả.

### Bài 3: Xoay, phản chiếu dọc và ghép ảnh núi và thuyền
- Đọc ảnh núi và thuyền.
- Resize về cùng kích thước.
- Xoay 45 độ giữ kích thước.
- Tạo hiệu ứng phản chiếu dọc.
- Ghép hai ảnh lên canvas nền trắng.
- Lưu ảnh kết quả.

### Bài 4: Phóng to và biến đổi hình học uốn cong ảnh ngôi chùa
- Đọc ảnh ngôi chùa.
- Phóng to ảnh lên 5 lần.
- Áp dụng biến đổi hình học tùy chỉnh tạo hiệu ứng uốn cong sóng ngang.
- Lưu ảnh kết quả.

### Bài 5: Menu tương tác biến đổi ảnh trong Jupyter Notebook
- Cho phép chọn 1 trong 3 ảnh mẫu.
- Chọn phép biến đổi: tịnh tiến, xoay, phóng to/thu nhỏ, làm mờ Gaussian, biến đổi sóng.
- Tùy chọn tham số biến đổi qua widget (slider, checkbox).
- Hiển thị kết quả ngay trong notebook.
- Không dùng input(), phù hợp môi trường notebook.

---

## Cách sử dụng

1. Cài đặt các thư viện cần thiết:

```bash
pip install opencv-python numpy matplotlib scipy ipywidgets
```

2. Chuẩn bị thư mục `exercise` hoặc `img` chứa các ảnh cần thiết (kiwi.jpg, papaya.png, watermelon.png, mountain.jpg, boat.jpg, pagoda.jpg,...).

3. Chạy từng notebook hoặc script tương ứng từng bài.

4. Với bài 5, chạy trong Jupyter Notebook để sử dụng menu tương tác.

---

## Mục đích chính

- Làm quen với các phép biến đổi hình học cơ bản: tịnh tiến, xoay, phóng to/thu nhỏ.
- Thực hành áp dụng hiệu ứng sóng, gradient màu sắc.
- Hiểu và sử dụng biến đổi tọa độ nội suy ảnh.
- Tạo hiệu ứng phản chiếu, ghép ảnh trên nền trong suốt hoặc nền trắng.
- Xây dựng giao diện tương tác đơn giản trong Jupyter Notebook.
- Phát triển kỹ năng xử lý ảnh thực tế với Python và OpenCV.

---



## Tài liệu tham khảo

- [OpenCV Documentation](https://docs.opencv.org/)
- [NumPy Documentation](https://numpy.org/doc/)
- [Matplotlib Documentation](https://matplotlib.org/stable/contents.html)
- [SciPy ndimage](https://docs.scipy.org/doc/scipy/reference/ndimage.html)
- [ipywidgets Documentation](https://ipywidgets.readthedocs.io/en/latest/)

