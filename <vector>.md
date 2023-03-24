- vector başlık dosyası, C++ dilindeki dinamik dizi yapısını sağlayan std::vector sınıfını içerir. std::vector, bellek yönetimi ile ilgilenmek zorunda kalmadan, dizilerle benzer işlevsellik sunar.

- std::vector, C++11 sürümünden sonra standart kütüphanede tanımlanmıştır ve C++ programlama dilinin önemli bir parçasıdır. Genellikle, birçok elemanın depolanması ve dinamik olarak genişletilebilmesi gereken durumlarda kullanılır.

- std::vector, birçok işlevsellik sağlar. Örneğin:

- Dizi elemanlarına erişim sağlar.
- Dizideki elemanları ekleme ve çıkarma işlemleri yapar.
- Diziyi sıralama ve tersine çevirme işlemleri yapar.
- Dizinin boyutunu değiştirme işlemleri yapar.
- Dizideki elemanları arama işlemleri yapar.
- std::vector sınıfı, STL (Standard Template Library) içinde yer alan bir sınıftır. STL, birçok farklı C++ sınıfının bir koleksiyonudur ve C++ programlamacılarına farklı veri yapıları sağlar.

- std::vector sınıfının kullanımı oldukça basittir. Örneğin, aşağıdaki gibi bir örnek kodla, std::vector sınıfını kullanarak bir dizi oluşturabilirsiniz:

```CPP
#include <iostream>
#include <vector>

int main() {
    // Int tipinde bir vector oluşturuluyor
    std::vector<int> myVector;

    // Vector'e elemanlar ekleniyor
    myVector.push_back(10);
    myVector.push_back(20);
    myVector.push_back(30);

    // Vector'ün boyutu
    std::cout << "Vector'un boyutu: " << myVector.size() << std::endl;

    // Vector'ün elemanları yazdırılıyor
    std::cout << "Vector'un elemanları: ";
    for (int i = 0; i < myVector.size(); i++) {
        std::cout << myVector[i] << " ";
    }
    std::cout << std::endl;

    return 0;
}

```

- Bu örnekte, std::vector sınıfı kullanılarak bir myVector adlı bir vector oluşturulur. push_back() fonksiyonu kullanılarak vector'e elemanlar eklenir. Vector'ün boyutu size() fonksiyonu kullanılarak elde edilir. Vector'ün elemanları, döngü kullanılarak myVector[i] şeklinde erişilerek yazdırılır.

- std::vector sınıfının avantajları arasında, bellek yönetimi işlemlerinin otomatik olarak gerçekleştirilmesi ve hızlı erişim özelliği sayılabilir. 

- std::vector, C++'ta dinamik boyutlu dizileri tutmak için kullanılan bir sınıftır. Dinamik boyutlu diziler, boyutu çalışma zamanında değiştirilebilen dizilerdir. Bu özellikleri nedeniyle, std::vector, statik olarak boyutlandırılmış dizilere kıyasla daha esnek bir veri yapısıdır.

- std::vector sınıfının özellikleri arasında aşağıdakiler yer alır:

- **Dizinin boyutu dinamik olarak değiştirilebilir.**
- Bellek dinamik olarak yönetilir, yani gereksiz bellek kullanımı en aza indirilir.
- Diziler, sadece aynı veri türüne sahip öğeleri içerebilir.
- Öğelere rasgele erişim sağlanabilir. Bu, dizinin bir öğesine doğrudan erişmek için dizin kullanılabileceği anlamına gelir.
- Diziler, aralıkların yanı sıra diğer vektörlerle birleştirilebilir ve böylece yeni vektörler oluşturulabilir.
- Bazı standart işlevler, örneğin sıralama, ters çevirme ve karıştırma işlemleri gibi işlemler, kolayca gerçekleştirilebilir.
- u özellikler, std::vector'ün geniş bir kullanım alanı olduğu anlamına gelir. Özellikle, dinamik olarak boyutlandırılmış diziler gerektiren birçok uygulama, std::vector'ü kullanır.

- Tabii, aşağıda vector sınıfının kullanımına dair örnekler verilmiştir:

- Örnek 1: vector oluşturma ve eleman ekleme

```CPP
#include <iostream>
#include <vector>

int main() {
    std::vector<int> vec; // boş bir vector oluşturuldu

    // vector'e elemanlar eklendi
    vec.push_back(1);
    vec.push_back(2);
    vec.push_back(3);

    // vector'ün elemanları ekrana yazdırıldı
    for (int i = 0; i < vec.size(); i++) {
        std::cout << vec[i] << " ";
    }

    return 0;
}

```

- Örnek 2: vector'ün boyutunu değiştirme

```CPP
#include <iostream>
#include <vector>

int main() {
    std::vector<int> vec = {1, 2, 3}; // elemanları olan bir vector oluşturuldu

    std::cout << "Vec'in boyutu: " << vec.size() << std::endl; // boyutu 3

    vec.resize(5); // boyutu 5 yapıldı

    std::cout << "Vec'in boyutu: " << vec.size() << std::endl; // boyutu 5

    vec.resize(2); // boyutu 2 yapıldı

    std::cout << "Vec'in boyutu: " << vec.size() << std::endl; // boyutu 2

    // vector'ün elemanları ekrana yazdırıldı
    for (int i = 0; i < vec.size(); i++) {
        std::cout << vec[i] << " ";
    }

    return 0;
}

```

- Örnek 3: vector'ün clear fonksiyonu ile içeriğini boşaltma

```CPP
#include <iostream>
#include <vector>

int main() {
    std::vector<int> vec = {1, 2, 3}; // elemanları olan bir vector oluşturuldu

    std::cout << "Vec'in boyutu: " << vec.size() << std::endl; // boyutu 3

    vec.clear(); // vector'ün içeriği boşaltıldı

    std::cout << "Vec'in boyutu: " << vec.size() << std::endl; // boyutu 0

    return 0;
}

```

**Tabii, örneğin şu şekilde bir vector tanımlayalım:**

```CPP
#include <iostream>
#include <vector>

int main() {
    std::vector<int> v = {10, 20, 30, 40, 50};
    
    // Dizi elemanlarına erişme
    std::cout << "v[0]: " << v[0] << std::endl; // 10
    std::cout << "v[3]: " << v[3] << std::endl; // 40
    
    // Eleman arama
    int x = 30;
    auto it = std::find(v.begin(), v.end(), x);
    if (it != v.end()) {
        std::cout << "Eleman bulundu: " << *it << std::endl; // 30
    } else {
        std::cout << "Eleman bulunamadi" << std::endl;
    }
    
    return 0;
}

```

- Bu örnekte, v adlı vector'ün 0'ıncı ve 3'üncü elemanlarına erişmek için v[0] ve v[3] kullanıldı. Eleman arama işlemi için ise std::find() algoritması kullanıldı ve eğer eleman bulunursa bu elemanın değeri ekrana yazdırıldı.
- 




























