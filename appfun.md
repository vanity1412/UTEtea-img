# 📱 ANDROID APP FUNCTIONS - UTE TEA SYSTEM

## 🏗️ KIẾN TRÚC TỔNG QUAN

Ứng dụng Android được xây dựng theo mô hình **MVVM** với kiến trúc phân lớp:
- **Activities/Fragments**: UI Layer - Giao diện người dùng
- **res(layout)**: XML layouts - Thiết kế giao diện
- **Network**: API Layer - Kết nối với backend
- **Models**: Data Layer - Cấu trúc dữ liệu
- **Adapters**: RecyclerView Adapters - Hiển thị danh sách

---

## 📱 1. ACTIVITIES & FRAGMENTS LAYER

### 🏠 MainActivity
**Chức năng chính:**
- Container chính cho Bottom Navigation với 4 tabs
- Quản lý Fragment lifecycle và navigation
- Preload dữ liệu (categories, products, stores) vào cache
- Xử lý token expired broadcast và auto logout
- Phân quyền: Chuyển Manager/Admin sang ManagerActivity
- Predictive Order: Kiểm tra và hiển thị gợi ý món dự đoán
- Cart badge: Hiển thị số lượng sản phẩm trong giỏ

**Tính năng đặc biệt:**
- Fragment caching để tối ưu performance
- Auto-redirect dựa trên role (USER/MANAGER/ADMIN)
- Deep linking support cho notifications

### 🔐 LoginActivity
**Chức năng chính:**
- Đăng nhập với username/phone + password
- Biometric login (vân tay) với encrypted token storage
- Auto-refresh token khi hết hạn
- OneSignal integration cho push notifications
- Session management với encrypted SharedPreferences

**Tính năng bảo mật:**
- KeyStore encryption cho biometric data
- JWT token auto-refresh mechanism
- Secure token storage với EncryptedSharedPreferences

### 🛒 CartActivity
**Chức năng chính:**
- Hiển thị giỏ hàng với select/unselect items
- Áp dụng voucher (promotion + spin wheel vouchers)
- Tính toán discount theo member tier (Bronze/Silver/Gold/Diamond)
- Chọn loại đơn hàng (PICKUP/DELIVERY)
- OTP verification trước khi đặt hàng
- Multiple payment methods (COD/VNPAY/VIETQR)

**Tính năng đặc biệt:**
- Combined voucher system (normal + spin rewards)
- Real-time voucher validation
- Tier-based discount calculation
- Rate limiting cho OTP requests
- Confetti celebration khi đặt hàng thành công

### 📦 ProductDetailActivity
**Chức năng chính:**
- Hiển thị chi tiết sản phẩm với sizes và toppings
- Tính toán giá real-time khi chọn options
- Add to cart với animation effects
- Review system với rating summary
- Voice order integration

**Tính năng UI/UX:**
- Seasonal effects và animations
- Smart image loading với Glide
- Dynamic price calculation
- Review display với pagination

### 🏠 HomeFragment
**Chức năng chính:**
- Banner carousel với auto-scroll và indicators
- Best seller và "For You" product carousels
- Quick actions: Voice Order, Chatbot, Spin Wheel, Group Order
- Smart suggestion card (Predictive Order)
- Weather integration
- Seasonal effects (snow, sakura, hearts, etc.)

**Tính năng độc đáo:**
- **Voice Order**: Đặt hàng bằng giọng nói với speech recognition
- **Predictive Order**: AI gợi ý món dựa trên lịch sử và thời tiết
- **Seasonal Effects**: Hiệu ứng theo mùa (tuyết rơi, hoa đào, lá vàng)
- **Draggable Quick Actions**: Card có thể kéo thả
- **Weather Card**: Hiển thị thời tiết real-time

### 🍽️ MenuFragment
**Chức năng chính:**
- Hiển thị toàn bộ thực đơn với grid layout
- Category filter với horizontal scroll
- Search với voice search support
- Price sorting (ascending/descending)
- Real-time search suggestions

**Tính năng tìm kiếm:**
- Text search với Vietnamese accent removal
- Voice search với speech recognition
- Smart suggestions với fuzzy matching
- Category-based filtering

### 📋 OrderFragment
**Chức năng chính:**
- Lịch sử đơn hàng với smart sorting
- Pagination với load more
- Order statistics (total, pending, completed)
- Status-based filtering và display

**Smart Sorting Logic:**
- Đơn đang xử lý: Sắp xếp theo thời gian đặt (cũ → mới)
- Đơn hoàn thành: Sắp xếp theo thời gian (mới → cũ)

