
# COVID-19 Hasta Durumu Tahminleme Projesi

## 📝 Proje Açıklaması
Bu proje, makine öğrenmesi algoritmalarını kullanarak bir kişinin klinik bulgularına, semptomlarına ve kronik hastalık geçmişine dayanarak COVID-19 risk durumunu (Pozitif/Negatif) tahmin etmeyi amaçlamaktadır. Proje kapsamında veri temizleme, keşifsel veri analizi (EDA) ve farklı sınıflandırma modellerinin karşılaştırılması süreçleri uçtan uca uygulanmıştır.

## 📊 Veri Seti Tanıtımı
Projede Meksika Sağlık Bakanlığı tarafından sağlanan **COVID-19 Patient Beginner Dataset** kullanılmıştır.
* **Veri Seti Linki:** [Kaggle - COVID-19 Dataset](https://www.kaggle.com/datasets/meirnizri/covid19-dataset)
* **Özellikler:** Veri seti yaş, cinsiyet, pnömoni, diyabet, astım, hipertansiyon ve tütün kullanımı gibi 20'den fazla klinik parametre içermektedir. Temizlik sonrası yaklaşık 1 milyon satır üzerinde çalışılmıştır.

## 🛠 Veri Ön İşleme Adımları
1.  **Geçersiz Değerlerin Temizlenmesi:** Veri setinde "bilinmiyor" anlamına gelen maskelenmiş değerler (97, 98, 99) `NaN` olarak işaretlenmiş ve bu satırlar veri setinden çıkarılmıştır.
2.  **Hedef Değişken Oluşturma:** `CLASIFFICATION_FINAL` sütunu baz alınarak; 1, 2 ve 3 değerleri "Pozitif (1)", diğer değerler (4, 5, 6, 7) "Negatif (0)" olacak şekilde ikili sınıflandırmaya (binary classification) dönüştürülmüştür.
3.  **Gereksiz Sütunların Kaldırılması:** Tahminleme sürecine doğrudan etkisi olmayan ve RAM yükünü artıran `DATE_DIED` gibi sütunlar veri setinden düşürülmüştür.
4.  **Veri Bölme:** Veri seti %80 eğitim ve %20 test olacak şekilde ayrılmıştır.

## 🤖 Kullanılan Algoritmalar ve Mantığı
* **Logistic Regression:** Bağımlı ve bağımsız değişkenler arasındaki ilişkiyi bir sigmoid fonksiyonu kullanarak olasılıksal olarak modeller. Doğrusal ayrılabilir verilerde hızlı ve etkilidir.
* **Random Forest:** Birden fazla karar ağacının birleşmesiyle oluşan bir topluluk öğrenmesi (ensemble) yöntemidir. Aşırı öğrenmeyi engelleyerek genel geçer sonuçlar üretir.
* **Decision Tree:** Veriyi belirli sorular sorarak dallara ayıran ve en son yaprak düğümlerde sınıflandırma yapan ağaç tabanlı bir yapıdır.
* **KNN (K-Nearest Neighbors):** Yeni bir veriyi, ona en yakın olan K sayıdaki komşusunun sınıfına göre atayan mesafe tabanlı basit bir algoritmadır.

## 📈 Model Performans Karşılaştırması
Test veri seti üzerinden elde edilen metrikler aşağıdaki tabloda özetlenmiştir. Rakamlar yuvarlanarak yüzde cinsinden verilmiştir:

| Algoritma | Accuracy | Precision (Pozitif) | Recall (Pozitif) | F1-Score |
| :--- | :---: | :---: | :---: | :---: |
| **Logistic Regression** | **%62.37** | **%63.00** | **%72.21** | **%67.29** |
| **Random Forest** | %59.32 | %61.25 | %65.64 | %63.37 |
| **Decision Tree** | %57.89 | %60.87 | %60.05 | %60.45 |
| **KNN** | %57.30 | %59.60 | %63.15 | %61.33 |

## 💡 Sonuç ve Yorumlar
* Yapılan testler sonucunda şaşırtıcı bir şekilde **Logistic Regression** algoritması, en yüksek doğruluk (%62.37) ve en yüksek duyarlılık (%72.21 Recall) oranını vererek diğer modelleri geride bırakmıştır.
* Bu durum, veri setindeki özelliklerin hedef değişkenle doğrusal (linear) bir ilişkiye daha yakın olduğunu göstermektedir.
* Modelin sağlık sektöründe kullanılması durumunda hasta olanları kaçırmamak adına en kritik metrik olan **Recall (Duyarlılık)**, yine Logistic Regression modelinde en yüksek çıkmıştır.
* Ancak, genel doğruluk oranları (%60 civarı) verideki gürültünün (noise) yüksek olduğunu ve sadece semptomlarla tam isabetli bir tahminin zor olduğunu göstermektedir.

## 🚀 Kodların Nasıl Çalıştırılacağı
1.  Gerekli kütüphaneleri yükleyin: `pip install pandas numpy scikit-learn seaborn matplotlib`
2.  Veri setini Kaggle üzerinden indirip ana dizine `Covid Data.csv` adıyla ekleyin.
3.  Proje dosyasındaki `final_code.ipynb` dosyasını Jupyter Notebook veya Google Colab üzerinde çalıştırın.

**Hazırlayan:** Ayşegül Duran  
**Öğrenci No:** 25019921045
**Üniversite:** Bartın Üniversitesi - Yapay Zeka Operatörlüğü
