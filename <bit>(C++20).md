- C++20 standart kütüphanesindeki  bit  başlık dosyası, bit manipülasyonu yapmak için kullanılır. Bu başlık dosyası, özellikle bit işlemleri gerektiren uygulamalar için yararlıdır.

- Bu başlık dosyası, özellikle iki tip bit işlemini destekler:

- **Bitwise manipülasyon (ve, veya, xor, vs.)**
- **Bit rotation (döndürme işlemleri)**
-  bit  başlık dosyası, C dilindeki bit işlemleri için tanımlanan işaretli ve işaretsiz tamsayı veri türlerine karşılık gelen C++ tamsayı veri türlerinin yanı sıra, bit işlemleri için kullanılacak fonksiyonlar ve sabitler de tanımlar.

### bit_cast()

- std::bit_cast C++20 standardında tanıtılan bir işlev şablonudur. Bu işlev, bir nesneyi farklı bir tipe dönüştürmek için kullanılır. std::bit_cast'in en önemli özelliği, bu işlemi tür bitleri düzeyinde yapmasıdır.

- Bir nesneyi tür bitleri düzeyinde farklı bir tipe dönüştürmek, yalnızca belirli koşullar altında tanımlanmıştır. Bu koşullar, kaynak ve hedef tiplerinin boyutu ve hafızadaki yerleşim biçimleriyle ilgilidir. Dolayısıyla, std::bit_cast işlevi, bu koşullar sağlandığında güvenli bir şekilde kullanılabilir.

- std::bit_cast işlevi, iki parametre alır: kaynak nesnenin türü ve hedef nesnenin türü. İşlev, kaynak nesnesinin türünü hedef tipe bit bit dönüştürür ve dönüştürülmüş nesneyi döndürür. Dönüştürme işlemi tamamen derleyici tarafından gerçekleştirilir ve herhangi bir çalışma zamanı maliyeti yoktur.

- Aşağıda std::bit_cast örneği verilmiştir:

```CPP
#include <iostream>
#include <bit>

int main() {
    float f = 3.14159265359f;
    std::uint32_t u = std::bit_cast<std::uint32_t>(f);
    std::cout << std::hex << u << std::endl;
    return 0;
}

```
> Bu örnekte, float türündeki bir f değişkeni, std::uint32_t türüne dönüştürülür. std::bit_cast işlevi, f değişkeninin bellekteki temsili olan tüm bitleri std::uint32_t türüne dönüştürür. Sonuç olarak, u değişkenine kaydedilen 0x40490fdb sayısı, f değişkeninin bellekteki temsilinin 32 bitlik tam sayı olarak gösterimini verir.

- std::bit_cast işlevi, bellek alanının türü ile ilgili herhangi bir değişiklik yapmaz, sadece türün bit düzeyindeki temsiline bakar. Bu nedenle, std::bit_cast işlevinin kullanımı sırasında dikkatli olmak gerektiğini unutmamalısınız.

### byteswap()

- std::byteswap C++20 standard kütüphanesinde bulunan bir işlev şablonudur. Bu işlev şablonu, argüman olarak aldığı türün byte sırasını değiştirir. Örneğin, bir int türünün byte sırasını tersine çevirerek büyük endian'dan küçük endian'a veya tam tersine dönüştürebilirsiniz.

- İşlev şablonu iki farklı sürüme sahiptir: std::byteswap(std::uint16_t) ve std::byteswap(std::uint32_t) gibi sabit boyutlu tamsayı türleri için bir sürüm ve std::byteswap(std::endian, T) şeklinde iki argüman alan bir sürüm. İkinci sürüm, T türünün byte sırasını, std::endian türü tarafından belirtilen byte sırasına göre tersine çevirir.

- İşlev şablonu, bit temelli verileri dönüştürmek için özellikle yararlıdır. Örneğin, bir float türünün binary verilerini bir tam sayı türüne dönüştürmek için std::bit_cast kullanarak bir std::byte dizisine dönüştürebilirsiniz. Daha sonra, byte sırasını tersine çevirerek float türünün binary verilerini elde edebilirsiniz.

