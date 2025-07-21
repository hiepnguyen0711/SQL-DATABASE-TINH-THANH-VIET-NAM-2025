
# 🇻🇳 DATABASE TỈNH THÀNH VIỆT NAM 2025

Cơ sở dữ liệu hành chính Việt Nam cập nhật đến năm **2025**, phục vụ các dự án liên quan đến **thương mại điện tử, logistics, phân tích địa lý, bản đồ**, v.v. Dữ liệu chuẩn hóa, bao gồm đầy đủ thông tin:

- Vùng miền (`mien_vung`)
- Loại đơn vị hành chính (`loai_don_vi`)
- Tỉnh thành (`tinh_thanh`)
- Phường xã (`phuong_xa`)

> 🧠 **Phù hợp với các hệ thống cần xử lý địa chỉ chi tiết đến cấp phường/xã.**

---

## 🧱 Cấu trúc cơ sở dữ liệu

| Bảng           | Mô tả                                    |
|----------------|-------------------------------------------|
| `mien_vung`    | Danh sách 8 vùng địa lý hành chính        |
| `loai_don_vi`  | Các loại đơn vị như Thành phố, Tỉnh, Xã...|
| `tinh_thanh`   | Danh sách đầy đủ các tỉnh/thành Việt Nam  |
| `phuong_xa`    | Dữ liệu đầy đủ các phường/xã toàn quốc    |

---

## 📦 Hướng dẫn sử dụng

### 1. Import dữ liệu SQL vào MySQL / MariaDB

<details>
<summary><strong>📥 Lệnh import bằng command line</strong></summary>

```bash
mysql -u <tên_user> -p < tên_database > < database_tinh_thanh_vietnam_update_2025.sql
```

</details>

### 2. Truy vấn mẫu

<details>
<summary><strong>📄 Lấy danh sách phường thuộc Hà Nội</strong></summary>

```sql
SELECT * 
FROM phuong_xa 
WHERE province_code = '01';
```

</details>

<details>
<summary><strong>📄 Lấy tên vùng của tỉnh cụ thể</strong></summary>

```sql
SELECT mv.name AS ten_vung, tt.full_name AS tinh_thanh
FROM mien_vung mv
JOIN tinh_thanh tt ON tt.unit_id = mv.id
WHERE tt.code = '01'
LIMIT 1;
```

</details>

---

## 🧾 Mô tả bảng dữ liệu

### `mien_vung`

```sql
CREATE TABLE mien_vung (
  id INT PRIMARY KEY,
  name VARCHAR(255) NOT NULL,
  name_en VARCHAR(255) NOT NULL,
  code_name VARCHAR(255),
  code_name_en VARCHAR(255)
);
```

### `loai_don_vi`

```sql
CREATE TABLE loai_don_vi (
  id INT PRIMARY KEY,
  full_name VARCHAR(255),
  full_name_en VARCHAR(255),
  short_name VARCHAR(255),
  short_name_en VARCHAR(255),
  code_name VARCHAR(255),
  code_name_en VARCHAR(255)
);
```

### `tinh_thanh`

```sql
CREATE TABLE tinh_thanh (
  code VARCHAR(20) NOT NULL,
  name VARCHAR(255) NOT NULL,
  name_en VARCHAR(255) DEFAULT NULL,
  full_name VARCHAR(255) NOT NULL,
  full_name_en VARCHAR(255) DEFAULT NULL,
  code_name VARCHAR(255) DEFAULT NULL,
  unit_id INT(11) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;
```

### `phuong_xa`

```sql
CREATE TABLE phuong_xa (
  code VARCHAR(20) PRIMARY KEY,
  name VARCHAR(255),
  name_en VARCHAR(255),
  full_name VARCHAR(255),
  full_name_en VARCHAR(255),
  code_name VARCHAR(255),
  province_code VARCHAR(20),
  unit_id INT
);
```

---

## 🧑‍💻 Tác giả

- **Nguyễn Văn Hiệp**
- 📘 [Facebook cá nhân](https://www.facebook.com/G.N.S.L.7/)

---

## ☕️ Ủng hộ tác giả một ly cà phê!

Nếu bạn thấy dự án này hữu ích, hãy ủng hộ để mình có động lực tiếp tục cập nhật:

```
Số tài khoản: 0601 5576 3127
Chủ tài khoản: NGUYEN VAN HIEP
Ngân hàng: Sacombank – PGD Lê Văn Quới
```

Cảm ơn bạn đã quan tâm và sử dụng!
