- C++20'de tanıtılan <syncstream> başlık dosyası, çoklu iplikli uygulamalarda standart çıkış akışlarının güvenli bir şekilde kullanımını sağlamak için bir dizi senkronizasyonlu akış sınıfı içerir.

- Bu başlık dosyasındaki ana sınıf std::basic_osyncstream'dir. Bu sınıf, std::basic_ostream sınıfından miras alır ve bir std::basic_ostream nesnesine benzer şekilde kullanılır, ancak çoklu iplikli bir ortamda güvenli bir şekilde kullanım için ek senkronizasyon özellikleri sağlar.

- Ayrıca, <syncstream> başlık dosyası std::osyncstream ve std::wosyncstream sınıflarını da tanıtır. Bu sınıflar, std::basic_osyncstream sınıfının tamsayı ve karater dizisi türleri için özellemeleridir.

- Bir örnek olarak, std::osyncstream sınıfı, kullanıcının standart çıkış akışına yazdığı çıktıların diğer iş parçacıkları tarafından aynı anda yazılmasını engelleyen bir mekanizma sağlar. Örneğin, aşağıdaki kod, "Hello, world!" çıktısının güvenli bir şekilde yazdırılmasını sağlar:
```CPP
#include <iostream>
#include <syncstream>
#include <thread>

int main() {
    std::osyncstream(std::cout) << "Hello, world!" << std::endl;
    return 0;
}

```
# çoklu iplikli uygulama ne demek? Bu terimin ingilizce karşılığı nedir
- Çoklu iplikli uygulama, aynı anda birden fazla işlemi yürütmek için birden fazla iş parçacığının kullanıldığı bir programdır. İngilizce karşılığı "multithreaded application" olarak geçmektedir.

# Bu pratikte karşımıza ne gibi örnekler ile çıkar
- Çoklu iplikli uygulamalar, birden fazla işlemci çekirdeği veya işlem hattı olan modern bilgisayarlarda yaygın bir şekilde kullanılır. Bu tür uygulamalar genellikle performansı artırmak, iş yükünü dağıtmak veya eşzamanlı olarak birden fazla görevi gerçekleştirmek amacıyla kullanılır.

- Örnek olarak, web sunucuları çoklu iplikli uygulamalara örnek olarak gösterilebilir. Web sunucuları, aynı anda birçok istemci isteğini işlemek zorunda olduğundan, her istek için ayrı bir iş parçacığı oluşturarak veya async/await kullanarak performansı artırabilirler. Benzer şekilde, büyük veri işleme, yapay zeka, oyun geliştirme ve multimedya işleme gibi diğer alanlarda da çoklu iplikli uygulamalar kullanılır.


# nasıl çalışır

- std::sync_ostream nesnesi, bir std::ostream nesnesi gibi davranır, ancak her yazdırma işlemi için bir mutex kullanarak senkronizasyonu sağlar. Yani, bir std::sync_ostream nesnesine yazdırılan veriler, tüm iş parçacıklarının erişimini koordine eden bir mutex tarafından korunur.

- Bu şekilde, farklı iş parçacıklarının aynı anda aynı std::sync_ostream nesnesine yazmaları durumunda, bir iş parçacığının çıktısının diğerinden önce veya araya girmesi gibi durumlar engellenir. Her zaman sırayla yazdırma yapılır ve bu sayede çıktıda bir tutarsızlık oluşmaz.

- şöyle bir örnek yazabilirim:

```CPP
#include <iostream>
#include <thread>
#include <vector>
#include <mutex>

using namespace std;

int main() {
    const int NUM_THREADS = 5;
    vector<thread> threads(NUM_THREADS);
    mutex output_mutex; // Çıkışı korumak için mutex oluşturuldu

    for (int i = 0; i < NUM_THREADS; ++i) {
        threads[i] = thread([&output_mutex, i]() {
            output_mutex.lock(); // Çıkışı kilitle
            cout << "Thread " << i << " started.\n";
            output_mutex.unlock(); // Çıkışı kilidini aç
        });
    }

    for (auto& t : threads) {
        t.join();
    }

    return 0;
}

```
> Bu örnekte, mutex kullanarak, her iş parçacığının ayrı ayrı konsol çıktısı yazmasını sağlıyoruz. Bu sayede, iş parçacıkları arasında birbirlerinin çıktılarını karıştırmadan, sırayla çalışıyorlar.












