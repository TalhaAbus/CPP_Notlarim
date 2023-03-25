- C++20'de eklendi, <semaphore> başlık dosyası, senkronizasyonu ve iş parçacığı arasındaki işbirliğini kolaylaştıran semafor nesnelerini tanımlar. Bu başlık dosyası, semaforlar aracılığıyla senkronizasyonu sağlamak için bir dizi fonksiyon ve sınıf sağlar.

- Bu başlık dosyasındaki en önemli sınıf, semafor sınıfıdır. Bu sınıf, bir iş parçacığının, bir başka iş parçacığının belirli bir noktada durmasını sağlamasına ve daha sonra devam etmesine izin veren bir senkronizasyon aracıdır. Semaforlar, sıkı bir senkronizasyon ihtiyacı olan çoklu iş parçacığı programlamasında yaygın olarak kullanılır.

- Bunun yanı sıra, bu başlık dosyası iki adet standart fonksiyon olan binary_semaphore ve counting_semaphore fonksiyonlarını da içerir. binary_semaphore fonksiyonu, yalnızca iki olası durumla ilişkili olan semaforlar için tasarlanmıştır. counting_semaphore fonksiyonu ise, belirli bir sayıda olası durumla ilişkili olan semaforlar için tasarlanmıştır.

- Örnek kullanım senaryoları şunlar olabilir:

- **Bir thread, belirli bir kaynağa aynı anda yalnızca bir iş parçacığının erişebilmesi gerektiği bir senaryoda, bu kaynağa erişimi kontrol etmek için bir semafor kullanılabilir.**
- **Bir producer-consumer senaryosunda, consumer iş parçacığı, üreticinin ürettiği verileri yalnızca veri hazır olduğunda ve consumer'ın hazır olduğunda tüketebilir. Bu durumda, producer iş parçacığı, consumer iş parçacığının semaforu beklemesi için bir semafor kullanabilir.**

- Örnek bir kullanım şu şekilde olabilir:

```CPP
#include <iostream>
#include <thread>
#include <semaphore>

using namespace std;

int main() {
    semaphore sem{0}; // 0'dan başlayan semafor nesnesi oluşturuldu

    thread t([&sem]() {
        cout << "Thread: I am waiting for the semaphore.\n";
        sem.acquire(); // semafor bekleniyor
        cout << "Thread: Acquired the semaphore. Doing some work.\n";
    });

    this_thread::sleep_for(3s); // 3 saniye bekle

    cout << "Main thread: Releasing the semaphore.\n";
    sem.release(); // semafor serbest bırakıldı

    t.join();

    return 0;
}

```
- Bu örnekte bir semaphore kullanarak iki farklı thread'in senkronize çalışmasını sağladık.

- Öncelikle semaphore sınıfından bir nesne oluşturduk. semaphore sınıfı, bir blok veya bir dizi işlemin aynı anda çalışmasını kontrol etmek için kullanılır. Bu örnekte semaphore nesnesi, başlangıçta 0 olarak ayarlandı. Bu, semaforun başlangıçta bloke edildiği anlamına gelir.

- Daha sonra, bir thread oluşturduk ve bu thread semaforu beklemeye başladı (sem.acquire()). Bu satır, semafor nesnesinin değerini kontrol eder. Eğer değer 0 ise semafor bekletilir, değer 0'dan büyükse semaforu hemen geçer.

- Ana thread, 3 saniye bekledikten sonra semaforu serbest bıraktı (sem.release()). Semaforu serbest bırakmak, semaforun değerini artırır ve bekleyen thread'in semaforu geçmesine izin verir.

- Son olarak, ana thread, oluşturulan thread'in işini tamamlaması için bekler (t.join()).

- Bu örnek, semaforların senkronize bir şekilde çalıştığını ve birden fazla thread'in bu mekanizmayı kullanarak birbirleriyle etkileşime girebileceğini göstermektedir.


# İş parçacıklarını yönetmek için farklı başlık dosyaları ve sınıfları var. Ben neden semaphore'u tercih edeyim

- Semaphore, thread ve processler arasında senkronizasyon sağlamak için kullanılan bir senkronizasyon aracıdır. Diğer thread veya processlerin bir kaynağı paylaşmasını engellemek için kullanılır. Semaphore'lar, işlemcilerin farklı sayıda thread'leri aynı anda çalıştırabileceği durumlarda özellikle faydalıdır.

