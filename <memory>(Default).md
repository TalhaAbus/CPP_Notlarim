# 	std::memory

- std::memory başlık dosyası, C++ standart kütüphanesinde yer alan bir bellek yönetimi kütüphanesidir. Bu kütüphane, bellek yönetimine ilişkin bazı standart işlevler, akıllı işaretçiler ve bellek arayüzleri sağlar.

- Bellek yönetimi, C++ programlamasında oldukça önemlidir ve doğru bir şekilde yönetilmediğinde hafıza sızıntıları veya bellek hataları gibi sorunlara neden olabilir. std::memory kütüphanesi, C++ programcılarının bu tür sorunları önlemelerine ve bellek yönetimini daha kolay hale getirmelerine yardımcı olur.

- Bu kütüphanedeki başlıca sınıflar ve işlevler şunlardır:

- **std::unique_ptr**: Dinamik bellek tahsisinde kullanılan akıllı bir işaretçi sınıfıdır. Tek sahipliğe dayalıdır ve bellek alanı otomatik olarak temizlenir.
- **std::shared_ptr**: Dinamik bellek tahsisinde kullanılan akıllı bir işaretçi sınıfıdır. Birden fazla sahip olma durumunu destekler ve bellek alanı tüm sahipler serbest bırakana kadar silinmez.
- **std::weak_ptr**: std::shared_ptr'ın zayıf bir referansıdır ve bir nesnenin ömrünü uzatmaz.
- **std::make_unique**: Dinamik bellek tahsis eder ve std::unique_ptr nesnesi oluşturur.
- **std::make_shared**: Dinamik bellek tahsis eder ve std::shared_ptr nesnesi oluşturur.
- **std::allocator**: Bellek tahsis eden bir sınıf şablonudur.
- **std::addressof**: Bir nesnenin adresini döndürür.
- Aşağıdaki örnek, std::unique_ptr ve std::make_unique işlevini kullanarak dinamik bellek tahsis eder:

```CPP
#include <iostream>
#include <memory>

int main() {
  std::unique_ptr<int> p = std::make_unique<int>(42);
  std::cout << *p << '\n'; // 42
  return 0;
}

```

- Bu örnekte, std::unique_ptr sınıfı, std::make_unique işlevi kullanılarak oluşturulan bir int değeri için bir bellek alanı tahsis eder. Daha sonra, std::unique_ptr nesnesi kullanılarak bu değere erişilir.

- std::memory kütüphanesi, bellek yönetimiyle ilgili zorlukları önlemek ve bellek hatalarını en aza indirmek için kullanışlı işlevler ve sınıflar sağlar. 

# std::unique_ptr

- std::unique_ptr, C++11'de standart kütüphaneye eklenen bir akıllı işaretçi sınıfıdır. Adından da anlaşılacağı gibi, herhangi bir nesne için yalnızca tek bir sahibi olan bir işaretçidir. Bu, özellikle dinamik bellek yönetimi ile ilgili sorunları önlemek için çok yararlıdır.

- Bir std::unique_ptr, bir nesneyi işaret eden ve o nesnenin silinmesi gerektiğinde otomatik olarak bellekten silineceği garanti edilen bir işaretçi oluşturur. Dolayısıyla, bir std::unique_ptr nesnesi, nesnenin hayat döngüsünü yönetir ve sahip olduğu nesneyi bellekten otomatik olarak siler.

- std::unique_ptr sınıfının kullanımı oldukça basittir. Aşağıdaki örnek, std::unique_ptr sınıfını kullanarak dinamik bellek tahsis etmenin basit bir yolunu gösterir:

```CPP
#include <iostream>
#include <memory>

int main() {
  std::unique_ptr<int> ptr(new int(42));
  std::cout << *ptr << '\n'; // 42
  return 0;
}

```
- Bu örnekte, std::unique_ptr sınıfından bir nesne oluşturulur ve bellek alanı tahsis edilir. Daha sonra, std::unique_ptr nesnesi kullanılarak bu bellek alanındaki değere erişilir. Program sonlandığında, std::unique_ptr nesnesi otomatik olarak bellekten silinir ve bellekte sızıntı oluşmaz.

- std::unique_ptr sınıfı, diğer akıllı işaretçi sınıflarıyla birlikte kullanılabilir. Örneğin, bir std::unique_ptr nesnesi, bir std::shared_ptr nesnesine dönüştürülebilir.

```CPP
#include <iostream>
#include <memory>

int main() {
  std::unique_ptr<int> ptr(new int(42));
  std::shared_ptr<int> shared_ptr = std::move(ptr);
  std::cout << *shared_ptr << '\n'; // 42
  return 0;
}

```

- Bu örnekte, std::unique_ptr nesnesi bir std::shared_ptr nesnesine dönüştürülür. Bu, aynı bellek alanı üzerinde birden fazla sahip olma durumu için kullanışlıdır.

