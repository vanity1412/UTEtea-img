# 🎭 HỆ THỐNG PHÂN QUYỀN VÀ LUỒNG HOẠT ĐỘNG - UTE TEA

## 📋 MỤC LỤC
1. [Tổng Quan Hệ Thống Phân Quyền](#1-tổng-quan-hệ-thống-phân-quyền)
2. [Chi Tiết Từng Role](#2-chi-tiết-từng-role)
3. [Luồng Hoạt Động Theo Role](#3-luồng-hoạt-động-theo-role)
4. [Ma Trận Chức Năng Theo Role](#4-ma-trận-chức-năng-theo-role)
5. [Luồng Chuyển Đổi Role](#5-luồng-chuyển-đổi-role)
6. [Sơ Đồ Luồng Hoạt Động Chi Tiết](#6-sơ-đồ-luồng-hoạt-động-chi-tiết)

---

## 1. TỔNG QUAN HỆ THỐNG PHÂN QUYỀN

### 1.1 Các Role Trong Hệ Thống

Hệ thống UTE Tea có **3 role chính**:

| Role | Mô tả | Quyền hạn |
|------|-------|-----------|
| **GUEST** | Khách chưa đăng nhập | Xem sản phẩm, tìm kiếm, xem cửa hàng |
| **USER** | Người dùng đã đăng nhập | Đặt hàng, thanh toán, đánh giá, loyalty |
| **MANAGER** | Quản lý (bao gồm Admin) | Quản lý đơn hàng, sản phẩm, người dùng, thống kê |

> **Lưu ý:** Admin được coi là Manager với quyền cao nhất, có thể quản lý tất cả cửa hàng và nâng/hạ cấp người dùng.

### 1.2 Sơ Đồ Phân Cấp Quyền

```
┌─────────────────────────────────────────────────────────────────────┐
│                         MANAGER (Admin)                             │
│  ┌─────────────────────────────────────────────────────────────┐   │
│  │ • Quản lý TẤT CẢ cửa hàng                                   │   │
│  │ • Nâng/Hạ cấp User ↔ Manager                                │   │
│  │ • Gán cửa hàng cho Manager                                  │   │
│  │ • Quản lý Whitelist IP                                      │   │
│  │ • Monitoring & Risk Score                                   │   │
│  │ • Xem doanh thu backup                                      │   │
│  └─────────────────────────────────────────────────────────────┘   │
├─────────────────────────────────────────────────────────────────────┤
│                         MANAGER (Store)                             │
│  ┌─────────────────────────────────────────────────────────────┐   │
│  │ • Quản lý stores được Admin gán                             │   │
│  │ • Quản lý đơn hàng của store                                │   │
│  │ • Khóa/Mở khóa USER (không khóa Manager khác)               │   │
│  │ • Quản lý voucher/khuyến mãi                                │   │
│  │ • Live Chat với khách hàng                                  │   │
│  │ • Xem dashboard & thống kê store                            │   │
│  └─────────────────────────────────────────────────────────────┘   │
├─────────────────────────────────────────────────────────────────────┤
│                            USER                                     │
│  ┌─────────────────────────────────────────────────────────────┐   │
│  │ • Đặt hàng, thanh toán                                      │   │
│  │ • Quản lý giỏ hàng                                          │   │
│  │ • Đánh giá sản phẩm                                         │   │
│  │ • Tích điểm, quay vòng xoay                                 │   │
│  │ • Đặt hàng nhóm                                             │   │
│  │ • Live Chat hỗ trợ                                          │   │
│  └─────────────────────────────────────────────────────────────┘   │
├─────────────────────────────────────────────────────────────────────┤
│                            GUEST                                    │
│  ┌─────────────────────────────────────────────────────────────┐   │
│  │ • Xem danh sách sản phẩm                                    │   │
│  │ • Xem chi tiết sản phẩm                                     │   │
│  │ • Tìm kiếm sản phẩm                                         │   │
│  │ • Xem danh sách cửa hàng                                    │   │
│  │ • Xem đánh giá sản phẩm                                     │   │
│  │ • Đăng ký tài khoản                                         │   │
│  └─────────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────────┘
```

---

## 2. CHI TIẾT TỪNG ROLE

### 2.1 GUEST (Khách Chưa Đăng Nhập)

#### Định nghĩa
Guest là người dùng truy cập ứng dụng nhưng chưa đăng nhập. Họ có thể xem thông tin nhưng không thể thực hiện các hành động yêu cầu xác thực.

#### Chức năng được phép

| STT | Chức năng | Mô tả |
|-----|-----------|-------|
| 1 | Xem trang chủ | Banner, Best Seller, For You |
| 2 | Xem thực đơn | Danh sách sản phẩm, danh mục |
| 3 | Xem chi tiết sản phẩm | Thông tin, giá, size, topping |
| 4 | Tìm kiếm sản phẩm | Text search, voice search |
| 5 | Xem đánh giá | Rating, comment của sản phẩm |
| 6 | Xem cửa hàng | Danh sách, vị trí, giờ mở cửa |
| 7 | Đăng ký tài khoản | Tạo tài khoản mới với OTP |
| 8 | Đăng nhập | Chuyển thành USER |
| 9 | Quên mật khẩu | Reset password qua OTP |

#### Chức năng bị hạn chế

| STT | Chức năng | Yêu cầu |
|-----|-----------|---------|
| 1 | Thêm vào giỏ hàng | Cần đăng nhập |
| 2 | Đặt hàng | Cần đăng nhập |
| 3 | Đánh giá sản phẩm | Cần đăng nhập |
| 4 | Tích điểm, quay vòng xoay | Cần đăng nhập |
| 5 | Live Chat | Cần đăng nhập |
| 6 | Đặt hàng nhóm | Cần đăng nhập |

#### Luồng hoạt động Guest

```
┌──────────────┐
│   GUEST      │
│  Mở App      │
└──────┬───────┘
       │
       ▼
┌──────────────────────────────────────────────────────────────┐
│                    TRANG CHỦ (PUBLIC)                        │
│  • Xem Banner quảng cáo                                      │
│  • Xem Best Seller                                           │
│  • Xem For You (random)                                      │
│  • Xem thời tiết                                             │
└──────────┬───────────────────────────────────────────────────┘
           │
           ├─────────────────┬─────────────────┬────────────────┐
           ▼                 ▼                 ▼                ▼
    ┌────────────┐    ┌────────────┐    ┌────────────┐   ┌────────────┐
    │ Xem Menu   │    │ Tìm kiếm   │    │ Xem Store  │   │ Đăng nhập/ │
    │            │    │            │    │            │   │ Đăng ký    │
    └─────┬──────┘    └─────┬──────┘    └────────────┘   └─────┬──────┘
          │                 │                                  │
          ▼                 ▼                                  ▼
    ┌────────────┐    ┌────────────┐                    ┌────────────┐
    │ Chi tiết   │    │ Kết quả    │                    │ Chuyển     │
    │ sản phẩm   │    │ tìm kiếm   │                    │ thành USER │
    └─────┬──────┘    └────────────┘                    └────────────┘
          │
          ▼
    ┌────────────────────────────────────────────────────────────┐
    │ ⚠️ THÊM VÀO GIỎ HÀNG → Yêu cầu đăng nhập                  │
    │    → Hiển thị dialog: "Vui lòng đăng nhập để tiếp tục"    │
    └────────────────────────────────────────────────────────────┘
```

---

### 2.2 USER (Người Dùng Đã Đăng Nhập)

#### Định nghĩa
User là người dùng đã đăng ký và đăng nhập vào hệ thống. Họ có đầy đủ quyền sử dụng các tính năng dành cho khách hàng.

#### Chức năng đầy đủ

| STT | Nhóm chức năng | Chức năng chi tiết |
|-----|----------------|-------------------|
| 1 | **Tài khoản** | Xem/Sửa profile, Upload avatar, Đổi mật khẩu, Xóa tài khoản |
| 2 | **Giỏ hàng** | Thêm/Sửa/Xóa sản phẩm, Chọn size/topping, Áp voucher |
| 3 | **Đặt hàng** | Tạo đơn, Chọn phương thức thanh toán, Theo dõi trạng thái |
| 4 | **Thanh toán** | COD, VNPay, MoMo, PayPal, VietQR |
| 5 | **Đánh giá** | Đánh giá sao, Viết comment, Upload ảnh |
| 6 | **Loyalty** | Tích điểm, Quay vòng xoay, Nhận voucher, Nâng hạng |
| 7 | **Đặt hàng nhóm** | Tạo/Tham gia nhóm, Chat nhóm, Checkout nhóm |
| 8 | **Live Chat** | Chat với nhân viên hỗ trợ |
| 9 | **Thông báo** | Nhận push notification, Xem lịch sử thông báo |
| 10 | **AI Features** | Voice Order, Predictive Order, Chatbot AI |

#### Member Tier (Hạng thành viên)

| Tier | Điểm yêu cầu | Giảm giá | Nhân điểm | Free Ship |
|------|--------------|----------|-----------|-----------|
| BRONZE | 0-49 | 0% | 1x | ❌ |
| SILVER | 50-149 | 5% | 1.5x | Đơn từ 100K |
| GOLD | 150-299 | 10% | 2x | Đơn từ 50K |
| PLATINUM | 300+ | 15% | 3x | Mọi đơn |

---

### 2.3 MANAGER (Quản Lý - Bao Gồm Admin)

#### Định nghĩa
Manager là người quản lý cửa hàng, có quyền quản lý đơn hàng, sản phẩm, người dùng và xem thống kê. Admin là Manager với quyền cao nhất.

#### Phân loại Manager

| Loại | Phạm vi quản lý | Quyền đặc biệt |
|------|-----------------|----------------|
| **Manager (Store)** | Chỉ stores được gán | Quản lý đơn hàng, voucher, live chat |
| **Manager (Admin)** | Tất cả stores | Nâng/Hạ cấp user, Gán store, Whitelist IP, Monitoring |

#### Chức năng Manager (Store)

| STT | Nhóm chức năng | Chức năng chi tiết |
|-----|----------------|-------------------|
| 1 | **Đơn hàng** | Xem/Cập nhật trạng thái đơn hàng của store |
| 2 | **Sản phẩm** | CRUD sản phẩm, Upload ảnh, Quản lý danh mục |
| 3 | **Voucher** | Tạo/Sửa/Xóa voucher, Theo dõi usage |
| 4 | **Người dùng** | Xem danh sách, Khóa/Mở khóa USER |
| 5 | **Live Chat** | Trả lời chat khách hàng |
| 6 | **Dashboard** | Thống kê doanh thu, Top sản phẩm |
| 7 | **Dự báo** | Dự báo doanh thu, Giờ cao điểm, Đề xuất nhân sự |
| 8 | **Thông báo** | Gửi push notification cho khách hàng |

#### Chức năng Manager (Admin) - Bổ sung

| STT | Nhóm chức năng | Chức năng chi tiết |
|-----|----------------|-------------------|
| 1 | **Quản lý Store** | Quản lý TẤT CẢ stores |
| 2 | **Phân quyền** | Nâng User → Manager, Hạ Manager → User |
| 3 | **Gán Store** | Gán/Bỏ gán store cho Manager |
| 4 | **Whitelist IP** | Quản lý IP được phép truy cập |
| 5 | **Monitoring** | Giám sát hành vi, Risk Score, Cảnh báo |
| 6 | **Block IP** | Chặn IP có hành vi xấu |
| 7 | **Backup** | Xem doanh thu backup của user đã xóa |

---

## 3. LUỒNG HOẠT ĐỘNG THEO ROLE

### 3.1 Luồng Đăng Ký & Đăng Nhập

```
┌─────────────────────────────────────────────────────────────────────┐
│                    LUỒNG ĐĂNG KÝ TÀI KHOẢN                          │
└─────────────────────────────────────────────────────────────────────┘

    ┌──────────────┐
    │    GUEST     │
    │  Mở App      │
    └──────┬───────┘
           │
           ▼
    ┌──────────────────────────────────────────────────────────────┐
    │ 1. NHẬP THÔNG TIN ĐĂNG KÝ                                    │
    │    • Username (3-50 ký tự)                                   │
    │    • Email (định dạng hợp lệ)                                │
    │    • Password (6-100 ký tự)                                  │
    │    • Phone (số điện thoại VN)                                │
    │    • Full Name, Address (tùy chọn)                           │
    └──────────┬───────────────────────────────────────────────────┘
               │
               ▼
    ┌──────────────────────────────────────────────────────────────┐
    │ 2. GỬI OTP QUA EMAIL                                         │
    │    • Backend tạo OTP 6 số                                    │
    │    • Gửi email qua SendGrid                                  │
    │    • OTP có hiệu lực 5 phút                                  │
    └──────────┬───────────────────────────────────────────────────┘
               │
               ▼
    ┌──────────────────────────────────────────────────────────────┐
    │ 3. XÁC THỰC OTP                                              │
    │    • User nhập mã OTP 6 số                                   │
    │    • Backend verify OTP                                      │
    │    • Nếu đúng → Kích hoạt tài khoản                          │
    │    • Nếu sai/hết hạn → Cho phép Resend OTP                   │
    └──────────┬───────────────────────────────────────────────────┘
               │
               ▼
    ┌──────────────────────────────────────────────────────────────┐
    │ 4. TÀI KHOẢN ĐƯỢC KÍCH HOẠT                                  │
    │    • Role mặc định: USER                                     │
    │    • Member Tier: BRONZE                                     │
    │    • Points: 0                                               │
    │    • Chuyển đến màn hình Login                               │
    └──────────────────────────────────────────────────────────────┘
```

```
┌─────────────────────────────────────────────────────────────────────┐
│                    LUỒNG ĐĂNG NHẬP                                  │
└─────────────────────────────────────────────────────────────────────┘

    ┌──────────────┐
    │    GUEST     │
    └──────┬───────┘
           │
           ▼
    ┌──────────────────────────────────────────────────────────────┐
    │ 1. NHẬP THÔNG TIN ĐĂNG NHẬP                                  │
    │    • Username/Phone + Password                               │
    │    • HOẶC Biometric (vân tay/Face ID)                        │
    └──────────┬───────────────────────────────────────────────────┘
               │
               ▼
    ┌──────────────────────────────────────────────────────────────┐
    │ 2. XÁC THỰC                                                  │
    │    • Backend verify credentials                              │
    │    • Kiểm tra tài khoản active & không bị block              │
    │    • Ghi log đăng nhập (monitoring)                          │
    └──────────┬───────────────────────────────────────────────────┘
               │
               ▼
    ┌──────────────────────────────────────────────────────────────┐
    │ 3. TRẢ VỀ JWT TOKEN                                          │
    │    • Access Token (24h)                                      │
    │    • Refresh Token                                           │
    │    • Thông tin user (role, tier, points)                     │
    └──────────┬───────────────────────────────────────────────────┘
               │
               ├─────────────────────────────────────────────────────┐
               │                                                     │
               ▼                                                     ▼
    ┌──────────────────────┐                          ┌──────────────────────┐
    │ Role = USER          │                          │ Role = MANAGER       │
    │ → MainActivity       │                          │ → ManagerActivity    │
    │ (Bottom Navigation)  │                          │ (Dashboard)          │
    └──────────────────────┘                          └──────────────────────┘
```

### 3.2 Luồng Đặt Hàng (USER)

```
┌─────────────────────────────────────────────────────────────────────┐
│                    LUỒNG ĐẶT HÀNG - USER                            │
└─────────────────────────────────────────────────────────────────────┘

    ┌──────────────┐
    │     USER     │
    │  Đã đăng nhập│
    └──────┬───────┘
           │
           ▼
    ┌──────────────────────────────────────────────────────────────┐
    │ 1. CHỌN SẢN PHẨM                                             │
    │    • Xem Menu / Tìm kiếm / Voice Search                      │
    │    • Xem chi tiết sản phẩm                                   │
    │    • Chọn Size, Topping, Số lượng                            │
    │    • Nhập ghi chú (ít đường, nhiều đá...)                    │
    └──────────┬───────────────────────────────────────────────────┘
               │
               ▼
    ┌──────────────────────────────────────────────────────────────┐
    │ 2. THÊM VÀO GIỎ HÀNG                                         │
    │    • Tính giá: (basePrice + sizeExtra + toppings) × quantity │
    │    • Animation add-to-cart                                   │
    │    • Cập nhật badge giỏ hàng                                 │
    └──────────┬───────────────────────────────────────────────────┘
               │
               ▼
    ┌──────────────────────────────────────────────────────────────┐
    │ 3. XEM GIỎ HÀNG                                              │
    │    • Danh sách sản phẩm đã chọn                              │
    │    • Select/Unselect từng item                               │
    │    • Cập nhật số lượng                                       │
    │    • Xóa sản phẩm                                            │
    └──────────┬───────────────────────────────────────────────────┘
               │
               ▼
    ┌──────────────────────────────────────────────────────────────┐
    │ 4. ÁP DỤNG GIẢM GIÁ                                          │
    │    • Nhập mã voucher (promotion)                             │
    │    • Chọn voucher từ Spin Wheel                              │
    │    • Tự động áp dụng Tier Discount                           │
    │    • Tính: finalPrice = subtotal - discount + shippingFee    │
    └──────────┬───────────────────────────────────────────────────┘
               │
               ▼
    ┌──────────────────────────────────────────────────────────────┐
    │ 5. CHỌN THÔNG TIN GIAO HÀNG                                  │
    │    • Loại đơn: DELIVERY / PICKUP                             │
    │    • Chọn cửa hàng                                           │
    │    • Nhập địa chỉ (nếu DELIVERY)                             │
    │    • Tính phí ship (GHN API)                                 │
    └──────────┬───────────────────────────────────────────────────┘
               │
               ▼
    ┌──────────────────────────────────────────────────────────────┐
    │ 6. CHỌN PHƯƠNG THỨC THANH TOÁN                               │
    │    • COD (Tiền mặt khi nhận)                                 │
    │    • VNPay (Online)                                          │
    │    • MoMo (Ví điện tử)                                       │
    │    • PayPal (Quốc tế)                                        │
    │    • VietQR (Quét mã)                                        │
    └──────────┬───────────────────────────────────────────────────┘
               │
               ▼
    ┌──────────────────────────────────────────────────────────────┐
    │ 7. XÁC NHẬN ĐẶT HÀNG                                         │
    │    • Preview Bill                                            │
    │    • OTP xác thực số điện thoại (nếu cần)                    │
    │    • Tạo đơn hàng → Status: PENDING                          │
    │    • Gửi notification cho Manager                            │
    └──────────┬───────────────────────────────────────────────────┘
               │
               ▼
    ┌──────────────────────────────────────────────────────────────┐
    │ 8. THEO DÕI ĐƠN HÀNG                                         │
    │    • WebSocket realtime update                               │
    │    • Push notification khi đổi trạng thái                    │
    │    • PENDING → MAKING → SHIPPING/READY → DONE                │
    └──────────────────────────────────────────────────────────────┘
```

### 3.3 Luồng Quản Lý Đơn Hàng (MANAGER)

```
┌─────────────────────────────────────────────────────────────────────┐
│                LUỒNG QUẢN LÝ ĐƠN HÀNG - MANAGER                     │
└─────────────────────────────────────────────────────────────────────┘

    ┌──────────────┐
    │   MANAGER    │
    │  Đã đăng nhập│
    └──────┬───────┘
           │
           ▼
    ┌──────────────────────────────────────────────────────────────┐
    │ 1. KIỂM TRA QUYỀN & STORE                                    │
    │    • Xác thực role = MANAGER                                 │
    │    • Lấy danh sách stores được gán                           │
    │    • Admin: quản lý tất cả stores                            │
    │    • Manager: chỉ stores được gán                            │
    └──────────┬───────────────────────────────────────────────────┘
               │
               ▼
    ┌──────────────────────────────────────────────────────────────┐
    │ 2. XEM DANH SÁCH ĐƠN HÀNG                                    │
    │    • Filter theo store (nếu Manager)                         │
    │    • Filter theo trạng thái                                  │
    │    • Pagination                                              │
    │    • WebSocket nhận đơn mới realtime                         │
    └──────────┬───────────────────────────────────────────────────┘
               │
               ▼
    ┌──────────────────────────────────────────────────────────────┐
    │ 3. CẬP NHẬT TRẠNG THÁI ĐƠN HÀNG                              │
    │                                                              │
    │    PENDING ──────► MAKING ──────► SHIPPING ──────► DONE      │
    │       │              │              │                        │
    │       │              │              ▼                        │
    │       │              │           READY ──────────► DONE      │
    │       │              │                                       │
    │       ▼              ▼                                       │
    │    CANCELED       CANCELED                                   │
    │                                                              │
    └──────────┬───────────────────────────────────────────────────┘
               │
               ▼
    ┌──────────────────────────────────────────────────────────────┐
    │ 4. GỬI THÔNG BÁO CHO KHÁCH HÀNG                              │
    │    • WebSocket realtime update                               │
    │    • Push notification (OneSignal)                           │
    │    • Email notification                                      │
    └──────────────────────────────────────────────────────────────┘
```

### 3.4 Luồng Đặt Hàng Nhóm (USER)

```
┌─────────────────────────────────────────────────────────────────────┐
│                    LUỒNG ĐẶT HÀNG NHÓM                              │
└─────────────────────────────────────────────────────────────────────┘

    ┌──────────────┐                              ┌──────────────┐
    │   HOST       │                              │   MEMBER     │
    │   (USER)     │                              │   (USER)     │
    └──────┬───────┘                              └──────┬───────┘
           │                                             │
           ▼                                             │
    ┌──────────────────────┐                             │
    │ 1. TẠO PHIÊN NHÓM    │                             │
    │    • Chọn store      │                             │
    │    • Chọn loại đơn   │                             │
    │    • Set max members │                             │
    │    • Set thời hạn    │                             │
    └──────────┬───────────┘                             │
               │                                         │
               ▼                                         │
    ┌──────────────────────┐                             │
    │ 2. NHẬN INVITE CODE  │                             │
    │    (6 ký tự)         │─────────────────────────────┤
    │    • Share link      │                             │
    │    • QR Code         │                             │
    └──────────┬───────────┘                             │
               │                                         ▼
               │                              ┌──────────────────────┐
               │                              │ 3. THAM GIA NHÓM     │
               │                              │    • Nhập invite code│
               │                              │    • Verify & Join   │
               │                              └──────────┬───────────┘
               │                                         │
               ▼                                         ▼
    ┌─────────────────────────────────────────────────────────────────┐
    │ 4. PHIÊN ĐẶT HÀNG NHÓM (REALTIME)                               │
    │    • Tất cả thành viên thêm món                                 │
    │    • Chat nhóm realtime (WebSocket)                             │
    │    • Xem danh sách món của mọi người                            │
    │    • Tính tổng tiền realtime                                    │
    └──────────┬──────────────────────────────────────────────────────┘
               │
               ▼
    ┌──────────────────────────────────────────────────────────────┐
    │ 5. HOST CONTROLS                                             │
    │    • Lock/Unlock phiên (ngăn thêm món)                       │
    │    • Xóa món của bất kỳ ai                                   │
    │    • Kick member                                             │
    │    • Hủy phiên                                               │
    └──────────┬───────────────────────────────────────────────────┘
               │
               ▼
    ┌──────────────────────────────────────────────────────────────┐
    │ 6. CHECKOUT (CHỈ HOST)                                       │
    │    • Lock phiên                                              │
    │    • Áp voucher (nếu có)                                     │
    │    • Chọn phương thức thanh toán                             │
    │    • Tạo đơn hàng chung                                      │
    │    • Thông báo cho tất cả thành viên                         │
    └──────────────────────────────────────────────────────────────┘
```

---

## 4. MA TRẬN CHỨC NĂNG THEO ROLE

### 4.1 Chức Năng Xem (Read)

| Chức năng | GUEST | USER | MANAGER |
|-----------|:-----:|:----:|:-------:|
| Xem trang chủ | ✅ | ✅ | ✅ |
| Xem thực đơn | ✅ | ✅ | ✅ |
| Xem chi tiết sản phẩm | ✅ | ✅ | ✅ |
| Xem đánh giá sản phẩm | ✅ | ✅ | ✅ |
| Xem cửa hàng | ✅ | ✅ | ✅ |
| Xem giỏ hàng | ❌ | ✅ | ❌ |
| Xem lịch sử đơn hàng (của mình) | ❌ | ✅ | ❌ |
| Xem đơn hàng (của store) | ❌ | ❌ | ✅ |
| Xem tất cả đơn hàng | ❌ | ❌ | ✅ (Admin) |
| Xem dashboard thống kê | ❌ | ❌ | ✅ |
| Xem danh sách người dùng | ❌ | ❌ | ✅ |
| Xem monitoring/risk score | ❌ | ❌ | ✅ (Admin) |

### 4.2 Chức Năng Tạo (Create)

| Chức năng | GUEST | USER | MANAGER |
|-----------|:-----:|:----:|:-------:|
| Đăng ký tài khoản | ✅ | ❌ | ❌ |
| Thêm vào giỏ hàng | ❌ | ✅ | ❌ |
| Tạo đơn hàng | ❌ | ✅ | ❌ |
| Tạo đánh giá | ❌ | ✅ | ❌ |
| Tạo phiên đặt hàng nhóm | ❌ | ✅ | ❌ |
| Tạo voucher | ❌ | ❌ | ✅ |
| Tạo sản phẩm | ❌ | ❌ | ✅ |
| Tạo danh mục | ❌ | ❌ | ✅ |
| Gửi thông báo | ❌ | ❌ | ✅ |

### 4.3 Chức Năng Sửa (Update)

| Chức năng | GUEST | USER | MANAGER |
|-----------|:-----:|:----:|:-------:|
| Sửa profile | ❌ | ✅ | ✅ |
| Sửa giỏ hàng | ❌ | ✅ | ❌ |
| Cập nhật trạng thái đơn hàng | ❌ | ❌ | ✅ |
| Sửa voucher | ❌ | ❌ | ✅ |
| Sửa sản phẩm | ❌ | ❌ | ✅ |
| Khóa/Mở khóa USER | ❌ | ❌ | ✅ |
| Khóa/Mở khóa MANAGER | ❌ | ❌ | ✅ (Admin) |
| Nâng cấp User → Manager | ❌ | ❌ | ✅ (Admin) |
| Gán store cho Manager | ❌ | ❌ | ✅ (Admin) |

### 4.4 Chức Năng Xóa (Delete)

| Chức năng | GUEST | USER | MANAGER |
|-----------|:-----:|:----:|:-------:|
| Xóa tài khoản (của mình) | ❌ | ✅ | ✅ |
| Xóa sản phẩm trong giỏ | ❌ | ✅ | ❌ |
| Hủy đơn hàng (của mình) | ❌ | ✅ | ❌ |
| Hủy đơn hàng (của store) | ❌ | ❌ | ✅ |
| Xóa voucher | ❌ | ❌ | ✅ |
| Xóa sản phẩm | ❌ | ❌ | ✅ |
| Block IP | ❌ | ❌ | ✅ (Admin) |

---

## 5. LUỒNG CHUYỂN ĐỔI ROLE

### 5.1 Sơ Đồ Chuyển Đổi Role

```
┌─────────────────────────────────────────────────────────────────────┐
│                    LUỒNG CHUYỂN ĐỔI ROLE                            │
└─────────────────────────────────────────────────────────────────────┘

    ┌──────────────┐
    │    GUEST     │
    └──────┬───────┘
           │ Đăng ký + OTP Verify
           ▼
    ┌──────────────┐
    │     USER     │◄─────────────────────────────────────────────────┐
    └──────┬───────┘                                                  │
           │                                                          │
           │ Admin nâng cấp                                           │
           │ PUT /api/manager/users/{id}/promote                      │
           ▼                                                          │
    ┌──────────────┐                                                  │
    │   MANAGER    │──────────────────────────────────────────────────┘
    │   (Store)    │  Admin hạ cấp
    └──────┬───────┘  PUT /api/manager/users/{id}/demote
           │
           │ Admin gán store
           │ POST /api/manager/users/{id}/stores/{storeId}
           ▼
    ┌──────────────┐
    │   MANAGER    │
    │   (Admin)    │ ← Có quyền quản lý tất cả stores
    └──────────────┘
```

### 5.2 Điều Kiện Chuyển Đổi Role

| Chuyển đổi | Điều kiện | Người thực hiện |
|------------|-----------|-----------------|
| GUEST → USER | Đăng ký + Xác thực OTP | Tự động |
| USER → MANAGER | Admin nâng cấp | Admin |
| MANAGER → USER | Admin hạ cấp | Admin |
| MANAGER → MANAGER (Admin) | Gán tất cả stores | Admin |

### 5.3 API Chuyển Đổi Role

```
# Nâng cấp User → Manager (Chỉ Admin)
PUT /api/manager/users/{userId}/promote
Authorization: Bearer {admin_token}

Response:
{
  "success": true,
  "message": "User promoted to Manager",
  "data": { ...user with role=MANAGER... }
}

# Hạ cấp Manager → User (Chỉ Admin)
PUT /api/manager/users/{userId}/demote
Authorization: Bearer {admin_token}

Response:
{
  "success": true,
  "message": "Manager demoted to User",
  "data": { ...user with role=USER... }
}

# Gán Store cho Manager (Chỉ Admin)
POST /api/manager/users/{userId}/stores/{storeId}
Authorization: Bearer {admin_token}

Response:
{
  "success": true,
  "message": "Store assigned to Manager",
  "data": { ...manager with assigned store... }
}

# Bỏ gán Store (Chỉ Admin)
DELETE /api/manager/users/{userId}/stores/{storeId}
Authorization: Bearer {admin_token}

Response:
{
  "success": true,
  "message": "Store unassigned from Manager"
}
```

---

## 6. SƠ ĐỒ LUỒNG HOẠT ĐỘNG CHI TIẾT

### 6.1 Luồng Tổng Quan Hệ Thống

```
┌─────────────────────────────────────────────────────────────────────────────────┐
│                         TỔNG QUAN LUỒNG HOẠT ĐỘNG HỆ THỐNG                      │
└─────────────────────────────────────────────────────────────────────────────────┘

                                    ┌─────────────┐
                                    │   GUEST     │
                                    └──────┬──────┘
                                           │
                    ┌──────────────────────┼──────────────────────┐
                    │                      │                      │
                    ▼                      ▼                      ▼
            ┌───────────────┐      ┌───────────────┐      ┌───────────────┐
            │ Xem sản phẩm  │      │ Tìm kiếm      │      │ Đăng ký/      │
            │ Xem cửa hàng  │      │ Voice Search  │      │ Đăng nhập     │
            └───────────────┘      └───────────────┘      └───────┬───────┘
                                                                  │
                                                                  ▼
                                                          ┌───────────────┐
                                                          │ Xác thực JWT  │
                                                          └───────┬───────┘
                                                                  │
                                    ┌─────────────────────────────┼─────────────────────────────┐
                                    │                             │                             │
                                    ▼                             ▼                             ▼
                            ┌───────────────┐             ┌───────────────┐             ┌───────────────┐
                            │     USER      │             │   MANAGER     │             │    ADMIN      │
                            │               │             │   (Store)     │             │   (Manager)   │
                            └───────┬───────┘             └───────┬───────┘             └───────┬───────┘
                                    │                             │                             │
        ┌───────────────────────────┼───────────────────────────┐ │                             │
        │           │               │               │           │ │                             │
        ▼           ▼               ▼               ▼           ▼ ▼                             ▼
┌─────────────┐ ┌─────────┐ ┌─────────────┐ ┌─────────────┐ ┌─────────────┐             ┌─────────────┐
│ Đặt hàng   │ │ Giỏ hàng│ │ Đánh giá    │ │ Loyalty     │ │ Quản lý     │             │ Monitoring  │
│ Thanh toán │ │ Voucher │ │ Review      │ │ Spin Wheel  │ │ Đơn hàng    │             │ Risk Score  │
│ Theo dõi   │ │         │ │             │ │ Member Tier │ │ Sản phẩm    │             │ Block IP    │
└─────────────┘ └─────────┘ └─────────────┘ └─────────────┘ │ Voucher     │             │ Whitelist   │
                                                           │ Live Chat   │             │ Phân quyền  │
                                                           │ Dashboard   │             └─────────────┘
                                                           └─────────────┘
```

### 6.2 Luồng Xử Lý Request

```
┌─────────────────────────────────────────────────────────────────────────────────┐
│                         LUỒNG XỬ LÝ REQUEST                                     │
└─────────────────────────────────────────────────────────────────────────────────┘

    ┌──────────────┐
    │ Android App  │
    │ (Client)     │
    └──────┬───────┘
           │ HTTP Request + JWT Token
           ▼
    ┌──────────────────────────────────────────────────────────────────────────┐
    │                         SECURITY FILTERS                                 │
    │                                                                          │
    │  ┌────────────────┐     ┌────────────────┐     ┌────────────────────┐   │
    │  │ BlockedIPFilter│────▶│ JwtAuthFilter  │────▶│ WhitelistIPFilter  │   │
    │  │                │     │                │     │ (Admin/Manager)    │   │
    │  │ Kiểm tra IP    │     │ Verify JWT     │     │                    │   │
    │  │ có bị block    │     │ Extract user   │     │ Kiểm tra IP trong  │   │
    │  │                │     │ Set auth       │     │ whitelist          │   │
    │  └────────────────┘     └────────────────┘     └────────────────────┘   │
    │                                                                          │
    └──────────────────────────────────────────────────────────────────────────┘
                                       │
                                       ▼
    ┌──────────────────────────────────────────────────────────────────────────┐
    │                         AUTHORIZATION                                    │
    │                                                                          │
    │  @PreAuthorize("hasRole('USER')")        → Chỉ USER                     │
    │  @PreAuthorize("hasRole('MANAGER')")     → Chỉ MANAGER                  │
    │  @PreAuthorize("hasAnyRole('MANAGER', 'ADMIN')") → MANAGER hoặc ADMIN   │
    │  @PreAuthorize("hasRole('ADMIN')")       → Chỉ ADMIN                    │
    │                                                                          │
    └──────────────────────────────────────────────────────────────────────────┘
                                       │
                                       ▼
    ┌──────────────────────────────────────────────────────────────────────────┐
    │                         CONTROLLER → SERVICE → REPOSITORY                │
    │                                                                          │
    │  Controller: Nhận request, validate input                                │
    │  Service: Business logic, kiểm tra quyền theo store                      │
    │  Repository: Truy vấn database                                           │
    │                                                                          │
    └──────────────────────────────────────────────────────────────────────────┘
                                       │
                                       ▼
    ┌──────────────────────────────────────────────────────────────────────────┐
    │                         RESPONSE                                         │
    │                                                                          │
    │  {                                                                       │
    │    "success": true/false,                                                │
    │    "message": "...",                                                     │
    │    "data": { ... }                                                       │
    │  }                                                                       │
    │                                                                          │
    └──────────────────────────────────────────────────────────────────────────┘
```

### 6.3 Luồng Loyalty & Gamification

```
┌─────────────────────────────────────────────────────────────────────────────────┐
│                         LUỒNG LOYALTY & GAMIFICATION                            │
└─────────────────────────────────────────────────────────────────────────────────┘

    ┌──────────────┐
    │     USER     │
    └──────┬───────┘
           │
           ▼
    ┌──────────────────────────────────────────────────────────────┐
    │ 1. TÍCH ĐIỂM                                                 │
    │    • Mỗi đơn hàng DONE = 1 điểm cơ bản                       │
    │    • Nhân với hệ số tier:                                    │
    │      - BRONZE: 1x                                            │
    │      - SILVER: 1.5x                                          │
    │      - GOLD: 2x                                              │
    │      - PLATINUM: 3x                                          │
    └──────────┬───────────────────────────────────────────────────┘
               │
               ▼
    ┌──────────────────────────────────────────────────────────────┐
    │ 2. NÂNG HẠNG TỰ ĐỘNG                                         │
    │    • BRONZE: 0-49 điểm                                       │
    │    • SILVER: 50-149 điểm                                     │
    │    • GOLD: 150-299 điểm                                      │
    │    • PLATINUM: 300+ điểm                                     │
    └──────────┬───────────────────────────────────────────────────┘
               │
               ▼
    ┌──────────────────────────────────────────────────────────────┐
    │ 3. QUAY VÒNG XOAY (5 điểm = 1 lượt)                          │
    │    • 70% cơ hội: Voucher giảm giá (5%, 10%, 15%, 20%)        │
    │    • 30% cơ hội: "Chúc may mắn lần sau"                      │
    │    • Voucher được lưu vào tài khoản                          │
    └──────────┬───────────────────────────────────────────────────┘
               │
               ▼
    ┌──────────────────────────────────────────────────────────────┐
    │ 4. SỬ DỤNG VOUCHER                                           │
    │    • Áp dụng khi checkout                                    │
    │    • Kết hợp với voucher promotion                           │
    │    • Kết hợp với tier discount                               │
    └──────────────────────────────────────────────────────────────┘
```

---

## 📊 TỔNG KẾT

### Hệ thống UTE Tea có 3 role chính:

1. **GUEST**: Khách chưa đăng nhập
   - Xem sản phẩm, tìm kiếm, xem cửa hàng
   - Không thể đặt hàng, đánh giá

2. **USER**: Người dùng đã đăng nhập
   - Đầy đủ chức năng khách hàng
   - Đặt hàng, thanh toán, đánh giá, loyalty
   - Đặt hàng nhóm, live chat

3. **MANAGER**: Quản lý (bao gồm Admin)
   - Manager (Store): Quản lý stores được gán
   - Manager (Admin): Quản lý tất cả, phân quyền, monitoring

### Luồng chuyển đổi:
- GUEST → USER: Đăng ký + OTP
- USER → MANAGER: Admin nâng cấp
- MANAGER → USER: Admin hạ cấp

### Bảo mật:
- JWT Authentication
- Role-based Authorization
- Whitelist IP cho Admin/Manager
- Blocked IP cho hành vi xấu
- Rate limiting
- Monitoring & Risk Score