```CPP
#include <bit>
#include <cstdint>
#include <concepts>
#include <iostream>
#include <iomanip>
 
template <std::integral T>
void dump(T v, char term = '\n') {
    std::cout << std::hex << std::uppercase << std::setfill('0')
              << std::setw(sizeof(T) * 2) << v << " : ";
    for (std::size_t i{}; i != sizeof(T); ++i, v >>= 8) {
        std::cout << std::setw(2) << static_cast<unsigned>(T(0xFF) & v) << ' ';
    }
    std::cout << std::dec << term;
}
 
int main()
{
    static_assert(std::byteswap('a') == 'a');
 
    std::cout << "byteswap for U16:\n";
    constexpr auto x = std::uint16_t(0xCAFE);
    dump(x);
    dump(std::byteswap(x));
 
    std::cout << "\nbyteswap for U32:\n";
    constexpr auto y = std::uint32_t(0xDEADBEEFu);
    dump(y);
    dump(std::byteswap(y));
 
    std::cout << "\nbyteswap for U64:\n";
    constexpr auto z = std::uint64_t{0x0123456789ABCDEFull};
    dump(z);
    dump(std::byteswap(z));
}
```

### has_single_bit()

- std::has_single_bit işlev şablonu, bir unsigned integral türde yalnızca bir bitin ayarlanıp ayarlanmadığını sorgulamak için kullanılır. İşlev, verilen argümanın yalnızca tek bir biti ayarlanmışsa true değerini, aksi takdirde false değerini döndürür.

- Aşağıdaki örnekte, std::has_single_bit işlev şablonu bir unsigned int türündeki bir sayıda yalnızca tek bir bitin ayarlanıp ayarlanmadığını kontrol eder:

```CPP
#include <iostream>
#include <bit>

int main() {
    unsigned int num = 8;
    std::cout << std::boolalpha << std::has_single_bit(num) << '\n'; // false

    num = 16;
    std::cout << std::boolalpha << std::has_single_bit(num) << '\n'; // true

    return 0;
}

```
```CPP
#include <bit>
#include <bitset>
#include <iostream>
 
int main()
{
    std::cout << std::boolalpha;
    for (auto u = 0u; u != 10u; ++u) {
        std::cout << "has_single_bit( " << std::bitset<4>(u) << " ) = "
                  << std::has_single_bit(u) // `ispow2` before P1956R1
                  << '\n';
    }
}
```

# bit_ceil()

- bit_ceil bir bit işlemi fonksiyonudur ve verilen sayıyı iki kuvvetinin üstündeki ilk sayıya yuvarlar. Fonksiyonun kullanımı aşağıdaki gibidir:

```CPP
#include <bit>
#include <iostream>

int main() {
    std::cout << std::bit_ceil(7) << '\n'; // Output: 8
    std::cout << std::bit_ceil(16) << '\n'; // Output: 16
    std::cout << std::bit_ceil(25) << '\n'; // Output: 32
    return 0;
}

```
> Bu örnekte, bit_ceil kullanarak 7'nin 8'e, 16'nın 16'ya ve 25'in 32'ye yuvarlandığını görebilirsiniz. Bu fonksiyonun kullanımı, özellikle veri hizalaması ve bellek yönetimi gibi işlemlerde yararlı olabilir.

### bit_floor()

- bit_floor işlevi, belirtilen tam sayının 2'nin kuvveti olan en büyük sayıya kadar olan bütün sayıları göz önünde bulundurarak floor işlemi uygular. Yani, verilen bir tam sayının 2'nin kuvveti olan en büyük sayıya kadar olan bütün sayılar arasında en küçük olanını döndürür.

- Örneğin, 9'un 2'nin kuvveti olan en büyük sayıya kadar olan bütün sayılar arasında en küçük olanı 8'dir, bu nedenle bit_floor(9) ifadesi 8 değerini döndürür.

- Aşağıdaki örnekte bit_floor işlevi kullanılarak bir sayının 2'nin kuvveti olan en büyük sayıya kadar olan bütün sayılar arasında en küçük olanının bulunması gösterilmektedir:

```CPP
#include <iostream>
#include <bit>

int main() {
    std::cout << std::bit_floor(13) << '\n'; // output: 8
    std::cout << std::bit_floor(16) << '\n'; // output: 16
    std::cout << std::bit_floor(19) << '\n'; // output: 16
    return 0;
}

```

### bit_width()

- bit_width() işlevi, verilen tamsayının iki tabandaki bit uzunluğunu hesaplar ve döndürür. Örneğin, bir unsigned char değeri için 8, bir unsigned int değeri için 32 bit uzunluğunda bit sıralaması kullanılır.

- bit_width() fonksiyonu C++20 standart kütüphanesinde tanıtılmıştır ve  bit  başlık dosyası içinde yer alır.

- Aşağıdaki örnekte, bit_width() işlevi birkaç tamsayı türü için nasıl kullanılır:

