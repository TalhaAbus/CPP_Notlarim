# std::deque nedir

- std::deque (double-ended queue) bir C++ standart kütüphanesi veri yapısıdır. "Double-ended" ifadesi, veri yapısının hem ön hem de arka tarafında eleman eklemeye ve çıkarmaya izin verir.

- std::deque bir sıra olarak düşünülebilir, ancak sadece ön veya arka tarafından eleman ekleme veya çıkarma yapmakla sınırlı kalmaz. std::deque aynı zamanda, bir vektörün yapabileceği gibi, arka arkaya bellek alanlarına elemanlar yerleştirmek için yeniden boyutlandırılabilir.

- std::deque, diğer birçok C++ standart kütüphanesi veri yapısına benzer şekilde çalışır. Elemanlar bir veya daha fazla bellek bloğunda saklanır ve belirli bir kapasiteye sahiptir. Ancak, std::deque veri yapısının bir diğer avantajı, elemanların ekleme ve çıkarma işlemlerinde O(1) zaman karmaşıklığına sahip olmasıdır. Bu, std::deque'nin büyük miktarda veri ile çalışırken performans açısından avantajlı olmasını sağlar.

- std::deque veri yapısı, std::vector ve std::list veri yapılarına benzer şekilde kullanılır. Ancak, std::vector'ün daha hızlı erişim zamanı ve std::list'in daha iyi dinamik boyutlandırma özellikleri varken, std::deque veri yapısı hem hızlı erişim hem de dinamik boyutlandırma özelliklerine sahiptir.

- Aşağıda, std::deque veri yapısının kullanımına dair bir örnek verilmiştir:

```CPP
#include <iostream>
#include <deque>

int main() {
    std::deque<int> myDeque;

    // Ön taraftan eleman ekleme
    myDeque.push_front(10);
    myDeque.push_front(20);
    myDeque.push_front(30);

    // Arka taraftan eleman ekleme
    myDeque.push_back(40);
    myDeque.push_back(50);
    myDeque.push_back(60);

    // Elemanları yazdırma
    std::cout << "Deque elemanlari: ";
    for (auto it = myDeque.begin(); it != myDeque.end(); ++it) {
        std::cout << *it << " ";
    }

    return 0;
}

```
> Bu örnekte, std::deque veri yapısından bir nesne oluşturulur ve önce ön taraftan, sonra da arka taraftan elemanlar eklenir. Son olarak, std::deque'nin elemanları for döngüsü kullanılarak yazdırılır.


# ben bu sinifi ne zaman kullanmaliyim? Bunun yerine ayni isi yapabilecegim bir baska sinif varsa hangisini sececegim?

- std::deque veri yapısını kullanmanız, aşağıdaki koşulların en az biri sağlandığında faydalı olabilir:

- std::vector veri yapısından daha iyi performans elde etmek istiyorsanız: std::vector veri yapısı, öğelerin bellekte ardışık bir blokta saklanması nedeniyle erişimde hızlıdır, ancak öğelerin eklenmesi veya çıkarılması genellikle son elemanların yeniden yerleştirilmesini gerektirdiği için performansı düşürebilir. Öte yandan, std::deque veri yapısı, öğelerin ön veya arka uçlarına eklenip çıkarılabildiği için performans açısından daha iyi olabilir.

- std::list veri yapısından daha iyi bellek kullanımı sağlamak istiyorsanız: std::list veri yapısı, eklenen öğelerin sayısına bağlı olarak yeniden boyutlandırılması gerekmeyen bir liste yapısıdır, ancak öğelerin bellekte dağınık olarak saklanması nedeniyle erişimde yavaş olabilir. std::deque veri yapısı, bellekte öğelerin ardışık bloklarda saklanması nedeniyle std::list veri yapısına göre daha iyi bellek kullanımı sağlar.

- Öğelerin hem ön hem de arka uçlara eklenmesi gerektiğinde: std::deque veri yapısı, öğelerin hem ön hem de arka uçlara eklenmesine izin verirken, std::vector veri yapısı yalnızca arka uca öğe eklenmesine izin verir.

- Öte yandan, std::deque veri yapısı bazı durumlarda std::vector veya std::list veri yapılarından daha az performanslı olabilir. Örneğin, bir sıraya erişim rastgele ise ve sıranın sonundan eleman silinmesi gerekiyorsa, std::vector veri yapısı daha iyi performans sağlayabilir.

- Sonuç olarak, std::deque veri yapısını kullanmanız, özellikle hem önden hem de arkadan eleman ekleme veya çıkarma işlemleri yapmanız gereken durumlarda uygun olabilir. Ancak, uygulamanın ihtiyaçlarına ve kullanım senaryosuna bağlı olarak, std::vector veya std::list gibi diğer veri yapılarının kullanımı daha uygun olabilir.