- std::unique_ptr sınıfı, bellek sızıntılarını önlemek için oldukça kullanışlı bir araçtır ve dinamik bellek yönetimi ile ilgili sorunları azaltır.

# std::shared_ptr

- std::shared_ptr, C++11'de standart kütüphaneye eklenen bir akıllı işaretçi sınıfıdır. Adından da anlaşılacağı gibi, birden fazla işaretçi nesnesi tarafından sahip olunan bir nesneyi temsil eder. Bu, özellikle dinamik bellek yönetimi ile ilgili sorunları önlemek için çok yararlıdır.

- Bir std::shared_ptr, bir nesneyi işaret eden ve nesneye birden fazla sahip olabilen bir işaretçi oluşturur. std::shared_ptr sınıfı, işaret ettiği nesnenin sayacını tutar ve herhangi bir sahip olma işlemi gerçekleştirildiğinde sayacı artırır. Sahip olma işlemi sonlandığında, sayacı azaltır ve sayac sıfıra düştüğünde nesne bellekten silinir.

- std::shared_ptr sınıfının kullanımı oldukça basittir. Aşağıdaki örnek, std::shared_ptr sınıfını kullanarak dinamik bellek tahsis etmenin basit bir yolunu gösterir:

```CPP
#include <iostream>
#include <memory>

int main() {
  std::shared_ptr<int> ptr(new int(42));
  std::cout << *ptr << '\n'; // 42
  return 0;
}

```
- Bu örnekte, std::shared_ptr sınıfından bir nesne oluşturulur ve bellek alanı tahsis edilir. Daha sonra, std::shared_ptr nesnesi kullanılarak bu bellek alanındaki değere erişilir. Program sonlandığında, std::shared_ptr nesnesi otomatik olarak bellekten silinir ve bellekte sızıntı oluşmaz.

- std::shared_ptr sınıfı, diğer akıllı işaretçi sınıflarıyla birlikte kullanılabilir. Örneğin, bir std::shared_ptr nesnesi, bir std::unique_ptr nesnesine dönüştürülebilir.

``CPP
#include <iostream>
#include <memory>

int main() {
  std::shared_ptr<int> shared_ptr(new int(42));
  std::unique_ptr<int> unique_ptr = std::move(shared_ptr);
  std::cout << *unique_ptr << '\n'; // 42
  return 0;
}

```
- Bu örnekte, std::shared_ptr nesnesi bir std::unique_ptr nesnesine dönüştürülür. Bu, aynı bellek alanı üzerinde yalnızca bir sahip olma durumu için kullanışlıdır.

- std::shared_ptr sınıfı, bellek sızıntılarını önlemek için oldukça kullanışlı bir araçtır ve dinamik bellek yönetimi ile ilgili sorunları azaltır. Ancak, birden fazla sahip olma durumunda işaretçilerin hayat döngülerinin iyi yönetilmesi önemlidir.

# std::weak_ptr

- std::weak_ptr, C++11'de standart kütüphaneye eklenen bir akıllı işaretçi sınıfıdır. std::shared_ptr gibi bir işaretçi nesnesine sahip olur, ancak std::shared_ptr gibi nesneye doğrudan sahip değildir.

- std::weak_ptr'ın amacı, std::shared_ptr'ın zayıf (weak) bir referansını oluşturmaktır. std::weak_ptr'ın sahip olduğu nesneye işaret eden bir referansı yoktur, sadece bir std::shared_ptr nesnesinin sahip olduğu nesneye işaret eden bir işaretçisi vardır.

- std::weak_ptr sınıfı, belirli bir nesneye birden fazla std::shared_ptr nesnesi sahip olduğunda, nesneyi bellekten silmek için bir yol sağlar. std::shared_ptr nesneleri, nesne hala yaşamakta iken sayacı sıfıra düştüğünde nesneyi bellekten silmek için sorumludur. Ancak, std::shared_ptr nesnelerinin sayacı sıfıra düşene kadar nesne yaşamaya devam edebilir. Bu durumda, std::weak_ptr nesnesi, nesnenin hala bellekte olduğunu gösterir ve nesne silinmeden önce ona işaret eden std::shared_ptr nesnelerinin silinmesini önlemek için kullanılabilir.

- Aşağıdaki örnekte, bir std::weak_ptr nesnesi oluşturulur ve bir std::shared_ptr nesnesine dönüştürülür:

```CPP
#include <iostream>
#include <memory>

int main() {
  std::shared_ptr<int> shared_ptr(new int(42));
  std::weak_ptr<int> weak_ptr(shared_ptr);
  std::cout << *weak_ptr.lock() << '\n'; // 42
  return 0;
}

