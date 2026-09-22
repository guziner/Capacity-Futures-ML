Capacity Futures: Derin Öğrenme Tabanlı Atıl Kapasite ve Dinamik Fiyatlandırma Sistemi
Tedarik zinciri operasyonlarında verimliliği maksimize etmek ve atıl araç kapasitelerini öngörmek amacıyla geliştirilmiş karar destek sistemidir. Yöneylem araştırması prensipleriyle makine öğrenmesi teknolojilerini harmanlayan bu proje, geçmiş depo envanter verilerini kullanarak gelecekteki lojistik darboğazlarını tahmin eder ve dinamik fiyatlandırma senaryoları sunar.

🛠️ Mimari ve Metodoloji
Veri Ön İşleme: Kayan pencere (sliding window) yöntemiyle geçmiş 24 saatlik veriler, diziler (sequences) halinde PyTorch tensorlarına dönüştürülmüştür.   

Derin Öğrenme Modelleri: Zaman serisi tahmini (Time Series Forecasting) için tekrarlayan sinir ağları olan LSTM (Uzun Kısa Süreli Bellek) ve GRU (Geçitli Tekrarlayan Birim) algoritmaları kullanılmıştır.   

Kapasite ve Kuyruk Yönetimi: Tahmin edilen envanter seviyelerine göre kamyon talepleri öngörülmüş; yüksek yoğunlukta fiyatı artıran, atıl durumda ise talebi teşvik eden algoritmik bir pazar yeri fiyatlandırması kurgulanmıştır.

📊 Veri Seti
Kaggle üzerinden sağlanan dynamic_supply_chain_logistics_dataset.csv kullanılmıştır.

Hedef Değişken (Target): warehouse_inventory_level (Depo Envanter Seviyesi)

Ölçeklendirme: Model stabilitesi için MinMaxScaler ile [-1, 1] aralığına normalize edilmiştir.   

Ayrım: Kronoloji korunarak verinin %80'i eğitim (train), %20'si test olarak ayrılmıştır.   


🚀 Kurulum ve Kullanım
Sistemi kendi yerel ortamınızda simüle etmek için aşağıdaki adımları izleyin:   

Depoyu bilgisayarınıza klonlayın:

Bash
git clone 
https://github.com/kullaniciadiniz/Capacity-Futures-ML.git

Gerekli Python kütüphanelerini yükleyin:

Bash

pip install torch pandas numpy scikit-learn matplotlib

Jupyter Notebook dosyasını açarak veri hazırlığı ve model eğitimi hücrelerini sırasıyla çalıştırın.   

📈 Model Karşılaştırması (LSTM vs. GRU)
Eğitim ve test süreçleri sonucunda iki modelin performansı aşağıdaki metriklerle değerlendirilmiştir:   


GRU Modeli: Daha az iç parametreye sahip olması sebebiyle daha hızlı eğitilmiş ve bu spesifik lojistik veri setinde LSTM'e yakın Hata Kareler Ortalaması (MSE) sunmuştur.   

LSTM Modeli: Uzun vadeli trendleri yakalamada güçlü olmasına rağmen, 24 saatlik kısa dönem pencerelerde GRU ile benzer bir Kök Hata Kareler Ortalaması (RMSE) üretmiştir.
