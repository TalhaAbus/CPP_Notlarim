- C++20'de yer alan <version> başlık dosyası, derlenen C++ standart sürümüne ilişkin bilgi sağlayan makro tanımları içerir. Bu başlık dosyası, derlenen C++ sürümüne bağlı olarak programda farklı davranışların sergilenmesini sağlayan koşullu derleme işlemlerinde kullanılır.

- Başlık dosyası, aşağıdaki makro tanımlarını içerir:

- **__cplusplus:** Bu makro, derlenen C++ sürümünü belirtir. Örneğin, C++17 sürümü 201703 olarak belirtilir.
- **_cpp*:** Bu makrolar, C++20 sürümüne eklenen özellikleri belirtir. Her makro, özelliğin bir sürüm numarası ile eşleştirilir. Örneğin, __cpp_concepts makrosu, kavramlar özelliğinin sürüm numarası olan 201907'ye eşittir.
- Bu başlık dosyası, C++20 sürümüne eklenen yeni özellikleri kullanırken programın derlenebilirliğini ve taşınabilirliğini artırmak için kullanılır. Özellikle, C++20 sürümünden önce var olmayan yeni özelliklerin kullanımında uyumluluk sağlamak için <version> başlık dosyasının kullanımı önerilir.

- Örnek olarak, aşağıdaki kod parçası <version> başlık dosyasını kullanarak, C++20 sürümünde eklendiği için öncesinde kullanılamayan kavramlar özelliğini kullanır:

```CPP
#include <iostream>
#include <vector>
#include <concepts>
#include <version>

template <typename T>
concept Numeric = std::is_arithmetic_v<T>;

template <Numeric T>
void print(const std::vector<T>& v) {
    for (const auto& i : v) {
        std::cout << i << " ";
    }
    std::cout << std::endl;
}

int main() {
    std::vector<int> int_vector{1, 2, 3, 4, 5};
    std::vector<double> double_vector{1.1, 2.2, 3.3, 4.4, 5.5};

    print(int_vector);
    print(double_vector);

    return 0;
}

```

> Bu örnekte, Numeric kavramı, yalnızca sayısal türleri şablon parametreleri olarak kabul eden bir kavramdır. Şablon parametresi, kavramın gereksinimlerini karşılamayan bir tür olduğunda, C++20 sürümünde eklendiği için öncesinde kullanılamayan kavramlar özelliği kullanılarak derleme hatası verir.

# <version> başlık dosyası sadece makroları mı içerir? Sınıflar ve fonksiyonları yok mudur?

- Evet, <version> başlık dosyası yalnızca makroları içerir. C++20 standartında yapılan değişiklikleri belirlemek için kullanılır. Bu değişikliklerin birçoğu dilin kendisindeki değişikliklerdir, bu nedenle kodu güncellemek için kullanılabilir. Ancak, doğrudan sınıflar veya fonksiyonlar içermez. Bununla birlikte, C++20 standartındaki değişikliklerin birçoğu, diğer başlık dosyalarındaki sınıflar ve fonksiyonlarla birlikte kullanılır.

# Ne gibi makrolar içerir? Ne gibi senaryolarda kullanılır?

- <version> başlık dosyası, C++ derleyicisinin ve standardı destekleyen diğer araçların kullanılabilirliği hakkında bilgi sağlayan makrolar içerir. Bu makrolar, belirli bir derleyici veya kütüphane sürümünün kullanımda olup olmadığını kontrol etmek, uyumluluk sorunlarını çözmek ve standarda uygunluğu sağlamak için kullanılır.

- Bir örnek senaryo, bir proje için belirli bir C++ sürümünün desteklenip desteklenmediğini kontrol etmek için kullanmaktır. Bu, proje gereksinimleri veya hedef platform tarafından belirlenebilir.

- Ayrıca, belirli bir sürümün özelliklerinin kullanıldığı durumlarda bu özelliklerin derlenip derlenemeyeceğini kontrol etmek için de kullanılabilir.

- Örneğin, aşağıdaki kod, C++20 özelliklerinin kullanılabilirliğini kontrol eder:

```CPP
#include <iostream>
#include <version>

#if defined(__cpp_lib_concepts) && __cpp_lib_concepts >= 201907L
#define HAS_CONCEPTS 1
#else
#define HAS_CONCEPTS 0
#endif

int main() {
    std::cout << "Has concepts: " << HAS_CONCEPTS << '\n';
    return 0;
}

```

> Bu örnekte, __cpp_lib_concepts makrosu, C++20 standardının desteklediği kavramlar özelliğini kontrol eder. Eğer özellik destekleniyorsa, HAS_CONCEPTS makrosu 1 değerini alır ve bunu ekrana yazdırır. Aksi takdirde, HAS_CONCEPTS 0 değerini alır.

- Bu örnek, bir derleyicinin C++20 kavramlarını destekleyip desteklemediğini kontrol etmek için kullanılabilir.

