### 👤 AccountFragment
**Chức năng chính:**
- User profile management
- Avatar upload với image compression
- Navigation đến các settings
- Account deletion với confirmation
- Logout với session cleanup

---

## 🎨 2. RES(LAYOUT) LAYER

### 📐 Layout Structure
**Activity Layouts (45+ files):**
- `activity_main.xml` - Bottom navigation container
- `activity_login.xml` - Login form với biometric option
- `activity_cart.xml` - Shopping cart với voucher section
- `activity_product_detail_new.xml` - Product detail với reviews
- `activity_user_monitoring.xml` - Admin monitoring dashboard

**Fragment Layouts:**
- `fragment_home.xml` - Home với banners và quick actions
- `fragment_menu.xml` - Menu grid với search và filters
- `fragment_order.xml` - Order history với stats
- `fragment_account.xml` - Profile management

**Item Layouts (50+ files):**
- `item_product_card.xml` - Product card cho grid
- `item_cart.xml` - Cart item với select checkbox
- `item_order.xml` - Order item với status chip
- `item_category.xml` - Category với image và selection state

**Dialog Layouts:**
- `dialog_voice_order.xml` - Voice order interface
- `dialog_spin_result.xml` - Spin wheel result
- `dialog_group_order_options.xml` - Group order options
- `dialog_voucher_selection.xml` - Voucher selection

### 🎨 Design System
**Colors:**
- Wine theme với primary, secondary, accent colors
- Status colors cho order states
- Tier colors cho member levels
- Seasonal colors cho effects

**Animations (30+ files):**
- `slide_in_right.xml`, `fade_in.xml` - Transition animations
- `bounce_in.xml`, `scale_up.xml` - Button animations
- `layout_animation_fall_down.xml` - List animations
- `pulse_animation.xml` - Loading animations

**Drawables (100+ files):**
- Background gradients và shapes
- Status indicators và badges
- Seasonal effect backgrounds
- Icon sets cho features

---

## 🌐 3. NETWORK LAYER

### 🔗 RetrofitClient
**Chức năng chính:**
- Singleton pattern cho API client
- OkHttp configuration với timeouts
- Logging interceptor (chỉ debug mode)
- AuthInterceptor integration
- Gson converter với custom deserializers

**Configuration:**
- Base URL switching (development/production)
- SSL certificate handling
- Request/response logging
- Error handling và retry logic

### 🛡️ AuthInterceptor
**Chức năng chính:**
- Auto-attach JWT token vào headers
- Token expiry detection (401 handling)
- Auto token refresh mechanism
- Session cleanup khi refresh fail
- Broadcast token expired events

**Security Features:**
- EncryptedSharedPreferences cho token storage
- Synchronous token refresh
- Automatic logout khi token invalid
- Debug logging chỉ trong development

### 📡 ApiService Interface
**100+ API Endpoints:**

#### Authentication APIs
- `login()`, `register()`, `refreshToken()`
- `registerWithOtp()`, `verifyOtp()`, `resendOtp()`
- `forgotPassword()`, `resetPassword()`

#### Product & Category APIs
- `getDrinks()`, `getDrinkById()`, `searchDrinks()`
- `getCategories()`, `getCategoryById()`

#### Order Management APIs
- `createOrder()`, `getUserOrders()`, `getOrderById()`
- `updateOrderStatus()`, `cancelOrder()`

#### Cart APIs
- `addToCart()`, `getCart()`, `updateCartItem()`
- `removeCartItem()`, `clearCart()`

#### Promotion APIs
- `getActivePromotions()`, `validatePromotion()`
- `createPromotion()`, `updatePromotion()`

#### Loyalty APIs
- `getUserPoints()`, `spinWheel()`, `getAvailableRewards()`
- `getTierBenefits()`, `previewTierDiscount()`

#### Group Order APIs
- `createGroupOrder()`, `joinGroupOrder()`, `getActiveGroupOrders()`
- `addGroupOrderItem()`, `checkoutGroupOrder()`

#### Live Chat APIs
- `startLiveConversation()`, `sendLiveMessage()`
- `getMyConversations()`, `closeConversation()`

#### Monitoring APIs (Admin)
- `getMonitoringDashboard()`, `getActivityLogs()`
- `getMonitoringAlerts()`, `getRiskScores()`

### 🔌 WebSocket Managers
**Real-time Communication:**
- `OrderWebSocketManager` - Order status updates
- `LiveChatWebSocketManager` - Live chat messages
- `GroupChatWebSocketManager` - Group order chat
- `MonitoringWebSocketManager` - Admin monitoring alerts

---

## 📊 4. MODELS LAYER

