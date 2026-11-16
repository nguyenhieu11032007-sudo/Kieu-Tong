# Đảo Marketing AI 🏝️

Một hòn đảo dễ thương để quản lý team marketing gồm các **AI Agent**. Mỗi phòng ban là một ngôi nhà trên đảo: chạm vào nhà để xem các Agent đang làm việc gì, giao việc cho phòng nào, và chỉnh sửa tên, vai trò, danh sách công việc ngay trên trang.

*A cute, game-style island dashboard for a marketing team of AI agents. Single HTML file, optional Firebase sync. English summary at the bottom.*

## Tính năng

- 5 phòng ban: Content Ads, Social, Ads, Designer, Editor, mỗi phòng một ngôi nhà riêng.
- Agent có tên, vai trò, màu, phụ kiện, thanh tiến độ và bong bóng trạng thái.
- Hộp quà chạy trên đường khi một phòng bàn giao việc cho phòng khác.
- Chế độ **Sửa**: thêm, xóa, đổi tên Agent và công việc, có nút **Lưu**.
- Đồng bộ thời gian thực qua **Firebase** (tùy chọn), có mật khẩu chung cho team.
- Chế độ ngày và đêm, dùng được trên điện thoại.

> ⚠️ Đây là **bản mô hình (prototype)**. Agent và các số liệu (ROAS, CPA…) hiện là **giả lập**, chưa nối với AI thật.

## Chạy thử nhanh (không cần Firebase)

Tải `index.html` về và đưa lên bất kỳ dịch vụ host tĩnh nào (Netlify Drop, GitHub Pages…). Khi chưa điền cấu hình Firebase, trang tự chạy ở **chế độ demo**: mọi thứ hoạt động nhưng chỉnh sửa sẽ mất khi tải lại trang.

## Cài đặt với Firebase (để cả team dùng chung)

1. Tạo dự án tại [console.firebase.google.com](https://console.firebase.google.com), thêm một **Web app** và chép đoạn `firebaseConfig`.
2. **Firestore Database**: tạo cơ sở dữ liệu ở chế độ *Production*.
3. **Authentication**: bật **Email/Password**, rồi thêm một người dùng `team@dao.local` với mật khẩu chung của team.
4. **Authentication → Settings → User actions**: tắt **Enable create (sign-up)** để người lạ không tự tạo tài khoản được (nếu tùy chọn này có trong dự án của bạn).
5. **Firestore → Rules**: dán nội dung file [`firestore.rules`](firestore.rules) và bấm Publish.
6. Mở `index.html`, thay các giá trị `YOUR_...` trong `firebaseConfig` bằng cấu hình của bạn.
7. Đưa trang lên host, rồi thêm tên miền vào **Authentication → Settings → Authorized domains**.

> Lưu ý: `firebaseConfig` không phải mật khẩu, nhưng **đừng commit cấu hình Firebase của team bạn lên kho công khai**. Hãy giữ bản đã điền cấu hình ở máy hoặc ở host, còn trên GitHub để nguyên `YOUR_...`.

## Cấu trúc

| File | Nội dung |
|---|---|
| `index.html` | Toàn bộ giao diện, hình vẽ SVG và logic, trong một file |
| `firestore.rules` | Luật bảo mật cho Firestore |

## Đóng góp

Mọi ý tưởng và cải tiến đều được chào đón! Xem [CONTRIBUTING.md](CONTRIBUTING.md). Một vài hướng đang cần giúp:

- Hộp thư đến cho mỗi phòng (chấm đỏ báo việc mới được giao).
- Bước "chờ duyệt" trước khi Agent chạy việc.
- Nối với AI Agent thật (Claude API, n8n…) qua `window.IslandAPI`.
- Tài khoản riêng cho từng thành viên thay vì mật khẩu chung.
- Thêm phòng ban mới, nhân vật và trang trí mới.

### Nối Agent thật

Trang có sẵn một API nhỏ trong trình duyệt:

```js
IslandAPI.simulate(false)                       // tắt giả lập
IslandAPI.setAgent("bo", { task: "Tối ưu chiến dịch A", progress: 0.4, status: "working" })
IslandAPI.sendParcel("CA", "DE", "Brief key visual mới")
IslandAPI.log("AD", "Bơ vừa tăng ngân sách adset 2")
```

Mã phòng: `CA` Content Ads · `SO` Social · `AD` Ads · `DE` Designer · `ED` Editor.

## English summary

A single-file, game-like island where each house is a marketing department staffed by (currently simulated) AI agents. Click a house to see tasks, progress and hand-offs; edit names, roles and task lists in place. Leave the `YOUR_...` placeholders in `index.html` to run in local demo mode, or follow the Firebase steps above for shared real-time data. UI text is in Vietnamese. Contributions welcome!

## Giấy phép

[MIT](LICENSE)
