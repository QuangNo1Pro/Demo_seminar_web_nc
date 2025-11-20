# 🎯 GA4 Deep Analysis - Hướng dẫn Toàn diện

Hướng dẫn chi tiết về **Phân tích chuyên sâu hành vi người dùng** với GA4:
- ✅ **Định danh người dùng** (User Properties)
- ✅ **Phân tích phễu mua hàng** (Ecommerce Funnel)
- ✅ **So sánh hành vi khách hàng** (Cohort Analysis)

---

## 📋 Mục lục

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

# 🎬 Tổng quan quy trình

```
1️⃣ Thay Measurement ID (GA4)
        ↓
2️⃣ Mở file HTML trong trình duyệt
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
3. Tìm: `G-XXXXXXX`
4. Thay bằng: Measurement ID của bạn (ví dụ: `G-A1B2C3D4E5`)
5. **Replace All** (thay tất cả)

**Ví dụ:**
```html
<!-- TRƯỚC (sai) -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXX"></script>
<script>
    gtag('config', 'G-XXXXXXX', {

<!-- SAU (đúng) -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-A1B2C3D4E5"></script>
<script>
    gtag('config', 'G-A1B2C3D4E5', {
```

---

# 🌐 BƯỚC 2: Mở file HTML trong trình duyệt

## 2.1 Cách mở file

**3 cách:**

### 🔹 Cách 1: Drag-drop
- Mở File Explorer
- Kéo file `index.html` vào trình duyệt (Chrome, Edge, Firefox, Safari)

### 🔹 Cách 2: Right-click
- Right-click file `index.html`
- Chọn **Open with** → chọn trình duyệt

### 🔹 Cách 3: Đường dẫn trực tiếp
- Ctrl + L trong trình duyệt
- Dán: `file:///C:/HCMUS/Nam4/Web_nang_cao/Demo-seminar/index.html`
- Enter

## 2.2 Kiểm tra file đã load thành công

✅ Bạn sẽ thấy:
- **Tiêu đề:** "GA4 Deep Analysis - User Properties & Ecommerce Funnel"
- **Màu tím gradient** ở header
- **6 phần** với các nút bấm màu sắc khác nhau

❌ Nếu thấy mã HTML thô → file chưa load đúng, kiểm tra lại đường dẫn

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

## 3.2 Ý nghĩa mỗi nút

| Nút | Sự kiện GA4 | Ý nghĩa |
|-----|-----------|---------|
| 👑 Đăng nhập VIP | `login` + `user_properties` | Gắn nhãn "VIP" cho user |
| 📷 Xem sản phẩm | `view_item` | User xem sản phẩm |
| 🛒 Thêm giỏ | `add_to_cart` | User quan tâm sản phẩm |
| 💳 Thanh toán | `purchase` | User hoàn thành giao dịch |
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
| File HTML (`index.html`) | Google Analytics DebugView |

## 6.2 Kịch bản quay video (2-3 phút)

```
0:00-0:10   "Xin chào thầy/cô. Hôm nay em xin trình bày GA4 Deep Analysis"
           (Show file HTML)

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

# 🎓 Kịch bản "chém gió" khi trình bày

> "Thầy/cô ơi, em xin trình bày về GA4 Deep Analysis - Phân tích chuyên sâu hành vi người dùng.
>
> **Câu hỏi 1: Họ là ai?**
> Thông thường GA4 chỉ biết người dùng là một con số ẩn danh. Nhưng em dùng User Properties để gắn 'nhãn' lên user. Ví dụ: VIP, Premium, Regular.
> Từ đó, em có thể so sánh: VIP chi tiêu trung bình 50 triệu, Regular chỉ 8 triệu. → VIP chi tiêu **gấp 6 lần**.
>
> **Câu hỏi 2: Họ rớt ở đâu?**
> Não chỉ đo lường mua hàng. Em đo lường cả **quy trình**: Xem hàng → Thêm giỏ → Mua.
> Nếu có 100 người xem, 50 người thêm giỏ, nhưng chỉ 2 người mua → **Quy trình thanh toán có vấn đề hoặc phí ship quá cao**.
>
> Em đã cấu hình 3 sự kiện riêng biệt trên GA4 để bắt tất cả các bước này. DebugView sẽ chứng minh dữ liệu được gửi real-time.
> 
> Như bạn thấy trên video, khi em bấm nút → sự kiện lập tức hiện trên GA4, kèm theo user_type, giá tiền, mã đơn hàng... → Đó là Deep Analysis! 📊"

---

**Good luck! 🚀**
