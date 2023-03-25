- C++20 ile birlikte, <numbers> başlık dosyası eklendi ve matematiksel sabitler ve işlevler için standart bir kütüphane sağlandı. Bu başlık dosyası, özellikle bilimsel hesaplama, fizik, matematik ve diğer hesaplama yoğun uygulamaları için yararlıdır.

- Bu başlık dosyası, iki ana bölümden oluşur:

- Matematiksel sabitler: Pi (π), e, log2 (2'nin logaritması), log10 (10'un logaritması) vb. Bu sabitler, double ve float türleri için standart doğrulukta sağlanır.

- Matematiksel işlevler: Bölme, üs alma, logaritma, kök alma, trigonometrik işlevler, hiperbolik işlevler vb. Bu işlevler, tam sayı, kayan noktalı sayı veya karmaşık sayı türleri için sağlanır.

```CPP
C++20 ile birlikte, <numbers> başlık dosyası eklendi ve matematiksel sabitler ve işlevler için standart bir kütüphane sağlandı. Bu başlık dosyası, özellikle bilimsel hesaplama, fizik, matematik ve diğer hesaplama yoğun uygulamaları için yararlıdır.

Bu başlık dosyası, iki ana bölümden oluşur:

Matematiksel sabitler: Pi (π), e, log2 (2'nin logaritması), log10 (10'un logaritması) vb. Bu sabitler, double ve float türleri için standart doğrulukta sağlanır.

Matematiksel işlevler: Bölme, üs alma, logaritma, kök alma, trigonometrik işlevler, hiperbolik işlevler vb. Bu işlevler, tam sayı, kayan noktalı sayı veya karmaşık sayı türleri için sağlanır.
```

- Çıktı:

```CPP
Pi: 3.14159
e: 2.71828
log2(e): 1.4427
sqrt(2): 1.41421
sin(pi/2): 1
log10(1000): 3

```

- C++20 standartlarına dahil olan <numbers> başlık dosyası, sabit sayılar ve matematiksel sabitler için önceden tanımlanmış bir dizi işlev ve sabitler içerir. Bu başlık dosyasındaki sabitler, kullanıcıların kodlarında doğrudan kullanılabilecek matematiksel sabitleri içerir.

- Bu başlık dosyasındaki sabitler, herhangi bir yerel tanım yerine, sabitlerin doğrudan kullanımını kolaylaştırarak kullanımı basitleştirmek için kullanılabilir. Ayrıca, kullanıcılara sabitlerin doğru değerini kullanmalarını sağlar.

- Bu başlık dosyası, C++ programcılarına doğrudan C matematik kütüphanesi sabitlerine erişme olanağı sağlar. Ayrıca, kodun okunurluğunu artırmak için sabitlerin adlarını kullanmanızı sağlar.

- Örnek olarak, pi sayısı sabiti <numbers> başlık dosyası içerisinde bulunur. Aşağıdaki kod örneği pi sayısını hesaplayarak kullanıcılara göstermektedir:
```CPP
#include <iostream>
#include <numbers>

int main()
{
    double pi = std::numbers::pi;
    std::cout << "Pi sayisi: " << pi << std::endl;

    return 0;
}

```

- Bu kod örneği, <numbers> başlık dosyasının pi sabiti kullanarak pi sayısını hesaplar ve ekrana yazdırır. Bu şekilde, kullanıcılar sabitleri doğrudan kullanarak matematiksel sabitleri hesaplayabilirler.

- <numbers> kütüphanesi, özel bir fonksiyon ve sınıf koleksiyonudur. Bu başlık dosyası, sabit sayılar, matematiksel sabitler ve işlevler sağlar. Bu koleksiyonun birkaç örneği şunlardır:

- **pi ve e matematik sabitleri**
- **std::numbers::sqrt2, std::numbers::sqrt3, std::numbers::golden_ratio gibi diğer sabitler**
- **std::numbers::log2, std::numbers::log10, std::numbers::ln2, std::numbers::ln10 gibi diğer matematiksel sabitler**
- **std::numbers::abs, std::numbers::floor, std::numbers::ceil, std::numbers::round gibi diğer matematiksel işlevler**
- Bu sabitler ve işlevler, matematiksel hesaplamalar gibi birçok alanda kullanılabilir. Ayrıca, özellikle derleme zamanında sabit olması gereken programlar için de kullanılabilirler.

Örnek kullanımlar şunlar olabilir:

```CPP
#include <iostream>
#include <numbers>

int main() {
    std::cout << "pi: " << std::numbers::pi << '\n';
    std::cout << "sqrt(2): " << std::numbers::sqrt2 << '\n';
    std::cout << "abs(-10): " << std::numbers::abs(-10) << '\n';
    
    return 0;
}

```
- Bu örnekte, std::numbers kullanılarak pi, sqrt2 ve abs sabitleri ve işlevleri çağrılmaktadır.



