# YAKIN — Google girişli, görüntülü sohbet

Bu ZIP doğrudan GitHub Pages'e yüklenir. Firebase, Node.js, npm veya derleme komutu kullanmaz. İki kişi davet bağlantısıyla bağlanır; canlı mesaj, ses ve görüntü WebRTC ile gönderilir.

## 1) Siteyi GitHub Pages'te yayınla

1. ZIP'i çıkar.
2. GitHub'da yeni depo oluştur.
3. Depoda **Add file → Upload files**'ı seç.
4. `meet-sifirdan` klasörünün **içindeki dosyaları** yükle. Depo ana sayfasında `index.html` ve `src` görünmeli.
5. **Commit changes**'e bas.
6. **Settings → Pages → Build and deployment** altında **Deploy from a branch** seç; branch `main`, klasör `/(root)` olsun ve kaydet.
7. GitHub Pages adresini aç. Yayına çıkması birkaç dakika alabilir.

## 2) Google girişini etkinleştir

Gerçek Google hesabıyla giriş için Google bir Web OAuth Client ID istiyor. Bu Firebase değildir ve şifre istemez.

1. Google Cloud Console'da **APIs & Services → Credentials → Create Credentials → OAuth client ID → Web application** seç.
2. Authorized JavaScript origins bölümüne GitHub Pages alan adını ekle: `https://KULLANICI.github.io` (sona depo yolunu yazma).
3. Client ID'yi kopyala.
4. GitHub'daki `src/config.js` dosyasını aç. `YOUR_GOOGLE_WEB_CLIENT_ID.apps.googleusercontent.com` değerini kendi Client ID'n ile değiştirip commit et.
5. Siteyi yenile. Google giriş düğmesi görünür.

Client ID eklemeden misafir olarak girip bağlantıyı deneyebilirsin.

## 3) Görüş ve mesaj

1. İki kişi de aynı siteyi açıp Google veya misafir girişi yapar.
2. Birinci kişi **Davet bağlantısını kopyala**'ya basıp linki diğer kişiye gönderir.
3. İkinci kişi linki açınca oda kodu otomatik algılanıp bağlanır. İstersen kodu soldaki kutuya elle yazabilirsin.
4. Sohbet alanından canlı mesaj gönder. **Ara** sesli görüşme, **Kamera** görüntülü görüşme başlatır. Tarayıcı mikrofon/kamera izni ister.

## Bilmen gerekenler

- Mesajlar canlı bağlantı üzerinden gider; sohbet geçmişi sunucuda saklanmaz. İki kişi aynı anda çevrimiçi olmalıdır.
- Oda/kişi listesi yoktur; katılımcı davet bağlantısıyla gelir.
- Google girişi bu örnekte tarayıcıda kimlik gösterimi sağlar. Mesajlaşma uygulamasında sunucu olmadığından uygulama düzeyinde hesap/oda yetkilendirmesi yoktur; hassas veya gizli görüşmeler için uygun değildir.
- Bağlantı eşleştirmesi PeerJS'in ortak bulut sunucusunu kullanır. Bazı ağlarda WebRTC araması için TURN sunucusu gerekir.

Google web giriş istemci kimliği gerektirir ([Google Identity Services](https://developers.google.com/identity/gsi/web/guides/get-google-api-clientid)). PeerJS varsayılan olarak ortak PeerServer Cloud eşleştirmesini kullanır ([PeerJS Cloud](https://peerjs.com/server/cloud)).
