- std::bitset sınıfı, C++ standart kütüphanesinde yer alan bir sınıftır. Bu sınıf, bir bit dizisi temsil eder ve birçok bit işlemi yapmak için kullanılabilir.

- std::bitset sınıfı, sabit boyutlu bir bit dizisini temsil eder ve bu boyut compile-time'da belirtilir. Yani, std::bitset nesneleri oluşturulduktan sonra boyutları değiştirilemez.

- std::bitset sınıfı, bit dizisindeki her bir bitin değerini 0 veya 1 olarak saklar. Bitleri kontrol etmek, ayarlamak veya temizlemek için birçok işlev sağlar. Ayrıca, std::bitset nesneleri, standart aritmetik operatörlerini (+, -, *, /, %, vb.) ve bit işlemleri operatörlerini (|, &, ^, vb.) destekler.

# Member Functions

- **set()**
> bir std::bitset nesnesinin belirtilen indeksindeki bit değerini 1 olarak ayarlar.
- **reset()**
> belirtilen bitleri 0'a ayarlar (sıfırlar) ve bit dizisinin diğer bitleri üzerinde herhangi bir etkisi yoktur. reset() işlevi, set() işlevinin tam tersidir.
- **flip()**
> belirtilen pozisyondaki bitin değerini tersine çevirir ve bitset'i döndürür.
- **count()**
> belirtilen bit setindeki 1 bitlerinin sayısını hesaplar ve döndürür. Fonksiyon, std::size_t türünde bir değer döndürür.
- **test()**
> belirtilen bitin değerini döndürür. Bit 1 olarak ayarlanmışsa true döner, aksi halde false döner.
- **any()**
> bit setinin herhangi bir bitinin ayarlanıp ayarlanmadığını sorgular. Eğer en az bir bit ayarlanmışsa, true değerini döndürür, aksi takdirde false değerini döndürür.
- **none()**
> bitset'teki tüm bitlerin 1 (true) olup olmadığını kontrol eder. Tüm bitler 1 ise all() fonksiyonu true değerini döndürür, aksi halde false değerini döndürür.
- **all()**
> bitset'teki tüm bitlerin 1 (true) olup olmadığını kontrol eder
- **size()**
> Bu fonksiyon, bit kümesindeki toplam bit sayısını verir.
- **to_string()**
> bir bit kümesini string bir biçime dönüştürür.
- **to_ulong()**
> bitset nesnesinde tutulan bitlerin bir unsigned long tamsayısına dönüştürülmesini sağlar. 
- **to_ullong()**

### set()

- std::bitset::set() bir std::bitset nesnesinin belirtilen indeksindeki bit değerini 1 olarak ayarlar.

- Örneğin, aşağıdaki kodda mybitset adında bir std::bitset nesnesi oluşturulur ve 2. indeksindeki bit değeri 1 olarak ayarlanır:

```CPP
#include <bitset>
#include <iostream>

int main() {
  std::bitset<4> mybitset;  // 4 bit uzunluğunda bir bitset nesnesi oluşturur
  mybitset.set(2);          // 2. indeksindeki bit değerini 1 olarak ayarlar

  std::cout << mybitset << '\n';  // 0001
  return 0;
}

```

### reset()

- reset() işlevi, belirtilen bitleri 0'a ayarlar (sıfırlar) ve bit dizisinin diğer bitleri üzerinde herhangi bir etkisi yoktur. reset() işlevi, set() işlevinin tam tersidir.

- Örnek kullanımı:

