- C++20 ile birlikte gelen <coroutine> başlık dosyası, dilde eşzamanlı programlama için koşut çalıştırma ve asenkron çalıştırma sağlayan yeni bir mekanizma olan coroutine'leri kullanmak için gerekli sınıf ve fonksiyonları içerir. Coroutine'ler, iş parçacıklarının maliyetlerine katlanmadan daha etkin eşzamanlı programlama yapmaya yardımcı olur.

- <coroutine> başlık dosyası aşağıdaki önemli sınıf ve fonksiyonları içerir:

- **std::coroutine_handle:** Coroutine'in temel kontrol nesnesidir ve coroutine'lerin çalışma zamanı durumlarıyla etkileşim kurmanızı sağlar. Özellikle, coroutine'i devam ettirmek, durdurmak ve yok etmek için kullanılır.

- **std::coroutine_traits:** Coroutine özelliklerini ve özelliklerine göre çıkarımlar yapmak için kullanılır. Bu sınıf, coroutine fonksiyonlarının döndürdüğü türlerle ilişkilendirilir.

- **std::suspend_always ve std::suspend_never:** Coroutine'lerin çalışma sürelerinde nasıl durdurulacağını ve devam ettirileceğini belirtir. suspend_always her zaman duraklamayı talep ederken, suspend_never duraklamayı asla talep etmez.

- **std::noop_coroutine_promise:** Boş coroutine vaadi oluşturmak için kullanılır.

- Coroutine'ler, genellikle asenkron işlemleri temsil etmek için kullanılır. Bir örnek olarak, asenkron bir dosya okuma işlemi şu şekilde yapılabilir:

```CPP
#include <coroutine>
#include <iostream>
#include <fstream>
#include <future>

struct AsyncReadFile {
    struct promise_type {
        std::ifstream file;
        std::string line;
        std::promise<std::string> result_promise;

        auto get_return_object() {
            return result_promise.get_future();
        }

        std::suspend_always initial_suspend() {
            return {};
        }

        std::suspend_always final_suspend() noexcept {
            return {};
        }

        void unhandled_exception() {
            std::terminate();
        }

        void return_void() {
            result_promise.set_value(std::move(line));
        }
    };

    using handle_type = std::coroutine_handle<promise_type>;
    handle_type coroutine_handle;

    explicit AsyncReadFile(handle_type h) : coroutine_handle(h) {}
    ~AsyncReadFile() {
        coroutine_handle.destroy();
    }

    void start() {
        coroutine_handle.resume();
    }
};

std::future<std::string> async_read_file(const std::string& filename) {
    co_await std::suspend_always{};
    AsyncReadFile::promise_type promise;
    promise.file.open(filename);
    std::getline(promise.file, promise.line);
    co_return;
}

int main() {
    auto result_future = async_read_file("test.txt");
    std::cout << "Dosya okunuyor...\n";
    result_future.wait();
    std::cout << "İşlem tamamlandı. İlk satır: " << result_future.get() << std::endl;
   

```

- Coroutine'ler, eşzamanlı programlama için başka bir seçenek sunar ve iş parçacığı temelli veya asenkron programlamaya göre bazı avantajlar sağlar. İşte coroutine'leri tercih etmeniz için bazı nedenler:

- **Düşük maliyetli eşzamanlılık:** Coroutine'ler, iş parçacıklarına kıyasla daha düşük maliyetli eşzamanlılık sunar. İş parçacıkları, işletim sistemi tarafından sağlanır ve her biri için özel kaynaklar (ör. bellek) tahsis edilir. Coroutine'ler ise kullanıcı düzeyinde daha hafif ve daha düşük maliyetlidir. Bu, çok sayıda eşzamanlı görevi yönetirken daha az sistem kaynağı kullanılacağı anlamına gelir.

- **Daha basit kod yapısı:** Coroutine'ler, asenkron programlama için kullanılan callback'lerden veya Promise/Future bazlı yaklaşımlardan daha doğal ve okunaklı bir kod yapısı sunar. Coroutine'lerde kod, sürekli yapılar (loops) ve hata yönetimi için daha az karmaşıktır.

- **Daha iyi performans:** Coroutine'ler, asenkron işlemler sırasında kodun doğrudan devam etmesini sağlar. Bu, daha hızlı yanıt süreleri ve daha iyi performans sunar. Özellikle, I/O veya ağ bağlantıları gibi beklemeye dayalı işlemlerde, coroutine'ler verimli bir şekilde çalışır ve sistem kaynaklarını kullanır.

- **İyileştirilmiş hata yönetimi:** Coroutine'ler, hataları daha kolay yönetmenizi sağlar. Asenkron işlemlerde, hata yönetimi daha karmaşık hale gelebilir ve callback'lerle uğraşırken hataların izlenmesi zor olabilir. Coroutine'ler ise hata yönetimini daha basit ve düzenli hale getirir.

