# CST Studio Suite ile X-Band WR90 Magic Tee Tasarımı ve Optimize Edilmesi

Bu proje, X-Band frekans aralığında (8.0 - 12.0 GHz) çalışan, WR90 standardına dayalı 4-portlu pasif bir mikrodalga devre elemanı olan **Magic Tee (180° Hibrit Eklem)** yapısının teorik analizini, 3D elektromanyetik modellenmesini ve optimizasyon süreçlerini içermektedir.

Geleneksel boş dalga kılavuzu kesişimlerinde meydana gelen ciddi empedans uyumsuzluklarını ve sinyal geri dönüş kayıplarını önlemek amacıyla, merkez bağlantı noktasına **Çok Basamaklı İletken Koni (Multi-Stepped Conducting Cone)** entegre edilerek geniş bantlı bir empedans transformatörü tasarlanmıştır.

---

## 🛠️ Tasarım Parametreleri ve Geometri

- **Dalga Kılavuzu Standardı:** WR90 ($a = 22.86 \text{ mm}$, $b = 10.16 \text{ mm}$, Et kalınlığı $= 1.27 \text{ mm}$)
- **Çalışma Frekansı:** 8.0 - 12.0 GHz (X-Band)
- **Arka Plan Malzemesi:** Vakum (Hollow Waveguide)
- **Simülasyon Ortamı:** CST Studio Suite

### Port Konfigürasyonu
- **Port 1 (H-Düzlemi Kolu):** Toplam (Sum - $\Sigma$) Portu
- **Port 4 (E-Düzlemi Kolu):** Fark (Difference - $\Delta$) Portu
- **Port 2 & Port 3:** Eş Doğrusal (Collinear) Yan Kollar

---

## 📐 Teorik Altyapı ve İdeal S-Matrisi

Kayıpsız, karşılıklı (reciprocal) ve tüm portları mükemmel uydurulmuş ideal bir Magic Tee için saçılma matrisi ($S$-matrix) şu şekilde formüle edilmiştir:

$$[S] = \frac{1}{\sqrt{2}} \begin{bmatrix} 0 & 1 & 1 & 0 \\ 1 & 0 & 0 & 1 \\ 1 & 0 & 0 & -1 \\ 0 & 1 & -1 & 0 \end{bmatrix}$$

### Fiziksel Davranış Kriterleri:
1. **Empedans Uydurma (Return Loss):** Tüm portlarda yansımaların minimize edilmesi ($S_{11}, S_{22}, S_{33}, S_{44} < -15 \text{ dB}$).
2. **Port İzolasyonu:** H ve E kollarının geometrik dikliği sayesinde $S_{41} < -90 \text{ dB}$ teorik sonsuz izolasyon; eş doğrusal kollar arasında ise $S_{32} < -20 \text{ dB}$ hedefi.
3. **Güç Bölme Dengesi:** Toplam portundan gelen gücün yan kollara eşit büyüklükte bölünmesi ($|S_{21}| \approx |S_{31}| \approx -3 \text{ dB}$).
4. **Faz Senkronizasyonu:** Sum portu uyarımında $0^{\circ}$ eş-faz, Difference portu uyarımında ise $180^{\circ}$ ters-faz davranışı.

---

## 📊 Simülasyon ve Optimizasyon Sonuçları

### 1. S-Parametre Analizi (Return Loss & Isolation)
- **Geri Dönüş Kaybı:** Tasarlanan basamaklı koni yapısı sayesinde tüm portlarda yansıma katsayıları 9.5 GHz merkez frekansında mükemmel dip noktalarına ulaşmıştır ($S_{11} \approx -33 \text{ dB}$, $S_{22}/S_{33} \approx -43 \text{ dB}$, $S_{44} \approx -29.5 \text{ dB}$).
- **Eş Doğrusal İzolasyon ($S_{32}$):** Merkezdeki koni saçılmaları minimuma indirerek yan kollar arasındaki kuplajı 8.8 GHz civarında $-52 \text{ dB}$ seviyesine kadar bastırmıştır.

### 2. Güç ve Faz Dengesi
- **Genlik Dengesi:** $S_{21}$ ve $S_{31}$ eğrileri tüm bant boyunca tam üst üste binerek **0 dB genlik dengesizliği** (Amplitude Imbalance) sunmuştur. Ekleme kaybı $-3.0$ ile $-3.1 \text{ dB}$ arasında kararlı kalmıştır.
- **Faz Dengesi:** Sum portu uyarımında $\angle S_{21} - \angle S_{31} = 0^{\circ}$ tam eş-faz doğruluğu; Difference portunda ise paralel faz gecikmesiyle tam $\pm180^{\circ}$ polarite terslemesi (Anti-Symmetry) doğrulanmıştır.

---

## 👁️ 3D Elektromanyetik Alan ve Enerji Akış İzleme

Proje kapsamında sadece matematiksel verilerle yetinilmemiş, CST 3D alan monitörleri ile dalga dinamiği doğrulanmıştır:

* **E-Alan (Elektrik Alan) Vektörleri:** Baskın $TE_{10}$ modunun Sum portunda eş yönlü, Difference portunda ise metal sınır koşullarından ötürü zıt yönlü (ters-faz) bölünmesi gözlemlenmiştir.
* **H-Alan (Manyetik Alan) Vektörleri:** Dalga kılavuzunun zemin ve tavanına paralel kapalı döngüler oluşturan manyetik alan çizgilerinin, kollar ayrılırken simetrik ve anti-simetrik kıvrılma (curling) mekanizmaları izlenmiştir.
* **Poynting Vektörü ($S = E \times H$):** Makroskobik enerji akış çizgilerinin basamaklı koni etrafından türbülans veya kararlı dalga (standing wave) oluşturmadan pürüzsüzce kayarak yan kollara $-3 \text{ dB}$ bölünmesi ve izole portlara hiç enerji sızmaması görselleştirilmiştir.

