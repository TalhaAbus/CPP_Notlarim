- C++17 standartı ile birlikte, <charconv> başlık dosyası, sayısal verilerin karakter dizilerine dönüştürülmesi ve karakter dizilerinin sayısal verilere dönüştürülmesi için kullanılan işlevleri içerir.

- Özellikle, std::from_chars ve std::to_chars işlevleri, sayısal veri tipleri ve karakter dizileri arasında dönüştürmeler yapmak için kullanılır. Bu işlevler, önceki C++ standartlarında yer alan atoi, atof, sprintf ve sscanf işlevlerine kıyasla daha güvenlidir.

- std::from_chars işlevi, karakter dizisinden sayısal bir değer çıkarmak için kullanılır. Bu işlev, bir karakter dizisi, bir pointer ve bir son pointer alır. Bu pointerlar, karakter dizisinin hangi kısımlarının işlev tarafından işlenmiş olduğunu gösterir. İşlev başarılı olursa, pointerlar işlevin işlenmiş olan kısmını gösterir. Bu işlev, C++17 öncesi sürümlerde sadece std::strtol işleviyle mümkündü.

- std::to_chars işlevi ise sayısal bir değeri karakter dizisine dönüştürmek için kullanılır. Bu işlev, bir sayısal değer, bir karakter dizisi, bir son pointer ve bir taban alır. İşlev, karakter dizisindeki sayıyı temsil eden karakter sayısını döndürür ve son pointer, işlevin karakter dizisindeki sayıyı temsil eden son karakterin sonrasını gösterir. Bu işlev, C++17 öncesi sürümlerde sadece std::sprintf işleviyle mümkündü.

- Ayrıca, <charconv> başlık dosyası, std::chars_format ve std::to_chars_result gibi diğer yardımcı işlevler de sağlar.

- Aşağıdaki örnek, std::from_chars ve std::to_chars işlevlerinin kullanımını göstermektedir:

```CPP
#include <iostream>
#include <charconv>

int main()
{
    char str[] = "1234";
    int n;

    // Convert string to integer
    auto result = std::from_chars(str, str + sizeof(str), n);

    if (result.ec == std::errc()) {
        std::cout << "Converted number: " << n << '\n';
    }

    // Convert integer to string
    char buf[10];
    auto ptr = std::to_chars(buf, buf + sizeof(buf), n);

    *ptr = '\0';
    std::cout << "Converted string: " << buf << '\n';

    return 0;
}

```
> Bu örnekte, "1234" karakter dizisi önce std::from_chars işlevi kullanılarak bir tamsayıya dönüştürülür ve sonrasında std::to_chars işlevi kullanılarak tekrar karakter dizisine dönüştürülür.

# Bu baslik dosyasi hangi fonksiyon ve siniflari iceriyor

- <charconv> başlık dosyası, C++17 ile birlikte eklenen, karakter dizileriyle sayısal değerler arasında dönüşümler yapmak için kullanılan bir dizi işlevi içerir. Bu işlevler, sayısal değerleri karakter dizilerine dönüştürmek veya karakter dizilerini sayısal değerlere dönüştürmek için kullanılır. <charconv> başlık dosyası ayrıca, sayısal değerleri değiştirmeden, sayısal bir veriyi farklı bir veri türüne dönüştürmek için kullanılan std::from_chars ve std::to_chars işlevlerini de içerir.

- charconv başlık dosyası, C++17 ile birlikte tanıtılan bir başlık dosyasıdır ve karakterlerin sayılara ve sayıların karakterlere dönüştürülmesini sağlar. Bu başlık dosyası, std::to_chars ve std::from_chars işlevleriyle birlikte çalışan dönüştürme işlemleri için gerekli işlevler ve sabitler sağlar.

- Bu başlık dosyasındaki ana sınıflar ve işlevler aşağıdaki gibidir:

- **std::to_chars()** - Bir sayıyı karakter dizisine dönüştürür.
- **std::from_chars()** - Bir karakter dizisini sayıya dönüştürür.
- **std::chars_format - std::to_chars()** işlevinde kullanılan sayı formatını belirlemek için kullanılan bir tamsayı numarasıdır. Decimal, hex, scientific ve fixed formatlarına karşılık gelen değerler içerir.
- **std::floating_point** - Float ve double tipi sayıları temsil etmek için kullanılan bir sınıftır. Bu sınıf, ondalık sayıların mantissa ve exponent kısımlarını ayırarak kayan noktalı sayıların tamamen doğru bir şekilde dönüştürülmesini sağlar.
- **std::from_chars_result - std::from_chars()** işlevinden dönen sonuç yapısını temsil eder. Bu yapı, dönüştürülen sayının değerini, sonraki karakterin konumunu ve dönüştürme işleminin başarılı olup olmadığını belirtir.

```CPP
#include <charconv>
#include <iostream>
#include <string>

int main() {
  // std::to_chars() örneği
  int value = 123;
  char buffer[10];
  auto result = std::to_chars(buffer, buffer + sizeof(buffer), value);
  *result.ptr = '\0'; // null karakterini ekle
  std::cout << "Value as string: " << buffer << '\n';

  // std::from_chars() örneği
  std::string str = "456";
  int int_value;
  auto str_end = str.data() + str.size();
  auto [ptr, ec] = std::from_chars(str.data(), str_end, int_value);
  if (ec == std::errc{}) {
    std::cout << "Parsed integer: " << int_value << '\n';
  } else {
    std::cout << "Failed to parse integer\n";
  }

  // std::floating_point örneği
  double f_value = 3.14159265359;
  char f_buffer[100];
  auto f_result = std::to_chars(f_buffer, f_buffer + sizeof(f_buffer), std::floating_point(f_value));
  *f_result.ptr = '\0'; // null karakterini ekle
  std::cout << "Floating point value as string: " << f_buffer << '\n';
}

```

> Son örnekte, string olarak verilen bir ondalık sayıyı, yani float veya double tipindeki bir sayıyı, std::from_chars fonksiyonunu kullanarak, karakter dizisinden sayıya dönüştürdük. Ardından, elde edilen sayının karesini aldık ve sonucu ekrana yazdırdık. std::from_chars fonksiyonu, C-style stringleri sayısal verilere dönüştürmek için kullanılabilen hızlı bir yöntemdir.


