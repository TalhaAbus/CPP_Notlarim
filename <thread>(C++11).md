- <thread> başlık dosyası, çoklu iş parçacıklı programlama için C++11 standartlarına uygun bir araç sağlar. Bu başlık dosyası, C++11 öncesi standartlarda yerleşik bir çoklu iş parçacıklı desteği yoktu, ancak C++11 ile birlikte gelen <thread> başlık dosyası sayesinde, birbirinden bağımsız birden fazla iş parçacığı oluşturulabilir ve her biri aynı anda çalıştırılabilir.

- Bu başlık dosyası, std::thread sınıfını içerir ve bu sınıf, bir iş parçacığı temsil eder. Bu sınıf sayesinde bir iş parçacığı oluşturulabilir ve bu iş parçacığına bir işlev (fonksiyon) atanabilir. Bu işlev, ayrı bir iş parçacığında çalıştırılır ve ana programın işlevselliği bundan etkilenmez.

- <thread> başlık dosyası ayrıca diğer yardımcı sınıflar ve işlevler de sağlar. std::mutex, std::condition_variable, std::lock_guard, std::unique_lock ve std::atomic gibi diğer başlık dosyalarında da yer alan bazı sınıfların benzerlerine sahiptir.

- <thread> başlık dosyasının kullanımı, özellikle büyük ve karmaşık projelerde, kodların düzenli olmasını ve hataların tespit edilmesini kolaylaştırabilir. Ancak, yanlış kullanıldığında, çoklu iş parçacıklı programlama büyük ölçüde hata verici olabilir ve bu nedenle <thread> başlık dosyasının kullanımı, bu konuda deneyimli programcılar tarafından yapılmalıdır.

- C++11'den önce, çoklu iş parçacıklı programlama için POSIX threads (pthread) kütüphanesi kullanılıyordu. Ancak bu kütüphane C++ dilinin standart kütüphanesi ile uyumlu değildi ve kullanımı zordu. Ayrıca, POSIX threads kütüphanesi, C++ dilinin diğer özellikleri gibi özellikle nesne yönelimli programlama paradigmasına uygun değildi.

- C++11'de <thread> başlık dosyası eklenerek, C++ dilinin standart kütüphanesi ile uyumlu bir şekilde çoklu iş parçacıklı programlama yapılabilmektedir. Bu başlık dosyası, C++11 standartlarına uygun olarak tanımlanmış bir thread sınıfı içerir ve bu sınıf, önceki yöntemlere kıyasla daha kolay ve nesne yönelimli bir şekilde çoklu iş parçacıklı programlama yapmayı sağlar. Ayrıca, <thread> başlık dosyası diğer faydalı sınıflar ve fonksiyonlar içerir, örneğin mutex, condition_variable, future vb.

- Bu nedenlerden dolayı, C++11'den sonra <thread> başlık dosyası kullanarak çoklu iş parçacıklı programlama yapmak, POSIX threads kütüphanesi kullanmaktan daha uygun ve kolaydır.

- C++'ın <thread> başlık dosyası, C++11 ile birlikte birçok çoklu iş parçacıklı programlama özelliği ekledi. Bu başlık dosyası, C++ programlarında çoklu iş parçacıklı programlama oluşturmak ve yönetmek için kullanılan bir dizi işlevi ve sınıfı içerir.

<thread> başlık dosyasındaki bazı işlevler şunlardır:

- **std::thread:** bir iş parçacığını temsil eden bir sınıf türüdür.
- **std::this_thread::sleep_for():** bir süre boyunca iş parçacığını uyutur.
- **std::this_thread::yield():** iş parçacığının işlemciden çıkmasını ve diğer iş parçacıklarının işlemciyi kullanmasına izin verir.
- **std::thread::join():** bir iş parçacığı nesnesinin sonlanmasını beklemek için kullanılır.
- **std::thread::detach():** bir iş parçacığının bağımsız hale getirilmesi için kullanılır.
- Bu başlık dosyasındaki sınıflar ve işlevler, birden fazla iş parçacığı oluşturma, iş parçacıkları arasında veri paylaşımı, senkronizasyon ve daha fazlası gibi işlemleri kolaylaştırır.


- örnek bir kullanım paylaşabilirim:

```CPP
#include <iostream>
#include <thread>
#include <chrono>

void threadFunction(int threadId) {
    std::cout << "Thread " << threadId << " started\n";
    std::this_thread::sleep_for(std::chrono::seconds(1));
    std::cout << "Thread " << threadId << " ended\n";
}

int main() {
    std::thread thread1(threadFunction, 1);
    std::thread thread2(threadFunction, 2);

    std::cout << "Main thread started\n";
    
    thread1.join();
    thread2.join();

    std::cout << "Main thread ended\n";

    return 0;
}

```

- Bu örnekte, threadFunction adında bir fonksiyon tanımlanmış ve bu fonksiyon parametre olarak bir tamsayı alıyor. main fonksiyonu içerisinde ise iki adet thread oluşturulmuş ve bunlara sırasıyla 1 ve 2 sayıları gönderilmiş. Ardından ana thread'in 1 saniye uyuması sağlanmış ve her iki thread de sonlandırılmış. Bu örnekte std::this_thread::sleep_for fonksiyonu, mevcut thread'in belirtilen süre boyunca uyumasını sağlar.

- Çalıştırıldığında, bu örnek aşağıdaki gibi bir çıktı üretir:

```CPP
Thread 1 started
Thread 2 started
Main thread started
Thread 1 ended
Thread 2 ended
Main thread ended

```


















































