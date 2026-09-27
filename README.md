# Proelium Fatale Cutscene — OwlBear Rodeo Eklentisi

Bir tusa basildiginda tum oyunculara tam ekran, fade-in/fade-out ile
oynayan bir cutscene videosu gosteren OwlBear Rodeo eklentisi.

## Nasil calisir

- `action.html` → GM'in gordugu toolbar butonu (popover). Tiklanince
  `OBR.broadcast.sendMessage` ile odadaki herkese (kendisi dahil) mesaj yollar.
- `background.html` → her oyuncunun tarayicisinda sessizce yuklenir, bu
  mesaji dinler ve `OBR.modal.open({ fullScreen: true, ... })` ile
  tam ekran video modalini acar.
- `video.html` → modal'in icerigi. Video baslarken fade-in yapar, video
  `ended` event'i tetiklendiginde fade-out yapip modali kapatir ve
  oyuncuyu otomatik olarak sahneye geri dondurur.

## 1. Video dosyani ekle

`public/` klasorune kendi sahip oldugun `cutscene.mp4` dosyasini koy
(dosya adi tam olarak `cutscene.mp4` olmali, farkli isim kullanirsan
`video.html` icindeki `src="/cutscene.mp4"` satirini guncelle).

> Not: "Proelium Fatale" ekran karti Limbus Company oyununa ait telifli
> bir gorseldir. Bu dosyayi kendi satin aldigin/sahip oldugun kopyadan,
> kendi masan icin kisisel kullanim amaciyla cikarman gerekiyor — bu
> repo veya ben bu dosyayi saglamiyoruz.

## 2. Bir yerde barindir (hosting)

OwlBear Rodeo, eklentini bir URL uzerinden yukler; bu yuzden
`public/` klasorunu internete acik bir adreste barindirman lazim.
En kolay ucretsiz seçenekler:

- **GitHub Pages**: Bu klasoru bir GitHub reposuna yukle, repo
  ayarlarindan Pages'i `public/` (veya root) klasorunden yayinla.
  (mp4 dosyasi ~100MB altinda kalmali)
- **Cloudflare Pages** veya **Netlify**: `public/` klasorunu surukle-birak
  ile deploy edebilirsin (drag & drop deploy), hesap bile gerektirmez.

Yayinladiktan sonra elinde su formatta bir adres olacak, orn:
`https://kullaniciadi.github.io/owlbear-cutscene/manifest.json`

## 3. OwlBear Rodeo'ya ekle

1. Bir odaya gir.
2. Sol ustteki eklenti (puzzle parcasi) ikonuna tikla → **"Add Custom Extension"**.
3. Yukaridaki `manifest.json` URL'ini yapistir.
4. Eklenti yuklendikten sonra toolbar'da "Proelium Fatale" butonu belirir.
   Bu butona GM (veya odadaki herkes, izin verdiysen) tikladiginda
   video tum oyunculara tam ekran oynar.

## Ozellestirme fikirleri

- `video.html` icindeki `transition: opacity 900ms` degerini degistirerek
  fade suresini ayarlayabilirsin.
- 15 saniyelik "guvenlik agi" timeout'unu videonun gercek suresine gore
  degistirebilir/kaldirabilirsin.
- Sadece GM'in tetikleyebilmesini istiyorsan (oyuncularin action
  butonunu gormemesi icin) manifest'e `permissions` yerine action
  gorunurlugunu OBR.player rolune gore kontrol eden bir kontrol
  ekleyebiliriz — istersen bunu da ekleyebilirim.
