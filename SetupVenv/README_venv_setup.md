# Hướng dẫn thiết lập môi trường ảo Python (venv) cho dự án

## 🔧 BƯỚC 1: Tạo thư mục dự án

```powershell
mkdir ten_project
cd ten_project
```

Ví dụ:

```powershell
mkdir ven_demo
cd ven_demo
```

---

## 🌱 BƯỚC 2: Tạo môi trường ảo

```powershell
python -m venv venv
```

- `venv`: tên thư mục chứa môi trường ảo (có thể đổi).
- Sau khi chạy sẽ có thư mục `venv/` xuất hiện.

---

## ⚡ BƯỚC 3: Kích hoạt môi trường ảo

### PowerShell:

```powershell
.\venv\Scripts\Activate.ps1
```
"python -m pip install --upgrade pip"
### CMD:

```cmd
venv\Scripts\activate.bat
```

> Nếu lỗi quyền, chạy:  
> ```powershell
> Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope Process
> ```

---

## 📦 BƯỚC 4: Cài đặt thư viện trong môi trường ảo

Ví dụ:

```powershell
pip install requests pandas numpy matplotlib

```

---

## 📝 BƯỚC 5: Lưu danh sách thư viện

```powershell
pip freeze > requirements.txt
```

---

## 🧠 BƯỚC 6: Mở dự án trong VS Code

```powershell
code .
```

> Chọn đúng interpreter: `Python: Select Interpreter` > chọn đường dẫn trong `venv`.

---

## ❌ BƯỚC 7: Dừng môi trường ảo

```powershell
deactivate
```

---

## ♻️ BƯỚC 8: Khôi phục môi trường từ file `requirements.txt`

```powershell
python -m venv venv
.\venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

---

## 🔍 Lưu ý khi sử dụng `venv`

| Trường hợp                           | Có nên `deactivate` không? |
|--------------------------------------|-----------------------------|
| ✔ Đã làm xong project                | ✅ Có, nên dừng lại         |
| ✔ Chuyển sang project khác           | ✅ Có, nên dừng lại         |
| ✘ Vẫn đang làm, chưa xong            | ❌ Không bắt buộc dừng      |
| ✔ Tắt máy hoặc đóng terminal         | ✅ Nên dừng hoặc nó tự dừng |

- Không deactivate vẫn chạy được bình thường, nhưng dễ gây nhầm nếu dùng nhiều dự án.
- Nếu deactivate khi đang làm dở, chỉ cần activate lại, không bị mất gì cả.

---

## 🔚 Tổng kết

- Tạo, activate, cài package, deactivate là vòng lặp chuẩn khi làm việc với Python project.
- Quản lý môi trường tốt giúp tránh lỗi khi deploy hoặc chia sẻ dự án với người khác.
