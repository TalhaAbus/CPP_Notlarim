- C++20 standart kütüphanesindeki <bit> başlık dosyası, bit manipülasyonu yapmak için kullanılır. Bu başlık dosyası, özellikle bit işlemleri gerektiren uygulamalar için yararlıdır.

- Bu başlık dosyası, özellikle iki tip bit işlemini destekler:

- **Bitwise manipülasyon (ve, veya, xor, vs.)**
- **Bit rotation (döndürme işlemleri)**
- <bit> başlık dosyası, C dilindeki bit işlemleri için tanımlanan işaretli ve işaretsiz tamsayı veri türlerine karşılık gelen C++ tamsayı veri türlerinin yanı sıra, bit işlemleri için kullanılacak fonksiyonlar ve sabitler de tanımlar.

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
















