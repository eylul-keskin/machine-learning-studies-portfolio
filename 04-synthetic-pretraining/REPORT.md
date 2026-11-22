# MNIST, CIFAR-10 ve Fruits360: Sentetik Ön Eğitim

[Notebook'u aç](synthetic_pretraining_mnist_cifar10_fruits360.ipynb) · [Ana sayfa](../README.md)

## Amaç ve yöntem

Bu çalışma, doğrudan gerçek görüntülerle eğitim ile önce aynı sınıftan türetilmiş sentetik görüntülerde, ardından gerçek görüntülerde eğitim akışlarını karşılaştırır. MNIST için MLP; CIFAR-10 ve Fruits360 için yapılandırılabilir CNN kullanılır.

Veri okuyucuları, veri kümesi ve DataLoader oluşturma, model tanımları, eğitim/değerlendirme işlevleri ve deney kayıtları ortak bir altyapıda toplanır. Doğrulama eğitim verisinden ayrılır. CIFAR-10 ve Fruits360 normalizasyon istatistikleri yalnız eğitim bölümünden hesaplanır.

Sentetik görüntüler aynı sınıftan seçilen görüntülerin yeniden boyutlandırılıp dikey, yatay veya 2×2 düzeninde birleştirilmesiyle oluşturulur. Bu yöntem, üçüncü çalışmadaki sabit çeyrekleri alma yaklaşımından farklıdır.

## Hiperparametre seçimi

MLP ve CNN yapılandırmaları kaba ve daraltılmış aramalarla araştırılır. Katman boyutları, aktivasyon, dropout, batch normalization, öğrenme oranı, batch büyüklüğü; CNN'de ayrıca kanal sayıları, blok başına konvolüsyon sayısı ve ağırlık azaltma ayarları ele alınır. Fruits360 için kısa ön eleme ve daha uzun eğitim aşamaları kullanılır.

Sentetik deneylerde birleştirme yöntemi, sentetik örnek oranı ve ön eğitim epoch sayısı doğrulama üzerinden seçilir. MNIST'te yöntem sıraları ve öğrenme oranları da araştırılır. Seçili yapılandırmalar `42`, `52`, `62` tohumlarıyla doğrulanır; final test için önceden belirlenen `42` tohumu kullanılır. Üç tohum özeti doğrulama sonuçlarına aittir.

## Güçlü taraflar ve sınırlılıklar

Üç veri kümesinde ortak deney işlevlerinin kullanılması, checkpoint kaydı, erken durdurma ve doğru/yanlış tahmin örnekleri içeren demo çalışmanın güçlü taraflarıdır.

Sentetik akış ek ön eğitim içerir; eşit toplam eğitim adımıyla yürütülen ek bir gerçek-veri kontrolü yoktur. Dolayısıyla karşılaştırma iki eğitim akışını değerlendirir; farkı yalnız sentetik içeriğe ayırmaz. Bazı aramalar önceki `.pt` kayıtlarından devam ederken veri sürümü, bölme ve tüm deney ayarlarını doğrulamaz; farklı deney kayıtlarının aynı klasörde karışmaması gerekir. Sentetik örneklere kaynak sınıf etiketi atanır; görüntünün sınıf anlamını koruması ayrıca sınanmaz.

## Çalıştırma

NumPy, PyTorch, OpenCV ve Matplotlib gerekir. Cihaz otomatik seçilir. Veri yapısı [rehberde](../DATA_SETUP.md) belirtilmiştir. Notebook çalışma dizini bu klasör olmalıdır. `checkpoints/`, `results/` ve `demo_examples/` çalışma sırasında oluşur; yeni bir ortamda demo için ilgili modellerin ve örneklerin önce üretilmesi gerekir.
