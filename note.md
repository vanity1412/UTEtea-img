TRƯỜNG ĐẠI HỌC SƯ PHẠM KỸ THUẬT THÀNH PHỐ HỒ CHÍ MINH
KHOA CÔNG NGHỆ THÔNG TIN







BÁO CÁO CHỨC NĂNG ĐỒ ÁN
LẬP TRÌNH DI ĐỘNG
Đề tài
XÂY DỰNG ỨNG DỤNG ĐẶT TRÀ SỮA 

Giảng viên: Nguyễn Hữu Trung
Mã môn học: MOPR331279
Thực hiện: Nhóm 3
Thành viên nhóm:	23162001 – Nguyễn Thành An
23162098 – Vũ Văn Thông
23162111 – Huỳnh Thanh Tú
23110231 – Xín Lợi Huy


Tháng 01, Năm 2026, TP. HCM











BÁO CÁO CHỨC NĂNG HỆ THỐNG UTE TEA
Android App (Kotlin, MVVM) + Backend API (Spring Boot, MVC)

Nhóm thực hiện: Nhóm 3 

 
BẢNG PHÂN CÔNG NHIỆM VỤ
Thành viên	Module phụ trách	Chức năng đảm nhiệm trong báo cáo
NGUYỄN THÀNH AN	UI/UX Android & Trải nghiệm người dùng 
• Thiết kế giao diện Android (layout, component) 
• RecyclerView, ViewPager2
 • Animation, Lottie
 • Seasonal Effects	•	Trang chủ (Banner, Best Seller, For You, Quick Actions, Weather, Seasonal Effects) 
•	Voice Order & Voice Search (UI/UX) 
•	Loyalty, hạng thành viên, Spin Wheel (UI) 
•	Thực đơn, hiển thị sản phẩm theo danh mục 
•	Tìm kiếm nâng cao (UI search, gợi ý realtime) 
•	Giao diện chi tiết sản phẩm (size, topping, animation add-to-cart, review)
XÍN LỢI HUY	User Account – Authentication – Security 
• Login / Register / OTP
 • Forgot / Reset Password
 • Profile người dung
 • Biometric Login • JWT, Session, Token	•	Đăng nhập (JWT, Biometric, Auto Refresh Token) 
•	Đăng ký tài khoản & OTP Verify / Resend 
•	Quên mật khẩu & xác thực OTP 
•	Quản lý hồ sơ người dùng (profile, avatar, đổi mật khẩu, xóa tài khoản)
VŨ VĂN THÔNG	Manager / Admin – Monitoring – Realtime System 
• Quản lý đơn hàng 
• Quản lý người dùng 
• Giám sát hệ thống
 • Dashboard & phân tích	•	Theo dõi & cập nhật trạng thái đơn hàng realtime (WebSocket – Manager) 
•	Lịch sử đơn hàng (filter, smart sorting, pagination, thống kê) 
•	Live Chat hỗ trợ & Admin Monitoring (logs, alerts, risk score)
HUỲNH THANH TÚ	Guest Flow – Cart – Checkout – Payment – Figma 
• Luồng khách chưa đăng nhập
 • Giỏ hàng & thanh toán 
• Voucher, tier discount
 • Prototype Figma	•	Luồng xem chi tiết sản phẩm (Guest flow hỗ trợ) 
•	Giỏ hàng & Checkout (cart, voucher, tier discount, thanh toán)
•	Đặt hàng nhóm (join session, invite code, group chat, checkout, Google Map)


BẢNG CHỨC NĂNG LỚN VÀ NHỎ HỆ THỐNG UTE TEA
1. HỆ THỐNG XÁC THỰC & BẢO MẬT
Cấp	Nhóm chức năng	Chức năng chi tiết
1	Xác thực người dùng	Đăng nhập bằng username / email / số điện thoại
		JWT Authentication
		Auto Refresh Token
		Phân quyền User / Manager / Admin
2	Đăng nhập nâng cao	Đăng nhập sinh trắc học (Biometric)
		Mã hóa token bằng Android Keystore
		Lưu session an toàn
3	Đăng ký & OTP	Đăng ký tài khoản
		Gửi OTP qua Email / SMS
		Xác thực OTP
		Resend OTP
4	Quên mật khẩu	OTP reset mật khẩu
		Nhập OTP + mật khẩu mới
5	Xác thực thanh toán	OTP xác thực số điện thoại khi checkout
________________________________________
2. QUẢN LÝ TÀI KHOẢN NGƯỜI DÙNG
Cấp	Nhóm chức năng	Chức năng chi tiết
1	Hồ sơ cá nhân	Xem thông tin tài khoản
		Cập nhật tên, email, số điện thoại, địa chỉ
2	Ảnh đại diện	Chọn ảnh từ thư viện
		Nén ảnh
		Upload avatar
3	Bảo mật tài khoản	Đổi mật khẩu
		Xóa tài khoản
		Đăng xuất
________________________________________
3. TRANG CHỦ & TRẢI NGHIỆM NGƯỜI DÙNG
Cấp	Nhóm chức năng	Chức năng chi tiết
1	Trang chủ	Banner
		Best Seller
		For You (gợi ý cá nhân)
		Quick Actions
2	Cá nhân hóa	Hiển thị thời tiết
		Seasonal Effects theo mùa
3	Điều hướng	Bottom Navigation
		Drawer Menu
		Search Bar
________________________________________
4. AI & TƯƠNG TÁC THÔNG MINH
CẤP	NHÓM CHỨC NĂNG	CHỨC NĂNG CHI TIẾT
1	AI Predictive Order	Phân tích lịch sử đặt hàng
		Phân tích thời gian
		Phân tích thời tiết
		Gợi ý món + độ tin cậy
2	Voice Interaction	Voice Order
		Voice Search
		Chuẩn hóa tiếng Việt
3	Chatbot AI	Trả lời tự động
		Gợi ý sản phẩm
		Hướng dẫn đặt hàng
________________________________________
5. QUẢN LÝ SẢN PHẨM & THỰC ĐƠN
Cấp	Nhóm chức năng	Chức năng chi tiết
1	Thực đơn	Hiển thị sản phẩm
		Phân loại theo danh mục
		Sắp xếp theo giá
		Load more / Pagination
2	Tìm kiếm	Tìm kiếm realtime
		Gợi ý từ khóa
		Fuzzy matching
		Bỏ dấu tiếng Việt
3	Chi tiết sản phẩm	Chọn size
		Chọn topping
		Tính giá realtime
		Animation add-to-cart
		Xem review
4	Quản lý danh mục	CRUD danh mục
		Upload ảnh danh mục
		Sắp xếp thứ tự hiển thị
