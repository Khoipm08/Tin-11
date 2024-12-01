<style>
    table {
        width: 100%;
    }
    body{
      max-width: 800px;
      margin: 0 auto;
    }
    h1 {
      text-align: center;
    }
</style>

<h1> Báo cáo tin học lớp 11A1<br/>Năm học 2024-2025</h1>

- [Bảng phân công việc nhóm](#bảng-phân-công-việc-nhóm)
- [1. Bài toán quản lí](#1-bài-toán-quản-lí)
  - [a. Thể loại](#a-thể-loại)
  - [b. Tác giả](#b-tác-giả)
  - [c. Hạn mức](#c-hạn-mức)
  - [d. Sách](#d-sách)
  - [e. Khách hàng](#e-khách-hàng)
  - [f. Đơn sách](#f-đơn-sách)
- [2. Code](#2-code)
  - [a. Khởi tạo cơ sở dữ liệu](#a-khởi-tạo-cơ-sở-dữ-liệu)
  - [b. Thêm dữ liệu mẫu vào cơ sở dữ liệu](#b-thêm-dữ-liệu-mẫu-vào-cơ-sở-dữ-liệu)
  - [c. 5 truy vấn đơn giản](#c-5-truy-vấn-đơn-giản)
  - [d. 3 truy vấn nâng cao](#d-3-truy-vấn-nâng-cao)

## Bảng phân công việc nhóm

| STT | Họ và tên | Nội dung công việc |
|-|-|-|
|1|Phạm Minh Khôi| - Nhóm trưởng, cố vấn. <br/>- Viết SQL phần truy xuất nâng cao. |
|2|Nguyễn Thị Thanh Mai| - Tìm dữ liệu. <br/>- Viết SQL phần thêm dữ liệu. |
|3|Nguyễn Trọng Nghĩa| - Viết báo cáo. <br/>- Viết SQL tạo bảng. |
|4|Ngô Nguyễn Nguyên Như| - Tìm dữ liệu. <br/>- Viết SQL truy xuất đơn giản. |

<br/>

## 1. Bài toán quản lí
- Bài toán quản lý đã chọn: Bài toán quản lý thư viện. 
- Các đối tượng gồm: 
    + Tên sách 
    + Tác giả 
    + Thể loại 
    + Hạn mức 
    + Tên khách hàng 
    + Đơn sách
- Dưới đây là mô hình dữ liệu quan hệ:

### a. Thể loại

| Gid | TheLoai |
|---|---|
| BK | Bi kịch |
| TT | Tiểu thuyết |
| ... | ... |

Bảng ***Thể loại*** lưu trữ những thông tin liên quan đến các thể loại truyện với các cột thuộc tính là ***mã thể loại*** (Gid) với ***tên thể loại*** (TheLoai).

### b. Tác giả

| Aid | TacGia |
|---|---|
| 1 | William Shakespeare |
| 2 | Charles Dickens |
| ... | ... |

Bảng ***Tác giả*** lưu trữ tên của các tác giả với các cột thuộc tính là ***mã định danh*** (Aid) và ***tên tác giả*** (TacGia).

### c. Hạn mức

| Did | HanMuc |
|---|---|
| 100 | 1 |
| 200 | 2 |
| ... | ... |

Bảng ***Hạn mức*** lưu trữ số lượng ngày được mượn sách với các cột thuộc tính là ***mã ngày*** (Did) và ***số ngày tối đa được mượn*** hay còn gọi là hạn mức (HanMuc).

### d. Sách

| Bid | TenSach | Gid | Did | Aid |
|---|---|---|---|---|
| 001 | Anna Karenina | TT | 300 | 3 |
| 002 | Biến hình | TN | 200 | 4 |
| ... | ... | ... | ... | ... |

Bảng ***Sách*** và bảng Thể loại có chung thuộc tính ***Gid***, bên cạnh đó bảng Tên sách và bảng Tác giả có chung thuộc tính ***Aid***, cuối cùng bảng Tên sách và bảng Hạn mức có chung thuộc tính ***Did***.

### e. Khách hàng

| Id | TenKhachHang | NgayDangKy | NgayHetHan |
|---|---|---|---|
| 1 | Nguyễn Văn A | 2023/01/01 | 2024/12/31 |
| 2 | Trần Thị B | 2022/05/15 | 2025/04/30 |
| ... | ... | ... | ... |

Bảng ***Khách hàng*** lưu trữ thông tin về khách hàng với các cột thuộc tính là ***mã định danh*** (id), ***họ và tên khách hàng*** (TenKhachHang), ***ngày đăng ký*** (NgayDangKy) và  ***ngày hết hạn*** (NgayHetHan).

### f. Đơn sách

| Id | Bid | NgayMuon |
|---|---|---|
| 10 | 19 | 2023-07-11 |
| 9 | 18 | 2023-10-13 |
| ... | ... | ... |

Bảng ***Đơn sách*** lưu trữ thông tin về các đơn mượn sách với các cột thuộc tính là ***mã đơn sách*** (id), ***mã sách*** (bid) và ***ngày mượn*** (NgayMuon).

<br/>

## 2. Code
[Link code ở OneCompiler](https://onecompiler.com/mysql/42zk3p857)

### a. Khởi tạo cơ sở dữ liệu

```sql
CREATE TABLE khachhang (
  id INT NOT NULL AUTO_INCREMENT,
  hovaten VARCHAR(255) NOT NULL,
  ngaygianhap DATE NOT NULL,
  ngayhethan DATE NOT NULL,
  PRIMARY KEY (id)
);

CREATE TABLE tacgia (
  aid INT NOT NULL AUTO_INCREMENT,
  hovaten VARCHAR(255) NOT NULL,
  PRIMARY KEY (aid)
);

CREATE TABLE theloai (
  gid VARCHAR(2) NOT NULL,
  theloai VARCHAR(255) NOT NULL,
  PRIMARY KEY (gid)
);

CREATE TABLE hanmuc (
  did INT NOT NULL,
  hanmuc INT NOT NULL,
  PRIMARY KEY (did)
);

CREATE TABLE sach (
  bid INT NOT NULL AUTO_INCREMENT,
  tensach TEXT NOT NULL,
  gid VARCHAR(2) NOT NULL,
  did INT NOT NULL,
  aid INT NOT NULL,
  PRIMARY KEY (bid),
  FOREIGN KEY (gid) REFERENCES theloai(gid),
  FOREIGN KEY (did) REFERENCES hanmuc(did),
  FOREIGN KEY (aid) REFERENCES tacgia(aid)
);

CREATE TABLE no (
  id INT NOT NULL,
  bid INT NOT NULL,
  ngaymuon DATE NOT NULL,
  FOREIGN KEY (id) REFERENCES khachhang(id),
  FOREIGN KEY (bid) REFERENCES sach(bid)
);
```

### b. Thêm dữ liệu mẫu vào cơ sở dữ liệu

```sql
INSERT INTO tacgia(hovaten) VALUES 
("William Shakespeare"),
("Charles Dickens"),
("Leo Tolstoy"),
("Franz Kafka"),
("Gabriel García Márquez"),
("Nguyễn Du"),
("Nam Cao"),
("Nguyễn Minh Châu"),
("Nguyễn Huy Thiệp"),
("Bảo Ninh");

INSERT INTO theloai VALUES  
("BK",	"Bi kịch"),
("TT",	"Tiểu thuyết"),
("TN",	"Truyện ngắn"),
("T",	"Thơ"),
("TD",	"Truyện dài");

INSERT INTO hanmuc VALUES 
(100, 1), 
(200, 2), 
(300, 3), 
(400, 4), 
(500, 5), 
(600, 6), 
(700, 7);

INSERT INTO sach(tensach, gid, did, aid) VALUES
('Anna Karenina', 'TT', 100, 3),
('Biến hình', 'TN', 500, 4),
('Chí Phèo', 'TT', 400, 7),
('Chiếc thuyền ngoài xa', 'TT', 300, 8),
('Chiến tranh và hòa bình', 'TT', 300, 3),
('Đại đoàn kết', 'TT', 400, 2),
('Đoạn trường tân thanh', 'TD', 600, 6),
('Hamlet', 'BK', 500, 1),
('Lão Hạc', 'TN', 100, 7),
('Lâu đài', 'TT', 200, 4),
('Mặt trận', 'TT', 300, 10),
('Mùa lạc', 'TT', 500, 9),
('Người đàn bà đi qua lửa', 'TT', 300, 8),
('Oliver Twist', 'TT', 400, 2),
('Quê mẹ', 'TT', 600, 9),
('Romeo và Juliet', 'BK', 100, 1),
('Sông không chảy ngược', 'TT', 200, 10),
('Tình yêu thời dịch tả', 'TT', 500, 5),
('Trăm năm cô đơn', 'TT', 100, 5),
('Truyện Kiều', 'T', 700, 6);

INSERT INTO khachhang(hovaten, ngaygianhap, ngayhethan) VALUES  
('Nguyễn Văn A', '2023-01-01', '2024-12-31'),
('Trần Thị B', '2022-05-15', '2025-04-30'),
('Lê Văn C', '2021-10-20', '2026-09-15'),
('Phạm Thị D', '2023-03-08', '2024-12-31'),
('Hoàng Văn E', '2022-11-22', '2025-11-21'),
('Vũ Thị F', '2021-07-10', '2026-06-30'),
('Đặng Văn G', '2023-02-15', '2024-12-31'),
('Bùi Thị H', '2022-12-25', '2025-12-24'),
('Đỗ Văn I', '2021-09-05', '2026-08-31'),
('Hồ Thị J', '2023-04-02', '2024-12-31');

INSERT INTO no (id, bid, ngaymuon)
SELECT 
    k.id,
    FLOOR(RAND() * (20 - 1 + 1)) + 1, 
    DATE_ADD('2023-01-01', INTERVAL FLOOR(RAND() * 365) DAY)
FROM khachhang k
CROSS JOIN sach s
LIMIT 12;   
```

### c. 5 truy vấn đơn giản

```sql
-- Truy vấn 5 tác giả đầu
SELECT aid, hovaten Tác_giả FROM tacgia LIMIT 5;

-- Truy vấn 5 thông tin khách hàng đầu
SELECT id, hovaten Họ_và_tên_khách_hàng, ngaygianhap Ngày_gia_nhập, ngayhethan Ngày_hết_hạn FROM khachhang LIMIT 5;

-- Truy vấn 5 thể loại đầu
SELECT gid, theloai Thể_loại FROM theloai;

-- Truy vấn 5 cuốn sách đầu cùng thể loại của chúng
SELECT bid, s.tensach Tên_sách, t.theloai Thể_loại FROM sach s LEFT JOIN theloai t ON s.gid = t.gid LIMIT 5;

-- Truy vấn 5 cuốn sách đầu cùng tác giả của chúng
SELECT bid, s.tensach Tên_sách, a.hovaten Tác_giả FROM sach s LEFT JOIN tacgia a ON s.aid = a.aid LIMIT 5;
```

Outputs

```
+-----+--------------------------+
| aid | Tác_giả                  |
+-----+--------------------------+
|   1 | William Shakespeare      |
|   2 | Charles Dickens          |
|   3 | Leo Tolstoy              |
|   4 | Franz Kafka              |
|   5 | Gabriel García Márquez   |
+-----+--------------------------+
+----+----------------------------+------------------+-------------------+
| id | Họ_và_tên_khách_hàng       | Ngày_gia_nhập    | Ngày_hết_hạn      |
+----+----------------------------+------------------+-------------------+
|  1 | Nguyễn Văn A               | 2023-01-01       | 2024-12-31        |
|  2 | Trần Thị B                 | 2022-05-15       | 2025-04-30        |
|  3 | Lê Văn C                   | 2021-10-20       | 2026-09-15        |
|  4 | Phạm Thị D                 | 2023-03-08       | 2024-12-31        |
|  5 | Hoàng Văn E                | 2022-11-22       | 2025-11-21        |
+----+----------------------------+------------------+-------------------+
+-----+-----------------+
| gid | Thể_loại        |
+-----+-----------------+
| BK  | Bi kịch         |
| T   | Thơ             |
| TD  | Truyện dài      |
| TN  | Truyện ngắn     |
| TT  | Tiểu thuyết     |
+-----+-----------------+
+-----+------------------------------+-----------------+
| bid | Tên_sách                     | Thể_loại        |
+-----+------------------------------+-----------------+
|   1 | Anna Karenina                | Tiểu thuyết     |
|   2 | Biến hình                    | Truyện ngắn     |
|   3 | Chí Phèo                     | Tiểu thuyết     |
|   4 | Chiếc thuyền ngoài xa        | Tiểu thuyết     |
|   5 | Chiến tranh và hòa bình      | Tiểu thuyết     |
+-----+------------------------------+-----------------+
+-----+------------------------------+---------------------+
| bid | Tên_sách                     | Tác_giả             |
+-----+------------------------------+---------------------+
|   1 | Anna Karenina                | Leo Tolstoy         |
|   2 | Biến hình                    | Franz Kafka         |
|   3 | Chí Phèo                     | Nam Cao             |
|   4 | Chiếc thuyền ngoài xa        | Nguyễn Minh Châu    |
|   5 | Chiến tranh và hòa bình      | Leo Tolstoy         |
+-----+------------------------------+---------------------+
```

### d. 3 truy vấn nâng cao

```sql
-- Truy vấn thể loại và tác giả của cuốn sách mà khách hàng đang mượn
SELECT no.id id, khachhang.hovaten Họ_và_tên_khách_hàng, theloai.theloai Thể_loại, tacgia.hovaten Tác_giả FROM no 
LEFT JOIN khachhang ON no.id = khachhang.id
LEFT JOIN sach ON no.bid = sach.bid
LEFT JOIN theloai ON sach.gid = theloai.gid
LEFT JOIN tacgia ON sach.aid = tacgia.aid LIMIT 5;

-- Truy vấn sách đang mượn, ngày mượn và ngày trả (dựa trên ngày mượn và hạn mức) của khách hàng
SELECT no.id id, khachhang.hovaten Họ_và_tên_khách_hàng, 
sach.tensach Sách_mượn, no.ngaymuon Ngày_mượn, 
DATE_ADD(no.ngaymuon, INTERVAL FLOOR(hanmuc.hanmuc) DAY) Ngày_trả
FROM no 
LEFT JOIN khachhang ON no.id = khachhang.id
LEFT JOIN sach ON no.bid = sach.bid
LEFT JOIN hanmuc ON sach.did = hanmuc.did LIMIT 5;

-- Truy vấn số sách đang mượn của mỗi khách hàng
SELECT k.id id, k.hovaten Họ_và_tên_khách_hàng, COUNT(no.id) Số_sách_đang_mượn FROM no
LEFT JOIN khachhang k ON no.id = k.id GROUP BY k.id LIMIT 5;
```

Outputs

```
+----+----------------------------+-----------------+--------------------------+
| id | Họ_và_tên_khách_hàng       | Thể_loại        | Tác_giả                  |
+----+----------------------------+-----------------+--------------------------+
| 10 | Hồ Thị J                   | Tiểu thuyết     | Gabriel García Márquez   |
|  9 | Đỗ Văn I                   | Tiểu thuyết     | Gabriel García Márquez   |
|  8 | Bùi Thị H                  | Tiểu thuyết     | Charles Dickens          |
|  7 | Đặng Văn G                 | Bi kịch         | William Shakespeare      |
|  6 | Vũ Thị F                   | Tiểu thuyết     | Leo Tolstoy              |
+----+----------------------------+-----------------+--------------------------+
+----+----------------------------+-------------------------------+---------------+-------------+
| id | Họ_và_tên_khách_hàng       | Sách_mượn                     | Ngày_mượn     | Ngày_trả    |
+----+----------------------------+-------------------------------+---------------+-------------+
| 10 | Hồ Thị J                   | Trăm năm cô đơn               | 2023-07-11    | 2023-07-12  |
|  9 | Đỗ Văn I                   | Tình yêu thời dịch tả         | 2023-10-13    | 2023-10-18  |
|  8 | Bùi Thị H                  | Đại đoàn kết                  | 2023-02-19    | 2023-02-23  |
|  7 | Đặng Văn G                 | Romeo và Juliet               | 2023-07-08    | 2023-07-09  |
|  6 | Vũ Thị F                   | Chiến tranh và hòa bình       | 2023-08-08    | 2023-08-11  |
+----+----------------------------+-------------------------------+---------------+-------------+
+------+----------------------------+--------------------------+
| id   | Họ_và_tên_khách_hàng       | Số_sách_đang_mượn        |
+------+----------------------------+--------------------------+
|    1 | Nguyễn Văn A               |                        1 |
|    2 | Trần Thị B                 |                        1 |
|    3 | Lê Văn C                   |                        1 |
|    4 | Phạm Thị D                 |                        1 |
|    5 | Hoàng Văn E                |                        1 |
+------+----------------------------+--------------------------+
```