# forward_list

- <forward_list> başlık dosyası, tek yönlü bağlı liste olarak adlandırılan bir veri yapısını sağlayan sınıf şablonu std::forward_list'i tanımlar.

- std::forward_list, std::list'in tek yönlü bir sürümüdür. Tek yönlü bağlı liste, her elemanın sadece bir sonraki elemanını bilen bir liste türüdür. Bu özellik, bir öğenin listeye eklendiğinde, sadece bir sonraki öğenin adresi ayarlanır ve önceki öğenin adresi saklanmaz. Bu nedenle, std::forward_list daha hafif ve daha az yer kaplayan bir liste türüdür ve belirli bir senaryoda tercih edilebilir.

# Member Functions

- **before_begin()**
- **begin()**
- **end()**
- **cbefore_begin()**
- **cbegin()**
- **cend()**
- **empty()**
- **max_size()**
- **front()**
- **assign()**
- **emplace_front()**
- **push_front()**
- **pop_front()**
- **emplace_after()**
- **insert_after()**
- **erase_after()**
- **swap()**
- **resize()**
- **clear()**
- **splice_after()**
- **remove()**
- **remove_if()**
- **unique()**
- **merge()**
- **sort()**
- **reverse()**
- **get_allocator()**




























# Diğer Örnekler

- Örnek olarak, std::forward_list kullanarak bir sayı listesi oluşturabiliriz ve listenin elemanlarını yazdırabiliriz:

```CPP
#include <iostream>
#include <forward_list>

int main() {
  std::forward_list<int> list = {1, 2, 3, 4, 5};
  
  for (auto it = list.begin(); it != list.end(); ++it) {
    std::cout << *it << " ";
  }
  
  return 0;
}

```
> Bu kod, std::forward_list sınıfını kullanarak bir sayı listesi oluşturur ve listenin elemanlarını yazdırır.


# forward_list ve list arasında ne fark var

- std::forward_list ve std::list her ikisi de C++ standart kütüphanesi içinde bulunan veri yapılarıdır ve her ikisi de verileri düğümler (node) olarak saklarlar. Ancak iki veri yapısının arasında farklılıklar vardır.

