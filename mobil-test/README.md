# Hepsiburada Mobil Test Otomasyonu

Maestro ile Hepsiburada Android uygulaması için e2e test otomasyonu.

## Test Akışı

Adidas ayakkabı arama → Filtreleme (Beden:42, Fiyat:3000-5000TL, Cinsiyet:Erkek, Renk:Beyaz) → Ürün seçimi → Sepete ekleme → Sepet kontrolü

## Kurulum
```bash
brew tap mobile-dev-inc/tap
brew install maestro
```

## Çalıştırma
```bash
maestro test flows/search-test.yaml
```

## Dosya Yapısı
```
mobil-test/
├── flows/search-test.yaml        # Ana test
└── screens/                      # POM yapısı
    ├── home-screen.yaml
    ├── search-screen.yaml
    ├── filter-screen.yaml
    ├── search-results-screen.yaml
    ├── product-detail-screen.yaml
    └── cart-screen.yaml
└── tests/ 
    ├── hepsiburada-e2e-test.yaml
```

## Notlar
- Maestro Türkçe karakter desteklemiyor ("ayakkabi" yerine "ayakkabı")
- Bazı elementler ID'siz, koordinat kullanıldı
- Happy path + negatif testler (Nike, Kadın, Siyah olmamalı)