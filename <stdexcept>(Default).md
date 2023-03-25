# stdexcept

- stdexcept başlık dosyası, C++ standart kütüphanesinde yer alan hata sınıflarını ve bunlara ilişkin özelleştirilmiş istisna türlerini tanımlar. Bu başlık dosyası, temel hata sınıflarının yanı sıra özelleştirilmiş hata sınıfları tanımlamak için de kullanılır.

- Bu başlık dosyası içinde tanımlanan bazı temel hata sınıfları şunlardır:

- **std::exception:** Tüm istisna sınıflarının temel sınıfıdır.
- **std::logic_error:** Programcı hatası gibi istisna durumları için kullanılır.
- **std::runtime_error:** Çalışma zamanı hatası gibi istisna durumları için kullanılır.
- stdexcept başlık dosyası, programda bir hata oluştuğunda kullanıcıya hatanın ne olduğunu bildiren ve hatanın kaynağı hakkında bilgi sağlayan özelleştirilmiş istisna türleri oluşturmak için de kullanılabilir.
  
- Evet, exception başlık dosyası stdexcept başlık dosyasını da kapsar. Dolayısıyla, eğer sadece std::exception sınıfını kullanacaksanız, exception başlık dosyasını kullanabilirsiniz. Ancak std::runtime_error, std::logic_error ve diğer std::exception alt sınıflarını kullanacaksanız, stdexcept başlık dosyasını kullanmanız gerekiyor.
  
  
 - Aşağıdaki örnek, std::invalid_argument sınıfının kullanımını gösteriyor:

```CPP
#include <stdexcept>
#include <string>
#include <iostream>

void divide(int a, int b) {
    if (b == 0) {
        throw std::invalid_argument("division by zero");
    }
    std::cout << "Result of division is: " << a / b << std::endl;
}

int main() {
    int a = 10;
    int b = 0;

    try {
        divide(a, b);
    } catch (const std::invalid_argument& e) {
        std::cerr << "Error: " << e.what() << std::endl;
    }

    return 0;
}

```
- Burada, divide() fonksiyonu ikinci parametrenin sıfıra eşit olması durumunda bir özel durum fırlatır. Bu özel durum, std::invalid_argument sınıfının bir örneği olan bir exception türünden nesne tarafından temsil edilir. Bu nesnenin oluşturulması sırasında bir hata iletisi ("division by zero") geçirilir. main() işlevi, divide() fonksiyonunu çağırır ve fırlatılan özel durumu yakalar ve hatayı bir hata iletisi şeklinde çıktıya yazdırır.


- Bir örnek olarak, std::out_of_range sınıfını kullanabiliriz. Bu sınıf, geçersiz bir indeks veya sınırlar dışında bir değerle bir diziye veya vektöre eriştiğimizde fırlatılabilen bir istisna türüdür. Aşağıdaki örnekte, bir vektöre erişirken olası bir std::out_of_range hatası yakalanmaktadır:

```CPP
#include <vector>
#include <stdexcept>
#include <iostream>

int main() {
    std::vector<int> v = {1, 2, 3};
    try {
        std::cout << v.at(5); // Hata: Geçersiz bir indeks
    } catch (const std::out_of_range& e) {
        std::cerr << "Hata: " << e.what() << '\n';
    }
    return 0;
}

```

- Bu örnekte, v.at(5) çağrısı geçersiz bir indeks olduğu için std::out_of_range istisnası fırlatılacak ve catch bloğu bu hatayı yakalayarak e.what() çağrısı ile hatanın ne olduğunu yazdıracaktır.


















