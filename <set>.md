# set 

- std::set sınıfı, C++ standart kütüphanesinde bulunan bir veri yapısıdır ve elemanları sıralı bir şekilde tutar. Bu sınıf, elemanların eşsiz (unique) olduğu bir koleksiyon (collection) tanımlamak için kullanılır, yani aynı eleman birden fazla kez eklenemez.

- std::set sınıfı, sıralama kriteri olarak varsayılan olarak "küçükten büyüğe" sıralamayı kullanır, ancak kullanıcı tanımlı sıralama işlevleri de kullanılabilir. Bu, elemanların türüne bağlı olarak, farklı sıralama kriterleri kullanarak elemanların sıralanmasını sağlamak için oldukça yararlıdır.

- std::set sınıfı, elemanların ekleme, çıkarma ve arama işlemlerini hızlı bir şekilde gerçekleştirir. Bu sınıfın bir diğer avantajı da, elemanları eklemeden önce sıralı bir şekilde tutmasıdır, bu sayede elemanlar her zaman sıralı bir şekilde tutulur ve sıralama işlemi yapılmak zorunda kalmaz.

- std::set sınıfı, standart kütüphanenin diğer bileşenleriyle birlikte kullanılarak birçok algoritma ve veri yapısı problemini çözmek için kullanılabilir. Örneğin, bir sözlük yapmak, elemanları sıralı bir şekilde tutmak, öğrencilerin notlarını saklamak gibi birçok kullanım alanı vardır.

- Ayrıca, std::set sınıfı, elemanların var olup olmadığını kontrol etmek, elemanları sıralı bir şekilde göstermek veya aralıklar halinde elemanları göstermek gibi birçok işlevsellik sağlar.

- std::set sınıfı, içinde saklanan öğeleri doğal olarak sıralar. Varsayılan olarak, sıralama öğelerin sıralanmış bir dizisini tutmak için std::less karşılaştırma işlevi kullanılarak gerçekleştirilir. Ancak, sıralama işlevi olarak kullanılacak bir karşılaştırma işlevi belirtmek de mümkündür.

- aşağıdaki örnek, bir std::set nesnesi oluşturarak bir dizi tam sayıyı doğal olarak sıralar:

```CPP
#include <iostream>
#include <set>

int main() {
    std::set<int> mySet = {5, 3, 1, 4, 2}; // doğal olarak sıralanmış olarak saklanacak
    for (auto element : mySet) {
        std::cout << element << " "; // çıktı: 1 2 3 4 5
    }
    return 0;
}

```
- Burada, std::set<int sınıfı, mySet nesnesi olarak oluşturuluyor ve içine {5, 3, 1, 4, 2} değerleri atanıyor. Set nesnesi, verileri doğal olarak sıralayarak saklanacak ve daha sonra for döngüsü kullanılarak bu veriler ekrana yazdırılacaktır.
  
  
 - std::set sınıfı, aynı isme sahip bir std::unordered_set sınıfı gibi, bir sıralı veri yapısıdır. Sınıfın elemanları, doğal olarak artan sırayla saklanır ve bir anahtar-değer çifti kullanır. Bu anahtar-değer çiftleri, anahtarlarla arama yapmayı kolaylaştırır. std::set sınıfının bazı yaygın kullanımları şunlardır:

- **.insert()** : Set nesnesine yeni bir anahtar-değer çifti ekler
- **.erase()** : Set nesnesinden bir veya daha fazla anahtar-değer çifti siler
- **.find()** : Belirli bir anahtarı arar ve varsa bir iterator döndürür
- **.size()** : Set nesnesindeki anahtar-değer çiftlerinin sayısını verir
- **.empty()** : Set nesnesinin boş olup olmadığını kontrol eder
- Ayrıca, diğer STL algoritmaları gibi std::set sınıfını işlemek için birçok algoritma da mevcuttur. Bunlar arasında .merge(), .unique(), .reverse(), .sort() ve .transform() gibi işlemler yer alır.

