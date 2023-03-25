- C++'ın <random> başlık dosyası, rasgele sayı oluşturma işlemleri için kullanılır. Bu başlık dosyası, rastgele sayı üreteçleri, dağılımlar ve diğer ilgili araçlar gibi birçok sınıfı içerir.

- Rastgele sayı üreteçleri, bize belirli bir aralıkta rastgele sayılar üretmek için kullanılır. Bu üreteçler, çeşitli veri türlerinde rastgele sayılar oluşturabilirler, örneğin int, float veya double. Bir rastgele sayı üreteci, rastgele sayılar üretmek için önceden belirlenmiş bir algoritma kullanır ve genellikle bir başlangıç değeri veya tohum sayısı alır.

- Dağılımlar, rastgele sayıların belirli bir dağılıma göre üretilmesine olanak tanır. Örneğin, normal dağılıma göre rastgele sayılar üretmek istediğimizde, normal dağılım dağılımını kullanabiliriz. Diğer kullanılabilecek dağılımlar arasında Bernoulli, binom, poisson ve uniform dağılımlar bulunur.

- <random> başlık dosyası ayrıca rastgele sayı üreteçlerinin performansını artırmak için kullanabileceğimiz bir dizi araç da içerir. Örneğin, std::random_device sınıfı, gerçek bir rastgele sayı üreteci sağlar ve std::chrono başlık dosyası ile birleştirerek saat gibi değişkenlere dayalı tohum sayıları oluşturabiliriz.

- Aşağıda, C++'ta <random> başlık dosyası kullanarak rastgele sayılar oluşturma örneği verilmiştir:

```CPP
#include <iostream>
#include <random>

int main() {
    std::random_device rd;
    std::mt19937 gen(rd());
    std::uniform_int_distribution<> dis(1, 6);

    for (int i = 0; i < 10; ++i) {
        std::cout << dis(gen) << ' ';
    }
    std::cout << '\n';
}

```
- Bu örnek, bir std::random_device nesnesi kullanarak bir tohum sayısı oluşturur ve ardından bir std::mt19937 rastgele sayı üreteci oluşturur. Daha sonra, std::uniform_int_distribution dağılımını kullanarak, 1 ila 6 arasında rastgele tamsayılar oluştururuz. Son olarak, oluşturulan rastgele sayıları ekrana yazdırırız.

- <random> başlık dosyası altında birçok farklı random sayı üretim aracı bulunur. Bunlar, rastgele sayı üretmek için farklı algoritmalar ve dağılımlar kullanır. Bazı alt sınıflar şunlardır:

**std::linear_congruential_engine**
**std::mersenne_twister_engine**
**std::subtract_with_carry_engine**
**std::mersenne_twister_64**
**std::ranlux24_base**
**std::ranlux48_base**
**std::ranlux24**
**std::ranlux48**
**std::knuth_b**

- Her bir alt sınıf farklı bir random sayı üretim algoritması kullanır ve bu algoritmaların bazıları daha iyi dağılımlar üretir veya daha güvenli olabilir.

- random sınıfının tam içeriği oldukça uzundur ve birçok alt sınıf içerir. Bu alt sınıflar arasında:

**linear_congruential_engine**
**mersenne_twister_engine**
**subtract_with_carry_engine**
**discard_block_engine**
**independent_bits_engine**
**shuffle_order_engine**
**knuth_b_engine**
**default_random_engine**
- gibi rastgele sayı üretici motorları bulunmaktadır. Her biri farklı bir yöntem kullanarak rastgele sayı üretir.

- Ayrıca, uniform_int_distribution, uniform_real_distribution ve normal_distribution gibi çeşitli dağıtım sınıfları da bulunmaktadır. Bu sınıflar, rastgele sayıların belirli bir dağılımı takip etmesini sağlamak için kullanılır.

- random sınıfı, rastgele sayı üretimi için standart bir arayüz sağlar ve farklı platformlarda ve uygulamalarda güvenilir sonuçlar elde edilmesini sağlar.

- Bir zar oyunu için 1-6 arası rastgele bir sayı üretme:

```CPP
#include <iostream>
#include <random>

int main() {
    std::random_device rd; // random_device kullanarak rastgelelik sağla
    std::mt19937 gen(rd()); // Mersenne Twister algoritmasını kullanarak generator oluştur
    std::uniform_int_distribution<> dis(1, 6); // 1-6 arası uniform bir dağılım oluştur

    std::cout << "Zar atma sonucu: " << dis(gen) << std::endl; // rastgele sayıyı yazdır
    return 0;
}

```

> Bu örneklerde std::random_device sınıfını kullanarak bir donanım tabanlı rastgelelik sağlanıyor. std::mt19937 sınıfı, Mersenne Twister algoritmasını kullanarak bir rastgele sayı üreteci oluşturuyor. std::uniform_int_distribution ve std::uniform_real_distribution sınıfları, sırasıyla tam sayı ve ondalık sayılar için uniform bir dağılım oluşturuyor.

- Evet, örneklerimde genellikle Mersenne Twister 19937 algoritması (mt19937) kullanmıştım. Ancak C++'ın <random> kütüphanesi, bir dizi farklı rastgele sayı üretme motoru (random number engine) ve dağıtım (distribution) sınıfı sağlar. Bu motorlar ve dağıtımlar, farklı rastgele sayı üretme ihtiyaçlarına göre seçilebilir.

- Örneğin, bir oyun için hızlı ve rastgele bir sayı üretmek gerekiyorsa, mt19937 kullanılabilir. Ancak bir simülasyon veya istatistiksel modelleme için daha spesifik bir dağıtım gerekebilir.

- Aşağıda, farklı motor ve dağıtımların kullanıldığı örnekler verilmiştir:

**Motor: linear_congruential_engine, Dağıtım: uniform_int_distribution**

```CPP
#include <iostream>
#include <random>

int main() {
    std::linear_congruential_engine<unsigned long long, 6364136223846793005ULL, 1442695040888963407ULL, std::numeric_limits<unsigned long long>::max()> engine;
    std::uniform_int_distribution<int> dist(1, 100);

    for (int i = 0; i < 10; i++) {
        std::cout << dist(engine) << " ";
    }

    return 0;
}

```
> Bu örnekte, bir linear congruential engine kullanarak uniform_int_distribution'ı kullanarak 1 ile 100 arasında bir rastgele tam sayı üretiyoruz.


**Motor: mt19937, Dağıtım: normal_distribution**

```CPP
#include <iostream>
#include <random>

int main() {
    std::mt19937 engine;
    engine.seed(std::random_device{}());
    std::normal_distribution<double> dist(0.0, 1.0);

    for (int i = 0; i < 10; i++) {
        std::cout << dist(engine) << " ";
    }

    return 0;
}

```
> Bu örnekte ise, mt19937 motorunu kullanarak normal_distribution'ı kullanarak standart normal dağılıma uygun rastgele sayılar üretiyoruz.












