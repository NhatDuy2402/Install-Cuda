# HƯỚNG DẪN CÀI ĐẶT CUDA VÀ SỬ DỤNG GPU TRÊN WINDOWS

# 1 KIỂM TRA GPU CÓ HỖ TRỢ CUDA HAY KHÔNG
- Mở Command Prompt và chạy lệnh sau:
```bash
wmic path win32_VideoController get name
```
Ví dụ:
```
Name
NVIDIA GeForce GTX 1050
Intel(R) UHD Graphics 630
```
- Nếu tên card màn hình chứa từ khóa "NVIDIA" thì card màn hình hỗ trợ CUDA.

# 2. Tải CUDA Toolkit và cuDNN archive từ trang chủ của NVIDIA
- Cài đặt CUDA Toolkit và cuDNN theo hướng dẫn của NVIDIA.
    + CUDA Toolkit: [Version 11.6](https://developer.nvidia.com/cuda-11-6-0-download-archive)
    + cuDNN: [Version 11.x](https://developer.nvidia.com/downloads/compute/cudnn/secure/8.9.7/local_installers/11.x/cudnn-windows-x86_64-8.9.7.29_cuda11-archive.zip/)

# 3. Cài đặt CUDA Toolkit
- Chạy file cài đặt CUDA Toolkit vừa tải về.
- Chọn "Custom (Advanced)" và bỏ chọn "Visual Studio Integration".
- Chọn "Next" và chờ quá trình cài đặt hoàn tất.

# 4. Cài đặt cuDNN
1. Giải nén file cuDNN vừa tải về.
2. Copy folder vừa giải nén rồi dán vào ổ C và đổi tên thành "`cnDNN`".
3. Copy toàn bộ file trong folder `bin` của cuDNN và dán vào folder `bin` của CUDA Toolkit. Đường dẫn mặc định là `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.6\bin`.
4. Copy toàn bộ file trong folder `include` của cuDNN và dán vào folder `include` của CUDA Toolkit. Đường dẫn mặc định là `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.6\include`.
5. Copy toàn bộ file trong folder `lib` của cuDNN và dán vào folder `lib` của CUDA Toolkit. Đường dẫn mặc định là `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.6\lib`.

# 5. Cài biến môi trường
- Thêm biến môi trường CUDA vào `Path`:
    + Mở Windows tìm kiếm "Edit the system environment variables".
    + Click vào "Environment Variables".
    + Click vào "Path" trong mục "System variables" và chọn "Edit".
    + Click vào "New" và thêm đường dẫn:
        + `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.6\bin`.
        + `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.6\extras\CUPTI\libnvvp`.
    + Click vào "OK" để lưu thay đổi.

# 6. Nếu chưa cà đặt Visual Studio community thì cài đặt
- Tải Visual Studio Community từ trang chủ của Microsoft.
    + Visual Studio Community: [visualstudio.microsoft.com](https://visualstudio.microsoft.com/)
    + Chọn phiên bản Visual Studio phù hợp với hệ điều hành Windows.
- Tải gói "Desktop development with C++" trong quá trình cài đặt Visual Studio.

# 6. Cài đặt PyTorch
- Cài đặt PyTorch theo hướng dẫn trên trang chủ của PyTorch.
    + PyTorch: [pytorch.org](https://pytorch.org/get-started/locally/)
    + Chọn phiên bản PyTorch phù hợp với CUDA Toolkit đã cài đặt.
  ```bash
  pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
  ```

# 7. Kiểm tra cài đặt
- Mở Python và chạy các lệnh sau:
```python
import torch
print(torch.cuda.is_available())
print(torch.cuda.get_device_name())
```
