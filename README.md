

# 🎯 GA4 Deep Analysis - Hướng dẫn Toàn diện

🔗 **GitHub Repository:** [https://github.com/QuangNo1Pro/Demo_seminar_web_nc.git](https://github.com/QuangNo1Pro/Demo_seminar_web_nc.git)  
🌐 **Live Demo:** [https://demo-seminar-web-nc.vercel.app/](https://demo-seminar-web-nc.vercel.app/)

---

Hướng dẫn chi tiết về **Phân tích chuyên sâu hành vi người dùng** với GA4:
- ✅ **Định danh người dùng** (User Properties)
- ✅ **Phân tích phễu mua hàng** (Ecommerce Funnel)
- ✅ **So sánh hành vi khách hàng** (Cohort Analysis)
- ✅ **Virtual Pageviews** (Theo dõi điều hướng trong SPA)
- ✅ **Search Tracking** (Theo dõi tìm kiếm)
- ✅ **Remove from Cart** (Theo dõi xóa sản phẩm)

---

## 🆕 Tính năng trong index.html

1. **📄 Virtual Pageview Tracking (SPA)**
   - Theo dõi điều hướng giữa: Trang chủ → Sản phẩm → Giỏ hàng → Về chúng tôi
   - Mỗi lần chuyển trang gửi `page_view` event với path riêng
   - Hoàn hảo cho Single Page Application

2. **🔍 Search Event Tracking**
   - Ghi nhận khi user tìm kiếm sản phẩm
   - Gửi `search` event với `search_term` parameter
   - Kèm theo `page_view` cho trang kết quả tìm kiếm

3. **🏷️ Brand Filter với Virtual Pageviews**
   - Mỗi brand có path riêng: `/products/brand/laptop`, `/products/brand/dien-thoai`
   - GA4 theo dõi brand nào được quan tâm nhiều nhất

4. **❌ Remove from Cart Event**
   - Ghi nhận khi user xóa sản phẩm khỏi giỏ
   - Hiểu tại sao user thay đổi ý định mua

5. **🔔 Notification System**
   - Feedback realtime cho user mỗi hành động
   - Toast notification đẹp mắt, tự động ẩn

6. **🛒 Enhanced Cart Flow**
   - Begin checkout event trước khi purchase
   - Thank you page với virtual pageview
   - Full ecommerce tracking đầy đủ

### **GA4 Events được track:**

| Event | Khi nào trigger | Parameters quan trọng |
|-------|----------------|----------------------|
| `page_view` | Điều hướng menu, filter, search, product detail | `page_title`, `page_location`, `page_path` |
| `login` | Đăng nhập VIP/Premium/Regular/Guest | `method`, `user_type` |
| `search` | Nhập từ khóa và search | `search_term` |
| `view_item` | Xem chi tiết sản phẩm | `items`, `value`, `currency` |
| `add_to_cart` | Thêm sản phẩm vào giỏ | `items`, `value`, `currency` |
| `remove_from_cart` | Xóa sản phẩm khỏi giỏ | `items`, `value`, `currency` |
| `begin_checkout` | Bắt đầu thanh toán | `items`, `value`, `currency` |
| `purchase` | Hoàn thành đơn hàng | `transaction_id`, `value`, `items`, `tax`, `shipping` |

---

## 📋 Mục lục

### **Phần I: Web Shop Hoàn chỉnh (Recommended)**

- [🛍️ Chạy Web Shop](#-chạy-web-shop)
- [✨ Tính năng Shop](#-tính-năng-web-shop)
- [🎬 Kịch bản Demo](#-kịch-bản-demo-indexhtml)

### **Phần II: Setup & Testing**
1. [🎬 Tổng quan quy trình](#-tổng-quan-quy-trình)
2. [📝 Bước 1: Thay Measurement ID](#-bước-1-thay-measurement-id)
3. [🌐 Bước 2: Mở file HTML](#-bước-2-mở-file-html-trong-trình-duyệt)
4. [🎬 Bước 3: Tạo dữ liệu Test](#-bước-3-bấm-nút-để-tạo-dữ-liệu-test)
5. [⚙️ Bước 4: Cấu hình Custom Dimension](#️-bước-4-cấu-hình-custom-dimension-trên-ga4-bắtbuộc)
6. [🔴 Bước 5: Kiểm tra DebugView](#-bước-5-kiểm-tra-dữ-liệu-trên-debugview)
7. [📹 Bước 6: Quay video](#-bước-6-quay-video-chứng-minh)
8. [📊 Xem thống kê Data](#-phần-ii-xem-thống-kê-data-trên-ga4)
9. [🆘 Xử lý lỗi](#-xử-lý-lỗi)

---

# 🛍️ CHẠY WEB SHOP

## ⚡ Cách 1: Deploy lên Vercel (Khuyên dùng)

1. Deploy project này lên Vercel.
2. Mở URL Vercel của bạn (index.html sẽ tự động load).
   (Ví dụ: `https://your-project.vercel.app/`)

## 💻 Cách 2: Chạy local

1. Mở terminal trong thư mục project.
2. Chạy lệnh: `python -m http.server 8000`
3. Mở trình duyệt và truy cập: `http://localhost:8000/`

---

## ✨ Tính năng Web Shop

### **1️⃣ Đăng nhập & User Properties**
- 4 nút đăng nhập: VIP, Premium, Regular, Guest
- GA4 sẽ ghi nhận loại user và áp dụng cho toàn bộ hành động
- Header hiển thị user badge (VIP 👑, Premium 💎, Regular ⭐, Guest 👤)

### **2️⃣ Tìm kiếm (Search)**
- Ô tìm kiếm sản phẩm
- Hỗ trợ tìm kiếm theo tên hoặc category
- Nhấn Enter hoặc click "Tìm kiếm"

### **3️⃣ Lọc (Filter)**
- 6 nút lọc: Tất cả, Điện thoại, Laptop, Audio, Tablet, Smartwatch
- Lọc real-time, có highlight nút đang chọn
- Kết hợp được với search

### **4️⃣ Đánh giá (Reviews)**
- Mỗi sản phẩm có rating (⭐ 4.6-4.9)
- Hiển thị 2 đánh giá top từ khách hàng
- Tên người review, số sao, nội dung

### **5️⃣ Giỏ hàng & Checkout**
- Thêm/xóa sản phẩm
- Hiển thị tổng tiền
- Nút thanh toán gửi GA4 purchase event

### **6️⃣ GA4 Tracking tích hợp**

- ✅ **page_view**: Theo dõi điều hướng giữa các trang (Trang chủ, Sản phẩm, Về chúng tôi, Giỏ hàng)
- ✅ **login**: Khi bấm nút đăng nhập
- ✅ **search**: Khi tìm kiếm sản phẩm
- ✅ **view_item**: Khi bấm "Xem" sản phẩm
- ✅ **add_to_cart**: Khi bấm "Thêm" vào giỏ
- ✅ **remove_from_cart**: Khi xóa sản phẩm khỏi giỏ
- ✅ **begin_checkout**: Khi bắt đầu thanh toán
- ✅ **purchase**: Khi bấm "Thanh toán"
- ✅ Tất cả events được gửi **async** (không block UI)
- ✅ **Virtual Pageviews** cho Single Page Application (SPA)

---

## 🎬 Kịch bản Demo (index.html)

### **Scenario 1: Khách VIP mua 1 sản phẩm**

```
1. Mở index.html (hoặc truy cập web đã deploy)
   → GA4 ghi nhận page_view: Trang chủ

2. Bấm 👑 "Đăng nhập VIP"
   → Header hiển thị "VIP Member"
   → GA4 ghi nhận event login + user_properties
   → Notification hiện: "Đã đăng nhập VIP!"

3. Bấm "Xem" sản phẩm iPhone 15 Pro
   → GA4 ghi nhận view_item (value: 15M)
   → GA4 ghi nhận page_view: Trang chi tiết sản phẩm
   → Notification: "Đang xem: iPhone 15 Pro"

4. Bấm "Thêm" vào giỏ
   → Giỏ hàng update (số lượng +1)
   → GA4 ghi nhận add_to_cart
   → Notification: "Đã thêm iPhone 15 Pro vào giỏ"

5. Bấm biểu tượng 🛒 giỏ hàng trên header
   → Chuyển sang màn hình giỏ hàng
   → GA4 ghi nhận page_view: Giỏ hàng

6. Bấm "Thanh toán"
   → GA4 ghi nhận begin_checkout
   → GA4 ghi nhận purchase (value: 15M, transaction_id: TXN_xxxxx)
   → GA4 ghi nhận page_view: Thank you page
   → Alert hiển thị mã đơn hàng
   → Giỏ hàng reset
```

### **Scenario 2: Khách Regular tìm kiếm & điều hướng**

```
1. Bấm ⭐ "Đăng nhập Regular"
   → GA4 set user_type: Regular_Member
   → Notification: "Đã đăng nhập Regular!"

2. Nhập "Laptop" vào ô tìm kiếm → bấm Enter
   → GA4 ghi nhận search event (search_term: "Laptop")
   → GA4 ghi nhận page_view: Search results
   → Trang lọc chỉ hiển thị 2 sản phẩm Laptop
   → Notification: "Tìm kiếm: Laptop"

3. Bấm nút lọc 💻 "Laptop"
   → GA4 ghi nhận page_view: Products/brand/laptop
   → Kết quả không đổi (đã filter rồi)
   → Notification: "Lọc: Laptop"

4. Bấm menu "Về chúng tôi"
   → Chuyển sang trang About
   → GA4 ghi nhận page_view: Về chúng tôi
   → Notification: "Về chúng tôi"

5. Bấm logo "Tech Shop" trên header
   → Quay về trang chủ
   → GA4 ghi nhận page_view: Trang chủ
   → Notification: "Trang chủ"

6. Bấm "Xem" Laptop Dell XPS
   → GA4 ghi nhận view_item
   → GA4 ghi nhận page_view: Product detail

7. (Không mua) → Chỉ có view_item, không có purchase
   → GA4 sẽ tính drop-off rate
```

### **Scenario 3: So sánh VIP vs Guest với Remove Cart**

```
1. VIP Login → Xem 3 sản phẩm → Thêm tất cả vào giỏ
   → GA4 ghi nhận: 3 view_item, 3 add_to_cart

2. Xóa 1 sản phẩm khỏi giỏ
   → GA4 ghi nhận remove_from_cart
   → Notification: "Đã xóa [tên sản phẩm] khỏi giỏ"

3. Mua 2 sản phẩm còn lại → Purchase value: 40M
   → GA4 ghi nhận begin_checkout + purchase

4. Guest Login → Xem hàng → Không mua
   → GA4 ghi nhận: view_item (không có purchase)

GA4 Report sẽ cho thấy:
- VIP: Conversion 100%, AOV 40M, có remove_from_cart
- Guest: Conversion 0%, AOV 0
```

---

## 📊 GA4 Reports bạn sẽ thấy

### **1. User Properties Report**
Vào GA4 → Reports → User attributes → Groupby "Loại khách hàng"

```
User Type    | Users | Avg Order Value | Conversion
-------------|-------|-----------------|-------------
VIP_Member   | 1     | 50,000,000      | 100%
Regular_     | 1     | 15,000,000      | 50%
Member       |       |                 |
Guest        | 1     | 0               | 0%
```

### **2. Ecommerce Funnel**
Vào GA4 → Explore → Funnel exploration

```
Step 1: view_item → 10 users
Step 2: add_to_cart → 6 users (60%)
Step 3: purchase → 4 users (67%)

Drop-off: 40% xem không mua, 33% thêm giỏ không mua
```

### **3. DebugView (Real-time)**
Vào GA4 → Admin → DebugView

Bạn sẽ thấy:
```
✓ login (user_type: VIP_Member)
✓ view_item (item_name: iPhone 15 Pro, value: 15M)
✓ add_to_cart (items: [{...}])
✓ purchase (transaction_id: TXN_12345)
```

---

# 🎬 Tổng quan quy trình

```
1️⃣ Thay Measurement ID (GA4) trong `shop.html`
        ↓
2️⃣ Chạy Web Shop (local hoặc Vercel)
        ↓
3️⃣ Bấm nút để tạo dữ liệu test
        ↓
4️⃣ Cấu hình Custom Dimension trên GA4
        ↓
5️⃣ Kiểm tra dữ liệu trên DebugView
        ↓
6️⃣ Quay video chứng minh
        ↓
7️⃣ Xem báo cáo thống kê
```

---

# 📝 BƯỚC 1: Thay Measurement ID

## 1.1 Tìm Measurement ID của bạn

**Cách làm:**
1. Đăng nhập vào **Google Analytics 4** → https://analytics.google.com/
2. Chọn **Property** của bạn (nếu chưa có, tạo mới)
3. Vào **Admin** (dấu bánh răng ⚙️ dưới cùng bên trái)
4. Chọn **Data streams** (trong mục Property)
5. Click vào **Web stream** của bạn
6. Sao chép **Measurement ID** (ví dụ: `G-A1B2C3D4E5`)

## 1.2 Thay Measurement ID trong file HTML

**Cách làm:**
1. Mở file `index.html` trong VS Code
2. **Ctrl + H** để mở Find and Replace
3. Tìm: `G-5T3BKBHZCZ`
4. Thay bằng: Measurement ID của bạn (ví dụ: `G-A1B2C3D4E5`)
5. **Replace All** (thay tất cả)

**Ví dụ:**
```html
<!-- TRƯỚC (sai) -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-5T3BKBHZCZ"></script>
<script>
    gtag('config', 'G-5T3BKBHZCZ', {

<!-- SAU (đúng) -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-A1B2C3D4E5"></script>
<script>
    gtag('config', 'G-A1B2C3D4E5', {
```

---

# 🎬 BƯỚC 3: Bấm nút để tạo dữ liệu Test

## 3.1 Quy trình mô phỏng (Scenario)

Hãy thực hiện theo thứ tự này:

### **Scenario 1: Khách VIP mua iPhone 15 Pro**

```
1. Bấm nút 👑 "Đăng nhập (VIP Member)"
   → Alert: "Đã set User Property: VIP_Member"
   → GA4 bây giờ biết user này là VIP

2. Bấm nút 📷 "Bước 1: Xem sản phẩm" (iPhone)
   → Alert: "Đã gửi sự kiện: view_item"
   → GA4 ghi nhận: VIP xem iPhone 15 Pro

3. Bấm nút 🛒 "Bước 2: Thêm vào giỏ"
   → Alert: "Đã thêm vào giỏ"
   → GA4 ghi nhận: VIP thêm iPhone vào giỏ

4. Bấm nút 💳 "Bước 3: Thanh toán"
   → Alert: "Mã đơn hàng: TXN_XXXXX"
   → GA4 ghi nhận: VIP mua 15 triệu
```

### **Scenario 2: Khách Regular xem Laptop rồi bỏ**

```
1. Bấm nút ⭐ "Đăng nhập (Regular Member)"
   → Alert: "Đã set User Property: Regular_Member"

2. Bấm nút 📷 "Xem Laptop"
   → Alert: "view_item"

3. Bấm nút ⚠️ "Xem sản phẩm rồi bỏ đi"
   → Alert: "Khách xem Apple AirPods Max"
   → GA4 ghi nhận: Regular xem nhưng KHÔNG mua (drop-off)
```

## 3.2 Ý nghĩa mỗi hành động

| Hành động | Sự kiện GA4 | Ý nghĩa |
|-----|-----------|---------|
| 👑 Đăng nhập VIP | `login` + `user_properties` | Gắn nhãn "VIP" cho user |
| 🏠 Bấm logo/menu | `page_view` | Điều hướng giữa các trang (SPA tracking) |
| 🔍 Tìm kiếm | `search` + `page_view` | User tìm kiếm sản phẩm |
| 🏷️ Lọc danh mục | `page_view` | User lọc theo brand |
| 📷 Xem sản phẩm | `view_item` + `page_view` | User xem chi tiết sản phẩm |
| 🛒 Thêm giỏ | `add_to_cart` | User quan tâm sản phẩm |
| ❌ Xóa khỏi giỏ | `remove_from_cart` | User thay đổi ý định |
| 💳 Thanh toán | `begin_checkout` + `purchase` + `page_view` | User hoàn thành giao dịch |
| ⚠️ Bỏ đi | `view_item` (không có purchase) | User KHÔNG mua (drop-off) |

---

# ⚙️ BƯỚC 4: Cấu hình Custom Dimension trên GA4 (BẮTBUỘC)

### ⚠️ **QUAN TRỌNG:** Nếu không làm bước này, User Properties sẽ không hiện trên báo cáo!

## 4.1 Vào Admin

1. Đăng nhập **Google Analytics 4**
2. Click dấu **bánh răng ⚙️** (dưới cùng bên trái)
3. Chọn **Admin**

## 4.2 Tạo Custom Dimension

1. Ở cột trái, click **Custom definitions**
2. Click **Custom dimensions**
3. Click nút **Create custom dimension** (màu xanh)

## 4.3 Điền thông tin (Quan trọng!)

**Form sẽ hiện:**

```
Dimension name: (tên hiển thị)
  → Nhập: "Loại khách hàng"

Description: (tùy chọn)
  → Nhập: "Phân loại khách: VIP, Premium, Regular, Guest"

Scope: (chọn phạm vi)
  → Chọn: "User" (Phạm vi người dùng)
  → ⚠️ PHẢI chọn "User", không chọn "Event"

User property: (khóa trong code)
  → Nhập: "user_type" (PHẢI trùng y hệt code)
```

## 4.4 Lưu

Click **Save**

---

# 🔴 BƯỚC 5: Kiểm tra dữ liệu trên DebugView

## 5.1 Vào DebugView

1. Mở **Google Analytics 4**
2. Vào **Admin** → **DebugView**
3. Bạn sẽ thấy giao diện real-time

## 5.2 Tìm User của bạn

**Có 2 cách:**

### 🔹 Cách 1: Dùng Client ID (dễ nhất)
1. Mở trang HTML trong tab Browser
2. **F12** (mở Developer Console)
3. **Console** tab
4. Dán code:
```javascript
gtag('get', 'client_id', (cid) => console.log('Client ID:', cid));
```
5. Copy Client ID hiện ra
6. Quay lại DebugView, paste vào ô tìm kiếm

### 🔹 Cách 2: Dùng User ID (nếu bạn set)
1. Nếu bạn bấm nút "Đăng nhập VIP" → User ID sẽ được ghi nhận
2. Tìm bằng User ID trên DebugView

## 5.3 Xem các sự kiện được gửi

**Ở DebugView, bạn sẽ thấy:**

```
📊 REAL-TIME EVENTS:
├─ login (19:30:45)
│  ├─ method: "Google"
│  └─ user_type: "VIP"
│
├─ view_item (19:30:50)
│  ├─ item_name: "iPhone 15 Pro"
│  ├─ value: 15000000
│  └─ currency: "VND"
│
├─ add_to_cart (19:30:55)
│  └─ value: 15000000
│
└─ purchase (19:31:00)
   ├─ transaction_id: "TXN_12345"
   ├─ value: 15000000
   └─ items: [...]
```

## 5.4 Kiểm tra User Properties

1. Click vào event **login**
2. Scroll xuống → tìm tab **"User properties"**
3. Bạn sẽ thấy:
   - `user_type: VIP_Member`
   - `customer_level: Gold`
   - `membership_status: Active`

✅ Nếu thấy được → Cấu hình thành công!

---

# 📹 BƯỚC 6: Quay video chứng minh

## 6.1 Chuẩn bị

**Mở 2 tab trong trình duyệt:**

| Tab 1 | Tab 2 |
|-------|-------|
| Web Shop (`shop.html`) | Google Analytics DebugView |

## 6.2 Kịch bản quay video (2-3 phút)

```
0:00-0:10   "Xin chào thầy/cô. Hôm nay em xin trình bày GA4 Deep Analysis"
           (Show Web Shop)

0:10-0:40   "Đầu tiên, em set user_type thành VIP Member"
           (Bấm nút 👑 Đăng nhập VIP)
           → Chuyển qua tab GA4 DebugView
           → Chỉ vào event "login" có user_type: VIP_Member
           
0:40-1:20   "Tiếp theo, mô phỏng khách VIP mua hàng"
           (Bấm lần lượt: Xem sản phẩm → Thêm giỏ → Thanh toán)
           → Tab GA4 sẽ update real-time
           → Chỉ vào: view_item → add_to_cart → purchase

1:20-1:50   "Em cũng test trường hợp khách bỏ cuộc"
           (Bấm nút ⚠️ "Xem rồi bỏ")
           → Chỉ vào GA4: chỉ có view_item, KHÔNG có purchase

1:50-2:00   "Kết luận: GA4 đã ghi nhận tất cả hành động"
           (Tóm tắt lại)
```

## 6.3 Công cụ quay video

**Cách 1: Dùng Windows (sẵn có)**
- **Win + G** (Game Bar)
- Click "Start recording" (tròn đỏ)
- Dừng bằng **Win + G** lần nữa

**Cách 2: Dùng OBS Studio (miễn phí)**
- Tải: https://obsproject.com/
- Cấu hình: Chọn monitor → Start recording

**Cách 3: Dùng Chrome Extension (OnlineScreenRecorder)**
- Cài extension trong Chrome
- Click → Record

---

# 📊 PHẦN II: XEM THỐNG KÊ DATA TRÊN GA4

## 🎯 Tóm tắt: Có 3 chỗ để xem data

```
1️⃣ DebugView (Real-time) → Xem ngay lập tức (0-10 giây)
     ↓
2️⃣ Realtime Report → Xem khách truy cập LIVE
     ↓
3️⃣ Reports (Báo cáo) → Xem dữ liệu tổng hợp (sau 24-48 giờ)
```

---

## 📺 CÁCH 1: DebugView (Real-Time - Nhanh nhất)

### 🚀 Khi nào dùng?
- **Muốn kiểm tra ngay lập tức** khi bấm nút trên trang web
- Không cần chờ 24 giờ
- Để quay video chứng minh

### 📝 Các bước:

1. Vào **Google Analytics 4** → https://analytics.google.com/
2. Chọn **Property** của bạn
3. Vào **Admin** (⚙️ dưới cùng bên trái)
4. Chọn **DebugView** (dưới mục "Trợ giúp thiết lập")
5. Tìm User bằng Client ID (xem Bước 5 ở trên)
6. Bấm nút trên trang HTML → sự kiện sẽ hiện real-time trên DebugView

---

## 📈 CÁCH 2: Realtime Report (Live Dashboard)

### 🚀 Khi nào dùng?
- Muốn thấy **người dùng ĐANG truy cập** ngay bây giờ
- Xem tổng số lượt xem, người dùng theo thời gian thực

### 📝 Các bước:

1. Vào **Google Analytics 4**
2. Ở menu trái, chọn **Realtime** (dưới "Reports")
3. Bạn sẽ thấy:

```
🔴 LIVE (Cập nhật mỗi 1-2 giây)

Tổng người dùng hiện tại: 1
Tổng lượt xem hiện tại: 5
Tổng sự kiện: 8

📊 Top Pages:
├─ https://your-site.vercel.app  → 1 user
│
📊 Top Events:
├─ page_view    → 3 events
├─ view_item    → 2 events
├─ add_to_cart  → 1 event
├─ purchase     → 1 event
├─ login        → 1 event
```

**Khi bạn bấm nút trên trang HTML → Realtime sẽ update ngay!**

---

## 📊 CÁCH 3: Reports (Báo cáo Chi Tiết)

### 🚀 Khi nào dùng?
- Muốn xem **báo cáo tổng hợp** (sau 24-48 giờ)
- Phân tích chi tiết hành vi người dùng
- So sánh các nhóm khách hàng (VIP vs Regular)

### A) Xem User Properties Report

1. Vào **Google Analytics 4**
2. Ở menu trái, chọn **Reports** → **User attributes** (hoặc tìm báo cáo tùy chỉnh)
3. Hoặc vào **Explore** để tạo báo cáo tùy chỉnh

**Sau khi tạo Custom Dimension:**
- Vào **Reports** → Báo cáo sẽ hiện custom dimension "Loại khách hàng"
- Bạn có thể filter/group theo user_type (VIP, Premium, Regular)

---

### B) Xem Ecommerce Report (Phễu Mua Hàng)

1. Vào **Google Analytics 4**
2. Menu trái → **Monetization** (hoặc tìm **Ecommerce purchases**)
3. Hoặc tạo báo cáo tùy chỉnh: **Explore** → **Blank**

**Tạo báo cáo Phễu:**

1. Vào **Explore** → **Funnel exploration**
2. Cấu hình:
   - **Step 1**: view_item (Xem sản phẩm)
   - **Step 2**: add_to_cart (Thêm giỏ)
   - **Step 3**: purchase (Mua hàng)
3. Click **Run report**

**Kết quả:**
```
📊 ECOMMERCE FUNNEL REPORT

Step 1: view_item
  └─ 10 users

Step 2: add_to_cart (60% conversion)
  └─ 6 users

Step 3: purchase (67% conversion)
  └─ 4 users

Drop-off rate:
├─ View → Cart: 40% bỏ cuộc
└─ Cart → Purchase: 33% bỏ cuộc
```

---

### C) So sánh hành vi VIP vs Regular (Cohort Analysis)

1. Vào **Explore** → **Segment overlap** (hoặc **Funnel**)
2. Tạo 2 segment:
   - Segment 1: user_type = "VIP_Member"
   - Segment 2: user_type = "Regular_Member"
3. Metrics: "Average Order Value", "Conversion Rate"

**Kết quả:**
```
Segment Analysis:

VIP Members:
  ├─ Tổng người: 5
  ├─ Conversion rate: 80%
  └─ Avg Order Value: 50M VND

Regular Members:
  ├─ Tổng người: 5
  ├─ Conversion rate: 40%
  └─ Avg Order Value: 8M VND

📊 Kết luận: VIP chi tiêu gấp 6 lần Regular!
```

---

## 🎯 Lịch trình xem data

| Thời gian | Nơi xem | Nội dung |
|-----------|---------|---------|
| **Ngay lập tức (0-10s)** | DebugView | Xem từng event chi tiết |
| **1-2 giây** | Realtime Report | Tổng người dùng, sự kiện hiện tại |
| **24-48 giờ** | Reports | Báo cáo tổng hợp, phễu, user segmentation |

---

# 🆘 Xử lý lỗi

## ❌ Lỗi 1: "GA4 không nhận dữ liệu"

**Nguyên nhân:** Measurement ID sai hoặc chưa kích hoạt

**Cách khắc phục:**
1. Kiểm tra lại Measurement ID (copy paste chính xác)
2. Vào GA4 → Admin → Data streams → kiểm tra Domain
3. Có thể cần chờ 5-10 phút để GA4 cập nhật
4. Mở **Console (F12)** → xem có lỗi gì không

---

## ❌ Lỗi 2: "DebugView trống, không thấy sự kiện"

**Nguyên nhân:** User chưa được GA4 chọn lọc

**Cách khắc phục:**
1. Mở file HTML → F12 → Console
2. Dán code lấy Client ID:
```javascript
gtag('get', 'client_id', (cid) => console.log('Client ID:', cid));
```
3. Copy Client ID
4. Vào GA4 → DebugView → Search bằng Client ID
5. Đợi 10-15 giây sẽ thấy sự kiện

---

## ❌ Lỗi 3: "User Properties không hiện trên báo cáo"

**Nguyên nhân:** Chưa tạo Custom Dimension

**Cách khắc phục:**
1. Vào GA4 → Admin → Custom definitions
2. Tạo Custom Dimension với:
   - **Dimension name:** "Loại khách hàng"
   - **Scope:** "User" (**BẮTBUỘC!**)
   - **User property:** "user_type"
3. Lưu
4. Đợi 24-48 giờ để GA4 xử lý dữ liệu cũ

---

## ❌ Lỗi 4: "Ecommerce sự kiện không hiện"

**Nguyên nhân:** Tên event sai hoặc thiếu thông số bắt buộc

**Cách khắc phục:**
1. Mở F12 → Console
2. Kiểm tra lỗi JavaScript
3. Verify code đúng: `view_item`, `add_to_cart`, `purchase` (chính tả phải đúng)
4. Kiểm tra có `currency` và `value` không (bắt buộc cho ecommerce)

---

# ✅ CHECKLIST: Đã hoàn thành chưa?

- [ ] 1. Thay Measurement ID trong file HTML
- [ ] 2. Mở file HTML trong trình duyệt
- [ ] 3. Bấm các nút theo scenario (VIP login → view → cart → purchase)
- [ ] 4. Cấu hình Custom Dimension trên GA4 (**user_type**)
- [ ] 5. Kiểm tra dữ liệu trên DebugView (thấy events + user_properties)
- [ ] 6. Quay video 2-3 phút chứng minh dữ liệu được gửi
- [ ] 7. Xem báo cáo thống kê trên GA4 (DebugView, Realtime, Reports)

---

# 📊 Kết quả dự kiến

**Sau khi hoàn tất, trên GA4 bạn sẽ thấy:**

### 1. Báo cáo User Segmentation
```
User Type | Total Users | Avg Order Value | Conversion Rate
---------|-------------|-----------------|----------------
VIP      | 1           | 50,000,000 VND | 100%
Regular  | 1           | 8,000,000 VND  | 50%
```

### 2. Ecommerce Funnel Report
```
view_item   → 5 users
add_to_cart → 3 users (60% conversion)
purchase    → 2 users (67% conversion)

Drop-off rate: 40% at cart step
```

### 3. Real-time Events (DebugView)
```
✓ login event (user_type: VIP_Member)
✓ view_item event (value: 15M)
✓ add_to_cart event (value: 15M)
✓ purchase event (transaction_id: TXN_12345)
```

---
---

# 📁 Cấu trúc File

```
Demo-seminar/
├── index.html         (⭐ Web Shop Demo - File chính)
├── README.md          (File hướng dẫn này)
└── .git/
```