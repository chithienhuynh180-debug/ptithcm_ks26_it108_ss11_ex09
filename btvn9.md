# Bài 9

## DanhMucTacGia

| Mã TG | Tên Tác Giả | Khoa/Viện | Phòng | Thù Lao |
|-------|-------------|-----------|-------|---------|
| TG001 | Nguyễn Văn An | CNTT | P.201-A | 500000 |
| TG002 | Trần Thị Bình | Điện Tử | P.305-B | 450000 |
| TG003 | Lê Minh Châu | CNTT | P.201-A | 500000 |
| ... | ... | ... | ... | ... |

## Phần 1: Phân tích

### DanhSachBaoCao

| Tên Tác Giả | Phòng Trình Bày | Thù Lao |
|-------------|-----------------|---------|
| Nguyễn Văn An | P.201-A | 500000 |
| Trần Thị Bình | P.305-B | 450000 |
| Lê Minh Châu | P.201-A | 500000 |
| … | chưa cập nhật | chưa cập nhật |

### Giải thích các tham số

- **Lookup_value:** là chìa khóa để tìm nội dung
- **Table_array:** là vùng bảng tham chiếu (vd: `$B$3:$E$6`)
- **Col_Index-num:** chỉ cần gõ số của cột, vd: cột D là cột số 3 đếm từ cột tên tác giả qua của bảng DanhMucTacGia

### Cách làm

Dùng hàm IFERROR, VLOOKUP, TRIM. Lồng nhau: `=IFERROR(VLOOKUP(TRIM(…), …, …, …))`

- B1: Dùng hàm IFERROR
- B2: Lồng vào IFERROR là hàm VLOOKUP
- B3: Lồng vào VLOOKUP là hàm TRIM để xóa khoảng trắng vô hình
- B4: chọn tùy dòng để xóa khoảng trắng vô hình vd: `TRIM(D14)`
- B5: chọn bảng tham chiếu Table_array từ B3 đến E6 (`$B$3:$E$6`)
- B6: chọn cột muốn thêm ndung vào bảng DanhSachBaoCao vd: gõ số 3 là thêm ndung cột phòng của bảng DanhMucTacGia
- B7: gõ False để ra kết quả chính xác
- B8: đóng ngoặc lại để kết thúc hàm VLOOKUP sau đó thêm dòng "chưa cập nhật" rồi đóng ngoặc để kết thúc hàm IFERROR

Dùng hàm IFERROR để không hiện lỗi #N/A thay vào đó sẽ hiện chưa cập nhật.

## Phần 2: Triển Khai & Chống lỗi

Chỉ cần thay Col_index_num chứ không cần viết lại toàn bộ cú pháp vì: tham số này để lấy nội dung từ bảng 1 để hiện vào bảng thứ 2

**Nếu bỏ $ trong Table_array, khi kéo công thức D2 xuống D5, vùng tra cứu sẽ thay đổi thành gì? Cho ví dụ cụ thể với địa chỉ ô.**

- Tại ô D2: là `B3:E6`
- Tại ô D3: Vùng tra cứu bị tịnh tiến xuống 1 hàng thành `B4:E7`
- Tại ô D4: Vùng tra cứu bị tịnh tiến xuống 2 hàng thành `B5:E8`
- Tại ô D5: nhích xuống 2 hàng thành `B6:E9`

Nên khi không có dấu $ thì từ D2 xuống D5 là `B6:E9`