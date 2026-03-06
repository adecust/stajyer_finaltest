# Stajyer Değerlendirme Paneli (Web, backend yok)

## Çalıştırma
```bash
python -m http.server 8000
```
Sonra: http://localhost:8000

## Google OAuth ayarı
- Google Cloud > Credentials > OAuth Client (Web)
- Authorized JavaScript origins:
  - http://localhost:8000
- OAuth Consent Screen > Test users: kendi Gmail adresini ekle

## Drive Klasörü
`DRIVE_FOLDER_ID` index.html içinde ayarlı.
Klasördeki dönem dosyaları Google Sheet olmalı (xlsx seçilemez).

## Rol akışı
- ADMIN / SUPERVISOR: Ana Sayfa + Yorum Yap menüsü
- UZMAN / HOSTEL_UZMANI: sadece Yorum Yap sayfası

## Kutular
Yorum Yap sayfasında:
- Kırmızı: bu ay kullanıcı henüz kaydetmemiş
- Yeşil: kaydetmiş (tıklayıp güncelleyebilir)


## 2026-02 Fixes
- Yorum kaydetme/güncelleme düzeltildi (upsert parametreleri, email/rol, dönem eşleşmesi).
- Değerlendirme güncellemede range genişliği header uzunluğuna göre ayarlandı.


## Yorum Tarihi / İzinli Günler (Takvim)
Yorum yapma ekranında **tarih seçimi** vardır. Seçilen tarih, Google Sheet içindeki **Takvim** sekmesinden kontrol edilir.

Takvim sekmesine şu kolonları ekleyin:
- **YorumIzinliRoller**: O tarihte yorum yapabilecek roller (örn: `UZMAN`, `PROJE_UZMANI`, `SUPERVISOR`, `ADMIN`, `ALL`). Birden fazla ise virgülle: `UZMAN, PROJE_UZMANI`
- **YorumIzinliGruplar** (opsiyonel): Sadece belirli grup(lar) için açmak isterseniz `GrupID` değerlerini yazın (virgülle).
- **YorumIzin** (opsiyonel): Boş veya `Evet` → açık. `Hayır` / `0` → kapalı.

Not: Bu kolonlar yoksa sistem güvenlik için **yorum kaydetmeyi kapatır** ve uyarı gösterir.
