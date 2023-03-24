# numeric

- numeric başlık dosyası, C++ standart kütüphanesinin bir parçasıdır ve sayısal algoritmalar için bir dizi işlev sağlar. Bu başlık dosyası, çeşitli aritmetik işlemler yapmak ve sayısal verileri işlemek için işlevler içerir. Bazı işlevler aşağıdaki gibidir:

- **std::accumulate()**: Verilen bir aralıktaki değerleri birleştirir.
- **std::iota()**: Verilen bir aralığı, ardışık sayılarla doldurur.
- **std::partial_sum()**: Bir aralıktaki değerlerin birikimli toplamını hesaplar.
- **std::adjacent_difference()**: Bir aralıktaki elemanların ardışık farklarını hesaplar.
- **std::inner_product()**: İki aralıktaki değerlerin iç çarpımını hesaplar.

- Bu işlevler, sayısal verilerle çalışmak için yararlı olabilir. Örneğin, std::accumulate() işlevi, bir dizi sayıyı toplamak için kullanılabilir. Benzer şekilde, std::iota() işlevi, bir dizi indeksi sırayla doldurmak için kullanılabilir. std::partial_sum() işlevi, bir dizi sayının birikimli toplamını hesaplamak için kullanılabilir. std::adjacent_difference() işlevi, bir dizideki ardışık elemanların farkını hesaplamak için kullanılabilir. std::inner_product() işlevi ise, iki dizinin iç çarpımını hesaplamak için kullanılabilir

# std::accumulate()

- std::accumulate() işlevi, C++ numeric başlık dosyasında tanımlanmış bir işlevdir ve bir aralıktaki elemanların toplamını hesaplar.

İşlev şu şekilde tanımlanır:

```CPP
template< class InputIt, class T >
T accumulate( InputIt first, InputIt last, T init );

```

- Burada, first ve last aralığı tanımlayan iki iteratör, init ise hesaplama işlemi için başlangıç değeridir. init değeri, aralıktaki elemanların türüne dönüştürülebilir olmalıdır.

- İşlevin kullanımı şu şekildedir:

```CPP
#include <iostream>
#include <numeric>
#include <vector>

int main() {
    std::vector<int> v = {1, 2, 3, 4, 5};

    int sum = std::accumulate(v.begin(), v.end(), 0);

    std::cout << "Toplam: " << sum << std::endl;

    return 0;
}

```

- Bu örnekte, std::vector sınıfı kullanılarak bir tamsayı vektörü tanımlanır. Sonra, std::accumulate() işlevi kullanılarak vektördeki elemanların toplamı hesaplanır ve sum değişkenine atanır. Son olarak, hesaplanan toplam std::cout kullanılarak ekrana yazdırılır.

- Bu örnekte, std::accumulate() işlevi, vektördeki elemanların toplamını hesaplamak için kullanılmıştır. Ancak, aynı işlev başka amaçlarla da kullanılabilir. Örneğin, bir vektördeki en büyük veya en küçük elemanı bulmak için de kullanılabilir.\

# std::iota()

- std::iota() işlevi, C++ numeric başlık dosyasında tanımlanmış bir işlevdir ve belirtilen aralıktaki değerleri artan bir şekilde atar.

- İşlev şu şekilde tanımlanır:


```CPP
  template< class ForwardIt, class T >
void iota( ForwardIt first, ForwardIt last, T value );

```
- Burada, first ve last aralığı tanımlayan iki iteratör ve value ise ilk değerdir. İşlev, value değerinden başlayarak aralıktaki her bir elemana sırasıyla artan bir şekilde değer atar.

- İşlevin kullanımı şu şekildedir:

```CPP
#include <iostream>
#include <numeric>
#include <vector>

int main() {
    std::vector<int> v(10);

    std::iota(v.begin(), v.end(), 1);

    for (auto x : v) {
        std::cout << x << " ";
    }

    return 0;
}

```
- Bu örnekte, std::vector sınıfı kullanılarak bir tamsayı vektörü tanımlanır. std::iota() işlevi kullanılarak vektöre 1'den 10'a kadar olan sayılar atanır. Son olarak, for döngüsü kullanılarak vektördeki elemanlar ekrana yazdırılır.

- Bu örnekte, std::iota() işlevi, vektördeki elemanlara artan bir şekilde değer atamak için kullanılmıştır. Ancak, aynı işlev başka amaçlarla da kullanılabilir. Örneğin, bir vektördeki elemanların sırasını değiştirmek için de kullanılabilir.

# std::partial_sum()

- std::partial_sum() işlevi, C++ numeric başlık dosyasında tanımlanmış bir işlevdir ve bir aralıktaki elemanların öncelikle toplamı ardından sonuç dizisinde birikimli olarak depolanmasını sağlar.

- İşlevin imzası aşağıdaki gibidir:

```CPP
template< class InputIt, class OutputIt >
OutputIt partial_sum( InputIt first, InputIt last, OutputIt d_first );

```

- Burada, first ve last aralığı tanımlayan iki iteratör ve d_first, sonuçların depolanacağı çıkış aralığının başlangıcını tanımlayan bir iteratördür.

