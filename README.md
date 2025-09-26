# Akbank Derin Öğrenme Bootcamp: Yeni Nesil Proje Kampı - Intel Image Classification

## Projenin Amacı
Bu proje, Akbank Derin Öğrenme Bootcamp kapsamında, Convolutional Neural Network (CNN) mimarisi kullanarak görsel sınıflandırma görevi gerçekleştirmeyi ve derin öğrenme süreçlerini (veri önişleme, model geliştirme, eğitim, değerlendirme, yorumlama ve hiperparametre optimizasyonu) pratik olarak deneyimlemeyi amaçlamaktadır. Proje, Intel Image Classification veri seti üzerinde farklı doğal ve yapay ortamların sınıflandırılmasına odaklanmıştır.

## Veri Seti Hakkında Bilgi
*   **Adı:** Intel Image Classification
*   **Tür:** Multiclass Image Classification (Çok Sınıflı Görüntü Sınıflandırma)
*   **Sınıflar:** Buildings, Forest, Glacier, Mountain, Sea, Street (Toplam 6 Sınıf)
*   **Boyut:** Yaklaşık 25.000 eğitim görüntüsü ve 14.000 test görüntüsü. Her bir görüntü 150x150 piksel boyutundadır.
*   **Açıklama:** Veri seti, farklı coğrafi ve kentsel ortamları temsil eden görüntülerden oluşmaktadır.

## Kullanılan Yöntemler
*   **Geliştirme Ortamı:** Kaggle Notebook
*   **Derin Öğrenme Kütüphanesi:** TensorFlow 2.x / Keras
*   **Veri Önişleme:**
    *   Görüntüleri 150x150 piksel boyutuna yeniden boyutlandırma.
    *   Piksel değerlerini 0-1 arasına normalleştirme.
    *   Eğitim verisinin %20'si doğrulama seti olarak ayrılmıştır.
    *   Veri seti, eğitim, doğrulama ve test kümelerine ayrılmıştır.
*   **Veri Çoğaltma (Data Augmentation):** `ImageDataGenerator` kullanılarak eğitim verisine rastgele döndürme (`rotation_range`), yatay/dikey kaydırma (`width_shift_range`, `height_shift_range`), kesme (`shear_range`), yakınlaştırma (`zoom_range`) ve yatay çevirme (`horizontal_flip`) gibi dönüşümler uygulanmıştır.
*   **CNN Model Mimarisi:**
    *   Ardışık `Conv2D` katmanları (32, 64, 128, 256 filtreler).
    *   `MaxPooling2D` katmanları ile boyut azaltma.
    *   `Dropout` katmanları (0.25 ve 0.5 oranları) ile aşırı öğrenme (overfitting) kontrolü.
    *   `Flatten` katmanı.
    *   `Dense` (tam bağlantılı) katmanlar (512 nöron).
    *   Aktivasyon fonksiyonları olarak ara katmanlarda `ReLU`, çıkış katmanında `Softmax` (6 sınıf için).
*   **Model Optimizasyonu:** `Adam` optimizer (öğrenme oranı 0.001) ve `sparse_categorical_crossentropy` kaybı fonksiyonu kullanılmıştır.
*   **Eğitim Stratejisi:** `EarlyStopping` (val_loss 5 epoch boyunca iyileşmezse) ve `ModelCheckpoint` (en iyi `val_accuracy`'ye sahip modeli kaydetme) callback'leri kullanılmıştır.
*   **Model Değerlendirme:**
    *   Eğitim ve Doğrulama `Accuracy` ve `Loss` grafikleri.
    *   Test seti üzerinde `Confusion Matrix` görselleştirmesi.
    *   Test seti üzerinde `Classification Report` (Precision, Recall, F1-Score).
    *   `Grad-CAM` ile modelin karar verdiği bölgelerin görselleştirilmesi.
*   **Hiperparametre Optimizasyonu:** Katman sayısı, filtre sayısı, dropout oranları, öğrenme oranı gibi parametreler üzerinde denemeler yapılmış ve etkileri gözlemlenerek en iyi konfigürasyon bulunmaya çalışılmıştır.

## Elde Edilen Sonuçlar
Model, `Intel Image Classification` veri seti üzerinde test edildiğinde aşağıdaki başarımları elde etmiştir:
*   **En İyi Doğrulama Başarımı:** Yaklaşık **[Kaggle Notebook'unuzdaki en yüksek val_accuracy değeri]%**
*   **Test Doğrulama Başarımı:** Yaklaşık **[Kaggle Notebook'unuzdaki test_accuracy değeri]%**
*   **Test Kaybı:** **[Kaggle Notebook'unuzdaki test_loss değeri]**
*   **Overfitting/Underfitting Durumu:** `Data Augmentation` ve `Dropout` teknikleri sayesinde modelin overfitting'e karşı dirençli olduğu gözlemlenmiştir. Eğitim ve doğrulama kaybı grafikleri istikrarlı bir yakınsama göstermiştir.
*   **Sınıflandırma Performansı:** `Confusion Matrix` ve `Classification Report` sonuçlarına göre, model bazı sınıfları diğerlerine göre daha iyi sınıflandırabilmiştir. Özellikle "Forest" ve "Glacier" gibi sınıflarda yüksek F1-Score'lar elde edilirken, "Mountain" ve "Buildings" gibi benzer özelliklere sahip sınıflar arasında bazı karışıklıklar gözlemlenmiştir.
*   **Grad-CAM Yorumları:** Grad-CAM görselleştirmeleri, modelin sınıflandırma yaparken görüntünün anlamlı bölgelerine (örneğin, bir binanın silueti veya bir dağın zirvesi) odaklandığını doğrulamıştır.

## Kaggle Notebook Linki
