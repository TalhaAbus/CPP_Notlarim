- C++20 standartları ile birlikte eklenen barrier başlık dosyası, senkronizasyon için bir bariyer mekanizması sağlar. Bir bariyer, bir grup thread'in bir noktada toplanması ve burada senkronize bir şekilde çalışmasını sağlar.

- Bir bariyer, bir veya daha fazla thread'in bir noktada toplanması ve devam etmek için diğer thread'lerin tamamlanmasını beklemesi gerektiği senaryolarda kullanışlıdır. Örneğin, birden fazla thread ile çalışan bir işlemcinin tüm işlemlerinin tamamlanmasını beklemek için kullanılabilir.

- Bariyer, bir sayaç ve bir mutex kullanarak çalışır. Bir thread sayaç değerini arttırır ve diğer thread'ler bu sayacı kontrol ederek işlemlerinin tamamlanıp tamamlanmadığını kontrol ederler. Mutex, sayacın eş zamanlı olarak değiştirilmesine karşı koruma sağlar.

- Bariyer, constructorda belirtilen sayıda thread tarafından birleştirilinceye kadar bekler. Tüm thread'ler bariyere ulaştığında devam etmek için bekleyebilir veya bir sonraki bariyer noktasına kadar bekleyebilirler.

**Ornek:**
```CPP
#include <barrier>
#include <iostream>
#include <string>
#include <thread>
#include <vector>
 
int main()
{
    const auto workers = { "Anil", "Busara", "Carl" };
 
    auto on_completion = []() noexcept
    {
        // locking not needed here
        static auto phase = "... done\n" "Cleaning up...\n";
        std::cout << phase;
        phase = "... done\n";
    };
 
    std::barrier sync_point(std::ssize(workers), on_completion);
 
    auto work = [&](std::string name)
    {
        std::string product = "  " + name + " worked\n";
        std::cout << product;  // ok, op<< call is atomic
        sync_point.arrive_and_wait();
 
        product = "  " + name + " cleaned\n";
        std::cout << product;
        sync_point.arrive_and_wait();
    };
 
    std::cout << "Starting...\n";
    std::vector<std::jthread> threads;
    threads.reserve(std::size(workers));
    for (auto const& worker : workers)
        threads.emplace_back(work, worker);
}
```

> Bu kod, std::barrier kullanarak senkronize edilmiş bir çalışma grubunu temsil ediyor. Kodda önce bir std::barrier nesnesi oluşturuluyor ve çalışan sayısı olarak workers listesinin boyutu ayarlanıyor. sync_point.arrive_and_wait() çağrıları, her bir çalışanın ilk önce işlerini yapmasını beklemesi için kullanılır. Bu işlem tamamlandıktan sonra, sync_point.arrive_and_wait() çağrıları tekrar çağrılır ve bu sefer temizlik yapmalarını bekler. on_completion() lambda ifadesi, temizliği tamamladıktan sonra çalışanlardan herhangi biri tarafından çağrılır ve "Cleaning up ..." mesajını yazdırır. Son olarak, her bir çalışanın işini yaptığı bir std::jthread oluşturulur ve çalıştırılır. Her bir çalışanın adı ve ne yaptığı, çalışanın oluşturulduğu std::jthread içinde belirtilir.




### arrive()

- barrier::arrive() fonksiyonu, bekleyen tüm iş parçalarının tamamlandığını işaret eder. Bu fonksiyon, sınıftaki öğeleri günceller ve öğelerdeki sayacı azaltır. Sayacın sıfıra düşmesiyle birlikte, barrier nesnesindeki tüm iş parçaları tamamlandı ve devam edebilirler. Bu nedenle, bir dizi iş parçasını senkronize etmek için kullanışlı bir araçtır.

```CPP
#include <iostream>
#include <thread>
#include <barrier>

const int num_threads = 3;
const int num_iterations = 3;

void worker(int id, std::barrier<>& b) {
    for (int i = 0; i < num_iterations; ++i) {
        std::cout << "Thread " << id << " is waiting" << std::endl;
        b.arrive_and_wait(); // Barrier
        std::cout << "Thread " << id << " resumed" << std::endl;
    }
}

int main() {
    std::barrier<> b(num_threads);
    std::thread t[num_threads];

    for (int i = 0; i < num_threads; ++i) {
        t[i] = std::thread(worker, i, std::ref(b));
    }

    for (int i = 0; i < num_threads; ++i) {
        t[i].join();
    }

    return 0;
}

```
> Yukarıdaki kod, 3 iş parçacığı oluşturur ve her biri 3 kez bir bariyerde bekler ve devam eder. İş parçacıkları, std::barrier sınıfı kullanılarak senkronize edilir. Bariyer, arrive_and_wait() yöntemiyle geçilir. Tüm iş parçacıkları geçince, arrive_and_wait() işlemi tamamlanır ve iş parçacıkları devam eder.























