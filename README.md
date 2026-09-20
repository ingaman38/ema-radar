# Binance EMA 52/320 Radar — iPhone Standalone

Bu sürümde backend/PC yoktur. HTTPS üzerinde statik olarak yayınlanan `index.html`, Binance public market-data API'sinden veriyi doğrudan Safari ile çeker ve EMA/ATR hesaplarını iPhone üzerinde yapar.

## Tarama mantığı
- Binance Spot USDT çiftleri
- 24 saatlik quoteVolume'a göre Top 50/100/150
- Her sembol için 1h, 600 mum
- EMA52, EMA320, Wilder ATR14
- Varsayılan yön: yukarı kesişim
- EMA52 < EMA320 olmalı
- Son 6 saatte gap kapanmalı
- EMA52 son 6 saatte yükselmeli
- Son 12 saatin tamamında EMA52 <= EMA320 olmalı (yakın zamanda yukarıdayken düşüp yeniden kesme gürültüsünü azaltır)
- 0.10 / 0.25 / 0.50 / 1.00 ATR yakınlık filtresi
- Sabit/fiat ve kaldıraçlı token çiftleri varsayılan olarak dışarıda

## iPhone'da kalıcı kullanım
Dosyaları HTTPS veren herhangi bir statik hosta yükle. GitHub Pages, Cloudflare Pages, Netlify veya benzeri yeterlidir. Sunucu kodu gerekmez.

GitHub Pages örneği:
1. Bu klasördeki dosyaları bir GitHub repository'sinin köküne yükle.
2. Repository > Settings > Pages.
3. Deploy from a branch > main / root seç.
4. Oluşan HTTPS adresini iPhone Safari'de aç.
5. Paylaş > Ana Ekrana Ekle.

## Not
İlk tarama yaklaşık 100 ayrı kline isteği yapar. Arayüz bunları 6'lı paralellik ile kontrollü gönderir ve 429/5xx hatalarında geri çekilip tekrar dener.
