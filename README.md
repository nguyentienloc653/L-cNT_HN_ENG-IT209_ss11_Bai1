# Bài 1: Khởi tạo Workflow chạy Unit Test tự động cho Java Spring Boot với Gradle

## 1. Mục tiêu
- Khởi tạo tệp kịch bản GitHub Actions Workflow cho dự án Java Spring Boot sử dụng Gradle.
- Cấu hình môi trường Java JDK 17 (Temurin) và tự động chạy bài kiểm thử JUnit Test bằng Gradle Wrapper (`./gradlew test`).

---

## 2. Kịch bản CI (`.github/workflows/ci.yml`)

Tệp kịch bản workflow được cấu hình tại đường dẫn `.github/workflows/ci.yml`:

```yaml
name: Java Spring Boot CI (Gradle)

on:
  push:
    branches: [ "main" ]

jobs:
  test:
    name: Run Unit Tests
    runs-on: ubuntu-latest

    steps:
      - name: Checkout mã nguồn
        uses: actions/checkout@v5

      - name: Thiết lập môi trường Java JDK 17
        uses: actions/setup-java@v5
        with:
          java-version: '17'
          distribution: 'temurin'

      - name: Cấp quyền cho Gradle Wrapper
        run: chmod +x gradlew

      - name: Thực thi JUnit Test với Gradle
        run: ./gradlew test
```

---

## 3. Giải thích chi tiết các thành phần trong Workflow

1. **`name: Java Spring Boot CI (Gradle)`**:
   - Tên hiển thị của Workflow trên giao diện GitHub Actions.

2. **`on.push.branches: [ "main" ]`**:
   - Điều kiện kích hoạt (Trigger): Workflow sẽ tự động khởi chạy mỗi khi có commit mới được đẩy (push) lên nhánh `main`.

3. **`runs-on: ubuntu-latest`**:
   - Môi trường máy ảo (Runner) do GitHub cấp phát sử dụng hệ điều hành Ubuntu phiên bản mới nhất.

4. **`uses: actions/checkout@v5`**:
   - Kéo (clone) mã nguồn dự án từ repository về máy ảo để runner có thể truy cập mã nguồn và chạy các lệnh tiếp theo.

5. **`uses: actions/setup-java@v5`**:
   - Thiết lập môi trường Java JDK 17 trên máy ảo.
   - `distribution: 'temurin'`: Sử dụng bản phân phối Eclipse Temurin (chuẩn OpenJDK phổ biến, ổn định cho CI/CD).

6. **`run: chmod +x gradlew`**:
   - Phân quyền thực thi (`execute`) cho tệp script `gradlew` (Gradle Wrapper) để runner Linux có thể gọi `./gradlew`.

7. **`run: ./gradlew test`**:
   - Lệnh thực thi toàn bộ các bài kiểm thử đơn vị (JUnit Tests) trong dự án Spring Boot thông qua Gradle Wrapper. Nếu toàn bộ test vượt qua, job sẽ kết thúc với mã thoát 0 (Success - tích xanh ✔️).

---

## 4. Hướng dẫn kiểm tra và nộp bài

### Bước 1: Khởi tạo Git & Đẩy mã nguồn lên GitHub
Nếu bạn đang làm việc trên thư mục dự án mới hoặc tạo repo trên GitHub:
```bash
git init
git add .
git commit -m "feat: initialize unit test CI workflow with Gradle"
git branch -M main
git remote add origin https://github.com/<tai-khoan-github>/<ten-repo>.git
git push -u origin main
```

*(Nếu repo đã liên kết sẵn, chỉ cần commit và push lên nhánh `main`)*:
```bash
git add .github/workflows/ci.yml
git commit -m "ci: add GitHub Actions workflow for running unit tests"
git push origin main
```

### Bước 2: Kiểm tra trạng thái trên GitHub Actions
1. Mở GitHub Repository trên trình duyệt.
2. Điều hướng tới tab **Actions**.
3. Chọn workflow run vừa được kích hoạt có tên **"Java Spring Boot CI (Gradle)"**.
4. Chọn Job **"Run Unit Tests"** và theo dõi các bước thực thi:
   - *Checkout mã nguồn*
   - *Thiết lập môi trường Java JDK 17*
   - *Cấp quyền cho Gradle Wrapper*
   - *Thực thi JUnit Test với Gradle*
5. Xác nhận Job hoàn thành với trạng thái tích xanh thành công (**Success** ✔️).

### Bước 3: Chụp ảnh màn hình nộp bài
- Chụp ảnh màn hình giao diện tab **Actions** hoặc chi tiết Job **Run Unit Tests** hiển thị trạng thái tích xanh (Success).
- Đặt tên tệp ảnh (ví dụ: `screenshot-success.png`) và lưu vào thư mục `homework/session_11/ex1/`.
