- queue başlık dosyası, C++ standart kütüphanesinde bulunan bir sıra veri yapısı olan queue sınıfını tanımlar. queue sınıfı, bir koleksiyonun başına eleman eklemek ve sonundan eleman çıkarmak için kullanılır.

- queue sınıfının başlıca işlevleri şunlardır:

- **push():** Sıranın sonuna yeni bir eleman ekler.
- **pop():** Sıranın başındaki elemanı çıkarır.
- **front():** Sıranın başındaki elemanı döndürür.
- **back():** Sıranın sonundaki elemanı döndürür.
- **empty():** Sıranın boş olup olmadığını kontrol eder.
- **size():** Sıradaki eleman sayısını döndürür.
- queue sınıfı, verileri FIFO (First-In-First-Out) şekilde yönetir. Yani, sıranın başındaki eleman, en önce eklenen elemandır ve sıranın sonundaki eleman, en son eklenen elemandır. Bu özellik, genellikle işlem sıralarını veya bekleyen işleri yönetmek için kullanılır.

- Örneğin, aşağıdaki kod, queue sınıfının temel kullanımını gösterir:

```CPP
#include <iostream>
#include <queue>

int main() {
    std::queue<int> myQueue;

    myQueue.push(10);
    myQueue.push(20);
    myQueue.push(30);

    std::cout << "Size of myQueue: " << myQueue.size() << std::endl;

    while (!myQueue.empty()) {
        std::cout << myQueue.front() << std::endl;
        myQueue.pop();
    }

    return 0;
}

```

- Bu kod, queue sınıfının push(), front(), empty() ve pop() işlevlerini kullanarak bir int sırası oluşturur ve sıradaki elemanları yazdırır.

- <queue> başlık dosyası, C++ standart kütüphanesindeki konteyner adaptörlerinden olan queue ve priority_queue sınıflarını içerir.

- queue sınıfı, FIFO (First In First Out) prensibine göre çalışan bir veri yapısıdır. queue sınıfı, varsayılan olarak deque yapısını kullanarak çalışır, ancak list ve vector yapısını da kullanabilir. queue sınıfının temel işlevleri, yine FIFO prensibine uygun şekilde, eleman ekleme işlemi için push(), eleman çıkarma işlemi için pop(), ilk elemana erişim işlemi için front(), son elemana erişim işlemi için back(), boş olup olmadığını kontrol etmek için empty() ve eleman sayısını öğrenmek için size() işlevleridir.

- priority_queue sınıfı ise, verileri öncelik sırasına göre saklamak için kullanılır. Bu sınıf, varsayılan olarak büyükten küçüğe doğru bir öncelik sırası kullanır, ancak kullanıcı tarafından belirlenen bir karşılaştırma işlevi kullanılarak öncelik sırası değiştirilebilir. priority_queue sınıfının temel işlevleri, eleman ekleme işlemi için push(), en yüksek önceliğe sahip elemanı çıkarma işlemi için pop(), en yüksek önceliğe sahip elemana erişim işlemi için top(), boş olup olmadığını kontrol etmek için empty() ve eleman sayısını öğrenmek için size() işlevleridir.

- Bu konteyner adaptörlerinin kullanımı, veri yapılarının işlevlerine ve kullanım amaçlarına göre değişiklik gösterir. Örneğin, verilerin öncelik sırasına göre saklanması gerektiğinde priority_queue sınıfı kullanılırken, verilerin sırayla işlenmesi gerektiğinde queue sınıfı kullanılabilir.



































