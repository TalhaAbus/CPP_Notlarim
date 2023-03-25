# algorithm

- Algorithm C++ standart kütüphanesinde bir container değildir. Tam tersine, algorithm sınıfı, C++ standart kütüphanesinde bulunan bir header dosyasıdır ve STL (Standard Template Library) için kullanılan bir dizi algoritma fonksiyonu sağlar.

- Bu algoritma fonksiyonları, STL'nin temel container sınıfları olan vector, list, set, map gibi sınıflarla birlikte kullanılabilir. algorithm sınıfı, bu container sınıflarının içeriğinde gezinmek ve bu içerikler üzerinde çeşitli işlemler yapmak için kullanılır.

- Örneğin, std::sort, std::find, std::count_if, std::transform gibi algoritma fonksiyonları, bir vector veya list gibi bir container içeriğindeki verileri sıralamak, aramak, saymak veya dönüştürmek için kullanılabilir.

- İşte std::sort algoritma fonksiyonunun bir örneği:

```CPP
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> vec { 5, 3, 1, 4, 2 };

    // Vector'un elemanlarını sıralama
    std::sort(vec.begin(), vec.end());

    // Sıralanmış vektörü yazdırma
    std::cout << "Sıralanmış vektör: ";
    for (int i : vec) {
        std::cout << i << " ";
    }
    std::cout << std::endl;

    return 0;
}

```

- Bu kodda, önce bir std::vectorint oluşturulur ve bu vektörün içine beş sayı eklenir. Daha sonra, std::sort algoritma fonksiyonu, vec.begin() ve vec.end() aralığında bulunan elemanları sıralar. Son olarak, for döngüsü ile sıralanmış vektör yazdırılır.

- Benzer şekilde, std::find, std::count_if, std::transform gibi diğer algoritma fonksiyonları da bir container içeriğindeki verileri aramak, saymak veya dönüştürmek için kullanılabilir. Örneğin:

```CPP
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> vec { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };

    // Vector'deki tek sayıların sayısını bulma
    int tek_sayi_sayisi = std::count_if(vec.begin(), vec.end(), [](int x) { return x % 2 != 0; });

    // Vector'deki her elemanı iki katına çıkarma
    std::transform(vec.begin(), vec.end(), vec.begin(), [](int x) { return x * 2; });

    // Yeni vektörü yazdırma
    std::cout << "Yeni vektör: ";
    for (int i : vec) {
        std::cout << i << " ";
    }
    std::cout << std::endl;

    return 0;
}

```
> Bu kodda, önce bir std::vectorint oluşturulur ve bu vektörün içine 1'den 10'a kadar olan sayılar eklenir. Daha sonra, std::count_if algoritma fonksiyonu, vec.begin() ve vec.end() aralığında bulunan elemanlar arasında gezinerek, tek sayıların sayısını hesaplar. std::transform algoritma fonksiyonu ise, vec.begin() ve vec.end() aralığındaki her elemanı iki katına çıkarır. Son olarak, for döngüsü ile yeni vektör yazdırılır.
