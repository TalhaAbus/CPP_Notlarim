# Ders 1
## C++ Diline Ait Bazı Tanımlar

### Undefined Behaviour
- Tanımsız davranış, Dilin kurallarına göre doğru olabilir fakat derleniip çalıştırıldığında nasıl bir durum olacağı konusunda bir granti yok.
### Unspecified Behaviour
- Derleyici herhangi bir şekilde kod üretebilir.
### Implementation Defined
- Bu da unspecified behaviour fakat derleyici bunu belgelemek zorunda. Derleyici kararlı bir şekilde belirli bir seçeneği tercih ederek kod üretmek zorunda.
### User-Defined type
- Kullanıcının bildirim ile tür oluşturması. (struct, enum, union sözcükleri ile oluşturulan türler)
### External Linkage
- Farklı kaynaklarda kulanılan aynı isimlerin aynı varlığa ait olması
### Internal Linkage
- Farklı kaynaklarda kullanılan aynı isimlerin farklı varlığa ait olması

Örnek: 
> static int x; internal linkage

### Scope Leakage: Kapsam Sızıntısı
- Eğer değişken tanımladığınız alan dışında görünür durumdaysa scope leakage vardır.

Örnek:
```javascript
void func()
{
    int i;
    for (i = 0; i < 10; ++i)    
}
```

### Bazı Farklılıklar:
- Aritmetik türlerden bool türüne tür dönüşümü vardır. Tam tersi de geçerlidir. Dönüşüm 1 veya 0 olur.
- C++ dilinde global const nesneler iç bağlantıda (internal linkage) (c dilinde external linkage)
- C++ dilinde adres türleri ile aritmetik türler arasında örtülü tür dönüşümü yoktur.
- Const t* türünden t* türüne dönüşüm yok.
- Farklı adres türleri arasında da örtülü tür dönüşümleri yok.

# Ders 1 Alıştırmalar

**Soru 1. Kod Geçerli midir?**

```CPP
#include <iostream>

int* gp;

int main()
{
	int x = 100;
	int* ptr = &x;

	bool b1 = ptr;
}
```
**Cevap:**
> Adres, poniter türlerinden bool türüne otomatik dönüşüm var.  b1'in değeri true
Burada true veya false dönüşümü pointer ın null pointer olup olmadığına bağlı.
gp zero initialize edildiği için null pointer değerini almıştır ve dönüşürken false olarak dönüşür.

 **Soru 2.**

```CPP
int main()
{
	bool flag = true;
	bool is_on = false;

    int *ptr = is_on;
}
```
**Cevap:** 
> Bool türünden pointer türüne dönüşüm yok. Kod hatalı. 
Pointer türünden bool türüne dönüşüm var fakat bool türünden pointer türüne dönüşüm yok.

**Soru 3: Kod Geçerli midir?**

```CPP
int main()
{
    const int x = 10;

    int* p = x;
}
```
**Cevap:**
> Sentaks hatası. C++ dilinde const int* türünden int* türüne dönüşüm yok. (c dilinde var)

**Soru 4: Geçerli midir?**

```CPP
int main{
    const int *p;  // Geçerli. Bu const nesne değil. Pointer söz konusu
    int *const p;   // Geçersiz. Const nesnelere ilk değer vermek mecburi.
}
```
# Ders 2
## Notlar:
- C++ dilinde karşılaştırma operatörleri boolean türünden değer üretiyorlar. (True, false)
- Karakter sabitlerinin türü C dilinde int türü iken c++ dilinde char türü.
- C dilinde "akif" sabiti char[5] türünde bir dizi. Sonunda null karakter de var. Array decay var. Aynı string literali C++ idilinde const char[5] türünde. C++ dilinde array decay olduğunda elde ettiğimiz adres, char* değil. Const char* olur. 
- Her iki dilde de string literalini değştirme girişimi tanımsız davranış.

## Array to pointer conversion: 
- Dizi isminin dizinin ilk elemanının adresine dönüştürülmesi C dilinde 2 istisna hariç dizi ismi diinin ilk elemanının adresine dönüştürülüyor.

**2 istisna:** 
> sizeof operatörünün operandının dizi olması.
> Adres operatörünün operandının bir dizi olması.

**Örnek:**
```CPP
int a[10] = {1,5,7};
- int a'nın türü = int[10]
- a'nın adresi olan tür = int (*)[10]
- a ifadesi array decay ile dizinin ilk elemaının adresine dönüştürülüyor. 
- Yani burada a = &a[0]
- Burada 2 ifadenin türü de int*
```