- Birlikte çalışabilirlik:** Coroutine'ler, mevcut asenkron ve eşzamanlı programlama kütüphaneleri ile uyumlu çalışabilir. Bu, mevcut kod tabanınıza kolayca entegre edilebilir ve farklı eşzamanlılık modellerini bir arada kullanabilmenizi sağlar.

- Yukarıdaki avantajlara rağmen, coroutine'lerin her durumda en iyi seçenek olmayabileceğini unutmamanız önemlidir. Uygulamanızın gereksinimlerine bağlı olarak, iş parçacıkları, iş parçacığı havuzları, asenkron I/O veya diğer eşzamanlılık modellerini kullanmanız daha uygun olabilir. Coroutine'lerin sunduğu avantajları değerlendirerek, projeniz için en uygun eşzamanlılık modelini seçebilirsiniz.

- Coroutine'lerin kullanım senaryoları, özellikle asenkron ve eşzamanlı işlemler gerektiren durumlarda karşımıza çıkar. İşte bazı pratik senaryolar:

- **Ağ programlama:** Ağ bağlantıları, genellikle gecikmeli I/O işlemleri gerektirir. Coroutine'ler, bu tür işlemleri etkili bir şekilde yönetmenizi sağlar. Örneğin, asenkron bir sunucu, bağlantı taleplerini kabul edip, istemcilerle veri alışverişi yaparken coroutine'leri kullanabilir. Bu sayede, sunucu istemcilerin yanıtını beklerken diğer istemcilerle etkileşime devam eder ve daha yüksek performans sunar.

- **Web API çağrıları:** Web API'leri ile çalışırken, asenkron istekler yaparak ve yanıtları beklerken coroutine'leri kullanabilirsiniz. Bu, uygulamanızın yanıt sürelerini iyileştirebilir ve kullanıcı deneyimini artırabilir.

- **Veritabanı işlemleri:** Veritabanı sorguları, genellikle yüksek gecikmeli işlemlerdir. Coroutine'ler kullanarak, sorguları asenkron bir şekilde çalıştırabilir ve beklenen sonuçlar gelene kadar diğer işlemlere devam edebilirsiniz.

- **UI/UX programlama:** Grafiksel kullanıcı arayüzlerinde, asenkron etkileşimler ve arka plan işlemleri önemlidir. Coroutine'ler, kullanıcı etkileşimlerini ve arka plan işlemlerini daha hızlı ve daha verimli bir şekilde yönetmenize olanak tanır. Örneğin, bir dosyayı asenkron olarak yüklerken kullanıcıya ilerleme durumunu gösterebilirsiniz.

- **Paralel hesaplamalar:** Belirli hesaplamalar, paralel olarak çalıştırılabilecek bir dizi bağımsız görevlere bölünebilir. Coroutine'ler, bu tür hesaplamaları yönetmek için kullanılabilir ve daha hızlı sonuçlar almanıza yardımcı olabilir.

- Asenkron bir HTTP istemcisi kullanarak bir web API'sinden veri almak için coroutine'lerin nasıl kullanılacağına dair bir örnek verelim. Bu örnek, C++20 ve cppcoro kütüphanesini kullanarak gerçekleştirilebilir. Önce kütüphaneyi yüklemeniz gerekmektedir:

- GitHub: https://github.com/lewissbaker/cppcoro

- Örnek olarak, basit bir JSON web API'sinden asenkron olarak veri alalım:

```CPP
#include <cppcoro/http_request.hpp>
#include <cppcoro/sync_wait.hpp>
#include <cppcoro/task.hpp>
#include <iostream>
#include <string>

cppcoro::task<std::string> fetch_data(const std::string& url) {
    cppcoro::http_request request(url);
    co_await request.async_connect();
    co_await request.async_write_request();
    auto response = co_await request.async_read_response();
    co_return response.body();
}

int main() {
    const std::string api_url = "https://api.example.com/data";

    try {
        std::cout << "Veri alınıyor...\n";
        std::string data = cppcoro::sync_wait(fetch_data(api_url));
        std::cout << "Veri alındı:\n" << data << std::endl;
    } catch (const std::exception& e) {
        std::cerr << "Hata: " << e.what() << std::endl;
    }

    return 0;
}

```

- Bu örnek, aşağıdaki adımları gerçekleştirir:

- **fetch_data adında bir coroutine fonksiyonu tanımlar. Bu fonksiyon, bir URL alır ve bu URL'deki web API'sinden veri almayı amaçlar.**
- **cppcoro::http_request nesnesi kullanarak HTTP isteği oluşturur ve bağlantıyı asenkron olarak gerçekleştirir.**
- **İstek gönderildikten sonra, yanıtı asenkron olarak okur ve istenen veriyi döndürür.**
- **Ana fonksiyonda, cppcoro::sync_wait kullanarak coroutine fonksiyonun sonucunu bekler ve sonucu ekrana yazdırır.**
- Bu örnek, coroutine'lerin asenkron işlemleri basit ve okunaklı bir şekilde nasıl yönetebileceğini gösterir. Ayrıca, bu örnek, eşzamanlı programlamada daha düşük maliyetli ve daha verimli bir yapı sunar.







