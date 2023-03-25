# std::exception nedir

- std::exception sınıfı, C++ standart kütüphanesinin temel sınıflarından biridir. Bu sınıf, istisnai durumlar için bir temel sınıf olarak kullanılır ve programcıların hata mesajları oluşturması için bir arayüz sağlar.

- std::exception sınıfı, what adında bir üye işlevi sağlar. Bu işlev, bir const char* türündeki bir hata mesajı döndürür ve genellikle try-catch bloklarında kullanılır. what işlevi, hata nedenini açıklayan bir metin dizesi döndürür.

- std::exception sınıfı, özelleştirilmiş istisna sınıfları için bir temel sınıf olarak kullanılır. Özelleştirilmiş bir istisna sınıfı, std::exception sınıfından kalıtım alarak oluşturulabilir. Bu şekilde, özelleştirilmiş bir istisna sınıfı, what işlevini sağlayan bir std::exception nesnesi olarak davranabilir.

- Aşağıda, std::exception sınıfının kullanımına dair bir örnek verilmiştir:

```CPP
#include <iostream>
#include <exception>

class MyException : public std::exception {
public:
    const char* what() const noexcept {
        return "Bu benim özelleştirilmiş istisna sınıfım.";
    }
};

int main() {
    try {
        throw MyException();
    }
    catch (std::exception& e) {
        std::cout << "Hata: " << e.what() << std::endl;
    }

    return 0;
}

```
> Bu örnekte, std::exception sınıfından türetilen MyException adlı bir özelleştirilmiş istisna sınıfı oluşturulur. Bu sınıf, what işlevini yeniden tanımlar ve özelleştirilmiş bir hata mesajı döndürür. Sonrasında, try-catch blokları kullanılarak özelleştirilmiş istisna sınıfı MyException fırlatılır ve yakalanır. Yakalandıktan sonra, hata mesajı what işlevi kullanılarak yazdırılır.


# exception

- exception (istisna) mekanizması, programların normal akışını bozan ve programcıların önceden tahmin edemediği hataların ortaya çıkmasını sağlayan bir mekanizmadır. Bu mekanizma sayesinde, programlar hata durumlarına karşı daha güvenilir hale getirilebilir ve hata durumlarından kurtulmak için özel işlemler yapılabilir.

- C++ dilinde, try-catch blokları kullanılarak istisna mekanizması uygulanır. Bir try bloğu, potansiyel bir istisna durumuna neden olabilecek kodu içerir. Eğer bu kod bir istisna durumuna neden olursa, throw anahtar kelimesi kullanılarak istisna nesnesi fırlatılır ve yakalanması gereken catch blokları aranmaya başlanır.

- catch blokları, fırlatılan istisna nesnesini yakalar ve uygun işlemleri yapar. Birden fazla catch bloğu kullanılabilir ve bu bloklar, fırlatılan istisna nesnesinin tipine göre sırayla denenecektir. Eğer bir catch bloğu, fırlatılan istisna nesnesinin tipine uymazsa, bir sonraki catch bloğu denenecektir.

- İstisna mekanizması, programlarda hata durumlarına karşı daha iyi bir kontrol sağlar ve hata durumlarında özel işlemler yapılmasına izin verir. Örneğin, bir dosya okuma işlemi sırasında hata oluşursa, istisna mekanizması kullanılarak hatanın nedeni tespit edilebilir ve kullanıcıya uygun bir mesaj gösterilebilir. Benzer şekilde, bellek yönetimi işlemleri sırasında ortaya çıkan hatalar da istisna mekanizması kullanılarak ele alınabilir.

- Sonuç olarak, exception mekanizması, programların daha güvenilir ve daha hatasız olmasını sağlayan önemli bir mekanizmadır ve pratik uygulamalarda sıklıkla kullanılır.

- Aşağıdaki örnek, dosya okuma işlemi sırasında oluşabilecek hata durumlarının nasıl ele alınabileceğine dair bir örnek sunar:

```CPP
#include <iostream>
#include <fstream>
#include <string>
#include <stdexcept>

int main() {
    std::string filename = "dosya.txt";
    std::ifstream file(filename);

    try {
        if (!file) {
            throw std::runtime_error("Dosya açılamadı.");
        }

        std::string line;
        while (getline(file, line)) {
            std::cout << line << std::endl;
        }
    }
    catch (std::exception& e) {
        std::cerr << "Hata: " << e.what() << std::endl;
    }

    return 0;
}

```

