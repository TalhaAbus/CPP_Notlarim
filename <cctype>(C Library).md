- =cctype başlık dosyası, karakter işleme işlevlerinin yer aldığı bir başlık dosyasıdır. Bu işlevler, bir karakterin özelliklerini belirlemek için kullanılır. Bu işlevler, karakterlerin harf, rakam, büyük harf, küçük harf vb. olup olmadığını kontrol etmek için kullanılır.

- Bu işlevler, özellikle metin işleme işlemlerinde karakter dizilerinin analizinde sıkça kullanılır. Ayrıca, cctype başlık dosyasında yer alan diğer işlevler de karakterlerin özelliklerini belirlemek için kullanılabilir.

- **isalnum()**
> 
- **isalpha()**
> 
- **islower()**
> 
- **isupper()**
> 
- **isdigit()**
> 
- **iscntrl()**
> 
- **isgraph()**
> 
- **isspace()**
> 
- **isblank()**
> 
- **isprint()**
> 
- **isounct()**
> 
- **tolower()**
> 
- **toupper()**
> 


### isalnum()
- std::isalnum() C++'ın  cctype  kütüphanesi içerisinde tanımlanan bir işlevdir. Bu işlev, karakterin bir harf veya rakam olup olmadığını kontrol eder. Harf ve rakam karakterleri true döndürürken, diğer karakterler false döndürür.

- Aşağıdaki örnek, isalnum() işlevinin kullanımını göstermektedir:

```CPP
#include <iostream>
#include <cctype>

int main() {
    char c = '3';

    if (std::isalnum(c)) {
        std::cout << c << " is alphanumeric.\n";
    } else {
        std::cout << c << " is not alphanumeric.\n";
    }

    return 0;
}

```

> Bu örnekte, karakter değişkeni c'ye atanmış ve isalnum() işlevi kullanılarak kontrol edilmiştir. Karakter, bir sayısal değer olduğundan, isalnum() işlevi true değerini döndürür. if bloğu, isalnum() işlevinin sonucuna göre bir çıktı üretir.

### isalpha()

- isalpha işlevi, verilen karakterin alfabede bir harf olup olmadığını kontrol eder. Standart C kütüphanesi olan cctype başlık dosyası içerisinde yer alır ve C++'ta da kullanılabilir.

- Bu işlev, int isalpha(int ch) prototipi ile tanımlanır. İşlevin parametresi, test edilecek karakterin int kodu olmalıdır. İşlev, karakter alfabede bir harf ise, işlev geriye 0 olmayan bir değer döndürür. Aksi halde, işlev geriye 0 değerini döndürür.

- Örnek kullanım:

```CPP
#include <cctype>
#include <iostream>
#include <string>

int main() {
    std::string str = "Hello, World!";

    for (char ch : str) {
        if (std::isalpha(ch)) {
            std::cout << ch << " is an alphabet character\n";
        } else {
            std::cout << ch << " is not an alphabet character\n";
        }
    }

    return 0;
}

```
> Bu örnekte, bir std::string nesnesi oluşturulur ve her karakteri std::isalpha() işlevi ile kontrol edilir. Eğer karakter bir harf ise, o karakterin bir harf olduğu ekrana yazdırılır. Aksi halde, karakterin bir harf olmadığına dair bir mesaj yazdırılır.

### islower()
- islower() işlevi, verilen karakterin küçük harf mi yoksa başka bir karakter mi olduğunu kontrol eder. Bu işlev  cctype  başlık dosyasında tanımlanmıştır ve özellikle standart karakter işlevlerinden biridir.

- Bu işlev bir int değer döndürür. Eğer karakter küçük harfse, işlev 0'dan farklı bir değer döndürür. Aksi takdirde, işlev 0 değerini döndürür.

- Aşağıdaki örnek, islower() işlevinin kullanımını göstermektedir:

```CPP
#include <iostream>
#include <cctype>

int main() {
    char ch = 'a';
    if (std::islower(ch)) {
        std::cout << "The character is lowercase." << std::endl;
    } else {
        std::cout << "The character is not lowercase." << std::endl;
    }
    return 0;
}

```

> Bu program, ch karakterinin küçük harf olup olmadığını kontrol eder ve sonucu ekrana yazdırır. Bu örnekte, ch karakteri 'a' olduğundan, çıktı "The character is lowercase." şeklinde olacaktır.

### isupper()

