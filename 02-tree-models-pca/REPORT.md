# MNIST: Ağaç Modelleri ve PCA

[Notebook'u aç](mnist_tree_models_pca.ipynb) · [Ana sayfa](../README.md)

## Amaç ve yöntem

Bu çalışma, MNIST rakamlarının sınıflandırılmasında karar ağacı, rastgele orman ve histogram tabanlı gradyan artırma yöntemlerini karşılaştırır. Her model ailesi, düzleştirilmiş piksel değerleriyle ve PCA ile boyutu azaltılmış özelliklerle ele alınır. İncelenen konu, model seçimi ile özellik temsilinin sınıflandırma üzerindeki etkisidir.

IDX dosyalarından okunan görüntüler vektörleştirilir ve 255'e bölünerek ölçeklenir. Eğitim verisinden her sınıf için 1.000 örnek doğrulamaya ayrılır. Bölmede ve desteklenen model ayarlarında rastgelelik tohumu `42` kullanılır.

## Hiperparametre seçimi

Önce kaba tarama, ardından seçilen bölgenin çevresinde daha ayrıntılı arama yapılır. Seçim ölçütü doğrulama doğruluğudur.

| Model | Araştırılan başlıca ayarlar |
| --- | --- |
| Karar ağacı | `gini`/`entropy`, maksimum derinlik, minimum bölme örneği |
| Rastgele orman | Kaba taramada `50`, `100`, `200` ağaç; derinlik ve `sqrt`/`log2` özellik seçimi |
| HistGradientBoosting | Öğrenme oranı ve derinlik; `max_iter=50`, `max_bins=32` ve erken durdurma |

PCA yalnızca eğitim bölümünden öğrenilir. İlk dönüşüm 256 bileşenlidir; etkin kaba model aramasında `20`, `100` ve `200` bileşenli temsiller değerlendirilir. Seçilen model ve varsa PCA, final değerlendirmeden önce tüm eğitim verisi üzerinde yeniden öğrenilir. Ayrı test kümesinde doğruluk ve karışıklık matrisi hesaplanır.

## Güçlü taraflar ve sınırlılıklar

Birden çok model ailesinin aynı veri hazırlama akışında değerlendirilmesi, ham piksel/PCA kollarının ayrılması ve final eğitimden önce doğrulama kullanılması çalışmanın güçlü taraflarıdır.

Deneyler tek sabit eğitim/doğrulama bölmesine dayanır. Çok sayıda adayın aranması hesaplama maliyetini artırabilir. Karşılaştırma tablosundaki KNN satırı birinci çalışmadan aktarılmıştır; bu notebook içinde yeniden eğitilmez. Ayrıca birinci çalışmanın doğrulama bölmesi burada kullanılan sınıf bazlı bölmeyle aynı değildir. Aktarılan satır bu bağlamla okunmalıdır. PCA'nın başarı veya hız açısından fayda sağladığı varsayılmaz; bu çalışma farklı temsilleri karşılaştıran bir deney düzenidir.

## Çalıştırma

NumPy, pandas, scikit-learn ve [rehberdeki](../DATA_SETUP.md) MNIST dosyaları gerekir. Notebook'un çalışma dizini bu klasör olmalıdır.
