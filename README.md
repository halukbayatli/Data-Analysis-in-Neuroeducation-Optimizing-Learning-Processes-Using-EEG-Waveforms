# Nöro-Eğitimde Veri Analizi: EEG Dalga Boyları ile Öğrenme Süreçlerinin Optimizasyonu

Bu proje, EEG frekans bantları ile öğrenme sürecindeki dikkat ve meditasyon durumları arasındaki ilişkiyi inceleyen bir veri analizi çalışmasıdır. Çalışmada 10 üniversite öğrencisinden toplanan 12.811 gözlemden oluşan EEG veri seti analiz edilmiş; frekans bantlarının bilişsel durumlarla ilişkisi istatistiksel yöntemler ve makine öğrenmesi modelleri ile değerlendirilmiştir.

![Proje Afişi](<Haluk Bayatlı Nöro-Eğitimde Veri Analizi EEG Dalga Boyları ile Öğrenme Süreçlerinin Optimizasyonu Afiş.png>)

## Proje Bilgileri

- **Yazar:** Haluk Bayatlı
- **Kurum:** Necmettin Erbakan Üniversitesi, Mühendislik Fakültesi, Bilgisayar Mühendisliği
- **Konu:** EEG dalga boyları kullanılarak öğrenme süreçlerinde dikkat ve meditasyon düzeylerinin analizi
- **Hedef değişken:** `UserDefinedLabel`

## Amaç

Çevrimiçi eğitim ortamlarında öğrencinin dikkat ve bilişsel yük durumunu anlık ve nesnel biçimde izlemek zordur. Bu proje, EEG sinyallerinden elde edilen frekans bantlarını kullanarak:

- dikkat ve meditasyon skorları ile EEG bantları arasındaki ilişkileri incelemeyi,
- bilişsel durumları açıklayan istatistiksel örüntüleri ortaya koymayı,
- dikkat/meditasyon düzeylerini tahmin edebilecek makine öğrenmesi modellerini karşılaştırmayı amaçlar.

## Veri Seti

Kullanılan ana değişkenler şunlardır:

- Kimlik ve video bilgileri: `SubjectID`, `VideoID`
- Bilişsel skorlar: `Attention`, `Mediation`
- EEG sinyali ve frekans bantları: `Raw`, `Delta`, `Theta`, `Alpha1`, `Alpha2`, `Beta1`, `Beta2`, `Gamma1`, `Gamma2`
- Etiketler: `predefinedlabel`, `user-definedlabeln`
- Demografik bilgiler: yaş, cinsiyet ve etnik köken bilgileri

Projede kullanılan veri dosyaları:

- [`EEG_data.csv`](<EEG_data.csv>)
- [`VA_23_030/EEG_data.csv`](<VA_23_030/EEG_data.csv>)
- [`VA_23_030/demographic_info.csv`](<VA_23_030/demographic_info.csv>)

## Yöntem

Analiz akışı aşağıdaki adımlardan oluşur:

1. EEG ve demografik veri setlerinin okunması ve birleştirilmesi
2. Eksik veri kontrolü
3. Veri dağılımlarının incelenmesi
4. Aykırı değer analizleri
5. RobustScaler ile ölçekleme
6. Spearman korelasyon analizi
7. Mann-Whitney U testi ve çoklu karşılaştırmalar için Bonferroni düzeltmesi
8. Sınıflandırma modellerinin eğitilmesi ve karşılaştırılması
9. GridSearchCV ile hiperparametre optimizasyonu

Kullanılan makine öğrenmesi modelleri:

- Logistic Regression
- Support Vector Machine
- Random Forest
- AdaBoost
- XGBoost
- LightGBM
- Gradient Boosting Classifier
- Yapay Sinir Ağı

## Bulgular

Analiz sonucunda tüm EEG frekans bantlarının `Attention` ve `Mediation` skorlarıyla istatistiksel olarak anlamlı negatif korelasyon gösterdiği görülmüştür. `Attention` ile en güçlü ilişki `Theta` bandında, `Mediation` ile en güçlü ilişki ise `Beta2` bandında tespit edilmiştir.

Model karşılaştırmalarında tek başına hiçbir özellik güçlü bir ayırt edici performans göstermemiştir. Başarım, özellik kombinasyonlarına bağlı olarak değişmiştir. Sekiz model arasında Gradient Boosting Classifier, genelleme ve başarı dengesiyle öne çıkmıştır.

Öne çıkan test sonuçları:

- **En iyi model:** Gradient Boosting Classifier
- **Test doğruluğu:** %65
- **F1 skoru:** 0.65

## Dosya Yapısı

```text
.
├── EEG_data.csv
├── VA_23_030.ipynb
├── VA_23_030/
│   ├── EEG_data.csv
│   └── demographic_info.csv
├── Haluk Bayatlı Nöro-Eğitimde Veri Analizi EEG Dalga Boyları ile Öğrenme Süreçlerinin Optimizasyonu Afiş.png
└── Nöro-Eğitimde Veri Analizi EEG Dalga Boyları ile Öğrenme Süreçlerinin Optimizasyonu.pdf
```

## Çalıştırma

Notebook dosyası:

```text
VA_23_030.ipynb
```

Gerekli temel Python kütüphaneleri:

```bash
pip install numpy pandas matplotlib seaborn missingno scikit-learn scipy xgboost lightgbm joblib
```

Notebook içinde `demographic_info.csv` dosyası doğrudan okunmaktadır. Bu nedenle notebook çalıştırılırken çalışma dizini veri dosyalarının bulunduğu klasör olacak şekilde ayarlanmalı ya da dosya yolları `VA_23_030/demographic_info.csv` biçiminde güncellenmelidir.

## Kaynak

H. Wang, Y. Li, X. Hu, Y. Yang, Z. Meng, K.-M. Chang, "Using EEG to Improve Massive Open Online Courses Feedback Interaction", 2011.
