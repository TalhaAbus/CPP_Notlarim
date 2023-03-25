- <compare> başlık dosyası, karşılaştırma işlemleri için üç yöntem sağlar: strong_order, weak_order ve partial_order. Bu yöntemlerin her biri, karşılaştırılan nesnelerin sıralanabilirliği durumunda geri döndürülecek sonucu belirler.

- Bu başlık dosyasındaki en önemli sınıf std::compare_three_way'dir. Bu sınıf, üç yönteme dayalı olarak karşılaştırma işlemini gerçekleştirir. Karşılaştırılan nesnelerin sıralanabilirliğine göre std::strong_ordering, std::weak_ordering veya std::partial_ordering değerlerinden birini döndürür. Bu değerler std::strong_ordering'in en büyük, std::weak_ordering'in orta büyüklükte ve std::partial_ordering'in en küçük olduğu bir tam sayı sıralaması ile ilişkilendirilebilir.

- std::compare_three_way sınıfı, bir nesne türü için karşılaştırma işlemlerini sağlamak üzere C++20'de tanıtılmıştır ve bu işlem, algoritma kütüphanesi gibi diğer standart C++ kütüphaneleri tarafından kullanılabilir hale gelmiştir.

- <compare> başlık dosyası, farklı türlerin karşılaştırılması için kullanılan üç yöntemi içerir: strong ordering, partial ordering ve weak ordering.

- **Strong ordering:** İki değer arasında kesin bir sıralama vardır. Örneğin, sayılar arasında sıralama yapmak için kullanılabilir.

- **Partial ordering:** İki değer arasında kısmi bir sıralama vardır. Bu, tamsayılar veya kayan noktalı sayılar gibi sıralanamayan türler için kullanılabilir.

- **Weak ordering:** İki değer arasında bir sıralama olmaması gereken durumlarda kullanılır. Örneğin, eşitlik durumları için kullanılabilir.

- Bu üç yöntem, karşılaştırma işleminin sonucuna göre bir std::strong_ordering, std::partial_ordering veya std::weak_ordering nesnesi döndürür. Bu nesneler, sıralama işlemini tamamlamak için kullanılabilir.

- Bu başlık dosyası, bu karşılaştırma işlemlerini gerçekleştirmek için std::compare_three_way fonksiyonunu sağlar. Bu fonksiyon, operator<=>'nin kullanılması ile benzer bir işlev görür. Ancak, std::compare_three_way işlevi, tüm sıralama yöntemlerini desteklediğinden daha esnek bir çözüm sunar.

- Örneğin, aşağıdaki kodda std::compare_three_way fonksiyonu kullanılarak iki tamsayının sıralaması yapılır:

```CPP
#include <compare>
#include <iostream>

int main() {
    int a = 10, b = 20;
    auto result = std::compare_three_way(a, b);
    if (result == std::strong_ordering::less) {
        std::cout << "a < b" << std::endl;
    } else if (result == std::strong_ordering::greater) {
        std::cout << "a > b" << std::endl;
    } else {
        std::cout << "a == b" << std::endl;
    }
    return 0;
}

```

- Bu kodda, std::compare_three_way işlevi, a ve b değişkenlerini karşılaştırarak bir std::strong_ordering nesnesi döndürür. Bu nesne, karşılaştırma sonucuna göre std::strong_ordering::less, std::strong_ordering::greater veya std::strong_ordering::equal olabilir.

**Tablo sıralama işlemi için compare kullanımı örneği:**

```CPP
#include <iostream>
#include <vector>
#include <algorithm>
#include <compare>

struct Person {
    std::string name;
    int age;
};

bool operator<(const Person& lhs, const Person& rhs) {
    return std::compare_three_way(lhs.age, rhs.age) == -1;
}

int main() {
    std::vector<Person> persons{
        {"Ali", 28},
        {"Ahmet", 25},
        {"Ayşe", 31},
        {"Fatma", 22}
    };

    std::sort(persons.begin(), persons.end());

    for (const auto& person : persons) {
        std::cout << person.name << " - " << person.age << "\n";
    }
}

```

- Burada Person struct'ı için kendi < operator'ünü overload ediyoruz ve onun yerine std::compare_three_way kullanarak üçlü karşılaştırma yaparak kodu daha güvenli ve okunaklı hale getiriyoruz. Kodda std::sort ile Person vektörünü sıralıyoruz ve sonuçları ekrana yazdırıyoruz.



















