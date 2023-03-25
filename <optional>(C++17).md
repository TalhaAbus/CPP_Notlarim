- <optional>, C++17 standardında tanıtılan bir başlık dosyasıdır. Bu başlık dosyası, bir nesnenin belirli bir durumda olup olmadığını belirlemek için kullanılan bir şablon sınıfı olan "optional" sınıfını tanımlar.

- "Optional" sınıfı, bir nesnenin var olup olmadığını belirleyen bir türdür. Eğer bir nesne varsa, o nesnenin değerine erişilebilir, aksi halde ise bir hata durumu oluşur. Böylece, optional sınıfı, kodun daha güvenli hale getirilmesine ve hata ayıklama işlemlerinin daha kolay hale getirilmesine yardımcı olur.

- Optional sınıfı, varsayılan değerlerle, başka bir optional nesnesiyle veya belirli bir değerle başlatılabilir. Değer atanmadığı durumda, optional nesnesinin değeri "boş" olarak ayarlanır.

- Optional sınıfının kullanımı, özellikle opsiyonel parametreler veya opsiyonel değer döndürme gibi durumlarda faydalıdır. Ayrıca, optional sınıfı, birçok örnek veri türü için daha düşük bellek kullanımı sağlar.

- Örnek kullanımlardan biri, bir işlevin opsiyonel bir parametre alması gerektiği durumlardır. Bu, kullanıcının opsiyonel bir parametre belirlemesine izin verir, ancak parametrenin belirtilmemesi durumunda da işlevin doğru şekilde çalışmasını sağlar.

```CPP
#include <optional>
#include <iostream>

// Bir işlem yapıp, sonucu opsiyonel olarak döndüren bir fonksiyon
std::optional<int> divide(int a, int b) {
    if (b == 0) {
        // Eğer b sıfırsa, opsiyonel değer boş döndürülür.
        return std::nullopt;
    }
    // Bölme işlemi yapılır ve sonuç opsiyonel olarak döndürülür.
    return a / b;
}

int main() {
    // divide fonksiyonunun sonucunu opsiyonel olarak alıyoruz.
    std::optional<int> result = divide(10, 5);

    // Eğer sonuç opsiyonel bir değer olarak döndürülmüşse, sonucu ekrana yazdırıyoruz.
    if (result) {
        std::cout << "Result: " << *result << std::endl;
    } else {
        std::cout << "Cannot divide by zero." << std::endl;
    }

    // Bölme işleminin sonucu opsiyonel olarak döndürülmüşse, sonucu kullanarak başka bir işlem yapabiliriz.
    if (result) {
        int multiplied_result = *result * 2;
        std::cout << "Multiplied result: " << multiplied_result << std::endl;
    }

    return 0;
}

```
> Bu örnek kod, std::optional sınıfının kullanımına ilişkindir. std::optional sınıfı, bir değeri veya hiçbir değeri içerebilen bir kutudur. Bu örnekte, std::optional<int> türünden bir değişken oluşturulur ve başlangıçta hiçbir değer içermediği belirtilir. Daha sonra, kullanıcıdan bir tamsayı değeri istenir ve bu değer, std::optional değişkenine atılır. Eğer kullanıcı hiçbir değer girmemişse, std::optional değişkeni hala hiçbir değer içermez ve bu durumda programın devam etmesi sağlanır. Eğer kullanıcı bir değer girmişse, bu değer std::optional değişkenine atanır ve sonrasında bu değer kullanılarak başka işlemler yapılabilir. Bu örnekte, eğer std::optional değişkeni bir değer içeriyorsa, bu değer ekrana yazdırılır.

- Özetle, std::optional sınıfı, bir değişkenin değeri olup olmadığını kontrol etmek için kullanılabilir. Bu, programlama hatalarını önlemeye ve kod güvenliğini artırmaya yardımcı olabilir.


- Tabii, şimdi bir örnek daha verelim. Diyelim ki bir programda kullanıcının yaşını sormak istiyoruz, ancak kullanıcının yaşını girmek zorunlu değil ve kullanıcı hiçbir şey girmeyebilir. Bu durumda optional kullanarak şöyle bir kod yazabiliriz:

```CPP
#include <iostream>
#include <optional>

std::optional<int> getAge() {
    int age;
    std::cout << "Enter your age (optional): ";
    std::cin >> age;

    if (std::cin.fail()) {
        std::cin.clear();
        std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n');
        return std::nullopt;
    } else {
        return age;
    }
}

int main() {
    auto age = getAge();

    if (age) {
        std::cout << "Your age is: " << *age << std::endl;
    } else {
        std::cout << "You did not enter your age." << std::endl;
    }

    return 0;
}

```

- Burada getAge() fonksiyonu, kullanıcının yaşını isteyen bir mesaj gösterir ve bir tamsayı okur. Eğer kullanıcı tamsayı girmeden önce bir hata yaparsa, std::nullopt döndürür. Aksi takdirde, kullanıcının yaşını içeren bir std::optional<int> döndürür. main() fonksiyonunda, age değişkeni getAge() tarafından döndürülen değeri alır. Daha sonra, if (age) koşulu kullanarak, age değişkeninin boş olup olmadığını kontrol ederiz. Eğer boş değilse, kullanıcının yaşını ekrana yazdırırız. Aksi takdirde, kullanıcının yaşını girmeden geçtiğini belirten bir mesaj yazdırırız.








