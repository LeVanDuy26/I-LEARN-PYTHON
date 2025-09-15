# 📌 Pipeline: MySQL → Python (Clean) → MySQL (bảng clean)

### 1. Extract dữ liệu từ MySQL

```python
import pandas as pd
from sqlalchemy import create_engine

# Kết nối MySQL
engine = create_engine("mysql+pymysql://root:123456@localhost:3306/finance_db")

# Load dữ liệu gốc
df = pd.read_sql("SELECT * FROM customers", con=engine)
```

---

### 2. Làm sạch dữ liệu trong Python

Ví dụ:

* Xử lý `NaN`
* Chuẩn hóa kiểu dữ liệu
* Loại bỏ trùng lặp
* Tạo thêm cột mới

```python
# Xóa dòng trùng lặp
df = df.drop_duplicates()

# Điền missing values cho cột 'age'
if "age" in df.columns:
    df["age"] = df["age"].fillna(df["age"].median())

# Chuẩn hóa chữ (nếu có cột tên)
if "name" in df.columns:
    df["name"] = df["name"].str.title()

# Tạo thêm cột 'age_group'
if "age" in df.columns:
    df["age_group"] = pd.cut(df["age"], bins=[0,18,35,60,100],
                             labels=["teen","young","adult","senior"])
```

---

### 3. Load ngược lại vào MySQL

Dùng `to_sql()` để ghi sang **bảng mới** (`customers_clean`):

```python
df.to_sql(
    name="customers_clean",
    con=engine,
    if_exists="replace",   # 'replace' = ghi đè, 'append' = thêm dữ liệu
    index=False,
    chunksize=10000,
    method="multi"
)

print("✅ Đã lưu dữ liệu sạch vào bảng 'customers_clean'")
```

---

### 4. Kiểm tra trong MySQL

```sql
USE finance_db;
SHOW TABLES;
SELECT * FROM customers_clean LIMIT 10;
```

---

## 🔹 Lưu ý quan trọng

* **Không nên ghi đè bảng gốc (`customers`)** → luôn tạo bảng mới (`customers_clean`) để bảo toàn dữ liệu gốc.
* Có thể thêm **timestamp** vào tên bảng (`customers_clean_20250915`) để versioning dữ liệu.
* Nếu muốn kiểm soát **kiểu dữ liệu** trong MySQL (ví dụ `INT`, `DATETIME`, `DECIMAL`) thì dùng `dtype` trong `to_sql`.

Ví dụ ép kiểu:

```python
from sqlalchemy.types import Integer, String

df.to_sql(
    name="customers_clean",
    con=engine,
    if_exists="replace",
    index=False,
    dtype={"customer_id": Integer(), "name": String(255)}
)
```