- ::partial_sum() işlevi, girdi aralığındaki her elemanın önceki elemanlarla toplanmasıyla elde edilen birikimli toplam dizisini d_first aralığına yazar.

- İşlevin kullanımı şu şekildedir:


```CPP
#include <iostream>
#include <numeric>
#include <vector>

int main() {
    std::vector<int> v = {1, 2, 3, 4, 5};
    std::vector<int> result(v.size());

    std::partial_sum(v.begin(), v.end(), result.begin());

    for (auto x : result) {
        std::cout << x << " ";
    }

    return 0;
}

```

- Bu örnekte, std::vector sınıfı kullanılarak bir tamsayı vektörü tanımlanır. std::partial_sum() işlevi kullanılarak vektördeki elemanların birikimli toplamı result vektörüne atanır. Son olarak, for döngüsü kullanılarak result vektöründeki elemanlar ekrana yazdırılır.

- Bu örnekte, std::partial_sum() işlevi, vektördeki elemanların birikimli toplamlarını hesaplamak için kullanılmıştır. Ancak, aynı işlev başka amaçlarla da kullanılabilir. Örneğin, bir vektördeki elemanların kümülatif çarpımını hesaplamak için de kullanılabilir.

# std::adjacent_difference()

- std::adjacent_difference() işlevi, C++ numeric başlık dosyasında tanımlanmış bir işlevdir ve bir aralıktaki elemanların ardışık farklarını hesaplar.

- İşlevin imzası aşağıdaki gibidir:

```CPP

template< class InputIt, class OutputIt >
OutputIt adjacent_difference( InputIt first, InputIt last, OutputIt d_first );

```
- Burada, first ve last aralığı tanımlayan iki iteratör ve d_first, sonuçların depolanacağı çıkış aralığının başlangıcını tanımlayan bir iteratördür.

- std::adjacent_difference() işlevi, girdi aralığındaki her elemanın bir önceki elemandan çıkarılmasıyla elde edilen ardışık fark dizisini d_first aralığına yazar. İlk eleman doğrudan first aralığından kopyalanır.

- İşlevin kullanımı şu şekildedir:

```CPP
#include <iostream>
#include <numeric>
#include <vector>

int main() {
    std::vector<int> v = {1, 2, 3, 4, 5};
    std::vector<int> result(v.size());

    std::adjacent_difference(v.begin(), v.end(), result.begin());

    for (auto x : result) {
        std::cout << x << " ";
    }

    return 0;
}

```

- Bu örnekte, std::vector sınıfı kullanılarak bir tamsayı vektörü tanımlanır. std::adjacent_difference() işlevi kullanılarak vektördeki elemanların ardışık farkları result vektörüne atanır. Son olarak, for döngüsü kullanılarak result vektöründeki elemanlar ekrana yazdırılır.

- Bu örnekte, std::adjacent_difference() işlevi, vektördeki elemanların ardışık farklarını hesaplamak için kullanılmıştır. Ancak, aynı işlev başka amaçlarla da kullanılabilir. Örneğin, bir vektördeki elemanların ardışık oranlarını hesaplamak için de kullanılabilir.

# std::inner_product()

- std::inner_product() işlevi, C++ numeric başlık dosyasında tanımlanmış bir işlevdir ve iki aralıktaki elemanların skaler çarpımını hesaplar.

- İşlevin imzası aşağıdaki gibidir:


```CPP
template< class InputIt1, class InputIt2, class T >
T inner_product( InputIt1 first1, InputIt1 last1, InputIt2 first2, T init );

```

- Burada, first1 ve last1 aralığı tanımlayan iki iteratör, first2, ikinci aralığı tanımlayan bir iteratör ve init, hesaplamanın başlangıç değerini tanımlayan bir değerdir.

- std::inner_product() işlevi, her iki aralıktaki elemanları, init değeriyle başlayarak skaler çarpımını hesaplar. Skaler çarpım, elemanların sırayla çarpılması ve toplanması yoluyla elde edilir. İşlevin sonuç değeri, skaler çarpımın sonucudur.

- İşlevin kullanımı şu şekildedir:


```CPP

#include <iostream>
#include <numeric>
#include <vector>

int main() {
    std::vector<int> v1 = {1, 2, 3, 4, 5};
    std::vector<int> v2 = {10, 20, 30, 40, 50};

    int result = std::inner_product(v1.begin(), v1.end(), v2.begin(), 0);

    std::cout << "Inner product = " << result << std::endl;

    return 0;
}

```

- Bu örnekte, std::vector sınıfı kullanılarak iki tamsayı vektörü tanımlanır. std::inner_product() işlevi kullanılarak, her iki vektördeki elemanların skaler çarpımı hesaplanır. Son olarak, sonuç ekrana yazdırılır.

- Bu örnekte, std::inner_product() işlevi, iki vektördeki elemanların skaler çarpımını hesaplamak için kullanılmıştır. Ancak, aynı işlev başka amaçlarla da kullanılabilir. Örneğin, iki vektördeki elemanların iç çarpımını hesaplamak için de kullanılabilir.

































