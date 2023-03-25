- <ratio> başlık dosyası, rasyonel sayıların sabit ifadelerini sağlar. C++11'de tanıtılan bir başlık dosyasıdır. Bir rasyonel sayı, iki tamsayının oranıdır. Örneğin, 1/2, 2/3 gibi.

- Bu başlık dosyası ile, rasyonel sayılarla çalışırken işlemler yapmak daha kolay hale gelir. İki rasyonel sayıyı çarpmak, bölmek, toplamak veya çıkarmak için kullanabilirsiniz. Bu başlık dosyasında bulunan öne çıkan sınıflar arasında std::ratio, std::ratio_add, std::ratio_subtract, std::ratio_multiply, std::ratio_divide, std::ratio_equal, std::ratio_greater, std::ratio_less, std::ratio_greater_equal ve std::ratio_less_equal bulunur.

- Örneğin, 1/3 oranının temsil edilmesi için aşağıdaki kodu yazabilirsiniz:

```CPP
std::ratio<1, 3> myRatio;

```
> Burada std::ratio sınıfı, <1, 3> türünden bir sabit oran nesnesi oluşturur. Bu nesne daha sonra çarpma, bölme, toplama veya çıkarma işlemlerinde kullanılabilir.

- Örneğin, iki oranı çarpmak için std::ratio_multiply kullanabilirsiniz:

```CPP
using myRatio1 = std::ratio<1, 3>;
using myRatio2 = std::ratio<3, 4>;
using myResultRatio = std::ratio_multiply<myRatio1, myRatio2>;
std::cout << myResultRatio::num << "/" << myResultRatio::den << std::endl;

```
- Bu kod, myRatio1 ve myRatio2 oranlarını çarparak sonucu myResultRatio'da saklar. std::cout ifadesi, sonucu ekrana yazdırır.

- Sonuç olarak, <ratio> başlık dosyası, rasyonel sayılarla çalışırken matematiksel işlemleri yapmayı kolaylaştırır.

- Taban birimleri farklı olan iki farklı oranı karşılaştırmak için ratio_equal kullanabiliriz:

```CPP
#include <iostream>
#include <ratio>

int main() {
    using half = std::ratio<1, 2>;
    using quarter = std::ratio<1, 4>;

    if (std::ratio_equal<half, quarter>::value) {
        std::cout << "1/2 and 1/4 are equal ratios.\n";
    } else {
        std::cout << "1/2 and 1/4 are not equal ratios.\n";
    }

    return 0;
}

```
- Çıktı:

```CPP
1/2 and 1/4 are not equal ratios.

```

- Oranları sadeleştirmek için ratio sınıfını kullanabiliriz:

```CPP
#include <iostream>
#include <ratio>

int main() {
    using ratio1 = std::ratio<25, 10>;
    using ratio2 = std::ratio<5, 2>;

    using result = std::ratio_divide<ratio1, ratio2>;

    std::cout << "The result is " << result::num << "/" << result::den << "\n";

    return 0;
}

```

- Çıktı:

```CPP
The result is 5/2

```

- duration sınıfı, ratio sınıfını kullanarak sürelerin ölçü birimlerini belirleyebilir:

```CPP
#include <iostream>
#include <chrono>

int main() {
    using namespace std::chrono;

    using my_minutes = duration<int, std::ratio<60>>;
    using my_hours = duration<int, std::ratio<60*60>>;
    using my_days = duration<int, std::ratio<60*60*24>>;

    my_minutes m(60);
    my_hours h(2);
    my_days d(3);

    std::cout << "60 minutes is equal to " << h.count() << " hours.\n";
    std::cout << "3 days is equal to " << d.count() << " days or " << (d/m).count() << " minutes.\n";

    return 0;
}

```
- Çıktı:

```CPP
60 minutes is equal to 2 hours.
3 days is equal to 3 days or 4320 minutes.

```


































