- std::atomic, C++11'de tanıtılan bir sınıftır ve atomic işlemler gerçekleştirmek için kullanılır. Atomic işlemler, çoklu thread'ler tarafından aynı anda erişilen bellek konumlarının okunması ve yazılması işlemlerini güvenli bir şekilde gerçekleştirir.

- std::atomic, bir değişkenin değerini okuma, yazma ve işleme yöntemleri sağlar. Bu yöntemler, bir değişkenin bir iş parçacığı tarafından okunurken diğer iş parçacıkları tarafından yazılması veya tam tersi durumlarında oluşabilecek hataları önler.

- std::atomic sınıfı, aynı zamanda "memory fence" denilen işlemci düzeyindeki optimizasyonları da destekler. Bu nedenle, atomic işlemler, multi-threading uygulamalarının güvenliği açısından önemlidir.

# Functions
- **atomic_is_lock_free**
> bir std::atomic nesnesinin kilitleme olmadan atomik olarak işlenebilir olup olmadığını kontrol eder. 
- **atomic_store**
- **atomic_store_explicit**
> bir std::atomic nesnesinin değerini atamak için kullanılır. Bu işlev, varsayılan olarak güçlü atomik işlem kullanır. Bu, işlemin tüm diğer işlemlere karşı atomik olduğu anlamına gelir.
- **atomic_load**
- **atomic_load_explicit**
> bir std::atomic nesnesinin değerini okumak için kullanılır. Bu işlev, varsayılan olarak güçlü atomik işlem kullanır. Bu, işlemin tüm diğer işlemlere karşı atomik olduğu anlamına gelir.
- **atomic_exchange**
- **atomic_exchange_explicit**
> 
- **atomic_compare_exchange_weak**
- **atomic_compare_exchange_weak_explicit**
> 
- **atomic_compare_exchange_strong**
- **atomic_compare_exchange_strong_explicit**
> 
- **atomic_fetch_add**
- **atomic_fetch_add_explicit**
> 
- **atomic_fetch_sub**
- **atomic_fetch_sub_explicit**
> 
- **atomic_fetch_and**
- **atomic_fetch_and_explicit**
> 
- **atomic_fetch_or**
- **atomic_fetch_or_explicit**
> 
- **atomic_fetch_xor**
- **atomic_fetch_xor_explicit**
> 
- **atomic_wait**
- **atomic_wait_explicit**
> 
- **atomic_notify_one**
- **atomic_notify_all**
> 
- **atomic_flag_test**
- **atomic_flag_test_explicit**
> 
- **atomic_flag_test_and_set**
- **atomic_flag_test_and_set_explicit**
> 
- **atomic_flag_clear**
- **atomic_flag_clear_explicit**
> 
- **atomic_flag_wait**
- **atomic_flag_wait_explicit**
> 
- **atomic_flag_notify_one**
- **atomic_flag_notify_all**
> 
- **atomic_init**
> 
- **kill_dependency**
> 
- **atomic_thread_fence**
> 
- **atomic_signal_fence**
> 

# Macros
- **ATOMIC_VAR_INIT**
- **ATOMIC_FLAG_INIT**

# FONKSİYONLAR

### atomic_is_lock_free()

- atomic_is_lock_free() işlevi, bir std::atomic nesnesinin kilitleme olmadan atomik olarak işlenebilir olup olmadığını kontrol eder. Bu işlev, ilgili türün kilitleme olmadan atomik olarak işlenebilir olup olmadığını belirleyen bir değer döndürür.

- Aşağıda bir örnek kullanım verilmiştir:


```CPP
#include <iostream>
#include <atomic>

int main() {
    std::atomic<int> a(0);

    // "a" nesnesinin kilitleme olmadan atomik olarak işlenebilir olup olmadığını kontrol etme
    if (a.is_lock_free()) {
        std::cout << "Atomic integer is lock-free\n";
    } else {
        std::cout << "Atomic integer is not lock-free\n";
    }

    return 0;
}

```
> Bu örnekte, std::atomic türünden bir a nesnesi oluşturulur ve is_lock_free() işlevi kullanılarak a nesnesinin kilitleme olmadan atomik olarak işlenebilir olup olmadığı kontrol edilir. Sonuç olarak, ekrana "Atomic integer is lock-free" veya "Atomic integer is not lock-free" yazılır.

### atomic_store()

- atomic_store() işlevi, bir std::atomic nesnesinin değerini atamak için kullanılır. Bu işlev, varsayılan olarak güçlü atomik işlem kullanır. Bu, işlemin tüm diğer işlemlere karşı atomik olduğu anlamına gelir.

- Aşağıda bir örnek kullanım verilmiştir:

```CPP
#include <iostream>
#include <atomic>

int main() {
    std::atomic<int> a(0);

    // Güçlü atomik işlem kullanarak "a" nesnesine değer atama
    std::atomic_store(&a, 42);

    std::cout << "Value of atomic integer is " << a << '\n';

    return 0;
}

```
> Bu örnekte, std::atomic türünden bir a nesnesi oluşturulur ve atomic_store() işlevi kullanılarak a nesnesine değer atanır. Sonuç olarak, a nesnesinin değeri 42 olur ve bu değer ekrana yazdırılır.

### atomic_load()

- atomic_load() işlevi, bir std::atomic nesnesinin değerini okumak için kullanılır. Bu işlev, varsayılan olarak güçlü atomik işlem kullanır. Bu, işlemin tüm diğer işlemlere karşı atomik olduğu anlamına gelir.

- Aşağıda bir örnek kullanım verilmiştir:

