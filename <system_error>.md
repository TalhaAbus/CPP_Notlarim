- <system_error> başlık dosyası, hata kodları ve hata kategorileri gibi hata işleme araçları sağlayan C++ standart kütüphanesinin bir parçasıdır. Bu başlık dosyası, özellikle işletim sistemi işlevleri gibi sistem çağrıları sırasında oluşabilecek hataları işlemek için kullanılır.

- Bu başlık dosyası, std::error_code, std::error_category ve std::system_error gibi sınıfları içerir. std::error_code, bir sistem hatası kodunu ve bir std::error_category nesnesini içeren bir nesnedir. std::error_category, belirli bir hatanın kategorisini temsil eden bir sınıftır. std::system_error, bir sistem hatası kodunu ve bu hatanın kategorisini içeren bir nesnedir.

- Bu başlık dosyası, özellikle dosya ve ağ işlemleri gibi sistem çağrılarında meydana gelebilecek hataların ele alınmasında yaygın olarak kullanılır. Örneğin, bir dosya açarken hata oluştuğunda, std::system_error kullanarak hatayı ele alabilirsiniz.

- Aşağıda bir örnek verilmiştir:

```CPP
#include <iostream>
#include <fstream>
#include <system_error>

int main() {
    std::ifstream file("example.txt");

    if (!file) {
        std::error_code ec = std::make_error_code(std::errc::no_such_file_or_directory);
        throw std::system_error(ec, "Failed to open file");
    }

    // ...

    return 0;
}

```

- Bu örnekte, example.txt dosyası açılamazsa, bir std::system_error nesnesi oluşturularak hata ele alınır.

# Burada exception da kullanabilirdik

- Evet, C++'ta hata yönetimi için exception sınıfı kullanılabileceği gibi, system_error sınıfı da kullanılabilir. exception sınıfı, bir programın çalışması sırasında beklenmeyen bir durum oluştuğunda atılan bir hata nesnesi olarak düşünülebilir. system_error sınıfı ise, sistem çağrıları sırasında hata oluştuğunda kullanılabilir. system_error sınıfı, C++11'den önce mevcut değildi ve C++11 ile birlikte standarta eklendi.

- system_error sınıfı, sistem çağrılarının döndürdüğü hata kodlarını ve bu hata kodlarına karşılık gelen hata mesajlarını işlemek için kullanılabilir. Bu sayede, sistem çağrıları sırasında oluşan hataları daha ayrıntılı bir şekilde ele almak mümkün hale gelir.

- Örneğin, bir dosya okuma işlemi sırasında bir hata oluştuğunda, system_error sınıfı kullanılarak bu hatanın ayrıntılarına erişilebilir ve gerekli işlemler yapılabilir.

# Neden exception yerine system_error kullanayim

- std::system_error ve std::exception farklı hataların yakalanmasına ve işlenmesine yönelik farklı mekanizmalar sağlarlar.

- std::exception sınıfı, hata yakalama ve işleme mekanizmalarında kullanılan genel bir arayüz sağlar. Bu sınıfın alt sınıfları daha özelleştirilmiş hata türleri için kullanılabilir ve kullanıcıya hata mesajı ve ayrıntılarını verir.

- Öte yandan std::system_error, genellikle sistem çağrıları sırasında veya sistemle etkileşimli işlemlerde oluşan hataları yakalamak için kullanılır. Bu hatalar genellikle bir hata kodu veya bir sistem tanımlayıcısı ile belirtilir ve bu hataların ne olduğu ve nasıl ele alınacağı sistemden sisteme değişebilir.

- Dolayısıyla, std::system_error özellikle sistem seviyesinde hataları işlemek için tasarlanmışken, std::exception daha genel bir hata işleme mekanizmasıdır. Hangi sınıfın kullanılacağı, hata türüne ve uygulamanın gereksinimlerine bağlı olarak değişebilir.

- Aşağıdaki örnekte std::system_error kullanılarak bir hata durumunda throw ifadesi ile bir hata nesnesi oluşturuluyor ve bu nesne catch bloğunda yakalanıyor:

```CPP
#include <iostream>
#include <system_error>

int main() {
    try {
        // Bir hata durumunu taklit edelim
        throw std::system_error(std::error_code(404, std::generic_category()), "Dosya bulunamadı");
    } catch(const std::system_error& e) {
        std::cout << "Hata yakalandı: " << e.what() << std::endl;
    }
    return 0;
}

```

- Bu örnekte, bir hata durumunu taklit etmek için throw ifadesi ile std::system_error sınıfından bir nesne oluşturuluyor. Bu nesne, std::error_code nesnesi tarafından sağlanan bir hata kodu ve bir hata mesajı ile başlatılıyor.

- catch bloğu, bir std::system_error nesnesi tarafından fırlatılan hataları yakalayarak, hata mesajını ekrana yazdırıyor.




























