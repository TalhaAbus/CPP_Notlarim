- <shared_mutex> başlık dosyası, C++11'de tanıtılan std::shared_mutex sınıfını içerir. Bu sınıf, aynı anda birden fazla okuma işlemine izin veren bir kilit mekanizması sağlar, ancak yazma işlemlerini yalnızca tek bir thread'e izin verir.

- Bu sınıf, std::mutex sınıfının bir uzantısıdır ve birçok iş parçacığı uygulamasında kullanışlıdır. Özellikle, paylaşılan bir kaynağa birden fazla okuyucu thread'in aynı anda erişebilmesi gereken senaryolarda kullanılır.

- Aşağıda, std::shared_mutex sınıfının kullanımına ilişkin bir örnek verilmiştir:

```CPP
#include <iostream>
#include <thread>
#include <mutex>
#include <shared_mutex>
#include <vector>

std::vector<int> data;
std::shared_mutex data_mutex;

void reader_thread()
{
    while (true) {
        std::shared_lock<std::shared_mutex> lock(data_mutex);
        std::cout << "Data: ";
        for (auto i : data) {
            std::cout << i << " ";
        }
        std::cout << std::endl;
        std::this_thread::sleep_for(std::chrono::seconds(1));
    }
}

void writer_thread()
{
    while (true) {
        std::unique_lock<std::shared_mutex> lock(data_mutex);
        data.push_back(rand() % 100);
        std::cout << "Added " << data.back() << " to data" << std::endl;
        std::this_thread::sleep_for(std::chrono::seconds(1));
    }
}

int main()
{
    std::thread reader(reader_thread);
    std::thread writer(writer_thread);

    reader.join();
    writer.join();
}

```

> Bu örnekte, std::shared_mutex kullanarak bir std::vector nesnesine aynı anda birden fazla okuyucu thread'in erişebildiği, ancak yalnızca bir yazma thread'inin erişebildiği bir senaryo oluşturulmuştur. std::shared_lock sınıfı, okuma işlemleri için kullanılırken, std::unique_lock sınıfı, yazma işlemleri için kullanılır.

# bu baslik dosyasinin icerigi nedir? nasil kullanabiliriz

- <shared_mutex> başlık dosyası, C++11'den itibaren desteklenen bir senkronizasyon aracı olan shared_mutex sınıfını içerir. Bu sınıf, özellikle birden fazla okuyucu ve yalnızca bir yazar arasında bir veri yapısını paylaşmak istediğimiz durumlarda kullanışlıdır.

- shared_mutex sınıfı, benzer bir şekilde çalışan mutex sınıfına benzer. Ancak, bir mutex sınıfı sadece bir thread tarafından kilitlenebilirken, bir shared_mutex sınıfı birden fazla thread tarafından kilitlenebilir. shared_mutex sınıfı, özellikle bir veri yapısının yazma işlemi dışında okuma işlemlerinin sıklıkla gerçekleştirildiği senaryolarda kullanışlıdır. Bu sayede birden fazla okuyucunun aynı anda veri yapısına erişebilmesine izin verilirken, yazma işlemi sırasında erişim kilitlenir.

- Bu başlık dosyasının kullanımı, bir shared_mutex nesnesi oluşturarak başlar. Bu nesne, sırayla kilitlemek veya kilidini açmak için lock() ve unlock() yöntemleri kullanılarak kullanılır. Ayrıca, bir unique_lock nesnesi kullanarak lock() yöntemini de çağırabilirsiniz. shared_mutex sınıfının bir diğer önemli yöntemi ise try_lock() yöntemidir, bu yöntemde bir kilit edinme işlemi gerçekleştirir ancak işlem başarısız olursa false değer döndürür.

- shared_mutex sınıfının bir diğer önemli özelliği ise, bir read lock (okuma kilidi) veya write lock (yazma kilidi) kullanarak işlem yapabilmemizi sağlamasıdır. Böylece, bir okuma kilidi ile birlikte aynı anda birden fazla thread okuyabilirken, yazma kilidi ile bir thread yazabilir ve diğer tüm threadlerin bu işlemden haberi olur. Bu sayede bir veri yapısının bütünlüğü korunmuş olur.

- Kısacası, shared_mutex sınıfı, aynı anda birden fazla okuyucu ve yalnızca bir yazar arasında bir veri yapısını paylaşmak istediğimiz senaryolarda kullanışlı bir senkronizasyon aracıdır.

**şöyle bir örnek yazabiliriz:**

```CPP
#include <iostream>
#include <thread>
#include <shared_mutex>
#include <vector>

std::vector<int> numbers; // shared resource
std::shared_mutex mutex;

void write_thread() {
    for (int i = 0; i < 5; ++i) {
        std::unique_lock<std::shared_mutex> lock(mutex);
        std::cout << "Adding " << i << std::endl;
        numbers.push_back(i);
        std::this_thread::sleep_for(std::chrono::milliseconds(100)); // simulate work
    }
}

void read_thread() {
    while (true) {
        std::shared_lock<std::shared_mutex> lock(mutex);
        std::cout << "Reading: ";
        for (const auto& n : numbers) {
            std::cout << n << " ";
        }
        std::cout << std::endl;
        std::this_thread::sleep_for(std::chrono::milliseconds(200)); // simulate work
    }
}

int main() {
    std::thread t1(write_thread);
    std::thread t2(read_thread);
    t1.join();
    t2.join();
    return 0;
}

```

- Bu örnekte, bir std::vector<int> nesnesi, iki farklı iş parçacığı tarafından paylaşılıyor: yazma işlemleri için write_thread() fonksiyonu ve okuma işlemleri için read_thread() fonksiyonu.

- Yazma işlemleri kilitlenerek gerçekleştirilirken (std::unique_lock<std::shared_mutex>), okuma işlemleri paylaşımlı okuma kilidi ile (std::shared_lock<std::shared_mutex>) gerçekleştirilir.

- Bu örnek, std::shared_mutex sınıfının paylaşımlı bellek yönetimi senaryolarında nasıl kullanılabileceğini göstermektedir.





















