```

- Bu örnekte, std::weak_ptr nesnesi, std::shared_ptr nesnesine dönüştürülür. Daha sonra, std::weak_ptr nesnesi, std::shared_ptr nesnesine işaret eder. std::weak_ptr sınıfının lock() üye işlevi kullanılarak, std::shared_ptr nesnesine dönüştürülür ve nesneye işaret eden değere erişilebilir.

- std::weak_ptr sınıfı, dinamik bellek yönetimi ile ilgili sorunları azaltmaya yardımcı olan std::shared_ptr sınıfı ile birlikte kullanılır. Ancak, std::weak_ptr nesnelerinin işaret ettiği nesnenin silinip silinmediğini kontrol etmek önemlidir. Aksi takdirde, std::weak_ptr nesnesi, artık geçersiz bir bellek bölgesine işaret edebilir.

# std::make_unique

- std::make_unique C++14'te standart kütüphaneye eklenen bir işlev şablonudur. Dinamik bellek yönetimi için std::unique_ptr işaretçisiyle birlikte kullanılır ve bellekte bir nesne oluşturur. std::make_unique, new operatörüne göre daha güvenlidir, çünkü otomatik olarak bellek yönetimi ile ilgili kodu işletir.

- std::make_unique işlev şablonu, verilen argümanlara dayalı olarak, dinamik olarak bir nesne oluşturur ve bir std::unique_ptr nesnesiyle işaret eder. Örnek olarak, aşağıdaki kod, bir tamsayı dizisi oluşturur ve bu diziyi bir std::unique_ptr nesnesiyle işaret eder:

```CPP
std::unique_ptr<int[]> p = std::make_unique<int[]>(10);

```

- Bu örnekte, std::make_unique işlev şablonu, 10 elemanlı bir tamsayı dizisi oluşturur ve bu dizinin ilk elemanına işaret eden bir std::unique_ptr nesnesi döndürür.

- std::make_unique işlev şablonu, dinamik bellek yönetimi ile ilgili sorunları azaltmaya yardımcı olur ve bellekteki nesnelerin yönetimini daha güvenli hale getirir. Ayrıca, kodun okunabilirliğini artırır ve tekrar kullanılabilirliği artırır.

-  Aşağıdaki örnekte, std::make_unique kullanarak bir std::unique_ptr işaretçisiyle işaret edilen 3 elemanlı bir tamsayı dizisi oluşturuyoruz:

```CPP
#include <memory>
#include <iostream>

int main() {
    // 3 elemanlı bir tamsayı dizisi oluştur
    auto arr = std::make_unique<int[]>(3);

    // dizi elemanlarını ayarla
    arr[0] = 1;
    arr[1] = 2;
    arr[2] = 3;

    // dizi elemanlarını yazdır
    for (int i = 0; i < 3; i++) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;

    return 0;
}

```
- Bu örnekte, std::make_unique işlev şablonu, 3 elemanlı bir tamsayı dizisi oluşturur ve bunu bir std::unique_ptr işaretçisiyle işaret eder. Daha sonra, bu dizinin elemanlarını ayarlarız ve son olarak, dizi elemanlarını ekrana yazdırırız. std::make_unique işlev şablonu sayesinde, dinamik bellek yönetimini otomatik olarak hallederiz ve kod daha güvenli ve okunaklı hale gelir.

# std::make_shared

- std::make_shared C++11'de standart kütüphaneye eklenen bir işlev şablonudur. Dinamik bellek yönetimi için std::shared_ptr işaretçisiyle birlikte kullanılır ve bellekte bir nesne oluşturur. std::make_shared, new operatörüne göre daha güvenlidir, çünkü otomatik olarak bellek yönetimi ile ilgili kodu işletir.

- std::make_shared işlev şablonu, verilen argümanlara dayalı olarak, dinamik olarak bir nesne oluşturur ve bir std::shared_ptr nesnesiyle işaret eder. Örnek olarak, aşağıdaki kod, bir tamsayı oluşturur ve bu sayıyı bir std::shared_ptr nesnesiyle işaret eder:


```CPP
std::shared_ptr<int> p = std::make_shared<int>(42);

```

- Bu örnekte, std::make_shared işlev şablonu, 42 değerini içeren bir tamsayı nesnesi oluşturur ve bu nesneyi bir std::shared_ptr nesnesiyle işaret eder.

- std::make_shared işlev şablonu, dinamik bellek yönetimi ile ilgili sorunları azaltmaya yardımcı olur ve bellekteki nesnelerin yönetimini daha güvenli hale getirir. Ayrıca, kodun okunabilirliğini artırır ve tekrar kullanılabilirliği artırır.

- Aşağıdaki örnekte, std::make_shared kullanarak bir std::shared_ptr işaretçisiyle işaret edilen bir Person nesnesi oluşturuyoruz:

```CPP
#include <memory>
#include <iostream>
#include <string>