- std::set sınıfı, nesneleri derleme zamanında değil, çalışma zamanında sıralar. Bu, sınıfın içinde std::less gibi bir karşılaştırma işlevi kullanılarak sıralama yapıldığı anlamına gelir. Sıralama işlemi, her ekleme işlemi veya belirli bir anahtarın aranması sırasında gerçekleşir. Bu da std::set sınıfını kullanmanın bir dezavantajıdır, çünkü eklemeler ve aramalar zaman zaman yavaşlayabilir. Ancak sıralama, özellikle std::set sınıfının büyük veri kümeleri için bir avantajdır, çünkü herhangi bir arama için hızlı bir şekilde sonuç almak mümkündür.

- std::set sınıfı, nesneleri derleme zamanında değil, çalışma zamanında sıralar. Bu, sınıfın içinde std::less gibi bir karşılaştırma işlevi kullanılarak sıralama yapıldığı anlamına gelir. Sıralama işlemi, her ekleme işlemi veya belirli bir anahtarın aranması sırasında gerçekleşir. Bu da std::set sınıfını kullanmanın bir dezavantajıdır, çünkü eklemeler ve aramalar zaman zaman yavaşlayabilir. Ancak sıralama, özellikle std::set sınıfının büyük veri kümeleri için bir avantajdır, çünkü herhangi bir arama için hızlı bir şekilde sonuç almak mümkündür.

- Aşağıdaki örnekte, bir set nesnesi oluşturulur ve insert() fonksiyonuyla birkaç eleman eklenir. Sonra find() fonksiyonu kullanılarak belirli bir elemanın set içinde olup olmadığı kontrol edilir:


```CPP
#include <iostream>
#include <set>

int main() {
    std::set<int> mySet;

    mySet.insert(10);
    mySet.insert(20);
    mySet.insert(30);

    auto it = mySet.find(20);

    if (it != mySet.end()) {
        std::cout << "Element found in set: " << *it << std::endl;
    } else {
        std::cout << "Element not found in set." << std::endl;
    }

    return 0;
}

```

- Bu örnekte, set nesnesi mySet adı altında oluşturulur ve içine 10, 20 ve 30 elemanları insert() fonksiyonu kullanılarak eklenir. Daha sonra find() fonksiyonu 20 değerini arar ve bu elemanın set içinde olup olmadığı kontrol edilir. find() fonksiyonu set içinde belirtilen değeri arar ve eğer değer bulunursa, değerin set içindeki konumunu temsil eden bir iterator döndürür. Bu örnekte, it değişkeni bu iterator ile ilgili bir nesnedir. Daha sonra, it değişkeni set'in sonunu göstermiyor ise (it != mySet.end()), elemanın set içinde bulunduğunu söyleyen bir mesaj yazdırılır. Aksi takdirde, eleman set içinde bulunmadığına dair bir mesaj yazdırılır.
- it değişkeni, aranan değerin set içinde olmaması durumunda set'in sonunu gösterir. Bu, aranan değerin set içinde olmadığı anlamına gelir. Ancak, bir önemli nokta, eğer set'in son elemanı aranan değere eşitse de yine it değişkeni set'in sonunu gösterir. Bu nedenle, it değişkeninin değerini kontrol etmek, aranan değerin set içinde olup olmadığını doğrulamak için yeterli değildir.

- Eğer son eleman aranan değere eşitse, std::set::find işlevi yine de son elemanın konumunu döndürecektir. Bu durumda, std::set::lower_bound işlevi kullanılabilir. std::set::lower_bound işlevi, verilen değerin eşleşmesi veya eşleşme durumunda sonraki en küçük değer için bir işaretçi döndürür.

- Örneğin, aşağıdaki kod bloğunda, 6 aranan değerdir ve son eleman da 6'dır. std::set::find işlevi son elemanın konumunu döndürür, bu yüzden it değişkeni s.end() ile eşleşir. Ancak std::set::lower_bound işlevi, aranan değerin sonraki en küçük değer için bir işaretçi döndürür, bu nedenle lb değişkeni son elemanın konumunu değil, sonraki en küçük değer olan ++it ile eşleşir.

```CPP
std::set<int> s = {1, 2, 3, 4, 5, 6};
auto it = s.find(6); // it == s.end()

auto lb = s.lower_bound(6); // lb == ++it

```
> Bu nedenle, arama sonucunda it == s.end() olup olmadığını kontrol etmek, aranan değerin set'te bulunup bulunmadığını doğrulamak için önemlidir.




























