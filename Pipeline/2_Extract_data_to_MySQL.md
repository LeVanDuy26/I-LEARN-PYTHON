# 📌 Extract Data từ MySQL bằng Python

### 1. Import thư viện & tạo kết nối

```python
import pandas as pd
from sqlalchemy import create_engine

# Kết nối MySQL
engine = create_engine("mysql+pymysql://root:password@localhost:3306/ten_db")
```

---

### 2. Đọc toàn bộ bảng từ MySQL

```python
# Lấy tất cả dữ liệu trong bảng
df = pd.read_sql("SELECT * FROM customers", con=engine)

print(df.head())      # 5 dòng đầu
print(df.shape)       # (số dòng, số cột)
```

---

### 3. Đọc với điều kiện (SQL query)

Bạn có thể viết bất kỳ câu **SQL** nào:

```python
query = """
SELECT customer_id, name, city
FROM customers
WHERE city = 'Hanoi'
LIMIT 10
"""
df_hanoi = pd.read_sql(query, con=engine)
print(df_hanoi)
```

---

### 4. Join nhiều bảng

```python
query = """
SELECT o.order_id, c.name, o.total_amount
FROM orders o
JOIN customers c ON o.customer_id = c.customer_id
WHERE o.total_amount > 1000000
ORDER BY o.total_amount DESC
"""
df_orders = pd.read_sql(query, con=engine)
print(df_orders.head())
```

---

### 5. Extract nhiều bảng cùng lúc (tách DataFrame)

```python
tables = ["customers", "orders", "products"]
data = {}

for t in tables:
    data[t] = pd.read_sql(f"SELECT * FROM {t}", con=engine)

# Truy cập từng DataFrame
print(data["customers"].head())
print(data["orders"].head())
```

---

✅ Như vậy:

* `pandas.read_sql()` cho phép **chạy SQL trực tiếp** và trả về **DataFrame**.
* Bạn có thể phân tích, vẽ biểu đồ, hoặc làm sạch dữ liệu ngay trong Python.


