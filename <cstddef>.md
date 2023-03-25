- <cstddef> başlık dosyası C++ standart kütüphanesinde yer alan bir başlık dosyasıdır. Bu başlık dosyası, C++ dilinde temel veri türleri ve sabitlerle ilgili makroları tanımlayan <stddef.h> başlık dosyasının C++ standart uyumlu bir sürümüdür.

- Bu başlık dosyası aşağıdaki türleri ve sabitleri tanımlar:

- **std::size_t:** tamsayı türü, nesne veya tür boyutunu temsil etmek için kullanılır.
- **std::ptrdiff_t:** tamsayı türü, iki bellek adresi arasındaki farkı temsil etmek için kullanılır.
- **std::nullptr_t:** null işaretçileri için kullanılır.
- **std::byte:** 8 bitlik veri depolamak için kullanılır.
- Ayrıca, C++ 11'den beri nullptr anahtar kelimesi de bu başlık dosyasında tanımlanmaktadır.

- Bu başlık dosyası, C++ standart kütüphanesi ve kullanıcı tanımlı sınıflar tarafından kullanılan birçok diğer başlık dosyasında kullanılan türleri ve sabitleri tanımlamak için kullanılır.

- Örnek olarak, bir std::vector nesnesindeki eleman sayısını hesaplamak için std::size_t türü kullanılabilir:

```CPP
#include <cstddef>
#include <vector>
#include <iostream>

int main() {
    std::vector<int> v {1, 2, 3, 4, 5};
    std::size_t size = v.size();
    std::cout << "Vector size is: " << size << std::endl;
    return 0;
}

```

> Bu örnekte, std::size_t türü v.size() işlevi tarafından döndürülen eleman sayısını hesaplamak için kullanılır. Sonra, hesaplanan boyut, std::cout ile kullanıcıya gösterilir.