```CPP
#include <iostream>
#include <atomic>

int main() {
    std::atomic<int> a(42);

    // Güçlü atomik işlem kullanarak "a" nesnesinin değerini okuma
    int value = std::atomic_load(&a);

    std::cout << "Value of atomic integer is " << value << '\n';

    return 0;
}

```
> Bu örnekte, std::atomic türünden bir a nesnesi oluşturulur ve değeri 42 olarak ayarlanır. Daha sonra, atomic_load() işlevi kullanılarak a nesnesinin değeri okunur ve value değişkenine atanır. Sonuç olarak, value değişkeninin değeri 42 olur ve bu değer ekrana yazdırılır.

### atomic_exchange()

- atomic_exchange() işlevi, bir std::atomic nesnesinin değerini başka bir değerle değiştirmek için kullanılır. Bu işlev, varsayılan olarak güçlü atomik işlem kullanır. Bu, işlemin tüm diğer işlemlere karşı atomik olduğu anlamına gelir.

- Aşağıda bir örnek kullanım verilmiştir:

```CPP
#include <iostream>
#include <atomic>

int main() {
    std::atomic<int> a(42);

    // Güçlü atomik işlem kullanarak "a" nesnesinin değerini 13 ile değiştirme
    int old_value = std::atomic_exchange(&a, 13);

    std::cout << "Old value of atomic integer was " << old_value << '\n';
    std::cout << "New value of atomic integer is " << a << '\n';

    return 0;
}

```
> Bu örnekte, std::atomic türünden bir a nesnesi oluşturulur ve değeri 42 olarak ayarlanır. Daha sonra, atomic_exchange() işlevi kullanılarak a nesnesinin değeri 13 ile değiştirilir ve eski değeri old_value değişkenine atanır. Sonuç olarak, old_value değişkeninin değeri 42 olur (eski değer) ve a nesnesinin yeni değeri 13 olur. Bu değerler ekrana yazdırılır.

### atomic_compare_exchange_weak()

- atomic_compare_exchange_weak() işlevi, bir std::atomic nesnesinin değerini belirli bir değerle değiştirmek için kullanılır, ancak bu işlem yalnızca belirli bir koşulu karşıladığında gerçekleştirilir. Bu işlev, zayıf atomik işlem kullanır, yani işlem başarısız olursa tekrar deneyebilir. Bu nedenle, bu işlev, bir döngü içinde kullanılarak kullanıcı tarafından tekrar denenebilir.

- Aşağıda bir örnek kullanım verilmiştir:
```CPP
#include <iostream>
#include <atomic>

int main() {
    std::atomic<int> a(42);

    int expected_value = 42;
    int new_value = 13;

    // Eğer a nesnesi beklenen değere eşit ise, değerini 13 ile değiştir
    bool result = std::atomic_compare_exchange_weak(&a, &expected_value, new_value);

    if (result) {
        std::cout << "Value of atomic integer was " << expected_value << " and is now " << new_value << '\n';
    } else {
        std::cout << "Value of atomic integer was not " << expected_value << ", so it was not changed\n";
    }

    return 0;
}

```
> Bu örnekte, std::atomic türünden bir a nesnesi oluşturulur ve değeri 42 olarak ayarlanır. Daha sonra, atomic_compare_exchange_weak() işlevi kullanılarak, a nesnesinin değeri belirli bir koşulu karşılaması durumunda 13 ile değiştirilir. Bu koşul, expected_value değişkeninde saklanır. expected_value değişkeni, a nesnesinin değeri ile aynı olması gereken 42 değeriyle başlatılır. Eğer a nesnesinin değeri beklenen değere eşitse, işlem başarılı olur ve new_value değişkeninde saklanan 13 ile a nesnesinin değeri değiştirilir. Eğer a nesnesinin değeri beklenen değere eşit değilse, işlem başarısız olur ve a nesnesinin değeri değiştirilmez. Sonuç olarak, ekrana expected_value değişkeninin değeri olan 42 yazılır, çünkü a nesnesinin başlangıç değeri bu değere eşit.

### 

- atomic_compare_exchange_strong() işlevi, bir std::atomic nesnesinin değerini belirli bir değerle değiştirmek için kullanılır, ancak bu işlem yalnızca belirli bir koşulu karşıladığında gerçekleştirilir. Bu işlev, güçlü atomik işlem kullanır, yani işlem başarısız olursa tekrar deneme yapılmaz.

- Aşağıda bir örnek kullanım verilmiştir:

```CPP
#include <iostream>
#include <atomic>

int main() {
    std::atomic<int> a(42);

    int expected_value = 42;
    int new_value = 13;

    // Eğer a nesnesi beklenen değere eşit ise, değerini 13 ile değiştir
    bool result = std::atomic_compare_exchange_strong(&a, &expected_value, new_value);

    if (result) {
        std::cout << "Value of atomic integer was " << expected_value << " and is now " << new_value << '\n';
    } else {
        std::cout << "Value of atomic integer was not " << expected_value << ", so it was not changed\n";
    }

    return 0;
}

```
> Bu örnekte, std::atomic türünden bir a nesnesi oluşturulur ve değeri 42 olarak ayarlanır. Daha sonra, atomic_compare_exchange_strong() işlevi kullanılarak, a nesnesinin değeri belirli bir koşulu karşılaması durumunda 13 ile değiştirilir. Bu koşul, expected_value değişkeninde saklanır. expected_value değişkeni, a nesnesinin değeri ile aynı olması gereken 42 değeriyle başlatılır. Eğer a nesnesinin değeri beklenen değere eşitse, işlem başarılı olur ve new_value değişkeninde saklanan 13 ile a nesnesinin değeri değiştirilir. Eğer a nesnesinin değeri beklenen değere eşit değilse, işlem başarısız olur ve a nesnesinin değeri değiştirilmez. Ancak bu durumda, işlem başarısız olduğunda expected_value değişkeni, a nesnesinin güncel değeri ile güncellenir. Bu nedenle, bir sonraki atomic_compare_exchange_strong() işlevi çağrısında, expected_value değişkeninin güncellenmiş değeri kullanılacaktır. Sonuç olarak, ekrana expected_value değişkeninin güncellenmiş değeri olan 13 yazılır, çünkü bir önceki atomic_compare_exchange_strong() işlevi çağrısında a nesnesinin değeri 42'den 13'e değiştirilmiştir.

