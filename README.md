# Trang redirect deep link 

`index.html` là một trang tĩnh để biến link chia sẻ thành dạng **https bấm được**. Khi
người nhận bấm link:

1. Trang thử mở `globalcitizen://ranking` → nếu đã cài app, app mở thẳng tab Ranking.
2. Nếu chưa cài, sau ~1.2s hiện nút "Tải ứng dụng" trỏ về store (hoặc trang giới thiệu).

Không cần domain riêng, không cần file xác thực App Links.

## Khi app lên store

Điền `ANDROID_STORE` / `IOS_STORE` trong `index.html` để nút "Tải ứng dụng" trỏ đúng
store theo nền tảng. Trước đó nút trỏ về `FALLBACK` (trang Google Sites hiện có).

## Nâng cấp lên App Links thật (tuỳ chọn, sau này)

Nếu muốn mở app **không nháy trình duyệt**, cần domain riêng + host
`/.well-known/assetlinks.json` (Android) và `/.well-known/apple-app-site-association`
(iOS), rồi thêm intent-filter `autoVerify` (Android) và Associated Domains (iOS).
Trang redirect này vẫn dùng được làm fallback song song.
