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