### atomic_fetch_add()

- atomic_fetch_add() işlevi, bir std::atomic nesnesinin değerini belirli bir tamsayı değeriyle artırmak için kullanılır ve artırma işlemi atomik olarak gerçekleştirilir. Bu işlev, aynı anda yalnızca bir iş parçacığı tarafından çağrılabilir ve bu nedenle birden çok iş parçacığı arasında senkronizasyon gerektirmez.

- Aşağıda bir örnek kullanım verilmiştir:

```CPP
#include <iostream>
#include <atomic>

int main() {
    std::atomic<int> a(42);

    std::cout << "Value of atomic integer was " << a << '\n';

    // a değerini 5 ile artır ve son değeri ekrana yazdır
    int result = std::atomic_fetch_add(&a, 5);

    std::cout << "Value of atomic integer is now " << a << '\n';
    std::cout << "Result of fetch_add operation was " << result << '\n';

    return 0;
}

```
> Bu örnekte, std::atomic türünden bir a nesnesi oluşturulur ve değeri 42 olarak ayarlanır. Daha sonra, atomic_fetch_add() işlevi kullanılarak, a nesnesinin değeri belirli bir tamsayı değeriyle artırılır ve artırma işlemi atomik olarak gerçekleştirilir. Bu işlem sonucunda, artırma işleminden önce a nesnesinin değeri olan 42 döndürülür ve result değişkeninde saklanır. Sonuç olarak, ekrana a nesnesinin güncel değeri olan 47 ve result değişkeninde saklanan 42 yazılır.

### atomic_fetch_sub()

- atomic_fetch_sub() işlevi, bir std::atomic nesnesinin değerini belirli bir tamsayı değeriyle azaltmak için kullanılır ve azaltma işlemi atomik olarak gerçekleştirilir. Bu işlev, aynı anda yalnızca bir iş parçacığı tarafından çağrılabilir ve bu nedenle birden çok iş parçacığı arasında senkronizasyon gerektirmez.

- Aşağıda bir örnek kullanım verilmiştir:

```CPP
#include <iostream>
#include <atomic>

int main() {
    std::atomic<int> a(42);

    std::cout << "Value of atomic integer was " << a << '\n';

    // a değerini 5 ile azalt ve son değeri ekrana yazdır
    int result = std::atomic_fetch_sub(&a, 5);

    std::cout << "Value of atomic integer is now " << a << '\n';
    std::cout << "Result of fetch_sub operation was " << result << '\n';

    return 0;
}

```

> Bu örnekte, std::atomic türünden bir a nesnesi oluşturulur ve değeri 42 olarak ayarlanır. Daha sonra, atomic_fetch_sub() işlevi kullanılarak, a nesnesinin değeri belirli bir tamsayı değeriyle azaltılır ve azaltma işlemi atomik olarak gerçekleştirilir. Bu işlem sonucunda, azaltma işleminden önce a nesnesinin değeri olan 42 döndürülür ve result değişkeninde saklanır. Sonuç olarak, ekrana a nesnesinin güncel değeri olan 37 ve result değişkeninde saklanan 42 yazılır.

### atomic_fetch_and()

- atomic_fetch_and() işlevi, bir std::atomic nesnesinin değerine belirli bir tamsayı değerini bit düzeyinde "ve" işlemi yaparak uygulamak için kullanılır. Bu işlem atomik olarak gerçekleştirilir ve birden çok iş parçacığı arasında senkronizasyon gerektirmez.

- Aşağıda bir örnek kullanım verilmiştir:

```CPP
#include <iostream>
#include <atomic>

int main() {
    std::atomic<int> a(42);

    std::cout << "Value of atomic integer was " << a << '\n';

    // a değerini 0b0101 ile bit düzeyinde "ve" işlemi yaparak uygula ve sonucu ekrana yazdır
    int result = std::atomic_fetch_and(&a, 0b0101);

    std::cout << "Value of atomic integer is now " << a << '\n';
    std::cout << "Result of fetch_and operation was " << result << '\n';

    return 0;
}

```
> Bu örnekte, std::atomic türünden bir a nesnesi oluşturulur ve değeri 42 olarak ayarlanır. Daha sonra, atomic_fetch_and() işlevi kullanılarak, a nesnesinin değerine belirli bir tamsayı değeri bit düzeyinde "ve" işlemi yapılır ve sonuç atomik olarak geri döndürülür. Bu işlem sonucunda, bit düzeyinde "ve" işleminden önce a nesnesinin değeri olan 42 döndürülür ve result değişkeninde saklanır. Sonuç olarak, ekrana a nesnesinin güncel değeri olan 40 ve result değişkeninde saklanan 42 yazılır.


### atomic_fetch_or()

- atomic_fetch_or() işlevi, bir std::atomic nesnesinin değerine belirli bir tamsayı değerini bit düzeyinde "veya" işlemi yaparak uygulamak için kullanılır. Bu işlem atomik olarak gerçekleştirilir ve birden çok iş parçacığı arasında senkronizasyon gerektirmez.

- Aşağıda bir örnek kullanım verilmiştir:
```CPP
#include <iostream>
#include <atomic>

int main() {
    std::atomic<int> a(42);

    std::cout << "Value of atomic integer was " << a << '\n';

    // a değerini 0b1100 ile bit düzeyinde "veya" işlemi yaparak uygula ve sonucu ekrana yazdır
    int result = std::atomic_fetch_or(&a, 0b1100);

    std::cout << "Value of atomic integer is now " << a << '\n';
    std::cout << "Result of fetch_or operation was " << result << '\n';

    return 0;
}

```

