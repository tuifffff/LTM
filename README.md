

## Giới thiệu
Project được thiết kế theo mô hình *3-layer architecture (Controller – Service – DAO/Entity)* giúp dễ dàng mở rộng, bảo trì và tích hợp cơ sở dữ liệu.

---

## Cấu trúc thư mục
```
OOP_MatchingMemory/
├── .idea/                     # Cấu hình IntelliJ IDEA
├── out/                       # Thư mục chứa file biên dịch (.class)
├── src/
│   ├── resources/             # Tài nguyên tĩnh (ảnh, icon, file config,...)
│   ├── client/
│   │   ├── controller/        # Xử lý logic phía client
│   │   ├── service/           # Kết nối socket và xử lý dữ liệu
│   │   ├── view/              # Giao diện người dùng hoặc console client
│   │   └── ClientRunApp.java  # Điểm khởi chạy ứng dụng client
│   ├── constants/             # Khai báo hằng số dùng chung
│   ├── entity/                # Các lớp mô hình dữ liệu (POJO)
│   ├── server/
│   │   ├── controller/        # Xử lý logic phía server
│   │   ├── dao/               # Tầng truy xuất dữ liệu (MySQL)
│   │   └── ServerRun.java     # Điểm khởi chạy server
│   └── ...
├── .gitignore                 # Loại trừ file khi push Git
└── LTM.iml                    # File cấu hình IntelliJ
```
---

## Công nghệ sử dụng

| Thành phần            | Phiên bản / Công nghệ                     |
| --------------------- |-------------------------------------------|
| *JDK*               | 23 (Java SE 21)                           |
| *MySQL Connector/J* | 8.4.0                                     |
| *IDE*               | IntelliJ IDEA / NetBeans                  |
| *Mô hình*           | Client–Server (Socket TCP)                |
| *CSDL*              | MySQL 8.x                                 |
| *Kiến trúc*         | MVC – 3 tầng (Controller / Service / DAO) |

---

## Hướng dẫn chạy project

### 1️ Chuẩn bị môi trường

* Cài *JDK 23*
* Cài *MySQL Server*
* Tạo database (ví dụ: OOP_db)
* Import thư viện **mysql-connector-j-8.4.0.jar**
  → File > Project Structure > Libraries > Add

---

### 2️ Cấu hình kết nối cơ sở dữ liệu

Trong các file thuộc thư mục server/dao, chỉnh thông tin kết nối:

String URL = "jdbc:mysql://localhost:3306/your_db";
String USER = "root";
String PASSWORD = "your_password";

---

### 3️ Chạy Server

* Mở file: src/server/ServerRun.java
* Chạy hàm main()
* Server sẽ khởi động và lắng nghe tại localhost:8888 (hoặc cổng khác nếu cấu hình lại)

---

### 4️ Chạy Client

* Mở file: src/client/ClientRunApp.java
* Chạy hàm main()
* Client sẽ kết nối đến server qua socket (theo IP và port định sẵn)

---

## Kiến trúc tổng quan

mermaid
graph TD
A[Client View] --> B[Client Controller]
B --> C[Client Service]
C -->|Socket| D[Server Controller]
D --> E[Server DAO]
E --> F[(MySQL Database)]

---

## Một số chức năng chính

* Giao tiếp *Socket TCP* giữa client và server
* Hỗ trợ *nhiều client kết nối song song*
* Gửi/nhận dữ liệu dạng *Object (ObjectInputStream / ObjectOutputStream)*
* Lưu trữ, xác thực thông tin người dùng qua *MySQL*
* Có thể mở rộng để gửi tin nhắn, file, hoặc xử lý yêu cầu phức tạp hơn

---

## Lưu ý khi phát triển

* Không commit thư mục out/ hoặc .idea/
* Không nên đẩy file .iml lên GitHub
* File .gitignore nên có:


/.idea/
/out/
*.iml

* Đảm bảo client và server sử dụng *cùng phiên bản JDK*

---

## Tham khảo

* [Java 23 Documentation](https://docs.oracle.com/en/java/javase/21/)
* [MySQL Connector/J 8.4.0](https://dev.mysql.com/downloads/connector/j/)
* [Socket Programming in Java (Oracle Guide)](https://docs.oracle.com/javase/tutorial/networking/sockets/)

---