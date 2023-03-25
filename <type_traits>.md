- C++ programlamada tür bilgilerini sorgulamak için kullanılan bir başlık dosyası olan <type_traits>, SFINAE (Substitution Failure Is Not An Error) tekniği ile birlikte kullanılarak, tür şablonlarında koşullu durumlar oluşturmak için yararlı özellikler sağlar.

- Bu başlık dosyası altında tanımlanan type_traits sınıfı, türlerin özelliklerini sorgulamak için kullanılan bir dizi fonksiyon ve sınıf sağlar. Örneğin, std::is_pointer sınıfı bir türün bir işaretçi olup olmadığını belirlemek için kullanılabilir.

- <type_traits> başlık dosyası altında tanımlanan bazı sınıflar ve fonksiyonlar şunlardır:

- **std::is_void:** Bir türün void olup olmadığını belirlemek için kullanılır.
- **std::is_pointer:** Bir türün bir işaretçi olup olmadığını belirlemek için kullanılır.
- **std::is_integral:** Bir türün tamsayı (integer) olup olmadığını belirlemek için kullanılır.
- **std::is_floating_point:** Bir türün kayan nokta (floating-point) sayı olup olmadığını belirlemek için kullanılır.
- **std::is_array:** Bir türün bir dizi olup olmadığını belirlemek için kullanılır.
- **std::is_function:** Bir türün bir işlev olup olmadığını belirlemek için kullanılır.
- **std::enable_if:** Belirli bir koşul sağlandığında, bir işlevin veya sınıfın geçerli olması için kullanılır.
- Bu sınıfların kullanımı, bir türün özelliklerini belirleyerek işlemler gerçekleştirmek için oldukça yararlıdır. Örneğin, bir şablon sınıfın özel bir türde kullanılabilmesi için belirli bir özellik göstermesi gerekiyorsa, std::enable_if kullanarak bir kontrol yapılabilir.

- Surekli kullanilan bir ornek olarak, bir sabitin baska bir veri turune donusturulmesi gosterilebilir. Ornegin, bir int sabitini double turune donusturmek istiyorsaniz, static_cast kullanabilirsiniz:

```CPP
int x = 10;
double y = static_cast<double>(x);

```

- Ancak, x veri turu degisirse (ornegin int -> long int), kodunuzun hala calismasi icin static_cast ifadesindeki veri turunu degistirmeniz gerekir. Bu sorunu cozmenin yolu, type_traits kullanimidir:


```CPP
#include <type_traits>
int x = 10;
std::conditional<std::is_same<decltype(x), int>::value, double, long>::type y = x;

```

- Bu ornekte, std::conditional kullanimi, x'in int turunden olup olmadigini kontrol eder. Eger x int ise, y double olacaktir. Aksi takdirde, y long olacaktir. Bu, veri turu degistiginde otomatik olarak duzeltilebilir.

- birkaç örnek verelim:

- is_pointer: Bir türün işaretçi türü olup olmadığını belirler. Örneğin:

```CPP
#include <iostream>
#include <type_traits>

int main() {
  std::cout << std::boolalpha;
  std::cout << std::is_pointer<int>::value << '\n';    // false
  std::cout << std::is_pointer<int*>::value << '\n';   // true
  std::cout << std::is_pointer<float>::value << '\n';  // false
  return 0;
}

```

- is_reference: Bir türün referans türü olup olmadığını belirler. Örneğin:

```CPP
#include <iostream>
#include <type_traits>

int main() {
  std::cout << std::boolalpha;
  std::cout << std::is_reference<int>::value << '\n';       // false
  std::cout << std::is_reference<int&>::value << '\n';      // true
  std::cout << std::is_reference<const float&>::value << '\n';  // true
  return 0;
}

```
- enable_if: Bir şablon türü, belirli bir koşul sağlandığında belirli bir işlemi yapmak için kullanılabilir. Örneğin:

```CPP
#include <iostream>
#include <type_traits>

template <typename T>
typename std::enable_if<std::is_integral<T>::value, bool>::type
is_odd(T i) {
  return bool(i % 2);
}

int main() {
  std::cout << std::boolalpha;
  std::cout << is_odd<int>(2) << '\n';   // false
  std::cout << is_odd<int>(3) << '\n';   // true
  std::cout << is_odd<double>(2.0) << '\n';  // error: no matching function for call to 'is_odd'
  return 0;
}

```

- Bu örnekte, is_odd işlevi yalnızca tamsayı türleri için kullanılabilir ve enable_if, işlevin yalnızca tamsayı türleri için özelleştirilmesine izin verir. Bu nedenle, is_odd işlevi çağrıldığında double türü için bir hata mesajı alırız.

- **is_same:** İki türün aynı olup olmadığını belirler. Örneğin:

```CPP
#include <iostream>
#include <type_traits>

int main() {
  std::cout << std::boolalpha;
  std::cout << std::is_same<int, int>::value << '\n';     // true
  std::cout << std::is_same<int, unsigned int>::value << '\n';  // false
  std::cout << std::is_same<double, double>::value << '\n';  // true
  return 0;
}

```
- Bu örnekte, is_same işlevi, iki türün aynı olup olmadığını belirler. İlk örnekte, int türü, int türüyle aynı olduğundan, is_same işlevi doğru olarak değerlendirir. Ancak, ikinci örnekte, int ve unsigned int türleri farklı olduğu için, is_same işlevi yanlış olarak değerlendir






# static_cast bu sinifin bir elemani mi

- Hayır, static_cast bir C++ dönüştürme operatörüdür ve C++ dilinde yerleşik bir özelliktir. Yani static_cast bir sınıf veya nesne değil, C++'ın kendisinde tanımlı olan bir yapıdır. Bu operatör, tür dönüşümleri yapmak için kullanılır ve farklı türler arasında uygun bir şekilde dönüşüm yapılmasını sağlar. Örneğin, int türündeki bir değişkeni double türüne dönüştürmek için static_cast kullanabilirsiniz:

```CPP
int i = 10;
double d = static_cast<double>(i); // i, double türüne dönüştürülür

```
- Bu şekilde, static_cast bir sınıf veya nesne değil, yalnızca C++ dilindeki yerleşik bir özelliktir.


- 












































