# postman-juice-shop-api-testing

# API Testing với Postman - OWASP Juice Shop

## 1. Giới thiệu

Bài thực hành tìm hiểu và sử dụng Postman để thực hiện kiểm thử các REST API của ứng dụng OWASP Juice Shop.

Trong bài thực hành, các API được kiểm thử bao gồm các chức năng:

* Lấy danh sách sản phẩm
* Đăng nhập người dùng
* Thêm sản phẩm
* Lấy thông tin giỏ hàng
* Xóa sản phẩm khỏi giỏ hàng
* Chỉnh sửa thông tin sản phẩm

Các request được thực hiện bằng Postman và kết quả được kiểm tra thông qua HTTP Status Code và Response trả về từ server.

---

## 2. Công cụ sử dụng

| Công cụ          | Mục đích                               |
| ---------------- | -------------------------------------- |
| OWASP Juice Shop | Ứng dụng cung cấp REST API để kiểm thử |
| Postman          | Gửi request và kiểm thử API            |
| GitHub           | Lưu trữ source và báo cáo              |
| Markdown         | Viết báo cáo                           |

---

## 3. Môi trường thực hiện

Ứng dụng OWASP Juice Shop được chạy trên máy local.

Base URL:

```text
http://localhost:3000
```

Công cụ kiểm thử:

```text
Postman
```

---

# 4. Danh sách API kiểm thử

| STT | Method | API                     | Chức năng                  |
| --- | ------ | ----------------------- | -------------------------- |
| 1   | GET    | `/api/Products`         | Lấy danh sách sản phẩm     |
| 2   | POST   | `/rest/user/login`      | Đăng nhập                  |
| 3   | POST   | `/api/Products`         | Thêm sản phẩm              |
| 4   | GET    | `/rest/basket/{id}`     | Lấy giỏ hàng               |
| 5   | DELETE | `/api/BasketItems/{id}` | Xóa sản phẩm khỏi giỏ hàng |
| 6   | PUT    | `/api/Products/{id}`    | Chỉnh sửa sản phẩm         |

---

# 5. Chi tiết kiểm thử API

## 5.1. GET - Lấy danh sách sản phẩm

### Request

```http
GET http://localhost:3000/api/Products
```

### Mục đích

Sử dụng API để lấy danh sách các sản phẩm hiện có trong hệ thống.

### Kết quả mong đợi

Server trả về danh sách sản phẩm và HTTP Status Code thành công.

### Kết quả thực tế

```text
Status: 200 OK
```

### Hình ảnh minh họa

<img width="1911" height="898" alt="Screenshot 2026-10-07 101340" src="https://github.com/user-attachments/assets/4a4e6873-1771-4674-a3af-bf3b9100b7a7" />


---

# 5.2. POST - Đăng nhập

### Request

```http
POST http://localhost:3000/rest/user/login
```

### Body

```json
{
    "email": "admin@juice-sh.op",
    "password": "********"
}
```

### Mục đích

Thực hiện đăng nhập vào hệ thống và nhận JWT Token để sử dụng cho các API yêu cầu authentication.

### Kết quả mong đợi

Server trả về thông tin authentication và JWT Token.

### Kết quả thực tế

```text
Login successful
JWT Token received
```

Token được sử dụng trong Header của các request cần xác thực:

```http
Authorization: Bearer <JWT_TOKEN>
```

### Hình ảnh minh họa

<img width="1904" height="926" alt="Screenshot 2026-10-07 102118" src="https://github.com/user-attachments/assets/8fc65ab0-d684-4b74-b49a-2ceae525de0b" />


> Lưu ý: Không công khai JWT Token thật trong ảnh chụp hoặc README khi đưa repository lên GitHub.

---

# 5.3. POST - Thêm sản phẩm

### Request

```http
POST http://localhost:3000/api/Products
```

### Header

```http
Content-Type: application/json
Authorization: Bearer <JWT_TOKEN>
```

### Body

```json
{
    "name": "Postman Test Product",
    "description": "Product created using Postman",
    "price": 99.99
}
```

### Mục đích

Kiểm tra khả năng tạo một sản phẩm mới thông qua API.

### Kết quả mong đợi

Server tiếp nhận dữ liệu và tạo sản phẩm mới.

### Kết quả thực tế

```text
Request successful
Product created
```

### Hình ảnh minh họa

<img width="1909" height="904" alt="Screenshot 2026-10-07 102051" src="https://github.com/user-attachments/assets/036185e7-854e-457e-acd4-242e0304f6d3" />


