# d187-conf

S2 Son Silah (District 187) özel sunucusunun **launcher güncelleme deposu**.

Oyuncular `LauncherApp.exe`'yi açtığında buradaki dosyaları kontrol eder,
değişenleri indirir ve oyunu başlatır.

## İçerik

| dosya | ne işe yarar |
|---|---|
| `files.json` | dağıtılan dosyaların listesi + SHA-256 + boyut |
| `files/` | dosyaların kendisi (oyun klasörüne göre aynı yapıda) |
| `args` | `TheRaw.exe` komut satırı — sunucu IP'si burada |
| `news.json` | launcher penceresinde görünen duyurular |
| `.gitattributes` | `* -text` — satır sonu dönüşümünü kapatır |

## Neden `.gitattributes` şart

Dosyaların SHA-256'sı `files.json`'da yazılı. Git satır sonlarını dönüştürürse
(Windows'ta varsayılan davranış) indirilen dosya bu hash'i tutturamaz ve
launcher aynı dosyayı sonsuza kadar indirmeye çalışır. `* -text` bunu engeller.

## Güncelleme

Depo elle düzenlenmez. Sunucu tarafındaki `yayinla.bat` çalıştırılır:
manifesti yeniden üretir, dosyaları kopyalar, commit + push eder.

## Notlar

- Depo **public** olmak zorunda — `raw.githubusercontent.com` kimlik doğrulamaz.
- Oyunun 984 MB'lık `Game.ResDt` arşivi burada **yok**; GitHub'ın 100 MB dosya
  sınırını aşıyor. Oyuncular ana kurulumu bir kez ayrı indiriyor.
- `Update_2.ResDt` 68 MB olduğu için GitHub her push'ta "50 MB üstü" uyarısı
  verir. Zararsızdır.
