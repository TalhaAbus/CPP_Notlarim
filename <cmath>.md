- <cmath> başlık dosyası, C++ standart kütüphanesinin bir parçasıdır ve matematiksel fonksiyonları içerir. Bu fonksiyonlar, programlama sırasında sıkça kullanılan trigonometrik, logaritmik, üs, karekök, trigonometrik invers, hiperbolik trigonometrik, radyan/derece dönüşümü gibi işlemleri yapmamızı sağlar.

- Başlık dosyasındaki bazı önemli fonksiyonlar şunlardır:

- **sin(), cos(), tan():** Sinüs, kosinüs ve tanjant fonksiyonları.
- **asin(), acos(), atan():** Arcsinüs, arccosinüs ve arktanjant fonksiyonları.
- **sinh(), cosh(), tanh():** Hiperbolik sinüs, kosinüs ve tanjant fonksiyonları.
- **exp():** e üzeri x işlemini yapar.
- **log():** ln(x) işlemini yapar.
- **log10():** log10(x) işlemini yapar.
- **pow():** x üzeri y işlemini yapar.
- **sqrt():** Karekök işlemini yapar.
- **abs(), fabs():** Mutlak değer işlemini yapar.
- **ceil(), floor():** Üste yuvarlama ve alta yuvarlama işlemlerini yapar.
- **fmod():** x mod y işlemini yapar.
Ayrıca, bazı matematiksel sabitler de <cmath> başlık dosyasında tanımlıdır, bunlar:

-**M_PI:** Pi sayısı.
-**M_E::** Euler sabiti.
Örnek olarak, bir çemberin alanını hesaplayan bir program yazalım:

```CPP
#include <iostream>
#include <cmath>

int main() {
    double r = 3.0;
    double area = M_PI * std::pow(r, 2);
    std::cout << "Circle area: " << area << std::endl;
    return 0;
}

```
> Bu programda, M_PI sabiti kullanılarak pi sayısı alınmış ve std::pow() fonksiyonu kullanılarak yarıçapın karesi hesaplanmıştır. Son olarak, hesaplanan alan ekrana yazdırılmıştır.







