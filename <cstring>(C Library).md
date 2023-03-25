- <cstring> başlık dosyası, C string işlevlerini tanımlayan C++ standart kütüphanesi başlık dosyasıdır. Bu başlık dosyası, C dilindeki string işlevleri için bir C++ arabirimi sağlar.

- Bu başlık dosyası, karakter dizilerinin işlenmesi için bir dizi fonksiyon içerir. Bazı yaygın kullanılan fonksiyonlar şunlardır:

- **strlen():** Bir C-string'in uzunluğunu hesaplar (sonlandırıcı karakteri olmadan).
- **strcpy():** Bir C-string'i başka bir C-string'e kopyalar.
- **strcat():** İki C-string'i birleştirir.
- **strcmp():** İki C-string'in eşitliğini karşılaştırır.
Bu başlık dosyası aynı zamanda bazı sabitler de tanımlar. Örneğin, NULL belirteci, boyut_t ve diğerleri gibi.

Örnek:

```CPP
#include <iostream>
#include <cstring>

int main() {
    char str1[] = "Hello";
    char str2[] = "World";
    char str3[11];

    std::cout << "str1: " << str1 << std::endl;
    std::cout << "str2: " << str2 << std::endl;

    std::strcpy(str3, str1);
    std::std::cout << "strcpy(str3, str1): " << str3 << std::endl;

    std::strcat(str1, str2);
    std::std::cout << "strcat(str1, str2): " << str1 << std::endl;

    int result = std::strcmp(str1, str2);
    std::std::cout << "strcmp(str1, str2): " << result << std::endl;

    return 0;
}

```

> Bu örnekte, C-string işlevleri kullanılarak farklı karakter dizileri birleştirilir ve karşılaştırılır.












