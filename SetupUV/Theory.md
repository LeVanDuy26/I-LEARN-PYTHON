# 🚀 Python Project Workflow với **uv**

Đây là hướng dẫn chuẩn để khởi tạo và quản lý dự án Python mới bằng công cụ **uv** (thay thế `venv`, `pip`, `pip-tools`).

---

## 🔧 BƯỚC 1: Tạo thư mục dự án

```powershell
mkdir ten_project
cd ten_project
````

Ví dụ:

```powershell
mkdir uv_demo
cd uv_demo
```

---

## 🌱 BƯỚC 2: Tạo môi trường ảo

```powershell
uv venv
```

* Mặc định sẽ tạo thư mục `.venv/`.
* Nếu muốn đặt tên khác, dùng:

```powershell
uv venv myenv
```

---

## ⚡ BƯỚC 3: Kích hoạt môi trường ảo

### Trên PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
```

### Trên CMD:

```cmd
.venv\Scripts\activate.bat
```

> ⚠️ Nếu gặp lỗi quyền, chạy:
>
> ```powershell
> Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope Process
> ```

---

## 📦 BƯỚC 4: Cài đặt thư viện cần thiết

Ví dụ:

```powershell
uv pip install requests pandas numpy matplotlib
```

---

## 📝 BƯỚC 5: Lưu danh sách thư viện

Tạo file `requirements.txt`:

```powershell
uv pip freeze > requirements.txt
```

---

## 🧠 BƯỚC 6: Mở dự án trong VS Code

```powershell
code .
```

> Chọn đúng interpreter:
> **Python: Select Interpreter** → chọn `.venv`.

---

## ❌ BƯỚC 7: Dừng môi trường ảo

```powershell
deactivate
```

---

## ♻️ BƯỚC 8: Khôi phục môi trường từ `requirements.txt`

Dùng khi clone project hoặc setup lại:

```powershell
uv venv
.\.venv\Scripts\Activate.ps1
uv pip install -r requirements.txt
```

---

## 🔍 Lưu ý khi dùng `uv`

| Trường hợp                   | Có nên `deactivate` không? |
| ---------------------------- | -------------------------- |
| ✔ Đã làm xong project        | ✅ Có                       |
| ✔ Chuyển sang project khác   | ✅ Có                       |
| ✘ Vẫn đang làm, chưa xong    | ❌ Không bắt buộc           |
| ✔ Tắt máy hoặc đóng terminal | ✅ Nên dừng hoặc auto dừng  |

* `uv` nhanh hơn nhiều so với pip, đặc biệt khi cài gói nặng.
* Có thể chạy trực tiếp code + auto cài package (không cần activate):

  ```powershell
  uv run python main.py
  ```

---

## 📓 Cài thêm thư viện trong Jupyter Notebook

Trong notebook, dùng `!` để gọi `uv pip` thay vì pip:

```python
!uv pip install seaborn
```

Hoặc nhiều package cùng lúc:

```python
!uv pip install scikit-learn xgboost lightgbm
```

👉 Thư viện sẽ được cài trực tiếp vào môi trường `.venv` mà notebook đang dùng.

---

## 🔚 Tổng kết

* `uv` thay thế toàn bộ **venv + pip + pip-tools**.
* Quy trình tạo môi trường → cài package → lưu requirements → khôi phục lại dễ dàng hơn pip.
* Workflow này áp dụng chuẩn cho mọi project Python mới.