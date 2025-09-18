# 🧹 Data Cleaning Cheatsheet

Làm sạch dữ liệu chiếm tới **80% thời gian** trong quy trình Data Science.  
Bảng dưới đây là checklist các vấn đề thường gặp và cách xử lý.

---

## 📌 Ràng buộc dữ liệu (Data Constraints)

| Vấn đề | Ví dụ | Giải pháp |
|--------|-------|-----------|
| **Ràng buộc kiểu dữ liệu**: đảm bảo cột có kiểu dữ liệu đúng | Cột `revenue_usd` lưu dưới dạng chuỗi thay vì số:<br>`"$1,000"`, `"$3,210"` | - Chuyển về kiểu dữ liệu đúng<br>- Kiểm tra lỗi gõ (ví dụ: sai dấu thập phân) |
| **Ràng buộc phạm vi giá trị** | Cột `gpa` chỉ nên trong khoảng `[0.0 – 4.0]`, nhưng có giá trị `5.1` | - Loại bỏ dòng sai<br>- Gán giá trị vượt ngưỡng về min/max<br>- Gán thành NaN rồi xử lý sau |
| **Ràng buộc tính duy nhất (duplicates)** | 2 dòng giống nhau ở `name`, `phone_number` nhưng khác `height_cm` | - Giữ lại 1 dòng duy nhất nếu trùng hoàn toàn<br>- Hợp nhất nếu chỉ trùng gần giống |

---

## 📝 Dữ liệu dạng text & phân loại (Text & Categorical Data)

| Vấn đề | Ví dụ | Giải pháp |
|--------|-------|-----------|
| **Danh mục không nhất quán** | Cột `city` có cả “New York” và “New York City” | - Chuẩn hóa lại tên danh mục<br>- Suy đoán từ dữ liệu khác nếu không rõ |
| **Độ dài chuỗi vi phạm** | Số điện thoại có 9 ký tự thay vì 14 | - Loại bỏ hoặc gán NaN cho giá trị sai |
| **Định dạng không nhất quán** | Cột `phone_number` có `(555) 200-5598` và `+1 555 2005598` | - Chuẩn hóa định dạng<br>- Loại bỏ dòng lỗi nếu không thể chuẩn hóa |

---

## 📐 Vấn đề đồng nhất dữ liệu (Data Uniformity)

| Vấn đề | Ví dụ | Giải pháp |
|--------|-------|-----------|
| **Đơn vị không đồng nhất (numeric)** | Cột nhiệt độ chứa cả °C và °F | - Chuẩn hóa về 1 đơn vị<br>- Loại bỏ giá trị bất hợp lý |
| **Đơn vị không đồng nhất (date)** | Cột ngày có cả `dd-mm-yyyy` và `mm-dd-yyyy` | - Chuẩn hóa định dạng ngày<br>- Loại bỏ giá trị không rõ định dạng |
| **Kiểm tra chéo số liệu (cross-field)** | Tổng số vé `economy + first class ≠ total` | - Áp dụng quy tắc kiểm tra từ domain knowledge<br>- Loại bỏ dòng sai |
| **Kiểm tra chéo ngày tháng** | Ngày sinh không khớp với tuổi | - So khớp giữa các cột liên quan<br>- Loại bỏ hoặc điều chỉnh nếu sai |

---

## ❓ Vấn đề dữ liệu thiếu (Missing Data)

| Vấn đề | Ví dụ | Giải pháp |
|--------|-------|-----------|
| **Thiếu ngẫu nhiên hoàn toàn (MCAR)** | Dữ liệu bị thiếu không theo quy luật | - Loại bỏ dòng thiếu<br>- Điền bằng mean/median<br>- Thu thập dữ liệu mới |
| **Thiếu ngẫu nhiên (MAR)** | Thiếu dữ liệu điều tra ở vùng B do bưu điện không phủ sóng | - Điền giá trị dựa vào dữ liệu khác<br>- Dùng mô hình ML để suy đoán |
| **Thiếu không ngẫu nhiên (MNAR)** | Cảm biến không ghi khi nhiệt độ quá cao/thấp | - Điền bằng thuật toán<br>- Thu thập thêm dữ liệu nếu cần |

---

📌 **Ghi chú**:  
- Khi xử lý dữ liệu cần dựa vào **kiến thức miền (domain knowledge)** để tránh mất thông tin quan trọng.  
- Không có một cách xử lý “chuẩn cho mọi trường hợp” → phải cân nhắc mục tiêu phân tích.  
