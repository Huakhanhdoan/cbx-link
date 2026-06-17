# Trang redirect deep link (share link bấm được)

`index.html` là một trang tĩnh để biến link chia sẻ thành dạng **https bấm được**. Khi
người nhận bấm link:

1. Trang thử mở `globalcitizen://ranking` → nếu đã cài app, app mở thẳng tab Ranking.
2. Nếu chưa cài, sau ~1.2s hiện nút "Tải ứng dụng" trỏ về store (hoặc trang giới thiệu).

Không cần domain riêng, không cần file xác thực App Links.

## Host miễn phí bằng GitHub Pages

1. Tạo repo mới trên GitHub, ví dụ `cbx-link` (có thể để public).
2. Copy `index.html` (trong thư mục này) vào **gốc** repo đó.
3. Repo → **Settings → Pages** → *Build and deployment* → Source = **Deploy from a branch**,
   chọn branch `main`, thư mục `/ (root)` → Save.
4. Đợi 1–2 phút, GitHub cấp URL dạng:
   `https://<tên-github>.github.io/cbx-link/`
5. Mở URL đó trên điện thoại đã cài app để kiểm tra (phải mở được app).

## Nối vào app

Mở `lib/core/constants/app_constants.dart`, set:

```dart
static final Uri? rankingShareUrl =
    Uri.parse('https://<tên-github>.github.io/cbx-link/');
```

Sau khi set, caption chia sẻ sẽ dùng link https này (bấm được). Để trống (`null`)
thì app dùng lại `globalcitizen://ranking` (không bấm được — chỉ hợp khi đã cài app).

## Khi app lên store

Điền `ANDROID_STORE` / `IOS_STORE` trong `index.html` để nút "Tải ứng dụng" trỏ đúng
store theo nền tảng. Trước đó nút trỏ về `FALLBACK` (trang Google Sites hiện có).

## Nâng cấp lên App Links thật (tuỳ chọn, sau này)

Nếu muốn mở app **không nháy trình duyệt**, cần domain riêng + host
`/.well-known/assetlinks.json` (Android) và `/.well-known/apple-app-site-association`
(iOS), rồi thêm intent-filter `autoVerify` (Android) và Associated Domains (iOS).
Trang redirect này vẫn dùng được làm fallback song song.
