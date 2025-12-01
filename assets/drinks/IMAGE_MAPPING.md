# UTE Tea - Image Mapping Guide

## Hướng dẫn đặt tên file ảnh

Tất cả ảnh đều có định dạng `.jpeg` và được đặt trong folder tương ứng với category.

---

## 📁 Category 1: Milk Tea (milk_tea/)

| ID | Tên món | Tên file |
|----|---------|----------|
| 1 | UTE Houjicha Classic | `ute_houjicha_classic.jpeg` |
| 2 | Houjicha Kem Cheese | `houjicha_kem_cheese.jpeg` |
| 3 | Trà sữa Houjicha Trân Châu Đường Đen | `houjicha_tran_chau_duong_den.jpeg` |
| 4 | Trà sữa Matcha – Houjicha Mix | `matcha_houjicha_mix.jpeg` |

---

## 📁 Category 2: Fruit Tea (fruit_tea/)

| ID | Tên món | Tên file |
|----|---------|----------|
| 5 | Trà Đào Hồng UTE | `tra_dao_hong_ute.jpeg` |
| 6 | Trà Vải Nhài Tươi | `tra_vai_nhai_tuoi.jpeg` |
| 7 | Trà Cam Sả Mật Ong | `tra_cam_sa_mat_ong.jpeg` |
| 8 | Trà Kiwi Nhiệt Đới | `tra_kiwi_nhiet_doi.jpeg` |
| 9 | Trà Xoài Kem Tuyết | `tra_xoai_kem_tuyet.jpeg` |

---

## 📁 Category 3: Macchiato (macchiato/)

| ID | Tên món | Tên file |
|----|---------|----------|
| 10 | Hồng Trà Macchiato | `hong_tra_macchiato.jpeg` |
| 11 | Trà Xanh Kem Cheese UTE | `tra_xanh_kem_cheese_ute.jpeg` |
| 12 | Oolong Kem Sữa | `oolong_kem_sua.jpeg` |

---

## 📁 Category 4: Special (special/)

| ID | Tên món | Tên file |
|----|---------|----------|
| 13 | UTE Galaxy Tea | `ute_galaxy_tea.jpeg` |
| 15 | UTE Brown Sugar Latte | `ute_brown_sugar_latte.jpeg` |
| 16 | Matcha Đá Xay UTE | `matcha_da_xay_ute.jpeg` |
| 17 | Cookie & Cream Đá Xay | `cookie_cream_da_xay.jpeg` |
| 33 | Matcha ddas xay nham anhmat em | `matcha_test_admin.jpeg` |

---

## 📁 Category 5: Soda & Mojito (soda_mojito/)

| ID | Tên món | Tên file |
|----|---------|----------|
| 42 | Soda Kiwi Chanh | `soda_kiwi_chanh.jpeg` |
| 43 | Mojito Cam Đào | `mojito_cam_dao.jpeg` |

---

## 📁 Category 6: Sữa Chua & Yogurt (yogurt/)

| ID | Tên món | Tên file |
|----|---------|----------|
| 44 | Yogurt Dưa Lưới | `yogurt_dua_luoi.jpeg` |
| 45 | Sữa Chua Việt Quất | `sua_chua_viet_quat.jpeg` |

---

## 📁 Category 7: UTE Coffee Series (coffee/)

| ID | Tên món | Tên file |
|----|---------|----------|
| 46 | Cold Brew Cam Mật Ong | `cold_brew_cam_mat_ong.jpeg` |
| 47 | Caramel Coffee Latte | `caramel_coffee_latte.jpeg` |

---

## 📁 Category 8: UTE Dessert & More (dessert/)

| ID | Tên món | Tên file |
|----|---------|----------|
| 48 | Sữa Tươi Kem Trứng Cháy | `sua_tuoi_kem_trung_chay.jpeg` |
| 49 | Trà Sữa Phô Mai Kem Trứng | `tra_sua_pho_mai_kem_trung.jpeg` |

---

## 🔗 URL Pattern

Khi upload lên server, URL sẽ có dạng:

```
http://localhost:8080/assets/drinks/{category}/{filename}
```

Ví dụ:
- `http://localhost:8080/assets/drinks/milk_tea/ute_houjicha_classic.jpeg`
- `http://localhost:8080/assets/drinks/fruit_tea/tra_dao_hong_ute.jpeg`
- `http://localhost:8080/assets/drinks/coffee/cold_brew_cam_mat_ong.jpeg`

---

## 📝 Lưu ý

1. **Tất cả file phải có định dạng `.jpeg`** (không phải .jpg)
2. **Tên file không dấu, viết thường, dùng underscore (_)**
3. **Nếu thiếu ảnh, có thể dùng ảnh placeholder tạm**
4. **Hiện tại đang dùng URL từ GitHub:** `https://raw.githubusercontent.com/vanity1412/UTEtea-img/main/matcha.jpeg`

---

## 🎨 Placeholder Image

Nếu chưa có ảnh thật, có thể tạo placeholder bằng cách:

1. Dùng ảnh mặc định: `placeholder.jpeg`
2. Hoặc dùng service online: `https://via.placeholder.com/400x400.jpeg?text=UTE+Tea`
3. Hoặc giữ nguyên URL GitHub hiện tại

---

**Tổng số món:** 23 món  
**Tổng số ảnh cần:** 23 files .jpeg