```CPP
#include <iostream>
#include <bit>

int main() {
    std::cout << std::bit_width(0) << '\n'; // 0
    std::cout << std::bit_width(1) << '\n'; // 1
    std::cout << std::bit_width(2) << '\n'; // 2
    std::cout << std::bit_width(255) << '\n'; // 8
    std::cout << std::bit_width(1024) << '\n'; // 11
    std::cout << std::bit_width(-1) << '\n'; // 32 (for unsigned int)
    return 0;
}

```

> Bu örnekte, bit_width() işlevi, 0 ve 1 için beklenen sonuçları üretirken, 2 ve 255 için 2 ve 8 gibi doğru bit uzunluklarını hesaplar. Ancak, 1024 için 11 gibi bir sonuç üretirken, -1 için 32 (bir unsigned int değeri için) döndürür.

### rotl()

- rotl (rotate left) işlemi, verilen sayının bitlerini belirli bir sayıda sola kaydırır ve kaydırma işlemi sırasında en sağdaki bitler en solda, en soldaki bitler de en sağda olacak şekilde döndürür. Özellikle bit tabanlı işlemlerde ve kriptografi gibi alanlarda kullanılabilir.

- C++20 ile birlikte, std::rotl fonksiyonu da dil standart kütüphanesine eklenmiştir. Bu fonksiyon, bir sayıyı belirli bir sayıda sola döndürür. Fonksiyonun imzası aşağıdaki gibidir:

```CPP
template< class T >
constexpr T rotl( T value, unsigned int count ) noexcept;

```
- Burada T parametresi, döndürülecek sayının türünü belirtir. value parametresi, döndürülecek sayıdır. count parametresi, döndürme işlemi sırasında kaç bitin kaydırılacağını belirtir. Bu fonksiyon, constexpr olduğu için derleme zamanında çalışabilir.

Örnek kullanımı aşağıdaki gibi olabilir:

```CPP
#include <iostream>
#include <bitset>

int main() {
    std::uint8_t x = 0b00011011;
    auto y = std::rotl(x, 3); // x'in bitlerini 3 bit sola kaydırır
    std::cout << std::bitset<8>(x) << " --> " << std::bitset<8>(y) << '\n';
    return 0;
}

```

> Bu kod örneğinde, 8 bitlik bir sayı olan x önce std::bitset ile yazdırılır, sonra std::rotl fonksiyonu kullanılarak bitleri 3 bit sola kaydırılır ve sonuç tekrar std::bitset ile yazdırılır.

### rotr()

- rotr C++20 standardıyla birlikte  bit  başlık dosyasına eklenen bir fonksiyondur. Bu fonksiyon, bir veriyi sağa doğru bir sayı kadar döndürür (sağa kaydırır) ve yuvarlama (wraparound) işlemi yapar.

- Örneğin, 8 bitlik 00110110 değeri (54 ondalık) 2 bit sağa kaydırılırsa, sonuç 10001101 (141 ondalık) olur. Ancak burada 8 bitlik bir tamsayı kullanıldığından, yalnızca son 3 bitin kaydırılması etkilidir ve üst 5 bit kaybolur. rotr fonksiyonu yuvarlama işlemi yaparak, kaybolan bitleri tekrar ekler.

- rotr fonksiyonunun imzası şöyledir:

```CPP
template <typename T>
constexpr T rotr(T value, unsigned int count) noexcept;

```
- Burada, T bir unsigned tamsayı türüdür ve value döndürülecek tamsayı değeridir. count ise sağa kaydırılacak bit sayısıdır.

- Örneğin:

```CPP
#include <iostream>
#include <bit>

int main() {
    uint32_t a = 0x87654321;
    uint32_t b = std::rotr(a, 8);
    std::cout << std::hex << b << '\n'; // prints "21876543"
    return 0;
}

```

> Bu örnekte, a değişkenindeki değer 0x87654321'dir ve rotr fonksiyonu ile 8 bit sağa kaydırılır. Sonuç olarak b değişkenindeki değer 0x21876543 olur.

### countl_zero()

- countl_zero işlevi, std::bitset'deki count işlevi gibi, verilen unsigned integral türündeki bir değerin başlangıcında yer alan 0 bitlerin sayısını hesaplar. Ancak, countl_zero bitleri en soldan başlayarak sayar. Yani, bir bit set edilene kadar 0 bitlerin sayısını sayar.

- Bu işlevin kullanımı aşağıdaki gibidir:


```CPP
#include <iostream>
#include <bit>

int main() {
    std::cout << std::countl_zero(0x00000100u) << '\n'; // output: 23
    std::cout << std::countl_zero(0x00000300u) << '\n'; // output: 22
    std::cout << std::countl_zero(0x00000400u) << '\n'; // output: 21
    return 0;
}

```

