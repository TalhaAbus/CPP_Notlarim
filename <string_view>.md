- <string_view> başlık dosyası, std::string gibi bir karakter dizisi türünün bir parçasını gösteren, ancak kendi bellek yönetimine sahip olmayan bir sınıf olan std::string_view sınıfını tanımlar. std::string_view, karakter dizisi işleme işlevleri için kullanılabilir ve aynı zamanda diğer işlevler tarafından da kullanılabilir.

- std::string_view sınıfının kullanımı, bir std::string nesnesi kullanımına benzerdir. Ancak, std::string_view nesnesi, bir std::string nesnesinin bir parçası değildir, sadece bir görünümüdür. Bu nedenle, std::string_view nesneleri, std::string nesnelerinden daha hafiftir ve özellikle büyük karakter dizileri işlemek için verimli bir yol sunarlar.

- Örneğin, bir fonksiyona bir std::string_view nesnesi geçirerek, bu fonksiyonun orijinal karakter dizisine erişebilirsiniz, ancak bellek kopyalaması yapmadan, ayrıca orijinal karakter dizisini değiştirerek orijinal std::string nesnesini değiştirebilirsiniz.

```CPP
#include <iostream>
#include <string_view>

void print(std::string_view str) {
    std::cout << str << std::endl;
}

int main() {
    std::string s = "Hello, world!";
    std::string_view sv = s;

    std::cout << "s: " << s << std::endl;
    std::cout << "sv: " << sv << std::endl;

    print(s);
    print(sv);

    s[0] = 'h';
    std::cout << "s: " << s << std::endl;
    std::cout << "sv: " << sv << std::endl;

    return 0;
}

```
> Bu örnekte, bir std::string nesnesi oluşturulur ve bir std::string_view nesnesine atanır. Ardından, hem std::string nesnesi hem de std::string_view nesnesi çıktıya yazdırılır ve bir print() işlevine hem std::string nesnesi hem de std::string_view nesnesi geçirilir. Son olarak, orijinal std::string nesnesi değiştirilir ve hem std::string nesnesi hem de std::string_view nesnesi çıktıya yazdırılır.

# ne zaman string_view kullanmaliyim? Neden string yerine string_view kullanayim

- string_view, string sınıfının bir alternatifi olarak kullanılabilir. string_view, bir string nesnesi gibi karakter dizisi verilerini temsil eder, ancak verileri kendisi depolamaz. Bunun yerine, string_view sadece bir arabellek görevi görür ve belirli bir bellek bölgesine bakarak çalışır.

- Bu özellikleri nedeniyle, string_view kullanımı özellikle performans açısından avantajlıdır. Özellikle, büyük boyutlu verileri depolamanın gerekli olmadığı durumlarda faydalıdır. string_view, bir string nesnesiyle karşılaştırıldığında daha hafiftir ve işlem yaparken daha az bellek kullanır.

- string_view'ın kullanımı özellikle C++11'den sonra yaygınlaşmıştır. Özellikle, metin işleme, veri yapıları ve algoritmalar için kullanışlıdır.

- Bununla birlikte, string_view, karakter dizileri üzerindeki değişiklikleri desteklemez, yalnızca sadece okuma işlemi yapabilir. Bu nedenle, değiştirilmesi gereken veriler için string nesnesi tercih edilebilir.

**şöyle bir örnek düşünebiliriz:**

```CPP
#include <iostream>
#include <string_view>

void print_string(std::string_view str) {
  std::cout << "String: " << str << '\n';
}

int main() {
  std::string str = "Hello, World!";
  print_string(str);  // std::string nesnesi string_view türüne otomatik olarak dönüştürülebilir
  print_string("Hello, again!");  // C-style string de string_view türüne otomatik olarak dönüştürülebilir
  return 0;
}

```

- Burada print_string isimli bir fonksiyon tanımladık ve std::string_view türünde bir argüman alıyor. Fonksiyon çağrılırken std::string ve C-style string argümanlarının std::string_view türüne otomatik olarak dönüştürülmesi sağlandı. Bu sayede, std::string ve C-style string değişkenlerinin kullanılması mümkün oldu.

# string_view kullanmanin performansa etkisi var midir

- Evet, string_view kullanmanın performansa etkisi olabilir. Bunun nedeni, string_view'un kendisinde bir bellek alanı tutmamasıdır. Bunun yerine, var olan bir string'in belirli bir bölümüne bir referans sağlar. Bu, string_view'ın kopyalanmasını veya taşınmasını gerektirmediği anlamına gelir ve bu nedenle bazı durumlarda performans avantajı sağlayabilir.

- Ancak, string_view'un belirli durumlarda string'den daha yavaş olabileceği durumlar da vardır. Örneğin, bir string_view'ın uzunluğunu bulmak için her seferinde bir döngü kullanmak, bir string'in uzunluğunu bulmak için çağrılan length() fonksiyonunu kullanmaktan daha yavaş olabilir.

- Bu nedenle, performans açısından karar vermek için belirli senaryoları ve kullanımları dikkate almak gerekir.

















