# Studio AI — Photo Lab (GitHub Pages)

Ứng dụng chỉnh ảnh chân dung chạy hoàn toàn trong trình duyệt. Không có backend; ảnh người dùng không được gửi lên máy chủ ứng dụng.

## Chức năng
- Tải ảnh JPG/PNG/WebP và xem trước.
- Tách nền AI bằng `@imgly/background-removal` (mô hình tải theo yêu cầu).
- Sửa mặt nạ bằng cọ xóa/giữ; đảo mask; hoàn tác.
- Thay màu nền, gradient, nền trong suốt.
- Mô phỏng ánh sáng studio bằng Canvas.
- AI super-resolution 2× bằng Swin2SR qua Transformers.js.
- Xuất PNG/JPG/WebP.

## Chạy thử
Do dùng JavaScript module, hãy mở bằng một web server cục bộ (không mở trực tiếp `file://`).

Ví dụ:
```bash
python -m http.server 8000
```
Sau đó mở `http://localhost:8000`.

## Triển khai GitHub Pages
1. Tạo repository mới trên GitHub.
2. Tải `index.html` và `README.md` lên nhánh `main` (root).
3. Vào **Settings → Pages**.
4. Trong **Build and deployment**, chọn **Deploy from a branch**.
5. Chọn branch `main`, folder `/ (root)`, nhấn Save.
6. Chờ GitHub tạo địa chỉ Pages.

## Yêu cầu trình duyệt
- Khuyến nghị Chrome hoặc Edge phiên bản mới trên máy tính.
- Kết nối Internet để tải thư viện và mô hình ở lần sử dụng đầu.
- Tách nền AI và super-resolution có thể tiêu thụ RAM/GPU đáng kể; nên thử ảnh vừa phải trước.
- Trên thiết bị không hỗ trợ WebGPU, thư viện có thể dùng CPU/WASM nếu runtime hỗ trợ; tốc độ sẽ thấp hơn.

## Lưu ý quan trọng về chất lượng
- AI tách nền là mô hình tổng quát, có thể nhầm tóc, vật thể trong suốt hoặc nền phức tạp. Dùng cọ để sửa mask.
- Công cụ ánh sáng trong bản này là mô phỏng hậu kỳ bằng gradient Canvas, chưa phải relighting AI như IC-Light.
- Super-resolution Swin2SR 2× là mô hình AI có thể tái tạo chi tiết dự đoán; cần kiểm tra mắt, da, chữ và chi tiết quan trọng sau khi xử lý.
- Bộ lọc “Làm rõ” là tinh chỉnh hậu kỳ nhẹ, không thay thế AI super-resolution.
- Phiên bản này chưa có SAM/GrabCut interactive segmentation; cọ thủ công trực tiếp trên mask là phương án dự phòng đang hoạt động.

## Thư viện và giấy phép bên thứ ba
- `@imgly/background-removal`: AGPL-3.0. Nếu triển khai/phân phối ứng dụng dùng thư viện này, cần đọc và tuân thủ đầy đủ AGPL-3.0, bao gồm nghĩa vụ cung cấp mã nguồn tương ứng trong các trường hợp áp dụng. Xem: https://github.com/imgly/background-removal-js
- `@huggingface/transformers`: Apache-2.0. Xem: https://github.com/huggingface/transformers.js
- Mô hình Swin2SR: xem thẻ mô hình và giấy phép của repository mô hình: https://huggingface.co/Xenova/swin2SR-classical-sr-x2-64

Đây là bản nền có thể triển khai và mở rộng. Kiểm tra lại giấy phép thư viện/mô hình trước khi dùng cho mục đích thương mại.