- Semaphore, bir kuyruk gibi çalışır. Kaynağı kullanmak isteyen thread, semaphoredan bir izin talep eder. Eğer izin verilirse, kaynak kullanılabilir hale gelir ve semaphoreda bir adım öne kaydedilir. Kaynak kullanımı tamamlandığında, thread semaphoredan bir izin bırakır ve semaphoreda bir adım geriye kaydedilir.

- Semaphore'lar, özellikle çoklu thread programlamada kullanılan diğer senkronizasyon araçlarına alternatif olarak kullanılabilir. Mutex ve condition variable gibi diğer senkronizasyon araçlarına göre daha esnek ve özelleştirilebilir bir yapıya sahiptirler.

- Semaphore, özellikle iş parçacığı havuzları, havuz kaynakları, kuyruklar ve ağ trafiği yönetimi gibi senkronizasyon gerektiren programlama durumlarında kullanılabilir.

- Örnek kullanımlar arasında; bir dosyanın aynı anda yalnızca bir thread tarafından yazılabileceği ve birden fazla thread'in yazma isteğinin bir kuyrukta bekletildiği senaryolar yer alabilir. Semaphore kullanarak, bir thread dosyayı yazarken diğer thread'lerin ona müdahale etmesini engelleyebilirsiniz.

- Ayrıca, semaphore kullanarak bir kaynağı birden fazla thread arasında paylaşabilir ve threadlerin bu kaynağı aynı anda kullanmalarını engelleyebilirsiniz.

- Özetle, semaphore senkronizasyon aracıdır ve thread ve processler arasınd


**Aşağıdaki örnekte, bir tüketici-üretici senaryosu simüle edilmiştir. Üreticiler bir sayı üretir ve bu sayıları sınırlı boyutlu bir puf içinde depolarlar. Tüketiciler pufu okuyarak sayıları alır. Amaç, pufun tamamlandığını belirtmek için bir senkronizasyon noktası kullanmaktır. Bu örnekte, bu amaçla bir semaphore kullanılır.**

```CPP
#include <iostream>
#include <thread>
#include <semaphore>

std::counting_semaphore<10> buffer_semaphore(10);
std::counting_semaphore<0> data_semaphore(0);

int buffer[10];
int next_producer_index = 0;
int next_consumer_index = 0;

void produce() {
  int produced_value = 0;
  while (true) {
    std::this_thread::sleep_for(std::chrono::milliseconds(500));
    buffer_semaphore.acquire();  // Wait until there is space in the buffer
    buffer[next_producer_index] = produced_value;
    std::cout << "Produced " << produced_value << " at index " << next_producer_index << std::endl;
    next_producer_index = (next_producer_index + 1) % 10;
    data_semaphore.release();   // Notify consumers that there is new data available
    ++produced_value;
  }
}

void consume() {
  while (true) {
    std::this_thread::sleep_for(std::chrono::milliseconds(1000));
    data_semaphore.acquire();   // Wait until there is data available
    int consumed_value = buffer[next_consumer_index];
    std::cout << "Consumed " << consumed_value << " from index " << next_consumer_index << std::endl;
    next_consumer_index = (next_consumer_index + 1) % 10;
    buffer_semaphore.release(); // Notify producers that there is space available in the buffer
  }
}

int main() {
  std::thread producer_thread(produce);
  std::thread consumer_thread(consume);

  producer_thread.join();
  consumer_thread.join();

  return 0;
}

```

> Bu örnekte counting_semaphore sınıfından iki örnek oluşturulmuştur: buffer_semaphore ve data_semaphore. buffer_semaphore pufun doluluk durumunu, data_semaphore ise içinde veri olup olmadığını belirler. acquire() fonksiyonu, senkronizasyonu sağlamak için beklemek için kullanılırken, release() fonksiyonu senkronizasyon noktasının diğer tarafta uyandırılmasını sağlar. acquire() ve release() fonksiyonları sırasıyla semaforu kilitler ve açar. Yukarıdaki örnekte, buffer_semaphore semaforu pufun kapasitesini kontrol etmek için kullanılırken, data_semaphore semaforu içinde veri olduğunu kontrol etmek için kullanılır.










