C++20 standardı ile birlikte tanıtılan <source_location> başlık dosyası, C++ kodunun kaynak konumunu temsil etmek için kullanılır. Bu başlık dosyasında yer alan sınıflar ve fonksiyonlar, kodun hangi dosya, satır ve sütunlarda yazıldığını, hangi işlevin hangi satırında çağrıldığını veya hangi kaynak dosyasından dahil edildiğini tanımlamak için kullanılır.

Bu başlık dosyasındaki en önemli sınıf std::source_location'dır. Bu sınıf, kaynak konumunu temsil eder. Sınıfın üyeleri arasında dosya adı, satır numarası, sütun numarası ve işlev adı bulunur.

Aşağıda bir örnek kod verilmiştir:

```CPP
#include <iostream>
#include <source_location>

void foo() {
    const std::source_location loc = std::source_location::current();
    std::cout << "Function name: " << loc.function_name() << std::endl;
    std::cout << "File name: " << loc.file_name() << std::endl;
    std::cout << "Line number: " << loc.line() << std::endl;
}

int main() {
    foo();
    return 0;
}

```
> Bu örnekte, foo() işlevi çağrıldığında std::source_location sınıfının current() üyesi kullanılarak kaynak konumu alınır ve sonrasında işlev adı, dosya adı ve satır numarası ekrana yazdırılır. Bu, özellikle hata ayıklama veya kaynak kodu analizi yaparken yararlıdır.

- C++20 ile birlikte getirilen <source_location> başlık dosyası, kodun kaynak dosyasındaki konumunu (dosya adı, satır numarası vb.) sağlar. Bu bilgiler, hata ayıklama, günlükleme ve performans izleme gibi senaryolarda kullanılabilir.

- Bu başlık dosyası sadece bir sınıf içerir: std::source_location. Bu sınıfın dört adet public üyesi vardır: dosya adı, satır numarası, sütun numarası ve işlev adı.

- source_location sınıfı genellikle kullanıcının doğrudan çağırmayacağı yardımcı işlevler tarafından kullanılır. Örneğin, bir loglama işlevi, kaynak konumunu otomatik olarak yakalayarak kullanıcının çağırdığı her yerde o anda çalışan kodun dosya adı ve satır numarasını kaydedebilir. Bu sayede, programda oluşan hataları veya performans sorunlarını daha kolay tespit edebilirsiniz.

- Örnek kullanım:

```CPP
#include <iostream>
#include <source_location>

void log(const std::string& message, const std::source_location& loc = std::source_location::current()) {
    std::cout << "[" << loc.file_name() << ":" << loc.line() << "] " << message << std::endl;
}

int main() {
    log("Hello, world!");
    return 0;
}

```

> Bu örnekte, log() işlevi bir mesaj ve kaynak konumu alır ve bu mesajı loglar. Kaynak konumu, varsayılan olarak çağrıldığı yeri (yani, std::source_location::current()) kullanır.

- Tabii, şöyle bir örnek yazabilirim:

```CPP
#include <iostream>
#include <source_location>

void foo(const std::source_location& loc = std::source_location::current()) {
    std::cout << "Function " << loc.function_name() << " called from " 
              << loc.file_name() << ":" << loc.line() << "\n";
}

int main() {
    foo(); // default argument ile çağrıldı
    foo(std::source_location::current()); // doğrudan source_location nesnesi verilerek çağrıldı
    return 0;
}

```

> Bu örnekte, foo fonksiyonu çağrılırken std::source_location sınıfının current fonksiyonu kullanılarak bir nesne oluşturuldu ve fonksiyon bu nesne ile çağrıldı. Fonksiyonun içinde, source_location nesnesi kullanılarak, fonksiyonun adı, dosya adı ve satır numarası yazdırıldı. İkinci çağrıda ise current fonksiyonu doğrudan çağrıldı.









