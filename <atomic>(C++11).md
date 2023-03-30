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





