- Aşağıda bir örnek verilmiştir:

```CPP
#include <iostream>
#include <thread>
#include <barrier>

void func(std::barrier& b, int id)
{
    std::cout << "Thread " << id << " is starting." << std::endl;
    b.arrive_and_wait(); // tüm thread'lerin buraya ulaşması bekleniyor
    std::cout << "Thread " << id << " is ending." << std::endl;
}

int main()
{
    constexpr int num_threads = 4;
    std::barrier b{ num_threads }; // 4 thread'li bir bariyer oluşturuldu

    std::thread t[num_threads]; // thread'ler oluşturuldu

    for (int i = 0; i < num_threads; ++i) {
        t[i] = std::thread{ func, std::ref(b), i }; // thread'lerin fonksiyonu başlatması için çağrıldı
    }

    for (auto& th : t) {
        th.join(); // thread'lerin sonlanması bekleniyor
    }

    return 0;
}

```
> Bu örnekte, 4 thread oluşturulur ve her biri func adlı bir fonksiyonu çağırır. func fonksiyonu, bir std::barrier nesnesi ve bir id değeri alır. func fonksiyonu, thread'in başlangıcını ve bitişini yazdırır ve arrive_and_wait yöntemi ile bariyer noktasına ulaşır. Tüm thread'ler bariyer noktasına ulaşana kadar beklerler ve sonra işlemlerine devam ederler.

# thread ne demek?

- "Thread" kelimesi, bir bilgisayar programındaki işlemler için kullanılan bir terimdir. Bir programda birden fazla thread varsa, bu farklı işlemler aynı anda çalışabilir ve program performansı artabilir. Bu durum "çoklu iş parçacığı programlama" olarak adlandırılır.

```CPP
#include <iostream>
#include <thread>
#include <vector>
#include <numeric>
#include <algorithm>
#include <random>
#include <chrono>
#include <barrier>

int main()
{
    const int N = 10'000'000;
    const int num_threads = std::thread::hardware_concurrency();
    std::vector<int> vec(N);
    
    // Rastgele sayı üretmek için kullanılacak nesne
    std::mt19937 gen(std::chrono::system_clock::now().time_since_epoch().count());
    std::uniform_int_distribution<> dis(1, 10);
    
    // Vektörün her elemanını rastgele sayılarla doldur
    std::generate(vec.begin(), vec.end(), [&] { return dis(gen); });
    
    // Thread'lere dağıtılacak iş parçacıkları
    auto worker = [&](int tid, std::barrier& b)
    {
        int chunk_size = N / num_threads;
        int start = tid * chunk_size;
        int end = start + chunk_size;
        std::partial_sum(vec.begin() + start, vec.begin() + end, vec.begin() + start);
        b.arrive_and_wait();
    };
    
    // Tüm thread'lerin senkronize olması için kullanılacak barier nesnesi
    std::barrier b(num_threads);
    
    // Thread'leri başlat
    std::vector<std::thread> threads(num_threads);
    for (int i = 0; i < num_threads; ++i)
    {
        threads[i] = std::thread(worker, i, std::ref(b));
    }
    
    // Thread'lerin tamamlanmasını bekle
    for (auto& t : threads)
    {
        t.join();
    }
    
    // Sonucu yazdır
    std::cout << "Partial sums: ";
    std::copy(vec.begin(), vec.begin() + 10, std::ostream_iterator<int>(std::cout, " "));
    std::cout << std::endl;
    
    return 0;
}

```
> Bu örnekte, std::barrier kullanarak vektörün parçalı toplamlarını hesaplamak için birden fazla thread kullanıyoruz. worker fonksiyonu, vektörün belirli bir bölümündeki elemanların parçalı toplamını hesaplayarak std::barrier nesnesini kullanarak diğer thread'lerle senkronize oluyor. Tüm thread'ler işlerini tamamladığında, vektörün tamamının parçalı toplamını hesaplamış oluyoruz.



































