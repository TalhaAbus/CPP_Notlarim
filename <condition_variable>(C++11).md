- condition_variable başlık dosyası, çoklu iş parçacığı uygulamaları için senkronizasyon araçları sağlayan C++11 standardı ile tanıtılan bir başlık dosyasıdır. Bu başlık dosyası, C++11'de tanıtılan "std::thread" sınıfı gibi diğer C++11 çoklu iş parçacığı araçlarıyla birlikte kullanılabilir.

- condition_variable başlık dosyası, "std::condition_variable" ve "std::condition_variable_any" sınıflarını sağlar. "std::condition_variable", C++11'de tanıtılan bir sınıftır ve bir iş parçacığının diğer iş parçacıklarıyla senkronize olmasına izin verir. "std::condition_variable_any", C++17'de tanıtılan bir sınıftır ve herhangi bir türde bir kilitleyici ile kullanılabilir.

- condition_variable başlık dosyası, C++11'den önce, çoklu iş parçacıklı programlama için POSIX thread kütüphanesi veya Windows API kullanarak senkronizasyon sağlamak için kullanılırdı. Ancak, C++11'de tanıtılan "std::thread" sınıfı ve "std::condition_variable" sınıfı, C++ dilindeki çoklu iş parçacıklı programlama için güvenli, taşınabilir bir yol sağlamıştır. Bu nedenle, <condition_variable> başlık dosyası, C++11'den önceki sürümler için önerilmemektedir.

- aşağıdaki örnek std::condition_variable kullanarak iki thread arasında bir senkronizasyon yapısını göstermektedir:

```CPP
#include <iostream>
#include <thread>
#include <mutex>
#include <condition_variable>

std::mutex m;
std::condition_variable cv;
bool ready = false;

void worker_thread()
{
    // İşlerin yapılması

    // Veriler hazır olduğunda ana thread

```


- condition_variable başlık dosyası, C++11 standartlarından itibaren çoklu iş parçacıklı programlamada senkronizasyon sağlamak için kullanılan bir sınıf olan std::condition_variable sınıfını tanımlar.

Bu sınıf, bir iş parçacığının bir şartın karşılanmasını beklemesine olanak tanır ve başka bir iş parçacığı tarafından bu şartın sağlandığını gördüğünde uyandırılır. Bu, iş parçacıklarının birbirleriyle koordinasyon halinde çalışmasını ve birbirlerinin işlerinin bitmesini beklemelerini sağlar.

Aşağıda std::condition_variable sınıfının kullanımına yönelik bir örnek verilmiştir:

```CPP
#include <iostream>
#include <thread>
#include <mutex>
#include <condition_variable>

std::mutex m;
std::condition_variable cv;
bool ready = false;

void print_number(int number) {
    std::unique_lock<std::mutex> lock(m);
    while (!ready) {
        cv.wait(lock);
    }
    std::cout << "Thread " << number << " is running." << std::endl;
}

int main() {
    std::thread t1(print_number, 1);
    std::thread t2(print_number, 2);
    std::thread t3(print_number, 3);
    
    std::this_thread::sleep_for(std::chrono::seconds(1));
    std::cout << "Ready!" << std::endl;
    {
        std::lock_guard<std::mutex> lock(m);
        ready = true;
    }
    cv.notify_all();

    t1.join();
    t2.join();
    t3.join();

    return 0;
}

```

- Bu örnekte, print_number() işlevi, herhangi bir numaralandırılmış iş parçacığı tarafından çağrılabilir. Ancak, bu iş parçacıkları eşzamanlı olarak çalıştırıldığında, sıralı olarak çalıştırılmalarını sağlamak için senkronize olmaları gerekiyor. Bu amaçla, bir std::mutex ve bir std::condition_variable kullanıyoruz.

- print_number() işlevi, std::unique_lock ile kilitlenir ve bir while döngüsü içinde ready değişkenini kontrol ederek uygun koşulda cv.wait(lock) çağrısı yaparak bekletilir. cv.notify_all() çağrısı yapılana kadar iş parçacıkları uyanmaz.

- main() işlevinde, bir saniye bekledikten sonra, ready değişkenini true olarak ayarlar ve cv.notify_all() çağrısı yaparak uyuyan tüm iş parçacıklarını uyandırır.

- Bu örnekte std::condition_variable sınıfı, iş parçacıklarının birbirleriyle koordinasyon halinde çalışmasını sağlamak için kullanılır.

# çoklu iş parçacıklı programlama tam olarak ne demek?

- Çoklu iş parçacıklı programlama, birden fazla iş parçacığı (thread) kullanarak bir programın çalıştırılmasıdır. İş parçacıkları, programın birden fazla görevi eşzamanlı olarak gerçekleştirmesine olanak tanır ve böylece programın daha hızlı ve verimli olmasını sağlar. Bu yöntem, özellikle büyük, karmaşık ve kaynak yoğunluğu yüksek programlarda sıklıkla kullanılır. Çoklu iş parçacıklı programlama, paralel programlama olarak da adlandırılabilir.

























