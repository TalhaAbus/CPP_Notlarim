- <expected> başlık dosyası, başarılı bir sonuç veya bir hata durumunu temsil etmek için kullanılacak std::expected sınıfını tanımlar. Bu sınıf, bir işlemin sonucunu veya hatayı temsil etmek amacıyla kullanılabilir ve genellikle hatalı durumları işlemek için kullanılan özel durum mekanizmasının (exception) bir alternatifidir.

- std::expected şu anda C++ standart kütüphanesinin resmi bir parçası olmadığı için, benzer özelliklere sahip olan ve yaygın olarak kullanılan üçüncü taraf kütüphaneler vardır. Bunlardan biri olan tl::expected kütüphanesi, GitHub'da bulunabilir:

- GitHub: https://github.com/TartanLlama/expected

- Bu kütüphane, <expected> başlık dosyasının yerini alabilecek ve istenen işlevselliği sağlayabilecek bir alternatiftir.

- tl::expected<T, E> sınıfının temel member tipleri şunlardır:

- **value_type:** Başarılı bir sonuç durumunda depolanan değerin türü (T).
- **unexpected_type:** Başarısız bir durumda depolanan hata değerinin türü (E veya std::unexpected<E>).
- **tl::expected<T, E>** sınıfı, başarılı veya başarısız durumları temsil etmek ve bu durumları sorgulamak için bir dizi üye işleve sahiptir. Başlıca üye işlevler şunlardır:

- **has_value():** tl::expected nesnesinin bir değer içerip içermediğini kontrol etmek için kullanılır.
- **operator*():** Depolanan değere erişmek için kullanılır (sadece başarılı bir durumda).
- **operator->():** Depolanan değerin üyelerine erişmek için kullanılır (sadece başarılı bir durumda).
- **value():** Depolanan değeri elde etmek için kullanılır (sadece başarılı bir durumda).
- **error():** Hata durumunu elde etmek için kullanılır (sadece başarısız bir durumda).
- **operator bool():** Başarılı bir durumun olup olmadığını kontrol etmek için kullanılır.
- **tl::expected kullanımıyla ilgili basit bir örnek:

```CPP
#include <iostream>
#include <string>
#include <tl/expected.hpp>

tl::expected<int, std::string> parse_positive_integer(const std::string& input) {
    int value;
    try {
        value = std::stoi(input);
    } catch (...) {
        return tl::unexpected{"Geçersiz giriş"};
    }

    if (value < 0) {
        return tl::unexpected{"Negatif sayı"};
    }

    return value;
}

int main() {
    std::string input = "42";
    auto result = parse_positive_integer(input);

    if (result) {
        std::cout << "Sayı: " << *result << std::endl;
    } else {
        std::cout << "Hata: " << result.error() << std::endl;
    }

    return 0;
}

```

- Bu örnek, tl::expected kullanarak başarılı ve başarısız durumları temsil etmektedir. Başarılı bir durumda, fonksiyon bir int değeri döndürürken, başarısız bir durumda hatayı temsil eden bir std::string döndürür.

- <expected> başlık dosyası, std::expected adlı bir sınıf ve bazı yardımcı fonksiyonlar içerir. std::expected sınıfı, bir değer veya bir hata kodu içeren bir nesnedir. Aşağıdaki gibi bir kullanım örneği gösterilebilir:

```CPP
#include <iostream>
#include <string>
#include <stdexcept>
#include <expected>

std::expected<std::string, std::runtime_error> get_string(bool success) {
    if (success) {
        return std::string("Success!");
    } else {
        return std::make_unexpected(std::runtime_error("Failure!"));
    }
}

int main() {
    auto result1 = get_string(true);
    if (result1) {
        std::cout << "Result1: " << *result1 << std::endl;
    }

    auto result2 = get_string(false);
    if (!result2) {
        std::cout << "Result2 error: " << result2.error().what() << std::endl;
    }

    return 0;
}

```
> Bu kod, get_string adlı bir fonksiyon tanımlar. Bu fonksiyon, parametre olarak bir bool değeri alır ve success parametresi true ise bir std::string içeren bir expected nesnesi döndürür. Ancak, success parametresi false ise bir hata kodu içeren bir expected nesnesi döndürür. 