### 🏗️ Core Data Models

#### 👤 User Models
```kotlin
User - Thông tin user cơ bản
UserProfileDto - Profile chi tiết với avatar
LoginRequest/LoginResponse - Authentication
RegisterRequest - Đăng ký tài khoản
```

#### 🛒 Order Models
```kotlin
Order - Đơn hàng với Parcelable support
OrderItem - Chi tiết sản phẩm trong đơn
CreateOrderRequest - Tạo đơn hàng
OrderStatus enum - Trạng thái đơn hàng
```

#### 🥤 Product Models
```kotlin
Drink - Sản phẩm với sizes và toppings
DrinkSize - Kích thước với extra price
DrinkTopping - Topping với giá
Category - Danh mục sản phẩm
```

#### 🛍️ Cart Models
```kotlin
Cart - Giỏ hàng với items
CartItem - Item trong giỏ với selection state
AddToCartRequest - Thêm vào giỏ
```

#### 🎁 Promotion Models
```kotlin
Voucher - Voucher thường
SpinRewardDto - Voucher từ vòng quay
TierDiscountPreview - Preview discount theo tier
```

#### 👥 Group Order Models
```kotlin
GroupOrderDto - Phiên đặt hàng nhóm
GroupOrderMemberDto - Thành viên trong phiên
GroupChatMessageDto - Tin nhắn chat nhóm
```

#### 🛡️ Monitoring Models
```kotlin
MonitoringAlert - Cảnh báo hệ thống
UserActivityLog - Log hoạt động user
UserRiskScore - Điểm rủi ro user
MonitoringDashboard - Dashboard tổng quan
```

### 🔄 Response Wrappers
```kotlin
ApiResponse<T> - Wrapper cho tất cả API responses
PageResponse<T> - Pagination support
```

---

## 🎨 5. ADAPTERS LAYER

### 📋 RecyclerView Adapters

#### 🛍️ ProductAdapter
**Chức năng:**
- Hiển thị products trong grid layout
- Click navigation đến ProductDetailActivity
- Image loading với Glide và placeholder
- Price formatting với Vietnamese locale

#### 🛒 CartAdapter
**Chức năng:**
- Cart items với checkbox selection
- Quantity display và item details
- Delete item functionality
- Selection state management
- Price calculation per item

**Interface:**
```kotlin
OnCartItemChangeListener {
    onItemSelectedChanged()
    onItemDeleted(item: CartItem)
}
```

#### 📦 OrderAdapter
**Chức năng:**
- Order history với status chips
- Color-coded status indicators
- Date formatting và currency display
- Click navigation đến OrderDetailActivity

**Status Colors:**
- PENDING: Orange
- MAKING: Blue
- SHIPPING: Purple
- DONE: Green
- CANCELED: Red

#### 🏷️ CategoryAdapter
**Chức năng:**
- Horizontal category scroll
- Selection state với visual feedback
- Image loading cho category icons
- Click handling với callback interface

#### 🎠 ProductCarouselAdapter
**Chức năng:**
- Horizontal product scroll cho Home
- Carousel effect với scaling animation
- Snap-to-center behavior
- Product click navigation

#### 💬 Specialized Adapters
- **ChatAdapter** - Live chat messages
- **GroupChatAdapter** - Group order chat
- **NotificationAdapter** - Push notifications
- **ReviewAdapter** - Product reviews
- **VoucherSelectionAdapter** - Voucher picker
- **MonitoringAlertAdapter** - Admin alerts

---

## 🚀 6. TÍNH NĂNG ĐỘC ĐÁO

### 🎤 Voice Order System
**Chức năng:**
- Speech-to-text cho đặt hàng bằng giọng nói
- Natural language processing cho tên món
- Voice search trong menu
- Microphone permission handling
- Real-time voice feedback

**Implementation:**
- Android SpeechRecognizer API
- Custom VoiceOrderDialog
- VoiceSearchHelper utility
- Permission management

### 🔮 Predictive Order (AI Gợi Ý)
**Chức năng:**
- AI prediction dựa trên lịch sử đặt hàng
- Weather-based recommendations
- Time-based suggestions
- Smart suggestion card trên Home
- One-click add to cart

**Logic:**
- Phân tích pattern đặt hàng của user
- Kết hợp với thời tiết hiện tại
- Tính toán confidence score
- Hiển thị với lý do gợi ý

### 👥 Group Order System
**Chức năng:**
- Tạo phiên đặt hàng nhóm với invite code
- Real-time collaboration với WebSocket
- Group chat integration
- Host controls (lock/unlock, checkout)
- Member management