```CPP
#include <bitset>
#include <iostream>

int main() {
  std::bitset<8> bits("11011011");
  std::cout << bits << '\n'; // 11011011

  bits.reset(3);
  std::cout << bits << '\n'; // 11010011

  bits.reset();
  std::cout << bits << '\n'; // 00000000
}

```
> Bu örnekte, öncelikle 8 bitlik bir std::bitset örneği tanımlanır ve ilk değeri "11011011" olarak ayarlanır. Sonra, üçüncü biti sıfırlamak için reset() işlevi kullanılır ve sonuç olarak bit dizisi "11010011" olarak değiştirilir. Daha sonra tüm bitleri sıfırlamak için reset() işlevi bir kez daha çağrılır ve bit dizisi sıfırlanır (tüm bitler 0'a ayarlanır).

### flip()

- std::bitset::flip() fonksiyonu, belirtilen pozisyondaki bitin değerini tersine çevirir ve bitset'i döndürür.

- Örneğin, aşağıdaki kod bir std::bitset oluşturur ve belirtilen pozisyonlardaki bitleri tersine çevirir:

```CPP
#include <iostream>
#include <bitset>

int main() {
  std::bitset<8> mybits("00001111");
  std::cout << "Before flip: " << mybits << '\n';

  mybits.flip(2);
  mybits.flip(5);

  std::cout << "After flip: " << mybits << '\n';

  return 0;
}

```
> Bu kod örneği, aşağıdaki çıktıyı üretir:

```CPP
Before flip: 00001111
After flip: 00101011

```

> Burada, mybits bit kümesi önce 00001111 olarak tanımlanır ve sonra 2. ve 5. bitler tersine çevrilir. flip() fonksiyonu, her bir belirtilen pozisyondaki bitin değerini tersine çevirir. Sonuç olarak, çıktıda 2. ve 5. bitlerin değeri 1, diğer bitlerin ise 0 olduğu görülür.


### count()

- std::bitset sınıfının count üye fonksiyonu, belirtilen bit setindeki 1 bitlerinin sayısını hesaplar ve döndürür. Fonksiyon, std::size_t türünde bir değer döndürür.

- Örneğin, aşağıdaki kod std::bitset sınıfının count üye fonksiyonunu kullanarak bir bit kümesindeki 1 bitlerinin sayısını hesaplar:

```CPP
#include <bitset>
#include <iostream>

int main() {
  std::bitset<8> bits(0b10101010);
  std::cout << "Number of set bits: " << bits.count() << std::endl;
  return 0;
}

```

- Bu program şu çıktıyı üretir:

```CPP
Number of set bits: 4

```

### test()

- std::bitset::test() fonksiyonu, belirtilen bitin değerini döndürür. Bit 1 olarak ayarlanmışsa true döner, aksi halde false döner.

- Örnek kullanımı aşağıdaki gibi olabilir:

```CPP
#include <bitset>
#include <iostream>

int main() {
    std::bitset<8> mybits("01010101");
    
    bool bit_value = mybits.test(3); // mybits'teki 3. bitin değerini alır

    std::cout << "3. bit value is " << bit_value << '\n';

    return 0;
}

```
> Bu örnek, "01010101" değerine sahip mybits bit kümesindeki 3. bitin değerini alır ve bunu bit_value değişkenine kaydeder. std::bitset::test() fonksiyonunun geri döndürdüğü bool değeri daha sonra ekrana yazdırılır.

### any()

- any fonksiyonu, std::bitset sınıfının üye fonksiyonlarından biridir ve bit setinin herhangi bir bitinin ayarlanıp ayarlanmadığını sorgular. Eğer en az bir bit ayarlanmışsa, true değerini döndürür, aksi takdirde false değerini döndürür. Örneğin:

```CPP
#include <iostream>
#include <bitset>

int main() {
  std::bitset<4> bits;
  bits.set(0);
  bits.set(2);

  if (bits.any()) {
    std::cout << "At least one bit is set.\n";
  } else {
    std::cout << "No bits are set.\n";
  }
  
  return 0;
}

```

> Bu örnekte, bits bit seti oluşturulur ve set() fonksiyonu kullanılarak 0. ve 2. bit ayarlanır. Daha sonra any() fonksiyonu kullanılarak bit setinin herhangi bir bitinin ayarlanıp ayarlanmadığı sorgulanır ve çıktı "At least one bit is set." şeklinde olur.

### none()

- none bir bit kümesinde tüm bitler 0 olduğunda true döndüren bir bit işlemidir. Bit kümesinde en az bir bit 1 ise false döndürür. Bu işlem, all işlemi ile tam tersidir.

- Örneğin, aşağıdaki kodda a bit kümesinde hiçbir bit 1 değilken, b bit kümesinde en az bir bit 1 olduğu için none işlemi true değer döndürür.

```CPP
#include <bitset>
#include <iostream>

int main() {
  std::bitset<4> a{0b0000};
  std::bitset<4> b{0b0011};

  std::cout << std::boolalpha;
  std::cout << std::bitset<4>{a}.to_string() << " none: " << a.none() << '\n';
  std::cout << std::bitset<4>{b}.to_string() << " none: " << b.none() << '\n';
}

```
- Çıktı:
```CPP
0000 none: true
0011 none: false

```

### all()

- all() bitset sınıfının bir üye fonksiyonudur ve bitset'teki tüm bitlerin 1 (true) olup olmadığını kontrol eder. Tüm bitler 1 ise all() fonksiyonu true değerini döndürür, aksi halde false değerini döndürür.

- Örneğin:

```CPP
#include <iostream>
#include <bitset>

int main() {
    std::bitset<8> bits1("10101010");
    std::bitset<8> bits2("11111111");

    if (bits1.all()) {
        std::cout << "Bits1 has all bits set to 1\n";
    } else {
        std::cout << "Bits1 does not have all bits set to 1\n";
    }

    if (bits2.all()) {
        std::cout << "Bits2 has all bits set to 1\n";
    } else {
        std::cout << "Bits2 does not have all bits set to 1\n";
    }

    return 0;
}

```

> Bu program "Bits1 does not have all bits set to 1" ve "Bits2 has all bits set to 1" çıktısını üretir.

### to_string()

- to_string() fonksiyonu C++'ın bitset kütüphanesinde bulunur ve bir bit kümesini string bir biçime dönüştürür.

- Örnek kullanım:

```CPP
#include <iostream>
#include <bitset>

int main() {
    std::bitset<8> bits{ 0b11001010 };
    std::string bits_string = bits.to_string();

    std::cout << bits_string << '\n';  // Output: 11001010
    return 0;
}

```
> Yukarıdaki örnekte bitset sınıfı kullanılarak bits adında bir nesne oluşturuldu ve bu nesne 8 bit uzunluğunda bir bit kümesi olarak tanımlandı. Daha sonra to_string() fonksiyonu kullanılarak bit kümesi, string bir biçime dönüştürüldü ve bits_string adındaki string nesnesine atandı. Son olarak, dönüştürülmüş bit kümesi std::cout kullanılarak ekrana yazdırıldı.



### to_ulong()

- to_ulong() fonksiyonu std::bitset sınıfının bir üye fonksiyonudur. Bu fonksiyon bitset nesnesinde tutulan bitlerin bir unsigned long tamsayısına dönüştürülmesini sağlar. bitset nesnesindeki bit sayısı, unsigned long tamsayısının boyutunu aşarsa, sonuç tanımsızdır.

- Aşağıdaki örnek, bitset nesnesinde tutulan bitleri unsigned long tamsayısına dönüştürerek yazdırır:

```CPP
#include <iostream>
#include <bitset>

int main() {
    std::bitset<8> bits("10101010");
    std::cout << bits.to_ulong() << std::endl; // prints 170
    return 0;
}

```

### to_ullong()

- std::bitset sınıfı, sabit boyutlu bitlerin bir dizisini depolamak için kullanılan bir sınıftır. to_ulong() ve to_ullong() fonksiyonları, bitlerin tam sayı olarak yorumlanmasını ve unsigned long veya unsigned long long türlerindeki temsilcilerini döndürür.

- to_ulong() fonksiyonu, std::bitset nesnesinin boyutu unsigned long'dan küçük veya eşit olduğunda kullanılır. Eğer bitset nesnesinin boyutu unsigned long türünün boyutundan daha büyükse, to_ulong() fonksiyonunun davranışı tanımsızdır.

- to_ullong() fonksiyonu ise, std::bitset nesnesinin boyutu unsigned long long'dan küçük veya eşit olduğunda kullanılır. Eğer bitset nesnesinin boyutu unsigned long long türünün boyutundan daha büyükse, to_ullong() fonksiyonunun davranışı tanımsızdır.

- Özetle, to_ulong() ve to_ullong() fonksiyonları, std::bitset nesnesinin tuttuğu bitleri unsigned long veya unsigned long long türünde temsil eden değerler döndürür. Ancak boyut sınırlandırmaları nedeniyle, bu fonksiyonların kullanımı dikkatli yapılmalıdır.



















