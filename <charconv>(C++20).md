- C++17 standartı ile birlikte, <charconv> başlık dosyası, sayısal verilerin karakter dizilerine dönüştürülmesi ve karakter dizilerinin sayısal verilere dönüştürülmesi için kullanılan işlevleri içerir.

- Özellikle, std::from_chars ve std::to_chars işlevleri, sayısal veri tipleri ve karakter dizileri arasında dönüştürmeler yapmak için kullanılır. Bu işlevler, önceki C++ standartlarında yer alan atoi, atof, sprintf ve sscanf işlevlerine kıyasla daha güvenlidir.

- std::from_chars işlevi, karakter dizisinden sayısal bir değer çıkarmak için kullanılır. Bu işlev, bir karakter dizisi, bir pointer ve bir son pointer alır. Bu pointerlar, karakter dizisinin hangi kısımlarının işlev tarafından işlenmiş olduğunu gösterir. İşlev başarılı olursa, pointerlar işlevin işlenmiş olan kısmını gösterir. Bu işlev, C++17 öncesi sürümlerde sadece std::strtol işleviyle mümkündü.

- std::to_chars işlevi ise sayısal bir değeri karakter dizisine dönüştürmek için kullanılır. Bu işlev, bir sayısal değer, bir karakter dizisi, bir son pointer ve bir taban alır. İşlev, karakter dizisindeki sayıyı temsil eden karakter sayısını döndürür ve son pointer, işlevin karakter dizisindeki sayıyı temsil eden son karakterin sonrasını gösterir. Bu işlev, C++17 öncesi sürümlerde sadece std::sprintf işleviyle mümkündü.

- Ayrıca, <charconv> başlık dosyası, std::chars_format ve std::to_chars_result gibi diğer yardımcı işlevler de sağlar.

- Aşağıdaki örnek, std::from_chars ve std::to_chars işlevlerinin kullanımını göstermektedir:

```CPP
#include <cassert>
#include <charconv>
#include <iomanip>
#include <iostream>
#include <optional>
#include <string_view>
#include <system_error>
 
int main()
{
    for (std::string_view const str : {"1234", "15 foo", "bar", " 42", "5000000000"})
    {
        std::cout << "String: " << std::quoted(str) << ". ";
        int result{};
        auto [ptr, ec] { std::from_chars(str.data(), str.data() + str.size(), result) };
 
        if (ec == std::errc())
            std::cout << "Result: " << result << ", ptr -> " << std::quoted(ptr) << '\n';
        else if (ec == std::errc::invalid_argument)
            std::cout << "That isn't a number.\n";
        else if (ec == std::errc::result_out_of_range)
            std::cout << "This number is larger than an int.\n";
    }
 
    // C++23's constexpr from_char demo:
    auto to_int = [](std::string_view s) -> std::optional<int>
    {
        if (int value; std::from_chars(s.begin(), s.end(), value).ec == std::errc{})
            return value;
        else
            return std::nullopt;
    };
 
    assert(to_int("42") == 42);
    assert(to_int("foo") == std::nullopt);
    #if __cpp_lib_constexpr_charconv and __cpp_lib_optional >= 202106
    static_assert(to_int("42") == 42);
    static_assert(to_int("foo") == std::nullopt);
    #endif
}
```
- Cikti:
```
String: "1234". Result: 1234, ptr -> ""
String: "15 foo". Result: 15, ptr -> " foo"
String: "bar". That isn't a number.
String: " 42". That isn't a number.
String: "5000000000". This number is larger than an int.
```
    
**Ornek:**
    
```CPP
#include <array>
#include <charconv>
#include <iostream>
#include <string_view>
#include <system_error>
 
void show_to_chars(auto... format_args)
{
    std::array<char, 10> str;
 
    if (auto [ptr, ec]
            = std::to_chars(str.data(), str.data() + str.size(), format_args...);
        ec == std::errc())
        std::cout << std::string_view(str.data(), ptr) << '\n';
    else
        std::cout << std::make_error_code(ec).message() << '\n';
}
 
int main()
{
    show_to_chars(42);
    show_to_chars(+3.14159F);
    show_to_chars(-3.14159, std::chars_format::fixed);
    show_to_chars(-3.14159, std::chars_format::scientific, 3);
    show_to_chars(3.1415926535, std::chars_format::fixed, 10);
} 
```
    
- Cikti:

```CPP
42
3.14159
-3.14159
-3.142e+00
Value too large for defined data type
```
    
    
    
    
    
    
    
    
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