- Bu örnekte, std::ifstream sınıfı kullanılarak bir dosya açılır ve getline işlevi kullanılarak dosyanın satırları okunur. try-catch blokları kullanılarak, dosya açma işlemi sırasında oluşabilecek hata durumları ele alınır. Eğer dosya açılamazsa, throw anahtar kelimesi kullanılarak std::runtime_error tipinde bir istisna nesnesi fırlatılır. Yakalanması gereken catch bloğu, fırlatılan istisna nesnesini yakalar ve hata mesajı yazdırır.

- Bu örnekte, istisna mekanizması kullanılarak, dosya okuma işlemi sırasında oluşabilecek hata durumlarına karşı bir önlem alınmıştır. Eğer dosya açılamazsa, kullanıcıya uygun bir hata mesajı gösterilir ve program sonlanmadan önce istisna nesnesi yakalanır.

# Exception throw edildikten hemen sonra programin akisi kesilip catch bloklarina mi gidiyor? Eger uygun catch blogu yoksa ne olacak?

- Evet, bir istisna nesnesi fırlatıldıktan sonra programın akışı kesilir ve yakalanması gereken catch blokları aranmaya başlanır. Eğer uygun bir catch bloğu bulunamazsa, programın çalışması sonlandırılır ve kullanıcıya bir hata mesajı gösterilir.

- Istisna mekanizması, bir hatanın ortaya çıktığı durumlarda programın hemen sonlandırılmasını önlemek ve hata durumuna uygun işlemler yapılmasını sağlamak için kullanılır. Bir throw ifadesi çalıştırıldıktan sonra, programın akışı hemen kesilir ve istisna nesnesi, uygun catch bloklarına kadar aranmaya devam eder. Bu nedenle, uygun catch bloklarının yazılması önemlidir ve bir throw ifadesinin programın sonlanmasına neden olmaması için gereklidir.

- Eğer uygun bir catch bloğu bulunamazsa, programın çalışması sonlandırılır ve bir hata mesajı gösterilir. Bu durumda, kullanıcıya bir hata mesajı gösterilerek, programın neden hata verdiği ve ne yapılması gerektiği hakkında bilgi verilir.

- Evet, uygun catch bloğu bulunduktan sonra, program kaldığı yerden devam eder. catch bloğu, fırlatılan istisna nesnesini yakalar ve uygun işlemleri yapar. Eğer işlemler başarılı bir şekilde tamamlanırsa, programın akışı normale döner ve program devam eder.

- Istisna mekanizması, programların hata durumlarında daha kontrol edilebilir olmasını sağlar ve programın hemen sonlanmasını önler. Bir catch bloğu, fırlatılan istisna nesnesini yakalayarak, uygun işlemleri yapabilir ve programın hata durumundan kurtulmasını sağlayabilir. Bu nedenle, uygun catch bloklarının yazılması önemlidir ve bir throw ifadesinin programın sonlanmasına neden olmaması için gereklidir.

- Ancak, istisna mekanizması doğru bir şekilde kullanılmadığında, programın performansını olumsuz etkileyebilir ve hatta bazı durumlarda programın çökmesine neden olabilir. Bu nedenle, istisna mekanizmasının doğru kullanımı ve uygun durumlarda kullanılması önemlidir.

# Senin verdigin ornek kodda, catch blogu hatayi yakaladiktan sonra ne gibi bir cozum uretilebilir? Cunku dosya acilmadigi icin bir istisna nesnesi firlatiliyor

- Verdiğim örnekte, dosya açma işlemi sırasında oluşabilecek hataları yakalamak için bir try-catch bloğu kullanılmıştı. Eğer dosya açılamazsa, throw anahtar kelimesi kullanılarak std::runtime_error tipinde bir istisna nesnesi fırlatılır. Yakalanması gereken catch bloğu, fırlatılan istisna nesnesini yakalar ve hata mesajı yazdırır.

- Bu örnekte, hatanın doğasına ve programın gereksinimlerine göre farklı işlemler yapılabilir. Örneğin, dosya açma işlemi sırasında oluşan hata, kullanıcının uygun bir hata mesajı görmesine neden olabilir. Bu durumda, catch bloğu kullanılarak bir hata mesajı gösterilebilir.

- Ayrıca, dosya açma işlemi sırasında oluşan hata, programın akışını etkileyebilir ve programın diğer işlemlerini yapmasına engel olabilir. Bu durumda, hata durumuna uygun bir işlem yapılması gerekebilir. Örneğin, dosya açma işlemi sırasında oluşan hata, programın sonlandırılmasına neden olabilir veya alternatif bir dosya açılabilir.

- Özetle, catch bloğu kullanılarak fırlatılan istisna nesnesi yakalanabilir ve hata durumuna uygun işlemler yapılabilir. Hangi işlemlerin yapılacağı, hatanın doğasına ve programın gereksinimlerine bağlıdır.
