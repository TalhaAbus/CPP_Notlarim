- C++11'de tanıtılan future başlık dosyası, C++ programlarında çoklu iş parçacıklı programlamayı kolaylaştırmak için kullanılır. Bu başlık dosyası, std::async ve std::future gibi sınıfları tanımlar.

- std::async, bir işlevi asenkron olarak başlatır ve std::future nesnesi döndürür. std::future, asenkron işlevin sonucunu depolar ve sonucu elde etmek için kullanılır.

- Bu sınıflar, programlarda aynı anda birden fazla iş yapılabilmesini ve işlerin sonuçlarının daha verimli bir şekilde yönetilebilmesini sağlar. Örneğin, bir işlemci çekirdeği hesaplama yaparken, diğer çekirdekler başka işlerle meşgul olabilir. Bu sayede programın daha hızlı ve verimli çalışması sağlanabilir.

- std::future başlık dosyasının kullanımı, özellikle büyük ve karmaşık programlarda oldukça yararlıdır. Özellikle işlemlerin birbirinden bağımsız olduğu durumlarda, çoklu iş parçacıklı programlama sayesinde daha hızlı sonuçlar elde edilebilir.

- **std::future** sınıfı, bir işlemi başlatmak ve sonucunu beklemek için kullanılır. 
- **std::promise** sınıfı, bir std::future nesnesi oluşturmak için kullanılan bir araçtır. 
- **std::async()** fonksiyonu, bir işlevi veya işlev nesnesini yeni bir iş parçacığında veya iş parçacığı havuzunda asenkron olarak çalıştırmak için kullanılır. 
- **std::packaged_task** sınıfı, bir işlevi veya işlev nesnesini, std::future sınıfı kullanarak başlatmak ve sonucunu döndürmek için bir araçtır.

- future başlık dosyası, C++11 standardında yer alan çoklu iş parçacığı desteği için tanımlanmış sınıfları içerir. Bu sınıflar, bir işlemi başlatmak ve bitene kadar beklemek için kullanılan araçlar sunar.

- std::future sınıfı, bir işlemi başlatmak ve sonucunu beklemek için kullanılır. std::promise sınıfı, bir std::future nesnesi oluşturmak için kullanılan bir araçtır. std::async() fonksiyonu, bir işlevi veya işlev nesnesini yeni bir iş parçacığında veya iş parçacığı havuzunda asenkron olarak çalıştırmak için kullanılır. std::packaged_task sınıfı, bir işlevi veya işlev nesnesini, std::future sınıfı kullanarak başlatmak ve sonucunu döndürmek için bir araçtır.

- Bu sınıflar, C++ programlamada çoklu iş parçacıklarla çalışırken, iş parçacıkları arasında veri paylaşımı ve senkronizasyonu kolaylaştırmak için kullanılır.
  

- Bir örnek kullanımı şu şekildedir:

```CPP
#include <iostream>
#include <future>

int main() {
    // asenkron olarak bir işlev çağırma
    std::future<int> future = std::async(std::launch::async, []() {
        return 42;
    });

    // işlev tamamlanana kadar bekleyin ve sonucu yazdırın
    std::cout << "The answer is: " << future.get() << std::endl;

    return 0;
}

```

- Bu kod, bir lambda işlevini asenkron olarak başlatır ve sonucu bir std::future nesnesinde depolar. std::future.get() işlevi, işlev tamamlanana kadar bekler ve sonucu yazdırır.





