**Workflow:**
1. Host tạo phiên → Generate invite code
2. Members join bằng code
3. Collaborative ordering với chat
4. Host checkout cho toàn bộ nhóm

### 🎡 Spin Wheel & Loyalty System
**Chức năng:**
- Vòng quay may mắn với animation
- 4-tier membership system (Bronze/Silver/Gold/Diamond)
- Points accumulation và tier benefits
- Spin rewards với voucher codes
- Tier-based discount calculation

**Member Tiers:**
- **Bronze**: 1x points, 0% discount
- **Silver**: 1.2x points, 2% discount  
- **Gold**: 1.5x points, 5% discount
- **Diamond**: 2x points, 10% discount

### 🌸 Seasonal Effects System
**Chức năng:**
- Dynamic seasonal animations
- Weather-based effects
- Holiday themes (Christmas, Tet, Valentine)
- Customizable effect settings
- Performance-optimized animations

**Effects:**
- ❄️ Winter: Snowfall animation
- 🌸 Spring/Tet: Sakura petals
- ☀️ Summer: Sunshine bubbles
- 🍂 Autumn: Falling leaves
- 💕 Valentine: Flying hearts

### 🛡️ User Monitoring System (Admin)
**Chức năng:**
- Real-time user behavior tracking
- Risk score calculation
- Automated alert system
- Activity logging
- IP blocking management

**Monitoring Features:**
- Login/logout tracking
- Order pattern analysis
- Suspicious activity detection
- Rate limiting violations
- Automated risk scoring

### 💳 Multi-Payment Integration
**Chức năng:**
- COD (Cash on Delivery)
- VNPay online payment
- VietQR payment
- Payment status tracking
- Refund handling

---

## 🔧 7. UTILITY CLASSES

### 🎨 Animation & Effects
- **AnimationHelper** - Common animations
- **SeasonalEffectManager** - Seasonal effects
- **AddToCartAnimator** - Cart animation
- **ConfettiView** - Success celebrations

### 🔒 Security & Session
- **SessionManager** - User session với encryption
- **SecurityChecker** - Security validations
- **KeyStoreManager** - Biometric data encryption

### 📱 UI Utilities
- **LoadingDialog** - Loading states
- **InAppNotification** - Toast alternatives
- **HapticFeedbackHelper** - Vibration feedback
- **DraggableViewHelper** - Drag & drop support

### 🌐 Network Utilities
- **DataCache** - In-memory caching
- **LocationHelper** - GPS location
- **WeatherHelper** - Weather integration

### 🎯 Specialized Utilities
- **PredictiveOrderHelper** - AI suggestions
- **VoiceOrderHelper** - Voice commands
- **CartManager** - Cart state management

---

## 📊 8. PERFORMANCE OPTIMIZATIONS

### 🚀 Memory Management
- Fragment caching trong MainActivity
- Image loading với Glide caching
- RecyclerView view recycling
- Proper lifecycle management

### 🌐 Network Optimization
- API response caching
- Batch API calls
- Request deduplication
- Offline support với cached data

### 🎨 UI Performance
- ViewHolder pattern trong adapters
- Layout optimization
- Animation performance tuning
- Lazy loading cho large lists

---

## 🔐 9. SECURITY FEATURES

### 🛡️ Data Protection
- EncryptedSharedPreferences cho sensitive data
- Biometric authentication
- JWT token auto-refresh
- Secure API communication

### 🚫 Abuse Prevention
- Rate limiting cho API calls
- Input validation và sanitization
- SQL injection prevention
- XSS protection

### 📱 App Security
- Certificate pinning
- Root detection
- Debug detection
- Tamper protection

---

## 🎯 10. USER EXPERIENCE FEATURES

### 🎨 Modern UI/UX
- Material Design 3 components
- Dark/Light theme support
- Smooth animations và transitions
- Responsive design

### ♿ Accessibility
- Content descriptions
- Screen reader support
- High contrast support
- Large text support

### 🌍 Localization
- Vietnamese language support
- Currency formatting
- Date/time localization
- Cultural adaptations

---

## 📈 11. ANALYTICS & MONITORING

### 📊 User Analytics
- Screen view tracking
- User interaction events
- Conversion funnel analysis
- Performance metrics

### 🐛 Error Tracking
- Crash reporting
- Error logging
- Performance monitoring
- User feedback collection

---

Ứng dụng Android UTE Tea được thiết kế với kiến trúc hiện đại, tối ưu performance và trải nghiệm người dùng tuyệt vời, tích hợp nhiều tính năng độc đáo như Voice Order, AI Prediction, Group Order và Seasonal Effects.