## Referans Semantiği: 
- Sabitlerin tek başına, değişkenlerin tek başına yada bunların operatörleri ile birlikte oluşturduğu birimler. Her ifadenin bir türü ve değer kategorisi var.
**C++ dilimdeki referanslar:**
- L value reference   (Sol taraf referans)
- R value reference   (Sağ taraf referansı)
- Forwarding reference    (Universal reference)

> Not: C dilinde pointer kullanımı çokçca var. Fakat C++ dilinde pointer kullanımı C diline göre çok daha az. Bunun sebebi pointer kullanılan durumalrdaki ihtiyacı karşılamaya yönelik reference semantiği var. Dinamik ömürlü nesnelerin hayatını kontrol etmek için pointer kullandığımız senaryoların büyük kısmında da C de olmayan fakat c++ ya olan "smart pointer" sınıflarını kullanıyoruz.

**Expression - İfade:**
```CPP
x 
x + 5 
f(x)
++X
x++ 
f(x) > g(x)
x * x + y * y
```

## Value Categories:

**C dilinde :**
- L Value expression
- R Value expression

**C++ value categories:**
- Primary value categories:
- PR Value
- L Value
- X Value (Ex-pired value) Hayatı bitmekte olan bir nesneye ilişkin

### Value Categories Notlar
- Bir ifadenin L value olması, o ifadenin bellekteki bir nesne olduğunu gösterir.
- Bir ifadenin R value olması, bellekte kalıcı yeri olmayan, bir ifadenin değerini hesaplamak için oluşturulan ifade demektir. 
- Atama işlecinin hem sol tarafında hem sağ tarafında yer alması geçerli olan ifadeler sol taraf değeridir.
- Atama işlecinin yalnızca sağ tarafında yer alabilen (sol tarafında yer alamayan) ifadeler sağ taraf değeridir.
- Değişkenlerin ouşturduğu ifedeler(diziler dahil) L value expression.
- L value olan ifadeler birer nesneye karşılık geliyor. (Değişkenler)
- PR value ve X value birleşimine R Value deniliyor.
- L value ve X value birleşimine GL Value deniliyor.

## Scope resolution operator: 
- Bir ismi isim alanı içinde arayıp bulmak için :: operatörü kullanılır. 
## Namespace:
- Global isim alanındaki isimleri birbirinden korruyan isimleri içeren bir konteynır.
## Static ömürlü nesleler:
1. Global değişkenler
2. Static anahtar sözcüğü ile tanıtılan yerel değişkenler.
3. String literalleri karşılığı derleyicinini oluşturduğu char diziler.

Örnek:
```CPP
bool b; //global olarak tanımlanan bu değişken false değeri ile hayata başlar.
int * gp; //bunun değeri nullptr olarka başlar.
```

## Initialization:

```CPP
int x;          // Default initialization
int x = 10;     // copy init
int x(98);      // direct init
int x{10};      // uniform init  // brace init
```
- Default initialization nesneleri çöp değer ile hayata başlatıyor. Bunu kullanmak undefined behaviour.

### Neden modern C++ ilk değer verme biçimi olarka {} getirdi?
1. Unmiform olması, neye ilk değer veirrsen ver küme parantei kulanabilrioysun.
2. Daraltıcı dönüşümler küme parantezi ile yapılırsa sentaks hatası.
```CPP
double dval = 5.6;
int i{dval}; // Burada veri  kaybı olduğundan sentaks hatası verecek. Normal parantez kullanılsaydı bu legal bir kod olacaktı.
```
**C++ dilinde bunların hepsi aynı anlamda:**
```CPP
int a1[4] = {0};
int a2[4] = {};
int a3[4]{};
```
> Hepsi zero initialize edilmiş oluyor. C dilinde boşluğun içi dolu olmak zorunda ama burdada boş bırakılabilir.

## Type Deduction - Tür çıkarımı:
- Tür çıkarımı derleme zamanına yönelik bir mekanizma, yani static bir mekanizma. Bazı durumlarda biz türü açıkça yazmasak ta dilin kuralları derleyicinin orada koda bakarak türü ne olduğunu anlamasını sağlıyor. Buna type deduction denir. Biz türü yazmıyoruz. Yazmış kabul ediliyorum, hangi tür olduğunu derleyici koda bakarak anlıyor.

