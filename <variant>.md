- <variant> başlık dosyası, C++17 standartlarına dahil edilmiştir. Bu başlık dosyası, C++ dilinde değişken sayıda veri türleri üzerinde çalışmayı mümkün kılan bir şablon sınıf olan std::variant sınıfını içerir.

- std::variant, özellikle belirli bir noktada farklı veri türlerinin kullanılması gereken, ancak her bir veri türü için ayrı bir değişken tanımlamak istemediğiniz durumlarda faydalıdır. Örneğin, bir XML dosyasındaki bir etiketdeki metni veya bir sayıyı temsil etmek için aynı değişkeni kullanabilirsiniz.

- std::variant sınıfı, içinde saklanan değerin türünü takip eden bir etiketle işaretlenmiş birliktelik yapısıdır. std::variant nesnesi, değerini birkaç farklı veri türünden birinde saklar ve bu veri türleri sabit olarak tanımlanır. Bu, std::variant nesnesinin sadece bir veri türüne sahip olduğu anlamına gelir, ancak bu veri türü farklı olabilir.

- std::variant sınıfı, alternatiflerin dizisine erişmek için C++'daki std::tuple sınıfına benzer bir arabirim sağlar.

- Aşağıda std::variant'ın bazı örnek kullanımları gösterilmiştir:

```CPP
// std::variant kullanımı

#include <variant>
#include <iostream>
#include <string>

int main()
{
    std::variant<int, double, std::string> v1, v2, v3;

    v1 = 42; // int tipi olarak atanır
    v2 = 3.14; // double tipi olarak atanır
    v3 = "Hello, World!"; // std::string tipi olarak atanır

    // Değerlerin türlerini sorgulama
    if (v1.index() == 0) {
        std::cout << "v1 contains an int with value " << std::get<0>(v1) << '\n';
    }

    if (v2.index() == 1) {
        std::cout << "v2 contains a double with value " << std::get<1>(v2) << '\n';
    }

    if (v3.index() == 2) {
        std::cout << "v3 contains a string with value " << std::get<2>(v3) << '\n';
    }

    // Farklı türlerdeki değerlere erişme
    std::get<int>(v1) = 13; // int tipi olarak atanır
    std::get<double>(v2) = 2.718; // double tipi olarak atanır
    std::get<std::string>(v3) = "Goodbye, World!"; // std::string tipi olarak atanır

    // Değerlerin türlerini sorgulama
    if (v1.index() == 0) {
        std::cout << "v1 contains an int with

```

# neden tuple yerine variant kullanmaliyim

- tuple ve variant sınıfları farklı amaçlar için tasarlanmışlardır. tuple, farklı türlerden elemanların bir araya getirilmesi için kullanılırken, variant tek bir değişkenin farklı türlerdeki değerleri alabilmesini sağlamak için kullanılır.

- Örneğin, bir fonksiyonun farklı türlerden argümanlarla çağrılabilmesi için variant kullanabilirsiniz. Variant, C++17 öncesindeki union yapısının geliştirilmiş bir versiyonudur ve union yapısının yetersiz kalan birçok özelliğini giderir.

- Bu nedenle, tuple ve variant sınıflarını farklı amaçlar için kullanmanız gerekir. Eğer farklı türlerden elemanlarınızı bir araya getirmeniz gerekiyorsa tuple kullanabilirsiniz. Eğer ise bir değişkenin farklı türlerdeki değerlerini saklamak istiyorsanız variant kullanabilirsiniz.

====================

- bir örnek üzerinden anlatmaya çalışayım.

- Elimizde bir araba yarışı uygulaması olsun ve bu uygulamada farklı tiplerde araçlarımız olsun. Bu araçlar farklı özelliklere sahip olabilirler, örneğin bazıları hızlı ama sağlam değillerdir, bazıları ise dayanıklı ama yavaştırlar. Bu durumda, farklı araçların özelliklerini tek bir nesnede toplayabileceğimiz bir veri tipine ihtiyacımız var.

- Bu noktada, tuple yerine variant kullanabiliriz. Örneğin, aşağıdaki gibi bir variant tanımlayabiliriz:

```CPP
#include <variant>
#include <iostream>
#include <string>

using namespace std;

struct FastCar {
    int topSpeed;
};

struct DurableCar {
    int durability;
};

struct BalancedCar {
    int topSpeed;
    int durability;
};

int main() {
    variant<FastCar, DurableCar, BalancedCar> car;

    car = FastCar{250};
    cout << "Top speed: " << get<FastCar>(car).topSpeed << endl;

    car = DurableCar{100};
    cout << "Durability: " << get<DurableCar>(car).durability << endl;

    car = BalancedCar{200, 50};
    cout << "Top speed: " << get<BalancedCar>(car).topSpeed << endl;
    cout << "Durability: " << get<BalancedCar>(car).durability << endl;

    return 0;
}

```

> Burada, variant içinde FastCar, DurableCar ve BalancedCar tiplerini kullanarak, farklı araçların özelliklerini tek bir nesnede topladık. Daha sonra, variant'ı istediğimiz şekilde değiştirip, get fonksiyonunu kullanarak variant içindeki nesnenin özelliklerine erişebiliriz.

- Variant kullanmanın tuple'a göre avantajı, her bir tipin farklı bir özelliği temsil etmesi ve bunların bir arada kullanılabilecek olmasıdır. Ayrıca, variant'ın kullanımı daha okunaklı ve anlaşılırdır. Dezavantajı ise, daha fazla bellek kullanımı ve performans kaybıdır.

- variant kullanımı performans kaybına neden olmaz. Ancak, variant kullanırken dikkat edilmesi gereken bazı hususlar vardır. Örneğin, variant'a farklı tipler eklenirken, tüm tiplerin aynı hafıza boyutuna sahip olması gerekir. Ayrıca, variant kullanılırken her zaman tüm tiplerin kullanılacağından emin olunmalıdır. Bu, variant'ın gereksiz yere şişmesine neden olabilir ve bu da performans kaybına yol açabilir.

- variant, tip güvenliği açısından yararlıdır ve birden fazla türün bulunduğu bir senaryoda, türler arasında kolayca geçiş yapmayı sağlar. Ancak, eğer bir senaryoda tek bir tür kullanılıyorsa, variant kullanımı gereksiz olabilir ve kodu daha karmaşık hale getirebilir.




























