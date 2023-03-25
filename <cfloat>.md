- <cfloat> başlık dosyası, ondalık sayılarla ilgili sabitlerin tanımlandığı bir C++ başlık dosyasıdır. Bu sabitler, kayan nokta sayılarının sınırlarını belirleyen minimum ve maksimum değerleri temsil eder.

- Bu başlık dosyası, genellikle sayısal hesaplamalar ve işlemler için kullanılır. Özellikle, sayısal hesaplamalar sırasında sınırları aşma durumlarının kontrolü için kullanılabilir.

- Başlık dosyası aşağıdaki sabitleri içerir:

- **FLT_RADIX:** Ondalık sayı sisteminin tabanını belirtir.
- **FLT_ROUNDS:** Kayan nokta sayılarının yuvarlanma modunu belirler.
- **FLT_DIG:** En az ondalık basamak sayısını temsil eder.
- **FLT_EPSILON:** 1.0 ve en yakın kayan nokta sayısı arasındaki en küçük farkı temsil eder.
- **FLT_MANT_DIG:** Kayan nokta sayısı için en az mantik basamak sayısını temsil eder.
- **FLT_MAX:** Kayan nokta sayısının maksimum değerini temsil eder.
- **FLT_MAX_10_EXP:** FLT_MAX için 10 tabanındaki en büyük üstel sayıyı temsil eder.
- **FLT_MAX_EXP:** FLT_MAX için en büyük üstel sayıyı temsil eder.
- **FLT_MIN:** Kayan nokta sayısının minimum pozitif değerini temsil eder.
- **FLT_MIN_10_EXP:** FLT_MIN için 10 tabanındaki en küçük üstel sayıyı temsil eder.
- **FLT_MIN_EXP:** FLT_MIN için en küçük üstel sayıyı temsil eder.
- **DBL_DIG, DBL_EPSILON, DBL_MANT_DIG, DBL_MAX, DBL_MAX_10_EXP, DBL_MAX_EXP, DBL_MIN, DBL_MIN_10_EXP, DBL_MIN_EXP:** Çift hassasiyetli kayan nokta sayıları için FLT sabitlerine karşılık gelen sabitler.
- Aşağıda <cfloat> başlık dosyası kullanarak bir örnek gösterilmiştir:

```CPP
#include <iostream>
#include <cfloat>

int main() {
    std::cout << "Min float value: " << FLT_MIN << std::endl;
    std::cout << "Max float value: " << FLT_MAX << std::endl;
    std::cout << "Min double value: " << DBL_MIN << std::endl;
    std::cout << "Max double value: " << DBL_MAX << std::endl;
    return 0;
}

```

> Bu örnek, en küçük ve en büyük kayan nokta sayılarını çıktı olarak verir.

# ben neden bu başlık dosyasını kullanayım?

- <cfloat> başlık dosyasını kullanarak, veri tiplerinin sınırlarını öğrenebilirsiniz. Bu bilgileri kullanarak, programlarınızda hata ayıklama yapabilir veya uygun işlemleri yapabilirsiniz. Örneğin, bir programda ondalık sayılar kullanıyorsanız, hangi değerlerin taşacağını ve hangilerinin taşmayacağını bilebilirsiniz. Böylece programınızın doğru bir şekilde çalışmasını sağlayabilirsiniz.




