# Veri Hazırlama ve Çalışma Dizinleri

Veri kümeleri ve eğitim sırasında üretilen dosyalar repoya dahil değildir. Her notebook göreli yollar kullandığı için **kendi klasörünü çalışma dizini yaparak** açılmalıdır. Aynı veri dosyaları ilgili çalışma klasörlerine ayrı ayrı yerleştirilebilir.

## MNIST — ilk üç çalışma

[CVDF MNIST dağıtımı](https://github.com/cvdfoundation/mnist), eğitim/test görüntülerini ve etiketlerini dört sıkıştırılmış IDX dosyası olarak sağlar. Arşivleri açın ve dosyaları aşağıdaki adlarla yerleştirin. Kaynaktaki `train-images-idx3-ubyte` gibi tireli adlar, notebook'ların beklediği `train-images.idx3-ubyte` biçimine dönüştürülmelidir.

İlk üç çalışma klasörünün her birinde:

```text
<project-folder>/
├── <notebook>.ipynb
└── archive/
    ├── train-images.idx3-ubyte
    ├── train-labels.idx1-ubyte
    ├── t10k-images.idx3-ubyte
    └── t10k-labels.idx1-ubyte
```

Birinci notebook `archive\...` biçimli Windows yolları kullanır. Diğer ikisi `archive/...` kullanır. Dosyalar sıkıştırılmış `.gz` hâliyle okunmaz.

## Dördüncü çalışma

```text
04-synthetic-pretraining/
├── synthetic_pretraining_mnist_cifar10_fruits360.ipynb
└── archive/
    ├── mnist/
    │   ├── train-images.idx3-ubyte
    │   ├── train-labels.idx1-ubyte
    │   ├── t10k-images.idx3-ubyte
    │   └── t10k-labels.idx1-ubyte
    ├── cifar10/
    │   └── cifar-10-batches-py/
    │       ├── data_batch_1
    │       ├── data_batch_2
    │       ├── data_batch_3
    │       ├── data_batch_4
    │       ├── data_batch_5
    │       ├── test_batch
    │       └── batches.meta
    └── fruits360/
        ├── Training/
        │   └── <class-name>/<image-files>
        └── Test/
            └── <class-name>/<image-files>
```

- **MNIST:** Aynı dört açılmış dosyayı bu kez `archive/mnist/` altına yerleştirin.
- **CIFAR-10:** [Veri kümesinin resmî sayfasındaki](https://www.cs.toronto.edu/~kriz/cifar.html) **CIFAR-10 Python version** arşivini açın. Kod, `cifar-10-batches-py/` klasörünün bulunmasını destekler; dosyalar doğrudan `archive/cifar10/` altında da olabilir.
- **Fruits360:** [Fruits-360 100×100 dağıtımını](https://github.com/fruits-360/fruits-360-100x100) kullanın. Kod `Training` ve `Test` klasörlerini alt dizinlerde de arar; her ad için tek eşleşme bulunmalıdır. Görüntüler aynı boyutta olmalı ve her sınıf ayrı klasörde yer almalıdır. Veri kümesinin sürümü/sınıf kapsamı değişirse deney koşulları da değişir; kullanılan sürümü ayrıca kaydedin.

## Çıktılar ve yeniden çalıştırma

Üçüncü çalışma checkpoint ve arama sonuçlarını çalışma klasöründeki `.pt` dosyalarına yazar. Dördüncü çalışma `checkpoints/`, `results/` ve `demo_examples/` klasörlerini oluşturur.

Kaydedilmiş deney dosyaları repoya eklenmemiştir. Dosyalara bağımlı sonraki hücreleri kullanmadan önce, gerekli eğitim/üretim adımları sırayla tamamlanmalıdır. Özellikle dördüncü çalışmada, aynı kayıt klasörlerinde farklı veri veya ayarlara ait sonuçları bir arada kullanmayın.