class Person {
public:
    Person(const std::string& name, int age) : name_(name), age_(age) {}
    void print() {
        std::cout << "Name: " << name_ << ", Age: " << age_ << std::endl;
    }

private:
    std::string name_;
    int age_;
};

int main() {
    // shared_ptr ile bir Person nesnesi oluştur
    auto personPtr = std::make_shared<Person>("John Doe", 30);

    // nesneyi kullan
    personPtr->print();

    return 0;
}

```

- Bu örnekte, std::make_shared işlev şablonu, Person sınıfından bir nesne oluşturur ve bu nesneyi bir std::shared_ptr işaretçisiyle işaret eder. Daha sonra, bu nesneyi kullanarak print() işlevini çağırarak, nesnenin adını ve yaşını ekrana yazdırırız. std::make_shared işlev şablonu, dinamik bellek yönetimini otomatik olarak halleder ve kod daha güvenli ve okunaklı hale gelir.

# std::allocator

- std::allocator C++ standart kütüphanesinde yer alan bir sınıftır. Bellek tahsisi ve serbest bırakma işlemlerini yönetmek için kullanılır. Bu sınıf, veri tipleri için bellek tahsisi ve serbest bırakma işlemlerini ele almak için kullanılır. Özellikle, özelleştirilmiş veri yapıları için bellek yönetimi için kullanılabilir.

- std::allocator sınıfı, C++ dilindeki new ve delete anahtar kelimelerinin yerine kullanılabilir. std::allocator sınıfı, bellek yönetimi işlemlerini yaparken, bellek havuzları kullanarak bellek yönetimini optimize eder.

- Aşağıdaki örnekte, std::allocator sınıfının kullanımı gösterilmiştir. Bu örnekte, bir int dizisi için bellek tahsisi yapmak için std::allocator sınıfı kullanılmıştır.

```CPP
#include <iostream>
#include <memory>

int main() {
    std::allocator<int> alloc; // int türü için bir allocator nesnesi oluştur

    int* arr = alloc.allocate(5); // 5 tane int için bellek tahsisi yap

    for (int i = 0; i < 5; i++) {
        arr[i] = i + 1; // dizi elemanlarını ayarla
    }

    for (int i = 0; i < 5; i++) {
        std::cout << arr[i] << " "; // dizi elemanlarını yazdır
    }
    std::cout << std::endl;

    alloc.deallocate(arr, 5); // bellek alanını serbest bırak

    return 0;
}

```

- Bu örnekte, std::allocator sınıfından bir nesne oluşturarak, int veri tipi için bellek tahsis ediyoruz. Daha sonra, bu bellek alanını kullanarak bir dizi oluşturuyoruz ve elemanlarını ayarlıyoruz. Son olarak, deallocate() işleviyle bellek alanını serbest bırakıyoruz. std::allocator sınıfı, dinamik bellek yönetimini optimize etmek için bellek havuzlarını kullanır ve bellek yönetimi işlemlerini daha güvenli ve okunaklı hale getirir.

# std::addressof

- std::addressof C++ standart kütüphanesinde bulunan bir işlev şablonudur. Bu işlev şablonu, bir nesnenin bellek adresini döndürür. Bu işlev, özellikle C++11'den önce, işaretçi almak yerine bir nesnenin adresini almak için kullanılırdı. std::addressof işlevi, & adres operatörünün aksine bir constexpr işlev olduğundan, derleme zamanında hesaplanabilir ve bu nedenle daha verimli olabilir.

- Aşağıdaki örnekte, std::addressof işlevinin kullanımı gösterilmiştir:

```CPP
#include <iostream>
#include <memory>

int main() {
    int n = 10;

    int* p = &n;
    int* q = std::addressof(n);

    std::cout << "p = " << p << std::endl;
    std::cout << "q = " << q << std::endl;

    return 0;
}

```

- Bu örnekte, bir int türünden n adlı bir değişken tanımlıyoruz. Daha sonra, p ve q adında iki işaretçi tanımlıyoruz. p işaretçisi, & adres operatörünü kullanarak n değişkeninin adresini alırken, q işaretçisi std::addressof işlevini kullanarak n değişkeninin adresini alır. Bu iki işaretçinin değerleri, ekrana yazdırılarak, & adres operatörü ve std::addressof işlevinin farkı gösterilir.

- std::addressof işlevi, bir nesnenin adresini almaya özelleştirilmiş sınıflarda kullanılabilir. Özellikle, bir sınıfın operator&() işlevi özelleştirilmişse, bir nesnenin adresini almak & adres operatörünü kullanarak mümkün olmayabilir. Bu durumda, std::addressof işlevi kullanılarak nesnenin adresi alınabilir.























































