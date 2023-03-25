- typeinfo başlık dosyası, C++ programlama dilinde tür bilgilerine erişim sağlayan std::type_info sınıfını tanımlar. Bu sınıfın temel amacı, çalışma zamanında nesnelerin türlerine erişim sağlamaktır.

- typeinfo başlık dosyası, C++'ta tür bilgisi hakkında bilgi toplama ve işleme işlevleri sağlar. Bu başlık dosyasındaki başlıca özellikler şunlardır:

- **typeid:** Bu operatör, verilen bir türün tür bilgisini döndürür. typeid operatörü, türün standard ismini veya bir demet ismini döndürebilir. Bu işlem yapılmadan önce, önceki bir nesnenin türünün veri türü hakkında bilgi edinmek için de kullanılabilir.

- **type_info:** Bu sınıf, tür bilgisi için bir öğe temsil eder. typeid operatörü tarafından döndürülen türün özelliklerini içerir. Bu sınıf aynı zamanda türler arasında karşılaştırma işlemlerini gerçekleştirmek için de kullanılabilir.

- **bad_cast:** Bu sınıf, tür dönüştürme işlemi sırasında bir dönüşümün yanlış olduğu durumlarda atılan bir istisna sınıfıdır. Bu durumlar, dynamic_cast operatörünün bir nesneyi farklı bir sınıf türüne dönüştürme girişiminde başarısız olduğu durumlardır.

- Bu başlık dosyasındaki özellikler genellikle dinamik tür bilgisiyle ilgili işlemlerde kullanılır. Özellikle, polimorfik sınıfların tanımlanması, nesne yönlendirmesi ve iskeleler gibi konularla ilgili çalışmalarda sıklıkla kullanılır.
  

- Özellikle, std::type_info sınıfı, typeid operatörünün dönüş değeri olarak kullanılır. typeid operatörü, bir nesnenin türü hakkında bilgi edinmek için kullanılır ve std::type_info sınıfının bir örneğini döndürür.

- Bunun yanı sıra, std::type_info sınıfı, birbirine eşit olmayan türlerin karşılaştırılmasını sağlar. iki std::type_info nesnesi == operatörü ile karşılaştırıldığında, aynı türden olanlar true döndürürken, farklı türler false döndürür.

- Özetle, typeinfo başlık dosyası, tür bilgilerine erişim sağlamak için kullanılan std::type_info sınıfını tanımlar.

- Örnek kullanım:

```CPP
#include <iostream>
#include <typeinfo>

int main() {
    int x = 5;
    std::cout << typeid(x).name() << std::endl;
    return 0;
}

```

- Bu program, x değişkeninin türünü typeid operatörü ile elde eder ve std::type_info::name() fonksiyonunu kullanarak tür ismini yazdırır.

- Bir değişkenin türünü typeinfo sınıfını kullanmadan da yazdırmak mümkündür ancak bu yöntem compile-time değil run-time'da çalışır. Bunun için öncelikle typeid operatörü kullanılarak değişkenin tipi runtime'da belirlenir ve daha sonra std::type_index sınıfı kullanılarak bu bilgi string olarak elde edilebilir. Örneğin:


```CPP
#include <iostream>
#include <string>
#include <typeindex>

int main() {
    int a = 5;
    std::type_index type = typeid(a);
    std::cout << type.name() << std::endl;

    return 0;
}

```
- Bu örnekte typeid operatörü ile a değişkeninin türü belirlenmiş ve std::type_index sınıfı kullanılarak bu türün adı string olarak ekrana yazdırılmıştır. Ancak bu yöntem typeid operatörünün oluşturduğu run-time maliyeti nedeniyle tercih edilen bir yöntem değildir.
- Sadece iostream başlık dosyasını kullanarak bir değişkenin türünü yazdıramayız. Değişkenin türüne erişmek için tip bilgisi gereklidir ve C++'ta tip bilgisi run-time'da elde edilemez. Bu nedenle, tip bilgisine erişmek için tipin typeid() işleviyle alınması gerekmektedir, bu işlevin başlığı ise <typeinfo> başlık dosyasında yer almaktadır.























