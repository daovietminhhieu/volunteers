
# Báo cáo Dự án Hệ thống Quản lý Tình nguyện Viên

## 1. Giới thiệu Dự án
Đây là một ứng dụng web full-stack để quản lý các hoạt động tình nguyện, kết nối giữa các tổ chức và tình nguyện viên. Dự án cung cấp các chức năng chính như đăng ký/đăng nhập, quản lý chiến dịch, ứng tuyển, chat thời gian thực và thông báo.

## 2. Cấu trúc Thư mục
```
final/
├── backend/               # Backend API
│   ├── controller/        # Controllers xử lý logic
│   ├── data/              # Dữ liệu lưu trữ dưới dạng JSON
│   ├── middleware/        # Middleware (auth, ...)
│   ├── routes/            # API Routes
│   ├── utils/             # Tiện ích (fileStore, ...)
│   ├── package.json       # Dependencies của backend
│   ├── server.js          # Entry point của server
│   └── socket.js          # Cấu hình Socket.io
├── public/                # Tệp tĩnh
│   └── html/              # Trang HTML tĩnh (volunteer home, org dashboard, ...)
├── src/                   # Frontend React
│   ├── context/           # Context API (AuthContext)
│   ├── pages/             # Trang React (Login, Register, ...)
│   ├── App.jsx            # App chính
│   └── main.jsx           # Entry point của React
├── package.json           # Dependencies của frontend
└── vite.config.js         # Cấu hình Vite
```

## 3. Công nghệ Sử dụng

### Frontend
- **React 19**: Thư viện xây dựng giao diện
- **Vite**: Build tool và dev server
- **React Router DOM 7**: Điều hướng trang

### Backend
- **Express.js 5**: Web framework cho Node.js
- **Socket.io**: Realtime communication (chat, thông báo)
- **JSON Web Token (JWT)**: Xác thực người dùng
- **CORS**: Cross-Origin Resource Sharing

### Lưu trữ dữ liệu
- **JSON Files**: Lưu trữ dữ liệu trong các tệp JSON (dễ triển khai, phù hợp cho dự án nhỏ)

## 4. Chức năng Chính

### 4.1 Xác thực người dùng
- **Đăng ký**: Người dùng có thể đăng ký với vai trò "volunteer" hoặc "organization"
- **Đăng nhập**: Đăng nhập bằng email và mật khẩu, nhận về JWT token
- **AuthContext**: Quản lý trạng thái xác thực trên frontend

### 4.2 Quản lý Chiến dịch (Organization)
- Tạo chiến dịch mới (title, description, category, skills, vacancies, timeline, location, ...)
- Xem danh sách chiến dịch
- Cập nhật và xóa chiến dịch
- Xem thống kê trên dashboard (số chiến dịch, số ứng viên được duyệt, chờ duyệt)

### 4.3 Ứng tuyển Chiến dịch (Volunteer)
- Xem danh sách chiến dịch
- Ứng tuyển chiến dịch
- Xem trạng thái ứng tuyển
- Cập nhật hồ sơ cá nhân

### 4.4 Quản lý Ứng viên
- Xem danh sách ứng viên, lọc theo trạng thái (Approved/Pending) và chiến dịch
- Duyệt/từ chối ứng viên
- Điểm danh tình nguyện viên

### 4.5 Chat Thời gian Thực
- Tạo cuộc trò chuyện mới giữa 2 người dùng
- Gửi và nhận tin nhắn theo thời gian thực bằng Socket.io
- Xem lịch sử tin nhắn

### 4.6 Thông báo
- Thông báo khi có chiến dịch mới (tới tất cả người dùng)
- Thông báo khi ứng tuyển được duyệt (tới tình nguyện viên cụ thể)
- Thông báo nhắc nhở trước khi chiến dịch bắt đầu (chạy mỗi giờ)
- Thông báo được gửi qua Socket.io để nhận theo thời gian thực

## 5. Dữ liệu Lưu trữ

| Tệp JSON          | Mô tả                                   |
|-------------------|-----------------------------------------|
| users.json        | Thông tin người dùng                    |
| campaigns.json    | Thông tin các chiến dịch tình nguyện    |
| candidates.json   | Thông tin các ứng viên cho chiến dịch  |
| conversations.json| Danh sách các cuộc trò chuyện           |
| messages.json     | Tin nhắn trong các cuộc trò chuyện     |
| notifications.json| Thông báo cho người dùng                |

## 6. Cách Chạy Dự án

### Chạy Backend
```bash
cd backend
npm install
npm start
# Server sẽ chạy trên http://127.0.0.1:3000
```

### Chạy Frontend
```bash
# Ở thư mục gốc
npm install
npm run dev
# Frontend sẽ chạy trên http://localhost:5173
```

## 7. Điểm mạnh và Điểm cần Cải thiện

### Điểm mạnh
- Cấu trúc rõ ràng, dễ hiểu
- Sử dụng Socket.io cho tính năng realtime (chat, thông báo)
- API RESTful được thiết kế tốt
- Hỗ trợ nhiều vai trò người dùng (volunteer, organization)

### Điểm cần Cải thiện
- **Bảo mật**: Mật khẩu lưu trữ dưới dạng plaintext, cần mã hóa bằng bcrypt
- **Lưu trữ dữ liệu**: Sử dụng JSON files không phù hợp cho dự án lớn, cần thay thế bằng cơ sở dữ liệu (MongoDB, PostgreSQL)
- **Validation**: Cần thêm validation cho dữ liệu đầu vào
- **Testing**: Chưa có unit test và integration test
- **Error Handling**: Cải thiện error handling và thông báo lỗi cho người dùng
