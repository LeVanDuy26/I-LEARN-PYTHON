# 📊 Matplotlib Cheat Sheet

## 1. **Khởi tạo**

```python
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
```

---

## 2. **Biểu đồ cột (Bar Chart)**

### 🔹 Dùng để so sánh giữa các nhóm/danh mục.

```python
categories = ["A", "B", "C", "D"]
values = [10, 15, 7, 12]

plt.bar(categories, values, color="skyblue", edgecolor="black")
plt.title("Biểu đồ cột")
plt.xlabel("Danh mục")
plt.ylabel("Giá trị")
plt.show()
```

* `color`: màu cột (có thể dùng `"red"`, `"#1f77b4"`, `["red","blue"]`).
* `edgecolor`: màu viền.
* `width`: độ rộng cột.

👉 **Biểu đồ ngang**

```python
plt.barh(categories, values, color="orange")
```

---

## 3. **Biểu đồ đường (Line Chart)**

### 🔹 Dùng để thể hiện xu hướng theo thời gian.

```python
x = np.linspace(0, 10, 100)
y = np.sin(x)

plt.plot(x, y, color="blue", linestyle="--", marker="o", label="sin(x)")
plt.title("Biểu đồ đường")
plt.xlabel("Trục X")
plt.ylabel("Trục Y")
plt.legend()
plt.grid(True, linestyle="--", alpha=0.6)
plt.show()
```

* `linestyle`: `"-"`, `"--"`, `"-."`, `":"`.
* `marker`: `"o"`, `"s"`, `"^"`, `"*"`, `"D"`.
* `label`: tên hiển thị trong `plt.legend()`.

---

## 4. **Biểu đồ tần suất (Histogram)**

### 🔹 Dùng để xem phân phối dữ liệu.

```python
data = np.random.randn(1000)  # dữ liệu ngẫu nhiên
plt.hist(data, bins=20, color="purple", edgecolor="black", alpha=0.7)
plt.title("Histogram")
plt.xlabel("Giá trị")
plt.ylabel("Tần suất")
plt.show()
```

* `bins`: số lượng cột trong histogram.
* `alpha`: độ trong suốt.

---

## 5. **Biểu đồ phân tán (Scatter Plot)**

### 🔹 Dùng để xem mối quan hệ giữa 2 biến.

```python
x = np.random.rand(50)
y = np.random.rand(50)
sizes = np.random.randint(50, 300, size=50)
colors = np.random.rand(50)

plt.scatter(x, y, s=sizes, c=colors, cmap="viridis", alpha=0.7, edgecolors="black")
plt.title("Scatter Plot")
plt.xlabel("X")
plt.ylabel("Y")
plt.colorbar(label="Màu sắc")
plt.show()
```

* `s`: kích thước điểm.
* `c`: màu sắc (có thể truyền list).
* `cmap`: bảng màu (`"viridis"`, `"plasma"`, `"coolwarm"`).

---

## 6. **Biểu đồ hộp (Box Plot)**

### 🔹 Dùng để xem phân phối, outliers.

```python
data = [np.random.normal(50, 10, 200),
        np.random.normal(60, 15, 200),
        np.random.normal(55, 20, 200)]

plt.boxplot(data, patch_artist=True,
            boxprops=dict(facecolor="lightblue", color="black"),
            medianprops=dict(color="red", linewidth=2))
plt.xticks([1, 2, 3], ["Nhóm 1", "Nhóm 2", "Nhóm 3"])
plt.title("Box Plot")
plt.show()
```

---

## 7. **Biểu đồ tròn (Pie Chart)**

### 🔹 Dùng để xem tỷ trọng.

```python
sizes = [40, 30, 20, 10]
labels = ["A", "B", "C", "D"]
colors = ["#ff9999","#66b3ff","#99ff99","#ffcc99"]

plt.pie(sizes, labels=labels, colors=colors, autopct="%.1f%%",
        startangle=90, explode=(0.1, 0, 0, 0), shadow=True)
plt.title("Pie Chart")
plt.show()
```

* `autopct`: hiển thị %.
* `startangle`: góc xoay ban đầu.
* `explode`: làm nổi 1 lát (giá trị 0.1 → tách ra).

---

## 8. **Biểu đồ nhiều subplot**

### 🔹 Dùng để vẽ nhiều biểu đồ trên cùng một figure.

```python
fig, axes = plt.subplots(2, 2, figsize=(10, 8))

axes[0,0].bar(categories, values)
axes[0,0].set_title("Bar Chart")

axes[0,1].plot(x, y, color="red")
axes[0,1].set_title("Line Chart")

axes[1,0].hist(data, bins=15, color="green")
axes[1,0].set_title("Histogram")

axes[1,1].scatter(x, y, color="purple")
axes[1,1].set_title("Scatter Plot")

plt.tight_layout()
plt.show()
```

---

## 9. **Tùy chỉnh chung**

* **Kích thước hình**: `plt.figure(figsize=(8,6))`
* **Tiêu đề & nhãn**:

  ```python
  plt.title("Tiêu đề", fontsize=14, fontweight="bold")
  plt.xlabel("Trục X", fontsize=12)
  plt.ylabel("Trục Y", fontsize=12)
  ```
* **Chữ viết tiếng Việt**: cần cài font (nếu bị lỗi font).

---