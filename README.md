<h1 align="center">🔐 GỬI CV AN TOÀN CÓ KIỂM TRA IP</h1>

## 📌 Giới thiệu  
Dự án mô phỏng quá trình gửi hồ sơ (CV) một cách an toàn và có kiểm soát truy cập theo địa chỉ IP. Hệ thống đảm bảo:

- 🔐 Mã hóa nội dung bằng AES-256 (CBC mode)  
- 🔑 Trao đổi khóa phiên qua RSA-1024 (OAEP + SHA-256)  
- ✍️ Ký số metadata (tên file, timestamp, IP) bằng RSA + SHA-512  
- 🧠 Kiểm tra toàn vẹn bằng SHA-512  
- 🌐 Xác minh IP ngay từ bước bắt tay  
- ⚙️ Giao tiếp TCP qua socket, đóng gói JSON gọn gàng  
- ✅ Phản hồi rõ ràng: `ACK`, `NACK (IP)`, `NACK (auth)`, `NACK (integrity)`

---

## 🎯 Tính năng  
- 📂 Gửi file `cv.pdf` đã mã hóa an toàn  
- 🛡️ Kiểm tra IP gửi trong whitelist  
- 🔒 Trao đổi khóa và ký số metadata tự động  
- 📦 Đóng gói JSON gồm khóa, IV, ciphertext, hash, signature  

---
## 📁 Cấu trúc dự án  

```
secure_cv_transfer/
├── crypto_utils.py     # Mã hóa AES/RSA, ký số
├── protocol.py         # Hash, đóng gói/gỡ gói JSON
├── sender.py           # Ứng viên gửi CV
├── receiver.py         # Hệ thống nhận CV
├── cv.pdf              # CV mẫu
├── requirements.txt    # Thư viện phụ thuộc
└── README.md           # Hướng dẫn này
```

## 🛠️ Cài đặt  

```bash
pip install cryptography
```

## 🚀 Cách chạy  

### 1. Người nhận (Receiver)  
```bash
python receiver.py
```  
– Lắng nghe cổng 12345, kiểm tra IP, giải mã và lưu `cv_received.pdf`

### 2. Người gửi (Sender)  
```bash
python sender.py
```  
– Nhập IP máy nhận, gửi handshake, trao đổi khóa, ký metadata, mã hóa và gửi gói tin

---

## 🧪 Kiểm thử  

| Tình huống                     | Phản hồi                      |
|--------------------------------|-------------------------------|
| ✅ IP đúng, dữ liệu hợp lệ      | `ACK` + lưu file thành công   |
| ❌ IP không hợp lệ              | `NACK (IP)`                   |
| ❌ Metadata bị giả mạo          | `NACK (auth)`                 |
| ❌ Ciphertext/IV bị thay đổi    | `NACK (integrity)`            |

---

## 🤝 Đóng góp

Dự án được phát triển bởi 3 thành viên:

| Họ và Tên            | Vai trò                                                                             |
|----------------------|-------------------------------------------------------------------------------------|
| Phạm Văn Trà         | Phát triển mã nguồn, thiết kế kiến trúc hệ thống, kiểm thử và biên soạn tài liệu.   |
| Phạm Thị Ngọc Thanh  | Biên soạn tài liệu, đề xuất cải tiến và hỗ trợ bài tập lớn.                         |
| Đinh Mai Phương      | Phát triển mã nguồn, hỗ trợ bài tập lớn, triển khai dự án và thực hiện.             |

---

© 2025 NHÓM 12, CNTT17-11, TRƯỜNG ĐẠI HỌC ĐẠI NAM
