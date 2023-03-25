- scoped_allocator başlık dosyası, C++11 standartlarından itibaren mevcut olan öncelikli tahsis ediciler (allocator) kullanımını kolaylaştıran bir araçtır. Bu başlık dosyası, C++11 öncesi sürümlerde yerleşik olmayan bir özellik olan scoped_allocator_adaptor sınıfını tanıtır.

- scoped_allocator_adaptor sınıfı, bir öncelikli tahsis edici (allocator) nesnesini alır ve bu öncelikli tahsis ediciyi kullanarak tahsis edilen bellek alanını (memory block) yönetir. Bu sınıf, belirtilen türdeki nesneler için tahsis edilen bellek alanının yaşam süresini belirleyen dış etmenlere bağlı olarak çalışır. Bu sayede, C++11 standartlarından itibaren desteklenen öncelikli tahsis edicileri (allocator) kullanarak bellek yönetimi işlemleri daha rahat bir şekilde gerçekleştirilebilir.

- scoped_allocator_adaptor sınıfı, birbirine bağlı bellek tahsis işlemleri yapmak isteyen sınıflar için kullanışlı bir araçtır. Örneğin, bir vector nesnesi oluşturulurken, scoped_allocator_adaptor sınıfı kullanılarak bu vektörün öğeleri için ayrılmış bellek alanı, vektör nesnesinin ömrü sona erdiğinde otomatik olarak serbest bırakılabilir.

- Özetle, scoped_allocator başlık dosyası, C++11 öncesi öncelikli tahsis edicilerin (allocator) kullanımını kolaylaştıran bir araçtır ve scoped_allocator_adaptor sınıfı, birbirine bağlı bellek tahsis işlemleri yapmak isteyen sınıflar için kullanışlı bir araçtır.

# Bunu ne gibi senaryolarda kullanmaliyim? Bana ornekler goster

- scoped_allocator özelliği, C++11'de tanıtılan bir özelliktir ve özellikle standart kütüphane tarafından kullanılır. Bu özellik, birleştirilmiş bellek havuzlarına erişim sağlar ve bir öğenin bellek ihtiyaçlarının tam olarak belirlenmesine olanak tanır.

- Örneğin, STL'nin vector sınıfı, allocator sınıfının özelleştirilmiş bir sürümünü kullanarak bellek tahsisi yapar. Bu özelleştirilmiş allocator, C++11'de tanıtılan scoped_allocator özelliğini kullanabilir. Böylece bir vector nesnesi ve içindeki elemanlar, aynı bellek havuzunda yönetilebilir.

- Bununla birlikte, scoped_allocator'ün kullanımı sadece STL sınıfları ile sınırlı değildir. Özellikle birleştirilmiş bellek havuzlarına ihtiyaç duyan özelleştirilmiş veri yapıları ve işlemler için kullanılabilir.

- Aşağıda, scoped_allocator kullanılarak vector nesnesi ve içindeki elemanların bellek havuzunda yönetilmesi örneği verilmiştir:

```CPP
#include <iostream>
#include <vector>
#include <memory>
#include <scoped_allocator>

// Bellek tahsisini yönetmek için kullanılacak havuz
template<typename T>
using MyPool = std::pmr::unsynchronized_pool_resource;

// Havuz ile eşleşen bir öğe türü
template<typename T>
using MyAlloc = std::scoped_allocator_adaptor<std::allocator<T>, MyPool<T>>;

// scoped_allocator kullanarak bir vector nesnesi oluşturma
void test_scoped_allocator()
{
    // Bellek havuzu oluşturma
    MyPool<int> pool;

    // scoped_allocator kullanarak vector nesnesi oluşturma
    std::vector<int, MyAlloc<int>> v(MyAlloc<int>{}, &pool);

    // Vector'a elemanlar ekleme
    v.push_back(1);
    v.push_back(2);
    v.push_back(3);

    // Elemanları yazdırma
    for (auto x : v) {
        std::cout << x << " ";
    }
    std::cout << std::endl;
}

```
- Bu örnekte, MyPool isimli bir bellek havuzu oluşturuluyor ve MyAlloc isimli bir öğe tipi tanımlanıyor. MyAlloc, std::scoped_allocator_adaptor kullanarak std::allocator ile MyPool arasında birleştirme yapıyor.

- std::vector<int, MyAlloc<int>> kullanılarak bir vector nesnesi oluşturuluyor ve bellek havuzu &pool adresi ile ilişkilendiriliyor. Son olarak, push_back yöntemi ile elemanlar ekleniyor ve for döngüsü ile elemanlar yazdırılıyor.



