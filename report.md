
# Báo cáo Bài 3 - Gradle Dependency Caching

## 1. Mục tiêu

Cấu hình Gradle Dependency Caching trong GitHub Actions
để giảm thời gian tải thư viện khi chạy CI.

## 2. Cấu hình

Trong bước actions/setup-java@v5, bổ sung:

```yaml
cache: 'gradle'
```

## 3. Kết quả so sánh

| Nội dung | Lần 1 | Lần 2 |
|---|           ---|    ---|
| Setup Java và cache | 1s | 1s |
| Chạy ./gradlew test | 43s | 20s |
| Tổng thời gian Job | 1m 1s | 31s |
| Cache được khôi phục | Chưa có cache ban đầu | Có cache |

## 4. Nhận xét

Sau lần chạy đầu tiên, GitHub Actions tạo cache Gradle
để sử dụng ở những lần chạy tiếp theo. Ở lần chạy thứ hai,
kiểm tra log của bước setup-java để xác nhận cache được
khôi phục. Thời gian thực tế được ghi nhận từ log GitHub Actions.
