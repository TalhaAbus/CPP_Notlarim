- C++20 standartları ile birlikte eklenen <barrier> başlık dosyası, senkronizasyon için bir bariyer mekanizması sağlar. Bir bariyer, bir grup thread'in bir noktada toplanması ve burada senkronize bir şekilde çalışmasını sağlar.

- Bir bariyer, bir veya daha fazla thread'in bir noktada toplanması ve devam etmek için diğer thread'lerin tamamlanmasını beklemesi gerektiği senaryolarda kullanışlıdır. Örneğin, birden fazla thread ile çalışan bir işlemcinin tüm işlemlerinin tamamlanmasını beklemek için kullanılabilir.

- Bariyer, bir sayaç ve bir mutex kullanarak çalışır. Bir thread sayaç değerini arttırır ve diğer thread'ler bu sayacı kontrol ederek işlemlerinin tamamlanıp tamamlanmadığını kontrol ederler. Mutex, sayacın eş zamanlı olarak değiştirilmesine karşı koruma sağlar.

- Bariyer, constructorda belirtilen sayıda thread tarafından birleştirilinceye kadar bekler. Tüm thread'ler bariyere ulaştığında devam etmek için bekleyebilir veya bir sonraki bariyer noktasına kadar bekleyebilirler.

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



