---

# 5.4. GET - Lấy giỏ hàng

### Request

```http
GET http://localhost:3000/rest/basket/{id}
```

Ví dụ:

```http
GET http://localhost:3000/rest/basket/1
```

### Header

```http
Authorization: Bearer <JWT_TOKEN>
```

### Mục đích

Lấy danh sách sản phẩm hiện đang có trong giỏ hàng của người dùng.

### Kết quả mong đợi

Server trả về thông tin giỏ hàng và các sản phẩm trong giỏ.

### Kết quả thực tế

```text
Status: 200 OK
```

### Hình ảnh minh họa

<img width="1910" height="928" alt="Screenshot 2026-10-07 103632" src="https://github.com/user-attachments/assets/31b290fd-ac7b-4545-a85d-1c1014b896e7" />


---

# 5.5. DELETE - Xóa sản phẩm khỏi giỏ hàng

### Request

```http
DELETE http://localhost:3000/api/BasketItems/{id}
```

Trong đó `{id}` là ID của BasketItem.

Ví dụ:

```http
DELETE http://localhost:3000/api/BasketItems/10
```

### Header

```http
Authorization: Bearer <JWT_TOKEN>
```

### Mục đích

Xóa một sản phẩm khỏi giỏ hàng.

### Kết quả mong đợi

Sản phẩm được xóa khỏi giỏ hàng.

### Kết quả thực tế

```text
Delete successful
```

Sau khi xóa, có thể sử dụng API:

```http
GET http://localhost:3000/rest/basket/1
```

để kiểm tra lại giỏ hàng.

### Hình ảnh minh họa

<img width="1910" height="871" alt="Screenshot 2026-10-07 103624" src="https://github.com/user-attachments/assets/383a4ca8-b209-400b-a704-ba08dbc61cf4" />


---

# 5.6. PUT - Chỉnh sửa sản phẩm

### Request

```http
PUT http://localhost:3000/api/Products/{id}
```

Ví dụ:

```http
PUT http://localhost:3000/api/Products/1
```

### Header

```http
Content-Type: application/json
Authorization: Bearer <JWT_TOKEN>
```

### Body

```json
{
    "name": "Postman Test Product Updated",
    "description": "Product updated using Postman",
    "price": 149.99
}
```

### Mục đích

Kiểm tra khả năng cập nhật thông tin sản phẩm thông qua API.

### Kết quả mong đợi

Thông tin sản phẩm được cập nhật thành công.

### Kết quả thực tế

```text
Update successful
```

### Hình ảnh minh họa

<img width="1901" height="874" alt="Screenshot 2026-10-07 110855" src="https://github.com/user-attachments/assets/69a4ca84-dc34-45f2-8009-f836a0ddb030" />


---

# 6. Authentication

Một số API của Juice Shop yêu cầu người dùng phải được xác thực.

Quy trình authentication được thực hiện như sau:

```text
POST /rest/user/login
        |
        v
   JWT Token
        |
        v
Authorization: Bearer <JWT>
        |
        v
Protected API
```

JWT Token được sử dụng để xác thực người dùng khi thực hiện các API yêu cầu quyền truy cập.

---

# 7. Tổng kết kết quả

Sau khi thực hiện kiểm thử, các API đã được kiểm tra thành công:

| STT | Method | Chức năng                  | Kết quả    |
| --- | ------ | -------------------------- | ---------- |
| 1   | GET    | Lấy danh sách sản phẩm     | Thành công |
| 2   | POST   | Đăng nhập                  | Thành công |
| 3   | POST   | Thêm sản phẩm              | Thành công |
| 4   | GET    | Lấy giỏ hàng               | Thành công |
| 5   | DELETE | Xóa sản phẩm khỏi giỏ hàng | Thành công |
| 6   | PUT    | Chỉnh sửa sản phẩm         | Thành công |

Thông qua bài thực hành, em đã tìm hiểu cách sử dụng Postman để gửi HTTP Request, kiểm tra Response, HTTP Status Code, truyền dữ liệu JSON và sử dụng JWT Token để xác thực với các API được bảo vệ.

---

# 8. Postman Collection

Postman Collection được lưu tại:

```text
postman/Juice-Shop-API.postman_collection.json
```

Có thể import Collection này vào Postman để thực hiện lại các API đã kiểm thử.

---

# 9. Cấu trúc Repository

```text
postman-juice-shop-api-testing/
│
├── README.md

```

