# 🛍️ Hepsiburada Mobil Test Otomasyonu

Hepsiburada Android uygulaması için Maestro framework kullanılarak geliştirilmiş end-to-end test otomasyonu projesi.

## 📋 Proje Hakkında

Bu proje, Hepsiburada mobil uygulamasında ürün arama, filtreleme ve sepete ekleme akışını otomatize eden test senaryolarını içerir.

### Test Senaryosu Akışı

1. Hepsiburada ana sayfası açılır
2. Arama alanına “Adidas ayakkabı” yazılır ve arama yapılır
3. Ürün listeleme sayfasının başarılı şekilde açıldığı doğrulanır
4. Filtreler alanına girilir
5. Aşağıdaki filtreler uygulanır:
  ○ Cinsiyet: Erkek
  ○ Renk: Beyaz
  ○ Numara: 42
  ○ Fiyat Aralığı: 3.000 TL – 5.000 TL
6. Filtrelerin doğru şekilde uygulandığı ve sonuçların güncellendiği doğrulanır
7. Listelenen ürünlerin seçilen filtre kriterlerine uygun olduğu kontrol edilir
8. Listeleme ekranında yer alan ürünlerden herhangi biri seçilir
9. Ürün detay sayfasında “Sepete Ekle” butonuna tıklanır
10. Kullanıcı login olmadan sepete yönlendirilir
11. Sepet sayfasında:
  ○ Eklenen ürünün sepette yer aldığı
  ○ Ürün adının, fiyatının ve temel bilgilerinin görüntülendiği
  doğrulanır

## 🛠️ Teknolojiler

- **Test Framework:** Maestro
- **Platform:** Android
- **Uygulama:** Hepsiburada (com.pozitron.hepsiburada)
- **Dil:** YAML
- **Tasarım Deseni:** Page Object Model (POM)

## 📁 Proje Yapısı
```
mobil-test/
├── flows/
│   └── search-test.yaml              # Ana test senaryosu
│
├── screens/
│   ├── home.yaml              # Adım 1: Ana sayfa
│   ├── search.yaml            # Adım 2-3: Arama
│   ├── filter.yaml            # Adım 4-5-6: Filtreler
│   ├── search-results.yaml    # Adım 7: Liste validasyonu
│   ├── product-detail.yaml    # Adım 8-9: Ürün detay
│   └── cart.yaml              # Adım 10-11: Sepet
│
└── README.md
```

## 🚀 Kurulum

### Gereksinimler

- [Maestro](https://maestro.mobile.dev/) (v1.x+)
- Android Emulator veya fiziksel cihaz
- Hepsiburada uygulaması yüklü

### Maestro Kurulumu
```bash
# macOS/Linux
curl -Ls "https://get.maestro.mobile.dev" | bash

# Homebrew
brew tap mobile-dev-inc/tap
brew install maestro
```

### Proje Kurulumu
```bash
# Projeyi klonlayın
git clone <repo-url>
cd mobil-test

# Cihaz/Emulator bağlantısını kontrol edin
adb devices
```

## ▶️ Testleri Çalıştırma

### Ana Test Senaryosunu Çalıştırma
```bash
maestro test flows/search-test.yaml
```

### Tek Bir Screen Testi Çalıştırma
```bash
maestro test screens/filter-screen.yaml
```

### Debug Modu ile Çalıştırma
```bash
maestro test --debug flows/search-test.yaml
```

### Maestro Studio ile İnceleme
```bash
maestro studio
```

## 📝 Test Detayları

### Uygulanan Filtreler

| Filtre | Değer |
|--------|-------|
| Cinsiyet | Erkek |
| Renk | Beyaz |
| Numara | 42 |
| Fiyat Aralığı | 3.000 - 5.000 TL |

### Doğrulama Kontrolleri

#### Pozitif Kontroller (Happy Path)
- ✅ Adidas markası görünür
- ✅ Fiyat 3000-5000 TL arasında
- ✅ Erkek ürünleri
- ✅ Beyaz renk

#### Negatif Kontroller
- ❌ Nike markası görünmemeli
- ❌ Kadın ürünleri görünmemeli
- ❌ Siyah renk görünmemeli

## 🎯 Page Object Model Yapısı

Her screen dosyası, ilgili ekranın işlemlerini ve doğrulamalarını içerir:
```yaml
# Örnek: filter-screen.yaml
appId: com.pozitron.hepsiburada
---
- tapOn: Filtrele
- tapOn: Erkek
- tapOn: Uygula
```

## 🐛 Hata Ayıklama

### Element Bulunamıyor
```bash
# Maestro Studio ile elementleri incele
maestro studio
```

### Test Başarısız Oluyor
```bash
# Debug modu ile detaylı log
maestro test --debug flows/search-test.yaml
```

### Uygulama Açılmıyor
```bash
# Uygulama paket adını kontrol et
adb shell pm list packages | grep hepsi
```

## 📊 Test Sonuçları

Test tamamlandığında:
- ✅ Tüm adımlar başarılı: Test PASSED
- ❌ Herhangi bir adım başarısız: Test FAILED

## 🤝 Katkıda Bulunma

1. Fork yapın
2. Feature branch oluşturun (`git checkout -b feature/yeni-ozellik`)
3. Commit yapın (`git commit -m 'Yeni özellik eklendi'`)
4. Push yapın (`git push origin feature/yeni-ozellik`)
5. Pull Request açın