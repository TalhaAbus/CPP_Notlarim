
# lambda Expressions

- Lambda ifadeleri, C++11 ile birlikte gelen bir özelliktir. Lambda ifadeleri, adlandırılmış fonksiyonlar yerine, yerel olarak tanımlanmış bir fonksiyon nesnesi oluşturmanıza olanak tanır. Bu fonksiyon nesnesi, programınızın çalışma zamanında kullanılabilir.

- Lambda ifadeleri, bir köşeli parantezden başlar ([) ve parantezlerle () bitirilir. Parantezlerin arasında, lambda ifadesinin parametreleri belirtilir. Bu parametreler, normal bir fonksiyondaki parametreler gibidir, yani bir tür ve bir ad içerir. Birden fazla parametre kullanmak isterseniz, bunları virgülle ayırın.

- Lambda ifadelerinin gövdesi, iki kısma ayrılır: lambda ifadesinin başlığından sonra köşeli parantezlerle [] belirtilen yakalama listesi ve süslü parantezler arasındaki kod bloğu. Yakalama listesi, lambda ifadesinin kod bloğunda kullanılacak değişkenleri ve referansları belirler.

- İşte basit bir lambda ifadesi örneği:

```CPP
#include <iostream>

int main() {
    int x = 10;
    int y = 20;

    // Lambda ifadesi oluşturma
    auto toplam = [](int a, int b) { return a + b; };

    // Lambda ifadesini kullanarak toplama işlemi yapma
    std::cout << "Toplam: " << toplam(x, y) << std::endl;

    return 0;
}

```


- Bu kodda, önce int x ve int y değişkenleri tanımlanır. Daha sonra, lambda ifadesi ile bir toplam fonksiyon nesnesi oluşturulur. Bu fonksiyon nesnesi, [] içinde belirtilen parametreleri alır (int a ve int b), ardından bu parametreleri toplayarak bir sonuç döndürür. Son olarak, toplam fonksiyon nesnesi kullanılarak x ve y değerleri toplanır ve sonuç yazdırılır.

- Lambda ifadeleri, C++ programlamada oldukça kullanışlı bir özelliktir. Özellikle, algoritma fonksiyonları gibi yerel olarak bir fonksiyon nesnesi gerektiren durumlarda lambda ifadeleri kullanılabilir. Ayrıca, lambda ifadeleri, C++11 ile birlikte gelen diğer özelliklerle birlikte kullanıldığında, kodun daha okunaklı ve daha kolay bakım yapılabilir hale gelmesine yardımcı olabilir.

# lambda ifadelerine ne den ihtiyac var

- Lambda ifadeleri, C++ programlamada bazı durumlarda oldukça kullanışlı bir özelliktir. Bazı durumlarda, adlandırılmış fonksiyonların kullanılması yerine lambda ifadeleri kullanmak daha pratiktir.

- Örneğin, STL algoritma fonksiyonları (std::sort, std::find, std::count_if, vb.) gibi yerel olarak bir fonksiyon nesnesi gerektiren durumlarda lambda ifadeleri kullanmak oldukça kullanışlıdır. Bu durumda, lambda ifadeleri, adlandırılmış bir fonksiyon tanımlamak yerine, kodun daha okunaklı ve daha kolay bakım yapılabilir hale gelmesine yardımcı olabilir.

- Ayrıca, lambda ifadeleri, C++11 ile birlikte gelen diğer özelliklerle birlikte kullanıldığında da oldukça kullanışlıdır. Örneğin, lambda ifadeleri, std::thread sınıfıyla birlikte kullanılarak çoklu iş parçacığı programlaması için kullanılabilir.

- Lambda ifadeleri ayrıca, C++ programlamada fonksiyonel programlama tekniklerinin kullanılmasına olanak tanır. Bu teknikler, kodun daha özlü ve daha yüksek seviyeli olmasını sağlar. Lambda ifadeleri, özellikle C++11'den önceki dönemlerde, fonksiyonel programlama tekniklerinin kullanılmasını kolaylaştırdı.

- Evet, lambda ifadeleri nihayetinde birer fonksiyondur ve birer fonksiyon nesnesi olarak kullanılır. Dolayısıyla, fonksiyonlar gibi giriş/çıkış maliyetleri vardır.

- Ancak, C++11 ile birlikte gelen özellikler sayesinde, lambda ifadeleri genellikle inline olarak işlenir. Bu, lambda ifadesinin çağrıldığı yerde kodun doğrudan yerleştirildiği anlamına gelir. Bu sayede, fonksiyon çağrısının getirdiği maliyetler azaltılır ve kod daha hızlı çalışır.

- Bununla birlikte, lambda ifadelerinin inline olarak işlenmesi, her zaman daha hızlı kod oluşturacağı anlamına gelmez. Çok büyük ve karmaşık lambda ifadeleri, kodun daha okunaklı ve daha bakım yapılabilir olması için ayrı bir fonksiyon olarak tanımlanabilir. Ancak, küçük ve basit lambda ifadeleri inline olarak işlenerek, kodun daha hızlı çalışmasına yardımcı olabilir.

- Özetle, lambda ifadeleri nihayetinde birer fonksiyondur ve birer fonksiyon nesnesi olarak kullanılır. Dolayısıyla, fonksiyonlar gibi giriş/çıkış maliyetleri vardır, ancak C++11 ile birlikte gelen özellikler sayesinde, inline olarak işlenerek, kodun daha hızlı çalışmasına yardımcı olabilir.
