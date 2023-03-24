- array başlık dosyası, C++11 standartlarıyla birlikte standart kütüphaneye eklenmiştir. Bu başlık dosyası, boyutu sabit olan diziler için bir veri türü sunar. Dizi boyutu, dizi nesnesi oluşturulurken belirtilir ve değiştirilemez.

std::array sınıfı, sabit boyutlu dizileri yönetmek için kullanılır. Bir std::array nesnesi, C++ dilindeki normal diziler gibi davranır, ancak bazı ek özellikler sunar. std::array sınıfı, normal dizilerin aksine bir geçici nesne olarak değil, bir değer olarak geçirilebilir ve fonksiyonlardan geri döndürülebilir.

std::array sınıfı, C-style dizilerin çoğu dezavantajını giderir. Dizinin boyutu, dizi nesnesi oluşturulurken belirtilir ve çalışma zamanında değiştirilemez. Bu nedenle, std::array sınıfı kullanarak, dizi boyutuna ilişkin hataların önüne geçilebilir.

Ayrıca, std::array sınıfı, diğer standart kütüphane sınıfları ile birlikte kullanılabilecek birçok fonksiyon ve özellik sağlar. Örneğin, std::array nesneleri, sıralama ve arama gibi işlemler için std::algorithm sınıfındaki fonksiyonlarla birlikte kullanılabilir.

std::array sınıfı, kullanımı kolaydır ve temel bir veri türü olarak düşünülebilir. Örneğin, aşağıdaki kodda, std::array nesnesi arr oluşturulmuştur ve ardından for döngüsü kullanılarak dizinin elemanları yazdırılmıştır:

```CPP
#include <iostream>
#include <array>

int main() {
    std::array<int, 5> arr = {1, 2, 3, 4, 5};

    for (int i = 0; i < arr.size(); i++) {
        std::cout << arr[i] << " ";
    }

    return 0;
}

```

- Bu kod, 1 2 3 4 5 çıktısını verir.

- std::array sınıfının bir başka özelliği, dizi elemanlarını atama veya karşılaştırma gibi işlemler için kullanılabilecek bir dizi operatör sağlamasıdır. Örneğin, aşağıdaki kodda, std::array nesneleri arr1 ve arr2 oluşturulmuş ve ardından bu nesnelerin elemanları karşılaştırılmıştır:

```CPP
#include <iostream>
#include <array>

int main() {
    std::array<int, 3> arr1 = {1, 2, 3};
    std::array<int, 3> arr2

```

# std::array ile neler yapabiliriz? Ne zaman kullanmalıyım?

- std::array sınıfı, sabit boyutlu bir dizi veriyi yönetmek için kullanılır. std::array sınıfı C dizilerine benzer, ancak birçok farklılıkları vardır. std::array, boyutu derleme zamanında bilinen bir dizi verisi için daha güvenli bir alternatiftir. C dizilerine göre birçok avantajı vardır, örneğin:

- **Sınıf yapısı nedeniyle, std::array ile C dizilerindeki gibi bellek sınırlarını aşmak mümkün değildir.**
- **Dizinin boyutu bilindiğinden, std::array'nin elemanlarına doğrudan erişebilirsiniz. Elemanları doğrudan erişebilmek, C dizilerindeki gibi bir dizide gezinmekten daha hızlı ve verimlidir.**
- **std::array sınıfı, C dizilerindeki gibi pointer aritmetiği kullanılmaz, bu nedenle hatalı dizinlere erişme riski yoktur.**
- **std::array sınıfı, C dizilerine göre daha kolay okunabilir ve daha özgüvenle kullanılabilir. Ayrıca, standart kütüphanenin diğer bileşenleriyle birlikte daha uyumlu çalışır.**
- std::array kullanımı özellikle boyutu sabit olan diziler için uygundur. Örneğin, sabit boyutlu matrisler, önceden belirlenmiş sütun ve satırlarla belirli bir boyuta sahip vektörler veya bir histogramda sayılan öğe sayısı gibi durumlarda kullanılabilir.**

- std::array sınıfının, dizi elemanlarına erişme, sıralama, arama, toplama ve benzeri işlemleri yapabilen bir dizi fonksiyonu vardır. Ayrıca, C++11'de eklenen özellikler olan begin() ve end() fonksiyonları sayesinde, C++11 öncesi sürümlerdeki C++ kodlarında bulunan for döngüleri gibi yerlerde de kullanılabilir.

# Ben neden std::vector yerine std::array kullanayım?

- std::vector ve std::array farklı yapılar olduğu için, hangisinin kullanılacağına karar vermek ihtiyaca göre değişir.

- std::array'ler statik bir boyuta sahipken, std::vector'ler dinamik olarak boyutlandırılabilirler. Yani, eğer sabit bir boyutlu bir veri kümesine ihtiyacınız varsa, std::array kullanmak uygun olabilir. Ancak, eğer veri kümeniz değişken bir boyuta sahip olacaksa, o zaman std::vector kullanmak daha uygun olacaktır.

- std::array'in avantajları arasında, boyutunun sabit olması nedeniyle, bellekte daha küçük bir ayak izi ve daha hızlı erişim zamanı bulunurken, std::vector'un boyutu dinamik olduğundan, daha esnek bir yapıya sahiptir ve dinamik olarak boyutlandırılabilir.

- Özetle, sabit bir boyuta sahip veri kümesi için std::array kullanmak daha uygunken, değişken bir boyuta sahip veri kümesi için std::vector kullanmak daha uygun olabilir.

# sabit boyutlu bir dizide std::vector kullandığımız zaman verimsiz bir kod yazmış mı oluruz çünkü dinamik bellek yömnetimi devreye giriyor

- Evet, doğru bir değerlendirme. Sabit boyutlu bir dizide std::vector kullanmak, gereksiz bir dinamik bellek yönetimi işlemi olduğu için verimsiz bir kod yazmış olabilirsiniz. Sabit boyutlu bir dizi için std::array kullanmak, bellek yönetimini daha verimli bir şekilde yapmanıza olanak tanır. Ayrıca, std::array'ın boyutu, derleme zamanında sabit olduğu için çalışma zamanında bellek boyutunu değiştirmeniz mümkün değildir. Bu nedenle, eğer sabit boyutlu bir diziye ihtiyacınız varsa, std::array'ı tercih etmek daha uygun olacaktır.










































