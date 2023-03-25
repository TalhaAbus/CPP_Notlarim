# std::locale

- std::locale, C++ standart kütüphanesinde yer alan bir sınıftır ve yerel ayarlar (locale settings) ile ilgili bilgileri içerir. Yerel ayarlar, çeşitli özellikleri tanımlayan ve değişen bir sıralama, karakter çevirimi, tarih ve saat biçimi, para birimi, sayı biçimi gibi birçok kültürel özelliklerdir. std::locale sınıfı, bu yerel ayar bilgilerini tutar ve C++ girdi/çıktı işlemlerinde bu ayarları kullanarak karakterlerin kodlamasını, sıralamasını, tarih/saat biçimini vb. belirleyebilir.

- std::locale sınıfı, yerel ayarları bir std::locale::id nesnesi aracılığıyla tanımlar. Bir std::locale nesnesi oluşturulurken, belirli bir std::locale::id kullanarak yerel ayar bilgilerine erişilir. Yerel ayar bilgileri, std::locale::facet adı verilen alt sınıflar tarafından temsil edilir. Örneğin, std::collate, std::ctype, std::time_get, std::money_put vb. gibi alt sınıflar, sıralama, karakter çevirimi, tarih/saat biçimi, para birimi gibi yerel ayarlarla ilgili işlevler sağlarlar.

- Örneğin, aşağıdaki kodda std::locale sınıfı kullanılarak bir std::money_put nesnesi oluşturulur ve belirli bir yerel ayar kullanarak para birimleri formatlanır:

```CPP
#include <iostream>
#include <locale>
#include <string>

int main() {
  double money = 1234.56;
  std::string currency = "USD";
  std::locale loc("");
  const auto& money_put_facet = std::use_facet<std::money_put<char>>(loc);
  std::ostringstream oss;
  money_put_facet.put(oss, false, oss, ' ', currency.c_str(), money);
  std::cout << oss.str() << '\n';
  return 0;
}

```
> Bu kodda, std::locale sınıfı kullanılarak bir yerel ayar nesnesi oluşturulur. std::use_facet işlevi kullanılarak std::money_put tipinde bir alt sınıf nesnesi elde edilir. Bu alt sınıf, para birimi formatlaması yapmak için kullanılır. Daha sonra std::ostringstream sınıfı kullanılarak bir çıktı akımı oluşturulur ve std::money_put::put işlevi kullanılarak para birimi formatlaması yapılır. Sonuç olarak, çıktı şu şekilde olur:


```CPP
USD1,234.56

```

- Bu örnekte, std::money_put sınıfı, para birimi formatlaması yapmak için kullanılır. std::money_put sınıfı, para birim formatlaması ile ilgili bilgileri tutar ve para birimi simgesini, sayı biçimini ve diğer ayarları belirleyerek para birimi formatlaması yapar. std::money_put::put işlevi, önceki örnek kodda gösterildiği gibi, std::ostringstream sınıfı kullanarak bir çıktı akımı oluşturur ve para birimi formatlaması yapar.

- std::locale sınıfı, C++ girdi/çıktı işlemlerinde de kullanılabilir. Örneğin, std::cin ve std::cout akımları, varsayılan olarak "C" yerel ayarını kullanırlar. Ancak, std::locale sınıfı kullanılarak bu ayarlar değiştirilebilir. Aşağıdaki örnekte, bir std::locale nesnesi kullanılarak std::cin ve std::cout akımlarının yerel ayarları değiştirilir:

```CPP
#include <iostream>
#include <locale>

int main() {
  std::cout.imbue(std::locale("tr_TR.utf8"));
  std::cin.imbue(std::locale("tr_TR.utf8"));
  double d;
  std::cout << "Lütfen bir ondalık sayı girin: ";
  std::cin >> d;
  std::cout << "Girdiğiniz sayı: " << d << '\n';
  return 0;
}

```
- Bu örnekte, std::cout ve std::cin akımlarının yerel ayarları tr_TR.utf8 olarak değiştirilir. Bu ayar, Türkçe karakterleri destekler. Daha sonra, kullanıcıdan bir ondalık sayı girmesi istenir ve std::cin kullanılarak girilen sayı alınır. Son olarak, std::cout kullanılarak girilen sayı tekrar yazdırılır. Bu örnekte, yerel ayar değişikliği nedeniyle Türkçe karakterlerin kullanımı da mümkündür.

- Özetle, std::locale sınıfı, C++ programlarında yerel ayarlarla ilgili bilgileri tutar ve girdi/çıktı işlemlerinde bu ayarları kullanarak karakterlerin kodlamasını, sıralamasını, tarih/saat biçimini vb. belirleyebilir.
