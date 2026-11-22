# MNIST: MLP ve Patch Mosaic Deneyleri

[Notebook'u aç](mnist_mlp_patch_mosaic.ipynb) · [Ana sayfa](../README.md)

## Amaç ve yöntem

Bu çalışma, MNIST rakamlarını sınıflandırmak için PyTorch ile çok katmanlı algılayıcı (MLP) kurar. Model yapılandırmalarının araştırılmasını ve aynı sınıftaki görüntülerden oluşturulan patch mosaic örneklerinin farklı eğitim bileşimlerinde kullanılmasını ele alır.

Görüntüler IDX dosyalarından okunur, piksel değerleri ölçeklenir ve 784 boyutlu vektörlere dönüştürülür. Eğitim kümesinden sınıf başına 1.000 örnek doğrulamaya ayrılır; resmî test kümesi ayrı tutulur.

## Hiperparametre seçimi ve karşılaştırmalar

Başlangıç modelinin ardından 40 geniş ve 18 daraltılmış deneme tanımlanır. Katman sayısı ve boyutları, aktivasyon, dropout, batch normalization, öğrenme oranı ve batch büyüklüğü araştırılır. Seçilen üç yapılandırma ayrıca `42`, `43`, `44` tohumlarıyla değerlendirilir. Erken durdurma ve en iyi checkpoint'in geri yüklenmesi doğrulama kaybına dayanır.

Patch mosaic üretiminde aynı rakam sınıfından dört farklı görüntünün kendi konumlarındaki 14×14 çeyrekleri birleştirilir. Sınıf başına `100`, `250`, `500`, `1.000` sentetik örnek adayları tanımlanır. Sabitlenmiş MLP yapılandırmasıyla gerçek+sentetik eğitimler ve yalnız sentetik örneklerden oluşan eğitimler karşılaştırılır. Miktar seçimi doğrulama sonuçları üzerinden yapılır.

## Güçlü taraflar ve sınırlılıklar

Veri ayrımı, yapılandırılabilir model, ayrı eğitim/değerlendirme işlevleri, checkpoint yönetimi ve mimari adayları için çoklu tohum karşılaştırması güçlü taraflardır.

Sentetik miktarı değiştikçe sınıf ağırlıkları yeniden hesaplanır. Doğrulama kayıpları da bu farklı ağırlıklarla ölçüldüğünden miktar seçimi ortak bir değerlendirme ölçütüne tam olarak dayanmaz. Veri kümesi büyürken epoch sınırının sabit kalması toplam eğitim adımlarını değiştirir. Sentetik deneyler tek tohumla tanımlanmıştır. Bu sınırlar, farkın yalnız sentetik içeriğe bağlanmasını ve seçilen miktarın optimal kabul edilmesini güçleştirir.

“Yalnız sentetik”, eğitimde değiştirilmemiş gerçek görüntü kullanılmadığını belirtir. Sentetik görüntüler etiketli gerçek eğitim verisinden türetilir. Aynı sınıftan parça seçilmesi, yeni görüntünün okunabilirliğini tek başına garanti etmez.

## Çalıştırma

NumPy, PyTorch ve scikit-learn gerekir. Kod CUDA destekli GPU kullanımını zorunlu tutar. MNIST dosyaları [veri rehberine](../DATA_SETUP.md) göre yerleştirilmelidir. Notebook'un çalışma dizini bu klasör olmalıdır; arama ve eğitimler `.pt` dosyaları üretir.
