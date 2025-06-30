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

## 👨‍💻 Tác giả  

Nhóm 9: Phạm Văn Trà, Phạm Thị Ngọc Thanh, Đinh Mai Phương • Lớp CNTT 17-11 • Trường Đại học Đại Nam • Nhập môn An toàn bảo mật thông tin • Đề tài: Gửi CV an toàn có kiểm tra IP  