> Yukarıdaki örnek, verilen sayıların başlangıcında yer alan 0 bitlerin sayısını hesaplar ve bunları ekrana yazdırır.

### countl_one()

- countl_one işlevi, bir tamsayının önde gelen sıfırlarından önceki ardışık 1 bitlerinin sayısını hesaplar. Örneğin, 0b00110100 argümanı verildiğinde, countl_one işlevi 2 değerini döndürür.

Aşağıda bir örnek verilmiştir:

```CPP
#include <iostream>
#include <bitset>

int main() {
    std::bitset<8> bits("00110100");

    std::cout << "Bits: " << bits << '\n';
    std::cout << "Number of leading ones: " << std::countl_one(bits.to_ulong()) << '\n';

    return 0;
}

```
> Bu program, "Bits: 00110100" ve "Number of leading ones: 2" çıktısını üretir. std::bitset sınıfı, ikili sayıları tutmak ve işlemek için kullanılan bir sınıftır. std::countl_one işlevi, bir unsigned int türündeki sayının önde gelen sıfırlarından önceki ardışık 1 bitlerinin sayısını hesaplar. Yukarıdaki örnekte, std::bitset sınıfının to_ulong() işlevi, ikili sayıyı ondalık sayıya dönüştürmek için kullanılır.

### countr_zero()

- countr_zero() işlevi, bir tamsayının sağdan sola ilk sıfır bitine kadar olan sıfırların sayısını döndürür. Örneğin, 0b1001010 (74) sayısı verildiğinde, sağdan sola ilk sıfır bitine kadar 1 tane sıfır olduğu için countr_zero(74) işlevi 1 değerini döndürecektir.

- Aşağıda countr_zero() işlevinin bir örneği verilmiştir:

```CPP
#include <iostream>
#include <bitset>

int main() {
    std::bitset<8> bits("1001010");
    unsigned long count = bits.count();
    unsigned long count0 = bits.count() - bits.count();
    std::cout << "Number of 0 bits: " << count0 << '\n';
    return 0;
}

```
> Bu örnek, "1001010" bitlerinin 0 sayısını hesaplar ve sonucu ekrana yazdırır.

### countr_one()

- countr_one() işlevi, bir unsigned veya unsigned long tamsayının sağdan başlayarak ilk bit 1 olana kadar kaç sıfır biti olduğunu sayar.

Örneğin, 10110100 ikili sayısında, sağdan ilk 1'in hemen solundaki sıfır bitine kadar olan 2 adet sıfır biti olduğundan, countr_one(0xb4) işlev çağrısı sonucunda 2 döndürür.

### popcount()

- popcount işlevi, bir tamsayının ikili (binary) gösterimindeki birlerin sayısını sayar ve bu sayıyı döndürür. Bu işlev C++20'de <bit> başlık dosyası altında bulunur.

- Örnek kullanım:

```CPP
#include <bit>
#include <iostream>

int main() {
    unsigned int n = 0b110101011;  // 219
    int count = std::popcount(n);
    std::cout << "Number of set bits in " << n << ": " << count << '\n';
    return 0;
}

```


# Notlar



Örneğin, std::bitset sınıfı kullanılarak bir bit kümesi oluşturulabilir ve bu kümedeki belirli bitlere erişilebilir. Aşağıdaki örnek, std::bitset sınıfı ile bir bit kümesi oluşturur ve 3. ve 5. bitlerini belirler:

```CPP
#include <iostream>
#include <bitset>

int main() {
  std::bitset<8> bits;
  bits.set(3);
  bits.set(5);
  std::cout << "Bits: " << bits << std::endl;
  return 0;
}

```

- Çıktı:

```CPP
Bits: 00101000

```

- Bu örnek, <bit> başlık dosyasının bir örneği değildir, ancak bit kümesi işlemlerinde <bit> başlık dosyası kullanımını daha basit hale getirebilir.

# Bit ve bitset arasinda ne fark var

- bit başlık dosyası bit operasyonları yapmak için fonksiyonlar içerirken bitset başlık dosyası bitleri depolamak ve manipüle etmek için sınıf ve fonksiyonlar içerir.

- bit başlık dosyasında yer alan fonksiyonlar arasında, bitleri okumak, yazmak, kaydırmak, ters çevirmek gibi işlemleri gerçekleştirmek için kullanabileceğimiz fonksiyonlar yer alırken bitset başlık dosyası bitleri bir sabit boyutlu dizi olarak tutar ve belli bitlere ulaşmak için [] operatörünü kullanabiliriz.

