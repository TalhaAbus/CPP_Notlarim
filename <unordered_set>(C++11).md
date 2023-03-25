- <unordered_set> başlık dosyası, unordered_set adlı sınıfın tanımlanmasını içerir. unordered_set, öğeleri anahtar olarak tutan bir bağlı liste veri yapısına dayalı bir veri koleksiyonudur. Bu sınıf, öğeleri key-value çiftleri olarak saklamak yerine sadece anahtarları saklar. Bu nedenle, her bir anahtar yalnızca bir kez bulunur.

- unordered_set sınıfı, arama, ekleme ve silme işlemleri gibi temel işlemler için O(1) karmaşıklığına sahip bir yapı sunar. Bu sınıf aynı zamanda, set sınıfına benzer bir arayüz sunar ancak set'in sıralanmış olması yerine anahtarların hash değerlerine göre düzensiz olarak saklanması ile farklılık gösterir.

- unordered_set sınıfı, C++11 standartlarından itibaren kullanılabilmektedir ve STL'nin bir parçasıdır.

# set ve unordered_set arasinda ne fark var

- set ve unordered_set arasındaki temel fark, depolama ve erişim sürelerindeki farklılıklardır.

- set, klasik kırmızı-siyah ağaç kullanarak verileri sıralı bir şekilde depolar. Bu nedenle, elemanların erişimi logaritmik zaman alır ve depolama bellek maliyeti nedeniyle bazen daha yavaştır.

- unordered_set, verileri bir karma tablosu kullanarak depolar. Bu, elemanların erişimi sabit zamanda gerçekleşir ve depolama bellek açısından daha verimlidir. Ancak, elemanlar depolama sırasına göre sıralanmaz ve set gibi sıralama özellikleri sunmaz.

- Özetle, set verileri sıralı olarak depolar ve erişimler logaritmik zamanda gerçekleşirken, unordered_set verileri karma tablolar kullanarak depolar ve erişimler sabit zamanda gerçekleşir.

- Hangi birini kullanmanız gerektiği, ihtiyacınız olan özelliklere ve performans gereksinimlerinize bağlıdır.

# neden set yerine unordered_set tercih etmeliyim

- unordered_set, set ile karşılaştırıldığında daha hızlı bir veri yapısıdır ve verileri ekleme, çıkarma ve arama işlemlerinde daha yüksek performans sağlar. Bunun nedeni, unordered_set'in elemanları benzersiz bir şekilde tanımlayan bir öğeyi (hash fonksiyonu) kullanmasıdır. Bu nedenle, eklenecek veya aranacak verilerin sıralaması veya doğru bir şekilde yerleştirilmesi gerekmeyen durumlarda, unordered_set tercih edilebilir.

- Örneğin, büyük veri setleri veya verilerin sıralanması gerekmeyen uygulamalarda unordered_set kullanılabilir. Ancak, set, elemanların sıralanması veya erişim sırasına göre işlem yapmak istenildiği durumlarda daha uygun bir seçenek olabilir.

# kripto para sifrelemelerinde bu kutuphaneler mi kullaniliyor

- C++ standart kütüphanesi içindeki bu başlık dosyaları, kripto para sifrelemelerinde kullanılan özel bir işlevsellik sunmazlar. Ancak, kripto para sifrelemeleri gibi özel amaçlı uygulamalarda, rastgele sayı üretimi gibi C++ standart kütüphanesi işlevleri kullanılabilir. Ayrıca, özel amaçlı kripto para kütüphaneleri de mevcuttur ve bunlar sıklıkla özel amaçlı sifreleme algoritmaları için özel bir arayüz sağlarlar.


