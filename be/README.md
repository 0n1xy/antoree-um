# Quản Lý Người Dùng API (Laravel + JWT Authentication)

## 📌 Giới Thiệu

Dự án này là API Laravel dùng **JWT Authentication** để quản lý người dùng, bao gồm **đăng ký, đăng nhập, phân quyền admin và user, CRUD người dùng, bảo vệ API bằng middleware**.

---

## 🚀 Tính Năng

-   **Đăng ký & Đăng nhập**
-   **Xác thực JWT & Refresh Token**
-   **Phân quyền (Admin & User)**
-   **Bảo vệ API bằng middleware**
-   **CRUD người dùng**
-   **Seeder tạo 20 người dùng (1 Admin + 19 User)**
-   **Tài khoản Admin mặc định**

---

## 📂 Hướng Dẫn Cài Đặt

### **1️⃣ Clone Dự án**

```sh
git clone https://github.com/yourusername/usermanagement.git
cd usermanagement
```

### **2️⃣ Cài Đặt Dependencies**

```sh
composer install
```

### **3️⃣ Cấu Hình Môi Trường**

```sh
cp .env.example .env
```

Sau đó, chỉnh sửa file `.env` để kết nối với database:

```env
DB_CONNECTION=mysql
DB_HOST=um_mysql
DB_PORT=3306
DB_DATABASE=laravel
DB_USERNAME=onixy
DB_PASSWORD=root
```

### **4️⃣ Tạo Application Key**

```sh
php artisan key:generate
```

### **5️⃣ Chạy Migration & Seed Database**

```sh
php artisan migrate --seed
```

✅ **Tạo bảng trong database**  
✅ **Tạo 20 người dùng (1 Admin + 19 User)**

### **6️⃣ Tạo JWT Secret Key**

```sh
php artisan jwt:secret
```

### **7️⃣ Chạy Server**

```sh
php artisan serve
```

API sẽ chạy tại:

```
http://localhost:8000
```

---

## 🔐 **Sử Dụng API**

### **📌 1️⃣ Đăng ký**

```http
POST /auth/register
```

**Body:**

```json
{
    "name": "Nguyen Van A",
    "email": "nguyenvana@example.com",
    "password": "password123"
}
```

### **📌 2️⃣ Đăng nhập**

```http
POST /auth/login
```

**Body:**

```json
{
    "email": "admin@example.com",
    "password": "password123"
}
```

**Response:**

```json
{
    "access_token": "your-jwt-token",
    "refresh_token": "your-refresh-token",
    "token_type": "bearer",
    "expires_in": 3600,
    "role": "admin"
}
```

### **📌 3️⃣ Lấy Thông Tin User Hiện Tại (Cần Xác Thực)**

```http
GET /auth/me
```

**Headers:**

```http
Authorization: Bearer your-jwt-token
```

### **📌 4️⃣ Lấy Danh Sách Users (Admin Only)**

```http
GET /admin/users
```

**Headers:**

```http
Authorization: Bearer your-jwt-token
```

### **📌 5️⃣ Đăng Xuất**

```http
POST /auth/logout
```

**Headers:**

```http
Authorization: Bearer your-jwt-token
```

---

## 👨‍💻 **Tài Khoản Mặc Định**

Sau khi seed database, dùng các tài khoản sau:

### **Admin**

```
Email: admin@example.com
Password: password123
Role: Admin
```

### **User**

```
Email: user@example.com
Password: password123
Role: User
```

---

## **📌 Lệnh Hữu Ích**

### **Xoá và Seed Lại Database**

```sh
php artisan migrate:fresh --seed
```

✅ Xóa và tạo lại bảng  
✅ Seed 20 users (1 Admin + 19 User)

---

## 👨‍🏫 **Cóng Góp**

Hãy đóng góp vào dự án bằng cách tạo pull request!

---

## 📜 **Giấy Phép**

Dự án được phát hành theo giấy phép **MIT License**.

---

## **🚀 Bạn Đã Sẵn Sàng Sử Dụng API!**

Hãy chạy:

```sh
php artisan serve
```

Và test API bằng **Postman** hoặc **cURL**.

Nếu gặp vấn đề, hãy liên hệ với chúng tôi! 🚀🔥
