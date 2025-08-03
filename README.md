# 🛒 Alışverişçi Davranış Analizi ve Gelir Üzerindeki Etkisi

## 📝 Genel Bakış
Bu proje, bir e-ticaret platformundaki alışverişçi davranış verilerinin analizini sunar. Ana hedef, bir kullanıcı oturumunun satın alma ile sonuçlanıp sonuçlanmayacağını tahmin edebilen makine öğrenmesi modelleri geliştirmektir. Davranışsal kalıpları analiz ederek, şirketlerin kullanıcı deneyimini geliştirmesine, dönüşüm oranlarını artırmasına ve gelirlerini maksimize etmesine yardımcı olacak içgörüler elde edilmiştir.

---

## 📂 Proje İçeriği
- Genel Bakış  
- Veri Seti  
- Proje Metodolojisi  
  - Veri Hazırlama  
  - Keşifsel Veri Analizi (EDA)  
  - Özellik Mühendisliği  
  - Modelleme ve Değerlendirme  
- Model Sonuçları  
- Temel Bulgular ve İçgörüler  
- Eyleme Geçirilebilir Öneriler  
- Proje Nasıl Çalıştırılır  
- Kullanılan Kütüphaneler  

---

## 📊 Veri Seti
Proje, 12,330 kullanıcı oturumunu ve 18 özelliği içeren bir çevrimiçi alışveriş davranış veri setine dayanmaktadır.

### Özellik Açıklamaları

| Özellik              | Açıklama |
|----------------------|----------|
| `YonetimSayfasi`     | Ziyaret edilen yönetim sayfası sayısı |
| `YonetimSuresi`      | Yönetim sayfalarında geçirilen süre (sn) |
| `BilgiSayfasi`       | Bilgi sayfası ziyaret sayısı |
| `BilgiSuresi`        | Bilgi sayfalarında geçirilen süre |
| `UrunSayfasi`        | Ürün sayfası ziyaret sayısı |
| `UrunSuresi`         | Ürün sayfalarında geçirilen süre |
| `HemenCikmaOrani`    | Hemen çıkma oranı |
| `SayfaCikisOrani`    | Sayfa çıkış oranı |
| `SayfaDegeri`        | Ortalama sayfa değeri |
| `OzelGunSkoru`       | Ziyaretin özel güne yakınlık skoru |
| `Ay`                 | Ziyaretin gerçekleştiği ay |
| `IsletimSistemi`     | Kullanıcının işletim sistemi |
| `Tarayici`           | Tarayıcı bilgisi |
| `Bolge`              | Coğrafi bölge |
| `TrafikTuru`         | Trafik kaynağı türü |
| `ZiyaretciTuru`      | Ziyaretçi tipi (`Returning_Visitor` / `New_Visitor`) |
| `HaftaSonu`          | Ziyaret hafta sonu mu? (`True/False`) |
| `SatinAlim`          | Hedef değişken (Satın alma gerçekleşti mi?) |

---

## 🛠️ Proje Metodolojisi

### 1. Veri Hazırlama
- Veri, `Shoppers_Behaviour_and_Revenue.csv` dosyasından yüklendi.  
- Eksik veri kontrolü yapıldı, eksik değer bulunmadı.  
- Sütun isimleri orijinal haliyle bırakıldı.  

### 2. Keşifsel Veri Analizi (EDA)
- Sayısal değişkenler için korelasyon analizi yapıldı.  
- `UrunSuresi` ve `SayfaDegeri`, satın alma ile pozitif korelasyona sahip çıktı.  
- Kategorik değişkenlerde (`ZiyaretciTuru`, `HaftaSonu`) gruplara göre satın alma oranları görselleştirildi.  

### 3. Özellik Mühendisliği
Yeni değişkenler türetildi:
- `ToplamSure`: Tüm sayfa türlerinde geçirilen toplam süre  
- `EtkilesimOrani`: Toplam sayfa sayısı / Toplam süre  
- `ZiyaretciBinary`: 1 = Returning, 0 = New  
- `YuksekDegerliSayfa`: `SayfaDegeri` ortalamanın üstünde mi?  

### 4. Modelleme ve Değerlendirme
Aşağıdaki modeller kullanılarak sınıflandırma yapıldı:
- Logistic Regression  
- Random Forest Classifier  
- XGBoost Classifier  

Kullanılan metrikler:
- Accuracy  
- Precision  
- Recall  
- F1-Score  
- ROC-AUC  

---

## 📈 Model Sonuçları

| Model              | Accuracy | Precision | Recall | F1-Score | ROC-AUC |
|--------------------|----------|-----------|--------|----------|---------|
| Logistic Regression| 0.875    | 0.706     | 0.449  | 0.549    | 0.895   |
| Random Forest      | 0.908    | 0.787     | 0.654  | 0.714    | 0.941   |
| XGBoost            | 0.907    | 0.771     | 0.672  | 0.718    | 0.946   |

> XGBoost, en iyi performansı göstermiştir.

---

## 💡 Temel Bulgular ve İçgörüler
- **Sayfa Değeri Kraldır:** `SayfaDegeri`, satın alma davranışının en güçlü göstergesidir.  
- **Ürünlerle Etkileşim Önemlidir:** `UrunSuresi` arttıkça satın alma olasılığı da artmaktadır.  
- **Müşteri Sadakati:** Geri dönen ziyaretçiler, daha yüksek dönüşüm oranlarına sahiptir.  
- **Zamanlama Etkisi:** Kasım ayında (örneğin Kara Cuma döneminde) en yüksek satın alma oranları gözlemlenmiştir.

---

##  Eyleme Geçirilebilir Öneriler
- **Kritik Sayfaları İyileştirin:** Hemen çıkma oranı yüksek olan sayfaları optimize edin.  
- **Yüksek Değerli Sayfalara Odaklanın:** `SayfaDegeri` yüksek sayfalarda UX iyileştirmeleri yapın.  
- **Sezonluk Kampanyalar:** Özellikle Kasım ayında özel indirimler ve promosyonlar planlayın.  
- **Retargeting Stratejileri:** Ürün sayfalarında vakit geçiren ama satın almayanlara özel kampanyalar.  
- **Dönüşüm Hunisi Optimizasyonu:** Sepet terk oranını azaltmak için hatırlatmalar ve kullanıcı dostu ödeme sistemleri kullanın.

---

