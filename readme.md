### Phần 1: Nhận diện rủi ro và xử lý sự cố

1. Tình huống 1:
-Phishing (cụ thể là Typosquatting). Dấu hiệu giả mạo là URL sai chính tả (githuh thay vì github).

2. Tình huống 2:
-Mã độc (Malware/Trojan) ẩn dưới vỏ bọc phần mềm Crack. Tắt Windows Defender sẽ vô hiệu hóa hàng rào bảo vệ, cho phép mã độc xâm nhập và kiểm soát máy tính mà không bị chặn.

3. Quy tắc 5 KHÔNG: 
- Tình huống 1: KHÔNG click link lạ. 
- Tình huống 2: KHÔNG dùng phần mềm Crack/lậu.

4. 4 Bước Cấp cứu: 
B1: Cô lập (Ngắt mạng) 
B2: Quét và diệt (Chạy Anti-virus) 
B3: Thay ổ khóa (Đổi mật khẩu từ một thiết bị khác) 
B4: Cảnh báo và Theo dõi.

### Phần 2: Chuyển sang Password Manager

1. Hậu quả: 
Hacker sẽ chiếm quyền kiểm soát cả Vercel và GitHub. Kiểu tấn công: Credential Stuffing (hoặc Password Reuse).

2. Giải thích
Zero-Knowledge Architecture: Dữ liệu được mã hóa/giải mã ngay trên thiết bị của bạn. Máy chủ chỉ lưu bản mã hóa và không giữ Master Password, nên hacker không thể đọc được dữ liệu thật.

3. Cấu hình Generator:

Thông số|Giá trị cấu hình|
|---|---|
Độ dài|>= 16 |ký tự|Chữ hoa (A-Z)|Bật|
Chữ thường (a-z)|Bật|
Chữ số (0-9)|Bật
Ký tự đặc biệt|Bật|

### Phần 3: Kích hoạt 2FA cho tài khoản GitHub tổ chức

1.Authenticator App:
-Lí do: Tạo mã offline an toàn hơn. 
-2 nhược điểm SMS OTP: Dễ bị tấn công viễn thông (SIM Swapping/đánh chặn) và hoàn toàn phụ thuộc vào sóng điện thoại.

2. Các bước kích hoạt: 
B1: Vào Settings > Password and authentication trên GitHub  
B2: Bật Enable 2FA và chọn Authenticator app 
B3: Mở Google Authenticator chọn Quét mã QR 
B4: Quét QR trên màn hình máy tính 
B6: Nhập mã 6 số hiển thị trên app để xác nhận.

3. Mã khôi phục (Recovery Codes): Nên lưu trong Password Manager hoặc USB mã hóa, két sắt. Không nên lưu dưới dạng ảnh chụp màn hình, file .txt không khóa, hoặc gửi qua tin nhắn.

### Phần 4: Bảo vệ Secrets trước khi push code
1. 2 giá trị hardcode: 
`"sk-proj-abc123456789"` và `"SmartCampus@2026"`.

2. Code `config.js` chuẩn:


```javascript
const API_KEY = process.env.API_KEY;
const DB_PASSWORD = process.env.DB_PASSWORD;
function connectDatabase() { return connect(DB_PASSWORD); }
```

3. Nội dung

- `.env`:

```
API_KEY=sk-proj-abc123456789
DB_PASSWORD=SmartCampus@2026
```

- `.gitignore`:

```
.env
```
- `.env.example`:
```
API_KEY=
DB_PASSWORD=
```

4. 4 Bước Kiểm tra trước khi Push:

`git status`: Đảm bảo .env không nằm trong danh sách chuẩn bị commit.

Kiểm tra `.gitignore`: Chắc chắn đã thêm dòng loại trừ `.env`.

`git diff`: Rà soát lại code để đảm bảo không còn Secret nào bị gõ trực tiếp (hardcode).

Kiểm tra `.env.example`: Đảm bảo có đủ tên biến nhưng để trống hoàn toàn giá trị.