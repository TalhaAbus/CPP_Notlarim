- any başlık dosyası, değişkenlerin türü bilinmeden depolanmasına ve yönetilmesine olanak tanıyan bir sınıf şablonu olan std::any sınıfını sağlar.

- std::any sınıfı, herhangi bir türe sahip bir nesne depolamak için kullanılabilir ve daha sonra depolanan nesneye erişmek için kullanılabilir. std::any sınıfı, içinde depolanan nesnenin türünden bağımsız olarak çalışır ve kullanıcı tarafından belirtilen türlerle hiçbir şekilde etkileşime girmez.

- std::any sınıfı, bir nesnenin türü ve değeri birbirinden ayrı olarak depolandığı için, türü bilinmeyen bir nesneyi değiştirme veya başka bir türe dönüştürme işlemi yapabilirsiniz.

# Classes

- **any**
- **bad_any_cast**
> std::bad_any_cast istisnası, std::any_cast işlevi std::any sınıfı nesnesinin içeriğini dönüştürmeye çalıştığında başarısız olduğunda fırlatılır.

# Functions

- **std::swap**
> std::swap(std::any) işlevi, std::any sınıfının bir örneğinin içeriğini başka bir std::any örneğinin içeriğiyle değiştirmek için kullanılır.
- **make_any**
> std::make_any C++17 ile tanıtılan bir standart kütüphane işlevidir ve bir tür belirtilen std::any nesnesi oluşturur.
- **any_cast**
> std::any_cast işlevi, std::any sınıfı tarafından desteklenen herhangi bir türdeki nesnenin içeriğine erişmek için kullanılır.

### bad_any_cast 
- std::bad_any_cast istisnası, std::any_cast işlevi std::any sınıfı nesnesinin içeriğini dönüştürmeye çalıştığında başarısız olduğunda fırlatılır. Bu istisna, std::any_cast işlevi tarafından otomatik olarak fırlatılır ve genellikle yakalayarak hatanın nasıl ele alınacağına karar vermek için kullanılır.

- std::bad_any_cast sınıfı, stdexcept başlık dosyasında tanımlanır ve std::exception sınıfından türetilir. Bu sınıf, what adlı bir işlevi içerir ve bu işlev, istisna nesnesi oluşturulduğunda açıklama veren bir C-strings döndürür.

- Örneğin, aşağıdaki kod parçasında, std::any_cast işlevi std::string türüne dönüştürmeye çalışıyor, ancak aslında içeriği bir int türünden olan std::any nesnesi veriliyor. Bu durumda, std::bad_any_cast istisnası fırlatılır ve what işlevi, açıklama veren bir C-strings döndürür:

```CPP
#include <iostream>
#include <any>
#include <stdexcept>

int main() {
    std::any a = 42;
    
    try {
        std::string s = std::any_cast<std::string>(a);
    } catch (const std::bad_any_cast & e) {
        std::cerr << "Error: " << e.what() << '\n';
    }

    return 0;
}

```
> Bu örnekte, a örneği int türünden bir değer içeriyor, ancak std::string türüne dönüştürülmeye çalışılıyor. Bu nedenle, std::bad_any_cast istisnası fırlatılır ve what işlevi, "bad any cast" mesajını döndürür.
    
## Functions

### swap()

- std::swap(std::any) işlevi, std::any sınıfının bir örneğinin içeriğini başka bir std::any örneğinin içeriğiyle değiştirmek için kullanılır.

- Bu işlev, std::any sınıfının içindeki swap üye işlevini çağırarak çalışır. İki parametre alır ve bu parametreler, birbirleriyle takas edilecek iki std::any örneğidir. İşlev, öncelikle herhangi bir std::any örneğinin içeriğinin boş olup olmadığını kontrol eder. Eğer boşsa, takas işlemi gerçekleştirilmez ve işlev sonlanır. Aksi halde, iki std::any örneği birbirleriyle takas edilir.

- İşte örnek bir kullanımı:

```CPP
#include <iostream>
#include <any>

int main() {
    std::any a = 42;
    std::any b = std::string("Hello, world!");

    std::cout << std::any_cast<int>(a) << '\n';
    std::cout << std::any_cast<std::string>(b) << '\n';

    std::swap(a, b);

    std::cout << std::any_cast<int>(a) << '\n';
    std::cout << std::any_cast<std::string>(b) << '\n';

    return 0;
}

```
> Bu örnek kodda, ilk önce std::any sınıfının a ve b isimli iki örneği oluşturulmuştur. a örneği int türünden 42 değeriyle, b örneği ise std::string türünden "Hello, world!" değeriyle başlatılmıştır.

- Daha sonra, std::swap() işlevi kullanılarak a ve b örnekleri takas edilmiştir. Bu işlem sonrasında, a örneği std::string türünden "Hello, world!" değerini içermekte, b örneği ise int türünden 42 değerini içermektedir.

### make_any()

