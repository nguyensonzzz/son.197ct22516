## Mục lục

*   [Tổng quan](#tổng-quan)

*   [Mô tả Scripts và Hàm](#mô-tả-scripts-và-hàm)
    *   [Bài 1: Biến đổi Điểm và Cân bằng Histogram](#bài-1-biến-đổi-điểm-và-cân-bằng-histogram)
    *   [Bài 2: Xử lý Ảnh trong Miền Tần số](#bài-2-xử-lý-ảnh-trong-miền-tần-số)
    *   [Bài 3: Kết hợp Shuffle Kênh Màu và Lọc Tần số Ngẫu nhiên](#bài-3-kết-hợp-shuffle-kênh-màu-và-lọc-tần-số-ngẫu-nhiên)
    *   [Bài 4: Xử lý Tuần tự: Shuffle Màu, Lọc Tần số và Lọc Không gian](#bài-4-xử-lý-tuần-tự-shuffle-màu-lọc-tần-số-và-lọc-không-gian)
*   [Thư viện sử dụng](#thư-viện-sử-dụng)


## Tổng quan

Dự án này bao gồm bốn script Python, mỗi script tập trung vào các khía cạnh khác nhau của xử lý ảnh:

1.  **Bài 1**: Thực hiện các phép biến đổi cường độ cơ bản như đảo ảnh, hiệu chỉnh gamma, biến đổi log, cân bằng histogram và giãn tương phản trên một ảnh đầu vào.
2.  **Bài 2**: Áp dụng các kỹ thuật xử lý trong miền tần số, bao gồm Biến đổi Fourier Nhanh (FFT) để xem phổ biên độ, và các bộ lọc Butterworth thông thấp/thông cao. Xử lý nhiều ảnh từ một thư mục.
3.  **Bài 3**: Kết hợp việc xáo trộn (shuffle) các kênh màu RGB của ảnh, sau đó chuyển sang ảnh xám và áp dụng một bộ lọc tần số được chọn ngẫu nhiên (FFT spectrum, Butterworth low/high-pass).
4.  **Bài 4**: Mở rộng Bài 3 bằng cách thêm một bước lọc không gian (Min hoặc Max filter) sau khi đã áp dụng bộ lọc tần số cho ảnh đã được xáo trộn kênh màu và chuyển xám.

## Thư viện sử dụng
*   **NumPy (`numpy`)**:
    *   **Mục đích**: Thư viện nền tảng cho tính toán khoa học trong Python. Được sử dụng rộng rãi để làm việc với mảng đa chiều (đại diện cho ảnh), thực hiện các phép toán số học hiệu quả, và các thao tác trên ma trận.
    *   **Sử dụng trong dự án**: Biểu diễn ảnh dưới dạng mảng NumPy, thực hiện các phép tính FFT, tạo mặt nạ lọc, và các phép toán pixel.

*   **Pillow (`PIL.Image`, `PIL.ImageFilter`)**:
    *   **Mục đích**: Là một "ngã ba thân thiện" của Thư viện Ảnh Python (PIL). Nó cung cấp khả năng mở, thao tác và lưu nhiều định dạng file ảnh khác nhau. `ImageFilter` chứa các bộ lọc ảnh tích hợp sẵn.
    *   **Sử dụng trong dự án**: Đọc ảnh từ file, chuyển đổi không gian màu (ví dụ: RGB sang ảnh xám 'L'), lưu ảnh đã xử lý, xáo trộn kênh màu, và áp dụng các bộ lọc không gian như Min/Max filter (trong Bài 4).

*   **Matplotlib (`matplotlib.pyplot`)**:
    *   **Mục đích**: Thư viện vẽ đồ thị 2D toàn diện, tạo ra các hình ảnh chất lượng xuất bản ở nhiều định dạng.
    *   **Sử dụng trong dự án**: Hiển thị ảnh gốc và ảnh kết quả sau khi xử lý.

*   **OpenCV-Python (`cv2`)**:
    *   **Mục đích**: Thư viện mã nguồn mở về thị giác máy tính và học máy, cung cấp một loạt các thuật toán và công cụ.
    *   **Sử dụng trong dự án**: Chủ yếu được sử dụng trong Bài 1 cho chức năng cân bằng histogram (`cv2.equalizeHist`).

*   **os**:
    *   **Mục đích**: Module tích hợp sẵn của Python, cung cấp một cách sử dụng các chức năng phụ thuộc vào hệ điều hành như đọc hoặc ghi vào hệ thống tệp.
    *   **Sử dụng trong dự án**: Kiểm tra sự tồn tại của file/thư mục, tạo thư mục, lấy tên file từ đường dẫn.

*   **pathlib (`pathlib.Path`)**:
    *   **Mục đích**: Module tích hợp sẵn (từ Python 3.4+), cung cấp các lớp biểu diễn đường dẫn hệ thống tệp với ngữ nghĩa phù hợp cho các hệ điều hành khác nhau (cách tiếp cận hướng đối tượng hơn so với `os.path`).
    *   **Sử dụng trong dự án**: Xây dựng đường dẫn file, kiểm tra sự tồn tại, tạo thư mục, và duyệt file trong thư mục (trong Bài 2, 3, 4).

*   **random**:
    *   **Mục đích**: Module tích hợp sẵn của Python để tạo ra các số giả ngẫu nhiên.
    *   **Sử dụng trong dự án**: Xáo trộn ngẫu nhiên các kênh màu (Bài 3, 4) và chọn ngẫu nhiên một phép biến đổi từ danh sách (Bài 3, 4).

*   **typing**:
    *   **Mục đích**: Module tích hợp sẵn của Python, hỗ trợ type hints, giúp cải thiện khả năng đọc và kiểm tra tĩnh cho code.
    *   **Sử dụng trong dự án**: Khai báo kiểu dữ liệu cho các tham số hàm và giá trị trả về (ví dụ: `Callable`, `Tuple`, `List`, `np.ndarray`).