________________________________________
6. GIỎ HÀNG & THANH TOÁN
Cấp	Nhóm chức năng	Chức năng chi tiết
1	Giỏ hàng	Thêm / xóa sản phẩm
		Cập nhật số lượng
		Select / Unselect
2	Giảm giá	Áp voucher
		Voucher Spin Wheel
		Tier Discount
3	Phí giao hàng	Tính phí theo khoảng cách
		Tích hợp GHN API
		Free ship theo điều kiện
4	Thanh toán	COD
		VNPay
		MoMo
		PayPal
		VietQR
5	Checkout	Tính tổng tiền
		OTP xác thực
		Tạo đơn hàng
		Bill preview
________________________________________
7. ĐƠN HÀNG & THEO DÕI REALTIME
Cấp	Nhóm chức năng	Chức năng chi tiết
1	Trạng thái đơn	PENDING / MAKING / SHIPPING
		READY / DONE / CANCELLED
2	Realtime	WebSocket cập nhật trạng thái
		Push notification
3	Lịch sử đơn	Filter
		Smart sorting
		Pagination
4	Chi tiết đơn	Tracking timeline
		Liên hệ hỗ trợ
________________________________________
8. ĐẶT HÀNG NHÓM (GROUP ORDER)
Cấp	Nhóm chức năng	Chức năng chi tiết
1	Quản lý nhóm	Tạo nhóm
		Invite code
		Join nhóm
2	Phiên nhóm	Thêm món chung
		Chat nhóm realtime
		Lock / Unlock
		Checkout nhóm
3	Chia sẻ	Share invite link
		QR code join
		Notification thành viên
________________________________________
9. LOYALTY & GAMIFICATION
Cấp	Nhóm chức năng	Chức năng chi tiết
1	Loyalty	Tích điểm
		Bronze / Silver / Gold / Diamond
		Quy đổi voucher
2	Spin Wheel	Quay vòng
		Nhận và lưu voucher
		Giới hạn lượt quay
3	Challenge	Challenge ngày / tuần
		Theo dõi tiến độ
		Leaderboard
4	Member Tier	Quyền lợi theo hạng
		Điều kiện nâng hạng
________________________________________
10. THÔNG BÁO & PUSH NOTIFICATION
Cấp	Nhóm chức năng	Chức năng chi tiết
1	Push Notification	OneSignal
		Thông báo đơn hàng
		Thông báo khuyến mãi
2	In-App Notification	Lưu thông báo
		Đã đọc / chưa đọc
		Xóa thông báo
3	Email Notification	Email xác nhận
		Reset mật khẩu
4	Notification Types	ORDER / PROMOTION
		SYSTEM / GROUP_CHAT
		LIVE_CHAT
________________________________________
11. LIVE CHAT & HỖ TRỢ
Cấp	Nhóm chức năng	Chức năng chi tiết
1	Live Chat User	Gửi / nhận tin realtime
		Upload ảnh
2	Live Chat Manager	Quản lý nhiều hội thoại
		Đóng / chuyển chat
3	Chatbot AI	Trả lời tự động
		Escalate to human
________________________________________
12. ĐÁNH GIÁ & REVIEW
Cấp	Nhóm chức năng	Chức năng chi tiết
1	Review sản phẩm	Đánh giá sao
		Bình luận
		Upload ảnh
2	Quản lý review	Phản hồi
		Xóa review
3	Review Analytics	Rating trung bình
		Phân tích sentiment
________________________________________
13. QUẢN LÝ CỬA HÀNG
Cấp	Nhóm chức năng	Chức năng chi tiết
1	Thông tin cửa hàng	Tên, địa chỉ, SĐT
		Giờ mở / đóng
2	Quản lý vị trí	GPS
		Bán kính giao hàng
3	Cài đặt vận hành	Công suất
		Thời gian chuẩn bị
________________________________________
14. QUẢN LÝ & ĐIỀU HÀNH (MANAGER)
Cấp	Nhóm chức năng	Chức năng chi tiết
1	Đơn hàng	Cập nhật trạng thái
		In hóa đơn
2	Sản phẩm	CRUD sản phẩm
		Upload ảnh
3	Voucher	Quản lý voucher
4	Người dùng	Khóa / nâng quyền
5	Dashboard	Thống kê realtime
________________________________________
15. GIÁM SÁT & BẢO MẬT (MANAGER)
Cấp	Nhóm chức năng	Chức năng chi tiết
1	Monitoring	Log hành vi
		Theo dõi IP
2	Risk Score	Phát hiện bất thường
3	Phòng thủ	Block IP
		Rate limiting
Whitelist IP
4	User Management	Quản lý toàn bộ user
5	System Config	Feature flags
		Maintenance mode
________________________________________
16. DỰ BÁO & PHÂN TÍCH (MANAGER)
Cấp	Nhóm chức năng	Chức năng chi tiết
1	Dự báo doanh thu	Hôm nay / 7 ngày / tháng
2	Giờ cao điểm	Thống kê theo giờ
3	Cảnh báo	Quá tải / hết hàng
4	Nhân sự	Đề xuất số nhân viên
5	BI	Xu hướng bán hàng














MỤC LỤC
1. Tổng quan dự án	1
2. Tổng quan kiến trúc	1
3. Danh sách chức năng & giải thích triển khai	1
3.1. Đăng nhập, JWT, Biometric Login, Auto Refresh Token	1
3.2. Đăng ký tài khoản, OTP Verify/Resend	2
3.3. Quên mật khẩu - Reset mật khẩu bằng OTP, Xác thực số điện thoại khi mua hàng	2
3.4. Quản lý hồ sơ, xem, sửa profile, upload avatar, đổi mật khẩu, xóa tài khoản	3
3.5. Trang chủ, Banner, Best Seller/For You, Quick Actions, Weather, Seasonal Effects	3
3.6. F06 - AI Predictive Order, gợi ý món theo lịch sử, thời gian, thời tiết	4
3.7. Voice Order và Voice Search	5
3.8. Loyalty, tích điểm, hạng thành viên, Spin Wheel nhận voucher	5
3.9. Thực đơn, hiển thị sản phẩm theo danh mục, sắp xếp theo giá	6
3.10. Tìm kiếm nâng cao, gợi ý realtime, bỏ dấu tiếng Việt, fuzzy matching	6
3.11. Chi tiết sản phẩm, chọn size hoặc topping, tính giá realtime, add-to-cart animation, xem review	7
3.12. Giỏ hàng và Checkout, chọn sản phẩm, voucher, tier discount, tạo đơn	7
3.13. Theo dõi trạng thái đơn hàng realtime (WebSocket) và cập nhật trạng thái (Manager)	8
3.14. Lịch sử đơn hàng, thống kê, filter trạng thái, smart sorting, pagination	8
3.15. Đặt hàng nhóm, tạo join session, invite code, lock và unlock, group chat, checkout	9
3.16. Live Chat hỗ trợ khách hàng và Admin Monitoring (logs/alerts/risk score)	9
3.17. Thông báo đẩy	10
4. Công nghệ và Tools sử dụng	11
5. Cấu trúc Database chính (Database Schema)	11
6. Tổng hợp API Endpoints	12
7. Bảo mật và Tối ưu hóa	13
8. Testing và Deployment	14
9. Tính năng độc đáo nổi bật (Unique Features Highlight)	14
10. Tài liệu tham khảo	14






 
 