- std::make_any C++17 ile tanıtılan bir standart kütüphane işlevidir ve bir tür belirtilen std::any nesnesi oluşturur.

- std::make_any işlevi, std::any sınıfı tarafından desteklenen tüm türleri kabul eder. Aşağıdaki gibi kullanılır:

```CPP
#include <any>

int main() {
    auto a = std::make_any<int>(42);
    auto b = std::make_any<std::string>("Hello, world!");

    return 0;
}

```
> Bu örnekte, std::make_any işlevi a ve b isimli iki std::any örneği oluşturur. a örneği int türünden 42 değeriyle, b örneği ise std::string türünden "Hello, world!" değeriyle oluşturulur.

- std::make_any işlevi, C++14'ten önce kullanılan std::experimental::make_any işleviyle benzerdir. Ancak, std::make_any işlevi C++17'de resmi olarak standart kütüphaneye eklendi ve std::experimental::make_any artık kullanımdan kaldırıldı.

### any_cast()
  
- std::any_cast işlevi, std::any sınıfı tarafından desteklenen herhangi bir türdeki nesnenin içeriğine erişmek için kullanılır.

- std::any_cast işlevi, C++11'de tanıtılan ve type_id adlı özel bir işlem gerektirmeyen, daha hızlı ve daha güvenli bir alternatif olan boost::any işleviyle benzerdir. std::any_cast işlevi, C++17 standardına dahil edildi.

- Aşağıdaki gibi kullanılır:

```CPP
#include <any>
#include <iostream>

int main() {
    std::any a = 42;
    std::cout << std::any_cast<int>(a) << '\n'; // prints "42"
    
    a = 3.14;
    std::cout << std::any_cast<double>(a) << '\n'; // prints "3.14"
    
    a = std::string("Hello, world!");
    std::cout << std::any_cast<std::string>(a) << '\n'; // prints "Hello, world!"
    
    return 0;
}

```

> Bu örnekte, std::any_cast işlevi std::any nesnesinin içeriğini belirtilen türe dönüştürür. Bu örnekte, std::any nesnesi önce int, sonra double, sonra std::string türlerine dönüştürülür ve std::cout işleviyle çıktı verilir.

- std::any_cast işlevi, std::any sınıfının desteklediği tüm türleri kabul eder. Ancak, dönüştürmeye çalışılan tür, std::any nesnesinin içeriğindeki türle eşleşmezse, std::bad_any_cast istisnası fırlatılır. Örneğin, aşağıdaki kod parçasında std::string türüne dönüştürmeye çalışılıyor, ancak std::any nesnesi aslında bir int türünden değer içeriyor:

```CPP
#include <any>
#include <iostream>
#include <stdexcept>

int main() {
    std::any a = 42;
    
    try {
        std::string s = std::any_cast<std::string>(a);
    } catch (const std::bad_any_cast & e) {
        std::cerr << "Error: " << e.what() << '\n';
    }

    return 0;
}

```

> Bu durumda, std::bad_any_cast istisnası fırlatılır ve std::cerr üzerinden hata mesajı yazdırılır.


# Örnekler:


```CPP
#include <iostream>
#include <any>

int main() {
    std::any a = 5;
    std::cout << std::any_cast<int>(a) << '\n'; // 5

    a = 3.14;
    std::cout << std::any_cast<double>(a) << '\n'; // 3.14

    a = std::string("Hello, world!");
    std::cout << std::any_cast<std::string>(a) << '\n'; // Hello, world!

    return 0;
}

```
- Yukarıdaki örnekte, std::any sınıfı kullanılarak herhangi bir türde değişkenler depolanıyor ve daha sonra ilgili türe dönüştürülüyor.

- Tabii, şöyle bir örnek verebilirim:

```CPP
#include <iostream>
#include <any>
#include <string>
#include <vector>

int main() {
  std::vector<std::any> myVector;
  
  myVector.push_back(5);
  myVector.push_back(std::string("Hello"));
  myVector.push_back(3.14);
  
  for (const auto& elem : myVector) {
    if (elem.type() == typeid(int)) {
      std::cout << "Integer element: " << std::any_cast<int>(elem) << std::endl;
    }
    else if (elem.type() == typeid(std::string)) {
      std::cout << "String element: " << std::any_cast<std::string>(elem) << std::endl;
    }
    else if (elem.type() == typeid(double)) {
      std::cout << "Double element: " << std::any_cast<double>(elem) << std::endl;
    }
  }
  
  return 0;
}

```
- Bu örnekte, std::any sınıfının kullanımı gösterilmiştir. std::any, farklı türde verileri tutabilen bir sınıftır. Bu örnekte, farklı türlerdeki verileri bir std::vector<std::any> içinde tutuyoruz ve sonrasında bu vektörün elemanlarına erişerek her birini kendi türünde bastırıyoruz. Bu şekilde, farklı türlerdeki verileri aynı vektörde tutabilir ve sonrasında bu verilere istediğimiz şekilde erişebiliriz.
