> Bu örnekte, std::atomic türünden bir a nesnesi oluşturulur ve değeri 42 olarak ayarlanır. Daha sonra, atomic_fetch_or() işlevi kullanılarak, a nesnesinin değerine belirli bir tamsayı değeri bit düzeyinde "veya" işlemi yapılır ve sonuç atomik olarak geri döndürülür. Bu işlem sonucunda, bit düzeyinde "veya" işleminden önce a nesnesinin değeri olan 42 döndürülür ve result değişkeninde saklanır. Sonuç olarak, ekrana a nesnesinin güncel değeri olan 46 ve result değişkeninde saklanan 42 yazılır.

### atomic_fetch_xor()

- atomic_fetch_xor() işlevi, bir std::atomic nesnesinin değerine belirli bir tamsayı değerini bit düzeyinde "XOR" işlemi yaparak uygulamak için kullanılır. Bu işlem atomik olarak gerçekleştirilir ve birden çok iş parçacığı arasında senkronizasyon gerektirmez.

- Aşağıda bir örnek kullanım verilmiştir:

```CPP
#include <iostream>
#include <atomic>

int main() {
    std::atomic<int> a(42);

    std::cout << "Value of atomic integer was " << a << '\n';

    // a değerini 0b1010 ile bit düzeyinde "XOR" işlemi yaparak uygula ve sonucu ekrana yazdır
    int result = std::atomic_fetch_xor(&a, 0b1010);

    std::cout << "Value of atomic integer is now " << a << '\n';
    std::cout << "Result of fetch_xor operation was " << result << '\n';

    return 0;
}

```
> Bu örnekte, std::atomic türünden bir a nesnesi oluşturulur ve değeri 42 olarak ayarlanır. Daha sonra, atomic_fetch_xor() işlevi kullanılarak, a nesnesinin değerine belirli bir tamsayı değeri bit düzeyinde "XOR" işlemi yapılır ve sonuç atomik olarak geri döndürülür. Bu işlem sonucunda, bit düzeyinde "XOR" işleminden önce a nesnesinin değeri olan 42 döndürülür ve result değişkeninde saklanır. Sonuç olarak, ekrana a nesnesinin güncel değeri olan 36 ve result değişkeninde saklanan 42 yazılır.

### atomic_wait()

- atomic_wait() işlevi, bir std::atomic nesnesinin değerinin belirli bir değere eşit olmasını beklemek için kullanılır. Bu işlev, belirtilen std::memory_order parametresi tarafından belirtilen hafıza düzenlemesi sırasına göre atomik bir bekleme işlemi gerçekleştirir.

- Aşağıda bir örnek kullanım verilmiştir:

```CPP
#include <iostream>
#include <atomic>
#include <thread>
#include <chrono>

int main() {
    std::atomic<int> a(0);

    std::thread t([&]() {
        std::this_thread::sleep_for(std::chrono::seconds(2));
        a.store(42, std::memory_order_release);
    });

    a.wait(42, std::memory_order_acquire);

    std::cout << "Value of atomic integer is now " << a << '\n';

    t.join();

    return 0;
}

```
- Bu örnekte, bir std::atomic türünden bir a nesnesi oluşturulur ve değeri varsayılan olarak 0 olarak ayarlanır. Daha sonra, başka bir iş parçacığı oluşturulur ve 2 saniye bekledikten sonra, a nesnesinin değeri 42 olarak ayarlanır. Ana iş parçacığı, a.wait() işlevini kullanarak a nesnesinin değerinin 42 olmasını bekler. wait() işlevi, belirtilen hafıza düzenlemesi sırasına (std::memory_order_acquire) göre atomik olarak bekler. Sonuç olarak, a nesnesinin değeri 42 olarak güncellenir ve ana iş parçacığı bu değeri ekrana yazdırır.

- atomic_wait() işlevi, bir zaman aşımı belirlemek için de kullanılabilir. Bu durumda, işlev bir std::cv_status::timeout değeri döndürür.

```CPP
#include <iostream>
#include <atomic>
#include <thread>
#include <chrono>

int main() {
    std::atomic<int> a(0);

    std::thread t([&]() {
        std::this_thread::sleep_for(std::chrono::seconds(2));
        a.store(42, std::memory_order_release);
    });

    auto status = a.wait(42, std::chrono::seconds(1), std::memory_order_acquire);

    if (status == std::cv_status::timeout) {
        std::cout << "Timed out waiting for atomic integer to become 42\n";
    } else {
        std::cout << "Value of atomic integer is now " << a << '\n';
    }

    t.join();

    return 0;
}

```
> Yukarıdaki kodda, bir std::atomic int  nesnesi a oluşturulur ve başlangıçta 0'a ayarlanır. Ardından, bir başka thread oluşturulur ve 2 saniye boyunca uyutulur. Uyanınca, a nesnesinin değeri 42 olarak ayarlanır. Ana thread, a nesnesinin 42 değerine kadar değiştirilmesini bekler ve bir saniyeden fazla sürerse, zaman aşımına uğrar ve bir mesaj yazdırır. Değer değiştirildiyse, yeni değeri yazdırır.

- Bu örnek, std::atomic_wait() işlevinin kullanımını basit bir senaryoda göstermektedir. Ancak bu işlevin gerçek dünya senaryolarında nasıl kullanılacağına bağlı olarak farklı şekillerde kullanılabilir.

### atomic_notify_one

- std::atomic_notify_one(), C++11'de tanıtılan bir std::condition_variable_any nesnesini bildiren bir işlevdir. Bu işlev, bir veya daha fazla bekleyen thread'in uyandırılmasına neden olur.

