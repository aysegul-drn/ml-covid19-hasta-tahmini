
# COVID-19 Hasta Durumu Tahminleme Projesi

## 📝 Proje Açıklaması
Bu proje, makine öğrenmesi algoritmalarını kullanarak bir kişinin klinik bulgularına, semptomlarına ve kronik hastalık geçmişine dayanarak COVID-19 risk durumunu tahmin etmeyi amaçlamaktadır. Proje kapsamında veri temizleme, keşifsel veri analizi (EDA) ve farklı sınıflandırma modellerinin karşılaştırılması süreçleri uçtan uca uygulanmıştır.

## 📊 Veri Seti Tanıtımı
Projede Meksika Sağlık Bakanlığı tarafından sağlanan **COVID-19 Patient Beginner Dataset** kullanılmıştır.
* **Veri Seti Linki:** [Kaggle - COVID-19 Dataset](https://www.kaggle.com/datasets/meirnizri/covid19-dataset)
* **Özellikler:** Veri seti yaş, cinsiyet, pnömoni, diyabet, astım, hipertansiyon ve tütün kullanımı gibi 20'den fazla klinik parametre içermektedir.

## 🛠 Veri Ön İşleme Adımları
1.  **Geçersiz Değerlerin Temizlenmesi:** Veri setinde "bilinmiyor" anlamına gelen maskelenmiş değerler (97, 98, 99) `NaN` olarak işaretlenmiş ve veri setinden çıkarılmıştır.
2.  **Hedef Değişken Oluşturma:** `CLASIFFICATION_FINAL` sütunu baz alınarak; 1, 2 ve 3 değerleri "Pozitif (1)", diğer değerler "Negatif (0)" olacak şekilde ikili sınıflandırmaya (binary classification) dönüştürülmüştür.
3.  **Gereksiz Sütunların Kaldırılması:** Tahminleme sürecine doğrudan etkisi olmayan `DATE_DIED` gibi sütunlar veri setinden düşürülmüştür.
4.  **Veri Bölme:** Veri seti %80 eğitim ve %20 test olacak şekilde ayrılmıştır.

## 🤖 Kullanılan Algoritmalar ve Mantığı
* **Logistic Regression:** Bağımlı ve bağımsız değişkenler arasındaki ilişkiyi bir sigmoid fonksiyonu kullanarak olasılıksal olarak modeller. Temel bir sınıflandırıcı olarak kullanılmıştır.
* **Random Forest:** Birden fazla karar ağacının (Decision Tree) birleşmesiyle oluşan bir topluluk öğrenmesi (ensemble) yöntemidir. Aşırı öğrenmeyi (overfitting) engelleyerek daha genel geçer sonuçlar üretir.
* **Decision Tree:** Veriyi belirli sorular sorarak dallara ayıran ve en son yaprak düğümlerde sınıflandırma yapan ağaç tabanlı bir yapıdır.
* **KNN (K-Nearest Neighbors):** Yeni bir veriyi, ona en yakın olan K sayıdaki komşusunun sınıfına göre atayan mesafe tabanlı bir algoritmadır.

## 📈 Model Performans Karşılaştırması
Aşağıdaki sonuçlar test veri seti üzerinden elde edilmiştir:

Algoritma,Accuracy,Precision (Pozitif),Recall (Pozitif),F1-Score
Logistic Regression,%62.37,%63.00,%72.21,%67.29
Random Forest,%59.32,%61.25,%65.64,%63.37
Decision Tree,%57.89,%60.87,%60.05,%60.45
KNN,%57.30,%59.60,%63.15,%61.33

## 💡 Sonuç ve Yorumlar
* Yapılan testler sonucunda en yüksek doğruluk oranına **Random Forest** algoritması ile ulaşılmıştır.
* Modelin sağlık sektöründe kullanılması durumunda **Recall (Duyarlılık)** oranının yüksek olması, hasta bireylerin gözden kaçırılmaması adına kritik önem taşımaktadır.
* Yaş ve Pnömoni bulgularının, COVID-19 pozitifliği üzerinde en belirleyici özellikler olduğu gözlemlenmiştir.

## 🚀 Kodların Nasıl Çalıştırılacağı
1.  Bu depoyu bilgisayarınıza clone'layın: `git clone https://github.com/kullaniciadi/ml-covid19-hasta-tahmini.git`
2.  Gerekli kütüphaneleri yükleyin: `pip install pandas numpy scikit-learn seaborn matplotlib`
3.  Veri setini Kaggle üzerinden indirip ana dizine `Covid Data.csv` adıyla ekleyin.
4.  `covid_prediction.ipynb` dosyasını Jupyter Notebook veya Google Colab üzerinde çalıştırın.

---

**Hazırlayan:** Ayşegül Duran  
**Öğrenci No:** 25019921045
**Üniversite:** Bartın Üniversitesi - Yapay Zeka Operatörlüğü
