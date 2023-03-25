- <unordered_map> başlık dosyası, C++'ta hash tablolarının bir uygulamasını içerir. Bu başlık dosyasında, unordered_map sınıfı ve bununla ilgili diğer sınıflar ve yapılar tanımlanmıştır.

- unordered_map veri yapısı, key-value çiftlerini depolar. Key ve value değerleri istenen türde olabilir. Bu veri yapısı, ekleme, silme ve arama işlemleri için sabit bir süre gerektirir.

- unordered_map sınıfının kullanımı, std::map sınıfına benzerdir, ancak std::map'tan daha hızlıdır. unordered_map sınıfı, elemanları hash tablosuna depolar ve elemanlara erişmek için bir anahtarın hash değerini kullanır. Bu, elemanların belirli bir sıraya göre saklanmaması anlamına gelir.

- unordered_map sınıfının kullanımı oldukça basittir. Öncelikle, unordered_map sınıfından bir nesne oluşturulmalıdır ve ardından bu nesne, çiftleri eklemek, silmek ve aramak için kullanılabilir.

- unordered_map ve map verileri anahtar-değer çiftleri şeklinde saklayan C++ standart kütüphanesi sınıflarıdır. map verileri içindeki anahtarlar sıralı şekilde saklanırken, unordered_map verileri sırasız şekilde saklar. Bu nedenle, map verileri arasında gezinme veya arama işlemleri sıralı olduğu için daha yavaş olabilirken, unordered_map verileri sabit zaman (O(1)) karmaşıklıkta arama ve ekleme işlemlerinde daha hızlıdır.

- Ayrıca, unordered_map verileri içindeki anahtarlar birbirinden farklı olmak zorundadır, yani her anahtar veri yapısında yalnızca bir kez bulunabilir. Bu nedenle, bir anahtarın birden fazla kez bulunabileceği multimap veri yapısı ile karşılaştırıldığında, unordered_map daha özelleştirilmiş bir veri yapısıdır ve bu özellik nedeniyle bazı senaryolarda daha etkili olabilir.

- Özetle, unordered_map verileri sırasız ve birbirinden farklı anahtarlar kullanırken, map verileri sıralı ve birbirinden farklı anahtarlar kullanır. Hangi veri yapısının kullanılacağı, uygulamanın gereksinimlerine bağlıdır.

```CPP
#include <unordered_map>
#include <iostream>

int main() {
    // unordered_map tanımlama
    std::unordered_map<int, std::string> myMap = {{1, "one"}, {2, "two"}, {3, "three"}};

    // eleman ekleme
    myMap.insert(std::make_pair(4, "four"));

    // eleman silme
    myMap.erase(3);

    // eleman arama
    auto search = myMap.find(2);
    if(search != myMap.end()) {
        std::cout << "Found " << search->second << " at key " << search->first << std::endl;
    } else {
        std::cout << "Key not found" << std::endl;
    }

    return 0;
}

```
> Bu örnekte, unordered_map sınıfından bir nesne oluşturulur ve {1, "one"}, {2, "two"}, {3, "three"} çiftleri ile başlatılır. Daha sonra, insert() fonksiyonu kullanılarak bir eleman eklenir ve erase() fonksiyonu kullanılarak bir eleman silinir. Son olarak, find() fonksiyonu kullanılarak bir eleman aranır.

# unordered_map ile map arasindaki fark nedir

- unordered_map ve map verileri anahtar-değer çiftleri şeklinde saklayan C++ standart kütüphanesi sınıflarıdır. map verileri içindeki anahtarlar sıralı şekilde saklanırken, unordered_map verileri sırasız şekilde saklar. Bu nedenle, map verileri arasında gezinme veya arama işlemleri sıralı olduğu için daha yavaş olabilirken, unordered_map verileri sabit zaman (O(1)) karmaşıklıkta arama ve ekleme işlemlerinde daha hızlıdır.

- Ayrıca, unordered_map verileri içindeki anahtarlar birbirinden farklı olmak zorundadır, yani her anahtar veri yapısında yalnızca bir kez bulunabilir. Bu nedenle, bir anahtarın birden fazla kez bulunabileceği multimap veri yapısı ile karşılaştırıldığında, unordered_map daha özelleştirilmiş bir veri yapısıdır ve bu özellik nedeniyle bazı senaryolarda daha etkili olabilir.

- Özetle, unordered_map verileri sırasız ve birbirinden farklı anahtarlar kullanırken, map verileri sıralı ve birbirinden farklı anahtarlar kullanır. Hangi veri yapısının kullanılacağı, uygulamanın gereksinimlerine bağlıdır.

- Tabii, bir örnek olarak unordered_map kullanarak bir kelime sayma programı yazabiliriz. Diyelim ki bir metin belgesi var ve her kelimenin kaç kez geçtiğini bulmak istiyoruz. Bu işlemi unordered_map kullanarak aşağıdaki şekilde yapabiliriz:

```CPP
#include <iostream>
#include <string>
#include <unordered_map>
#include <sstream>

int main() {
    std::string text = "Bu bir örnek metindir. Bu metin, örnek olması için yazılmıştır.";
    std::unordered_map<std::string, int> wordCounts;
    std::stringstream ss(text);
    std::string word;
    while (ss >> word) {
        // kelimeyi küçük harfe çevirerek karşılaştırma işlemini kolaylaştırıyoruz
        std::transform(word.begin(), word.end(), word.begin(), ::tolower);
        // kelimenin bulunup bulunmadığını kontrol ediyoruz
        if (wordCounts.find(word) == wordCounts.end()) {
            // bulunamazsa, yeni bir anahtar ve değer çifti oluşturuyoruz
            wordCounts[word] = 1;
        } else {
            // bulunursa, değeri bir arttırıyoruz
            wordCounts[word]++;
        }
    }
    // sonuçları yazdırıyoruz
    for (const auto& pair : wordCounts) {
        std::cout << pair.first << ": " << pair.second << std::endl;
    }
    return 0;
}

```
- Bu örnekte, metni bir stringstream nesnesine yükleyerek, kelime kelime okuyoruz. Okunan her kelimeyi bir unordered_map nesnesinde saklıyoruz. Kelime daha önce görülmemişse, bir yeni anahtar-değer çifti oluşturuyoruz ve değeri 1 olarak atıyoruz. Kelime daha önce görülmüşse, ilgili değeri bir arttırıyoruz. Sonuçları yazdırmak için, unordered_map nesnesindeki anahtar-değer çiftlerini gezerek kelime sayılarını yazdırıyoruz.

- unordered_map ve map arasındaki fark sadece elemanların depolanış biçiminde değil, aynı zamanda arama ve ekleme işlemlerinde de farklılık gösterir. map sıralanmış bir anahtar-değer çiftleri koleksiyonudur ve anahtarların sırası korunurken, unordered_map anahtar-değer çiftlerini bir karma işlevi kullanarak depolar ve anahtarların sırasını korumaz. Bu, unordered_map'ın arama, ekleme ve silme işlemlerinde map'e göre daha hızlı olmasını sağlar. Ayrıca, unordered_map'ın bazı işlemleri sıralı bir veri yapısından daha az bellek kullanarak yapabilmesi nedeniyle, daha düşük bellek kullanımına sahiptir.
