- std::atomic_notify_one() işlevi, bir std::condition_variable_any nesnesi tarafından bekleyen herhangi bir thread'i uyandırmak için kullanılır. Bu işlev çağrıldığında, uyandırılacak tek bir thread seçilir ve uyandırılır. Ancak, bu işlevin hangi thread'i uyandıracağı belirsizdir.

- Aşağıdaki örnek, std::atomic_notify_one() işlevinin kullanımını göstermektedir:

```CPP
#include <iostream>
#include <atomic>
#include <thread>
#include <condition_variable>

std::condition_variable cv;
std::mutex m;
std::atomic<bool> ready(false);

void worker_thread() {
    std::this_thread::sleep_for(std::chrono::seconds(1));
    {
        std::lock_guard<std::mutex> lock(m);
        ready = true;
    }
    cv.notify_one();
}

int main() {
    std::thread worker(worker_thread);

    {
        std::unique_lock<std::mutex> lock(m);
        cv.wait(lock, [] { return ready; });
    }

    std::cout << "Worker thread ready\n";
    worker.join();

    return 0;
}

```
> Bu örnekte, bir std::atomic bool  nesnesi olan ready, başlangıçta false olarak ayarlanır ve bir thread tarafından true olarak ayarlanır. Ana thread, std::condition_variable_any nesnesi olan cv üzerinde bekler ve ready nesnesi true olarak ayarlandığında, cv.notify_one() işlevini çağırarak bekleyen thread'i uyandırır. Worker thread kendini beklemeye aldığı için bir saniye beklenir ve ardından ready değeri true olarak ayarlanır ve cv.notify_one() işlevi çağrılır. Bu işlev çağrıldığında, ana thread'in cv.wait() işlevi uyanır ve "Worker thread ready" yazdırılır.

- Bu örnek, std::atomic_notify_one() işlevinin, bir veya daha fazla bekleyen thread'i uyandırmak için nasıl kullanılabileceğini göstermektedir.

### atomic_notify_all()

- std::atomic_notify_all() fonksiyonu, belirtilen std::condition_variable nesnesine bağlı olan tüm bekleme noktalarını uyandırır. Yani, bu fonksiyon çağrıldığında bekleyen tüm iş parçacıkları uyandırılır ve tekrar çalışmaya başlar.

- Bu fonksiyon, std::atomic_notify_one() fonksiyonu gibi, bekleyen iş parçacıklarını uyandırmak için kullanılır, ancak std::atomic_notify_all() fonksiyonu, tüm iş parçacıklarını uyandırırken, std::atomic_notify_one() fonksiyonu sadece bir iş parçacığını uyandırır. Bu nedenle, std::atomic_notify_all() fonksiyonu daha geniş bir senkronizasyon işlemi için kullanılabilirken, std::atomic_notify_one() fonksiyonu daha küçük ve belirli bir senkronizasyon işlemi için kullanılabilir.

### atomic_flag_test()

- std::atomic_flag_test() fonksiyonu, belirtilen std::atomic_flag nesnesinin değerini okur ve nesnenin belirtilen değere eşit olup olmadığını kontrol eder. Bu fonksiyon, nesnenin değerinin okunmasını sağlamak için kullanılır.

- Aşağıdaki gibi kullanılabilir:

```CPP
#include <iostream>
#include <atomic>

int main() {
    std::atomic_flag flag = ATOMIC_FLAG_INIT;

    std::cout << "Initial value of flag is " << flag.test_and_set() << '\n';

    bool was_set = flag.test_and_set();
    std::cout << "Value of flag was " << was_set << " and now is " << flag.test_and_set() << '\n';

    return 0;
}

```

> Bu örnekte, std::atomic_flag_test() fonksiyonu, flag adlı bir std::atomic_flag nesnesinin değerini okur ve test_and_set() fonksiyonu tarafından değiştirilir. test_and_set() fonksiyonu, nesnenin değerini belirtilen değere ayarlar ve önceki değerini döndürür. İlk test_and_set() çağrısı, flag nesnesinin değerini true olarak ayarlar ve std::atomic_flag_test() fonksiyonu da true değerini döndürür. İkinci test_and_set() çağrısı, nesnenin değerini true olarak ayarlar ve önceki değeri olan true değerini döndürür.

### atomic_flag_test_and_set()

- std::atomic_flag_test_and_set() fonksiyonu, belirtilen std::atomic_flag nesnesinin değerini atomik olarak ayarlar ve önceki değerini döndürür. Bu fonksiyon, bir semafor olarak kullanılabilir.

- Aşağıdaki gibi kullanılabilir:

```CPP
#include <iostream>
#include <atomic>
#include <thread>
#include <chrono>

std::atomic_flag flag = ATOMIC_FLAG_INIT;

void func1() {
    while (flag.test_and_set(std::memory_order_acquire)) {
        std::this_thread::sleep_for(std::chrono::milliseconds(100));
    }

    std::cout << "func1() acquired the flag\n";
}

void func2() {
    while (flag.test_and_set(std::memory_order_acquire)) {
        std::this_thread::sleep_for(std::chrono::milliseconds(100));
    }

    std::cout << "func2() acquired the flag\n";
}

int main() {
    std::thread t1(func1);
    std::thread t2(func2);

    t1.join();
    t2.join();

    return 0;
}

```
> Bu örnekte, std::atomic_flag_test_and_set() fonksiyonu, flag adlı bir std::atomic_flag nesnesinin değerini ayarlar ve önceki değerini döndürür. test_and_set() fonksiyonu, nesnenin değerini belirtilen değere ayarlar ve önceki değerini döndürür. func1() ve func2() işlevleri, flag nesnesinin değerini sırayla ayarlamak için yarışırlar. Bu işlemler, diğer işlem tarafından bayrağın ayarlanmadığı duruma kadar tekrarlanır.

### atomic_flag_clear()

