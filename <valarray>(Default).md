- valarray başlık dosyası, "value arrays" olarak adlandırılan matematiksel işlemler için bir dizi sınıf ve işlev sağlar. Bir valarray nesnesi, bellek yerine matematiksel işlemleri vurgulayan verileri depolamak için kullanılır. Bu nesne türleri özellikle büyük veriler üzerinde hızlı ve etkili işlemler gerçekleştirmek için tasarlanmıştır.

Bazı örnek işlevler şunları içerir:

- std::valarray::apply(): Belirtilen işlevi bir valarray nesnesinin her elemanına uygular.
- std::valarray::sum(): Bir valarray nesnesinin elemanlarının toplamını hesaplar.
- std::valarray::min(): Bir valarray nesnesinin en küçük elemanını bulur.
- std::valarray::max(): Bir valarray nesnesinin en büyük elemanını bulur.
- std::valarray::size(): Bir valarray nesnesinin boyutunu döndürür.

- Bu sınıfların ve işlevlerin kullanımı matematiksel işlemler gerektiren uygulamalar için yararlı olabilir, özellikle büyük veri setleri üzerinde hızlı işlemler gerçekleştirmek gerektiğinde.

- Aşağıdaki örnek, iki adet valarray nesnesi oluşturur ve bunların elemanları toplanarak üçüncü bir valarray nesnesine atanır:

```CPP
#include <iostream>
#include <valarray>

int main() {
    std::valarray<int> v1 = {1, 2, 3, 4, 5};
    std::valarray<int> v2 = {6, 7, 8, 9, 10};
    std::valarray<int> v3 = v1 + v2;

    for (auto elem : v3) {
        std::cout << elem << " ";
    }

    return 0;
}

```

> Bu örnekte, valarray sınıfı sayesinde, iki dizi elemanlarının toplamı üçüncü bir diziye atanabildi.

- valarray'ın performansı, diğer STL konteynırlarından daha hızlıdır. Bunun nedeni, özellikle matematiksel hesaplamalar için optimize edilmiş işlemler içermesidir. Ancak, bu avantajın kullanılabilmesi için, işlemlerin C++ standart kütüphanesi tarafından sunulan yerleşik veri türlerinde (örneğin, double, float) gerçekleştirilmesi gerekir. Özel bir veri türü gerektiren özel işlemler durumunda performans düşük olabilir.
- Özel bir veri türü, standart C++ veri türleri arasında yer almaz ve kullanıcının ihtiyacına göre özel olarak tanımlanmış bir veri türüdür. Özel veri türleri, örneğin bir oyun programlama kütüphanesi gibi belirli bir uygulama için özelleştirilmiş bir veri yapısı veya sınıfı olabilir. Özel veri türleri, belirli bir amaca yönelik olarak optimize edilebilir ve daha yüksek performans sağlayabilir.


```CPP
int main() {

	std::valarray<int> myArray{ 1,2,3, 4};


	auto ex = myArray.sum();

	std::cout << ex;
}
```





