- std::forward_list (C++11'den itibaren) tek yönlü bir bağlı liste (singly linked list) veri yapısıdır. Bu, her bir düğümün sadece bir sonraki düğüme bir referans içermesi anlamına gelir. Bu nedenle, liste sonuna doğru gezinmek istiyorsanız, her zaman listenin başından başlamak ve her bir düğüme sırayla erişmek zorundasınız. Bu, listenin başına veya ortasına bir düğüm eklemek veya düğüm silmek için çok hızlı olmasını sağlar, ancak listenin sonuna erişim maliyeti yüksektir.

- std::list, çift yönlü bir bağlı liste (doubly linked list) veri yapısıdır. Bu, her bir düğümün bir sonraki ve bir önceki düğüme referans içermesi anlamına gelir. Bu nedenle, herhangi bir yönde (baştan veya sondan) gezinebilirsiniz. Bu, herhangi bir düğüm eklemek veya silmek için diğer listelere göre daha yavaş olmasına rağmen, listenin herhangi bir yerindeki bir düğümü hızlı bir şekilde erişmenizi sağlar.

- Özetle, eğer listenin sonuna erişim maliyeti yüksekse ve listeye sık sık ekleme veya çıkarma işlemleri yapıyorsanız, std::forward_list tercih edebilirsiniz. Ancak, listeyi tersten gezmek veya sık sık bir düğümü erişmek isterseniz, std::list daha uygun olabilir.

# hangi senaryolarda list yerine forward_list tercih etmeliyiz ve bu tercihin verim açısından bir faydası var mıdır?

- forward_list, veri yapısında elemanları tek yönlü olarak sıralı şekilde tutan bir sınıftır. list sınıfı ise elemanları iki yönlü olarak sıralı şekilde tutar. Dolayısıyla forward_list'in sadece bir sonraki elemana erişim sağlayabilmesi ve geri dönüş yapamaması, list sınıfından daha az esnek bir veri yapısına sahip olduğu anlamına gelir.

- Bununla birlikte, forward_list'in daha düşük bellek tüketimi sağladığı durumlar vardır. Özellikle, sadece tek yönlü iterasyonların kullanıldığı veya sadece son elemana erişimin gerektiği durumlarda forward_list daha verimli olabilir. list sınıfı ise elemanlara her iki yönde de erişim sağlayabildiği için, özellikle elemanların sıklıkla ekleme veya silme işlemlerine tabi tutulduğu durumlarda daha uygun olabilir.

- Sonuç olarak, hangi sınıfın kullanılacağı, uygulamanın gereksinimlerine ve kullanım senaryosuna bağlıdır. Verim açısından bir fark, kullanım senaryosuna bağlı olarak oluşabilir.

# forward_lsit ve list verileri bellekte sıralı olarak mı tutar?

- list ve forward_list sınıfları, elemanlarını tutmak için dinamik bellek kullanır ve bu elemanları yalnızca bellekten tahsis edilen alanın adresleriyle birbirlerine bağlarlar. Bu nedenle, elemanlar bellekte sıralı olarak tutulmazlar. list sınıfı elemanları çift yönlü bağlantılı bir liste şeklinde tutar, forward_list sınıfı ise elemanları tek yönlü bağlantılı bir liste şeklinde tutar.

# Bağlı liste nedir nasıl çalışır? List ve forward_list bağlı liste midir?

- Bağlı liste, verilerin düğümler adı verilen bağlı bir listeyle depolandığı bir veri yapısıdır. Her düğüm, veriyi ve bir sonraki düğümün konumunu içeren bir yapıya sahiptir.

- List ve forward_list C++'ta bağlı liste veri yapısını uygulamak için kullanılan standart kütüphane sınıflarıdır. Hem list hem de forward_list sınıfları, verileri düğümlerle depolayarak bağlı liste yapısını uygularlar. Farkları, list sınıfının çift yönlü bir bağlı liste yapısı oluşturması, forward_list sınıfının ise tek yönlü bir bağlı liste yapısı oluşturmasıdır. Yani list sınıfında her düğümün hem bir sonraki hem de bir önceki düğümü gösteren işaretçileri vardır, forward_list sınıfında ise sadece bir sonraki düğümü gösteren bir işaretçe vardır.

- Bağlı liste yapısı, verileri rastgele bir sırayla depolamak yerine verilerin eklenme ve çıkarılma sırasına göre düzenlenmesine izin verir. Bu nedenle, verilerin sık sık eklenip çıkarılması gerektiği durumlarda bağlı liste yapısı tercih edilebilir. Ayrıca, herhangi bir yerden veri ekleme veya çıkarma işlemi yapılabilmesi de bağlı liste yapısının esnekliğini artırır. Ancak, verilere erişim işlemi için bir döngü kullanılması gerektiğinden bağlı liste yapısı, verilere rastgele erişim gerektiren işlemlerde daha yavaş çalışabilir.

# list'te her nesne önceki ve sonraki nesnenin adresini mi tutar?

- Evet, std::list'te her nesne (düğüm) önceki ve sonraki düğümün adreslerini tutar. Bu şekilde, düğümler bağlı bir liste oluştururlar. Bu sayede, std::list'in herhangi bir noktasında veri ekleme veya silme işlemi oldukça verimlidir.

# yani bağlı listerlerde listenin herhangi bir yerine bir nesne ekleyip çıkartabilir miyim? Bu işlemi yapmak için en verimli araçlar bağlı listeler midir? Örneğin vector ile bir listeye erişip bir nesne eklersem daha mı verimsiz olur?

- Evet, bağlı listelerde listenin herhangi bir yerine bir nesne eklemek veya çıkarmak mümkündür. Bağlı listeler, bu tür işlemleri gerçekleştirmek için en verimli veri yapılarından biridir çünkü herhangi bir nesnenin eklenmesi veya çıkarılması sadece ilgili düğümlerin (node) adreslerinin güncellenmesini gerektirir.

- Öte yandan, vector sınıfı, elemanların bellek üzerinde ardışık olarak saklandığı bir veri yapısıdır. Bu nedenle, vector sınıfı, belirli bir indekse eleman eklenmesi veya çıkarılması gerektiğinde, bu işlem için tüm elemanların kaydırılması gerektiğinden, bağlı listelere göre daha yavaş olabilir. Ancak, eklenen veya çıkarılan elemanların sıklığına ve vektörün boyutuna bağlı olarak, performans farkı önemsiz olabilir.

- Bu nedenle, ekleme veya çıkarma işlemlerinin çok sık gerçekleştirildiği durumlarda bağlı liste, performansın daha iyi olması nedeniyle tercih edilebilir. Ancak, elemanların sıklıkla erişilmesi ve aranması gerektiği durumlarda vector daha verimli olabilir.





















































