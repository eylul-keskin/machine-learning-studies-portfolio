# MNIST: PCA, KNN ve Parça Birleştirme ile Veri Artırma

[Notebook'u aç](mnist_pca_knn_mosaic.ipynb) · [Ana sayfa](../README.md)

## Amaç ve yöntem

Bu çalışma, MNIST rakam görüntülerinde boyut indirgeme ve komşuluk tabanlı sınıflandırmayı temel işlemlerden başlayarak uygular. Aynı sınıftaki farklı görüntülerden üretilen sentetik örneklerin eğitim verisine eklenmesiyle oluşan değişimi karşılaştırır.

Görüntü ve etiketler IDX dosyalarından okunur. Görüntüler 784 boyutlu vektörlere dönüştürülür ve piksel değerleri 255'e bölünür. PCA; eğitim ortalamasıyla merkezleme, kovaryans matrisi, özdeğer ayrışımı ve seçilen bileşenlere izdüşüm adımlarıyla uygulanır. KNN, kareli Öklid uzaklığına göre komşuları belirler ve çoğunluk oylamasıyla tahmin üretir. Doğruluk ve karışıklık matrisi ayrı fonksiyonlarla hesaplanır.

## Hiperparametre seçimi ve deney düzeni

Eğitim verisinden sabit rastgelelik tohumu ile 10.000 örneklik doğrulama bölümü ayrılır. PCA bileşeni sayıları `20, 30, 50, 75, 100, 200`; komşu sayıları `1, 3, 5, 7, 9` arasından değerlendirilir. Önce 1.000 doğrulama örneğiyle hızlı tarama yapılır. Her bileşen sayısında seçilen iki aday, ardından doğrulama bölümünün tamamında karşılaştırılır. Seçimden sonra PCA tüm eğitim verisiyle yeniden hesaplanır.

Sentetik örnek için aynı sınıftan dört farklı görüntünün çeyrekleri birleştirilir. Sınıf başına `100`, `500` ve `1.000` ek örnek içeren seçenekler denenir. Seçilen komşu ve bileşen sayıları korunur; PCA genişletilmiş eğitim verisiyle yeniden öğrenilir.

## Güçlü taraflar ve sınırlılıklar

Veri okuyucularının, PCA/KNN adımlarının ve metriklerin ayrı fonksiyonlarla gösterilmesi algoritmik akışı izlemeyi kolaylaştırır. Temel modelin hiperparametreleri doğrulama verisiyle seçilir.

Bununla birlikte, sentetik miktarlar test doğruluğuyla karşılaştırılır ve en yüksek seçenek bu ölçütten seçilir. Bu durum nihai test değerlendirmesinin bağımsızlığını sınırlar. Ek örneklerle PCA temeli de değiştiği için olası fark yalnızca yeni KNN komşularına bağlanamaz. Aynı sınıftan parçalar seçmek, oluşan görüntünün okunabilirliğini tek başına garanti etmez. Üretim değişkenliği de tekrarlı deneylerle ayrıca ölçülmez.

## Çalıştırma

NumPy ve [rehberdeki](../DATA_SETUP.md) dört MNIST dosyası gerekir. Kod Windows biçimli göreli yollar kullanır. Notebook'un çalışma dizini bu klasör olmalıdır.
