- mutex başlık dosyası, çoklu iş parçacığı programlamada eşzamanlılığı sağlamak için kullanılan kilitleme mekanizmalarını sağlar. Mutex, bir iş parçacığının başka bir iş parçacığı tarafından kullanılmaması gereken bir kaynağa eriştiği yerlerde kullanılır.

- Bu başlık dosyasında iki tür mutex bulunur: std::mutex ve std::recursive_mutex. std::mutex, sıradan bir mutex'tir ve bir kez kilitlendiğinde, başka bir iş parçacığı tarafından kullanılamaz. std::recursive_mutex ise, aynı iş parçacığının birden fazla kez kilitleyebileceği bir mutex'tir. Bu, bir işlevin birden fazla iş parçacığı tarafından çağrılması durumunda yararlıdır.

- mutex başlık dosyası ayrıca std::lock_guard ve std::unique_lock adlı iki sınıf da sağlar. Bu sınıflar, otomatik olarak bir mutex'i kilitleyip serbest bırakarak, kodun daha güvenli hale getirilmesine yardımcı olur.

- mutex başlık dosyası, C++11'in eşzamanlılık özelliklerinden biridir ve çoklu iş parçacıklı programlama sırasında önemli bir role sahiptir.
  
 
- Aşağıdaki örnekte std::mutex kullanarak iki iş parçacığı arasında bir count değişkeni üzerinde senkronizasyon yapılıyor. Birinci iş parçacığı, değişkenin ilk değerini 0'dan 1000'e kadar artırırken, diğer iş parçacığı değişkenin değerini 10 kere yazdırıyor. İki iş parçacığı arasında count değişkenine aynı anda erişim olmadığından, programın sonuçları doğru olacaktır.
-  

```CPP
#include <iostream>
#include <thread>
#include <mutex>

std::mutex mtx;

void incrementCounter(int &count, int numIterations)
{
    for (int i = 0; i < numIterations; ++i)
    {
        mtx.lock();
        ++count;
        mtx.unlock();
    }
}

void printCounter(int &count)
{
    for (int i = 0; i < 10; ++i)
    {
        mtx.lock();
        std::cout << "Counter value: " << count << std::endl;
        mtx.unlock();
    }
}

int main()
{
    int count = 0;
    const int numIterations = 1000;

    std::thread t1(incrementCounter, std::ref(count), numIterations);
    std::thread t2(printCounter, std::ref(count));

    t1.join();
    t2.join();

    return 0;
}

```
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
