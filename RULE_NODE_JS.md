# Quy định về Cấu trúc Source và Coding Conventions cho Dự án Node.js

## Giới thiệu
- Đây là tài liệu hướng dẫn về cấu trúc thư mục và quy tắc viết mã nguồn cho dự án Node.js.
- Mục tiêu: Xây dựng ứng dụng Node.js chất lượng cao, dễ bảo trì và mở rộng.
- Đối tượng: Lập trình viên JavaScript/TypeScript muốn phát triển ứng dụng Node.js chuyên nghiệp.
- Tài liệu này giúp hiểu rõ cấu trúc thư mục, quy tắc viết mã nguồn và quy trình phát triển dự án Node.js.
- Phiên bản hiện hành: 1.0.0-alpha
- Ngày cập nhật: 27/02/2025
- Thuộc quyền sở hữu và biên soạn bởi [Dương Thái Bảo/Kennex](https://github.com/Kennex666).

## Mục lục
1. [Cấu trúc Thư mục](#1-cấu-trúc-thư-mục)
    1.1. [Thư mục /config](#11-thư-mục-config)
    1.2. [Thư mục /middlewares](#12-thư-mục-middlewares)
    1.3. [Thư mục /utils](#13-thư-mục-utils)
2. [Coding Conventions](#2-coding-conventions)
    2.1. [Đặt tên](#21-đặt-tên)
    2.2. [Quy tắc Indentation](#22-quy-tắc-indentation)
    2.3. [Commenting](#23-commenting)
    2.4. [Quản lý Dependencies](#24-quản-lý-dependencies)
    2.5. [Kiểm tra Mã Nguồn](#25-kiểm-tra-mã-nguồn)
3. [Sự Tương Tác Giữa Các Module](#3-sự-tương-tác-giữa-các-module)
4. [Hướng dẫn Cài đặt Môi trường Phát triển](#4-hướng-dẫn-cài-đặt-môi-trường-phát-triển)
5. [Quy trình Phát triển](#5-quy-trình-phát-triển)
6. [Được Ghi Nhớ](#6-được-ghi-nhớ)
7. [Quy định về naming branch và commit](#7-quy-định-về-naming-branch-và-commit)
    7.1. [Branch](#71-branch)
        7.1.1. [Hướng dẫn đặt tên branch](#711-hướng-dẫn-đặt-tên-branch)
        7.1.2. [Các tiền tố tên công việc](#712-các-tiền-tố-tên-công-việc)
    7.2. [Commit](#72-commit)
        7.2.1. [Hướng dẫn đặt tên commit](#721-hướng-dẫn-đặt-tên-commit)
        7.2.2. [Các tiền tố tên công việc](#722-các-tiền-tố-tên-công-việc)
8. [Quy định về Pull Request](#8-quy-định-về-pull-request)
    8.1. [Hướng dẫn tạo Pull Request](#81-hướng-dẫn-tạo-pull-request)
    8.2. [Hướng dẫn về đặt tên Pull Request](#82-hướng-dẫn-về-đặt-tên-pull-request)

## 1. Cấu trúc Thư mục
```
/project-root
│
├── /src
│   ├── /config                    # Cấu hình ứng dụng
│   ├── /controllers               # Chứa các Controller xử lý request
│   ├── /models                    # Chứa các model cho cơ sở dữ liệu
│   ├── /routes                    # Chứa các route của ứng dụng
│   ├── /services                  # Chứa các service xử lý logic nghiệp vụ
│   ├── /middlewares               # Chứa các middleware xử lý request
│   ├── /utils                     # Chứa các hàm tiện ích chung
│   ├── /exceptions                # Chứa các class xử lý lỗi tùy chỉnh
│   ├── /database                  # Chứa các file kết nối database
│   ├── app.js                     # File khởi động ứng dụng
│
├── /tests                         # Chứa các test cases
├── /docs                          # Tài liệu dự án
├── .env                           # Biến môi trường
├── package.json                   # File cấu hình npm
├── README.md                      # Hướng dẫn dự án
```

### 1.1. **Thư mục /config**
- Chứa các tệp cấu hình như kết nối database, cấu hình JWT, Redis, môi trường.

### 1.2. **Thư mục /middlewares**
- Chứa các middleware như xác thực JWT, kiểm tra quyền truy cập.

### 1.3. **Thư mục /utils**
- Chứa các hàm tiện ích như xử lý chuỗi, định dạng ngày tháng.

## 2. Coding Conventions
### 2.1. Đặt tên
- Sử dụng **camelCase** cho biến và phương thức.
- Sử dụng **PascalCase** cho class.
- Sử dụng **kebab-case** cho tên file JavaScript.

### 2.2. Quy tắc Indentation
- Sử dụng **tab** thay vì dấu cách.

### 2.3. Commenting
- Sử dụng JSDoc để viết tài liệu.
```js
/**
 * Xác thực người dùng bằng token JWT
 * @param {Request} req - Request từ client
 * @param {Response} res - Response từ server
 * @param {Function} next - Middleware tiếp theo
 */
```

### 2.4. Quản lý Dependencies
- Sử dụng **npm** hoặc **yarn** để quản lý dependencies.
- Chỉ cài đặt dependencies thực sự cần thiết.

### 2.5. Kiểm tra Mã Nguồn
- Viết **unit test** với **Jest** hoặc **Mocha**.
- Sử dụng **ESLint** để kiểm tra coding style.

## 3. Sự Tương Tác Giữa Các Module
- **Controller** gọi **Service** để xử lý logic nghiệp vụ.
- **Service** gọi **Model** để truy xuất dữ liệu từ database.
- **Middleware** xử lý trước khi request tới Controller.
- **Utils** được sử dụng bởi nhiều module khác.

## 4. Hướng dẫn Cài đặt Môi trường Phát triển
- Cài đặt **Node.js** phiên bản mới nhất.
- Cài đặt **MongoDB** (hoặc PostgreSQL nếu sử dụng SQL).
- Sử dụng **Postman** để kiểm thử API.

## 5. Quy trình Phát triển
- **Mỗi tính năng mới** phải có một nhánh Git riêng.
- **Commit rõ ràng**, dễ hiểu.
- **Code phải được review** trước khi merge.


## 6. Được Ghi Nhớ
- Luôn giữ mã nguồn sạch sẽ và có thể tái sử dụng.
- Thực hiện kiểm thử đầy đủ trước khi triển khai.


## 7. Quy định về naming branch và commit 
### 7.1. Branch
#### 7.1.1. Hướng dẫn đặt tên branch
- Tên branch phải mô tả rõ ràng nội dung công việc.
- <Tên của công việc>/<Mô tả công việc>
- Ví dụ: `feature/add-user-management`, `bugfix/fix-login-issue`
#### 7.1.2. Các tiền tố tên công việc
- `feature/`: Công việc liên quan đến việc thêm tính năng mới.
- `bugfix/`: Công việc liên quan đến việc sửa lỗi.
- `hotfix/`: Công việc liên quan đến việc sửa lỗi nhanh.
- `refactor/`: Công việc liên quan đến việc tái cấu trúc mã nguồn.
- `docs/`: Công việc liên quan đến việc cập nhật tài liệu.
- `style/`: Công việc liên quan đến việc cập nhật style mã nguồn.
- `test/`: Công việc liên quan đến việc viết test.

### 7.2. Commit
#### 7.2.1. Hướng dẫn đặt tên commit
- Tên commit phải mô tả rõ ràng nội dung công việc.
- Tiền tố tên công việc không viết hoa. (add, feat, fix, refactor, docs, style, test)
- <Tên công việc>: <Mô tả công việc>
- Ví dụ: `feat: Add user management feature`, `bugfix: Fix login issue`
##### 7.2.2. Các tiền tố tên công việc
- `add`: Thêm tính năng mới.
- `feat`: Thêm tính năng mới.
- `fix`: Sửa lỗi.
- `refactor`: Tái cấu trúc mã nguồn.
- `docs`: Cập nhật tài liệu.
- `style`: Cập nhật style mã nguồn.
- `test`: Viết test.
- `chore`: Công việc không liên quan đến việc thay đổi mã nguồn.
- `revert`: Revert lại commit trước đó.
- `merge`: Merge branch.
- `deploy`: Deploy ứng dụng.
- `release`: Release phiên bản.
- `hotfix`: Sửa lỗi nhanh.
- `config`: Cấu hình.
- `update`: Cập nhật.
- `remove`: Xóa.
- `clean`: Dọn dẹp.
- `move`: Di chuyển.
- `rename`: Đổi tên.
- `upgrade`: Nâng cấp.
- `downgrade`: Hạ cấp.
- `init`: Khởi tạo.
- `improve`: Cải thiện.
- `make`: Tạo ra.
- `change`: Thay đổi một cài đặt
- `correct`: Sửa lỗi chính tả.
- `ci`: Cập nhật cấu hình CI/CD.
- `build`: Cập nhật cấu hình build.
- `reformat`: Định dạng lại mã nguồn.
- `resolve`: Giải quyết một vấn đề.
- `optimize`: Tối ưu hóa mã nguồn.

## 8. Quy định về Pull Request
### 8.1. Hướng dẫn tạo Pull Request
- Sau khi thực hiện và test các thay đổi, tạo Pull Request (PR) để hợp nhất vào nhánh chính.
- Mô tả rõ ràng nội dung công việc đã thực hiện trong PR.
- Gắn nhãn (label) cho PR để phân loại công việc.
- Đặt tên PR: <Tên công việc>: <Mô tả công việc>
### 8.2. Hướng dẫn về đặt tên Pull Request
- Tên PR phải mô tả rõ ràng nội dung công việc.
- <Tên công việc>: <Mô tả công việc>
- Ví dụ: `SCRUM-01: Add user management feature`, `SCRUM-02: Fix login issue`
- Đối với các tính năng WIP (Work In Progress), thêm tiền tố `[WIP]` vào tên PR.
- Khi nào cần WIP: Khi công việc cần thời gian để hoàn thành, hoặc cần phải chia nhỏ ra thành các công việc nhỏ hơn.
- Khi công việc đã hoàn thành, xóa tiền tố `[WIP]` ra khỏi tên PR.