1. Tổng quan dự án
UTE Tea là hệ thống đặt đồ uống (trà sữa) gồm Android app (Kotlin) và Backend API (Spring Boot). Hệ thống hỗ trợ nhiều vai trò: User (khách hàng), Manager (quản lý cửa hàng) và Admin (giám sát bảo mật). Các tính năng chính bao gồm: đặt hàng, giỏ hàng, thanh toán, khuyến mãi, loyalty (tích điểm + vòng quay), đặt hàng nhóm, live chat và hệ thống giám sát hành vi người dùng.
2. Tổng quan kiến trúc
Frontend Android xây dựng theo mô hình MVVM (UI: Activities/Fragments; Network: Retrofit/OkHttp/WebSocket; Data Models; Adapters). Backend xây dựng theo Spring Boot MVC phân lớp Controller - Service - Repository, kèm Security/Filters (JWT, phân quyền theo role, ghi log, rate limiting).
3. Danh sách chức năng & giải thích triển khai 
3.1. Đăng nhập, JWT, Biometric Login, Auto Refresh Token
Phụ Trách: Xín Lợi Huy
Thành phần Android: LoginActivity, SessionManager (EncryptedSharedPreferences), KeyStoreManager, AuthInterceptor, RetrofitClient/ApiService
Thành phần Backend: AuthController (POST /api/auth/login, POST /api/auth/refresh-token), AuthService, SecurityConfig/JWT filter
Luồng xử lý:
•	User nhập username/phone + password trên LoginActivity.
•	App gọi POST /api/auth/login để nhận access token + thông tin user (role, tier).
•	Lưu token vào EncryptedSharedPreferences; nếu bật Biometric thì mã hóa token bằng Android KeyStore.
•	Mọi request đi qua AuthInterceptor: tự gắn header Authorization: Bearer <token>. Nếu gặp 401 thì gọi refresh-token và retry.
Giải thích triển khai:
Android: Tạo LoginRequest -> ApiService.login() -> lưu token + user vào SessionManager.
Android: BiometricPrompt xác thực -> giải mã token từ KeyStore -> đăng nhập nhanh không cần nhập lại mật khẩu.
Backend: AuthService verify mật khẩu, sinh JWT; refresh-token cấp token mới khi token cũ hết hạn.
			 
3.2. Đăng ký tài khoản, OTP Verify/Resend
Phụ Trách: Xín Lợi Huy
Thành phần Android: RegisterActivity, OtpActivity, ApiService
Thành phần Backend: AuthController (POST /api/auth/register-with-otp, POST /api/auth/otp-verify, POST /api/auth/resend-otp), AuthService
Luồng xử lý:
•	User nhập thông tin đăng ký (username/email/phone/password).
•	App gọi register-with-otp -> backend tạo OTP 6 số và gửi qua email.
•	User nhập OTP ở OtpActivity -> gọi otp-verify để kích hoạt tài khoản.
•	Nếu hết hạn/chưa nhận OTP -> gọi resend-otp để gửi lại.
Giải thích triển khai (tóm tắt):
Android: Validate form trước khi gọi API; UX countdown cho resend OTP.
Backend: Lưu OTP kèm expiry; verify đúng OTP mới active user; sai OTP trả lỗi và ghi log.

 
	Hình ảnh otp gửi qua gmail khi đăng ký 
 
