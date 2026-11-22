# Makine Öğrenmesi Çalışmaları

Görüntü sınıflandırma, boyut indirgeme, model seçimi ve sentetik görüntülerle eğitim üzerine dört deneysel çalışma. Notebook'lar; temel algoritmaların NumPy ile uygulanmasından, scikit-learn modellerinin karşılaştırılmasına ve PyTorch ile çok aşamalı eğitime uzanan bir bütün oluşturur.

Her çalışmanın raporu; kullanılan yöntemi, hiperparametre seçimini, deney düzeninin güçlü taraflarını ve yorumlama sınırlarını kısaca açıklar.

## Çalışmalar

| Sıra | Çalışma | İçerik | Dosyalar |
| --- | --- | --- | --- |
| 1 | PCA, KNN ve veri artırma | PCA/KNN'nin elle uygulanması; aynı sınıftan parça birleştirme ile ek eğitim örnekleri | [Notebook](01-pca-knn/mnist_pca_knn_mosaic.ipynb) · [Rapor](01-pca-knn/REPORT.md) |
| 2 | Ağaç modelleri ve PCA | Karar ağacı, rastgele orman ve histogram tabanlı gradyan artırma; ham piksel/PCA karşılaştırması | [Notebook](02-tree-models-pca/mnist_tree_models_pca.ipynb) · [Rapor](02-tree-models-pca/REPORT.md) |
| 3 | MLP ve patch mosaic | MLP hiperparametre araması; gerçek, gerçek+sentetik ve yalnız sentetik eğitim bileşimleri | [Notebook](03-mlp-mosaic/mnist_mlp_patch_mosaic.ipynb) · [Rapor](03-mlp-mosaic/REPORT.md) |
| 4 | Sentetik ön eğitim | MNIST üzerinde MLP, CIFAR-10 ve Fruits360 üzerinde CNN; sentetik ön eğitim ardından gerçek veriyle eğitim | [Notebook](04-synthetic-pretraining/synthetic_pretraining_mnist_cifar10_fruits360.ipynb) · [Rapor](04-synthetic-pretraining/REPORT.md) |

Çalışmaların önerilen okuma sırası tablodaki sıradır. Önce kısa rapor, ardından ilgili notebook incelenebilir.

## Kullanılan araçlar

- **NumPy:** veri hazırlama, IDX okuma, matris işlemleri ve sentetik örnek üretimi.
- **scikit-learn ve pandas:** klasik modeller, PCA, değerlendirme ve karşılaştırma tabloları.
- **PyTorch:** MLP/CNN modelleri, eğitim döngüleri, erken durdurma ve checkpoint yönetimi.
- **OpenCV ve Matplotlib:** görüntü okuma, yeniden boyutlandırma ve demo görselleştirmeleri.

**Parametre**, modelin veriden öğrendiği değerdir; örneğin sinir ağı ağırlıkları veya bir karar ağacının bölme eşikleri. **Hiperparametre**, deney kurulurken seçilen ayardır; örneğin KNN'nin komşu sayısı, PCA bileşeni sayısı, ağaç derinliği, öğrenme oranı veya batch büyüklüğü. Her rapor ilgili seçimleri kendi bağlamında açıklar.

## Ortam ve çalıştırma

Notebook metadata'sında Python **3.12.10** kayıtlıdır. Paket sürümleri dosyalarda tam olarak belirtilmediğinden `requirements.txt`, kaynak kodda kullanılan paketlerin bir listesidir; özgün ortamın sürüm kilidi değildir.

1. Bir Python sanal ortamı oluşturun ve etkinleştirin.
2. PyTorch çalışmalarında donanımınıza uygun kurulumu [resmî PyTorch kurulum sayfasından](https://pytorch.org/get-started/locally/) seçin. Üçüncü notebook CUDA destekli GPU kullanımını zorunlu tutar; dördüncü notebook cihazı otomatik seçer.
3. Paketleri yükleyin:

   ```shell
   python -m pip install -r requirements.txt
   ```

4. [Veri hazırlama rehberindeki](DATA_SETUP.md) klasörleri ve dosya adlarını hazırlayın.
5. İlgili çalışma klasörünü çalışma dizini yaparak Jupyter'ı başlatın:

   ```shell
   cd 03-mlp-mosaic
   python -m jupyterlab
   ```

6. Notebook hücrelerini sırayla çalıştırın. Model aramaları ve çok aşamalı eğitimler uzun sürebilir. Üretilen checkpoint ve sonuç dosyaları aynı deneyin devamında kullanılabilir.

Birinci notebook'un veri yolları Windows biçimindedir. Veri kümeleri, eğitim ağırlıkları ve deney sırasında oluşan dosyalar bu repoya dahil değildir. Tam veri düzeni ve çalışma klasörleri [veri rehberinde](DATA_SETUP.md) açıklanır.

## Deneyleri yorumlama

Raporlar kodda kurulan deneyleri açıklar. Veri artırma veya ön eğitimin yararlı olduğu peşinen varsayılmaz. Çalışmaların veri ayrımları, model aileleri ve eğitim düzenleri farklıdır; farklı notebook'lardaki değerler tek başına kontrollü bir model üstünlüğü karşılaştırması oluşturmaz.

Notebook'ların özgün içerikleri ve kayıtlı çıktıları korunmuştur. Bu düzenleme sırasında yeni eğitim veya çıktıların sayısal doğrulaması yapılmamıştır. Kullanılan veri kaynakları [veri hazırlama rehberinde](DATA_SETUP.md) listelenmiştir.
