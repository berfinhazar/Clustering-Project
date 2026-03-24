# Unsupervised Academic Clustering: Autoencoder & Deep Embedding

### Projenin Amacı ve Kapsamı
Bu çalışmada, etiket bilgisi kullanılmaksızın ham akademik tez özetlerinin içerik benzerliklerine göre otomatik olarak gruplandırılması **amaçlanmıştır.** Geleneksel yöntemlerin ötesinde, derin öğrenme tabanlı boyut indirgeme teknikleriyle metinlerin anlamsal haritasının çıkarılması **hedeflenmiştir.**

### Ham Veri ve Derin Öğrenme Yaklaşımı (Zero Preprocessing)
* **Veri Stratejisi:** Proje kapsamında metinler üzerinde hiçbir ön işleme (temizleme, kök bulma vb.) **yapılmamıştır.** Modellerin, akademik terminolojideki gürültülü veriler içerisinden doğrudan öznitelik (feature) yakalama kapasitesi test edilmiştir.
* **Autoencoder Mimarisi:** Ham metinlerden elde edilen yüksek boyutlu TF-IDF vektörleri, bir **Autoencoder** sinir ağı aracılığıyla daha düşük boyutlu (latent space) anlamsal temsillere sıkıştırılmıştır.
* **Hibrit Modelleme:** Encoder katmanından elde edilen bu anlamsal çıktılar üzerinde K-Means algoritması koşturularak, branş dağılımına en yakın doğal kümelerin elde edildiği **gözlemlenmiştir.**

### Bulgular ve Değerlendirme
* **Anlamsal Başarı:** Derin öğrenme (Autoencoder) tabanlı yaklaşımın, ham metinlerden çıkardığı özniteliklerle akademik branşları (Fizik, Kimya, Biyokimya, Eczacılık, Dahiliye) temsil etmede klasik yöntemlere göre daha üstün bir **ARI (Adjusted Rand Index)** skoru ürettiği **saptanmıştır.**
* **Dinamik Tahmin:** Geliştirilen `predict_cluster` fonksiyonu ile sisteme verilen yeni bir ham metnin, herhangi bir ön işlemden geçmeksizin ilgili akademik kümeye başarıyla atandığı **doğrulanmıştır.**
* **Model Kayıt:** Eğitilen Encoder ve K-Means modelleri `.h5` ve `.pkl` formatlarında kaydedilerek, gerçek zamanlı çıkarım (inference) süreçlerine hazır hale getirildiği **görülmüştür.**

---

### Teknik Altyapı
* **Boyut İndirgeme:** Deep Autoencoders (Keras/TensorFlow).
* **Kümeleme Algoritmaları:** K-Means, DBSCAN, GMM, Hierarchical Clustering.
* **Pipeline:** TF-IDF Vectorization -> StandardScaler -> Encoder -> K-Means.
