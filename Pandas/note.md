# 🐼 Pandas Cheat Sheet

---

## 1. 📥 Khởi tạo & Import dữ liệu

```python
import pandas as pd
```

* **Tạo DataFrame từ dict**

  ```python
  df = pd.DataFrame({"Name":["A","B"], "Age":[20,25]})
  ```
* **Đọc dữ liệu**

  ```python
  pd.read_csv("data.csv")              # CSV
  pd.read_csv("data.tsv", sep="\t")    # TSV
  pd.read_excel("data.xlsx")           # Excel
  pd.read_json("data.json")            # JSON
  pd.read_sql(query, connection)       # SQL
  ```
* **Ghi dữ liệu**

  ```python
  df.to_csv("out.csv", index=False)
  df.to_excel("out.xlsx", index=False)
  ```

---

## 2. 🔎 Khám phá dữ liệu

```python
df.head()       # 5 dòng đầu
df.tail()       # 5 dòng cuối
df.shape        # (số_hàng, số_cột)
df.info()       # Thông tin chung
df.describe()   # Thống kê số liệu
df.dtypes       # Kiểu dữ liệu cột
df.columns      # Danh sách tên cột
df.index        # Index của DataFrame
```

---

## 3. 🎯 Truy cập dữ liệu

* **Theo cột**

```python
df['col']             # 1 cột (Series)
df[['col1','col2']]   # nhiều cột (DataFrame)
```

* **Theo hàng**

```python
df.iloc[0]          # dòng đầu (theo vị trí)
df.loc[0]           # dòng nhãn = 0
df.loc[0, 'col']    # giá trị ô
```

* **Slicing**

```python
df[0:5]     # 5 dòng đầu
df.iloc[0:5, 0:2]   # 5 dòng đầu, 2 cột đầu
```

---

## 4. 🧮 Lọc dữ liệu (Condition)

```python
df[df['quantity'] == 15]
df[df['price'] > 100]
df[(df['quantity']==15) & (df['price']>100)]
df[(df['quantity']==15) | (df['price']==200)]
```

---

## 5. 🛠️ Xử lý dữ liệu

* **Đổi tên cột**

```python
df.rename(columns={'old':'new'}, inplace=True)
```

* **Thêm / xoá cột**

```python
df['new'] = df['col1'] + df['col2']
df.drop(columns=['col'], inplace=True)
```

* **Thêm / xoá hàng**

```python
df.drop(index=0, inplace=True)   # xoá hàng 0
df.append(other_df)              # nối thêm
```

---

## 6. 📊 Thống kê & toán học

```python
df['col'].mean()
df['col'].sum()
df['col'].min(), df['col'].max()
df['col'].value_counts()
df['col'].unique()
df['col'].nunique()
```

---

## 7. 🧹 Làm sạch dữ liệu

```python
df.isnull().sum()               # đếm giá trị null
df.dropna()                     # xoá hàng null
df.fillna(0)                    # thay null bằng 0
df['col'].astype(float)         # đổi kiểu dữ liệu
df.duplicated().sum()           # đếm bản ghi trùng
df.drop_duplicates()            # xoá bản ghi trùng
```

---

## 8. 🧾 Sắp xếp & GroupBy

```python
df.sort_values('col')                     # sắp xếp
df.groupby('category')['sales'].sum()     # group
df.groupby(['cat1','cat2']).mean()
```

---

## 9. 🔄 Merge / Join / Concatenate

```python
pd.concat([df1, df2])      # nối dọc
pd.merge(df1, df2, on="id", how="inner")  # join
```
