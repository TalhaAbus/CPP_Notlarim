- utility başlık dosyası, C++ standart kütüphanesinin bir parçasıdır ve çeşitli faydalı araçlar sağlayan bazı şablon sınıflar, işlevler ve diğer öğeler içerir. İşlevler, özellikle de şablon işlevler, bir argümanın değerini işleyip başka bir değer döndürmek için kullanılabilir. Ayrıca, std::pair sınıfı, bir anahtar-değer çiftini temsil etmek için kullanılabilir. Bu, özellikle bir map yapısı gibi, anahtar-değer çiftlerinin bulunduğu bir koleksiyonda kullanışlıdır. utility başlık dosyası ayrıca bazı tür dönüştürme işlevleri içerir, örneğin std::move işlevi, bir nesnenin sahipliğini başka bir nesneye aktarmak için kullanılır.

İşlevlerin yanı sıra, utility başlık dosyası ayrıca bazı tür özellikleri için şablon sınıflar içerir. Örneğin, std::integral_constant şablon sınıfı, herhangi bir tamsayı sabitinin bir tür olarak temsil edilmesine olanak tanır. Bu, diğer şablon sınıfları veya işlevler için bir tamsayı sabiti kullanmak istediğinizde kullanışlıdır.  utility başlık dosyası ayrıca, bir tamsayı dizisi oluşturmak veya bir dizi içindeki minimum ve maksimum değerleri bulmak için kullanabileceğiniz std::integer_sequence şablon sınıfını da içerir.

- <utility başlık dosyası, birçok farklı durumda kullanılabilecek işlevlere ve sınıflara ev sahipliği yapar. En önemli sınıflar arasında std::pair ve std::tuple yer alır. Bu sınıflar, farklı türdeki iki veya daha fazla değeri bir arada tutmak için kullanılabilir.

Ayrıca, std::move ve std::forward gibi C++11'de eklenen hareketli semantikler için önemli işlevleri de içerir. Bunlar, programcılara performansı artırmak ve bellek yönetimini daha etkin hale getirmek için kullanılır.

std::swap ve std::make_pair gibi işlevler de <utility başlık dosyasında yer alır. Bunlar, C++ standart kütüphanesi tarafından sağlanan işlevlerdir ve programcılara pratik yardımcı işlevler sunarlar.

Kısacası, <utility başlık dosyası, farklı türler arasında değerlerin hareket ettirilmesi, çift ve tuple gibi yapıların kullanımı, swap işlemi ve diğer yardımcı işlevler gibi birçok işlev ve sınıf sağlar. Bu nedenle, C++ programlamada oldukça yaygın olarak kullanılır.

- utility başlık dosyası, STL konteyner sınıflarının birçoğunda yer alan özel bir yapı olan std::pair'ın yanı sıra diğer bazı sınıfların da tanımlandığı bir başlık dosyasıdır. std::pair, iki nesneyi bir çift olarak tutmak için kullanılır.

Örneğin, bir işlem sonucunu ve geri dönüş değerini tutmak için std::pair kullanabilirsiniz. Aşağıdaki örnek, bir std::map nesnesinin find() yöntemini kullanarak bir anahtarın varlığını kontrol ederken std::pair kullanarak sonucu ve geri dönüş değerini bir çift olarak tutar:

```CPP
#include <iostream>
#include <map>
#include <utility>

int main() {
    std::map<int, std::string> myMap = {{1, "one"}, {2, "two"}, {3, "three"}};

    auto result = myMap.find(2);

    if (result != myMap.end()) {
        std::cout << "Key found: " << result->first << ", value: " << result->second << std::endl;
    } else {
        std::cout << "Key not found" << std::endl;
    }

    return 0;
}

```
- Burada, myMap.find(2) çağrısı, 2 anahtarına karşılık gelen bir değer arar. find() yöntemi, std::map'ın std::pair<iterator, bool> türünden bir değer döndürür. Bu çiftin ilk elemanı, bulunan elemanın bir işaretçisi (iterator)dir ve ikinci elemanı ise, işlemin başarılı olup olmadığını belirten bir bool değeridir. İkinci eleman, true ise bulunan eleman var demektir ve birinci eleman da bu elemanın konumunu gösterir. Eğer ikinci eleman false ise, eleman bulunamamış demektir ve birinci eleman geçersiz olacaktır.

- Bir diğer örnek, bir pair nesnesi oluşturmaktır. pair sınıfı, birbirleriyle ilişkili iki değeri tutmak için kullanılır ve utility başlık dosyası içinde tanımlanmıştır.

```CPP
#include <iostream>
#include <utility>

int main() {
    std::pair<std::string, int> myPair("example", 100);
    std::cout << myPair.first << " " << myPair.second << std::endl;

    return 0;
}

```

- Bu örnekte, bir pair nesnesi oluşturulur ve first öğesi "example" ve second öğesi 100 değerleriyle atanır. Daha sonra, pair nesnesinin first ve second öğeleri ayrı ayrı yazdırılır.



















