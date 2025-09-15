# 📌 Các bước load dữ liệu CSV vào MySQL

## 1. Chuẩn bị môi trường

* Cài đặt **MySQL Server** và **MySQL Workbench**.
* Cài Python và thư viện cần thiết:

```bash
pip install pandas sqlalchemy pymysql
```

---

## 2. Tạo Database trong MySQL

Mở **MySQL Workbench** hoặc command line:

```sql
CREATE DATABASE ten_db_muondat;
USE ten_db_muondat;
```

---

## 3. Chuẩn bị file CSV

* Đặt file CSV trong thư mục dự án (ví dụ: `data.csv`).
* Kiểm tra encoding (`utf-8` thường an toàn).

---

## 4. Dùng Python import CSV vào MySQL

```python
import pandas as pd
from sqlalchemy import create_engine

# 1. Kết nối MySQL
engine = create_engine("mysql+pymysql://root:password@localhost:3306/ten_db_muondat")

# 2. Đọc file CSV
df = pd.read_csv("data.csv")

# 3. Đẩy dữ liệu vào MySQL
df.to_sql(
    name="bang_du_lieu",   # Tên bảng muốn đặt
    con=engine,
    if_exists="replace",   # 'replace' ghi đè, 'append' ghi thêm
    index=False
)

print("✅ Import thành công vào MySQL!")
```

---

## 5. Kiểm tra trong MySQL

```sql
USE finance_db;
SHOW TABLES;
SELECT * FROM bang_du_lieu LIMIT 10;
```

---
