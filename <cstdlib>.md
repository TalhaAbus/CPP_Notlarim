- <cstdlib> başlık dosyası, C++ standard kütüphanesi içinde yer alan bir başlık dosyasıdır. Bu başlık dosyası, C dili standart kütüphanesi <stdlib.h> başlık dosyasının C++ diline uygun hale getirilmiş halidir. <cstdlib> başlık dosyası, programların çalışma zamanında ihtiyaç duyabileceği, bellek yönetimi, sayısal dönüşümler, rastgele sayı üretimi, çevre değişkenleri, program sonlandırma ve diğer bazı işlemler için fonksiyonlar ve sabitler sağlar.

- Bu başlık dosyasında yer alan en önemli fonksiyonlar şunlardır:

- **void* malloc(size_t size) :** Bellekte size kadar alan ayırmak için kullanılır.
- **void free(void* ptr) :** malloc() ile ayrılmış bellek bloklarını serbest bırakmak için kullanılır.
- **void* calloc(size_t nmemb, size_t size) :** Bellekte nmemb * size kadar alan ayırmak için kullanılır.
- **void* realloc(void* ptr, size_t size) :** malloc() veya calloc() ile ayrılmış bellek bloklarının boyutunu yeniden boyutlandırmak için kullanılır.
- **int rand(void) :** 0 ile RAND_MAX arasında bir rastgele tamsayı üretir.
- **- **void srand(unsigned int seed) :** Rastgele sayı üreticisinin başlangıç değerini belirler.
- **int atoi(const char* str) :** Bir karakter dizisini tamsayıya dönüştürmek için kullanılır.
- **double atof(const char* str) :** Bir karakter dizisini double tipine dönüştürmek için kullanılır.
- **int system(const char* command) :** Komut satırı ile çalışan bir işlemi çalıştırmak için kullanılır.

- Örnek kullanımlar:

- Bellek ayırmak ve serbest bırakmak:

```CPP
#include <cstdlib>
#include <iostream>

int main() {
  int* ptr = static_cast<int*>(malloc(sizeof(int) * 10));
  if (ptr == nullptr) {
    std::cerr << "Memory allocation failed\n";
    exit(EXIT_FAILURE);
  }

  for (int i = 0; i < 10; ++i) {
    ptr[i] = i + 1;
  }

  for (int i = 0; i < 10; ++i) {
    std::cout << ptr[i] << ' ';
  }
  std::cout << '\n';

  free(ptr);
  return EXIT_SUCCESS;
}

```

- Rastgele sayı üretmek:

```CPP
#include <cstdlib>
#include <iostream>
#include <ctime>

int main() {
  srand(time(nullptr));

  for (int i = 0; i < 10; ++i) {
    std::cout << rand() << ' ';
  }
  std::cout << '\n';

  return EXIT_SUCCESS;
}

```

- Bir karakter dizisini tamsayıya dönüştürmek:

```CPP

#include <cstdlib>
#include <iostream>

int main() {
  const char* str = "123

```






















