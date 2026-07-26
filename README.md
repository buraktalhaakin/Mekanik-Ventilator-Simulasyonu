# 🫁 Mekanik Ventilasyon Simülatörü

İnteraktif, tarayıcıda çalışan bir **mekanik ventilasyon eğitim simülatörü**. Ventilatör ayarlarını değiştirdikçe hasta, gerçek fizyolojiye dayalı bir modele göre — zaman sabitleriyle, kademeli olarak — iyiye ya da kötüye gider. Yoğun bakım, anestezi, göğüs hastalıkları ve acil tıp eğitiminde ventilatör yönetimi pratiği için tasarlanmıştır.

![Tek dosya](https://img.shields.io/badge/tek%20dosya-HTML-2dd4bf) ![Bağımlılık yok](https://img.shields.io/badge/ba%C4%9F%C4%B1ml%C4%B1l%C4%B1k-yok-37d99a) ![Vanilla JS](https://img.shields.io/badge/vanilla-JS%20%2B%20Canvas-f7b733) ![Lisans](https://img.shields.io/badge/lisans-MIT-25c3f0)

> ⚕️ **Sorumluluk reddi:** Bu bir **eğitim/simülasyon aracıdır**. Fizyoloji modeli öğretim amacıyla basitleştirilmiştir; gerçek klinik karar, tanı, tedavi veya hasta yönetimi için **kullanılamaz**.

---

## ✨ Özellikler

### Klinik senaryolar (her açılışta rastgele, çeşitli)
Her açılış ve **"Sıfırla"da farklı bir hasta** oluşur: rastgele isim, yaş, cinsiyet, boy, hastalık şiddeti ve buna uygun randomize vaka öyküsü + giriş kan gazı. 7 klinik tablo:

- **ARDS** — ağır hipoksemi, düşük kompliyans, yüksek şant
- **KOAH atağı** — hava hapsi, oto-PEEP, kronik CO₂ retansiyonu
- **Status astmatikus** — ağır bronkospazm, dinamik hiperinflasyon
- **Kardiyojenik pulmoner ödem** — PEEP'e iyi yanıt, ard yük
- **Ağır pnömoni / orta ARDS**
- **Nöromusküler solunum yetmezliği (Guillain-Barré)** — akciğer sağlam, solunum pompası zayıf, zorlu weaning
- **Postop / sağlıklı akciğer** — kısa süreli ventilasyon

### Ventilasyon modları
`VC-AC` · `PC-AC` · `Basınç Desteği (PS)` · `SIMV+PS` · `CPAP / SBT`
— ayarlanabilir FiO₂, PEEP, tidal volüm / inspiratuvar basınç, solunum sayısı, İ:E oranı, tetik hassasiyeti.

### Gerçek zamanlı monitör
- Canlı **basınç–akım–volüm** dalga formları + **kapnografi** (obstrüksiyonda shark-fin morfolojisi)
- Sürekli **SpO₂, etCO₂, nabız, kan basıncı** ve mekanik değerler (PIP, ΔP, Vte, toplam SS, oto-PEEP, direnç, solunum dürtüsü)
- **Alarm sesi** — hasta instabil olduğunda çalar (uyarı/kritik tonları)
- Her monitör değerinin üstüne gelince **"nasıl değiştirilir" ipucu**

### Fizyoloji motoru
- **Gaz kinetiği:** değerler anında değil, gerçekteki gibi zaman sabitleriyle oturur (FiO₂ → SpO₂ dakikalar içinde; ventilasyon → PaCO₂ daha yavaş)
- **Oksijenasyon:** şant fraksiyonu, alveolo-arteriyel gradient, PEEP ile **rekrütman histerezisi** (açılma yavaş, kollaps hızlı)
- **PEEP–kompliyans ilişkisi (best-PEEP U-eğrisi):** optimal PEEP'te kompliyans maksimum, altında derekrütman, üstünde overdistansiyon
- **Non-lineer basınç–volüm** (üst bükülme noktası / overdistansiyon)
- **Oto-PEEP / hava hapsi**, aşırı distansiyon → ölü boşluk artışı
- **Asit-baz:** Henderson-Hasselbalch, renal kompanzasyon, laktik metabolik asidoz
- **Hemodinamik eşlenme:** yüksek PEEP → venöz dönüş↓, obstrüktif şok, vazopresör/sıvı yanıtı
- **Sedasyon & paralizi:** solunum dürtüsü + **metabolik hız (VCO₂/VO₂)** + hemodinami üzerinde gerçekçi etki; paralizi solunum kası işini kaldırıp oksijenasyonu düzeltir, **P-SILI**'yi (hasta kaynaklı akciğer hasarı) önler
- **Hasta–ventilatör uyumsuzluğu (dissenkroni)** ve solunum pompası gücü (nöromusküler)

### Otomatik komplikasyonlar
Manuel değil — **klinik seyre veya zararlı ayarlara (iyatrojenik)** bağlı kendiliğinden gelişir: pnömotoraks (barotravma, oturum başına en fazla bir kez), bronkospazm, sekresyon tıkacı, ajitasyon.

### Yatak başı müdahaleler
Prone pozisyon · bronkodilatör · aspirasyon · sıvı bolüsü · göğüs tüpü · **dozaj seçmeli vazopresör** (noradrenalin infüzyonu) · sedasyon (RASS) · nöromusküler blokaj.

### Weaning / SBT
Spontan solunum denemesi başlatma, **canlı ekstübasyon kriterleri** (spontan çaba, RSBI, SpO₂/FiO₂/PEEP, pH, hemodinami) ve ekstübasyon değerlendirmesi.

### Değerlendirme
- İstenildiğinde **gecikmeli arteriyel kan gazı** (pH, PaCO₂, PaO₂, HCO₃, baz açığı, laktat, P/F)
- **Debrief karnesi:** alan skorları (oksijenasyon, ventilasyon, akciğer koruma/VILI, hemodinami, güvenlik, weaning), ayrıntılı ölçümler (hedefte kalma süreleri, VILI dozu, mekanik güç), ARDSnet PEEP/FiO₂ merdiveni ve kişiye özel notlar

---

## 🚀 Kullanım

### Doğrudan çalıştırma
`ventilator.html` dosyasını indirip **çift tıklayarak tarayıcıda açman yeterli**. Kurulum, sunucu, internet bağlantısı gerekmez.

### Web sitesine gömme (iframe)
Dosyayı bir web sunucusuna yükledikten sonra:

```html
<iframe
  src="/ventilator.html"
  title="Mekanik Ventilasyon Simülatörü"
  loading="lazy"
  allow="autoplay"
  style="width:100%; height:90vh; min-height:1000px; border:0; border-radius:12px;">
</iframe>
```

### Canlı demo (GitHub Pages)
Depoyu GitHub'a yükledikten sonra **Settings → Pages** bölümünden yayınlayarak ücretsiz canlı bir demo elde edebilirsin:
`https://<kullanıcı-adı>.github.io/<depo-adı>/ventilator.html`

---

## 🎯 Nasıl oynanır?

1. Sağ üstteki **vaka sunumunu** oku (öykü, komorbidite, entübasyon nedeni, giriş kan gazı, hedef).
2. Ventilatör ayarlarını (mod, FiO₂, PEEP, Vt, SS…) titre ederek oksijenasyonu ve ventilasyonu düzelt, akciğeri koru (ΔP < 15, plato < 30, ~6 mL/kg).
3. Gerekirse **kan gazı al**, hastanın solunum çabasıyla uyumu sağla, komplikasyonları yatak başı müdahalelerle yönet.
4. Hasta stabilleşince **SBT** başlat ve kriterler karşılanınca **ekstübe et**.
5. **Debrief karnesiyle** performansını değerlendir. **"Sıfırla"** ile yeni bir hasta al.

> İpucu: Monitördeki her değerin üstüne fareyle gelirsen o değeri hangi ayarla nasıl değiştireceğini gösteren bir ipucu açılır.

---

## 🛠️ Teknik

- **Tek dosya, sıfır bağımlılık.** Tüm CSS ve JavaScript `ventilator.html` içine gömülüdür; harici font, kütüphane, CDN veya ağ isteği yoktur.
- Saf (vanilla) JavaScript + HTML5 **Canvas** (dalga formları, trend, kapnografi).
- Karanlık, yoğun bakım monitörü estetiğinde arayüz; responsive (masaüstü/tablet/mobil).
- Fizyoloji, gerçek zamanlı bir `requestAnimationFrame` döngüsünde çözülür; kare hatalarına karşı korumalıdır.

---

## 📁 Depo yapısı

```
.
├── ventilator.html   # Simülatörün tamamı (tek dosya)
└── README.md
```

---

## 🤝 Katkı

Öneri, hata bildirimi ve geliştirme katkıları için Issues / Pull Request açabilirsiniz. Özellikle klinik doğruluk geri bildirimleri değerlidir.

## 📄 Lisans

MIT — dilediğiniz gibi kullanabilir, değiştirebilir ve dağıtabilirsiniz. Ayrıntı için `LICENSE` dosyasına bakın.

---

*Bu simülatör eğitim amaçlıdır ve gerçek hasta bakımında kullanılamaz.*