- std::atomic_flag_clear() fonksiyonu, bir std::atomic_flag nesnesinin değerini temizler (sıfırlar).

- Aşağıdaki gibi kullanılabilir:

```CPP
#include <iostream>
#include <atomic>
#include <thread>

std::atomic_flag flag = ATOMIC_FLAG_INIT;

void func() {
    while (flag.test_and_set()) {
        std::this_thread::yield();
    }

    std::cout << "func() acquired the flag\n";

    flag.clear();
    std::cout << "func() cleared the flag\n";
}

int main() {
    std::thread t(func);
    t.join();

    return 0;
}

```
> Bu örnekte, std::atomic_flag_clear() fonksiyonu, flag adlı bir std::atomic_flag nesnesinin değerini temizler. func() işlevi, flag nesnesinin değerini ayarlamak ve temizlemek için yarışır. Bu işlemler, diğer işlem tarafından bayrağın temizlenmediği duruma kadar tekrarlanır.

### atomic_flag_wait()

- std::atomic_flag_wait() fonksiyonu, bir std::atomic_flag nesnesi üzerinde bir değişiklik beklemek için kullanılır.

- Bu fonksiyon, belirtilen expected değeri flag nesnesinin mevcut değerine eşit olmadığı sürece, işlemciye dinlenme (wait) emri verir. Dinlenme (wait) sırasında diğer iş parçacıkları çalışabilir. Değer değişirse, işlemci uyanır ve devam eder.

- Aşağıdaki gibi kullanılabilir:
```CPP
#include <iostream>
#include <atomic>
#include <thread>

std::atomic_flag flag = ATOMIC_FLAG_INIT;

void func() {
    std::cout << "func() waiting for the flag\n";
    while (flag.test_and_set(std::memory_order_acquire)) {
        std::this_thread::yield();
    }

    std::cout << "func() acquired the flag\n";

    // do some work

    flag.clear(std::memory_order_release);
    std::cout << "func() cleared the flag\n";
}

int main() {
    std::thread t(func);
    // wait for func to acquire the flag
    while (flag.test_and_set(std::memory_order_acquire)) {
        std::this_thread::yield();
    }
    std::cout << "main() acquired the flag\n";

    // do some work

    flag.clear(std::memory_order_release);
    std::cout << "main() cleared the flag\n";

    t.join();

    return 0;
}

```
> Bu örnekte, std::atomic_flag_wait() fonksiyonu, flag adlı bir std::atomic_flag nesnesinin belirli bir değere eşit olmasını bekler. func() ve main() işlevleri, flag nesnesinin değerini ayarlamak ve temizlemek için yarışır. Bu işlemler, diğer işlemin bayrağı temizlediği duruma kadar tekrarlanır.

### atomic_flag_notify_one()

- atomic_flag_notify_one() işlevi, atomic_flag_wait() işlevini kullanarak bekleyen bir threadi uyandırır. Eğer birden fazla thread bekliyorsa, hangi threadin uyandırılacağı belirli değildir. Bu işlevin kullanımı, atomic_flag tipi bir değişkenin paylaşıldığı senaryolarda kullanılabilir.

- Aşağıdaki örnek, atomic_flag tipi bir değişkenin kullanımını ve atomic_flag_notify_one() ve atomic_flag_wait() işlevlerinin kullanımını göstermektedir:

```CPP
#include <iostream>
#include <atomic>
#include <thread>
#include <chrono>

int main() {
    std::atomic_flag flag = ATOMIC_FLAG_INIT;

    std::thread t1([&]() {
        std::this_thread::sleep_for(std::chrono::seconds(2));
        flag.test_and_set();
        std::cout << "Flag set by thread 1\n";
    });

    std::thread t2([&]() {
        flag.wait(true);
        std::cout << "Flag is set. Thread 2 notified\n";
    });

    std::thread t3([&]() {
        flag.wait(true);
        std::cout << "Flag is set. Thread 3 notified\n";
    });

    t1.join();

    flag.notify_one();

    t2.join();
    t3.join();

    return 0;
}

```
> Bu örnek, std::atomic_flag tipi bir değişken kullanılarak iki threadin senkronize edilmesini gösterir. İlk thread, flag adlı değişkeni 2 saniye sonra set eder. İkinci ve üçüncü threadler, flag değişkeninin true olmasını bekleyerek uyutulur. Sonra, ilk thread flag değişkenini set eder ve notify_one() işlevini çağırarak bekleyen threadlerden birini uyandırır. Uyanan thread, wait() işlevinden döner ve "Flag is set. Thread 2 notified" veya "Flag is set. Thread 3 notified" mesajlarını yazdırır.

### atomic_flag_notify_all()

- atomic_flag_notify_all() fonksiyonu, belirtilen bayrağa bağlı bekleyen tüm iş parçacıklarını uyandırır. atomic_flag_clear() fonksiyonuna benzer şekilde, bu fonksiyonu çağıran iş parçacığından farklı bir iş parçacığı tarafından beklenen bir bayrağın değerini değiştirirken dikkatli olunmalıdır.

- Aşağıda bir örnek verilmiştir:

```CPP
#include <iostream>
#include <thread>
#include <atomic>

int main() {
    std::atomic_flag flag = ATOMIC_FLAG_INIT;
    std::thread threads[5];

    for (int i = 0; i < 5; i++) {
        threads[i] = std::thread([&]() {
            while(flag.test_and_set(std::memory_order_acquire)) {
                std::this_thread::yield();
            }

            std::cout << "Thread ID " << std::this_thread::get_id() << " entered critical section\n";
            std::this_thread::sleep_for(std::chrono::seconds(1));
            std::cout << "Thread ID " << std::this_thread::get_id() << " left critical section\n";

            flag.clear(std::memory_order_release);
        });
    }

    std::this_thread::sleep_for(std::chrono::seconds(3));

    std::cout << "Notifying all threads to enter critical section\n";
    flag.notify_all();

    for (int i = 0; i < 5; i++) {
        threads[i].join();
    }

    return 0;
}

```

