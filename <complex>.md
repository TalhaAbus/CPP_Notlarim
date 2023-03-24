- std::complex sınıfı, C++ standart kütüphanesinde yer alan bir sınıftır ve kompleks sayıları temsil etmek için kullanılır. Kompleks sayılar, gerçek ve sanal bileşenlere sahip sayılardır ve matematiksel işlemlerde sıklıkla kullanılır.

- std::complex sınıfı, bir gerçek sayı ve bir sanal sayı olmak üzere iki bileşenden oluşur. Bu bileşenler, genellikle std::complex<double, std::complex<float veya std::complex<long double türlerinde tanımlanırlar.

- std::complex sınıfı, birçok aritmetik işlemi (toplama, çıkarma, çarpma, bölme vb.) destekler ve ayrıca birçok matematiksel işlevi (karekök alma, trigonometrik işlemler, logaritmalar, vb.) de destekler.

- İşte bir örnek:

```CPP
#include <iostream>
#include <complex>

int main() {
    // İki kompleks sayı oluşturma
    std::complex<double> z1(1.0, 2.0);
    std::complex<double> z2(3.0, 4.0);

    // Toplama işlemi
    std::complex<double> sum = z1 + z2;

    // Çıkarma işlemi
    std::complex<double> diff = z1 - z2;

    // Çarpma işlemi
    std::complex<double> prod = z1 * z2;

    // Bölme işlemi
    std::complex<double> quot = z1 / z2;

    // Sonuçları yazdırma
    std::cout << "Toplam: " << sum << std::endl;
    std::cout << "Fark: " << diff << std::endl;
    std::cout << "Çarpım: " << prod << std::endl;
    std::cout << "Bölüm: " << quot << std::endl;

    return 0;
}

```

- Bu örnekte, iki kompleks sayı oluşturulur ve sonra dört aritmetik işlem yapılır (toplama, çıkarma, çarpma ve bölme). Sonuçlar, std::cout çıktı akışı kullanılarak yazdırılır.

- std::complex sınıfı, bilimsel hesaplama, mühendislik uygulamaları ve diğer matematiksel problemler için oldukça kullanışlıdır.

# Bu sinif kompleks sayilar haricinde kullanilabilir mi? 

- std::complex sınıfı, kompleks sayıları temsil etmek için tasarlanmış olsa da, diğer kullanımlar için de uyarlanabilir.

- Örneğin, std::complex sınıfı, gerçek sayıların çift sayılılarla modüler aritmetiği gibi işlemleri gerçekleştiren bazı algoritmalar için kullanılabilir. Böyle bir durumda, std::complex sınıfının sanal kısmı kullanılmadan, gerçek sayılar sadece kullanılabilir.

- Aşağıda, gerçek sayılarla çalışan bir std::complex örneği verilmiştir:

```CPP
#include <iostream>
#include <complex>

int main() {
    // Gerçek sayıları kullanarak bir std::complex nesnesi oluşturma
    std::complex<double> real_num(2.0, 0.0);

    // Gerçek sayı ile işlem yapma
    std::complex<double> sum = real_num + 3.0;

    // Sonucu yazdırma
    std::cout << "Toplam: " << sum << std::endl;

    return 0;
}

```


> Bu örnekte, bir std::complex nesnesi, gerçek sayılarla oluşturulur ve gerçek sayılarla işlem yapılır. std::complex sınıfı, gerçek sayıların işlem yapılabilmesi için sanal kısmı 0 olarak ayarlar.
