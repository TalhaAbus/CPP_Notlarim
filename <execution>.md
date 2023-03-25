- C++17 standartı ile birlikte eklendiği için, henüz kullanımı yaygın değildir. execution başlık dosyası, C++'da paralel algoritmaların tasarımı için bir dizi araç sağlar.

- Bu başlık dosyasındaki ana öğe, std::execution::par ve std::execution::seq adında iki politika sınıfıdır. Bu politika sınıfları, std::for_each, std::transform, std::reduce, std::sort gibi STL algoritmalarının paralel sürümlerinde kullanılabilir.

- std::execution::par politikası, STL algoritmasının paralel sürümünü yürütürken, paralelleştirme yoluyla performans artışı elde etmek için birden fazla iş parçacığı kullanılmasına izin verir. std::execution::seq politikası ise sıralı bir şekilde yürütülür.

- Ayrıca, std::execution::unseq politikası da mevcuttur ve bu politika, algoritmanın döngüsel bir şekilde yürütülmesine izin vererek vektörizasyon ve diğer optimizasyon tekniklerini kullanır. Ancak, bu politika sınıfı, algoritmanın yan etkilerinin olmadığı durumlarda yalnızca kullanılmalıdır.

- std::execution başlık dosyası ayrıca, std::parallel_invoke adında bir fonksiyon da sağlar. Bu fonksiyon, birden çok işlevi eşzamanlı olarak çağırmak için kullanılabilir.

- Özetle, execution başlık dosyası, STL algoritmalarının paralel sürümlerinin tasarımını ve uygulanmasını kolaylaştıran araçlar sağlar.

- <execution> başlık dosyası, C++20 ile birlikte sunulan yürütme politikalarını (execution policies) tanımlar. Bu politikalar, özellikle paralel algoritmaların performansını artırmak için kullanılır.

- Aşağıdaki örnekte, std::execution::par kullanılarak bir vektördeki tüm elemanların toplamı hesaplanmaktadır. std::execution::par, paralel yürütme politikasıdır ve işlemleri otomatik olarak paralelleştirir.

```CPP
#include <iostream>
#include <vector>
#include <numeric>
#include <execution>

int main() {
  std::vector<int> v(1000000, 1);

  auto result = std::reduce(std::execution::par, v.begin(), v.end());

  std::cout << "Result: " << result << '\n';
}

```

- Bu örnekte, std::reduce fonksiyonu kullanılarak std::execution::par yürütme politikasıyla birlikte vektördeki tüm elemanların toplamı hesaplanmaktadır. std::execution::par kullanımı, işlemleri otomatik olarak paralelleştirmeye yarar.

- Bu örnekte sadece std::execution::par kullanılmış olsa da, <execution> başlık dosyası, paralel algoritmaların yürütme hızını artırmak için bir dizi yürütme politikası sunar. Bunlar şunlardır:

- **std::execution::seq:** Sıralı yürütme politikasıdır.
- **std::execution::par:** Paralel yürütme politikasıdır.
- **std::execution::par_unseq:** Paralel ve sırasız yürütme politikasıdır.
- **std::execution::unseq:** Sırasız yürütme politikasıdır.
- Bu yürütme politikaları, paralel algoritmaların performansını artırmak için kullanılabilir. Ancak, paralelleştirme işlemi, belirli bir işlem yükü altında avantajlı olur. Küçük veri setleri için paralelleştirme işlemi, sıralı işleme göre daha yavaş olabilir.

# islemleri paralellestirmak ne demek

- İşlemleri paralelleştirme, bir görevi daha hızlı bir şekilde tamamlamak için birden çok işlemci veya işlem birimini kullanarak işlemleri aynı anda yürütmeyi ifade eder. Bu, bir işlemci birden çok işlemi aynı anda işleyebildiği için işlemlerin daha hızlı tamamlanmasını sağlar. Bu özellikle büyük veri işleme, makine öğrenimi ve benzeri alanlarda faydalıdır.













































