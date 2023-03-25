- <typeindex> başlık dosyası, type_info nesnelerinin isimlerinin, türlerinin ve diğer özelliklerinin depolanmasına, karşılaştırılmasına ve kullanımına yönelik araçlar sağlar.

- typeindex sınıfı, bir type_info nesnesinin özelliklerini depolar ve karşılaştırma işlemleri için kullanılabilir. Ayrıca, type_info nesnelerine erişmek için kullanılan type_index türü ile değiştirilebilir.

- type_info sınıfı, tür bilgisini depolar ve çalışma zamanında tür bilgisini sorgulamak için kullanılır. type_info nesneleri, typeid operatörü kullanılarak elde edilir. Bu nesneler, RTTI (Run-Time Type Information) olarak bilinen bir mekanizma tarafından kullanılır ve özellikle kalıtım ilişkileri gibi tür bilgileri için kullanışlıdır.

- type_traits başlık dosyası ile birlikte kullanıldığında, typeindex sınıfı, özellikle türlerin özelliklerini kontrol etmek için yararlıdır. Örneğin, std::is_same tür özellikleri kontrolü için kullanılan bir typeindex sınıfı kullanır.

- Aşağıda typeindex sınıfının örnek kullanımlarını görebilirsiniz:

```CPP
#include <iostream>
#include <typeindex>
#include <typeinfo>

int main() {
    // typeid ile tür bilgisi elde edilir
    std::cout << typeid(int).name() << std::endl; // i

    // type_index nesnesi oluşturulur
    std::type_index ti1(typeid(int));
    std::type_index ti2(typeid(float));

    // iki type_index nesnesi karşılaştırılır
    if (ti1 == ti2) {
        std::cout << "Types are the same." << std::endl;
    } else {
        std::cout << "Types are different." << std::endl;
    }

    return 0;
}

``
- Bu örnekte, typeid ile int türünün type_info nesnesi alınır ve std::type_index nesnesi oluşturmak için kullanılır. Daha sonra, std::type_index nesneleri karşılaştırılır ve sonuç ekrana yazdırılır.

- Tabii, aşağıdaki örnekte type_index sınıfının kullanımı gösterilmiştir:

```CPP
#include <iostream>
#include <typeindex>
#include <unordered_map>

struct Base {
    virtual void foo() {}
};

struct Derived1 : public Base {
    void foo() override {}
};

struct Derived2 : public Base {
    void foo() override {}
};

int main() {
    std::unordered_map<std::type_index, int> typeMap;

    typeMap[std::type_index(typeid(Base))] = 1;
    typeMap[std::type_index(typeid(Derived1))] = 2;
    typeMap[std::type_index(typeid(Derived2))] = 3;

    std::cout << "Type of Base: " << typeMap[std::type_index(typeid(Base))] << '\n';
    std::cout << "Type of Derived1: " << typeMap[std::type_index(typeid(Derived1))] << '\n';
    std::cout << "Type of Derived2: " << typeMap[std::type_index(typeid(Derived2))] << '\n';

    return 0;
}

```
> Bu örnekte, type_index sınıfı, std::unordered_map'de depolanan ve bir türden bir değeri ilişkilendiren öğelerin anahtarları olarak kullanılmaktadır. Anahtarlar, std::type_index tipindeki türlerin örnekleri kullanılarak oluşturulur ve bir örnek, typeid operatörü kullanılarak alınabilir.



# type_index sinifi genellikle type_info ile birlikte mi kullanilir

- Evet, std::type_index genellikle std::type_info ile birlikte kullanılır. std::type_info nesnesi, bir C++ türünün tanımlayıcısını içerir ve tür tanımlayıcısı, tür adını içermez. std::type_index sınıfı ise türlerin RTTI bilgisinin bir bölümünü içerir ve std::type_info nesneleriyle ilişkilendirilmiş olan türlerin tür adlarını temsil eder. Yani, std::type_index tür adını elde etmek için kullanılabilir.

# type_index sinifini hangi senaryolarda kullanmaliyim

- type_index sınıfı, özellikle tür tanımlayıcılarının depolanması ve karşılaştırılması gerektiği durumlarda kullanışlıdır. Örneğin, türlerin dinamik olarak oluşturulması gereken kodlarda kullanılabilir. Type_index sınıfı, dinamik tür oluşturma veya kaynak kodunu çalışma zamanında inceleme gerektiren karmaşık kodlar için kullanışlıdır. Ayrıca, bir türü diğer bir türle karşılaştırmak veya bir map yapısı gibi bir veri yapısında türlerin anahtar olarak kullanılması gibi durumlarda da faydalıdır.
























