- std::isupper() işlevi, verilen karakterin büyük harf olup olmadığını kontrol eder. İşlev, karakterin büyük harf olup olmadığını kontrol ederse true değerini döndürür; aksi takdirde false döndürür.

- Bu işlev için cctype başlık dosyası dahil edilmelidir.

- Örnek kullanım:

```CPP
#include <iostream>
#include <cctype>

int main() {
    char ch = 'A';
    if (std::isupper(ch)) {
        std::cout << ch << " is an uppercase letter\n";
    } else {
        std::cout << ch << " is not an uppercase letter\n";
    }
    return 0;
}

```

> Bu kod çıktı olarak A is an uppercase letter verecektir.

### isdigit()

- isdigit fonksiyonu, verilen karakterin rakam olup olmadığını kontrol eder. Fonksiyon, bir karakteri argüman olarak alır ve o karakter bir rakam ise (0, 1, 2, 3, 4, 5, 6, 7, 8, 9), true değerini döndürür. Aksi takdirde, yani karakter bir rakam değilse false değerini döndürür.

- Örneğin, aşağıdaki kod karakter dizisi içindeki her bir karakterin bir rakam olup olmadığını kontrol eder:

```CPP
#include <iostream>
#include <cctype>

int main() {
    char str[] = "123abc";
    for (int i = 0; str[i] != '\0'; i++) {
        if (std::isdigit(str[i])) {
            std::cout << str[i] << " is a digit\n";
        } else {
            std::cout << str[i] << " is not a digit\n";
        }
    }
    return 0;
}

```
- Çıktı:

```CPP
1 is a digit
2 is a digit
3 is a digit
a is not a digit
b is not a digit
c is not a digit

```

### isxdigit()
- isxdigit() C++ standart kütüphanesinin bir fonksiyonudur ve bir karakterin onaltılık bir sayı mı yoksa harf mi olduğunu kontrol eder.

- Genel olarak, bir karakterin bir onaltılık rakam olduğunu kontrol etmek için isdigit() fonksiyonu kullanılırken, isxdigit() fonksiyonu bir karakterin bir onaltılık rakam ya da büyük/küçük harf olduğunu kontrol eder.

- Örneğin, aşağıdaki kod bloğunda isxdigit() fonksiyonu kullanılarak bir karakterin onaltılık bir sayı veya harf olup olmadığı kontrol edilmektedir:
```CPP
#include <iostream>
#include <cctype>

int main() {
    char ch1 = 'A';
    char ch2 = '9';
    char ch3 = '#';

    std::cout << std::boolalpha;
    std::cout << ch1 << " is a hexadecimal digit or a letter: " << std::isxdigit(ch1) << std::endl;
    std::cout << ch2 << " is a hexadecimal digit or a letter: " << std::isxdigit(ch2) << std::endl;
    std::cout << ch3 << " is a hexadecimal digit or a letter: " << std::isxdigit(ch3) << std::endl;

    return 0;
}

```
- Çıktı:

```CPP
A is a hexadecimal digit or a letter: true
9 is a hexadecimal digit or a letter: true
# is a hexadecimal digit or a letter: false

```

### iscntrl()

- iscntrl() işlevi, verilen karakterin bir kontrol karakteri olup olmadığını kontrol eder. Kontrol karakterleri, yazı karakterleri değil, belirli işlevleri veya gösterimleri olan özel karakterlerdir.

- Örnek olarak, bir satırın sonunu belirten "new line" karakteri (\n) ve "carriage return" karakteri (\r), terminallerde kullanılan kontrol karakterleridir.

- iscntrl() işlevi, standart C kütüphanesinde <cctype> başlık dosyasında tanımlanır ve aşağıdaki gibi kullanılır:

```CPP
#include <cctype>
#include <iostream>

int main() {
    char c = '\n';

    if (std::iscntrl(c)) {
        std::cout << "The character is a control character.\n";
    } else {
        std::cout << "The character is not a control character.\n";
    }

    return 0;
}

    
```
> Bu örnekte, iscntrl() işlevi, karakter c'nin bir kontrol karakteri olup olmadığını kontrol eder. Karakter bir "new line" karakteridir, bu nedenle iscntrl() işlevi true değeri döndürür ve "The character is a control character." yazısı ekrana yazdırılır.


### isgraph()
- isgraph() işlevi, karakterin grafiğe sahip olup olmadığını kontrol eder. Grafiği olmayan kontrol karakterleri hariç tüm karakterler true değerini döndürür.

- İşlev, <cctype> başlık dosyasında tanımlanır ve şu şekildedir:

