# Quy định về Cấu trúc Source và Coding Conventions cho Dự án Spring Boot và Thymeleaf
## Giới thiệu
- Đây là tài liệu hướng dẫn về cấu trúc thư mục và quy tắc viết mã nguồn cho dự án Spring Boot và Thymeleaf.
- Mục tiêu: Xây dựng ứng dụng Spring Boot chất lượng cao, dễ bảo trì và mở rộng.
- Đối tượng: Lập trình viên Java muốn học cách phát triển ứng dụng Spring Boot chuyên nghiệp.
- Tài liệu này sẽ giúp bạn hiểu rõ cấu trúc thư mục, quy tắc viết mã nguồn và quy trình phát triển dự án Spring Boot.
- Phiên bản hiện hành: 1.0.0-alpha
- Ngày cập nhật: 04/01/2025
- Thuộc quyền sở hữu và biên soạn bởi [Dương Thái Bảo/Kennex](https://github.com/Kennex666).

## Mục lục
1. [Cấu trúc Thư mục](#1-cấu-trúc-thư-mục)
    1.1. [Package /config](#11-package-config)
    1.2. [Package /exception](#12-package-exception)
    1.3. [Package /utilities](#13-package-utilities)
2. [Coding Conventions](#2-coding-conventions)
    2.1. [Đặt tên](#21-đặt-tên)
    2.2. [Quy tắc Indentation](#22-quy-tắc-indentation)
    2.3. [Commenting](#23-commenting)
    2.4. [Quản lý Dependencies](#24-quản-lý-dependencies)
    2.5. [Kiểm tra Mã Nguồn](#25-kiểm-tra-mã-nguồn)
3. [Sự Tương Tác Giữa Các Package](#3-sự-tương-tác-giữa-các-package)
    3.1. [Package `entities`](#31-package-entities)
    3.2. [Package `repository`](#32-package-repository)
    3.3. [Package `service`](#33-package-service)
    3.4. [Package `service.impl`](#34-package-serviceimpl)
    3.5. [Package `controller`](#35-package-controller)
    3.6. [Package `utilities`](#36-package-utilities)
    3.7. [Package `exception`](#37-package-exception)
4. [Hướng dẫn Cài đặt Môi trường Phát triển](#4-hướng-dẫn-cài-đặt-môi-trường-phát-triển)
5. [Quy trình Phát triển](#5-quy-trình-phát-triển)
    5.1. [Quy trịnh làm việc với Git](#51-quy-trịnh-làm-việc-với-git)
    5.2. [Quy trình Review](#52-quy-trình-review)
    5.3. [Template Pull Request](#53-template-pull-request)
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
│   ├── /main
│   │   ├── /java
│   │   │   └── /com
│   │   │       └── example
│   │   │           └── project
│   │   │               ├── Application.java            # File chính khởi động Spring Boot
│   │   │               ├── /config                     # Thư mục chứa các cấu hình Spring
│   │   │               ├── /controller                # Thư mục chứa các Controller
│   │   │               │   └── UserController.java      # Ví dụ Controller cho người dùng
│   │   │               ├── /service                   # Thư mục chứa các interface Service
│   │   │               │   └── UserService.java        # Ví dụ interface cho nghiệp vụ người dùng
│   │   │               ├── /service/impl              # Thư mục chứa các lớp triển khai Service
│   │   │               │   └── UserServiceImpl.java     # Triển khai của UserService
│   │   │               ├── /repository                # Thư mục chứa các Repository
│   │   │               │   └── UserRepository.java      # Ví dụ Repository cho người dùng
│   │   │               ├── /entities                  # Thư mục chứa các Entity
│   │   │               │   └── User.java                # Entity cho người dùng
│   │   │               ├── /utilities                  # Thư mục chứa các hàm tiện ích chung
│   │   │               │   └── UtilityClass.java        # Ví dụ hàm tiện ích
│   │   │               └── /exception                  # Thư mục chứa các exception tùy chỉnh
│   │   │                   └── CustomException.java      # Ví dụ exception tùy chỉnh
│   │   └── /resources
│   │       ├── /templates                             # Thư mục chứa các file Thymeleaf (HTML)
│   │       │    └── user.html                         # Ví dụ template cho trang người dùng
│   │       ├── /static                                # Thư mục chứa tài nguyên tĩnh (CSS, JS, hình ảnh)
│   │       └── application.properties                 # File cấu hình của ứng dụng
│   └── /test                                          # Thư mục chứa tests
│       └── /java
│           └── /com
│               └── example
│                   └── project
│                       ├── /service                   # Các test cho Service
│                       └── /controller                # Các test cho Controller
└── /docs                                              # Tài liệu dự án
```
### 1.1. **Package **/config

Chứa các lớp cấu hình như:

Cấu hình bảo mật: Ví dụ SecurityConfig.java sử dụng Spring Security.

Cấu hình datasource: Ví dụ DataSourceConfig.java để cấu hình kết nối cơ sở dữ liệu.

Cấu hình chung: Các cấu hình khác như cấu hình CORS, Message Source.

### 1.2. **Package **/exception

Bổ sung: Khuyến khích sử dụng @ControllerAdvice và @ExceptionHandler để xử lý lỗi toàn cục hoặc tùy chỉnh thông báo lỗi trả về API.
```java
@ControllerAdvice
public class GlobalExceptionHandler {
    @ExceptionHandler(CustomException.class)
    public ResponseEntity<String> handleCustomException(CustomException ex) {
        return new ResponseEntity<>(ex.getMessage(), HttpStatus.BAD_REQUEST);
    }
}
```

### 1.3. **Package **/utilities

Lưu ý: Không lạm dụng package này như một "bãi rác" cho các chức năng không liên quan. Chỉ nên chứa các hàm:

Xử lý chuỗi (StringUtils).

Định dạng ngày (DateUtils).

Chuyển đổi kiểu dữ liệu (ConverterUtils).

...

## 2. Coding Conventions

### 2.1. Đặt tên
- Sử dụng **camelCase** cho tên biến và phương thức.
- Sử dụng **PascalCase** cho tên lớp và giao diện.
- Tên file nên sử dụng **PascalCase** cho các lớp (chẳng hạn: `UserService.java`).

### 2.2. Quy tắc Indentation
- Sử dụng tab cho Indentation, không dùng dấu cách.

### 2.3. Commenting
- Viết bình luận cho các phương thức và lớp phức tạp để giải thích chức năng của chúng.
- Sử dụng `//` cho bình luận dòng đơn và `/* ... */` cho bình luận nhiều dòng.
- Viết tên người thực hiện tính năng và ngày thực hiện ở đầu feature.
Ví dụ:
```java
/**
 * UserService interface defines the operations that can be performed related to User entity.
 * It provides methods to register a new user and get user details by id.
 *
 * @author Kennex
 * @since 2025-01-01
 */
```

Khuyến khích sử dụng JavaDoc đầy đủ với các tag phổ biến:

```java
/**
 * Registers a new user in the system.
 *
 * @param user the user entity to be registered
 * @return the registered user entity
 * @throws CustomException if the user already exists
 */
User registerUser(User user) throws CustomException;
```

### 2.4. Quản lý Dependencies
- Sử dụng Maven để quản lý dependencies.

- Nên tận dụng các Spring Boot Starter:

 * spring-boot-starter-data-jpa: Quản lý database.

 * spring-boot-starter-thymeleaf: Tích hợp Thymeleaf.

 * spring-boot-starter-web: API và web.

 * spring-boot-starter-test: Unit test.

### 2.5. Kiểm tra Mã Nguồn
- Viết unit test cho các Service và Controller.
- Sử dụng JUnit và Mockito cho việc kiểm thử.

## 3. Sự Tương Tác Giữa Các Package
### 3.1. Package `entities`
- Chứa các lớp quản lý dữ liệu (Data Model).
- Ví dụ: `User.java` với các thuộc tính như `id`, `name`, `email`, v.v.

### 3.2. Package `repository`
- Chứa các interface truy cập dữ liệu (Data Access Layer) sử dụng Spring Data JPA.
- Các interface này sẽ kế thừa từ `JpaRepository` để tận dụng các phương thức CRUD.
- Ví dụ: `UserRepository.java` sẽ chứa các phương thức như `findByEmail(String email)`.

Ví dụ sử dụng query tùy chỉnh:
```java
@Query("SELECT u FROM User u WHERE u.email = :email")
Optional<User> findByEmail(@Param("email") String email);
```

### 3.3. Package `service`
- Chứa các interface định nghĩa nghiệp vụ (Business Logic) cho ứng dụng.
- Ví dụ: `UserService.java` định nghĩa các phương thức như `registerUser(User user)` và `getUserById(Long id)`.

### 3.4. Package `service.impl`
- Chứa các lớp triển khai của các interface trong package `service`.
- Ví dụ: `UserServiceImpl.java` thực hiện các phương thức trong `UserService`, tương tác với `UserRepository` để thực hiện các nghiệp vụ.

### 3.5. Package `controller`
- Chứa các lớp điều khiển (Controller) xử lý các yêu cầu từ client.
- Ví dụ: `UserController.java` sẽ sử dụng `UserService` để xử lý các yêu cầu như đăng ký và lấy thông tin người dùng, trả về các trang Thymeleaf phù hợp.
- Khuyến khích tách biệt API (@RestController) và controller giao diện (@Controller):
```java
@RestController
@RequestMapping("/api/users")
public class UserApiController {
    private final UserService userService;

    @GetMapping("/{id}")
    public ResponseEntity<User> getUserById(@PathVariable Long id) {
        return ResponseEntity.ok(userService.getUserById(id));
    }
}
```

### 3.6. Package `utilities`
- Chứa các hàm tiện ích (Utility) chung mà có thể dùng ở nhiều nơi trong ứng dụng.
- Ví dụ: `UtilityClass.java` có thể bao gồm các phương thức xử lý chuỗi, định dạng ngày tháng, v.v.

### 3.7. Package `exception`
- Chứa các exception tùy chỉnh cho phép xử lý lỗi một cách rõ ràng và dễ dàng.
- Ví dụ: `CustomException.java` có thể sử dụng để xử lý các trường hợp lỗi cụ thể trong ứng dụng.

## 4. Hướng dẫn Cài đặt Môi trường Phát triển
- Cài đặt **Java JDK** (phiên bản 17).
- Cài đặt **Maven** cho quản lý dependencies.
- Sử dụng **IDE** IntelliJ IDEA hoặc Eclipse cho phát triển.

## 5. Quy trình Phát triển
### 5.1. Quy trịnh làm việc với Git
1. Tạo nhánh (branch) mới cho mỗi tính năng hoặc sửa lỗi.
2. Thực hiện các thay đổi và commit theo quy luật.
3. Gửi yêu cầu hợp nhất (PR) mô tả rõ ràng những gì bạn đã thay đổi.
4. Đợi đánh giá mã nguồn trước khi hợp nhất vào nhánh chính.

### 5.2. Quy trình Review

- Code Review Checklist:

 [ ] Có tuân thủ Coding Convention không?

 [ ] Có viết Unit Test đầy đủ không?

 [ ] Code có dễ đọc và dễ bảo trì không?

 [ ] Có tồn tại lỗi tiềm ẩn như NPE không?

### 5.3. Template Pull Request

Gợi ý template PR:
```markdown
## Mô tả thay đổi
<!-- Mô tả chi tiết nội dung thay đổi -->

## Hướng dẫn kiểm tra
<!-- Hướng dẫn cách kiểm tra thay đổi -->

## Liên quan đến issue nào không?
- [ ] Không liên quan
- [ ] Có liên quan: <!-- Đính kèm issue -->
```

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

## 9. Tài liệu tham khảo (GPT đề xuất)
- Để hiểu rõ hơn về Spring Boot, bạn có thể tham khảo tài liệu chính thức tại [Spring Boot Reference Guide](https://docs.spring.io/spring-boot/docs/current/reference/html/index.html).
- Để hiểu rõ hơn về Thymeleaf, bạn có thể tham khảo tài liệu chính thức tại [Thymeleaf Documentation](https://www.thymeleaf.org/doc/tutorials/3.0/usingthymeleaf.html).
- Để hiểu rõ hơn về Maven, bạn có thể tham khảo tài liệu chính thức tại [Maven Documentation](https://maven.apache.org/guides/index.html).
- Để hiểu rõ hơn về JUnit, bạn có thể tham khảo tài liệu chính thức tại [JUnit 5 User Guide](https://junit.org/junit5/docs/current/user-guide/).
- Để hiểu rõ hơn về Mockito, bạn có thể tham khảo tài liệu chính thức tại [Mockito Documentation](https://javadoc.io/doc/org.mockito/mockito-core/latest/index.html).
- Để hiểu rõ hơn về Git, bạn có thể tham khảo tài liệu chính thức tại [Git Handbook](https://guides.github.com/introduction/git-handbook/).
- Để hiểu rõ hơn về Pull Request, bạn có thể tham khảo tài liệu chính thức tại [Creating a pull request](https://docs.github.com/en/github/collaborating-with-pull-requests/creating-a-pull-request).
- Để hiểu rõ hơn về Code Review, bạn có thể tham khảo tài liệu chính thức tại [Code Review](https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/about-pull-request-reviews).
- Để hiểu rõ hơn về JavaDoc, bạn có thể tham khảo tài liệu chính thức tại [JavaDoc](https://www.oracle.com/java/technologies/javase/javadoc.html).
- Để hiểu rõ hơn về Java Coding Conventions, bạn có thể tham khảo tài liệu chính thức tại [Java Coding Conventions](https://www.oracle.com/java/technologies/javase/codeconventions-contents.html).
- Để hiểu rõ hơn về Java Naming Conventions, bạn có thể tham khảo tài liệu chính thức tại [Java Naming Conventions](https://www.oracle.com/java/technologies/javase/codeconventions-namingconventions.html).
- Để hiểu rõ hơn về Java Indentation, bạn có thể tham khảo tài liệu chính thức tại [Java Indentation](https://www.oracle.com/java/technologies/javase/codeconventions-indentation.html).
- Để hiểu rõ hơn về Java Commenting, bạn có thể tham khảo tài liệu chính thức tại [Java Commenting](https://www.oracle.com/java/technologies/javase/codeconventions-comments.html).
- Để hiểu rõ hơn về Java Dependencies, bạn có thể tham khảo tài liệu chính thức tại [Java Dependencies](https://www.oracle.com/java/technologies/javase/codeconventions-dependencies.html).