- Özetle, bit başlık dosyası bit manipülasyonu için daha geniş bir kütüphane sağlarken, bitset başlık dosyası bitleri depolamak ve manipüle etmek için özel bir sınıf sağlar.

# bit operasyonlari yapmak icin iverdigi fomksiyonlar nedir ve ne ise yarar

- <bit> başlık dosyası, bit düzeyinde işlemler yapmak için kullanılan fonksiyonları ve sabitleri içerir. Bu işlemler, örneğin bitleri kaydırmak, tek tek bitlere erişmek, belirli bir biti ayarlamak veya sıfırlamak gibi işlemleri içerir.

- Aşağıda, <bit> başlık dosyası tarafından sağlanan bazı özelliklerden bazılarını listeleyeceğim:

- **std::bitset:** Belirtilen boyutta bir bit kümesi oluşturur ve bitlerin değerlerini ayarlamak ve sorgulamak için bir dizi işlev sağlar.
- **std::rotl, std::rotr:** Verilen bir değeri belirli bir bit sayısı kadar sola veya sağa kaydırır.
- **std::popcount:** Verilen bir değerin kaç tane 1 biti olduğunu hesaplar.
- **std::has_single_bit:** Belirtilen bir değerin sadece bir biti ayarlanmışsa true, aksi takdirde false döndürür.
- **std::countl_zero, std::countl_one, std::countr_zero, std::countr_one:** Belirtilen bir değerin başında veya sonunda kaç tane sıfır veya bir biti olduğunu hesaplar.
- Bu işlevlerin birçoğu, özellikle yerel ağ, veri şifreleme, video işleme ve veri sıkıştırma gibi performans açısından yoğun uygulamalarda kullanılabilir.

# ornek uzerinde bunlari kullanarak anlat

- Tabii, aşağıdaki örnekte std::bitset sınıfını kullanarak bit operasyonlarını gösterelim:

```CPP
#include <iostream>
#include <bitset>

int main() {
  std::bitset<8> bits1(0b00010101);
  std::bitset<8> bits2(0b00000110);

  std::cout << "bits1: " << bits1 << std::endl;
  std::cout << "bits2: " << bits2 << std::endl;
  std::cout << std::endl;

  std::cout << "bits1 & bits2: " << (bits1 & bits2) << std::endl;  // bit-wise AND
  std::cout << "bits1 | bits2: " << (bits1 | bits2) << std::endl;  // bit-wise OR
  std::cout << "bits1 ^ bits2: " << (bits1 ^ bits2) << std::endl;  // bit-wise XOR
  std::cout << "~bits1: " << (~bits1) << std::endl;                // bit-wise NOT
  std::cout << std::endl;

  std::cout << "bits1 << 2: " << (bits1 << 2) << std::endl;  // left shift
  std::cout << "bits1 >> 2: " << (bits1 >> 2) << std::endl;  // right shift
  std::cout << std::endl;

  std::cout << "bits1.count(): " << bits1.count() << std::endl;  // number of set bits
  std::cout << "bits1.any(): " << bits1.any() << std::endl;      // at least one bit is set
  std::cout << "bits1.none(): " << bits1.none() << std::endl;    // no bits are set
  std::cout << std::endl;

  std::bitset<8> bits3;
  bits3.set(0);  // set bit at position 0
  bits3.set(2);  // set bit at position 2
  bits3.reset(2);  // reset bit at position 2
  bits3.flip(3);   // flip bit at position 3

  std::cout << "bits3: " << bits3 << std::endl;

  return 0;
}

```
> Bu örnekte, 8 bitlik iki bit kümesi oluşturuluyor: bits1 ve bits2. Bit işlemleri & (ve), | (veya) ve ^ (XOR) kullanılarak yapılmıştır. Ayrıca, ~ (değil) operatörü kullanılarak bir bit kümesinin tamamı ters çevrilebilir. Bit kaydırmaları için << (sola kaydırma) ve >> (sağa kaydırma) operatörleri kullanılır. Ayrıca count() ile kaç bitin ayarlandığı, any() ile en az bir bitin ayarlandığı ve none() ile hiçbir bitin ayarlanmadığı kontrol edilebilir.

> Bu örnekte, bitset sınıfının set, reset ve flip fonksiyonları kullanılarak bir sayının ikilik sistemdeki bitlerine erişildi ve değiştirildi. Daha sonra, bir önceki örnekte olduğu gibi, bit başlık dosyasındaki rotl fonksiyonu kullanılarak sayının belli bir miktarda sola döndürülmesi sağlandı.
















