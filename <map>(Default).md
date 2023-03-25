# std::map

- std::map, C++ standart kütüphanesinde bulunan bir ilişkisel veri yapısıdır. std::map bir anahtar-değer çiftleri koleksiyonudur ve anahtarlar benzersizdir. Bu özellik, std::map'i bir anahtarın değerini hızlı bir şekilde aramak için kullanışlı hale getirir.

- std::map veri yapısı, kırmızı-siyah ağaçlar kullanılarak gerçekleştirilir. Bu nedenle, std::map'in performansı, en kötü durumda bile logaritmiktir ve arama, ekleme ve silme işlemleri için O(log n) zaman karmaşıklığına sahiptir. Ancak, bu performans avantajı, std::map'in bir anahtar-değer çiftleri koleksiyonu olarak kullanılmasının yanı sıra, bir sıralı liste gibi de kullanılabileceği anlamına gelir.

- std::map sınıfı, std::pair sınıfından oluşan bir anahtar-değer çiftleri koleksiyonu tutar. Anahtar-değer çiftleri, std::pair sınıfından türetilen std::map::value_type sınıfı ile temsil edilir. std::map sınıfı, bir anahtarın değerine hızlı bir şekilde erişmek için std::map::find işlevini sağlar. std::map ayrıca, std::map::insert işlevi kullanılarak yeni anahtar-değer çiftleri eklemek için de kullanılabilir.

- Aşağıdaki örnek, std::map kullanarak bir kelimenin sayısını hesaplar:

```CPP
#include <iostream>
#include <map>
#include <string>
#include <algorithm>
#include <cctype>

int main() {
  std::map<std::string, int> word_counts;
  std::string word;
  while (std::cin >> word) {
    std::transform(word.begin(), word.end(), word.begin(),
                   [](unsigned char c) { return std::tolower(c); });
    ++word_counts[word];
  }
  for (const auto& p : word_counts) {
    std::cout << p.first << ": " << p.second << '\n';
  }
  return 0;
}

```

- Bu örnekte, std::map kullanılarak girilen kelimelerin sayısı hesaplanır. std::transform işlevi kullanılarak girilen kelimeler küçük harfe dönüştürülür. Daha sonra, std::map::operator[] işlevi kullanılarak her kelime için bir sayac oluşturulur. Son olarak, std::map'de bulunan tüm anahtar-değer çiftleri yazdırılır.

- std::map sınıfı, bir anahtar-değer koleksiyonu tutmak istediğimizde ve anahtarların benzersiz olması gerektiğinde kullanışlıdır. std::map, herhangi bir tür için kullanılabilir ve performansı yüksek bir veri yapısıdır.