> Bu örnekte, std::atomic_flag tipinde bir bayrak flag oluşturulur ve ATOMIC_FLAG_INIT sabiti ile başlatılır. Ardından, 5 iş parçacığı oluşturulur ve her biri kritik bölgeye girip çıkmak için bayrağı kullanır. İlk önce, flag.test_and_set(std::memory_order_acquire) fonksiyonu çağrılarak bayrağın değeri ayarlanır ve std::this_thread::yield() fonksiyonu ile iş parçacığı kilitli bir döngüde bekletilir. Sonra, kritik bölgeye girmek için bayrak değiştirilir ve çıkış için bayrak temizlenir. Son olarak, tüm iş parçacıklarına bayrağı beklemeleri için bir sinyal göndermek için flag.notify_all() fonksiyonu çağrılır.

### atomic_init()

- std::atomic_init fonksiyonu, bir std::atomic nesnesini belirtilen değerle başlatmak için kullanılır. Fonksiyon, ilgili std::atomic türüne bağlı olarak değişken sayıda argüman kabul eder.
```CPP
void atomic_init(std::atomic<T>* obj, T desired);

```
- Örneğin, aşağıdaki kod, bir std::atomic int  nesnesini 0 ile başlatır:

```CPP
#include <atomic>
#include <iostream>

int main() {
    std::atomic<int> a;
    std::atomic_init(&a, 0);

    std::cout << "Value of a is " << a << '\n';

    return 0;
}

```
### kill_dependency

- std::kill_dependency işlevi, bir yazma işleminden sonra okuma işlemine kadar ki bir sıralama ilişkisini önlemek için kullanılır. Bu işlev, optimize edicilerin, yazma işlemi ile okuma işlemi arasındaki ilişkiyi yok saymasını önler.

- Bu işlev, genellikle bir std::memory_order_consume içeren bir okuma işleminden sonra bir std::memory_order_relaxed içeren bir yazma işlemine kadar olan sıralama ilişkisini sağlamak için kullanılır.

- Örneğin:

```CPP
#include <atomic>
#include <iostream>

int main() {
    std::atomic<int> a(0);
    std::atomic<int> b(0);

    a.store(1, std::memory_order_relaxed);
    b.store(2, std::memory_order_relaxed);

    int x = a.load(std::memory_order_consume);
    int y = b.load(std::memory_order_relaxed);

    // Sıralama ilişkisi garantisi yok.
    std::cout << "x: " << x << ", y: " << y << '\n';

    x = std::kill_dependency(x);
    b.store(3, std::memory_order_relaxed);

    // Sıralama ilişkisi garantisi var.
    std::cout << "x: " << x << ", y: " << y << '\n';

    return 0;
}

```

> Bu örnekte, a ve b adında iki adet std::atomic int nesnesi oluşturulmuştur. Daha sonra, a ve b'ye sırasıyla 1 ve 2 değerleri atanmıştır. Sonra a'nın load işlemi, std::memory_order_consume ile yapılmıştır. Ancak, bu işlem y'ye atanmadan önce gerçekleştirilmiştir. Bu nedenle, y'nin değerini okurken, x'in değeri 1 veya 2 olabilir. Ancak x, std::kill_dependency işlevi ile işaretlendikten sonra b'ye 3 atanmadan önce güncellendiği için, x'in değeri artık 1 veya 2 olamaz.

### atomic_thread_fence()

- atomic_thread_fence() fonksiyonu, herhangi bir veri türünden herhangi bir bellek erişimindeki kodun sıralamasını değiştirmeyen bir engelleme işlemi gerçekleştirir. Bu işlev, kodun çıktısını belirli bir şekilde yapılandırmaya yardımcı olmak için kullanılabilir.

- atomic_thread_fence() işlevi, belirli bir bellek düzenlemesi türünden (örneğin, bellek erişimi öncesinde yazma işlemini barındıran) herhangi bir bellek erişiminden önce ve sonra çağrılmalıdır.

- Bu işlevin örnek kullanımı şöyle olabilir:

```CPP
#include <atomic>
#include <thread>

std::atomic<int> a;
int b;

void thread_1() {
    a.store(1, std::memory_order_relaxed);
    std::atomic_thread_fence(std::memory_order_acquire);
    b = a.load(std::memory_order_relaxed);
}

void thread_2() {
    a.store(2, std::memory_order_relaxed);
    std::atomic_thread_fence(std::memory_order_acquire);
    b = a.load(std::memory_order_relaxed);
}

```

> Bu örnekte, std::atomic_thread_fence(std::memory_order_acquire) işlevi, belirli bir bellek düzenlemesi türünden bellek erişiminden önce ve sonra çağrılır. Bu, kodun çıktısını yapılandırmaya yardımcı olur ve beklenmeyen davranışları önler.

### atomic_signal_fence()

- atomic_signal_fence() işlemci tarafından üretilen sinyallerin, std::atomic tipi değişkenlerin işlemleri için tamponlarına yazılmadan önce gönderilmesini sağlar. Yani, atomic_signal_fence() işlemci tarafından üretilen sinyallerin (örneğin SIGINT) std::atomic tipi değişkenlerdeki işlemlerle karışmamasını garanti eder.

- Bu fonksiyon, belirtilen yerde bir sinyal bariyeri oluşturur ve değişkenler üzerindeki tüm okuma/yazma işlemlerinin tamponlardan gerçek hafızaya doğru yürütülmesini garanti eder.

