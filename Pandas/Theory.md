# 🐼 Pandas Cheat Sheet (Full Version)

---

## 1. 📥 Khởi tạo & Import dữ liệu

```python
import pandas as pd
```

### Tạo DataFrame

```python
data = {"Name":["An","Bình","Chi"], "Age":[20,25,30]}
df = pd.DataFrame(data)
```

### Đọc dữ liệu từ file

```python
pd.read_csv("data.csv")              # CSV
pd.read_csv("data.tsv", sep="\t")    # TSV
pd.read_excel("data.xlsx")           # Excel
pd.read_json("data.json")            # JSON
pd.read_sql("SELECT * FROM users", connection) # SQL
```

### Ghi dữ liệu ra file

```python
df.to_csv("out.csv", index=False)
df.to_excel("out.xlsx", index=False)
```

---

## 2. 🔎 Khám phá dữ liệu

```python
df.head(5)        # 5 dòng đầu
df.tail(3)        # 3 dòng cuối
df.shape          # (số_hàng, số_cột)
df.info()         # thông tin tổng quan
df.describe()     # thống kê số liệu
df.dtypes         # kiểu dữ liệu từng cột
df.columns        # danh sách tên cột
df.index          # index
```

Ví dụ:

```python
df.describe(include="all")  # bao gồm cả cột object
```

---

## 3. 🎯 Truy cập dữ liệu

### Truy cập cột

```python
df['Name']              # 1 cột (Series)
df[['Name','Age']]      # nhiều cột (DataFrame)
```

### Truy cập hàng

```python
df.iloc[0]             # dòng đầu (theo vị trí)
df.loc[0]              # dòng có index = 0
df.loc[0, 'Name']      # lấy giá trị 1 ô
```

### Slicing

```python
df[0:5]                # 5 dòng đầu
df.iloc[0:5, 0:2]      # 5 dòng đầu, 2 cột đầu
```

---

## 4. 🧮 Lọc dữ liệu (Condition)

```python
df[df['Age'] > 25]                        # Age > 25
df[df['Name'] == "An"]                    # tên = "An"
df[(df['Age'] > 20) & (df['Age'] < 30)]   # điều kiện AND
df[(df['Age'] < 20) | (df['Age'] > 40)]   # điều kiện OR
```

---

## 5. 🛠️ Xử lý dữ liệu

### Đổi tên cột

```python
df.rename(columns={'Name':'FullName'}, inplace=True)
```

### Thêm / xoá cột

```python
df['Age_next_year'] = df['Age'] + 1
df.drop(columns=['Age_next_year'], inplace=True)
```

### Thêm / xoá hàng

```python
df.drop(index=0, inplace=True)     # xoá hàng đầu tiên
df2 = pd.DataFrame({"Name":["Dũng"], "Age":[22]})
df = df.append(df2, ignore_index=True)   # thêm hàng
```

---

## 6. 📊 Thống kê & toán học

```python
df['Age'].mean()        # trung bình
df['Age'].median()      # trung vị
df['Age'].sum()         # tổng
df['Age'].min(), df['Age'].max()   # min & max
df['Age'].std()         # độ lệch chuẩn

df['Name'].value_counts()  # đếm tần suất
df['Name'].unique()        # giá trị duy nhất
df['Name'].nunique()       # số lượng giá trị duy nhất
```

---

## 7. 🧹 Làm sạch dữ liệu

```python
df.isnull().sum()              # đếm null
df.dropna()                    # xoá hàng null
df.fillna(0)                   # thay null bằng 0
df['Age'].astype(float)        # đổi kiểu dữ liệu
df.duplicated().sum()          # đếm bản ghi trùng
df.drop_duplicates()           # xoá bản ghi trùng
```

Ví dụ: thay giá trị null bằng trung vị:

```python
df['Age'].fillna(df['Age'].median(), inplace=True)
```

---

## 8. 🧾 Sắp xếp & GroupBy

```python
df.sort_values('Age')                   # sắp xếp theo Age
df.sort_values(['Age','Name'], ascending=[True, False])

df.groupby('Name')['Age'].mean()        # group theo Name
df.groupby(['Name','Age']).size()       # group nhiều cột
```

---

## 9. 🔄 Merge / Join / Concatenate

### Nối dọc / ngang

```python
pd.concat([df1, df2])               # nối dọc (thêm hàng)
pd.concat([df1, df2], axis=1)       # nối ngang (thêm cột)
```

### Merge (giống SQL JOIN)

```python
pd.merge(df1, df2, on="id", how="inner")   # inner join
pd.merge(df1, df2, on="id", how="left")    # left join
pd.merge(df1, df2, on="id", how="right")   # right join
pd.merge(df1, df2, on="id", how="outer")   # full join
```

---

## 🔟 ⏱️ Xử lý ngày giờ (Datetime)

```python
df['dob'] = pd.to_datetime(df['dob'])
df['year'] = df['dob'].dt.year
df['month'] = df['dob'].dt.month
df['day'] = df['dob'].dt.day
df['weekday'] = df['dob'].dt.day_name()
```

Ví dụ tính tuổi:

```python
today = pd.to_datetime("today")
df['age'] = ((today - df['dob']).dt.days / 365.25).astype(int)
```

---

## 11. 📊 Trực quan hoá nhanh với Pandas

```python
df['Age'].plot(kind='hist')          # histogram
df['Age'].plot(kind='box')           # boxplot
df['Name'].value_counts().plot(kind='bar')  # bar chart
```