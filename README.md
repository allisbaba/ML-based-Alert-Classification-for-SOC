# Güvenlik Operasyon Merkezleri için Makine Öğrenimine Dayalı Otomatik Uyarı Sınıflandırması

Bu proje, Ege Üniversitesi Fen Bilimleri Enstitüsü Bilgisayar Mühendisliği Anabilim Dalı bünyesinde, Siber Güvenlik Bilimi dersi kapsamında geliştirilmiştir. Projenin temel amacı, Siber Güvenlik Operasyon Merkezlerinde (SOC) görev yapan analistlerin en büyük problemlerinden biri olan "alarm yorgunluğunu" (alert fatigue) azaltmak amacıyla akıllı bir alarm triyaj ve önceliklendirme mekanizması kurmaktır.

## 👥 Yazar
* **Furkan ALLİŞ** - Ege Üniversitesi, Bilgisayar Mühendisliği

## 📝 Projenin Özeti ve Problem Tanımı
Modern siber güvenlik altyapılarında SIEM sistemleri günde binlerce alarm üretmektedir. Ancak bu alarmların büyük bir kısmı bağlamdan yoksun ve "False Positive" (yanlış alarm) niteliğindedir. Bu durum, gerçek siber saldırıların gürültü arasında kaybolmasına ve analistlerin yıpranmasına yol açmaktadır. 

Bu çalışmada, siber güvenlik domainine özgü ağ trafiği istatistikleri ile Doğal Dil İşleme (NLP) teknikleri harmanlanarak otonom bir triyaj modeli geliştirilmiştir. Proje mimarisi oluşturulurken literatürdeki güncel **AACT (Automated Alert Classification and Triage)** modeli referans alınmıştır.

## 🛠️ Kullanılan Teknolojiler ve Yöntemler
* **Programlama Dili:** Python
* **Veri İşleme & Analiz:** Pandas, NumPy
* **Makine Öğrenmesi & Modelleme:** Scikit-learn, XGBoost
* **Veri Dengeleme:** Imbalanced-learn (SMOTE)
* **NLP (Doğal Dil İşleme):** TF-IDF Vectorizer
* **Veri Seti:** CIC-IDS2017 (DDoS ve Benign ağ akışları)

## 🏗️ Metodoloji ve İş Akışı
1. **Boyut Azaltma & Temizlik:** 79 sütundan oluşan ham CIC-IDS2017 veri setindeki sabit (constant) ve %95 üzeri yüksek korelasyona sahip gürültülü öznitelikler ayıklanarak 43 kritik sütuna indirilmiştir.
2. **Yapay Log & NLP Vektörleştirme (Feature-to-String):** Port, paket boyutu ve akış süresi gibi metrikler birleştirilerek sentetik siber güvenlik log cümleleri üretilmiş ve bu cümleler TF-IDF yöntemiyle 50 boyutlu vektörlere dönüştürülmüştür.
3. **Sınıf Dengeleme (SMOTE):** Eğitim setindeki DDoS ve Benign sınıfları arasındaki dengesizlik SMOTE algoritmasıyla giderilerek adil bir eğitim alanı yaratılmıştır.
4. **Modelleme:** Random Forest ve XGBoost algoritmaları eğitilerek operasyonel hız ve performans bazında yarıştırılmıştır.

## 📊 Deneysel Sonuçlar ve Performans Karşılaştırması

Proje öneri raporunda hedeflenen %70 doğruluk başarısı, optimize edilen öznitelik mühendisliği ve topluluk öğrenmesi (Ensemble Learning) sayesinde aşılmıştır.

| Model | Eğitim Süresi | Doğruluk (Accuracy) | Kaçırılan Saldırı (False Negative) |
|---|---|---|---|
| **Random Forest** | 9.26 sn | %99.99 | 3 |
| **XGBoost** | **2.76 sn** | **%99.99** | **2 (En Düşük)** |

###Açıklanabilir Yapay Zeka (XAI)
Modelin karar mekanizması incelendiğinde, NLP ile ürettiğimiz **`port_80`** özniteliğinin model kararlarında **%73 ağırlıkla** en kritik faktör olduğu tespit edilmiştir. Bu durum, siber güvenlik verilerinde bağlamsal log modellemenin önemini akademik olarak kanıtlamaktadır.

## 🚀 Kurulum ve Çalıştırma

1. Repoyu klonlayın:
   ```bash
   git clone <github-repo-url>
   cd <repo-name>

2. Sanal Ortamı oluşturun ve aktif edin:
    ```bash
    python -m venv venv
    # Windows için:
    .\venv\Scripts\activate 

3. Gerekli kütüphaneleri yükleyin:
    ```bash
    pip install -r requirements.txt

4. notebooks/01_eda_initial_look.ipynb dosyasını VS Code üzerinden sırasıyla çalıştırın.

## 📚 Referanslar
    [1] M. Turcotte, F. Labrèche, and S. O. Paquette, "Automated Alert Classification and Triage (AACT): An Intelligent System for the Prioritisation of Cybersecurity Alerts," arXiv preprint arXiv:2505.09843, 2025.

    [2] Sharafaldin, I., et al. "Toward Generating a New Intrusion Detection Dataset and Intrusion Traffic Characterization" ICISSP, 2018.