**Static mekanizma ne demek?**
- Bir özellik veya bir araç seti compile time ile ilişkili ise, derleyici koda bakarak bir takım kodları üretiyorsa bu tür araçlara static araçlar denir. Söz konusu araç programın çalışma zamanına ilişkin ise dinamik sözcüğü kullanılıyor.

**Tür çıklarımının faydaları:**
- Bazı durumlarda bir türü tanımlamak için çok fazla token kullanmak gerekiytor. Tür çıkarımı ile hata yapma riski azalıyor.

**Tür çıkarımları:**
- auto type deduction
- decltype type deduction
- decltype(auto)
- lambda expression
- template
**Örnek:**
```CPP
int* foo(const int*, size_t);

int main()
{
    int* (*fp)(const int*, size_t) = &foo;  // auto fp = &foo
}
```
**Not:**
- NULL bir makrodur. c nin standart başlık dosyasında tanımlnamış.
```CPP
time(NULL);
time(0);
```
> İkisi arasında bir fark yok. nullptr bir anahtar sözcük, bir constant, türü de nullptr_t türüdür. Bunu kullanmak için herhangi bir başlık dosyasını iclude etmemiz gerekmiyor.

## Ders 2 Alıştırmalar

**Soru 1: sizeof operatörünün ürettiği değerin türü nedir?**

**Cevap:** 
> size_t türü

**Soru 2: Bu ifade geçerli midir? Değeri nedir?**

```CPP
#include <stdio.h>

int main()
{
    int x = 10;
    sizeof x+5;
}
```

**Cevap:**
> Geçerlidir, değeri 9 dur. sizeof operatörünün önceliği aritmetik operatörelerden daha yüksektir.

**Soru 3: int türünün 4 byte olduğu sistemde bu kod çalıştığında ekranda ne yazar?**

```CPP
int main()
{
    int x = 10;
    size_t y = sizeof x++;

    printf("%zu %d \n", y, x);
}
```
**Cevap:**
> Cevap: y=4 x=10 olarka çıkar. sizeof operatörünün operandı olan ifade için işlem kodu üretilmez. C++ dilinde bir ifadenin karşışıoğında i,şlem kodunun üretilmedi durumlara "unevaluated context" denir.
> C dilinde unavaluated context sadece sizeof operatörü için var. C++ dilinde işlem kodu üretilmeyen context 8-9 adet var.

**Soru 4: Kod neden hatalı?**

```CPP
int main()
{
	char* p = "batuhan";
}

```
**Cevap:**
> Cevap: Bu const char bir dizi olduğu için array decay ile const char * türüne dönüştü. const char* türünden char* türüne c++ dilinde örtülü dönüşüm olmadığı içiçn sentaks hatası oldu.
> Hata kodu: a value of const char* type cannot be used to initialize an entity of type char *

**Soru 5: Türü nedir?**
```CPP
int main()
{
    short s1 = 5, s2 = 7;
    s1 + s2 
}
```
**Cevap:**
> s1 + s2 ifadesinin türü short değil, int türüdür. İnt türü altı işlemler yapıldığında int türüne dönüşür.

**Soru 6: Türü nedir?**
```CPP
int main()
int main()
{
    int x = 10;
    x > 5 ? 3 : 4.7; 
}
```
**Cevap:**
> Runtime ve x değerinin ne oldupunndan bağımsız bu ifadenin türü double dır.

**Soru 6: Kodu açılayınız.**
```CPP
#include <iostream>

int main()
{
    std::cout << "hello world";
}
```
**Cevap:**
> Bir ismi isim alanı içinde arayıp bulmak için :: operatörü kullanılır. Bunun ismi scope resolution operator.
> cout bir değişkenin ismi, ismi ostream olan sınıf türünden global bir değişkenin ismi.
> << bitsel kaydırma operatörü burada operator overloading denilen mekanizmanın arcı olarak kullanılıyor.
Operator overloading: Sınıf nesnesinin operator operandı olması durumunda derleyicinin bu ifadeyi bir fonksiyon çağrısına dönüştürmesi.
cout nesnesi << operatorunun operandı olduğu için derleyici bunu bir fonksiyon çağrısına dönüştürüyor.
Derleyicinin çağıdığı fonskliyona cout nesnesi ve string literali argüman olarka gönderiliyor.













