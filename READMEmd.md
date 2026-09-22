# Capacity Futures: PyTorch ile Tedarik Zincirinde Atıl Kapasite Tahmini 🚛

## Proje Amacı (Project Overview)
Bu proje, "Capacity Futures" vizyonu doğrultusunda, lojistik tedarik zinciri ağlarındaki atıl araç kapasitelerini ve depo envanter seviyelerini tahmin etmek amacıyla geliştirilmiştir. PyTorch derin öğrenme kütüphanesi kullanılarak, saatlik zaman serisi verileri üzerinden Regresyon tabanlı LSTM (Uzun Kısa Süreli Bellek) ve GRU (Geçitli Tekrarlayan Birim) modelleri inşa edilmiştir. Temel hedef, geçmiş 24 saatlik `warehouse_inventory_level` (Depo Envanter Seviyesi) verisine bakarak bir sonraki saatin doluluk oranını ve dolayısıyla filodaki boş kapasiteyi öngörmektir.

## Veri Seti (Dataset)
Projede Kaggle'dan alınan `dynamic_supply_chain_logistics_dataset.csv` kullanılmıştır.
*   **Özellik:** Saatlik zaman damgası (`timestamp`) ve depo envanter seviyesi (`warehouse_inventory_level`).
*   **Ön İşleme:** Veriler `MinMaxScaler` ile -1 ve 1 aralığında ölçeklendirilmiş, geçmiş 24 saati girdi (lookback=24), 25. saati hedef (target) kabul eden kayan pencere (sliding window) algoritmasıyla dizilere (sequences) dönüştürülmüştür. Veri setinin %80'i eğitim, %20'si test için ayrılmıştır.

## Kurulum ve Çalıştırma (Setup Instructions)
Kodları kendi ortamınızda çalıştırmak için aşağıdaki adımları izleyebilirsiniz:
1.  Bu depoyu bilgisayarınıza klonlayın.
2.  Gerekli kütüphanelerin (Pandas, NumPy, PyTorch, Scikit-learn, Matplotlib) kurulu olduğundan emin olun.
3.  `dynamic_supply_chain_logistics_dataset.csv` dosyasını ana dizine ekleyin.
4.  `Capacity_Futures_Model.ipynb` adlı Jupyter Notebook dosyasını açın ve hücreleri yukarıdan aşağıya sırasıyla çalıştırın[cite: 1].

## Model Karşılaştırması ve Sonuçlar (Project Findings: LSTM vs GRU)
Test verisi üzerinde her iki modelin ürettiği tahminlerin Hata Kareler Ortalaması (MSE) ve Kök Hata Kareler Ortalaması (RMSE) metrikleriyle değerlendirmesi aşağıdaki gibidir[cite: 1]:

| Model | Eğitim Süresi (sn) | Test MSE | Test RMSE (Kapasite Birimi) |
| :--- | :--- | :--- | :--- |
| **LSTM** | [Örn: 12.50] | [Örn: 450.2] | [Örn: 21.2] |
| **GRU**  | [Örn: 8.30]  | [Örn: 420.5] | [Örn: 20.5] |

**Değerlendirme:** Deneylerimiz sonucunda GRU modelinin, LSTM'e kıyasla daha az parametreye sahip olmasından dolayı [daha hızlı eğitildiği / benzer hata oranları verdiği] gözlemlenmiştir[cite: 1]. Çizgi grafiklerinde modellerin genel envanter trendini başarıyla yakaladığı görülmektedir.

## Kritik Düşünce ve Gelecek Adımlar (Reflection)
Makine öğrenmesi modelleri her ne kadar karmaşık örüntüleri yakalayabilse de, tedarik zinciri ve lojistik gibi insan faktörünün (şoför davranışları, anlık kazalar, hava durumu) yoğun olduğu alanlarda tahminlerin gerçek dünyadaki kesinliği sınırlıdır. *AI Snake Oil* (Narayanan & Kapoor) perspektifinden bakıldığında, yapay zekanın karmaşık sosyal/fiziksel sistemleri kusursuz tahmin edebileceği yanılgısına düşmemek ve modeli yalnızca bir "karar destek mekanizması" olarak konumlandırmak esastır[cite: 1]. Gelecek çalışmalarda hava durumu ve trafik yoğunluğu gibi diğer değişkenler modele entegre edilerek çok değişkenli bir yapı kurulabilir.