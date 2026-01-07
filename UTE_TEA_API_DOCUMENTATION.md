# 🔌 API DOCUMENTATION - UTE TEA

## 📋 MỤC LỤC
1. [Authentication APIs](#1-authentication-apis)
2. [User Profile APIs](#2-user-profile-apis)
3. [Product APIs](#3-product-apis)
4. [Cart APIs](#4-cart-apis)
5. [Order APIs](#5-order-apis)
6. [Payment APIs](#6-payment-apis)
7. [Promotion APIs](#7-promotion-apis)
8. [Group Order APIs](#8-group-order-apis)
9. [Notification APIs](#9-notification-apis)
10. [Loyalty APIs](#10-loyalty-apis)
11. [Manager APIs](#11-manager-apis)
12. [Admin APIs](#12-admin-apis)
13. [Monitoring APIs](#13-monitoring-apis)
14. [Blocked IP Management](#14-blocked-ip-management)
14.1. [Whitelist IP Management](#141-whitelist-ip-management)
15. [Shipping APIs](#15-shipping-apis)
16. [Challenge APIs](#16-challenge-apis)
17. [Banner APIs](#17-banner-apis)

---

## 1. AUTHENTICATION APIs

### Register with OTP
```
POST /api/auth/register-with-otp
Content-Type: application/json

Request:
{
  "username": "user123",
  "email": "user@example.com",
  "phone": "0912345678",
  "password": "Password@123"
}

Response:
{
  "success": true,
  "message": "OTP đã được gửi thành công!",
  "data": "Vui lòng kiểm tra email: user@example.com"
}
```

### Verify OTP
```
POST /api/auth/otp-verify
Content-Type: application/json

Request:
{
  "email": "user@example.com",
  "otp": "123456"
}

Response:
{
  "success": true,
  "message": "Kích hoạt tài khoản thành công!",
  "data": "Vui lòng đăng nhập để tiếp tục."
}
```

### Resend OTP
```
POST /api/auth/resend-otp?target=user@example.com
Response: { "success": true, "message": "OTP resent successfully" }
```

### Login
```
POST /api/auth/login
Content-Type: application/json

Request:
{
  "username": "user123",
  "password": "Password@123"
}

Response:
{
  "success": true,
  "message": "Login successful",
  "data": {
    "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "user": {
      "id": 1,
      "username": "user123",
      "email": "user@example.com",
      "role": "USER",
      "memberTier": "BRONZE"
    }
  }
}
```

### Refresh Token
```
POST /api/auth/refresh-token
Content-Type: application/json

Request:
{
  "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}

Response:
{
  "success": true,
  "data": {
    "accessToken": "new_token...",
    "refreshToken": "new_refresh_token..."
  }
}
```

### Forgot Password
```
POST /api/auth/forgot-password
Request: { "email": "user@example.com" }
Response: "Mã xác nhận đã được gửi đến email của bạn."
```

### Reset Password
```
POST /api/auth/reset-password
Request:
{
  "email": "user@example.com",
  "otp": "123456",
  "newPassword": "NewPassword@123"
}
Response: "Đặt lại mật khẩu thành công."
```

---

## 2. USER PROFILE APIs

### Get My Profile
```
GET /api/me
Authorization: Bearer {accessToken}

Response:
{
  "success": true,
  "data": {
    "id": 1,
    "username": "user123",
    "email": "user@example.com",
    "phone": "0912345678",
    "fullName": "Nguyễn Văn A",
    "address": "123 Đường ABC, TP.HCM",
    "memberTier": "SILVER",
    "points": 250,
    "avatarUrl": "https://..."
  }
}
```

### Update Profile
```
PUT /api/me
Authorization: Bearer {accessToken}
Content-Type: application/json

Request:
{
  "fullName": "Nguyễn Văn A",
  "phone": "0912345678",
  "address": "456 Đường XYZ, TP.HCM"
}

Response: { "success": true, "data": { ...updated profile... } }
```

### Upload Avatar
```
POST /api/me/avatar
Authorization: Bearer {accessToken}
Content-Type: multipart/form-data

Request:
- image: [file]

Response: { "success": true, "data": { ...profile with new avatar... } }
```

### Change Password
```
PUT /api/me/change-password
Authorization: Bearer {accessToken}
Content-Type: application/json

Request:
{
  "oldPassword": "OldPassword@123",
  "newPassword": "NewPassword@123"
}

Response: "Đổi mật khẩu thành công"
```

### Delete Account
```
DELETE /api/me
Authorization: Bearer {accessToken}

Response: { "success": true, "message": "Account deleted successfully" }
```

---

## 3. PRODUCT APIs

### Get All Drinks
```
GET /api/drinks
Response:
{
  "success": true,
  "data": [
    {
      "id": 1,
      "name": "Trà sữa Thái",
      "description": "Trà sữa Thái ngon lạ",
      "basePrice": 35000,
      "imageUrl": "https://...",
      "category": { "id": 1, "name": "Trà sữa" },
      "sizes": [
        { "id": 1, "sizeName": "M", "extraPrice": 0 },
        { "id": 2, "sizeName": "L", "extraPrice": 5000 }
      ],
      "toppings": [
        { "id": 1, "toppingName": "Trân châu", "price": 5000 },
        { "id": 2, "toppingName": "Thạch", "price": 3000 }
      ]
    }
  ]
}
```

### Get Drink by ID
```
GET /api/drinks/{id}
Response: { "success": true, "data": { ...drink details... } }
```

### Search Drinks
```
GET /api/drinks/search?keyword=trà
Response: { "success": true, "data": [ ...matching drinks... ] }
```

### Get Categories
```
GET /api/categories
Response:
{
  "success": true,
  "data": [
    { "id": 1, "name": "Trà sữa", "imageUrl": "https://..." },
    { "id": 2, "name": "Cà phê", "imageUrl": "https://..." }
  ]
}
```

---

## 4. CART APIs

### Add to Cart
```
POST /api/cart/add
Authorization: Bearer {accessToken}
Content-Type: application/json

Request:
{
  "drinkId": 1,
  "sizeId": 2,
  "quantity": 2,
  "toppingIds": [1, 2],
  "note": "Ít đường"
}

Response:
{
  "success": true,
  "message": "Đã thêm vào giỏ hàng",
  "data": {
    "id": 1,
    "userId": 1,
    "items": [
      {
        "id": 1,
        "drink": { "id": 1, "name": "Trà sữa Thái" },
        "size": { "id": 2, "sizeName": "L" },
        "quantity": 2,
        "unitPrice": 40000,
        "totalPrice": 80000,
        "toppings": [ { "id": 1, "toppingName": "Trân châu" } ],
        "note": "Ít đường"
      }
    ]
  }
}
```

### Get My Cart
```
GET /api/cart
Authorization: Bearer {accessToken}

Response: { "success": true, "data": { ...cart details... } }
```

### Update Cart Item Quantity
```
PUT /api/cart/items/{cartItemId}?quantity=3
Authorization: Bearer {accessToken}

Response: { "success": true, "message": "Đã cập nhật giỏ hàng", "data": { ...updated cart... } }
```

### Update Cart Item Full
```
PUT /api/cart/items/{cartItemId}/full
Authorization: Bearer {accessToken}
Content-Type: application/json

Request:
{
  "sizeId": 2,
  "quantity": 2,
  "toppingIds": [1, 2],
  "note": "Ít đường"
}

Response: { "success": true, "data": { ...updated cart... } }
```

### Remove Cart Item
```
DELETE /api/cart/items/{cartItemId}
Authorization: Bearer {accessToken}

Response: { "success": true, "message": "Đã xóa khỏi giỏ hàng" }
```

### Clear Cart
```
DELETE /api/cart/clear
Authorization: Bearer {accessToken}

Response: { "success": true, "message": "Đã xóa giỏ hàng" }
```

### Reorder from History (Đặt lại đơn hàng)
```
POST /api/cart/reorder
Authorization: Bearer {accessToken}
Content-Type: application/json

Request:
{
  "orderId": 123
}

Response:
{
  "success": true,
  "message": "Đã thêm tất cả món vào giỏ hàng thành công!",
  "data": {
    "cart": { ...cart details... },
    "itemStatuses": [
      {
        "drinkName": "Trà sữa Thái",
        "sizeName": "L",
        "drinkAvailable": true,
        "sizeAvailable": true,
        "toppingStatuses": [
          { "toppingName": "Trân châu", "available": true }
        ],
        "addedToCart": true,
        "reason": null,
        "suggestions": null
      },
      {
        "drinkName": "Trà đào cam sả",
        "sizeName": "M",
        "drinkAvailable": false,
        "sizeAvailable": false,
        "toppingStatuses": [],
        "addedToCart": false,
        "reason": "Món 'Trà đào cam sả' hiện không còn bán",
        "suggestions": [
          {
            "drinkId": 5,
            "drinkName": "Trà đào",
            "drinkImage": "https://...",
            "basePrice": 35000,
            "reason": "Cùng danh mục"
          }
        ]
      }
    ],
    "hasUnavailableItems": true
  }
}
```

---

## 5. ORDER APIs

### Preview Bill
```
POST /api/orders/preview
Authorization: Bearer {accessToken}
Content-Type: application/json

Request:
{
  "storeId": 1,
  "type": "DELIVERY",
  "address": "123 Đường ABC, TP.HCM",
  "pickupTime": "2024-01-15T14:30:00",
  "paymentMethod": "VNPAY",
  "promotionCode": "SAVE10",
  "items": [
    {
      "drinkId": 1,
      "sizeId": 2,
      "quantity": 2,
      "toppingIds": [1, 2],
      "note": "Ít đường"
    }
  ]
}

Response:
{
  "success": true,
  "message": "Bill preview generated",
  "data": {
    "orderId": null,
    "userId": 1,
    "storeId": 1,
    "type": "DELIVERY",
    "address": "123 Đường ABC, TP.HCM",
    "pickupTime": "2024-01-15T14:30:00",
    "paymentMethod": "VNPAY",
    "items": [ ...items... ],
    "subtotal": 80000,
    "discount": 8000,
    "shippingFee": 15000,
    "finalPrice": 87000,
    "promotionCode": "SAVE10"
  }
}
```

### Create Order
```
POST /api/orders
Authorization: Bearer {accessToken}
Content-Type: application/json

Request: { ...same as preview... }

Response:
{
  "success": true,
  "message": "Order created successfully",
  "data": {
    "id": 1,
    "userId": 1,
    "storeId": 1,
    "type": "DELIVERY",
    "status": "PENDING",
    "totalPrice": 80000,
    "discount": 8000,
    "shippingFee": 15000,
    "finalPrice": 87000,
    "paymentMethod": "VNPAY",
    "createdAt": "2024-01-15T10:00:00"
  }
}
```

### Get My Orders
```
GET /api/orders/my
Authorization: Bearer {accessToken}

Response:
{
  "success": true,
  "data": [ ...list of orders... ]
}
```

### Get My Current Orders
```
GET /api/orders/my/current
Authorization: Bearer {accessToken}

Response: { "success": true, "data": [ ...current orders (PENDING, MAKING, SHIPPING, READY)... ] }
```

### Get Order by ID
```
GET /api/orders/{orderId}
Authorization: Bearer {accessToken}

Response: { "success": true, "data": { ...order details... } }
```

### Get All Orders (Manager)
```
GET /api/orders/all?page=0&size=10
Authorization: Bearer {accessToken}
Role: MANAGER

Response:
{
  "success": true,
  "data": {
    "content": [ ...orders... ],
    "totalElements": 100,
    "totalPages": 10,
    "currentPage": 0
  }
}
```

### Update Order Status (Manager)
```
PUT /api/orders/{orderId}/status?status=MAKING
Authorization: Bearer {accessToken}
Role: MANAGER

Response: { "success": true, "message": "Order status updated", "data": { ...updated order... } }
```

---

## 6. PAYMENT APIs

### VNPay - Create Payment
```
POST /api/vnpay/create-payment
Authorization: Bearer {accessToken}
Content-Type: application/json

Request:
{
  "orderId": 1,
  "amount": 87000,
  "orderInfo": "Thanh toán đơn hàng #1"
}

Response:
{
  "success": true,
  "data": {
    "paymentUrl": "https://sandbox.vnpayment.vn/paygate/...",
    "transactionId": "20240115123456"
  }
}
```

### MoMo - Create Payment
```
POST /api/momo/create-payment
Authorization: Bearer {accessToken}
Content-Type: application/json

Request:
{
  "orderId": 1,
  "amount": 87000,
  "orderInfo": "Thanh toán đơn hàng #1"
}

Response: "https://momo.vn/qr/..."
```

### PayPal - Create Payment
```
POST /api/paypal/create-payment
Authorization: Bearer {accessToken}
Content-Type: application/json

Request:
{
  "orderId": 1,
  "amount": 87000,
  "currency": "USD"
}

Response:
{
  "success": true,
  "data": {
    "approvalUrl": "https://www.paypal.com/checkoutnow?token=...",
    "transactionId": "PAYID-..."
  }
}
```

---

## 7. PROMOTION APIs

### Get Active Promotions
```
GET /api/promotions
Response:
{
  "success": true,
  "data": [
    {
      "id": 1,
      "code": "SAVE10",
      "description": "Giảm 10% cho đơn từ 100K",
      "discountType": "PERCENT",
      "discountValue": 10,
      "minOrderValue": 100000,
      "maxDiscountAmount": 50000,
      "startDate": "2024-01-01T00:00:00",
      "endDate": "2024-12-31T23:59:59",
      "isActive": true
    }
  ]
}
```

### Validate Promotion
```
GET /api/promotions/validate?code=SAVE10&orderAmount=150000
Response:
{
  "success": true,
  "message": "Mã voucher hợp lệ",
  "data": { ...promotion details... }
}
```

### Create Promotion (Manager)
```
POST /api/promotions/manager?sendNotification=true
Authorization: Bearer {accessToken}
Role: MANAGER
Content-Type: application/json

Request:
{
  "code": "NEWYEAR20",
  "description": "Giảm 20% năm mới",
  "discountType": "PERCENT",
  "discountValue": 20,
  "minOrderValue": 50000,
  "startDate": "2024-01-01T00:00:00",
  "endDate": "2024-01-31T23:59:59",
  "usageLimit": 100
}

Response: { "success": true, "message": "Tạo voucher thành công", "data": { ...promotion... } }
```

### Update Promotion (Manager)
```
PUT /api/promotions/manager/{id}
Authorization: Bearer {accessToken}
Role: MANAGER
Content-Type: application/json

Request: { ...updated fields... }
Response: { "success": true, "message": "Cập nhật voucher thành công", "data": { ...promotion... } }
```

### Delete Promotion (Manager)
```
DELETE /api/promotions/manager/{id}
Authorization: Bearer {accessToken}
Role: MANAGER

Response: { "success": true, "message": "Xóa voucher thành công" }
```

### Toggle Promotion Status (Manager)
```
PATCH /api/promotions/manager/{id}/toggle-status
Authorization: Bearer {accessToken}
Role: MANAGER

Response: { "success": true, "data": { ...promotion with toggled status... } }
```

---


## 8. GROUP ORDER APIs

### Create Group Order
```
POST /api/group-orders
Authorization: Bearer {accessToken}
Content-Type: application/json

Request:
{
  "name": "Nhóm đặt trà sữa",
  "storeId": 1,
  "orderType": "DELIVERY",
  "deliveryAddress": "123 Đường ABC, TP.HCM",
  "maxMembers": 10
}

Response:
{
  "success": true,
  "message": "Tạo phiên đặt hàng nhóm thành công",
  "data": {
    "id": 1,
    "hostUserId": 1,
    "inviteCode": "ABC123XYZ",
    "name": "Nhóm đặt trà sữa",
    "status": "OPEN",
    "members": [ { "id": 1, "username": "user123", "isHost": true } ],
    "items": [],
    "expiresAt": "2024-01-15T14:00:00"
  }
}
```

### Join Group Order
```
POST /api/group-orders/join
Authorization: Bearer {accessToken}
Content-Type: application/json

Request:
{
  "inviteCode": "ABC123XYZ"
}

Response: { "success": true, "message": "Tham gia phiên thành công", "data": { ...group order... } }
```

### Get Group Order
```
GET /api/group-orders/{id}
Authorization: Bearer {accessToken}

Response: { "success": true, "data": { ...group order details... } }
```

### Get Group Order by Code
```
GET /api/group-orders/code/{inviteCode}
Authorization: Bearer {accessToken}

Response: { "success": true, "data": { ...group order details... } }
```

### Get Active Group Orders
```
GET /api/group-orders/active
Authorization: Bearer {accessToken}

Response: { "success": true, "data": [ ...active group orders... ] }
```

### Add Item to Group Order
```
POST /api/group-orders/{id}/items
Authorization: Bearer {accessToken}
Content-Type: application/json

Request:
{
  "drinkId": 1,
  "sizeName": "L",
  "quantity": 2,
  "unitPrice": 40000,
  "toppingIds": [1, 2],
  "note": "Ít đường"
}

Response: { "success": true, "message": "Thêm món thành công", "data": { ...updated group order... } }
```

### Update Item in Group Order
```
PUT /api/group-orders/{id}/items/{itemId}
Authorization: Bearer {accessToken}
Content-Type: application/json

Request: { ...updated item fields... }
Response: { "success": true, "message": "Cập nhật món thành công", "data": { ...updated group order... } }
```

### Remove Item from Group Order
```
DELETE /api/group-orders/{id}/items/{itemId}
Authorization: Bearer {accessToken}

Response: { "success": true, "message": "Xóa món thành công", "data": { ...updated group order... } }
```

### Lock Group Order
```
POST /api/group-orders/{id}/lock
Authorization: Bearer {accessToken}

Response: { "success": true, "message": "Đã khóa phiên", "data": { ...group order with status LOCKED... } }
```

### Unlock Group Order
```
POST /api/group-orders/{id}/unlock
Authorization: Bearer {accessToken}

Response: { "success": true, "message": "Đã mở khóa phiên", "data": { ...group order with status OPEN... } }
```

### Leave Group Order
```
POST /api/group-orders/{id}/leave
Authorization: Bearer {accessToken}

Response: { "success": true, "message": "Đã rời khỏi phiên", "data": { ...updated group order... } }
```

### Checkout Group Order
```
POST /api/group-orders/{id}/checkout
Authorization: Bearer {accessToken}
Content-Type: application/json

Request:
{
  "paymentMethod": "VNPAY",
  "promotionCode": "SAVE10"
}

Response:
{
  "success": true,
  "message": "Đặt hàng thành công",
  "data": {
    "id": 1,
    "userId": 1,
    "storeId": 1,
    "status": "PENDING",
    "finalPrice": 87000,
    "paymentMethod": "VNPAY"
  }
}
```

### Cancel Group Order
```
DELETE /api/group-orders/{id}
Authorization: Bearer {accessToken}

Response: { "success": true, "message": "Đã hủy phiên" }
```

---

## 9. NOTIFICATION APIs

### Get My Notifications
```
GET /api/notifications/my
Authorization: Bearer {accessToken}

Response:
{
  "success": true,
  "data": [
    {
      "id": 1,
      "title": "Cập nhật đơn hàng #1",
      "content": "Đơn hàng của bạn đang được pha chế.",
      "type": "ORDER_STATUS",
      "isRead": false,
      "relatedId": 1,
      "createdAt": "2024-01-15T10:00:00"
    }
  ]
}
```

### Get Unread Notifications
```
GET /api/notifications/unread
Authorization: Bearer {accessToken}

Response: { "success": true, "data": [ ...unread notifications... ] }
```

### Get Unread Count
```
GET /api/notifications/unread-count
Authorization: Bearer {accessToken}

Response:
{
  "success": true,
  "data": {
    "count": 5
  }
}
```

### Mark Notification as Read
```
PUT /api/notifications/{id}/read
Authorization: Bearer {accessToken}

Response: { "success": true, "data": { ...notification with isRead=true... } }
```

### Mark All as Read
```
PUT /api/notifications/read-all
Authorization: Bearer {accessToken}

Response:
{
  "success": true,
  "data": {
    "updated": 5
  }
}
```

### Delete Notification
```
DELETE /api/notifications/{id}
Authorization: Bearer {accessToken}

Response: { "success": true, "message": "Đã xóa thông báo" }
```

---

## 10. LOYALTY APIs

### Get User Points
```
GET /api/loyalty/points
Authorization: Bearer {accessToken}

Response:
{
  "success": true,
  "data": {
    "userId": 1,
    "totalPoints": 250,
    "memberTier": "SILVER",
    "pointsToNextTier": 250
  }
}
```

### Spin Wheel
```
POST /api/loyalty/spin
Authorization: Bearer {accessToken}

Response:
{
  "success": true,
  "message": "Trúng voucher giảm 20%!",
  "data": {
    "voucherCode": "SPIN20ABC",
    "discountPercent": 20,
    "pointsUsed": 5,
    "message": "Trúng voucher giảm 20%!"
  }
}
```

### Get Available Rewards
```
GET /api/loyalty/rewards
Authorization: Bearer {accessToken}

Response:
{
  "success": true,
  "data": [
    {
      "id": 1,
      "voucherCode": "SPIN20ABC",
      "discountPercent": 20,
      "isUsed": false
    }
  ]
}
```

### Validate Spin Voucher
```
GET /api/loyalty/voucher/validate?code=SPIN20ABC
Authorization: Bearer {accessToken}

Response:
{
  "success": true,
  "message": "Mã voucher hợp lệ, giảm 20%",
  "data": { ...voucher details... }
}
```

### Get Tier Benefits
```
GET /api/loyalty/tier/benefits
Authorization: Bearer {accessToken}

Response:
{
  "success": true,
  "data": {
    "currentTier": "SILVER",
    "benefits": {
      "freeShipMinOrder": 100000,
      "discountPercent": 5,
      "bonusPoints": 1.5
    },
    "nextTier": "GOLD",
    "pointsToNextTier": 250
  }
}
```

### Check Tier Upgrade
```
POST /api/loyalty/tier/check-upgrade
Authorization: Bearer {accessToken}

Response:
{
  "success": true,
  "message": "Đã kiểm tra và cập nhật hạng thành viên",
  "data": { ...updated tier benefits... }
}
```

### Preview Tier Discount
```
GET /api/loyalty/tier/preview-discount?orderTotal=150000
Authorization: Bearer {accessToken}

Response:
{
  "success": true,
  "data": {
    "orderTotal": 150000,
    "currentTier": "SILVER",
    "discountPercent": 5,
    "discountAmount": 7500,
    "finalPrice": 142500
  }
}
```

---

## 11. MANAGER APIs

### Get Dashboard Summary
```
GET /api/manager/summary
Authorization: Bearer {accessToken}
Role: MANAGER

Response:
{
  "success": true,
  "data": {
    "todayRevenue": 5000000,
    "todayOrders": 45,
    "activeOrders": 8,
    "totalUsers": 1250,
    "newUsersToday": 12
  }
}
```

### Get Revenue Statistics
```
GET /api/manager/statistics/revenue?days=7&months=6
Authorization: Bearer {accessToken}
Role: MANAGER

Response:
{
  "success": true,
  "data": {
    "dailyRevenue": [ ...7 days of data... ],
    "monthlyRevenue": [ ...6 months of data... ]
  }
}
```

### Get Full Forecast
```
GET /api/manager/forecast
Authorization: Bearer {accessToken}
Role: MANAGER

Response:
{
  "success": true,
  "data": {
    "revenueForecast": { ...forecast data... },
    "peakHours": [ ...peak hour analysis... ],
    "lowStockWarnings": [ ...low stock items... ],
    "staffingRecommendations": [ ...staffing suggestions... ],
    "overloadWarnings": [ ...overload alerts... ]
  }
}
```

### Get Revenue Forecast
```
GET /api/manager/forecast/revenue
Authorization: Bearer {accessToken}
Role: MANAGER

Response:
{
  "success": true,
  "data": {
    "todayForecast": 4500000,
    "tomorrowForecast": 4800000,
    "weekForecast": [ ...7 days... ],
    "monthForecast": [ ...30 days... ],
    "growthRate": 1.05,
    "trend": "GROWTH"
  }
}
```

### Get Peak Hours Analysis
```
GET /api/manager/forecast/peak-hours
Authorization: Bearer {accessToken}
Role: MANAGER

Response:
{
  "success": true,
  "data": [
    {
      "hour": 8,
      "averageOrders": 5,
      "averageRevenue": 200000,
      "peakLevel": "LOW",
      "recommendedStaff": 2
    },
    {
      "hour": 12,
      "averageOrders": 25,
      "averageRevenue": 1000000,
      "peakLevel": "HIGH",
      "recommendedStaff": 5
    }
  ]
}
```

### Get Low Stock Warnings
```
GET /api/manager/forecast/low-stock
Authorization: Bearer {accessToken}
Role: MANAGER

Response:
{
  "success": true,
  "data": [
    {
      "drinkId": 1,
      "drinkName": "Trà sữa Thái",
      "sellRate": 3.5,
      "alertLevel": "WARNING",
      "estimatedOutOfStockHours": 4
    }
  ]
}
```

### Get Staffing Recommendations
```
GET /api/manager/forecast/staffing
Authorization: Bearer {accessToken}
Role: MANAGER

Response:
{
  "success": true,
  "data": [
    {
      "date": "2024-01-15",
      "recommendedStaff": 8,
      "peakHours": "11:00-14:00, 17:00-19:00",
      "isWeekend": false
    }
  ]
}
```

### Get Overload Warnings
```
GET /api/manager/forecast/overload
Authorization: Bearer {accessToken}
Role: MANAGER

Response:
{
  "success": true,
  "data": [
    {
      "hour": 12,
      "expectedOrders": 55,
      "capacity": 50,
      "overloadPercent": 110,
      "alertLevel": "CRITICAL",
      "recommendation": "Tăng nhân viên + nguyên liệu"
    }
  ]
}
```

### Get Manager Orders
```
GET /api/manager/orders?status=PENDING&page=0&size=10
Authorization: Bearer {accessToken}
Role: MANAGER

Response:
{
  "success": true,
  "data": {
    "content": [ ...orders... ],
    "totalElements": 45,
    "totalPages": 5,
    "currentPage": 0
  }
}
```

### Update Order Status
```
PUT /api/manager/orders/{orderId}/status?status=MAKING
Authorization: Bearer {accessToken}
Role: MANAGER

Response: { "success": true, "data": { ...updated order... } }
```

### Get Manager Users
```
GET /api/manager/users?role=USER&page=0&size=10
Authorization: Bearer {accessToken}
Role: MANAGER

Response:
{
  "success": true,
  "data": {
    "content": [ ...users... ],
    "totalElements": 1250,
    "totalPages": 125,
    "currentPage": 0
  }
}
```

### Block/Unblock User
```
PUT /api/manager/users/{userId}/block?blocked=true
Authorization: Bearer {accessToken}
Role: MANAGER

Response: { "success": true, "data": { ...user with isBlocked=true... } }
```

### Promote User to Manager
```
PUT /api/manager/users/{userId}/promote
Authorization: Bearer {accessToken}
Role: MANAGER

Response: { "success": true, "data": { ...user with role=MANAGER... } }
```

### Assign Store to Manager
```
POST /api/manager/users/{userId}/stores/{storeId}
Authorization: Bearer {accessToken}
Role: MANAGER

Response: { "success": true, "data": { ...user with assigned store... } }
```

### Get My Managed Stores
```
GET /api/manager/my-stores
Authorization: Bearer {accessToken}
Role: MANAGER

Response:
{
  "success": true,
  "data": [
    {
      "id": 1,
      "storeName": "UTE Tea - TP.HCM",
      "address": "123 Đường ABC, TP.HCM",
      "phone": "0912345678"
    }
  ]
}
```

---

## 12. ADMIN APIs

### Create Drink
```
POST /api/admin/drinks
Authorization: Bearer {accessToken}
Role: ADMIN
Content-Type: application/json

Request:
{
  "name": "Cà phê đen",
  "description": "Cà phê đen nguyên chất",
  "basePrice": 25000,
  "categoryId": 2,
  "isActive": true
}

Response: { "success": true, "data": { ...created drink... } }
```

### Update Drink
```
PUT /api/admin/drinks/{id}
Authorization: Bearer {accessToken}
Role: ADMIN
Content-Type: application/json

Request: { ...updated fields... }
Response: { "success": true, "data": { ...updated drink... } }
```

### Delete Drink
```
DELETE /api/admin/drinks/{id}
Authorization: Bearer {accessToken}
Role: ADMIN

Response: { "success": true }
```

### Upload Drink Image
```
POST /api/admin/drinks/upload-image
Authorization: Bearer {accessToken}
Role: ADMIN
Content-Type: multipart/form-data

Request:
- file: [image file]
- drinkName: "Cà phê đen"

Response:
{
  "success": true,
  "data": {
    "imageUrl": "https://..."
  }
}
```

### Create Category
```
POST /api/admin/categories
Authorization: Bearer {accessToken}
Role: ADMIN
Content-Type: application/json

Request:
{
  "name": "Cà phê",
  "description": "Các loại cà phê",
  "displayOrder": 2
}

Response: { "success": true, "data": { ...created category... } }
```

### Update Category
```
PUT /api/admin/categories/{id}
Authorization: Bearer {accessToken}
Role: ADMIN
Content-Type: application/json

Request: { ...updated fields... }
Response: { "success": true, "data": { ...updated category... } }
```

### Delete Category
```
DELETE /api/admin/categories/{id}
Authorization: Bearer {accessToken}
Role: ADMIN

Response: { "success": true }
```

---

## 13. MONITORING APIs

### Get Monitoring Dashboard
```
GET /api/monitoring/dashboard
Authorization: Bearer {accessToken}
Role: ADMIN

Response:
{
  "success": true,
  "data": {
    "totalUsers": 1250,
    "activeUsers": 450,
    "suspiciousUsers": 12,
    "blockedUsers": 5,
    "totalAlerts": 45,
    "pendingAlerts": 8,
    "blockedIPs": 23
  }
}
```

### Get Activity Logs
```
GET /api/monitoring/activities?userId=1&activityType=LOGIN_SUCCESS&riskLevel=WARNING&page=0&size=20
Authorization: Bearer {accessToken}
Role: ADMIN

Response:
{
  "success": true,
  "data": {
    "content": [
      {
        "id": 1,
        "userId": 1,
        "activityType": "LOGIN_SUCCESS",
        "description": "Đăng nhập thành công",
        "riskLevel": "NORMAL",
        "ipAddress": "192.168.1.1",
        "endpoint": "/api/auth/login",
        "responseStatus": 200,
        "createdAt": "2024-01-15T10:00:00"
      }
    ],
    "totalElements": 100,
    "totalPages": 5,
    "currentPage": 0
  }
}
```

### Get Monitoring Alerts
```
GET /api/monitoring/alerts?severity=HIGH&status=PENDING&page=0&size=20
Authorization: Bearer {accessToken}
Role: ADMIN

Response:
{
  "success": true,
  "data": {
    "content": [
      {
        "id": 1,
        "userId": 1,
        "alertType": "BRUTE_FORCE",
        "severity": "HIGH",
        "title": "Phát hiện tấn công brute force",
        "message": "User 1 đã thử đăng nhập sai 5 lần trong 10 phút",
        "status": "PENDING",
        "createdAt": "2024-01-15T10:00:00"
      }
    ],
    "totalElements": 45,
    "totalPages": 3,
    "currentPage": 0
  }
}
```

### Handle Alert
```
PUT /api/monitoring/alerts/{alertId}/handle
Authorization: Bearer {accessToken}
Role: ADMIN
Content-Type: application/json

Request:
{
  "status": "RESOLVED",
  "actionTaken": "TEMP_BLOCKED",
  "handlerNote": "Tạm khóa tài khoản 24 giờ"
}

Response: { "success": true, "data": { ...updated alert... } }
```

### Get Risk Scores
```
GET /api/monitoring/risk-scores?riskLevel=SUSPICIOUS&page=0&size=20
Authorization: Bearer {accessToken}
Role: ADMIN

Response:
{
  "success": true,
  "data": {
    "content": [
      {
        "id": 1,
        "userId": 1,
        "totalScore": 65,
        "riskLevel": "SUSPICIOUS",
        "loginFailedCount": 3,
        "orderCancelCount": 5,
        "paymentFailedCount": 2,
        "autoBlocked": false
      }
    ],
    "totalElements": 12,
    "totalPages": 1,
    "currentPage": 0
  }
}
```

### Get User Risk Score
```
GET /api/monitoring/risk-scores/user/{userId}
Authorization: Bearer {accessToken}
Role: ADMIN

Response:
{
  "success": true,
  "data": {
    "id": 1,
    "userId": 1,
    "totalScore": 65,
    "riskLevel": "SUSPICIOUS",
    "adminNote": "Hành vi đáng ngờ",
    "autoBlocked": false
  }
}
```

### Add Admin Note
```
POST /api/monitoring/risk-scores/user/{userId}/note
Authorization: Bearer {accessToken}
Role: ADMIN
Content-Type: application/json

Request:
{
  "note": "Hành vi đáng ngờ, cần theo dõi"
}

Response: { "success": true, "data": { ...updated risk score... } }
```

### Reset Risk Score
```
POST /api/monitoring/risk-scores/user/{userId}/reset
Authorization: Bearer {accessToken}
Role: ADMIN

Response: { "success": true, "data": { ...reset risk score... } }
```

### Unblock User
```
POST /api/monitoring/users/{userId}/unblock
Authorization: Bearer {accessToken}
Role: ADMIN
Content-Type: application/json

Request:
{
  "reason": "Xác nhận không phải hành vi độc hại"
}

Response: { "success": true, "message": "Đã mở khóa tài khoản" }
```

---

## 14. BLOCKED IP MANAGEMENT

### Block IP
```
POST /api/blocked-ips/block
Authorization: Bearer {accessToken}
Role: ADMIN
Content-Type: application/json

Request:
{
  "ipAddress": "192.168.1.100",
  "blockType": "TEMPORARY",
  "reason": "Tấn công brute force",
  "blockedUntil": "2024-01-16T10:00:00"
}

Response: { "success": true, "data": { ...blocked IP... } }
```

### Unblock IP
```
POST /api/blocked-ips/{id}/unblock
Authorization: Bearer {accessToken}
Role: ADMIN
Content-Type: application/json

Request:
{
  "reason": "Xác nhận không phải tấn công"
}

Response: { "success": true, "data": { ...unblocked IP... } }
```

### Get Active Blocked IPs
```
GET /api/blocked-ips?page=0&size=20
Authorization: Bearer {accessToken}
Role: ADMIN

Response:
{
  "success": true,
  "data": {
    "content": [ ...blocked IPs... ],
    "totalElements": 23,
    "totalPages": 2,
    "currentPage": 0
  }
}
```

### Check IP Status
```
GET /api/blocked-ips/check?ip=192.168.1.100
Authorization: Bearer {accessToken}
Role: ADMIN

Response:
{
  "success": true,
  "data": {
    "isBlocked": true,
    "blockType": "TEMPORARY",
    "reason": "Tấn công brute force",
    "blockedUntil": "2024-01-16T10:00:00"
  }
}
```

---

## 14.1 WHITELIST IP MANAGEMENT

### Add IP to Whitelist
```
POST /api/whitelist-ips/add
Authorization: Bearer {accessToken}
Role: ADMIN
Content-Type: application/json

Request:
{
  "ipAddress": "123.21.109.117",
  "description": "IP văn phòng chính"
}

Response:
{
  "success": true,
  "message": "Đã thêm IP vào whitelist",
  "data": {
    "id": 1,
    "ipAddress": "123.21.109.117",
    "description": "IP văn phòng chính",
    "addedById": 1,
    "isActive": true,
    "createdAt": "2024-01-15T10:00:00",
    "updatedAt": "2024-01-15T10:00:00"
  }
}
```

### Remove IP from Whitelist
```
POST /api/whitelist-ips/{id}/remove
Authorization: Bearer {accessToken}
Role: ADMIN

Response:
{
  "success": true,
  "message": "Đã xóa IP khỏi whitelist"
}
```

### Get Active Whitelist IPs
```
GET /api/whitelist-ips
Authorization: Bearer {accessToken}
Role: ADMIN

Response:
{
  "success": true,
  "data": [
    {
      "id": 1,
      "ipAddress": "123.21.109.117",
      "description": "IP văn phòng chính",
      "addedById": 1,
      "isActive": true,
      "createdAt": "2024-01-15T10:00:00",
      "updatedAt": "2024-01-15T10:00:00"
    },
    {
      "id": 2,
      "ipAddress": "192.168.1.50",
      "description": "IP nhà quản lý",
      "addedById": 1,
      "isActive": true,
      "createdAt": "2024-01-14T08:00:00",
      "updatedAt": "2024-01-14T08:00:00"
    }
  ]
}
```

### Get All Whitelist IPs (Paginated)
```
GET /api/whitelist-ips/all?page=0&size=20
Authorization: Bearer {accessToken}
Role: ADMIN

Response:
{
  "success": true,
  "data": {
    "content": [ ...whitelist IPs... ],
    "totalElements": 10,
    "totalPages": 1,
    "currentPage": 0
  }
}
```

### Check IP Whitelist Status
```
GET /api/whitelist-ips/check?ip=123.21.109.117
Authorization: Bearer {accessToken}
Role: ADMIN

Response:
{
  "success": true,
  "data": {
    "isWhitelisted": true,
    "ipAddress": "123.21.109.117",
    "description": "IP văn phòng chính"
  }
}
```

### Get My Current IP
```
GET /api/auth/my-ip
Authorization: Bearer {accessToken}

Response:
{
  "success": true,
  "data": {
    "yourIP": "123.21.109.117"
  }
}
```

### Whitelist Configuration
```
# application.properties

# Bật/tắt kiểm tra whitelist IP cho Admin/Manager
# Khi bật: Admin/Manager chỉ truy cập được từ IP trong whitelist (database)
# User thường KHÔNG bị ảnh hưởng
whitelist.check.enabled=${WHITELIST_CHECK_ENABLED:true}
```

---

## 15. SHIPPING APIs

### Get GHN Provinces
```
GET /api/ghn/provinces
Response:
{
  "success": true,
  "data": [
    { "id": 1, "name": "TP. Hồ Chí Minh" },
    { "id": 2, "name": "Hà Nội" }
  ]
}
```

### Get GHN Districts
```
GET /api/ghn/districts/{provinceId}
Response:
{
  "success": true,
  "data": [
    { "id": 1, "name": "Quận 1" },
    { "id": 2, "name": "Quận 2" }
  ]
}
```

### Get GHN Wards
```
GET /api/ghn/wards/{districtId}
Response:
{
  "success": true,
  "data": [
    { "id": 1, "name": "Phường 1" },
    { "id": 2, "name": "Phường 2" }
  ]
}
```

### Calculate Shipping Fee
```
POST /api/ghn/calculate-fee/simple
Content-Type: application/json

Request:
{
  "toDistrictId": 1,
  "toWardCode": "100001",
  "weight": 500
}

Response:
{
  "success": true,
  "data": {
    "fee": 15000,
    "estimatedDeliveryTime": "2024-01-15T18:00:00"
  }
}
```

### Get Shipping Fee
```
GET /api/ghn/shipping-fee?toDistrictId=1&toWardCode=100001
Response:
{
  "success": true,
  "data": 15000
}
```

---

## 16. CHALLENGE APIs

### Get Challenge Status (User)
```
GET /api/challenges/status
Authorization: Bearer {accessToken}
Role: USER, MANAGER, ADMIN

Response:
{
  "success": true,
  "data": {
    "activeChallenges": [
      {
        "id": 1,
        "name": "Mua 3 sản phẩm giống nhau",
        "description": "Mua 3 sản phẩm giống nhau trong 1 đơn hàng để nhận 5 điểm thưởng",
        "challengeType": "SAME_PRODUCT_IN_ORDER",
        "requiredQuantity": 3,
        "rewardPoints": 5,
        "isActive": true
      }
    ],
    "completionHistory": [
      {
        "id": 1,
        "challengeId": 1,
        "challengeName": "Mua 3 sản phẩm giống nhau",
        "orderId": 123,
        "pointsEarned": 5,
        "drinkName": "Trà sữa Thái",
        "quantityAchieved": 3,
        "completedAt": "2024-01-15T10:00:00"
      }
    ],
    "totalPointsFromChallenges": 15
  }
}
```

### Get All Challenges (Manager/Admin)
```
GET /api/challenges
Authorization: Bearer {accessToken}
Role: MANAGER, ADMIN

Response:
{
  "success": true,
  "data": [
    {
      "id": 1,
      "name": "Mua 3 sản phẩm giống nhau",
      "description": "Mua 3 sản phẩm giống nhau trong 1 đơn hàng để nhận 5 điểm thưởng",
      "challengeType": "SAME_PRODUCT_IN_ORDER",
      "requiredQuantity": 3,
      "rewardPoints": 5,
      "isActive": true
    }
  ]
}
```

### Get Challenge by ID (Manager/Admin)
```
GET /api/challenges/{id}
Authorization: Bearer {accessToken}
Role: MANAGER, ADMIN

Response:
{
  "success": true,
  "data": {
    "id": 1,
    "name": "Mua 3 sản phẩm giống nhau",
    "description": "Mua 3 sản phẩm giống nhau trong 1 đơn hàng để nhận 5 điểm thưởng",
    "challengeType": "SAME_PRODUCT_IN_ORDER",
    "requiredQuantity": 3,
    "rewardPoints": 5,
    "isActive": true
  }
}
```

### Create Challenge (Manager/Admin)
```
POST /api/challenges
Authorization: Bearer {accessToken}
Role: MANAGER, ADMIN
Content-Type: application/json

Request:
{
  "name": "Mua 5 sản phẩm giống nhau",
  "description": "Mua 5 sản phẩm giống nhau trong 1 đơn hàng để nhận 10 điểm thưởng",
  "challengeType": "SAME_PRODUCT_IN_ORDER",
  "requiredQuantity": 5,
  "rewardPoints": 10,
  "isActive": true
}

Response:
{
  "success": true,
  "message": "Tạo challenge thành công",
  "data": { ...created challenge... }
}
```

### Update Challenge (Manager/Admin)
```
PUT /api/challenges/{id}
Authorization: Bearer {accessToken}
Role: MANAGER, ADMIN
Content-Type: application/json

Request:
{
  "name": "Mua 3 sản phẩm giống nhau - Updated",
  "rewardPoints": 8
}

Response:
{
  "success": true,
  "message": "Cập nhật challenge thành công",
  "data": { ...updated challenge... }
}
```

### Delete Challenge (Manager/Admin)
```
DELETE /api/challenges/{id}
Authorization: Bearer {accessToken}
Role: MANAGER, ADMIN

Response:
{
  "success": true,
  "message": "Xóa challenge thành công"
}
```

### Toggle Challenge Status (Manager/Admin)
```
PATCH /api/challenges/{id}/toggle-status
Authorization: Bearer {accessToken}
Role: MANAGER, ADMIN

Response:
{
  "success": true,
  "message": "Đã kích hoạt challenge",
  "data": { ...challenge with toggled status... }
}
```

---

## 17. BANNER APIs

### Get Active Banners (Public)
```
GET /api/banners

Response:
{
  "success": true,
  "data": [
    {
      "id": 1,
      "title": "Khuyến mãi mùa hè",
      "description": "Giảm 20% tất cả đồ uống",
      "imageUrl": "https://...",
      "actionUrl": "utetea://promotion/summer2024",
      "bannerType": "PROMOTION",
      "displayOrder": 1,
      "startDate": "2024-06-01T00:00:00",
      "endDate": "2024-08-31T23:59:59",
      "isActive": true
    }
  ]
}
```

### Get Banners by Type (Public)
```
GET /api/banners/type/{type}
Types: PROMOTION, ANNOUNCEMENT, EVENT, NEW_PRODUCT

Response:
{
  "success": true,
  "data": [ ...banners of specified type... ]
}
```

### Get All Banners (Manager/Admin)
```
GET /api/banners/manage
Authorization: Bearer {accessToken}
Role: MANAGER, ADMIN

Response:
{
  "success": true,
  "data": [
    {
      "id": 1,
      "title": "Khuyến mãi mùa hè",
      "description": "Giảm 20% tất cả đồ uống",
      "imageUrl": "https://...",
      "actionUrl": "utetea://promotion/summer2024",
      "bannerType": "PROMOTION",
      "displayOrder": 1,
      "startDate": "2024-06-01T00:00:00",
      "endDate": "2024-08-31T23:59:59",
      "isActive": true,
      "createdAt": "2024-05-15T10:00:00",
      "updatedAt": "2024-05-15T10:00:00"
    }
  ]
}
```

### Get Banner by ID (Manager/Admin)
```
GET /api/banners/manage/{id}
Authorization: Bearer {accessToken}
Role: MANAGER, ADMIN

Response:
{
  "success": true,
  "data": { ...banner details... }
}
```

### Create Banner (Manager/Admin)
```
POST /api/banners/manage
Authorization: Bearer {accessToken}
Role: MANAGER, ADMIN
Content-Type: application/json

Request:
{
  "title": "Sản phẩm mới",
  "description": "Trà sữa Matcha đã có mặt!",
  "imageUrl": "https://...",
  "actionUrl": "utetea://drink/123",
  "bannerType": "NEW_PRODUCT",
  "displayOrder": 1,
  "startDate": "2024-01-15T00:00:00",
  "endDate": "2024-02-15T23:59:59",
  "isActive": true
}

Response:
{
  "success": true,
  "message": "Tạo banner thành công",
  "data": { ...created banner... }
}
```

### Update Banner (Manager/Admin)
```
PUT /api/banners/manage/{id}
Authorization: Bearer {accessToken}
Role: MANAGER, ADMIN
Content-Type: application/json

Request:
{
  "title": "Sản phẩm mới - Updated",
  "displayOrder": 2
}

Response:
{
  "success": true,
  "message": "Cập nhật banner thành công",
  "data": { ...updated banner... }
}
```

### Delete Banner (Manager/Admin)
```
DELETE /api/banners/manage/{id}
Authorization: Bearer {accessToken}
Role: MANAGER, ADMIN

Response:
{
  "success": true,
  "message": "Xóa banner thành công"
}
```

### Toggle Banner Status (Manager/Admin)
```
PATCH /api/banners/manage/{id}/toggle-status
Authorization: Bearer {accessToken}
Role: MANAGER, ADMIN

Response:
{
  "success": true,
  "message": "Đã kích hoạt banner",
  "data": { ...banner with toggled status... }
}
```

---

## 📊 RESPONSE FORMAT

### Success Response
```json
{
  "success": true,
  "message": "Operation successful",
  "data": { ...response data... }
}
```

### Error Response
```json
{
  "success": false,
  "message": "Error message",
  "data": null
}
```

### Pagination Response
```json
{
  "success": true,
  "data": {
    "content": [ ...items... ],
    "totalElements": 100,
    "totalPages": 10,
    "currentPage": 0,
    "pageSize": 10
  }
}
```

---

## 🔐 AUTHENTICATION

Tất cả API (trừ auth, public endpoints) yêu cầu JWT token trong header:

```
Authorization: Bearer {accessToken}
```

Token được lấy từ login response và có thể refresh bằng refresh token.

---

## 📝 NOTES

- Base URL: `http://localhost:8080/api` (development) hoặc `https://api.utetea.com/api` (production)
- Tất cả request/response sử dụng JSON
- Timestamp format: ISO 8601 (2024-01-15T10:00:00)
- Currency: VND (Vietnamese Dong)
- Pagination: page (0-indexed), size (default 10)