```CPP
 int isgraph(int c);

```
> Burada c, kontrol edilen karakterin ASCII değerini temsil eder. Eğer c grafiğe sahip bir karakter ise, işlev 0'dan farklı bir değer döndürür. Aksi takdirde, işlev 0 değerini döndürür.

- Örnek kullanımı aşağıdaki gibidir:

```CPP
#include <iostream>
#include <cctype>

int main() {
    char ch = 'A';
    if (isgraph(ch)) {
        std::cout << ch << " is a printable character with graphical representation\n";
    } else {
        std::cout << ch << " is not a printable character with graphical representation\n";
    }
    return 0;
}
 
```
> Bu örnekte, isgraph() işlevi ch karakterinin grafiğe sahip bir karakter olduğunu kontrol eder. Eğer karakter grafiğe sahipse, program "A is a printable character with graphical representation" şeklinde bir çıktı verir.
    
### isspace()
    
- isspace() standart C kütüphanesi cctype başlık dosyasında yer alan bir fonksiyondur. Bu fonksiyon, verilen karakterin boşluk karakteri olup olmadığını kontrol eder. Boşluk karakterleri şunlardır:

- Boşluk (space)
- Yatay sekme (tab)
- Yeni satır (newline)
- Satır başı (carriage return)
- Diğer özel boşluk karakterleri
- Fonksiyon, verilen karakterin bir boşluk karakteri olması durumunda true değerini, aksi takdirde false değerini döndürür.

- Örnek kullanım:
    
```CPP
#include <cctype>
#include <iostream>
#include <string>

int main() {
  std::string str = "Hello, World!";

  for (char c : str) {
    if (std::isspace(c)) {
      std::cout << "space found\n";
    }
  }

  return 0;
}
 
```
> Bu örnekte, isspace() fonksiyonu kullanılarak str dizesinin her bir karakteri boşluk karakteri mi diye kontrol ediliyor. Eğer bir boşluk karakteri bulunursa ekrana "space found" yazdırılıyor.
    
    
### isblank()

- isblank() C++11 standardında tanımlanmış bir fonksiyondur ve <cctype> başlık dosyasında yer alır. Bu fonksiyon, parametre olarak aldığı karakterin bir boşluk veya sekme karakteri olup olmadığını kontrol eder.

- Örneğin, aşağıdaki kod örneğinde, kullanıcı tarafından girilen karakterlerin boşluk veya sekme karakterleri olup olmadığını kontrol ediyoruz:
    
```CPP
#include <iostream>
#include <cctype>

int main()
{
    char ch;
    std::cout << "Enter a character: ";
    std::cin >> ch;

    if (std::isblank(ch)) {
        std::cout << "The character is a blank or tab character.\n";
    } else {
        std::cout << "The character is not a blank or tab character.\n";
    }

    return 0;
}
 
```
    
> Bu örnekte, kullanıcı tarafından girilen karakterin isblank() fonksiyonu ile kontrol edilerek, bir boşluk veya sekme karakteri olup olmadığı belirlenir. Bu bilgiye göre, ekrana uygun mesaj yazdırılır.
    
### isprint()
    
- isprint C++'ın <cctype> başlık dosyasında tanımlı bir işlevdir. Bu işlev bir karakterin ekrana yazdırılabilir bir karakter mi yoksa başka bir özel karakter mi olduğunu kontrol eder. İşlev, verilen karakterin ASCII kodunu alır ve eğer karakter ekrana yazdırılabilirse (yani ' ' (boşluk) ve ASCII değeri 33-126 arasındaki karakterler gibi) 0 olmayan bir değer döndürür. Aksi takdirde 0 döndürür.

- Örneğin:
    
```CPP
#include <iostream>
#include <cctype>

int main() {
    char ch = '\n';
    if (std::isprint(ch)) {
        std::cout << ch << " is printable." << std::endl;
    } else {
        std::cout << ch << " is not printable." << std::endl;
    }
    return 0;
}
 
```
> Bu örnekte, ch değişkeni '\n' karakterini içerir, bu da bir satır atlama karakteridir. isprint işlevi bu karakteri ekrana yazdırılabilir bir karakter olarak kabul etmez ve sonuç olarak " is not printable." yazdırır.
    
### ispunct()
    