3.3. Quên mật khẩu - Reset mật khẩu bằng OTP, Xác thực số điện thoại khi mua hàng
Phụ Trách: Xín Lợi Huy
Thành phần Android: ForgotPasswordActivity, ResetPasswordActivity, ApiService
Thành phần Backend: AuthController (POST /api/auth/forgot-password, POST /api/auth/reset-password), AuthService, HttpSmsService (/api/otp/**),
Luồng xử lý:
•	User nhập email/username để yêu cầu quên mật khẩu.
•	Backend gửi OTP reset password qua email.
•	User nhập OTP và mật khẩu mới -> gọi reset-password.
•	Backend xác thực OTP, hash mật khẩu mới và cập nhật user.
•	Xác thực OTP với số điện thoại: Khi đặt hàng, hệ thống gửi mã 6 số qua SMS (sử dụng httpSMS Gateway). User nhập mã vào App để Backend đối soát và xác thực quyền thanh toán.
Giải thích triển khai (tóm tắt):
Android: Tách 2 màn hình (gửi OTP, nhập OTP + mật khẩu mới) để giảm nhầm luồng.
Backend: Hash password bằng BCrypt; vô hiệu OTP sau khi dùng thành công; Tích hợp API cổng tin nhắn để biến thiết bị Android Gateway thành trạm phát SMS OTP nội địa, giúp tối ưu chi phí và tránh bị nhà mạng chặn spam bằng cách đính kèm Timestamp vào nội dung tin.
  
Hình ảnh nhập gmail để gửi otp khi quên mật khẩu
3.4. Quản lý hồ sơ, xem, sửa profile, upload avatar, đổi mật khẩu, xóa tài khoản
Phụ Trách: Xín Lợi Huy
Thành phần Android: AccountFragment, UserProfileActivity, ChangePasswordActivity, image compression, ApiService
Thành phần Backend: UserProfileController (/api/me), UserProfileService
Luồng xử lý:
•	App gọi GET /api/me để lấy profile (tên, email, phone, địa chỉ, tier, điểm).
•	Cập nhật profile qua PUT /api/me.
•	Upload avatar: chọn ảnh -> nén ảnh -> POST /api/me/avatar.
•	Đổi mật khẩu qua PUT /api/me/change-password; xóa tài khoản qua DELETE /api/me (có confirm).
Giải thích triển khai (tóm tắt):
Android: Chọn ảnh từ thư viện, nén ảnh trước upload để giảm dung lượng.
Backend: Validate dữ liệu, lưu avatar và cập nhật đường dẫn; xóa tài khoản có thể dùng soft delete và backup dữ liệu.


 
           Hình ảnh chức năng về cài đặt user
3.5. Trang chủ, Banner, Best Seller/For You, Quick Actions, Weather, Seasonal Effects
Phụ trách: Nguyễn Thành An
Thành phần Android: HomeFragment, adapters (carousel), DataCache, OneSignal notifications
Thành phần Backend: DrinkController (GET /api/drinks, best-sellers), các API phụ trợ
Luồng xử lý:
•	HomeFragment tải banner + best seller + danh sách sản phẩm gợi ý.
•	Hiển thị quick actions: Voice Order, Chatbot, Spin Wheel, Group Order.
•	Gọi API thời tiết để hiển thị Weather Card.
•	SeasonalEffectManager kích hoạt hiệu ứng theo mùa (tuyết rơi/hoa đào/lá vàng...).
Giải thích triển khai (tóm tắt):
Android: RecyclerView + ViewPager2 cho banner/carousel; caching Fragment để tối ưu hiệu năng.
Android: SeasonalEffectManager điều khiển custom view/animation theo tháng hoặc sự kiện.
 
Hình ảnh Trang chủ

 
Hình ảnh Best Seller và For you
 
Hình ảnh Quick Action
 
Hình ảnh Tuỳ chọn hiệu ứng giao diện theo Seasons và Event

 
Hình ảnh giao diện theo các Seasons

 
Hình ảnh giao diện theo các Event

3.6. AI Predictive Order, gợi ý món theo lịch sử, thời gian, thời tiết
Phụ trách: Nguyễn Thành An
Thành phần Android: MainActivity/HomeFragment (dialog gợi ý), ApiService
Thành phần Backend: Predictive Order API (GET /api/predictive-order) + service tính điểm
Luồng xử lý:
•	Khi mở app, HomeFragment gọi /api/predictive-order.
•	Backend tính score theo TimeScore/DayScore/RecencyScore/FrequencyScore và trả predictedDrink + confidence.
•	App hiển thị dialog gợi ý, cho phép 'Thêm vào giỏ' hoặc 'Để sau'.
•	Chống spam: giới hạn số lần gợi ý/ngày và khoảng cách thời gian giữa các gợi ý.
Giải thích triển khai:
Backend: Tính điểm và chọn món có score cao nhất vượt ngưỡng; trả kèm lý do gợi ý để giải thích cho user.
Android: Map predictedDrink -> addToCart() nếu user đồng ý.
 
Hình ảnh Gợi ý thông minh từ AI (AI Predictive Order)

 
Hình ảnh Gợi ý món dựa trên Lịch sử, thời gian và thời tiết
3.7. Voice Order và Voice Search
Phụ trách: Nguyễn Thành An
Thành phần Android: HomeFragment/MenuFragment, SpeechRecognizer, microphone permission handling
Thành phần Backend: DrinkController (GET /api/drinks/search)
Luồng xử lý:
•	User bấm Voice Order -> app xin quyền microphone -> mở dialog voice.
•	Speech-to-Text chuyển giọng nói thành text.
•	App dùng text để search món (gửi keyword đến API search hoặc lọc local).
•	User xác nhận -> thêm món vào giỏ hàng nhanh.
Giải thích triển khai (tóm tắt):
Android: Chuẩn hóa text (lowercase, bỏ dấu) để tăng độ chính xác nhận diện.
Backend: Search sanitize input, giới hạn độ dài và trả danh sách phù hợp.
 
Hình ảnh Đặt hàng bằng giọng nói

 
Hình ảnh Tìm kiếm bằng giọng nói
3.8. Loyalty, tích điểm, hạng thành viên, Spin Wheel nhận voucher
Phụ trách: Huỳnh Thanh Tú
Thành phần Android: SpinWheelActivity, UI animation, voucher dialog, ApiService
Thành phần Backend: LoyaltyController (/api/loyalty/points, /api/loyalty/spin, /api/loyalty/rewards, /api/loyalty/tier/benefits)
Luồng xử lý:
•	App gọi /points để hiển thị điểm và tier hiện tại.
•	User quay vòng xoay -> POST /spin -> backend random phần thưởng theo xác suất.
•	Backend trả voucher code/giá trị; app hiển thị dialog kết quả.
•	Voucher spin được lưu và có thể áp dụng trong Cart (kết hợp voucher thường).
Giải thích triển khai:
Backend: Tính tier dựa trên điểm/doanh thu; tự nâng hạng khi đạt ngưỡng.
Android: SpinWheelActivity chạy animation rồi reveal kết quả từ API để UX mượt.
 
Hình ảnh: Tích điểm hạng thành viên
3.9. Thực đơn, hiển thị sản phẩm theo danh mục, sắp xếp theo giá
Phụ trách: Nguyễn Thành An
Thành phần Android: MenuFragment, CategoryAdapter, ProductAdapter, pagination
Thành phần Backend: DrinkController (GET /api/drinks, GET /api/categories, GET /api/drinks/page)
Luồng xử lý:
•	MenuFragment gọi API lấy categories và danh sách drinks (có thể phân trang).
•	User chọn category -> lọc danh sách theo categoryId.
•	User chọn sort -> sắp xếp tăng/giảm theo giá.
•	Load more khi scroll đến cuối (pagination).
Giải thích triển khai (tóm tắt):
Android: RecyclerView GridLayoutManager 2 cột; adapter update list theo filter/sort.
Backend: Endpoint page trả PageResponse; service tối ưu query (JOIN FETCH/batch loading) để giảm N+1.

3.10. Tìm kiếm nâng cao, gợi ý realtime, bỏ dấu tiếng Việt, fuzzy matching
Phụ trách: Vũ Văn Thông
Thành phần Android: Search bar trong MenuFragment, voice search, suggestion list
Thành phần Backend: DrinkController (GET /api/drinks/search)
Luồng xử lý:
•	User gõ keyword -> hiển thị suggestion realtime.
•	App chuẩn hóa keyword (lowercase, trim, bỏ dấu) để tìm kiếm tốt hơn.
•	Gửi keyword đến API search hoặc lọc local tùy chế độ.
•	Hiển thị kết quả và highlight từ khóa.
Giải thích triển khai:
Android: removeVietnameseAccents() để normalize trước khi so sánh chuỗi.
Backend: Sanitize keyword, chống injection, và giới hạn kết quả trả về để tối ưu.
3.11. Chi tiết sản phẩm, chọn size hoặc topping, voucher, tính giá realtime, add-to-cart animation, xem review
Phụ trách: Huỳnh Thanh Tú
Thành phần Android: ProductDetailActivity, Glide image, AddToCartAnimator, ReviewAdapter
Thành phần Backend: DrinkController (GET /api/drinks/{id}); Review API (GET /api/reviews/drink/{drinkId})
Luồng xử lý:
•	App tải chi tiết đồ uống theo id.
•	User chọn size và toppings -> app tính giá theo công thức (base + extra + toppings) x quantity.
•	Bấm 'Thêm vào giỏ' -> chạy animation bay vào giỏ.
•	Hiển thị danh sách review và rating summary.
Giải thích triển khai (tóm tắt):
Android: Recalculate mỗi lần đổi size/topping/quantity để UX realtime.
Backend: Trả sizes/toppings kèm giá; review API hỗ trợ phân trang.


 	 	 
Hình ảnh: Chi tiết sản phẩm
 

Hình ảnh: Chọn size cho sản phẩm

 
Hình ảnh: Chọn voucher
3.12. Giỏ hàng và Checkout, chọn sản phẩm, tier discount, tạo đơn
Phụ trách: Huỳnh Thanh Tú
Thành phần Android: CartActivity, CartAdapter (select/unselect), VoucherSelection dialog, OTP verification
Thành phần Backend: CartController (/api/cart/**), PromotionController (/api/promotions/validate), OrderController (POST /api/orders)
Luồng xử lý:
•	CartActivity gọi GET /api/cart để lấy giỏ hàng.
•	User chọn item (select/unselect), cập nhật quantity (PUT /api/cart/items/{id}).
•	Áp voucher: gọi /api/promotions/validate (và/hoặc validate voucher spin).
•	Tính tổng: subtotal - voucherDiscount - tierDiscount + shippingFee.
•	Tạo đơn: POST /api/orders; sau khi thành công có thể clear cart.
Giải thích triển khai:
Android: Tính toán giá realtime để hiển thị ngay; backend vẫn re-check để chống gian lận.
Backend: Validate items/quantity, áp dụng promotion/tier, ghi log hoạt động và phát sự kiện realtime.
 	 
Hình ảnh: Giỏ hàng
 
Hình ảnh: Sản phẩm trong giỏ hàng
3.13. Theo dõi trạng thái đơn hàng realtime (WebSocket) và cập nhật trạng thái (Manager)
Phụ trách: Vũ Văn Thông
Thành phần Android: OrderWebSocketManager, OrderFragment/OrderDetailActivity
Thành phần Backend: OrderController (GET /api/orders/my, GET /api/orders/{id}, PUT /api/orders/{id}/status) + WebSocket (STOMP)
Luồng xử lý:
•	Sau khi đặt hàng, app hiển thị trạng thái (PENDING/MAKING/SHIPPING/READY/DONE).
•	OrderWebSocketManager subscribe topic cập nhật trạng thái theo orderId.
•	Manager cập nhật trạng thái qua API PUT /orders/{id}/status.
•	App nhận message WebSocket -> cập nhật UI realtime.
Giải thích triển khai:
Android: WebSocket callback dispatch lên UI thread để cập nhật chip trạng thái.
Backend: Khi status đổi, service publish event qua WebSocket để các client cập nhật ngay.

 
Hình ảnh trạng thái đơn hàng (PENDING/MAKING/SHIPPING/READY/DONE)

3.14. Lịch sử đơn hàng, thống kê, filter trạng thái, smart sorting, pagination,setting
Phụ trách: Vũ Văn Thông
Thành phần Android: OrderFragment (tabs + filters), OrderAdapter, load more
Thành phần Backend: OrderController (GET /api/orders/my, GET /api/orders/my/current)
Luồng xử lý:
•	OrderFragment gọi /my và /my/current để lấy đơn hàng.
•	Smart sorting: đơn đang xử lý ưu tiên; đơn DONE sort mới->cũ; đơn xử lý sort cũ->mới.
•	Filter theo trạng thái (PENDING, MAKING, ...).
•	Pagination/load more khi cuộn
•	Quản lý cửa hàng (thông tin chi nhánh, trạng thái hoạt động, cấu hình)
•	Quản lý người dùng (danh sách khách, khóa/mở khóa, xem lịch sử/risk)
•	Quản lý Voucher (CRUD voucher, bật/tắt, theo dõi usage)
•	Thông báo đẩy (gửi push notification cho khách hàng qua OneSignal)
•	Quản lý đánh giá (xem/ẩn/xóa/duyệt đánh giá sản phẩm)

Giải thích triển khai:
Android: Adapter hỗ trợ hiển thị theo trạng thái; load more để tối ưu performance.
	Backend: Có thể hỗ trợ page/filter để giảm tải dữ liệu trả về.
                             
			                     Thống kê doanh thu
                                      
                                     
		       Hình ảnh top sản phẩm bán chạy và đánh giá cao
                     
		          Hình ảnh sắp xếp đơn hang từ cũ đến mới
                     
Hình ảnh chức năng của admin có thể quản lý thêm xóa, nâng user->manager
    
 
3.15. Đặt hàng nhóm, tạo join session, invite code, lock và unlock, group chat, checkout, goolemap
Phụ trách: Huỳnh Thanh Tú
Thành phần Android: CreateGroupOrderActivity, JoinGroupOrderActivity, GroupOrderActivity, GroupChatWebSocketManager
Thành phần Backend: GroupOrderController (/api/group-orders/**) + WebSocket group updates
Luồng xử lý:
•	Host tạo phiên nhóm -> backend trả inviteCode 6 ký tự.
•	Thành viên join bằng inviteCode; backend kiểm tra status và maxMembers.
•	Cùng thêm món, chat realtime; host có quyền lock/unlock và checkout.
•	Khi checkout, backend tạo đơn nhóm và cập nhật trạng thái phiên.
Giải thích triển khai:
Android: WebSocket subscribe updates để đồng bộ danh sách items/members.
Backend: GroupOrderService kiểm soát quyền (host-only), trạng thái OPEN/LOCKED/COMPLETED/EXPIRED.
 	 	 
Hình ảnh: Nhóm đặt hàng

 	 
Hình ảnh: Chi nhánh trên Google Map
3.16. Live Chat hỗ trợ khách hàng và Admin Monitoring (logs/alerts/risk score)
Phụ trách: Vũ Văn Thông
Thành phần Android: LiveChatWebSocketManager, LiveChatActivity, UserMonitoringActivity, Monitoring adapters
Thành phần Backend: LiveChatController (/api/chat/**), UserMonitoringController (/api/monitoring/**)
Luồng xử lý:
•	User mở Live Chat -> tạo conversation và gửi/nhận message realtime qua WebSocket.
•	Manager xem hàng đợi hội thoại, nhận phân công và phản hồi.
•	Admin Monitoring dashboard lấy logs/alerts/risk score để đánh giá hành vi user và xử lý cảnh báo.
•	Alert mới có thể push realtime qua WebSocket để admin xử lý kịp thời.
Giải thích triển khai:
Android: Live chat dùng adapter hiển thị tin nhắn theo sender (user/manager).
Backend: MonitoringService ghi log, tính risk score, tạo alert khi phát hiện hành vi bất thường.

               
		Hình ảnh livechat hỗ trợ khách hang realtime
                          
                                 Hình ảnh giám sát user hoạt động
 
 
                         Hình ảnh quản lý blockIP
3.17. Thông báo đẩy
Phụ trách: Xín Lợi Huy
Thành phần Android: UTETeaApplication (OneSignal Init), LoginActivity (External ID Mapping), AccountFragment
Thành phần Backend: OneSignalService, NotificationController (/api/notifications/**)
Luồng xử lý:
•	Định danh thiết bị: Khi User đăng nhập thành công, App gọi OneSignal.login(userId) để ánh xạ ID database với thiết bị, cho phép gửi thông báo cá nhân hóa mà không cần lưu Token thủ công.
•	Thông báo đơn hàng: Khi Manager cập nhật trạng thái đơn hàng (MAKING, SHIPPING, DONE...), Backend tự động gọi OneSignal API để đẩy thông báo realtime đến đúng thiết bị của User dựa trên External ID.
•	Quản trị viên (Manager):
	Tích chọn "Gửi thông báo" khi thêm Voucher mới để gửi tin nhắn Broadcast cho toàn bộ khách hàng.
	Sử dụng giao diện "Quản lý thông báo đẩy" để soạn tiêu đề/nội dung và chọn đối tượng gửi (Tất cả hoặc danh sách ID cụ thể).
Giải thích triển khai:
Android: Tích hợp SDK OneSignal để nhận Push Notification.
Backend: Sử dụng HttpURLConnection gửi JSON payload kèm x-api-key để ra lệnh cho OneSignal Server đẩy tin.

 
                 Hình ảnh thông báo đẩy

4. Công nghệ và Tools sử dụng
-	Frontend Android:
	Kotlin 100%, Android SDK 24-34, MVVM Architecture
	Retrofit 2, OkHttp 3, WebSocket, Gson
	Material Design 3, RecyclerView, ViewPager2
	Biometric Authentication, EncryptedSharedPreferences, OneSignal
	Speech Recognition, Lottie Animations, Glide
-	Backend Spring Boot:
	Java 17, Spring Boot 3.5.7, Spring Security 6.x
	MySQL 8.0, JPA/Hibernate, JWT Authentication
	WebSocket (STOMP), Redis Caching
	VNPay Payment, SendGrid Email, OneSignal Push, HttpSMS
	Docker, Railway/Render Deployment
5. Cấu trúc Database chính (Database Schema)
Hệ thống sử dụng MySQL với các bảng cốt lõi phục vụ: người dùng, sản phẩm, đơn hàng, khuyến mãi, đặt hàng nhóm, live chat, và giám sát hành vi (monitoring).
Bảng	Trường chính (tiêu biểu)	Mục đích
users	id, username, email, phone, password, role, member_tier, points, is_blocked, otp, otp_expiry, avatar_url	Quản lý tài khoản, xác thực, phân quyền, hạng thành viên, điểm thưởng, trạng thái khóa và OTP.
drinks	id, name, base_price, category_id, is_active, image_url	Danh sách đồ uống, giá gốc, phân loại theo danh mục, trạng thái hiển thị.
drink_categories	id, name, display_order, is_active, image_url	Quản lý danh mục đồ uống, thứ tự hiển thị, bật/tắt danh mục.
drink_sizes	id, drink_id, size_name, extra_price	Quản lý size theo từng món và giá cộng thêm.
drink_toppings	id, drink_id, topping_name, price, is_active	Quản lý topping theo món (hoặc dùng chung), giá và trạng thái.
orders	id, user_id, store_id, status, total_price, shipping_fee, discount, final_price, payment_method, created_at	Đơn hàng, trạng thái xử lý, phí ship/giảm giá, tổng thanh toán, phương thức thanh toán.
order_items	id, order_id, drink_id, drink_name_snapshot, size_name_snapshot, quantity, item_price, note	Chi tiết từng món trong đơn (lưu snapshot tên/size để không phụ thuộc dữ liệu thay đổi).
order_item_toppings	id, order_item_id, topping_name_snapshot, price_snapshot	Topping của từng món trong đơn (snapshot tên + giá).
promotions	id, code, discount_type, discount_value, start_date, end_date, usage_limit, used_count, min_order_value, is_active	Voucher/Promotion: loại giảm, giá trị giảm, điều kiện áp dụng và giới hạn lượt dùng.
group_orders	id, host_user_id, invite_code, status, store_id, order_type, delivery_address, expires_at, final_order_id	Phiên đặt hàng nhóm: mã mời, trạng thái mở/khóa, thông tin cửa hàng và đơn chốt cuối.
group_order_members	id, group_order_id, user_id, is_host	Thành viên tham gia phiên đặt nhóm (host và member).
group_order_items	id, group_order_id, user_id, drink_id, drink_name_snapshot, size_name, quantity, unit_price, item_price, toppings_snapshot	Món do từng thành viên thêm vào phiên nhóm (lưu snapshot để ổn định dữ liệu).
chat_conversations	id, user_id, manager_id, store_id, status, last_message, unread_user, unread_manager	Phiên live chat giữa user–manager, trạng thái và số tin chưa đọc.
live_chat_messages	id, conversation_id, sender_id, sender_type, content, is_read, created_at	Tin nhắn chi tiết trong live chat, phân loại người gửi và trạng thái đã đọc.
user_activity_logs	id, user_id, activity_type, ip_address, device_info, endpoint, response_status, risk_level, created_at	Log hoạt động để audit, thống kê và phục vụ tính điểm rủi ro (risk score).
user_risk_scores	id, user_id, total_score, risk_level, login_failed_count, promotion_abuse_count, auto_blocked	Bảng tổng hợp điểm rủi ro theo user, hỗ trợ cảnh báo và tự động khóa.
monitoring_alerts	id, user_id, alert_type, severity, status, handled_by, action_taken, created_at	Cảnh báo tự động (fraud/spam/brute-force…), trạng thái xử lý và hành động của admin.

6. Tổng hợp API Endpoints và chức năng

1) AUTHENTICATION
API	Method	Endpoint	Auth	Mục đích
Register OTP	POST	/api/auth/register-with-otp	No	Đăng ký và gửi OTP
Verify OTP	POST	/api/auth/otp-verify	No	Xác thực OTP kích hoạt
Resend OTP	POST	/api/auth/resend-otp?target=	No	Gửi lại OTP
Login	POST	/api/auth/login	No	Đăng nhập, trả access/refresh
Refresh token	POST	/api/auth/refresh-token	No	Làm mới access token
Forgot password	POST	/api/auth/forgot-password	No	Gửi OTP reset
Reset password	POST	/api/auth/reset-password	No	Reset mật khẩu bằng OTP
________________________________________
2) USER PROFILE (ME)
API	Method	Endpoint	Auth	Mục đích
Get profile	GET	/api/me	Yes	Lấy thông tin cá nhân
Update profile	PUT	/api/me	Yes	Cập nhật thông tin
Upload avatar	POST	/api/me/avatar	Yes	Upload ảnh đại diện
Change password	PUT	/api/me/change-password	Yes	Đổi mật khẩu
Delete account	DELETE	/api/me	Yes	Xóa tài khoản
________________________________________
3) PRODUCT (DRINKS & CATEGORIES)
API	Method	Endpoint	Auth	Mục đích
List drinks	GET	/api/drinks	No	Danh sách đồ uống
Drink detail	GET	/api/drinks/{id}	No	Chi tiết 1 món
Search drinks	GET	/api/drinks/search?keyword=	No	Tìm kiếm món
List categories	GET	/api/categories	No	Danh sách danh mục
________________________________________
4) CART
API	Method	Endpoint	Auth	Mục đích
Add to cart	POST	/api/cart/add	Yes	Thêm món vào giỏ
Get my cart	GET	/api/cart	Yes	Xem giỏ hàng
Update quantity	PUT	/api/cart/items/{cartItemId}?quantity=	Yes	Sửa số lượng
Update full item	PUT	/api/cart/items/{cartItemId}/full	Yes	Sửa size/topping/note
Remove item	DELETE	/api/cart/items/{cartItemId}	Yes	Xóa 1 item
Clear cart	DELETE	/api/cart/clear	Yes	Xóa toàn bộ giỏ
________________________________________
5) ORDERS
API	Method	Endpoint	Auth	Role	Mục đích
Preview bill	POST	/api/orders/preview	Yes	USER	Xem trước hóa đơn (giảm giá/ship)
Create order	POST	/api/orders	Yes	USER	Tạo đơn
My orders	GET	/api/orders/my	Yes	USER	Lịch sử đơn
My current orders	GET	/api/orders/my/current	Yes	USER	Đơn đang xử lý
Order detail	GET	/api/orders/{orderId}	Yes	USER	Chi tiết đơn
All orders	GET	/api/orders/all?page=&size=	Yes	MANAGER	Danh sách đơn (phân trang)
Update status	PUT	/api/orders/{orderId}/status?status=	Yes	MANAGER	Cập nhật trạng thái
________________________________________
6) PAYMENTS
API	Method	Endpoint	Auth	Mục đích
VNPay create	POST	/api/vnpay/create-payment	Yes	Tạo link thanh toán VNPay
MoMo create	POST	/api/momo/create-payment	Yes	Tạo link/QR MoMo
PayPal create	POST	/api/paypal/create-payment	Yes	Tạo link PayPal approval
________________________________________
7) PROMOTIONS (VOUCHER)
API	Method	Endpoint	Auth	Role	Mục đích
List active promotions	GET	/api/promotions	No	Public	Xem voucher đang chạy
Validate promotion	GET	/api/promotions/validate?code=&orderAmount=	No	Public	Kiểm tra hợp lệ
Create promotion	POST	/api/promotions/manager?sendNotification=	Yes	MANAGER	Tạo voucher
Update promotion	PUT	/api/promotions/manager/{id}	Yes	MANAGER	Sửa voucher
Delete promotion	DELETE	/api/promotions/manager/{id}	Yes	MANAGER	Xóa voucher
Toggle status	PATCH	/api/promotions/manager/{id}/toggle-status	Yes	MANAGER	Bật/tắt voucher
________________________________________
8) GROUP ORDER
API	Method	Endpoint	Auth	Mục đích
Create group	POST	/api/group-orders	Yes	Tạo phiên nhóm
Join group	POST	/api/group-orders/join	Yes	Tham gia bằng mã
Group detail	GET	/api/group-orders/{id}	Yes	Xem phiên nhóm
Get by code	GET	/api/group-orders/code/{inviteCode}	Yes	Tra theo mã mời
Active groups	GET	/api/group-orders/active	Yes	Danh sách phiên đang hoạt động
Add item	POST	/api/group-orders/{id}/items	Yes	Thêm món vào phiên
Update item	PUT	/api/group-orders/{id}/items/{itemId}	Yes	Sửa món trong phiên
Remove item	DELETE	/api/group-orders/{id}/items/{itemId}	Yes	Xóa món
Lock	POST	/api/group-orders/{id}/lock	Yes	Khóa phiên
Unlock	POST	/api/group-orders/{id}/unlock	Yes	Mở khóa phiên
Leave	POST	/api/group-orders/{id}/leave	Yes	Rời phiên
Checkout	POST	/api/group-orders/{id}/checkout	Yes	Chốt đơn từ phiên nhóm
Cancel group	DELETE	/api/group-orders/{id}	Yes	Hủy phiên
________________________________________
9) NOTIFICATIONS
API	Method	Endpoint	Auth	Mục đích
My notifications	GET	/api/notifications/my	Yes	Danh sách thông báo
Unread list	GET	/api/notifications/unread	Yes	Thông báo chưa đọc
Unread count	GET	/api/notifications/unread-count	Yes	Đếm chưa đọc
Mark read	PUT	/api/notifications/{id}/read	Yes	Đánh dấu đã đọc
Read all	PUT	/api/notifications/read-all	Yes	Đọc tất cả
Delete	DELETE	/api/notifications/{id}	Yes	Xóa thông báo
________________________________________
10) LOYALTY
API	Method	Endpoint	Auth	Mục đích
Get points	GET	/api/loyalty/points	Yes	Xem điểm + tier
Spin wheel	POST	/api/loyalty/spin	Yes	Quay nhận voucher
Rewards list	GET	/api/loyalty/rewards	Yes	Voucher spin hiện có
Validate spin voucher	GET	/api/loyalty/voucher/validate?code=	Yes	Check voucher spin
Tier benefits	GET	/api/loyalty/tier/benefits	Yes	Quyền lợi theo hạng
Check upgrade	POST	/api/loyalty/tier/check-upgrade	Yes	Kiểm tra nâng hạng
Preview tier discount	GET	/api/loyalty/tier/preview-discount?orderTotal=	Yes	Xem giảm theo tier
________________________________________
11) MANAGER
API	Method	Endpoint	Auth	Mục đích
Summary dashboard	GET	/api/manager/summary	Yes (MANAGER)	Tổng quan hôm nay
Revenue statistics	GET	/api/manager/statistics/revenue?days=&months=	Yes (MANAGER)	Thống kê doanh thu
Forecast full	GET	/api/manager/forecast	Yes (MANAGER)	Forecast tổng hợp
Forecast revenue	GET	/api/manager/forecast/revenue	Yes (MANAGER)	Dự báo doanh thu
Peak hours	GET	/api/manager/forecast/peak-hours	Yes (MANAGER)	Giờ cao điểm
Low stock	GET	/api/manager/forecast/low-stock	Yes (MANAGER)	Cảnh báo sắp hết
Staffing	GET	/api/manager/forecast/staffing	Yes (MANAGER)	Đề xuất nhân sự
Overload	GET	/api/manager/forecast/overload	Yes (MANAGER)	Cảnh báo quá tải
Orders filter	GET	/api/manager/orders?status=&page=&size=	Yes (MANAGER)	Đơn theo trạng thái
Update status	PUT	/api/manager/orders/{orderId}/status?status=	Yes (MANAGER)	Cập nhật trạng thái
Users list	GET	/api/manager/users?role=&page=&size=	Yes (MANAGER)	Danh sách user
Block/unblock user	PUT	/api/manager/users/{userId}/block?blocked=	Yes (MANAGER)	Khóa/mở khóa
Promote to manager	PUT	/api/manager/users/{userId}/promote	Yes (MANAGER)	Nâng quyền
Assign store	POST	/api/manager/users/{userId}/stores/{storeId}	Yes (MANAGER)	Gán cửa hàng
My stores	GET	/api/manager/my-stores	Yes (MANAGER)	Store đang quản lý
________________________________________
12) ADMIN (PRODUCT/CATEGORY)
API	Method	Endpoint	Auth	Mục đích
Create drink	POST	/api/admin/drinks	Yes (ADMIN)	Tạo món
Update drink	PUT	/api/admin/drinks/{id}	Yes (ADMIN)	Sửa món
Delete drink	DELETE	/api/admin/drinks/{id}	Yes (ADMIN)	Xóa món
Upload image	POST	/api/admin/drinks/upload-image	Yes (ADMIN)	Upload ảnh món
Create category	POST	/api/admin/categories	Yes (ADMIN)	Tạo danh mục
Update category	PUT	/api/admin/categories/{id}	Yes (ADMIN)	Sửa danh mục
Delete category	DELETE	/api/admin/categories/{id}	Yes (ADMIN)	Xóa danh mục
________________________________________
13) MONITORING (ADMIN)
API	Method	Endpoint	Auth	Mục đích
Monitoring dashboard	GET	/api/monitoring/dashboard	Yes (ADMIN)	Tổng quan giám sát
Activity logs	GET	/api/monitoring/activities?userId=&activityType=&riskLevel=&page=&size=	Yes (ADMIN)	Log hành vi
Alerts list	GET	/api/monitoring/alerts?severity=&status=&page=&size=	Yes (ADMIN)	Danh sách cảnh báo
Handle alert	PUT	/api/monitoring/alerts/{alertId}/handle	Yes (ADMIN)	Xử lý cảnh báo
Risk scores	GET	/api/monitoring/risk-scores?riskLevel=&page=&size=	Yes (ADMIN)	Danh sách điểm rủi ro
Risk score detail	GET	/api/monitoring/risk-scores/user/{userId}	Yes (ADMIN)	Chi tiết 1 user
Add admin note	POST	/api/monitoring/risk-scores/user/{userId}/note	Yes (ADMIN)	Ghi chú admin
Reset score	POST	/api/monitoring/risk-scores/user/{userId}/reset	Yes (ADMIN)	Reset điểm
Unblock user	POST	/api/monitoring/users/{userId}/unblock	Yes (ADMIN)	Mở khóa user
________________________________________
14) BLOCKED IP (ADMIN)
API	Method	Endpoint	Auth	Mục đích
Block IP	POST	/api/blocked-ips/block	Yes (ADMIN)	Chặn IP
Unblock IP	POST	/api/blocked-ips/{id}/unblock	Yes (ADMIN)	Mở chặn
List blocked IPs	GET	/api/blocked-ips?page=&size=	Yes (ADMIN)	Danh sách IP bị chặn
Check status	GET	/api/blocked-ips/check?ip=	Yes (ADMIN)	Kiểm tra IP

7. Bảo mật và Tối ưu hóa
Security Features:
•	JWT Authentication với auto-refresh token (giảm nguy cơ session hijack và đảm bảo trải nghiệm).
•	Rate Limiting (5-100 requests/minute tùy endpoint) để chống brute-force và spam API.
•	IP Blocking kết hợp risk score algorithm để phát hiện hành vi bất thường.
•	Biometric login với Android KeyStore encryption và EncryptedSharedPreferences.
•	Input validation & SQL injection prevention (sanitize dữ liệu, giới hạn độ dài, kiểm tra định dạng).
•	Phone OTP để xác thực sau khi mua hàng, chống giả mạo và số điện thoại giả.
Performance Optimizations:
•	N+1 Query prevention bằng JOIN FETCH/batch loading trong JPA/Hibernate.
•	Redis caching cho session, rate limiting và dữ liệu đọc nhiều (tùy cấu hình triển khai).
•	Image compression & CDN (Cloudinary) giúp tải ảnh nhanh và giảm dung lượng.
•	WebSocket cho real-time updates (order status, group order, live chat, monitoring alerts).
•	Database indexing cho các truy vấn thường dùng (userId, orderId, status, createdAt...).
8. Testing và Deployment
Testing:
-	Unit tests cho business logic (service layer).
-	Integration tests cho API endpoints (controller -> service -> repository).
-	UI tests cho các luồng quan trọng: login, add-to-cart, checkout, payment.
-	Load testing để đánh giá hiệu năng (đặc biệt với các endpoint order/cart và WebSocket).
Deployment:
-	Backend: Railway/Render (Docker container).
-	Database: Aiven MySQL Cloud.
-	CDN: Cloudinary cho images.
-	Monitoring: Health checks (endpoint /api/auth/health) và theo dõi logs.
9. Tính năng độc đáo nổi bật (Unique Features Highlight)
-	Voice Order - Đặt hàng bằng giọng nói (Speech-to-Text).
-	AI Predictive Order - Gợi ý thông minh theo thời tiết/lịch sử.
-	Group Order - Đặt hàng nhóm real-time với invite code.
-	4-Tier Loyalty - Bronze/Silver/Gold/Diamond kết hợp spin wheel.
-	Seasonal Effects - Hiệu ứng động theo mùa trên Home.
-	User Monitoring - Risk score & automated alerts.
-	Live Chat - Hỗ trợ real-time (kết hợp chatbot/FAQ tùy triển khai).
-	Biometric Security - Vân tay + KeyStore encryption.
10. Tài liệu tham khảo

