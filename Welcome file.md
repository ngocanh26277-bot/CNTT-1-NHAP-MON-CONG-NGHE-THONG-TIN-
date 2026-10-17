## PHÂN TÍCH HỆ THỐNG (IPO & SƠ ĐỒ)

-   **Input:** Cảm biến nhiệt độ, độ ẩm đất + Lệnh từ App Mobile
    
-   **Process:** ESP32 xử lý dữ liệu và so sánh với ngưỡng cài đặt
    
-   **Output:** Bật/Tắt Rơ-le (máy bơm/phun sương) + Hiển thị LCD

 Phần 2
## Trang Trại Lan

*Hệ thống tự động chăm sóc hoa lan bằng công nghệ **SoC** và mô hình **DIKW**

---

## 📸 Sơ Đồ Hệ Thống

![Sơ đồ Smart-Farm](https://hunonic.com/wp-content/uploads/2023/10/cong-tac-lahu-4CH-RTC05.jpg)

---


## 📋 Tính Năng

-  Đo nhiệt độ, độ ẩm đất theo thời gian thực
-  Tự động tưới/phun sương khi nhiệt độ >32 
-  Ghi nhật ký vận hành (Log data)
- Dự báo bệnh cây bằng AI (Đang phát triển)

---

##  Thông Số Kỹ Thuật

| Thiết bị | Mã | Vai trò | Điện áp |
| :--- | :--- | :--- | :--- |
| **SoC** | ESP32 | Xử lý trung tâm | $3.3\text{V}$ |
| **Cảm biến** | DHT22 | Đo nhiệt độ/độ ẩm | $5\text{V}$ |
| **Rơ-le** | Relay 4-CH | Đóng/mở máy bơm | $5\text{V}$ |

---

##  Chu Kỳ Xử Lý Của CPU (Fetch – Decode – Execute)

> 1. **Fetch:** CPU lấy lệnh kiểm tra độ ẩm từ bộ nhớ
> 2. **Decode:** Giải mã lệnh, so sánh độ ẩm thực tế với ngưỡng $40\%$
> 3. **Execute:** Nếu độ ẩm $< 40\%$, gửi tín hiệu bật máy bơm tưới lan

---

## 📐 Mô Hình DIKW

* **Data (Dữ liệu):** $35^\circ\text{C}$
* **Information (Thông tin):** Nhiệt độ hiện tại là $35^\circ\text{C}$ (Mức cao)
* **Knowledge (Tri thức):** Nhiệt độ $35^\circ\text{C}$ kéo dài sẽ làm cháy lá lan
* **Wisdom (Trí tuệ):** Tự động bật hệ thống phun sương làm mát



## Lưu Ý Vận Hành (Xử Lý Tràn Bộ Nhớ RAM)

> **KỊCH BẢN KIỂM THỬ: RAM BỊ ĐẦY NẰM TRONG TRẠNG THÁI NGUY HIỂM**
> 
> Nếu mất kết nối mạng kéo dài, nhật ký (system logs) sẽ tích tụ liên tục làm dung lượng RAM khả dụng giảm xuống mức báo động ($< 10\%$)
> 
> **QUY TRÌNH XỬ LÝ AN TOÀN:**
> 
> 1.  **Tự động (Cơ chế phần cứng):** Hệ thống sẽ tự động chuyển sang cơ chế **Ring Buffer** (Bộ đệm xoay vòng) - tự xóa các dòng log cũ nhất để giải phóng RAM mà không làm dừng hệ thống
>     
> 2.  **Thủ công (Thao tác của nông dân):** Nếu hệ thống bị treo hoặc không phản hồi
>