- ispunct() fonksiyonu, standart bir karakterin, standart bir baskı tipinde görüntüsü olmayan bir işaret karakteri olup olmadığını belirler. İşaret karakterleri, boşluk, harf, sayı veya kontrol karakterleri olmayan karakterlerdir. Örnek işaret karakterleri şunlardır: nokta, virgül, soru işareti, ünlem işareti vb.

- Fonksiyon, int ispunct(int c) şeklinde tanımlanır ve geçilen karakterin işaret karakteri olması durumunda 0 olmayan bir değer döndürür. Aksi takdirde 0 döndürür.

- Örneğin:
    
```CPP
#include <iostream>
#include <cctype>

int main() {
  char c = '!';

  if (std::ispunct(c)) {
    std::cout << c << " is a punctuation character\n";
  } else {
    std::cout << c << " is not a punctuation character\n";
  }

  return 0;
}
 
```
> Bu örnekte, ispunct() fonksiyonu c karakterinin işaret karakteri olup olmadığını kontrol eder. c karakteri bir ünlem işareti olduğu için, ispunct() fonksiyonu 0 olmayan bir değer döndürür ve program "!" karakterinin bir işaret karakteri olduğunu belirtir.
    
    
### tolower()
    
- tolower() işlevi, verilen karakterin küçük harfli eşdeğerini döndürür. Karakter veri türü int olmalıdır. Eğer verilen karakter zaten küçük harfli ise, fonksiyon verilen karakteri aynen döndürür. Karakterin küçük harfe dönüştürülmesi, yerel ayarlamalara bağlıdır.

- <cctype> başlık dosyasında tanımlıdır.

- Örnek kullanım:
    
```CPP
   #include <iostream>
#include <cctype>

int main() {
    char ch = 'A';

    std::cout << "Original character: " << ch << '\n';
    ch = std::tolower(ch);
    std::cout << "Lowercase character: " << ch << '\n';

    return 0;
}
 
```
- Bu program aşağıdaki çıktıyı üretir:
    
```CPP
Original character: A
Lowercase character: a

```

### toupper()

- std::toupper ve std::tolower C++'ta yerleşik karakter işlevleri (character functions) olarak tanımlanmış fonksiyonlardır ve <cctype> başlık dosyasında tanımlanmışlardır.

- std::toupper verilen karakterin büyük harf karşılığını verirken, std::tolower verilen karakterin küçük harf karşılığını verir. İkisi de int türünde bir karakter kodu alır ve yine int türünde bir karakter kodu döndürür.

- Örnek kullanım:
    
    
```CPP
 #include <iostream>
#include <cctype>

int main() {
    char ch = 'a';
    std::cout << "ch before: " << ch << '\n';
    ch = std::toupper(ch);
    std::cout << "ch after toupper: " << ch << '\n';
    ch = std::tolower(ch);
    std::cout << "ch after tolower: " << ch << '\n';

    return 0;
}

```
    
- Bu program, önce ch değişkenine 'a' karakterini atar, sonra std::toupper() fonksiyonuyla ch değişkenindeki 'a' karakterini büyük harfe dönüştürür ve sonrasında std::tolower() fonksiyonuyla tekrar küçük harfe dönüştürür. Son çıktı 'a' olacaktır.
    
    
    
    
# Notlar
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
- Örnek olarak, bir kullanıcının girdiği bir karakter dizisindeki rakam sayısını bulmak için <cctype> başlık dosyasındaki isdigit() işlevi kullanılabilir:

```CPP
#include <iostream>
#include <cctype>

int main() {
    std::string str = "Hello 123 World!";
    int digitCount = 0;
    for (char c : str) {
        if (isdigit(c)) {
            digitCount++;
        }
    }
    std::cout << "The string \"" << str << "\" contains " << digitCount << " digits.\n";
    return 0;
}

```

- Bu kod, verilen karakter dizisindeki rakam sayısını bulur ve çıktı olarak ekrana yazdırır.

# Bu başlık dosyası olmadan da aynı işi yapabileceğimiz standart c++ kütüphanesi var mıdır

- Evet, standart C++ kütüphanesi içerisinde karakter sınıflandırma işlemleri için kullanılabilecek bazı fonksiyonlar yer almaktadır. Bunlar arasında std::isalnum, std::isalpha, std::isdigit, std::isspace, std::islower, std::isupper gibi fonksiyonlar yer alır. Ancak cctype başlık dosyası, C dilinde yer alan standart karakter sınıflandırma fonksiyonlarını (örneğin isxdigit, ispunct, isgraph vb.) da C++ dilinde kullanılabilir hale getirmektedir.


















