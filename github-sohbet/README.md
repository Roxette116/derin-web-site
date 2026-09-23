# DERİN — GitHub Pages sohbet sitesi

Bu paket GitHub Pages'e doğrudan yüklenebilir. Node.js, npm veya derleme adımı yoktur. Ana sayfa `index.html`'dir.

## GitHub Pages'te yayımla

1. ZIP'i bilgisayarında çıkar.
2. GitHub'da yeni bir depo oluştur. GitHub Free kullanıyorsan depo görünürlüğünü **Public** seç.
3. Depoda **Add file → Upload files**'a tıkla.
4. ZIP'ten çıkan `github-sohbet` klasörünün *içindeki tüm dosya ve klasörleri* yükle. Depo kökünde `index.html`, `firestore.rules` ve `src/` görünmeli. `index.html` başka klasörün içine gömülü kalmamalı.
5. **Commit changes**'e bas.
6. Depoda **Settings → Pages → Build and deployment** bölümünde **Deploy from a branch** seç. Branch olarak `main`, klasör olarak `/(root)` seçip **Save**'e bas.
7. Birkaç dakika sonra aynı Pages ekranındaki bağlantıya tıklayarak siteyi aç.

## Mesajlaşma, Google girişi ve görüşmeleri etkinleştir

GitHub Pages yalnızca site dosyalarını barındırır; kullanıcı girişi, mesajların eşitlenmesi ve arama sinyalleri Firebase üzerinden çalışır. Firebase bağlantısı olmadan sayfa kurulum yönergesini gösterir.

1. [Firebase Console](https://console.firebase.google.com/) içinde proje oluştur ve web uygulaması ekle.
2. **Authentication → Sign-in method** bölümünde **Google** sağlayıcısını aç.
3. **Firestore Database** oluştur.
4. Firebase web uygulamasının config değerlerini `src/firebase-config.js` dosyasındaki `YOUR_...` değerlerinin yerine yapıştır. Dosyada her bir alan kendi satırında gösterilmiştir.
5. Firebase Console → **Firestore Database → Rules** bölümüne `firestore.rules` dosyasının tamamını yapıştırıp **Publish**'e bas.
6. Firebase Console → **Authentication → Settings → Authorized domains** içine GitHub Pages alan adını ekle. Örnek: `ahmet.github.io` (depo adını değil, alan adını yaz).
7. `src/firebase-config.js` ve gerekiyorsa kurallardaki değişiklikleri GitHub'a commit et. Pages yeni sürümü kendiliğinden yayınlar.

Sonra sen ve arkadaşın siteyi açıp farklı Google hesaplarıyla giriş yapın. Kullanıcılar birbirlerinin kişi listesinde görünür; mesaj ve arama bu hesaplardaki kullanıcılar arasında çalışır. Tarayıcı, arama sırasında mikrofon/kamera izni ister. Görüşme için HTTPS veya localhost gereklidir.

## Dosyalar

- `index.html`: Sitenin giriş sayfası.
- `src/main.js`: Google oturumu, kişi listesi, canlı mesajlaşma, arama ve WebRTC çağrı kodu.
- `src/firebase-config.js`: Firebase web ayarlarını gireceğin dosya. Bu değerler Firebase web uygulamalarında publictir; Firestore güvenliğini `firestore.rules` sağlar.
- `src/firebase.js`: Firebase SDK bağlantısı. SDK modülleri Firebase'in CDN'inden alınır.
- `src/style.css`: Arayüz ve mobil tasarım.
- `firestore.rules`: Sohbet ve çağrı verilerinin erişim kuralları.

Varsayılan STUN sunucuları bazı ağlarda yeterli olmaz. Kurumsal ağ veya sıkı NAT durumlarında sesli/görüntülü arama için ayrıca TURN sunucusu yapılandırılmalıdır.