- Örneğin, bir sinyal (örneğin SIGINT) ile ayrılmış iki iş parçacığı olduğunu ve bir iş parçacığının std::atomic tipi bir değişkene yazdığını ve diğer iş parçacığının okuduğunu düşünelim. Bu işlemlerin bir sinyal bariyeri olmadan yapılması durumunda, sinyalin bu işlemlere müdahale etmesi mümkündür. Ancak atomic_signal_fence() kullanarak sinyal bariyeri oluşturursak, bu tür bir müdahale engellenir ve değişkenlerin doğru değerleri korunur.

### ATOMIC_VAR_INIT
- ATOMIC_VAR_INIT bir makro olup, bir atomik değişkenin başlatılmasına yardımcı olur. Bu makro, bir atomik değişkenin başlatılmasında kullanılmak üzere sabit bir değer sağlar.

- Örneğin, aşağıdaki kodda x adında bir atomik bir tamsayı değişkeni tanımlanmaktadır ve 0 ile başlatılmaktadır:

```CPP
#include <atomic>

std::atomic<int> x(ATOMIC_VAR_INIT(0));

```

> Bu makro, birçok derleyicide, aynı zamanda C++11'in önerdiği std::atomic_init işlevi yerine de kullanılabilir.

### ATOMIC_FLAG_INIT

- ATOMIC_FLAG_INIT bir makro olup, bir atomik bayrak değişkeninin başlatılmasına yardımcı olur. Bu makro, bir atomik bayrak değişkeninin başlatılmasında kullanılmak üzere sabit bir değer sağlar.

- Örneğin, aşağıdaki kodda flag adında bir atomik bayrak değişkeni tanımlanmaktadır ve ATOMIC_FLAG_INIT kullanılarak başlatılmaktadır:

```CPP
#include <atomic>

std::atomic_flag flag = ATOMIC_FLAG_INIT;

```
> Bu makro, birçok derleyicide, aynı zamanda C++11'in önerdiği std::atomic_flag_init işlevi yerine de kullanılabilir.

































































































































































































































































































































































































































# Diğer Örnekler
- Örneğin, bir std::atomic<int> nesnesi aşağıdaki gibi tanımlanabilir:

```CPP
std::atomic<int> myAtomicVariable(0);

```

- Bu nesne, 0 ile başlatılır ve herhangi bir işlem yapılacağı zaman, ilgili işlemler std::atomic sınıfının member fonksiyonları kullanılarak gerçekleştirilir. Örneğin:

```CPP
myAtomicVariable++; // atomic increment operation
int value = myAtomicVariable.load(); // atomic load operation

```

- Bu kodda, ++ operatörü ile myAtomicVariable değişkeninin değeri atomik olarak arttırılır ve load() fonksiyonu ile değişkenin değeri atomik olarak okunur.

- std::atomic sınıfı, C++'ta multi-threading uygulamalarının güvenliğini sağlamak için oldukça önemlidir. Ancak, yanlış kullanımı, performans sorunlarına ve hatalara neden olabilir.

# kısaca değişkenlerin değerlerinin farklı kaynaklar tarafından okunması ve yazılması sistemini mi yönetir

- Evet, doğru. std::atomic, birden çok iş parçacığı tarafından aynı anda erişilen değişkenlerin değerlerinin güvenli bir şekilde okunması ve yazılmasını sağlar. Bu, verilerin tutarlılığını sağlamak için çok önemlidir ve özellikle paralel programlama veya çoklu iş parçacığı uygulamalarında kullanışlıdır.

# pratikte uygulamalarda nerelerde kullanılır? Bana örnekler ver

- std::atomic başlık dosyasında tanımlanan sınıflar, değişkenlerin thread-safe bir şekilde okunması ve yazılması için kullanılır. Bunlar, birden fazla iş parçacığı tarafından paylaşılan verilerin güvenli bir şekilde kullanılmasını sağlar.

- std::atomic sınıfı, birçok farklı senaryoda kullanılabilir. Örneğin:

**İş parçacığı güvenli sayılar: std::atomic ile iş parçacığı güvenliği sağlanmış sayılar (int, float, double, vb.) tanımlanabilir. Bu sayılar, birden fazla iş parçacığı tarafından okunabilir ve yazılabilir.**

**Atomic işlemler: Bir işlemin birçok adımının bir arada çalıştırılması gereken senaryolarda (örneğin bankacılık işlemleri), std::atomic sınıfı kullanılabilir. Bu şekilde, birden fazla işlem arasında kesinti olmadan çalışan bir sistem sağlanabilir.**

**Thread-safe veri yapıları: std::atomic sınıfı, thread-safe veri yapılarının oluşturulmasına yardımcı olabilir. Örneğin, std::atomic_flag sınıfı, bir bool değişkeni gibi çalışarak bir iş parçacığının kritik bölgesine girmesini önleyebilir.**

Örnek olarak, bir sayacı birden fazla iş parçacığı tarafından güvenli bir şekilde artırmak istediğinizi düşünelim. Bu durumda, std::atomic sınıfı kullanarak bir iş parçacığı güvenli sayı tanımlayabilirsiniz:

```CPP
#include <iostream>
#include <atomic>
#include <thread>

std::atomic<int> counter(0);

void incrementCounter(int id) {
    for (int i = 0; i < 100; i++) {
        counter++;
        std::cout << "Thread " << id << " incremented counter to " << counter << std::endl;
    }
}

int main() {
    std::thread t1(incrementCounter, 1);
    std::thread t2(incrementCounter, 2);
    t1.join();
    t2.join();
    std::cout << "Final counter value: " << counter << std::endl;
    return 0;
}

```
> Bu kodda, iki iş parçacığı tarafından incrementCounter() fonksiyonu aynı anda çalıştırılır ve counter değişkeni thread-safe bir şekilde güncellenir. Sonuç olarak, bu programı çalıştırdığınızda counter değişkeninin son değerinin 200 olacağını görebilirsiniz.





















