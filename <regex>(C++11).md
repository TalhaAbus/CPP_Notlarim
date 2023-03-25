- regex başlık dosyası, C++11'de tanıtılan bir başlık dosyasıdır ve düzenli ifadeler (regular expressions) için destek sağlar. regex sınıfı, düzenli ifade tabanlı arama için kullanılan ana sınıftır. Bu sınıf, bir düzenli ifadeyi tanımlamanıza, metin dizilerinde arama yapmanıza ve eşleşmeleri bulmanıza olanak tanır.

- Ayrıca, başlık dosyası regex altında diğer yardımcı sınıflar ve işlevler de vardır. Bunlar arasında match_results, sub_match, regex_iterator, regex_token_iterator ve regex_replace gibi sınıflar yer alır.

- Bir örnek olarak, regex_search() işlevi, bir dize içinde bir düzenli ifade arayabilir. Aşağıdaki örnek, bir dizede bir düzenli ifade arayarak eşleşme sayısını hesaplar:
  
  - regex, bir dizedeki metin kalıplarını tanımlamak ve aramak için kullanılan bir C++ kütüphanesidir. Örneğin, bir metin içindeki e-posta adreslerini, telefon numaralarını veya belirli bir formata sahip tarihleri aramak için kullanılabilir. Bu tür işlemler için düzenli ifadelerin (regular expressions) kullanımı oldukça önemlidir ve regex kütüphanesi, bu işlemleri kolaylaştıran birçok fonksiyona sahiptir. Bunun yanı sıra, birçok metin işleme işlevinde regex kullanımı oldukça yaygındır.
  
  - C++'da düzenli ifadeleri kullanmak için regex başlık dosyası dışında alternatif olarak Boost C++ kütüphanesi de kullanılabilir. Boost kütüphanesi de C++'ın düzenli ifadeler için kullanılabilecek diğer bir kütüphanesidir ve genellikle C++'ın standart kitaplığında bulunmayan birçok işlevselliği içerir. Bunun dışında, bazı durumlarda düzenli ifadeler yerine C++'ın standart string işlevleri kullanılabilir, ancak bu sınırlı bir işlevsellik sağlar.
  
  
  ```CPP
  #include <iostream>
#include <regex>

int main() {
    std::string str = "The quick brown fox jumps over the lazy dog";
    std::regex pattern("the");

    std::smatch matches;
    int count = 0;

    while (std::regex_search(str, matches, pattern)) {
        count++;
        str = matches.suffix().str();
    }

    std::cout << "The pattern 'the' matches " << count << " times." << std::endl;

    return 0;
}

  ```

- Regex kullanarak örnekler verelim:

- Verilen bir metindeki belli bir kelimeyi veya kelime öbeğini bulmak için:

```CPP
#include <iostream>
#include <regex>
#include <string>

int main() {
    std::string text = "The quick brown fox jumps over the lazy dog";
    std::regex word_regex("fox");
    std::smatch matches;

    if (std::regex_search(text, matches, word_regex)) {
        std::cout << "The word '" << matches.str() << "' is found in the text.\n";
    } else {
        std::cout << "The word is not found in the text.\n";
    }

    return 0;
}

```

- Verilen bir metindeki belli bir deseni aramak için:

```CPP
#include <iostream>
#include <regex>
#include <string>

int main() {
    std::string text = "The quick brown fox jumps over the lazy dog";
    std::regex pattern("[a-z]+");
    std::smatch matches;

    while (std::regex_search(text, matches, pattern)) {
        for (auto match : matches) {
            std::cout << match << " ";
        }
        std::cout << std::endl;
        text = matches.suffix().str();
    }

    return 0;
}

```

- Verilen bir metindeki belli bir desenin tekrar sayısını bulmak için:

```CPP
#include <iostream>
#include <regex>
#include <string>

int main() {
    std::string text = "The quick brown fox jumps over the lazy dog";
    std::regex pattern("[aeiou]");
    std::sregex_iterator iter(text.begin(), text.end(), pattern);
    std::sregex_iterator end;

    int count = std::distance(iter, end);
    std::cout << "The number of vowels in the text: " << count << std::endl;

    return 0;
}

```

- Bu örneklerde, regex kütüphanesi kullanılarak bir metindeki belli bir kelime, kelime öbeği veya desenin aranması, tekrar sayısının bulunması gibi işlemler gerçekleştirilmiştir.














