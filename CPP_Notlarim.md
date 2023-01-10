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

# Ders 2 Alıştırmalar

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

# Ders 3
## Basic type türler:
```CPP
char 
signed char
unsigned char

char türünün storage 1 byte olması garanti altında 
---------
bool (tam sayı türü ve integral promotion a tabi)
---------
short
unsigned short
---------
long
unsigned long
---------
long long   en az 8 byte
unsigned long long
---------
int     çalışılan ortama bağlı olarak 2-4-8 byte
unsigned int

sizeof(short) <= sizeof(int) <= sizeof(long) <= sizeof(long long)  // garanti altında, veri kaybı yok

char türü karakterlerden bağımsız bir tam sayı türü olarka da kullanılabilir.

Gerçek sayı türleri:
float
double
long double
```

## Scope Kategorileri:
### C dilindeki scope kategoerileri:

- block scope 
- file scope 
- function scope 
- function prototype scope

### C++ dilindeki scope kategorileri:

- block scope 
- namescape scope 
- class scope 
- function scope 
- function prototype scope

## Short Circuit Behaviour:

- || , && operatörleri söz konusu olduğunda bu operatörlerin sol operandları önce değerlendiriliyor. 
- Lojik ve operatöçrünün sol oeprandı doğru sonucu elde edilmişse sağ taraf için işlem kodu üretilmiyor.

# Ders 3 Alıştırmalar:

**Soru 1: Hangi fonksiyon daha önce çağırılır?**
```CPP
x = f1() + (f2() * 5);
```
**Cevap:**
> Unspecified behaviour. Bunun garnatisi yok. Derleyiciye bağlı.

**Soru 2: If doğru kısmına girer mi?**
```CPP
int main()
{
    const char* p1 = "oytun";
    const char* p2 = "oytun";

    if(p1 == p2){
    }
}
```
**Cevap:**
> Unspecified behaviour. Aynı string literallerinin derleyici tarafından aynı bellek alanında tutulup tutulmayacağı tamamen deeleyiciye bağlı.
> C++ visual sutudio ile denendi ve aynı adreste tutulduğu görüldü.

**Soru 3: Kod doğru mudur?**
```CPP
int x;

int main()
{
#include <stdio.h>

int main(void)
{
    int printf = 5;
    printf("merhaba \n");
}
```
**Cevap:**
> Burada sentaks hatası var. Ama hatanın nedeni name lookup değil. printf name lookup sonucu int türden bir değişken ismi olduğu anlaşılıyor ve bu fonksiyon çağrı operatörününü operandı oluyor. Bu sentaks hatasıdır.

**Soru 4: Kod doğru mudur?**
```CPP
#include <stdio.h>

int main(void)
{
    printf("merhaba \n");
    int printf = 5;
}
```
**Cevap:**
> Burada sentaks hatası yok. Legal bir code. Printf ismi local alanda bulunamadı ve global alanda devam etti ve bulundu.

**Soru 5: Kod geçerli midir?**
```CPP
int main()
{
    for(int i = 0; i<10; i++)
    int i = 56;
}
```
**Cevap:**
> Bu kod C dilinde geçerlidir. C++ dilinde sentaks hatasıdır.

**Soru 6: Kod geçerli midir? **
```CPP
void x();

int main(){
    int x = 34;

    x(); // geçersiz
    ::x(); // geçerli, global namespace araması
}
```

**Soru 7: Kod geçerli midir?**
```CPP
int main(){
    
    int printf{};
    ::printf(_Format: "ali");
}
```
**Cevap:**
> Geçerli globalden printf çağırılıyor.

**Soru 8: y nin değeri nedir?**
```CPP
int main()
{
    int x =  0;
    int y = 10;

    int a = x && ++y;
}
```
**Cevap:**
> y nin değeri 10 olarak kalır. İşlem kodu üretilmez. Short circuit behaviour var.

# Ders 5

## Type Conversion:

- Öyle bir durum ki deleryici bir işlemi yapabilmesi için bir ifadenin statik olarak koddaki türünü kullanmak yerine farklı bir türden değer olarak işe sokuluyor.
- Burada genelde geçici bir nesne oluşturuluyor.

1. Implicit Type Conversion : Örtülü Tür dönüşümü
2. Explicit Type Conversion : Açık tür dönüşümü

**Implicit:** Bir kod yazarak derleyiciye bir talimaty verilememsine rağmen derleyici dil kurallarına dayanarak örtülü bir tür dönüşümü yapıyor.
**Explicit:** Biz derleyiciye bunu yapması emrini veriyoruz.

## References:
**Modern c++ dilinde 3 ayrı referans kategorisi var:**

- L value Reference
- R value Reference
  > Move semantics
  > Perfect Forwarding
- Forwarding Reference (Universal Reference)

**Örnek:**
```CPP
int main()
{
    int x = 10;
    int* p = &x;

    *p = 20;
}
```
- Burada *p, x nesnesinin kendisidir. Kullandığın zaman x i kullanmış olursun.
- * p; 
- *p = 20;
- Burada üzerinde işlem yaptığımız nesne x in kendisidir. Yani *p demek x demektir.

> Referanslar default initialize edilemez:

```CPP
int& x; // Sentaks hatası
int& r = x; // geçerli
```

```CPP
int* p = nullptr;
int* & r = p;

Burada r = p demektir.
```

### Referans kullanımı:
%99 ihtimal ile :
- Bir nesneyi bir fonksiyona call by reference 
- Bir fonksiyonun kendisini çağıran koda bir nesnenin kendisini göndermesi / iletmesi
- C dilinde fonksiyon çağrı ifadeleri her zaman R value expression.
- C++ dilinde fonksiyon çağrı ifadeleri, fonksiyonun geri dönüş değeri L value referece türü ise , fonksiyon çağrısının türü de sol taraf değeridir.

### Type Deduction (Tür çıkarımı)
- Runtime ile bir alakası yok. Tamamen compile time ile ilişkili.
- Bir nesnenin türünün programın çalışma zamannında belirlenmesi (Dinamik tür)
- Tür çıkarımı auto için yapılıyor, bildirilen değişkenin türü için değil.

```CPP
const int cx = 6;
auto y = cx; // Burada y nin türü int. Const düşüyor.

int main
{
    int a[3] = {1,2,3};
    
}
```
### [Ders 5 Örnek Kodlara Bak](https://github.com/TalhaAbus/CPP_Notlarim/blob/main/Ders%205%20Ornekler.md)

# Ders 5 Alıştırmalar:

**Soru 1: Kod legal midir?**
```CPP
int main()
{
	int x= 5;
	int y = 9;
	int a = x+++y;
	std::cout << "a =" << a << "\n";
}
```
**Cevap:**
> Geçerli. Maximal munch kuralı geçerlidir. En uzun token oluşacak şekilde tokenizing yapılıyor.

**Soru 2: Ekrana merhaba yaz ama ; kullanma.**

**Cevap 1:**
```CPP
int main()
{
	if (std::cout << "merhaba\n")
	{
	}
}
```
**Cevap 2:**
```CPP
int main()
{
	while (!(std::cout << "merhaba"))
	{
	}
}
```
**Cevap 3:**
```CPP
int main()
{
	switch (!(std::cout << "merhaba"))
	{
	}
}
```

**Soru 3: Çıktı nedir?**
```CPP
#include <iostream>

int main()
{
	int x = 10;

	int* p = &x;

	++* p;
	std::cout << x;
}
```
**Cevap:**
> Burada değişen x in kendisidir.


**Soru 4: Çıktı nedir?**
```CPP
#include <iostream>

int main()
{
	int x{ 3 };
	int& r{ x };
	// Buradan sonra r nin scope içinde r yazmak ile x yazmak arasında bir fark yok.
	std::cout << "x = " << x << "\n";

	r = 67;
	std::cout << "x = " << x << "\n";
	++r;
	std::cout << "x = " << x << "\n";
}
```
**Cevap:**
> çıktılar     x = 3  x = 67  x = 68

**Soru 5: C dilinde ve c++ dilinde burada ki x in değeri nedir?**
```CPP
int main()
{
	int x = 45;
	// func(x);
	std::cout << "x =" << x << "\n";
}
```
**Cevap:**
> C dilinde tüm fonksiyon çağrıları call by value dur. Bu sebeple x indeğeri her zaman 45 tir. Fakat C++ dilinde func fonksiyonunda referans semantiği kullanılmış olabilir. Fonksiyonun kodunu görmeden bu sorunun cevabı verilemez.

# Ders 6

```CPP
auto x{3};      // Burada çıkarım int olarak yapılıyor.
auto x = {3};   // Burada çıkarım std::initializer_list olarak yapılıyor.
```

```CPP
int x = 10;
auto p1 = &x;       // int *p1 = &x; auto ==> int*
auto* p2 = &x;      // int *p2 = &x; auto ==> int
```

```CPP
int* ptr = &x;

auto p1 = &ptr;     // auto nun yerine gelen tür int**
auto* p2 = &ptr;    // int*
auto** p3 = &ptr;   // int

Ama sonuçta p1, p2, p3 int** türünen değişkenler. Çıkarım değişken için değil auto için yapılıyor.
```
## Reference Collapsing:

- C++ dilinin kurallarında referecen to reference yok. Ama bazı bağlanlar ile oluşturuluyor.
- Referecne to referecne olması gereken türn yerine L value veya R value reference kullanılıyor.

## Decltype:

- Bir ifadeyi temsil ediyor. Decltype(x);

```CPP
decltype(expr);
```
Burada hangi türün elde edileceği expr ifadesinin değer kategorisine (primary value category) bağlı.

## Varsayılan Argüman:

- C'de olmayan bir araçtır. Argüman fonsksiyon çağrısında kullanılan ifadedir.

> Parameter: Fonksiyıonun parametresi.
> Argument: Fonksiyıon çağrısında değeri gönderilen ifadeler.

```CPP
foo(12); // Fonksiyona 12 değerindeki argümanı gönderdim.
```

```CPP
void func(int, int, int = 10);
```
> Fonksiyonun 3. parametesi gödnerilmez ise 10 gönderilmiş varsayılacak.
> Varsayılan argünamlar son parametreler için geçerli.

**Bir sabitr ifadesi olmak zorunda değil, örnek:**
```CPP
void f(int = x);
veya,
int f1(int x = 0);
void f2(int y = f1());
int main()
{
    f2(); == f2(f1(0));
}
```

# Ders 7

## Function Overloading
- Function overloading derleme zamanına ilişkin bir mekanizma.

**Genel Programlama alanında kullanılan popüler terimler:**
- Derleyici, hangi fonksiyonun çağırıdlığını koda bakarak anlayacak ve o fonksiyonu çağıracak. Çağrının fonksiyona bağlanması, derleyicinin ürettiği kod ile belirleniyor. 
> Eğer fonksiyon çağrısı derleme zamanında bir fonksiyona bağlanıyorsa buna programlamada "static binding" (early binding)denir.
> Hangi fonksiyonun çağırıldığı programın çalışma zamanında anlaşılıyorsa (programın çalışma zamanıunda koşan bir kod ile tespit ediliyorsa) buna "dynamic binding" (late binding) denir.

- Function overloading olmasaydı C gibi olurdu. Birden fazla fonskiyona aynı işi yapsalar da farklı isimler vermek zorunda kalırdık ve kodu yazmak daha zor olurdu.
- Overload olan fonksiyonları nasıl seçeceğimizi bilmezsek yanlış fonksiyonu çağırabiliriz.

**Dilin kurallarına göre aynı isimli fonksiyonlar bir overloading oluşturabilriler veya oluşturmayabilirler.**

### Function overloading olması için:
1. Fonksiyonların ismi aynı olacak
2. Kapsamları (scope) aynı olacak
3. İmzaları farklı olacak

**C++ Scope kategorileri**
1. namespace scope
2. class scope
3. block scope
4. Function prototype scope 
5. Function scope

- Aynı isimli fonksiyonlar farklı scope ta ise: name hiding, name masking, name shadowing olabilir.
- Farklı scope'taki fonksiyonlar overload oluşturmazlar. Farklı scopetaki isimler birbirini gizleyebilirler.

### Function signature :
- Fonksiyon parametre değişkeni sayısı ve her bir parametresini türü. Overloading olması için imzalarının da farklı olması gerekiyor.

```CPP
int foo(int, int);
int func(int, int);
```
> Bunların imzaları aynı.

## Fucntion Overload Resolution:
- Derleyicinin Hangi fonksiyonun çağrılacağını anlamaya  çalışma sürecine function overload resolution denir.
- Derleyiciye göre değişmeyen bir durumdur.

**Overload Resolution nasıl yapılır?**
- En fazla 3 aşamada yapılır.

> 1. aşamada Derleyici derleyici sadece fonk. isminden hareketle aynı isimli fonksiyonları kayda alıyor. Bunlar aday fonksiyonlar.
> 2.aşamda derleyici "bu fonksiyon tek başına olsaydı bu fonksiyon çağrısındaki argümanlar ile çağırılması legal olur muydu" sorusunun cevabını alıyor. Bunun cevabı evet ise bu fonksiyonlara "viable function" deniliyor.

**Not:**
> Function overloading var olması o isimli fonksiyona yapılan her çağrının legal olduğunu göstermiyor. o fonksiyon çağırısı sentaks hatası da olabilir.

### User- defined conversion :
- Normalde olmayan bir dönüşüm, bir fonksiyonun bildirilmesiyle ve derleyicinin bu fonksiyonu kullanarak dönüşümü gerçekleştirmesi olayı.

# Ders 7 Alıştırmalar
Alıştırma soruları: [Tıkla](https://github.com/TalhaAbus/CPP_Notlarim/blob/main/Ders%207%20Alistirmalar.md)


### Sorulardan notlar:
1. Parametrenin constluğu bir imza farklılığı yaratmaz
2. Aynı türe verilenm tür eş isimleri overloading yaratmaz.
3. Call by value, call by reference overloading oluşturur.

# Ders 8
**Bazı Tanımlar:**

### Function overloading:
- Aynı isimli fonksiyonların aynı scopeta bulunması özelliği. Function overload resolution yapılarak hangi fonksiyonun çağırıldığı anlaşılıyor.

### User - defined conversion:
- Örtülü olarka yapılamayan dönüşüm kullanıcı fonksiyon bildirdiği için derleyici fonksiyonma çağrı yaparak dönüşüm gerçekleştiriliyor.

```CPP
void func(int x, int y = 0);
void func(int x);
```
> Function overloading çünkü imzaları farklı.

**Örnek:**
int x = 5;

- x in value category si nedir?

> Bir ifadenin value category si olur. Bir değişkenin olmaz. Bu exression u niteleyen bir terim.

> X in bize data type ı sorulabilir. Bunun cevabı int. 

> Value category soruluğunda 3 cevap olabilir: PR - X - L value.

**Örnek:**
```CPP
int x = 10;
int &r = x;
```
- r nin value category si L value.

```CPP
int &&r = 10;
```
**r nin value category si?**
> Eğer R value expression kullanılırsa, bu nesnenin yerine geçen bir isimdir. Yani L value expressiondır.

> Yani bir ifade isim tarafında oluşturulmuşlsa her zaman l value expressinodur.

## Bazı Tanımlar:

### One Definition Rule
- Bazı varlıklar farklı kaynak dosylarrda tanımları aynı olmak üzere external olmalarına rağmen ODR yi ihlal etmiyor.
### Inline expension: 
- Derleyicilerin en sık kulandığı bir optimizasyon tekniğidir. Complier optimizationdır.
### Compiler optimization:
- Derleyici birebir assembly kodu üretmek zorunda değil. Observable behaviour değişmeden derleyici istediği gibi kod üretebilir.
### Dead code elimination:
- Observable behaviour değiştirmeyen her kodu derleyici siler.
**Kısaca:**
> biz derleyiciye ne istedğimizi veriyoruz. O bize sonuç garantisi vererek istediği gibi kod üretebiliyor. ve bu optimizasyon yapılırken derleyici UB olmadığına güvenerek yapıyor.
### Loop unrolling:
- Bir döngü olmasına rağmen derleyici ilave maliyet yaratan iişlemleri elimine etmek için bu döngü yokmuş gibi kodu derliyor. Döngü kadar kodu tekrar yazabiliyor (Ek optimizasyonlar ile birlikte)
### Loop reversal: 
- Döngünün ters çevirilmesi
### Generic programming:
- Derleyici compile time da yazdığı kodun ne olacağı, yine derleyicinin compile time da yaptığı bir takım kontroller ile belli oluyor.
- Yani farklı versiyonlarda kod yazıp o kodu da yine optimize edebiliyor.
### Inline expension:
- En sık ve en eski kullanılan teknik. En fazla verim üstünde en çok verim sağlayan teknik.


## Bu tanımlar ile ilgili notlar:

- C++ ve C en büyük farklarından biri, c++ derleyicileri sadece çeviri programı değil. Derleyici bizim için kod yazaıyor. Bunu yazarken kullandığı paradigma , **generic programming paradigması**.

```CPP
a = func();
```
> func ın bir geri dönüş değeri var, yazılacağı bir bellek adresi var. O bellek adresindeki değeri de a ya kopyalamaya yönelik bir kod üretiyor diyelim.

> Bu satırdaki koddan önce func ın definition ının olduğunu varsayalım. Derleyici direkt a = (fonksiyonun kodu); olacak şekilde bir kod üretecek. Peki neden böyle bir kod üretilsin? 

> Fonksiyona giriş ve çıkışın da bir maliyeti var. Fakat optimize edildiğinde doğrudan aritmetik işelemler yapan kodlar var.

> Örneğin fonksiyonun içinde 3 birimlik iş yapılıyor ise, fonksiyına giriş ve çıkışın maliyetinin 10 birim olduğunu varsayalım. İşte derleyici maliyet hesaplaması ile bunun daha verimli olup olmadığına bakıyor. İşte buna inline expension denir. Yani kaynak kodda bir fonksiyon çağrısı var ama derleyicinin ürettiği kodda aritmetik işlemler yapan kodlar var.

> Bunun en büyük adayları, kodu küçük olan ve çok sık çağırılan fonksiyonlar.

### inline fonksiyonlar: 
- one definition rule ihlal etmeyecek demek.

```CPP
inline int func(int x, int y)
{
    
}
```
- Bu fonksiyonun tanımını birden fazla kaynak dosyada token by token aynı yapılırsa, one definition rule ihlal etmeyecek demek.
- Yani inline fonksiyon başlık dosyasına tanıumı koyulduğuda, ODR ihlal etmeyecek.
- Bunu neden yapalıkm?

> Derleyiciye inline expension olanağı sağlamak amacıyla yapalım.
Biz inline fonksiyon yaptığımızda derleyicinin bu fonksiyonu görmesini sağlıyoruz.

**Not:**
> Derleyici inline anahtar sözcüğü kullanıldı diye onu inline etmek zorunda değil ve yine inline yazmadığımız fonksiyonları derleyici inline expend edebilir.

- inline yazmanın amacı başlık dosyasına koymak, inline omasaydı ODR ihlali olurdu.

### Complete Type - Incomplete Type

```CPP
class Nec; // Class decleration
```
- Derleyici bir türün varlığınndan harberdar ama o türün detaylarını bilmiyor.
- Biz böyle bir bildirim yaparsak derleyici bu bildirimini gördüğünde sınıf türünü bilecek ama tanımını görmüyor.
- Bu bir incomplete type. Complete type ise tam tersi. Tüm bilgilere derleyici hakim.

**Türün complete ya da incomplete olması bizi niye ilgilendiriyor?**
> Bazı kodlar için türün incomplete olması o kodun derlenmesi için yeterli. Bazıları için complete olması gerekiyor.

```CPP
struct Nec;
Nec f1(Nec);
Nec* f2(Nec&);

typedef Nec* NecPtr;
using NecRef = Nec&;
extern Nec necx; // Burada sentaks hatası yok. Bu bir değişken bildirimi.
                    // Bu bir decleration. Definition olsaydı derleyici bunun için yer ayırmak zorunda kalacaktı ve storage ihgtiyacını bilmek zorunda olacaktı.
```
> Bunların hepsi incomplete type olmasına rağmen sentaks hatası yok.

> sizeof operatörünün operandı yapılamaz, yapılması için complete type olması gerekiyor.

# Ders 8 Alıştırmalar

```CPP
struct Nec;

int main()
{
	Nec mynec;
}
```
**Hata: incomplete type is not allowed.**

```CPP
struct Nec;
Nec* foo();

int main()
{
	Nec *p = foo();
	*p = 1;
}
```
**Cevap:**
> Türün incomplete olması sebebiyle sentaks hatası, dereference ediliyorsa o nesneye erişiliyor ama o nesnenin bilgileri bilinmiyor.

**Örnek:**
```CPP
void func(int &);   viable değil
void func(int &&);  viable

int main()
{
    func(10);
}
```
# Ders 9

## Inline Fonksiyonlar
- Eğer inline fonksiyıonun tanımı ciddi işlem gerektiriyorsa bunu inline ezxpand edilmesi yüksek bir fayda sağlamayacak.

1. Doğrudan inline anahtar sözcüğü ile tanımlanması
2. Bildirimi sınıf içinde yapılması

```CPP
class Myclass{
    void func();
}
```
> Bildirimi sınıf içinde yapılan fonksiyonlar her zaman inline kabul ediliyor.

**Başlık dosyasında bulunupta ODR (one definition rule) ihlal etmeyen varlıklar:**

- inline fonksiyonlar
- class definitions
- templetes(şablonlar)
>    function templates
>    class templates
>    alias templates
>    variable templates

**inline variables:**
```CPP
inline int x = 10;
```

- Birden fazla kaynak dosyada bulunması odr ihlal etmiyor. Global bir değişkenin tanımını başlık dosyasına koyduğumuzda normalde odr ihlal ediliyordu.

## constexpr anahtar sözcüğü:

```CPP
const int x = 10;   // değiğşkenin kendisinin oluşturduğu ifade bir constant expression
```

- x ifadesini constant expression gereken yerlerde kullanılabilir.
- Ancak const anahtar sözcüğü ile tanımlanan bir değişkene sabit ifadesi ile değer vermek mecburi değil.

```CPP
int foo();
const int x = foo();
```
- Geçerlidir.

**Notlar:**
- constexpr anahtar sözcüğü ile tanımlanan değişkene ilk değer veren ifadenin sabit ifadesi olaması zorunludur.


```CPP
constexpr int x;
```

- constexpr keyword ile tanımlanmış ise o değişkenin bir sabit ifadesi olma garantisi var.
- const nesne için böyle bir garantisi yok.

**Örnek:**
```CPP
constexpr int x = 10;
decltype(x) = const int
```
- Orada implicit const var.

> constexpr bir tür değil. Sadece değişkenin sabit ifadesi gereken yerde kullanılabileceğini söylüyor. Implicit olarak const değişken tanımlıyor.

```CPP
constexpr int* p = &g;
```
- p nin türü const int* değil. int* const. Burada değişkenin kendisi const. Bu pointer to const int. 

## constexpr fonksiyonlar:
- Geri dönüş değeri derleme zamanında belli olan fonksiyonlar (Derleme zamanında çağırılan fonksiyonlar)
- Aslında constexpr fonskyinoların varlık nedeni verim.
- Eğer compile time da bazı ifadelerin değeri görülebiliyorsa runtime da bunlar yapılmasın.

```CPP
func (x + y)
```
> Derleyici bu ifadenin değerinin compile time da hesaplanabileceğini görürse bizim yerimize comple time da hesaplayıp, fonksiyon çağrısı olmaqdan bir sabit kullanarak.

# Ders 9 Alıştırmalar:

**Soru 1: başlık dosyasında bu fonksiyon tanımı olursa ne olur?**

```CPP
void func(int x)
{
    //
}
```
**Cevap:**
> Bu başlık dosyası birden fazla kaynak dosya tarafından include edildiğnide ODR ihlal edilmiş olur.

> Bir başlık dosyasına fonksiyon koyacaksak bu inline fonksiyon, şablon veya constexpr fonksiyonu olmalı. constexpr fonksiyonlar zaten örtülü olarak inline.

**Soru 2: Bu başlık dosyası birdenb fazla kaynak dosyada include edildiğpinde runtime ve link açısından func fonksiyonu nasıl görülecek? 
(1 adet mi yoksa her kaynak dosya için ayrı func objesi mi görecek)**

```CPP
//nec.h

inline void func(int x)
{
    //
}
```
**Cevap:**
> 1 adet görülür.

# Ders 10

## Sınıflar

```CPP
class Myclass {

// Burada memberlarin tanimi yapiliyor
// Memberlar: 
// 1. Data member
    bunlar non-static data member. Birde static data memberlar var.

// 2. Member function
    bunlar non-static member function. Birde staci data memberlar var.
// 3. Member Type
    bir turun bildirimini class definition icinde yaparsak member type deniliyor.

};
```
## Class memberlarin ozellikleri:
- Ayri bir scope talar.
- Memberlar public, provate, protected olabilir.
- class ile tanimladigimizda default access specifier: private
- struct ile tanimladigimizda default access specifier: public

**Member Fuctionlar 2 ye ayriliyor:**
1. static
2. Non-static

```CPP
class Mylass {
public:
    void foo();
};
```
> Aslinda bir parametresi var. Myclass* turunden bir parametresi var. Bir pointer istiyor. Myclass turunden bir nesnenin adresini istiyor.


```CPP
int main()
{
    Myclass m;
    m.foo();
}
```

> Sinif nesnesini nokta opratorunun operandi yaptigimizda ve saginda da non-static member function ismi kullandigimizda, derleyici name lookup yapiyor. Ismin sinifin non-static member function ismi oldugunu goruyor.

> Noktanin solundaki nesnenin adresini, foo fonksoyunun aslinda gosterilmeyen Myclass* parametresine arguman olarak gonderiyor.

- Once namelookup
- Sonra context kontrolu
- Sonra acess kontrolu.

**Sinifin uye fonksoyunun tanimi:**

```CPP
//fighter.h

class Fighter{
public:
    void attack(Fighter&);
};

//fighter.cpp

void Fighter::attack(Fighter &r);   // imca ve geri donus turu, sinifta tanimlanan ile ayni olmak zorunda
{

}

public void Myclass::foo() // yanlis. Yasak. Tanimlarken kullanilamaz.
```

**Makrodan faydalanmak:**

```CPP
#define NEC

NEC void foo();
```

> Onislemci program bu makroyu silmek zorunda. Yani derleyiciye geldiginde Translation unit oldugunda Makronun olmadigi garantisi var.

> Bazi programcilar cpp dosyasina bakildiginda tanimlarda da public,private,protected gormek istediginde (ide yardimi olmadan), cpp dosyasinda makro olarak ifade ediyorlar.

```CPP
#define PUBLIC
#define PRIVATE
#define PROTECTED

PUBLIC void Myclass::foo()
{

}
```

**ClassUye fonksiyonlarin taniminda 2 alternatif var.**
1. cpp dosyasinda 
2. Fonksiyonun tanimini direkt class definition icinde yapmak.

> Bu ikisi kesinlikle ayni sey degil.

> Sin1if icinde fonksiyon taniminda fonksiyonu inline yapmis oluyoruz.

> Inline koymasan bile inline olcak. Implicit inline fonksiyon. Inline koyarsan da hata olmaz.

**Dikkat:**

- Eger bir isim sinifin uye fonksionu icinde nitelenmeden kullanilmissa su sira ile aranir:

1. Kullanildigi blok icinde
2. Onu kapsayan blok icinde 
3. Onu kapsayan blok icinde 
4. Class scope

**Örnek:**

```CPP
class Myclass{
public: 
    void foo();
private:
    int a,b;
    int x;  // non-static member
};

void Myclass::foo()
{
    x; 
}
```
> Burada x kullandigimda isim arama ile bunun non statci data member oldugu anlasiliyor.

> Bu x icin kod uretilirken fonksiyonun gizli parametre degiskeni olan pointerin gosterdigi nesnenin x i.

**Redecletarion konusunda not:**
- Global fonksiyonlar icin redecleration soz konusudur ama class member function lari class definition icinde yeniden bildirilemez.

```CPP
class Myclass {
public:
    void func(int);
    void func(int);
};
```

## this Keyword'u
- Bu anahtar sozcuk yalnizca sinifin non-static uye fonksiyonlari icin kullanilabilir.
- Global bir fonksiyon icidne sinifin static uye fonksiyonu icinde kullanilmi sentaks hatasidir.
- Birlikte kullanildigi nesnenin adresi anlamina geliyor.
- this ifadesinin value category si PR value expression.

> this bir pointer , * this bir sinif turudnen nesne. L value expression.

### this neden var?

- Bazi durumlardan this kullanmadan derdimizi ifade etmenin bir baska yolu var. Nedir bunlar?

**Ornek:**
- Bir sinifin uye fonksiyonunun global bir fonksiyona cagri yapmasi gerekiyor. Global fonksiyonun parametresi Myclass*. Ama bizim fonksiyonumuz hangi nesne icin cagirildiysa o nesnenin adresi ile fonksiyona gonderilmek isteniyor.

```CPP
class Mylass {
public:
    void f();

private:
    int x;
    int y;
};

void foo(Myclass*)
void bar(Myclass)
void baz(Myclass&)

void Myclass::f()
{
    foo(this);
    bar(*this);
    baz(*this);
}
```

## Const member functions

**Const correctness:** : Const olmasi gereken her sey const yapilir mi?

**Not:**
- C++ dili olusturuldugu zaman c++ derleyicisi de yoktu. Kodlar c nin onislemci programi kullanilac=rak derleniyordu.
- Yani derleme isini c derleyicisi yapiyordu. Onlislemci prigramin komutlari kullanilarak c++ kodunu c diline donusturen onislemci programi vardi.

**Siniflarin const non-static uye fonksiyonlari 2 kategoride olabilir**

1. const membr function ->  () sonrasinda const keyword kullanimi
2. non - const member function

```CPP
int main()
{
    const vector<int> x{1,2,3,4,5};

    x.front()= 23;
    auto y = x.front();
}
```
> ustteki sentaks hatasi. Const olamdiginda sentaks hatasi vemiyor.
Const overloading yapiyor.

# Ders 10 Alıştırmalar

**Soru 1: Hata Nedir?**

```CPP
class Myclass {
public:
    void foo();
};

int main()
{
    Myclass::foo();
}
```

**Cevap:**
> Namelookup ta bir sorun olmaz. Derleyici :: opratoru ile nitelenmis bir isim gordugunde bu ismi class scope ta arar. Name lookup biter.

> Yani isim classtaki fonksiyonun ismi. Hata namelookup ile ilgili degil. Context kontrolune takiliyor. 

> Bu bir non-static uye fonksiyon. Bu fonksiyonun cagirilmasi icin ortada bir Myclass nesnesinin olmasi gerekir ama bir myclass nesnesi yok. Fonksiyon static olsaydi gecerli olacakti.

**Soru 2: Hata Nedir?**

```CPP
class Myclass {
public:
    void foo();
};

int main()
{
    Myclass m;
    foo(&m); 
}
```

**Cevap:**
> namelookup hatasi, foo ismi bulunamadi.

> Myclasss::foo(&m) Yazsaydik, Yine hatanin nedeni namelookup degil, fonksiyonun cagirilmasi yanlis.

**Soru 3:**

```CPP
class Myclass{
public:
    void foo();
private:
    int x;
};

Myclass g;

void Myclass::foo()
{
    g.x = 10;
}
```

**Cevap:**

> Sinifin uye fonksiyonu icinde sinifin private ismi kullanilabilir.

**Soru 4:Function overloading mi?**

```CPP
class Myclass{
public:
    void func(int);
private:
    void func(int, int);
}
```

**Soru 5: Hangi fonksiyon cagirilacak**

```CPP
class Myclass{
public:
    void func(int);
private:
    void func(double);
};

int main()
{
    Myclass m;
    m.func(2.3);
}
```

**Cevap:**
> Once functoin overload resolution yapilacak. Double parametreli olan kazanacak. Access control yapilacak. Private double parametreli oldugundan derleyici access control hatasi verecek.

> Yani access conrol function overload resolution dan daha sonra yapiliyor.

**Soru 6: Kod legal mi?**

```CPP
class Myclass{
public: 
    void foo()
    {
 
    }
    void func()const
    {
        foo();
    }
}
```

**Cevap:**
> Illegal. func parametresi const Myclass* ama foo parametresi Myclass*

> Bu yazilirken ayni zamanda derleyiciyi const T* dan T* a ortulu tur donusumune zorluyorum.

**Soru 7: Kod legal mi?**

```CPP
class Myclass{
public: 
    void foo()
    {
        func();
    }
    void func()const
    {

    }
}
```

**Cevap:**

> Legal. Buradaki donusum T* dan const t* turune. Yani kisaca sinifin const uye fonksyinonlari sinifin non-const uye fonksiyonlarini dogrudan cagiramaz.

> Ama sinifin non cost uye fonsiyonlari const uye fonksiyonlarini ismi ile cagirabilir.

**Soru 8: Kod legal mi?**

```CPP
class Myclass{
public: 
    void foo()
    {
        func();
    }
    void func()const
    {

    }
}

int main(){
    Myclass m;

    m.foo();
    m.func();
}
```

**Cevap:**
> Legal. Birisi myclass* dan myclass* a donusum, Digeri myclass* dan const myclass * a donusum.

**Soru 9: Kod legal mi?**

```CPP
class Myclass{
public: 
    void foo()
    {
        func();
    }
    void func()const
    {

    }
}

int main(){
    const Myclass m;

    m.foo();
    m.func();
}
```

**Cevap:**

> foo cagrisi error. func legal. const t* dan t* donusum yok.

**Soru 10: Kod legal mi?**

```CPP
class Myclass{
public:
    Myclass* foo()const
    {
        return this;
    }
}
```

**Cevap:**

> illegal. This pointer degeri sinif nesnesinin adresi. Sinif nesnesi const. This in degeri olan adres const t*

> Ama geri donus degeri Myclass* oldugundan const t* dan t* donusumune zorluyorum.

# Ders 11

## Sinifin const uye fonksiyonlari:

**Bir sinifin non-static uye fonksiyonlari**
1. const olabiliyor
2. non-const olabiliyor.

```CPP
class Nec{
public:
    void set(int);  // parametre degiskeni Nec*
    int get()const; // int get(const Nec*) // yani fonksiyonun gizli parametre degiskeni, low level const pointer.
};
```
> Const uye fonksiyonlar kendisini cagiran fonksiyona, bu nesnenin degerini degistirmeyecegi garantisini veriyor.

> Nesneler problem domeninde aslinda varligi temsil ediyor. Bu sebeple o varligin problem domeninde obsevable state i var. (Gozlenebilir durum)

> Ornegin fighter nesnesi bircok silaha sahip olabilir. Bu observable state i arttiriyor.

> Ornegin, nesnenin veri elemanlari degismiyor ancak degeri (observable state) degisiyor.

> Ornegin, nesnenin veri elemanlari degisiyor ancak degeri (observable state) degismiyor.

**Dikkat!**
- Sinifin tum veri elemanlari (non-static data members), sinifin nesnesinin observable state i dogrudan ilisliki olmayabilir.
- Yani sinifin bir veri elemaninin degeri degistiginde sinif nesnesinin degeri degismek zorunda degil.

```CPP
class Date{
public:
    void print()const
    {
        ++m_debug_count;
        m_crashed_value += 365;
    }
private:
    int mm, md, my;
    mutable int m_debug_count;
    mutable int m_cashed_value;
}
```
> mutable verdigimiz nesneler dogrudan nesnenin observable state i ile ilgili degil. const nesneler icin de const uye fonsiyonlari icin de bu degiskenlerin degerinin degismesi semantik acindan bir hata degil. Boylece derleyici bu kontrolu yapmayip bunu legal kontrol edecek.

**mutable:**
- Derleyici const uye fonksiyonlari icinde sinifin bu elemaninin degerinin degismesini legal kabul et. 
- const nesneler icin bu veri elemanin degerinin degismesini legal kabul et.

## Constructor - Destructor
- Bir sinif nesnesinin hayata gelmesi, kullanilablir bir varlik haline donusmesi, sinifin bir uye fonksiyonu tarafindan gerceklestiliyor. Bu tur fonksoyonlara constructor deniliyor.
- Her nesneyi hayata bir constructor fonksiyona yapilan cagri getiriyor.
- Bir sinif nesnesinin hayatinin bitmesi onun destructor fonksiyonunun cagrisi ile gerceklesir.
- Constructor ismi sinif ismi ile ayni olmak zorunda

```CPP
class Myclass{
public:
    Myclass();
    Myclass(int);  // constructorlar da overload edileblir.
};
```
> void olmasi ile geri donus degeri olmamasi durumu farklidir. Constructer lar geri donus degeri kavrani yok.

## Destructor
- non-static uye fonksiyonu olmak zorunda.
- ismi sinif ismi ile ayni olacak ama basinda ~ karakteri olacak. ~Myclass
- overload edilemiyor, parametre degiskeni olmamak zorunda.
- Constructor ismi ile(nokta ya da ok operator ile) cagrilmiyor ama destructor cagirilablir. Bu legaldir. Ama dogru diyemeyiz.
- Default contructor aslinda arguman gonderilmeden cagrilabilen constructor.

## Special member functions:
- Bu fonksyonlarin kodlari (tanimlari) belirli kosullar saglandiginda derleyici tarafindan yazilabiliyor. 
- Derleyicinin bir fonksiyonun kodlarini yazmasi icin kullanilan terim, derleyicinin o fonksiyonu default etmesi.
- Biz hic constructor tanimlamasak derleyici sinif icin bir default constructor default eder.

**Default contruct olayi 2 farkli sekilde olablir:**

1. Dil kurallarina gore implicitly olarak derleyici bu fonksiyonlari bildirebilir ve bizim icin bu fonksiyonlarin kodlarini yazabilir.
2. Programci derleyiciden bu fonksiyonlarin kodunu yazmasini isteyebilir.

**6 tane special member function var.**

- default constructor
- Desctructor
- copy constructor
- move constructor
- copy assignment
- move assignment

**Constructor, destructor programin neresinde cagiriliyor?**
- global sinif nesneleri icin main fonk. cagirilmasindan once, 
- destructor: main fonk. calismasindan sonra.

**Örnek:**

```CPP
//#include <stdio.h>
#include <iostream>

class Myclass {
public:
    Myclass()
    {
        std::cout << "default ctor this:" << this << '\n';
    }
    ~Myclass()
    {
        std::cout << "destructor this:" << this << '\n';
    }
};

Myclass g1;
Myclass g2;
Myclass g3;

int main()
{
    std::cout << "main basladi\n";
    std::cout << "main sonra eriyor\n";
}
```
**Dikkat!**
- Farkli kaynak dosyalarda tanimlanmis global sinif nesnelerinin hayata gelme sirasi belirli degil.
- Static initialization Fiasco: Farkli kaynak dosyalardaki global degiskenlerin hayata gelme sirasi dil tarafindan belli degil.

## static yerel sinif nesneleri

**Örnek:**

```CPP
#include <iostream>

class Myclass {
public:
    Myclass()
    {
        std::cout << "default ctor this:" << this << '\n';
    }
    ~Myclass()
    {
        std::cout << "destructor this:" << this << '\n';
    }
};

void foo()
{
    std::cout << "foo cagrildi";
    static Myclass m;
}

int main()
{
    std::cout << "main basladi\n";
    foo();
    foo();
    foo();
    foo(); 
    foo();
    std::cout << "main sonra eriyor\n";
}
```

> foo cagirildiginda nesne hayata geliyor, statik omurlu oldugundan dolayi tekrar cagirildiginda zaten hayatta oldugu icin tekrar hayata gelmiyor. main fonksiyonu bittkten sonra nesnenin hayati biitiyor.

## Otomatik omurlu sinif nesneleri:
- constructor o nesnenin olusturyldugu noktada cagirilacak ve o nesnenin scope unun sonunda destructor cagirilacak.

## Dinamik omurlu nesneler:
- C++ dilinde dinamik omurlu nesneler operatorler ile hayata getiriliyor.

```CPP
new operators
delete operators
```
> Bunlar dilin anahtar sozcukleri.

**Dikkat!**
- new ve delete malloc ve free nin karsiligi degil.
- new dinamik omurlu nesne olusturmanin, delete ifadesi bir nesnenin hayatini sonlandiran ifade.

**Açıklama: new Fighter yazıldığında neler olacak?**
> sizeof fighter kadar bir bellek alaninin elde edimesi gerekiyor. Bunun icin bi alocation fonksiyonunnun cagirilmasi gerekiyor. C dilinde olsaydik burada malloc cagirilacakti. C++ dilinde default olara cagirilan fonksiyon:

> operator new fonksiyonu.

- new operatoru ve operator new fonksiyonu farkli. operator new standart c++ kutuphanesinin bir fonksiyonu. malloc gibi.

```CPP
void* malloc (std::size_t)
void* operator new(std::size_t)
```

- parametrik yapi acisindan malloc ve operator new fonksiyonlarinin bir farki yok. 
**Aradaki fark:** 
- parametreye aktarilan tam sayi degeri olan byte kadar blok elde etmeye calisiyor.

> malloc fonk. basarisiz oldugunda nullptr donduruyor. basarili olursa alocate edilmis bellegin adresini donduruyor.

> Ama operator new basarisiz oldugunda exception throw ediyor. Bu exception handling arac seti ile ilgili. 

> Yani new operatoru demek baska, operator new fonksiyonu demek baska.

**Örnek Kod:**

```CPP
int main()
{
    std::cout << "main basladi\n";
    auto p = new Nec;
    p->func();

    delete p;

    std::cout << "main devam ediyor\n";

}
```

### delete ne yapiyor?

> Once sinifin destructor ini cagiriyor. 

p-> ~Fighter();

> operator new ve operator delete, standart kutuphanenin fonksiyonlarinin isimleri. 

> operator new malloc ile ayni parametrik yapida, operator delete free ile ayni parametrik yapida.

```CPP
void operator delete(void *p)
void free(void *vp)
```

**Yani:**

**new = operator new cagrisi + constructor cagrisi**
**delete = distructor cagrisi + operator delete cagrisi**

### delete unutulursa ne olur?

> delete unutulursa destructor ve operator delete cagrilmayacak. Bellek sizintisi, operator delete in cagrilmamasinin sonucu. 

> Ornegin dimanik omurlu bir nesneyi new ifadesi ile olusturuldu. Bir bellek alani alocate edildi. Bu delete edilmezse bu bellek alani free store a geri verilmeyecek. Isin bu tarafi memory leak, bellek sizintisi olarak ifade edilebilir.

> Ama burada problem cogu zaman bellek sizintisi ile sinirli degil. Cunku destructor cagirilmiyor. Bunun sonucunda RAII idiomu devreye giriyor.

> Bircok sinif turu icin, bir nesnenin kullanilabilmesi icin o nesne hayata getirildiginde bir veya birden fazla kaynagin o nesneye baglanmasi, o nesnenin o kaynagi ya da kaynaklari kullaniyor duruma getirilmesi saglaniyor. Bu kaynaklara recource deniliyor.

> Bu resource bir bellek alani olabilir, bir dosya, veri tabani baglantisi, mutex, network baglantisi ... olabilir.

> Yani bir nesney hayata getirdigimizde cagirilan constructor bir kaynak ediniyor. cinku o nesnenin isini gorebilmesi icin o kaynaklari kullanabilmesi gerekiyor.

> Nesnenin destructor i cagirildiginda destrucor bu kaynaklari geri veriyor. C dilinde olsaydi handle sistemi kullanilacakti. Nesnenin kaynak edilmesini saglayan bir global fonksiyona cagri yapiyor olacaktik. (fopen, createwindow gibi)

> O nesne ile is bittiginde open ya da create donksiyonunun geri dondurdugu adresi (bu adreslere handle deniliyor) kaynaklari geri verecek, temizlik islemlerini gerceklestirecek bir fonksiyona arguman olarak gonderilir.

> C++ dilinde bu otomatik. Constructor open ya da create fonksiyonunun yaptigi isi yapiyor, destructor da clean foksiyonunun yaptigi isi yapior.

> Constructor kaynagi ediniyor, destructor kaynagi geri veriyor.

> delete unutulursa destructor cagirilmayacak. Eger destructor kaynak iade ediyorsa o kaynaklari geri veremiyecek. Buna resource leak deniliyor. Memory bir resource ama resource memory degil. 

**Nasıl bir sentaks ile değişken tanımladığımda sınıfın default constructor unun çağırılması söz konusu?**

1. Default initialization
2. Value initialization

- Yani burada bir sınıf nesnesi value initialize edildiğinde default constructor çağırılacak.

**Not:** Bir sınıfın default constructor ı olmak zorunda değil. (not declared)

**Örnek:**

```CPP
#include <iostream>

class Nec {
public:
	Nec(int);
}; // Nec sınıfı için int parametreli bir constructor yazıldı. Derleyici bu sınıf için bir default constructor implicit declared yapmıyor.(Örtülü bir default constructor bildirmiyor)

int main()
{
	Nec x;
}
```
> Hata: C++ no default constructor exists for class "Nec"

> Yani bu şekilde nesne tanımlamak için derleyicinin default constructor a çağrı yapması gerekiyor ama default constructor yok.


**Örnek:**

```CPP
#include <iostream>

class Nec {
public:

}; 

int main()
{
	Nec x;
}
```
> Burada ise dilin kurallarına göre default cosntructor imlicip declared. hata yok.

### Special member function:
> Bu fonksiyonlarin kodları derleyici tarafindan yazilabiliyor.

> Derleyicinin bir kodu bizim yerimize yazmasina da derleyicinin o fonksiytonu default etmesi deniliyor.

> Yani special member functionlar derleyici tarafindan default edilebilen fonksiyonlar.

**Kac tane special member function var?**

1. Default cosntructor 
2. destructor
3. Copy cosntructor 
4. Move constructor        Since (C++ 11)
5. Copy assignment
6. Move assignment     	Since (C++ 11)

**User declared - defaulted:**
> Fonksiyonu ben bildiriyorum ama tanimlamayi derleyiciye birakiyorum.

==============================
- user declared - defined 
- user declared - defaulted 
- user declared - deleted

**Örnek:**

```CPP
#include <iostream>

class Nec {
public:
	const int x;
}; 

int main()
{
	Nec x;
}
```
> Bu sinifin default constructer i var, Derleyici bildirdi. Bu sinifin default cosntructor i deleted. Derleyici implicitly declere etti ama deleted olarak.

**Örnek:**

```CPP
#include <iostream>

class Nec {
public:
	Nec(int x)
	{
		std::cout << "Myclass(int x) x =" << x << "\n";
	}
}; 

int main()
{
	Nec x1(10); // direct init
	Nec x2{20}; // direct list init
	Nec x3 = 92; // Copy init

	Nec x4 = (4,5); 
	Nec x5 = {6,7}; 
	Nec x6 = {9,12}; 
}
```

## Constructor initializer list:

> Cosntructor bir sınıfın nesnelerini hayata getiriyor. Hayata getirmek demek, nesnenin non-static veri elemanlarını initialize etmesi demek.

> Bu non-static veri elemanlarını initialize etmek için contructorların kullandığı sentaksa, constructor initializer lsit deniyor.

1. Yalnızca ctor lar için kullanılabilir.
2. non-static veri elemanalrını init eder.

```CPP
#include <iostream>

class Myclass {
public:
    Myclass() : mx(10), my(20), md(9.8)  // Bu constructor çağırıldığında mx,my,md yi değerler ile init edecek.
    {   

    }
}
```
- Eğer programın akışı bir sınıfın contructor ının ana bloğu içindeki kodları yürütmekteyse, zaten sınıfın tüm veri elemanalrı hayata gelmiş demektir.
- Yani constructor ana bloğu içinde sınıfın veri elemanlarinin kulanirsam init edilmis veri elemanlariin kullanmmis oluyorum.

```CPP
Myclass() : mx{10}, my{20}, md{9.8} // C++11 standartları ile bu tanımalma geldi.
```

**Soru : Tüm veri elemanlarıın bu sentaks ile init etmek zorudan miyim?**
> Sadece mx yazsam digerleriini belirtmesem sentaks hatasi olmaz.

> Ama init edilmemis ogeler default init edilmis sayiliyor. Bu cop degerde birakilmasi demek.

```CPP
Myclass() : mx{10}, my{20}, md{9.8}
Myclass()
{
    mx = 10;    // assignment
    my = 20;    // assignment
    md = 9.8;   // assignment
}
```
> Bu iki tanimlama arasinda fark var. Ikinci tanimlamada once init ediliyor sonra atama yapiliyor. Bunlar initializer degil, assignment.

> Bizim ilk tecihimiz constructor init list olmali.

**Not:** Her zaman veri elemanlarıının hayata gelme sırası, sınıf bildirimindeki sıradır.

```CPP
class Myclass{
private:
    int mx{10};
    //defeult member initializer
    //in class initializer
}
```

[Ders 11 Ornek koddlar > calistir](https://github.com/TalhaAbus/CPP_Notlarim/blob/main/Ders%2011%20kodlari.md)

# Ders 12

**Bir sınıfın özel üye fonksiyonlari 3 statude olabilir.**

- not declared: fonksiyon yok demek
- user declared: programci fonksiyonu bildirmis demek
- implicitly declared: derleyici dilin kurallarina dayanarak fonksiyonu bildirmis.

**User declared: 3 ihtimal**

- User declared defined: programci bildiriyor ve tanimliyor
- User declared defaulted: Programci bildiriyor ama derleyicinin tanimlamasini istiyor.
- User declared deleted: Programci bildiriyor ama delete ediyor. (Bunu cagirilmasi sentaks hatasi)

### Derleyici bir ozel uye fonksiyonu nasil yaziyor?

- Her ozel uye fonksiyonu icin derleyicinin yazdigi fonksiyonun nasil yazilacagini belirleyen kurallar var:

**Derleyici tarafindan default edilen "default ctor", sinifin:**

non-static, public, inline fonksiyonudur.

**Implicityli declared:**

1. Derleyici tanimiyor
2. Derleyici ortulu bildirdigi fonksiyonu delete ediyor.

**Not:** 
> Eger derleyici bir special member fnction u default ettiginde dilin kuralarini cigneyen bir durum olusursa derleyici sentaks hatasi vermek yerine defaukt etmesi gerektigi fonksiyonu delete eder.

**Neden sentaks hatasi olusabilir?**
- default init edilemiyor olabilir. (Referans veya const tur.)
- Olmayan bir fonskyina cagri olabilir.
- Private fonksiyona cagri 
- Deleted fonsiyona cagri

**Ornek:**
```CPP
class Nec {
public:

private:
	const int x;
};
```
> Derleyici Myclass icin dil kurallarina gore default constructor i default etmek zorunda ve derleyicinin yazdigi default cosntructor elemanlari default init etmek zorunda.

> Burada const bir nesne default init edilemez. Bu durumda derleyicinin yazmasi gereken default constructor sentaks hatasi olusturacak. 

> Burada derleyici sentaks hatasi vermek yerine sinifin default constructor ini delete edecek.

**Ornek:**

```CPP
class Nec {
public:

private:
	const int x;
};

int main{
    Nec m;
}

```
> Sentaks hatasi : delete edilmis fonksiyona cagri.

**Ornek:**

```CPP
class Nec {
public:

private:

};

class Myclass {
public:

private:
	Nec mnec;
};

int main(){
	Myclass m;
}
```
**Analiz:**
> Derleyici Myclass icin default constructor yazdi. Derleyicinin yazdigi default constructor, sinifin private veri elemani olan Nec turudnen mnec isimli elemani default init etti.

> Bu default constructor cagirilmasinda bir engel yok.

**Ornek:**

```CPP
class Nec {
public:
	Nec(int);
};

class Myclass {
public:

private:
	Nec mnec;
};

int main(){ 

}

```
**Analiz:**

> Suan Nec in default constructor i yok. Myclass sinifi icin derleyici default constructor yazmak zorunda ve Myclass sinifi icin derleyici default cosntructor yazmak zorunda. Burada eleman olan mnec icin de default constructor cagirilmak zorunda ama default constructor yok.

> Bu durumda sentaks hatasi olusmasi gerekiyor. Bunun yerine Myclass sinifinin default constructor ini delete edecek. Burada sentaks hatasi alcagim durum: Myclass sinifinda default constructor gerektirecek bir nesne olusturmak.

**Ornek: **

```CPP
class Nec {

	Nec();
};

class Myclass {
public:

private:
	Nec mnec;
};

int main(){ 

}
```
**Analiz:**
> Myclass sinifinin default constructor i suanda deleted.

> Nec constructor i private. Private olan default constructor a yapilan cagri sentaks hatasi. Derleyici Myclass sinifi icin yazdigi default constructorda eleman olan mnec icin default constructor a cagri yapcak. Bu da private oldugu icin sentaks hatasdi olusturacak. 

> Bu durumda derleyici Myclass sinifinin implicitly devlared olan default constructor ini delete edecek. 

> Yani Myclass default constructor i derleyici tarafindan delete edilmis durumda. Ama bunun nedeni private fonksiyona yapilan cagri.

**Not:**
> Derleyici, eger bir sinifin special member function i implicityly declared ise ve derleyici bu ozel uye fonksiyonu default ederken bir sentaks hatasi olusursa (yazilmasi gereken kod dilin kuralarina ayriki duruma duserse) bu durumda derleyici yazmasi gereken special member function i delete ediyor.

**Ornek:**

```CPP
#include <iostream>

class Myclass {
public:

    void print()const
    {
    std::cout << mx << " " << my << "\n";
    }
private:
    int mx;
    int my;
};


int main()
{
    Myclass m;

    m.print();
}
```
> mx ve my cop degerde. Bunlari kulanmak UB. Neden cop degerde?

> Cunku derleyicinin yazdigi default constructor bunlari default init etti. Default init demek garbage value demek.

**Ornek :**

```CPP
#include <iostream>

class Myclass {
public:

    void print()const
    {
    std::cout << mx << " " << my << "\n";
    }
private:
    int mx{10};
    int my{35};
};


int main()
{
    Myclass m;

    m.print();
}

```
> Burada ise UB yok. Myclass sinifinin default constructor ini derleyici yazdi. Ama yazarken default member initializer a bakti ve bu degerler ile init edecek sekilde default constructor i yazdi.


**Notlar:**

- Bircok dilde (nesne yonelimli programlamaya destek veren) constructor kavrami var. Fakat destructor bircok dilde yok. Destructor olmasi aslinda RAII idiomu ile ilgili.

> Bir sinif nesnesi kaynak kullanacaksa, kullandigi kaynagi sinif nesnesine baglayan constructor yolu ile kaynagi ediniyor. Fakat bu kaynagi nesne hayatta oldugu surece kullanacak. Nesnenin hayati bittigi zaman bu kaynagin geri verilmesi gerekiyor.

> C dilinde bu kaynagin geri verilmesini bir fonksiyona cagri yaparak gerceklestirecektik ve bunu unutma ihtimali de var. Fakat C++ dilinde destructor kavrami bu olayi otomatik yapiyor.
RAII kisaca: kaynagin edinilmesi ve geri verilmesi.

**Ornek: Copy constructor **

```CPP
#include <iostream>

class Nec {
public: 
	Nec()
	{
		std::cout << "default ctor this" << this << "\n";
	}
	~Nec()
	{
		std::cout << "destructor this" << this << "\n";
	}
};

void foo(Nec x)
{

}

int main()
{
	Nec mynec;

	foo(mynec);
	(void)getchar();
}
```
**Çıktı:**

default ctor this000000E5338FF854
destructor this000000E5338FF830

destructor this000000E5338FF854

**Peki burada fonksiyonun parametre degiskeni icin destructor cagirildi ama constructor cagirilmadi, neden?**
**Cevap:** onun icin de constructor cagirildi, onunu icin cagirilan cosntructor default constructor degil. Copy constructor.

## Copy Constructor : 3. special member function

1. ogrendigimiz default constructor
2. desctructor
3. copy constructor

> Bir sinif nesnesi hayata degerini ayni turden bir baska sinif nesnesinden alarak getirildiginde burada sinif nesnesini hayata getirecek constructor, sinifin copy constructor i.

**Ornek:**

```CPP
Student batuhan 
Student korhan= batuhan;
```

> Batuhan hayatta olan bir sinif nesnesi.

> Ayni turden korhan degiskeni olusturdum. Bu degiskenin degerini batuhan ile ayni olmasini istiyorum. Yani korhan da ayni turden bir sinif degiskeni olsun fakat degerini batuhandan alsin. Yani surec tamamlandiginda korhan ve batuhan ayni degerde ama birbirinden farkli 2 degisken olsun.

> Iste bu durumda cagirilan korhani hayata getirecek fonksiyon, student sinifinin copy constructor i.

**Derleyici tarafindan yazilan copy constructor sinifin:**
- non - static, public, inline üye fonksiyonudur.

```CPP
class Nec{
public:
	Nec(const Nec&);
private:
	A ax;
	B bx;
	C cx;
};
```
> Nec, ismi sinif ismi ile ayni oldugu icin bir constructor. Ama sinif turunden parametreye sahip oldugu icin bu bir copy constructor. 

```CPP
Nec x;
Nec y = x;
```
> Bu sekilde bir nesne olusturdugumuzda x hayata gelmiyor, hayata gelen y. 

> Burada this pointer i hayata getirilecek olan nesnenin adresi olduguna gore (constructor icinde) y nin adresidir.

> Burada x aslinda fonksiyona referans semantigi ile arguman olarak gonderiliyor.

> Bazi durumlarda ise sinifin copy constructor ini kendimiz yamamiz gerekecek. Cunku derleyicinin yazdigi copy consttuctor bizim icin uygun olmayacak.

> Derleyicinin yazdigi copy constructor dogrudan elemanlari birbirine kopyaliyor. Elemanlarin pointer olmasi durumunda bir pointerin degeri bir baskasina aktariliyor ayni ikisi de ayni adresteki nesneyi gosteriyor.

**Eger bir sinifa destructor yaziyorsaniz %99 bu sinif icin copy constructor da yazmalisiniz.**

### Operator overloading: 
- Bir sinif nesnesi bir operatorun operandi oldugunda derleyici bunu fonksiyona yapilan bir cagriya donusturuyor. Burada cagirilan fonksiyonlara operator fonksiyonlari deniliyor.

### Copy assignment function:
- bir sinif nesnesine ayni turden aska sinif nesnesi atandiginda.

> Hayatta olan bir sinif nesnesine = yine hayatta olan bir baska sinif nesnesini atama operator ile atadigimizda bir fonksiyon cagiriliyor. 

**Örnek:**

```CPP
class Nec{
public:
	Nec& operator=(const Nec& other);
private:
	A ax;
	B bx;
	C cx;
};
```
necx = necy;
Burada aslinda 
necx.operator=(necy);
fonksiyonu cagiriliyor.

> Burada this pointer i necx in adresi
other in adresi = necy nin adresi

**Hatirlatma:** Atama operatorunun urettigi deger nesneye atanan degerdir.

### Move Semantics:
- Oyle yerler var ki biz bir nesneyi hayata getirirken, degerini bir baska nesneden alarak hayata gelemsini istiyoruz.
```CPP
T x = other;
```
Copy constructer ne yapiyordu:
```CPP
T x = other;
```
- Bu nesnenin kaynagina esdeger bir kaynak edinecek ve bu nesnenin kaynagindan kendi kaynagina kpyalama yapacak.
- Atama durumunda: kendi kaynagini geri verecek, yeni kaynak edinecek ve edindigi yeni kaynaga diger nesnenin kaynagindan kopyalama yapacak.

**Baska bir senaryo:**
```CPP
T x = other;
```
> other ile ifade ettigimiz nesnenin hayatinin bitmekte oldugunu, bu nesneyi kullanacak baska bir kodun olmadigindan emin olalim. Bu durumda bu nesnenin kaynagini kopyalamak gereksiz olacak ve bu nesne de hayati bittiginde kaynagini geri vermis olacak.

> Burada boyle bir kod calisacagina, bizim nesnemizin pointer i diger nesnenin pointerini kopyalasin. Yani onun kaynagini kullanir hale gelsin. Other icin destructor cagirildiginda bizim destructor geri cerilmesin.

> Yani hayati bitecek olan nesnenin hayatinin biteceginden emin isek onun kaynagini calabiliriz.

```CPP
T x = expr;
```
> Sagdaki ifade hayati bitecek olan, baska kodlarin kullanamayacagi bir nesne anlamina geliyorsa, (compile time da) farkli bir kodu sececek, hayati devam edecek bir nesne ise baska bir kodu sececek.

> expr, hayati bitecek olan bir nesne ise yani baska bir kodun bunu kullanma ihtimali yoksa bu ifade R value expression.

> Yani bir ifade PR value veya X value ise bu sinif nesnesini kullanacak baska bir kod yok. Bunun kaynagi calinabilir.

> Ama ifadenin deger kategorisi L value expression ise o kaynagi kopyalamamiz gerekiyor. Nesne zaten hayatta, eger calinirsa nesne kullanilamayacak bir duruma duser.

> Bir ifade R value expression ise ve sinif nesnesi ise, o sinif nesnesinin baska bir kod tarafindan kullanilma ihtimali yok.

```CPP
class Myclass{
public:
	Myclass(const Myclass&);	// copy constructor
	Myclass(Myclass&&r);	// move constructor
};
```
> Derleyici koda bakarak fonksiyona gonderilen argumanin value categorysinin ne oldugunu anlayarak function overload resolution ile ustteki veya alttaki fonksiyonu cagiracak.

> Ustteki kaynak kopyalamaya yonelik olusturulmus, alttaki kaynak calmaya gore olusturulmus.

**Örnek:**

```CPP
class Myclass{
public:
	Myclass();
	Myclass(const Myclass&);	// copy constructor
	Myclass(Myclass&&r);	// move constructor
};

Myclass foo();

int main()
{
	Myclass x;
	Myclass y = foo();
}
```
> Y yi hayata getirmek icin alttaki fonk cagirilir cunku foo() R value expression.

> Yani biz bir nesneyi L value expression olan bir ifade ile hayata getirdigimizde onun kaynaginin kopyalanmasinis saglayacaz.

> Ama nesneyi hayata getirirken ona ilk deger verdigimiz ifade bir R value expression ise o zaman move constructor cagirilacak ve move constructor onun kaynagini calacak.

> Buradaki amac, zaten olecek bir nesnenin kaynagini alip, yeni nesne icin gereksiz kopyalama yapmanin engellenmesi. 

# Ders 12 Alıştırmalar
[Ders 12 kodları](https://github.com/TalhaAbus/CPP_Notlarim/blob/main/Ders%2012%20Kodlari.md)

# Ders 13

**Sinifin ozel uye fonksiyonlari:**

- Default constructor
- Destructor
- Copy constructor
- Move constructor
- Copy assignment
- Move assignment

> Bu fonksiyonlarin ortak ozelligi: derleyici bunlarin kodlarini bizim icin yazabiliyor. Bu yazma izlemine derleyicinin default etmesi deniyor.

**Bu fonksiyonlar:**
1. not declared
2. user declared
3. implicitly declared
olabilir.

**Eger user declared ise:**
1. user declared defined, programci tanimlayabilir.
2. User declared defaulted, programci bildirir ama derleyicinin tanimlamasini ister
3. User declared deleted: Programci bildirir ama delete edilmis olarak.  
**Cagirilmasi sentaks hatasi.**

**Hangi durumda derleyici ortulu olarak bildirdigi ozel uye fonksiyonu delete eder?**
> Derleyicinin yazdigi kodda bir sentaks hatasi olusursa, sentaks hatasi vermek yerine yazmasi gereken special member function i delete ediyor. Boylece implicitly declared deleted oluyor.


```CPP
class Nec{
public:
    Nec() : ax(), bx(), cx() {}
    ~Nec() {}
    Nec(const Nec& other) : ax(other.ax), bx(other.bx), cx(other.cx)

private:
    A ax;
    B bx;
    C cx;
}
```
**Derleyicinin yazdigi default constructor sinifin:**
non-static, public, inline fonksiyonudur.
- Sinifin butun elemanlarini default initialize ediyor. Bu cop deger ile hayata baslamak demek.

> Eger copy constructor yazmayiderleyiciye birakirsak derleyici sinifimizin her bir elemanini parametreye referans yolu ile baglanan diger nesnenin karsilikli elemani ile initialize edilecek.

> Sinifi kopyalama ve tasimaya kapatabiliriz,
Kopyalamaya kapatabilir, tasimaya acabiliriz,
Ya da her ikisine de acabiliriz.

```CPP
int x = y;
```
> int turden bir nesnenin tasinmasi soz kunusu degil. Primitiv turler icin tasima = kopyalama.

**Ama sinif turleri icin:**
```CPP
Myclass m2= m1;
```
> Boyle yazarsak Myclass sinifinin hem copy contructor i hem move constructor i varsa m2 yi hayata getirmek icin copy constructor cagirilir. 

```CPP
Myclass m2 = std:move(m1);
```
> Boyle olsaydi m2 yi hayata getirmek icin move constructor cagirilacakti.

**Not:** Bir nesneyi sag taraf referansina baglamak o nesneyi tasimak anlamina gelmez.

```CPP
string s = move(str);
```
> move fonksiyonu ile tasima gerceklestirmis olmuyorum, sadec value category degistiriyor.

**Örnek:**

```CPP
void func(const std::string& s)
{

}
int main()
{
    std::string s(10000, '+');
    func(s);
}
```
> Burada bir kopyalama yok, referans semantigi. Burada bir tasima da yok.

**Örnek:**

```CPP
void func(const std::string& s)
{
    std::string str(s);
}

void func(std::string&& s)
{
    std::string str(std::move(s));
}

int main()
{
    std::string s(10000, '+');
    func(s);
}
```
> L value olan string fonksiyonlari icin ustteki fonk. 

> R value olan string fonksiyonlari icin alttaki fonk.

> Burada function overloading yaparak func fonksyonuna gelen nesnenin deger kategorisine gore kaynagi kopyalama (copy ctor) veya calma islemi(move ctor) yaptiriyoruz. 

**Dikkat:** const bir sinif nesnesinin kaynagini calamazsiniz ve calmamalisiniz. Dilin kurallari buna engel olur.

**Örnek:**

```CPP
class Myclass{
public:
    Myclass() = default;
    Myclass(const Myclass&)
    {
        std::cout << "copy ctor\n";
    }
    Myclass(Myclass&&)
    {
        std::cout << "move ctor\n";
    }
};

int main()
{
    Myclass x;
    Myclass y = std::move(x);
}
```
> Derleyip calistirildiginda move ctor cagirilacak. 

> const Myclass x; yaparsak copy ctor cagirilacak.

> move fonksiyonu const bir neneyi aldiginda move un degi donus degeri const qualified R value expression.

**Special member functions** oyle fonksiyonlar ki bunlarin kodunu derleyici belirli kosullar saglandiginda bizim icin yaziyor.
**Hangi kosullarda bunu yapiyor?**
- Eger bir sinifa hicbir constructor yazilmazsa (special member function bildirilmezse) bu durumdaderleyici sinifin 6 ozel uye fonksiyonunu da default ediyor.
- Yani sinifi bu sekilde olusturmak ve hicbir special member fucntion yazmamak arasinda hicbir fark yok:

```CPP
class Myclass{
public:
    Myclass() = default;
    ~Myclass() = default;
    Myclass(const Myclass&) = default;
    Myclass(Myclass&&) = default;
    Myclass& operator = (const Myclass&) = default;
    Myclass& operator = (Myclass&&) = default;
};
```

**Eger sinifa parametreli bir cnstructor yazilirsa,**

```CPP
class Myclass{
public:
    Myclass(int);  // biz yazdik. Alttakileri derleyici yazdi

    Myclass(const Myclass&) = default;
    Myclass& operator = (const Myclass&) = default;
    Myclass(Myclass&&) = default;
    Myclass& operator = (Myclass&&) = default;

};
```
> Bir constructor yazdigimiz icin derleyici default constructor i default etmeyecek. 

Destructor
Copy constructor
Copy assignment
move constructor
Move assignment

default edecek.

> Yani sinifin default constructor i yok.

**Eger sinifa default cosntructor yazilirsa:**

```CPP
class Myclass{
public:
    Myclass();  // default constructor user declared

    Myclass(const Myclass&) = default;
    Myclass& operator = (const Myclass&) = default;
    Myclass(Myclass&&) = default;
    Myclass& operator = (Myclass&&) = default;

};
```
destructor
Copy constructor
Copy assignment
Move constructor
Move assginment 

default edecek.


**Eger sinifa destructor yazilirsa:**

```CPP
class Myclass{
public:
    ~Myclass();  // destructer user declared

    Myclass() = default;
    Myclass(const Myclass&) = default;
    Myclass& operator = (const Myclass&) = default;
};
```
default constructor
copy constructor
copy assginment

default edilecek.

> move vonstructor ve move assignment default edilmeyecek. Not declared durumunda. Bu cok tehlikeli bir durum.

> Eger destructor user declared yapilmissa muhtemeken bir kaynak iadesi yapiliyordur ve bu durumda copy cosntructor ve copy assignment in derleyici tarafindan yazilmasi istenmez. Yani eger sinifin destructor i user declared ise copy constructor ve copy assignment da user declared olmasi gerekir.

**Eger copy constructor i kendimiz yazarsak:**

```CPP
class Myclass{
public:
    Myclass& operator = (const Myclass&);

    ~Myclass();  
    Myclass& operator = (const Myclass&) = default;
};
```
> Bu durumda default constructor in durumu not declared.

**Kural:** Eger bir cosntructor yazarsaniz derleyici sizin icin default cosntructor yazmaz. Yani suanda default cosntructor not decalared.

Destructor 
copy assignment

Derleyici tarafindan yazilir.

**Copy assignment yazilirsa:**

```CPP
class Myclass{
public:

    Myclass& operator = (const Myclass&) = default;

    Myclass() = default;
    ~Myclass() = default;
    Myclass(const Myclass&) = default;

};
```
default cosntructor
destructor
copy constructer

derleyici tarafindan yazilir.


**Eger move cosntructor yazilrisa:**

```CPP
class Myclass{
public:
    Myclass(Myclass&&);

    ~Myclass() = default;
    Myclass(const Myclass&) = delete;
    Myclass& operator = (const Myclass&) = delete;

};
```
- Derleyici yine cosntructor yazmaz cunku bu da bir constructor. 
- Derleyici copy memberlari delete eder.
- Destructer yine yazilacak.

**Sinifa bir move assignment yazarsak:**

```CPP
class Myclass{
public:
    Myclass& operator = (Myclass&&);


    Myclass() = default;
    ~Myclass() = default;
    Myclass& operator = (const Myclass&) = delete;
    Myclass(const Myclass&) = delete;
};
```

**Soru: Bir sinifi kopyalama ve tasimaya kapatmak istiyorum.**

```CPP
class Myclass{
public:
    Myclass(const Myclass&) = delete;
    Myclass& operator(const Myclass&) = delete;

};
```
> Copy constructor ve copy assignment delete ediyoruz. Move memberlari delete etmeme gerek yok.

**Ornek: kopyalamaya karsi kapatilmis ama tasimaya karsi acilmis:**

```CPP
class Myclass{
public:

    Myclass();
    Myclass(int);

    Myclass(const Myclass&) = delete;
    Myclass& operator(const Myclass&) = delete;

    Myclass(Myclass&&);
    Myclass& operator = (Myclass&&);
};
```


**Yapilmamasi gereken bir ornek:**

```CPP
class Myclass{
public:

    Myclass();
    Myclass(int);

    Myclass(const Myclass&);
    Myclass& operator(const Myclass&);

    Myclass(Myclass&&)= delete;
    Myclass& operator = (Myclass&&) = delete;
};
```
> copy memberlar bildirilmis ama move memberlar delete edilmis. Tasima olmasi gereken yerde kopyalama yapilmasi gerekiyor, burada sentaks hatasi olur.

**Costructor ismi ile cagirilamaz:**

```CPP
Myclass m;
Myclass *ptr = &m;

m.Myclass();    // sentaks hatasi
ptr-> Myclass();    // sentaks hatasi
```

**Destructor ismi ile cagirilabilir ama cagirmayin.**

```CPP
m.~Myclass(); // gecerli bir kod 
ptr-> ~Myclass(); // sadece tek senaryoda yazilabilir, placement new operator ile ilgili.
```

**Oyle durumlar var ki, isimizi gerceklestirmemiz icin dinamik omurlu bir sinif nesnesini kendi temin ettigimiz bir bellek alaninda olusturmamiz gerekiyor.**

```CPP
class Myclass{
public:
    Myclass()
    {
        std::cout << "Myclass()\n";
    }
    ~Myclass()
    {
        std::cout << "~Myclass()\n";
    }
    int a[4]{};
};

int main()
{
        std::cout << "sizeof(Myclass)= " << sizeof(Myclass) << "\n";

        unsigned char buffer[sizeof(Myclass)];

        std::cout << "&buffer =" << &buffer << '\n';
        Myclass* p = new (buffer)Myclass;

}
```

**Cikti:**
> Ayni adresler gozukuyor. Yani benim nesnem buffer bellek alaninda hayata getirilmis oldu.

> Simdi nesneyi delete etmemiz gerekiyor ama direkt delete p; yazarsam felaket olur.

> Delete operetoru karsiligi aslinda derleyici once sinifin destructor ini cagiriyor. Sonra delete operatorunun operandi olan adresi operator delete fonksiyonuna gonderiyor.

- Bu yozden destructor direkt ismi ile cagirmamzi gerekiyor:

```CPP
p-> ~Myclass();
```

### Delegating constructor:
- Dile sonradan eklendi, diger dillerin etkisi ile.
- Oyle bir constructor ki, isi baska bir constructor a havale ediyor. Yani constrcutor nesneyi initialize etmek icin baska bir constructor cagiriliyor. Burada kullanilan sentaksa delegating constructor deniliyor.
- Bircok durumda sinifin birden fazla contructor inin ortak bir kodu oluyor.

## Geçici Nesneler (Temporary objects)
- Ayrı bir ömür statüsü aslında. Otomatik ömürlü nesneler geçici nesneler değil.
- Öyle durumlar var ki kodda bir değişken ismi görünmese de arka planda derleyici dilin kurallarına uyarak bir nesne oluşturuyor.
- Yani kaynak kodda direkt ismi olmayan ama üretilen kodda bir nesnenin hayat getirilmesi durumundaki nesnelere tempporary objeect deniyor. Bazı durumlarda da derleyici durumda bir vazife çıkartarak bir geçici nesne oluşturuyor.
- Bir geçici nesnenin hayatı o geçici nesne ifadesinin icinde bukundugu ifadenin degerlendirilmesinden (evaluate edilmesinden) sonra sona erer.

**Örnek:**

```CPP
class Myclass {
public:
	Myclass()
	{
		std::cout << "default ctor this:" << this << "\n";
	}
	~Myclass()
	{
		std::cout << "destructor this:" << this << "\n";
	}
	
	void foo()
	{
		std::cout << "Myclass foo() this:" << this << "\n";
	}
private:

};

int main()
{
	std::cout << "main baslıyor\n";
	Myclass{}.foo();
	std::cout << "main devam ediyor\n";
}
```

**Çıktı:**
main baslıyor
default ctor this:00000009800FFD54
Myclass foo() this:00000009800FFD54
destructor this:00000009800FFD54
main devam ediyor

**Sonuç:**
> Geçici nesnenin bulunduğu ifadenin yürütülmesinden sonra nesnenin hayatı sona ermiş olacak.

**Örnek:**
```CPP
class Myclass {
public:
	Myclass(int a, int b)
	{
		std::cout << "Myclass (int, int) a = " << a << "b = " << b << "\n";
	}
	~Myclass()
	{
		std::cout << "destructor this:" << this << "\n";
	}
	
	void foo()
	{
		std::cout << "Myclass foo() this:" << this << "\n";
	}
private:

};

int main()
{
	std::cout << "[1] main basladi\n";
	
	if (1) {
		Myclass&& r = Myclass{ 3,5 };
		std::cout << "[2] main decam ediyor\n";
		r.foo();
	}
}
```
**Çıktı:**
[1] main basladi
Myclass (int, int) a = 3b = 5
[2] main decam ediyor
Myclass foo() this:00000073B474FB74
destructor this:00000073B474FB74

## Reference Qualifiers:

Bir sınıfın non-static üye fonskiyonları 
1) Değer kategorisi L value olan sınıf nesneleri ifadeleri ile çağırılabilir,
2) Değer kategorisi R value olan sınıf nesneleri ifadeleri ile çağırılabilir

## Conversion Constructors:
- Bir special member funstion değil. Constructor ı niteleyen bir terim.
- Asıl varlık nedenininn yanında örtülü yada örtülü olmayan şekilde tür dönüşümü için kullanılabilecek constructorlar. Sınıf türünden olmayan bir ifafde sınıfın conversion cosntructorlarının kullanılmasıyla sınıf  türlerine dönüştürülebilirler.

**Örnek:**

```CPP
class Myclass{
public:

};

int main()
{
    Myclass m;
    m=12;
}
```
> Sentaks hatası, sebebi int türünden Myclass türüne bir dönüşüm yok. Ama bu sınıfa int parametreli bir constructoır bildirmiş olsam kod legal olacak.

**Örnek:**

```CPP
class Myclass{
public:
    Myclass() = default;
    Myclass(int);

};

int main()
{
    Myclass m;
    m=12;
}
```
> Kod legal oldu. Myclass türünden bir nesneye int türünden bir değer atayabiliyorum.

> Burada Myclass(int); sınıfın conversion constructor ı.

> Burada derleyicinin yazdığı:

> m = Myclass(12);

> Derleyici durumdan bir vazife çıkarttı ve geçici nesne oluşturdu. Geçici nesneyi oluşturmak için sınıfın int parametreli constructor ını kullandı.

**Kodu tekrar yazıp anlatalım.**

```CPP
class Myclass {
public:
	Myclass()
	{
		std::cout << "Myclass default ctor. this =" << this << '\n';
	}
	Myclass(int x)
	{
		std::cout << "Myclass (int x) x =" << x << "this " << this << '\n';
	}
	~Myclass()
	{
		std::cout << "Myclass default ctor. this =" << this << '\n';
	}
};

int main()
{
	Myclass m;

    m =5;

    std::cout << "main devam ediyor \n";
}
```
> m = 5 ifadesi yürütüldüğünde geçici nesnenin destructor ı çağırılacak. Ama main closing brace geldiğimizde diğer destructor çağırılacak. 

**Çıktı:**
Myclass default ctor. this =00000001000FF854
Myclass (int x) x =5this 00000001000FF934
Myclass destructor this =00000001000FF934
main devam ediyor
Myclass destructor this =00000001000FF854

> Buradaki atamayı da sınıfın move constructor ı gerçekleştiriyor. Ama ben sınıfa bir copy constructor yazarsam copy constructor cağırılacak.

```CPP
class Myclass {
public:
	Myclass()
	{
		std::cout << "Myclass default ctor. this =" << this << '\n';
	}
	Myclass(int x)
	{
		std::cout << "Myclass (int x) x =" << x << "this " << this << '\n';
	}
	~Myclass()
	{
		std::cout << "Myclass destructor this =" << this << '\n';
	}
	Myclass& operator = (const Myclass& other)
	{
		std::cout << "copy assignment func" << "\n";

		std::cout << "this =" << this << "\n";
		std::cout << "other =" << &other << "\n";
		return *this;
	}
};

int main()
{
	Myclass m;

	m = 5;

	std::cout << "main devam ediyor \n";
}
```
**Çıktı :**
Myclass default ctor. this =0000007A7EAFF7A4
Myclass (int x) x =5this 0000007A7EAFF884
copy assignment func
this =0000007A7EAFF7A4
other =0000007A7EAFF884
Myclass destructor this =0000007A7EAFF884
main devam ediyor
Myclass destructor this =0000007A7EAFF7A4

**Sonuç:**
Böyle bir dönüşüm çok tehlikeli. Tehlikenin bir örneği:

```CPP
class Myclass{
public:
    Myclass();
    Myclass(int x);
};

int main()
{
    Myclass m{23};
    int ival{};

    m = ival;
}
```
> Bir Myclass nesnesine yanlışlıkla int türünden  bir değer atarsam sentaks hatası değil, tür güvenliği açısından son derece riskli.

> Conversion cosntructor tahmin edilmeyen yerde dönüşümün otomatik olarka yapılması sebebiyle yanlış yazılmış bir kodun legal olmasını sağlayabilir.

**Çok önemli bir kural:**

```CPP
class Myclass{
public:
    Myclass();
    Myclass(int x);
};

int main()
{
    Myclass m;
    double dval{};

    m = dval;   // Myclass türünden nesneye double türünden nesne atandı
    m = 10 > 5;  // Myclass türünden nesneye boolean türünden nesne atandı
}
```

Burada sentaks hatası yok. Bunu sebebi çok önemli bir kural.
Function overload resolution sürecinde argümandan parametreye yapılan dönüşümlerden birisi user-defined consversion.
Yani sınıfın conversion cosntructorını çağırılması ile yapılan dönüşüm user-defined conversion.
User defined consversion neydi?
Eğer dil kurallarına göre bir dönüşüm yoksa ve bildirilen fonksiyona çağrı ile bu dönüşüm mümkün hale geliyorsa (örneğin conversion cosntructor) bu dönüşmülere user edfined conversion denir.

**Önemli olan kural:**
```CPP
Eğer bir örtülü dönüşüm  =

standart conversion + user defined conversion
user defined conversion + standart conversion

bunlardan birisiyle yapılıyorsa,

derleyici bu dönüşümü yapmak zorunda.
```

```CPP
m = dval;
```
dediğimizde, dval in int e dönüşmesi gerekiyor. int in de Myclass a dönüşmesi gerekiyor. 
dval den int e dönüşüm standart conversion. int ten Myclass a dönüşüm, user define conversion.

- Bu durumda derleyici bu dönüşümlerin ikisini de otomatik olarak yapmak zorunda. 
- Aslında derleyiciye şu talimatı veriyoruz:

```CPP
static_cast<Myclass>(static_cast<int>(dval))  // derleyici bizim yazdığımız deyimi bu şekilde ele almak zorunda.
```

**Bir örnek daha:**

```CPP
class Myclass {
public:
    Myclass();
    Myclass(bool);
};

int main()
{
    int x;
    int* ptr = &x;
    Myclass m;

    m = ptr;
}
```
> Bu kod da legal. Çünkü int* türünden bool türüne implicit conversion var. Bu standart conversion. Bool türünden de myclass türüne user defined conversion var. Derleyici bu dönüşümü yapmak zorunda oluyor.

- user defined conversion + user defined conversion olarak yapılabilen bir dönüşüm varsa derleyici bunu örtülü olrak yapmaz.

**Örnek:**

```CPP
class A{

};

class B {
public: 
    B(A);   // A dan B ye ortülü donusum var.
};

class C {
public:
    C(B);   // B den C ye örtülü dönüşüm var.
};

int main()
{
    A ax;

    C cx = ax;
} 
```
> Bu legal değil. Nden?

> Çünkü bu dönüşümün yapılabilmesi için önce ax in b ye. Sonra b den c ye dönüşmesi lazım. Her ikisi de user defined conversion olduğu için derleyici bu dönüşümü örtülü olarak gerçekleştirmeyecek.

```CPP
C cx = ax;  
```
> bu sentaks hatası. Ama şöyle yazsaydım hata olmayacaktı:

```CPP
C cx = static_cast<B>(ax);
```
> İlk dönüşüm explicit olarak yapıldı 2. dönüşüm implicit olarak yapıldı.

Özet:
Eğer bir derleyici örtülü olarak bir dönüşümü:
1. standart conversion + user defined conversion
2. user defined conversion + standart conversion

yaparak gerçekleştirebiliyorsa, derleyici bunu otomatik olarak yapmak zorunda.

- Söz konusu dönüşüm arka arkaya 2 tane user defined conversion ile yapılabliyorsa derleyici bunu yapmamak zorunda.
- Örtülü dönüşümü engellemenin yolu, constructor bildiriminde bir explicit anahtar sözcüğü tanımlanırsa buna explicit constructor denir. Explicit sadece bildirimde olacak tanımda olmayacak.

**Ornek:**

```CPP
class Myclass{
public:
    explicit Myclass(int)
    {
        std::cout << "explicit Myclass(int)\n";
    }
    Myclass(double){
        std::cout << " Myclass(double)\n";
    }

};

int main()
{
    Myclass x = 12;
}

```
**Sonuc:**

double parametreli constructor cagirildi. int parametreli olan explicit oldugu icin.
Constructor in explicito lmasi donusumu imkansiz kilmasi demek degildir.

**Soyle bir kod da yazilabilir:**

```CPP
int main()
{
    int ival{54};
    Myclass m;

    m = static_cast<Myclass>(ival);
    m = (Myclass)(ival);
}
```

## Copy Elision

- kopyalamanin yapilmamasi, kopyalamadan kacinma
- Oyle durumlar var ki aslinda sentaks geregi orada bir kopyalama soz konusu. Ama derleyici kodu optimize ederek kopaylamayi elimine ediyor. 
- Yani kagit ustunde kopyalama var ama derleyicinin urettigi kodda, derleyici daha etkin kod uretmesi sebebiyle kopyalamadan kaciliyor.
- c++17 standartlari ile copy elision in belli bicimleri zorunlu oldu. Yani belirli copy elision senarayolari derleyici optimizasyonu olmaktan cikartilip dilin kurallarinca garantiye baglandi.
- Yani oyle durular var ki artik derleyici optimizasyon yaptigi icin degil, dilin kuralalri debebiyle copy elision yapiyor.
- Sadece optimizasyon ise derleyici bunu yapmak zorunda degil

**1. senaryo:**
**Elimizde bir sinif var ve fonksiyonun parametresi sinif turunden. Call by value**

**Ornek:**

```CPP
class Myclass{
public:
    Myclass()
    {
        std::cout << "Myclass default ctor\n";
    }
    Myclass()
    {
        std::cout << "Myclass copy ctor\n";
    }
    ~Myclass()
    {
        std::cout << "Myclass destructor\n";
    }
};

void func(Myclass)
{

}

int main()
{
    func(Myclass{});
}
```

> Eger copy elision olmasaydi once derleyici gecici nesne icin default constructor cagirmaliydi. Sonra da fnksiyonun parametre degiskenini copy constructor ile hayata getirmeliydi. Ama burada sadece default constructor cagirilacak.

**Burada derleyicinin yaptigi:**
> Gecici nesne zaten kullanilmiyor, gecici nesneyi olusturup copy constructor ile aktarmak yerine, sanki dogrudan fonksiyonun parametre degikeninin hayatagelecegi adreste bu nesneyi hayata getiriyor. Derleyici bu optimizasyonu daha onceden de yapailiyordu ama simdi zorunlu.

**Debug mode:** Derleyici belirli optimizasyonlari yapmiyor ve kendisi de kod ilave ediyor.
**Release Mode:** Derleyici o debug kodlarinieklemiyor ve optimizasyon konusunda daha agresif oluyor.

# Ders 14

## Return value optimization:

- Oyle durumlar var ki derleyicinin kopyalama kodu olusturasi gerekiyor. ve burada bir sinif turu soz konusu ise kopyalamayi yapmak icin duruma gore sinifin copy consturcot veya move constructor inin cagirilmasi gerekiyor. Fakat derleyici copy constructor ya da move constructor cagirmak yerine kopyalamayi tamamen ortadan kaldiriyor. 

> Return value optimization bir bicimi dahavar ve mandatory degil.

- named return value optimization  NRVO

> Farki, derleyici bunu yapmak zorunda degil ve copy construcotr in cagirilabilir durumda olmasi gerekiyor.

```CPP
class Myclass(){
public:
    Myclass()
    {
        std:cout << "myclass default ctor\n";
    }
    // Myclass(const Myclass&) = delete;

    ~Myclass()
    {
        std::cout << "Myclass destructor";
    }
};

Myclass foo()
{
    Myclass m;

    return;
}

int main()
{
    Myclass m foo();
}
```
> copy cosntructor delete ettigimizde sentaks hatasi veriyor.

## Siniflarin static veri elemanlari:

### static nedir?
- Simdiye kadar gordugumuz veri elemanlari object iliskili. Yani:

```CPP
class Nec{
    int a,b,c;
};
```
> Her nec nesnesinin 1 adet a b ve c si var.

> Yani sizeof Nec 3xsizeof int

- Ama sinifin static veri elemanlari adeta C deki global degiskenler. Ayni degil ama assembly duzeyinde ayni. Nesnenin icinde degil ama sinifa ait.

**Global degiskenleri global olmaktan cikartip sinifin static veri elemani yaptigimizda ne degisiyor?**
> class scope a almis oluyoruz. Bir erisim kontrulu soz kunusu oluyor.

- static omurludur, global degisken gibi. Program calismayabasladigi anda hayatta. main cagirilmadan hayata baslayacak. Program sonuna kadar hayatta kalcak.
 
```CPP
class Myclass{
    static int x;
};

int main()
{
    Myclass::x =10;
}
```
> Sentaks hatasi, sebebi erisim kontrolu.

**Bir sinifin static veri elemanini dogrudan ismi ile kullanabilmem icin**

o ismi aratip bulmam gerekiyor
eristigim ismin public olmasi gerekiyor
ya da friend bildirimi ile bana erisim hakkinin verilmis olmasi gerekiyor.

**Sinifin static veri elemanlari nasil tanimlanacak?**

```CPP
// myclass.h

class Myclass{
public:
    static int x;
};

// myclass.cpp
// #include "myclass.h"

int Myclass::x;  // bildirimde static anahtar sozcugu olacak ama tanimda olmayacak.
int Myclassx = 10;
```

```CPP
class Myclass {
private:
    Myclass m;
};
```
> Sentaks hatasi,

```CPP
class Myclass {
private:
    static Myclass m;
};
```
static oldugu zaman sentaks hatasi degil. 
Sonuc: Bir sinifin static veri elemani kendi turunden olabilir.

**C++ 17 standartlari ile:**
- sinifin static veri elemanlari ve global degiskenler inline anahtar ozcugu ile tanimlanabiliyorlar.

### inline variable neydi?
- Bu bir definition, link asamasina geldigimizde bundan 1 tane olma garantisi var. Birden fazla kaynak dosyada bu token by token tanimi ayni ise, ODR ihlal edilmiyor.

**Örnek:**

```CPP
//necati.h

inline int x =5;
```
> Kac tane kod dosyasi necati.h include ederse etsin ODR ihlal edilmis olmayacak.

### Static member functions:

non-static member functions
    const
    non-const
static member functions

```CPP
class Myclass{
public:
    void foo(); //non-static member fucntion
    static void bar();  // static member function
};
```
> Burada foo fonksiyonu Myclass nesnesinin adresi ile cagiriliyor. Bunlarin this pointer i var.

> Ama static uye fonksiyonlar yine scope class ta ve erisim kontrolune sahip. Ama this pointeri yok.
```CPP
Myclass::foo(); 
```
> dersem sentaks hatasi. Cunku bu fonksiyonun cagirilmasi icin bir object gerekiyor.

```CPP
Myclass::bar();
```
> Derleyici isim aramayla bu fonksiyonun static uye fonksiyon oldugunu gorecek. This pointeri olmadigi icin buna cagri kodunu dogrudan olusturacak. Bu bir nesneye ihtiyac duymuyor. Hata yok.

**Yani semantik olarak bakarsak ta;**
- sinifin geneli ile ilgili is yapan, ama nesnenin ozeli ile ilgili is yapan bir fonksiyon degil.

```CPP
class Myclass {
public:
    static void bar();
private:
    int mx;
}

void Myclass::bar()
{
    Myclass m;
    auto a = m.mx;
}
```

> Sinifin uye fonksiyonu oldugu icin sinifin private bolumune erisebiliyor. Hata yok.

# Ders 15

## friend Bildirimleri:
- Bir friend bildirimi sınıfın kendi kodlari disinda diger kodlara, private bolume erisim hakki taniyor.

**friend anahtar sozcugu ile yapilan bir bildirim:**

1. Bir namespace deki fonksiyona
2. B'r sinifin bir uye fonksiyonuna
3. Bir sinifin tum uye fonksiyonlarina

friend lik verebiliyor.

> Namespace deki bir fonksiyona friend lik verdigimiz zaman bu fonksiyonun tanimini sinifin tanimi icinde yapabiliyoruz.

> A, B ye  friendlik vermisse ve B, C ye friendlik vermisse; A, C ye friendlik vermis degil.

## OPERATOR OVERLADING: OPERATOR YUKLEMESI

- Bir sınıf nesnesi normalde sadece sizeof operatörünün operandı olabilir. Fakat bir sınıf nesnesi bir operatörün operandı olduğunda, öyle bir mekanizma var ki; operatörün operandı olmuş sınıf nesnesi ifadesini bir fonksiyon çağrısına dönüştürüyor. Bu mekanizmaya operatör overloading deniyor.
- Örneğin bir sınıf nesnesi toplama operatörünün operandı olmuşsa ve eğer toplama operatörü bu sınıf için overload edilmişse bu fonksiyon çağırılacak. Bu fonksiyon çağırmanın bir başka biçimi.
- Neden böyle bir araç var? Böyle bir aracın çalışma zamanına ek bir maliyeti var mı? Doğrudan fonksiyon ouşturup fonksiyonu ismi ile çağırsaydık daha az maliyet mi olacaktı?

> Amaç programcının işini kolaylaştırmak, daha yüksek bir soyutlama ortamı sağlamak.

```CPP
Date mydate{31,12,2022};
++mydate;

if(date1 > date2)
    date1 -= 20;
```

**Neden operator everloading mekanizmasını çok iyi öğrenmeliyiz?**
> standart c++ kütüphanesi operator overloading mekanizmasını kullanıyor.


**Örnek:**

```CPP
#include <iostream>
#include <string>

using namespace std;

int main()
{
	string name{ "ferhat" };
	string str{ "murat" };

	if (name == str)
		name += "can";
}
```

**Operandlardan en az birinin sınıf türünden ya da bir numaralandırma türlerinden olması gerekiyor.**

### overload edilemeyen operatörler:

nokta operatörü
sizeof operatörü
ternary operator
:: scope resolution operatörü
.* operatörü (C dilinde olmayan)
typeid operatörü


```CPP
#include <iostream>

using namespace std;

int main()
{
    int x = 5;
    cout << x;
}
```
> cout << operatörünün operandı oldu ve derleyici bunu fonksiyona yapılan çağrıya dönüştürdü. Burada bir fonksiyıon çağrısı var.

**Fonksiyon ile cagirmak istersek**
```CPP
cout.operator<<(x);
```

- Bazi operatorler icin sadece uye operator fonksiyou olusturabiliyoruz. 

Member operator function 

[]
(->)
type cast 
()

> Diger operatorler ile istersem global operator fonksiyonu, istersem uye operator fonksiyonu yazabiliyorum.

> Ama bunlar ile sadece uye operator fonk. olusturabiliyorum.

- Bu fonksiyonlar operatorlerin arity sine uymak zorunda (binary ise binary olarak overload edilecek, unary ise unary olarak overload edilecek)

```CPP
a > b 
```

> a ve b sinif turunden nesneler olsun. Bu ifade fonksiyon cagrisina donusturulecek.
    
- Eger burada cagirilacak fonksiyon global bir fonksiyon ise, yani bu operator global operator fonksiyonu olarak overload edilmisse derleyici, ismi operator>() olan fonksiyona her iki ifadeyi de arguman olarak gonderecek yani:

```CPP
operator>(a,b);
```

**Ama operator unary operator ise**

```CPP
!x      operator!(x);
```
> olacak.

**Ornek:**

```CPP
using namespace std;

class Nec{

};

bool operator>(const Nec&);
// Derleyici burada hata verdi cunku tek parametreli.
```
> Hata: binary 'operator >' has too few parameters. Sadece 2 parametresi var ise gecerli olacak.

**Ornek:**

```CPP
class A{
public:
    bool operator>(const A&)const;  // geçerli
    bool operator!(const A&)const;  // Geçersiz
};
```

**Ornek:**

```CPP
class A{};

A operator+(const A&); // Kod geçerli, bu toplama operatörünü overload etmiyor, işaret operatörünü overload ediyor.
```

**4 Tane token 2 ayrı operator gorevinde:**
> + - & *

- A operator+(const A&); // sign operator
- A operator+(const A&, const A&);    // addition operator

# Ders 16

## Ok ve içerik operatörlerinin overload edilmesi

- p -> x demek aslında (*p).x demek

```CPP
SmartPtr    ptr;
ptr -> foo();
```

> Eğer ptr bir sınıf nesnesi ise ve ok operatörün operandı olmuşsa derleyici ptr nin ait olduğun sınıfın ok operatör fonksiyonunun olup olmadığına bakacak

**Dikkat: Ok operatörü binary bir operatör olmasına rağmen unary bir operatör gibi yüklenir.**

**Örnek üzerinden anlayalım:**

```CPP
class Prt{
public:
    A & operator*();
    A* operator->();
};

int main()
{
    Ptr p;

    p->foo();
    p.operator->()->foo();
}
```

> p->foo yazmakla operator ok fonksiyonunu çağırıp oradan elde edilen geri dönüş değerini yine gerçek ok operatorunun soluna koymak aynı anlama geliyor.

## Fonksiyon çağrı operatörlerinin overload edilmesi

- Fonksiyon çağrı operatörü de bir operatör ve bu operatör de dilin kurallarına göre overload edilebiliyor. En sık overload edilen operatördür.

- Fonksiyon çağrı operatörünün overload edilmesi daha çok generic programlama araçları ile birlikte kullanılıyor. C++ dilinin en önemli araçlarından birisidir.

```CPP
func();
```

- C dilinde bu yapıyı geçerli kılan 3 ihtimal var.

1. func bir fonksiyon ismidir.
2. func bir fucntion pointer olabilir. (Bu durumda function pointer olan func ın değeri olan adresteki fonksiyon çağırılacak.)
3. func bir fonksiyonel makro olabilir. Yani önişlemci program bir yer değiştirme yapacak.


- C++ dilinden bu ihtimalin dışındaki olasılıklar da söz konusu.

1. func bir sınıf nesnesi olabilir ve bu sınıf fonksiyon çağrı operatörünü overload etmiş olabilir. 

**Bu durumda derleyici :**

```CPP
func(10) ifadesini,
func.operator()(10); (func nesnesinin operator fonksiyon çağrı fonksiyonunu çağıracak ve 10 değerini argüman olarak gönderecek.)
```

- Fonksiyon çağrı operatörünü overload eden sınıflara karşılık gelen 2 terim var. 

1. function class 
2. functıon object

**Fonksiyon çağrı operatörünün overload edilmesini inceleyelim.**

```CPP
class Nec {
public:
    int operator()()
    {
        std::cout << "Nec::operator()() this = " << this << '\n';
        return 1;
    }
};

int main()
{
    Nec mynec;
    std::cout << "&mynec = " << &mynec << "\n";

    auto val = mynec();
    std::cout << "val = " << val << "\n";
}
```

> mynec() ifadesi karşılığı derleyici operator() fonksiyonunu çağıracak. Bu fonksiyonda *this mynec nesnesi olacak. 

- **Bir soru: Bir sınıfın birden fazla fonksiyon çağrı operatörü olabilir mi?**

```CPP
class Nec {
public:
    void operator()()
    {
        std::cout << "Nec::operator()() \n";
    }
    void operator()(int)
    {
        std::cout << "Nec::operator()(int) \n";
    }
    void operator()(int, int)
    {
        std::cout << "Nec::operator()(int, int) \n";
    }
    void operator()(double)
    {
        std::cout << "Nec::operator()(double) \n";
    }
};

int main()
{
    Nec mynec;

    mynec();
    mynec(10);
    mynec(3.4);
    mynec(3,5);
}
```

- Neden ben bir sınıf nesnesinin fonksiyon çağrı operatörünün operandı olması durumunda bir fonksiyonun çağırılmasını istiyorum?

```CPP
mynec.func();
```

> Bu şekilde bir üye fonksiyon oluşturup onun ismiyle çağırabilirdim.

> mynec(); yazarak sanki sınıf nesnesini bir fonksiyonmuş gibi izlenim yaratıyoruz.

> Bu sorunun cevabı generic programlama tarafında.
mynec() bir sınıf nesnesi. Sınıf nesnesi olduğu için bir state e sahip. Aynı sınıf türünden nesneler ayunı state te olmak zorunda değil. Bu bir gerçek fonksiyon olsaydı sadece kendisine gelen argümanları kullanabilirdi. Ya da static yerel değişkenleri kullabilirdi. Ama bu bir sınıf nesnesi olduğu için kendi elemanalrını da kullanabilir. 

**Örnek:**

```CPP
int main()
{
    Nec nf1;
    Nec nf2;
    Nec nf3;

    nf1();
    nf2();
    nf3();
}
```
> Bu sınıfları fonksiyuon çağrı operatörünün operandı yaptığımızda her biri ayrı verileri kullanıyor olabilir. Bu normal fonksiyonlarda doğrudan mümkün olmayan bir araç.

**Bir örnek:**
Fonksiyonumuzun verilen bir aralıkta rastgele bir sayı üretmesini istiyoruz. Normal fonksiyon olarak yazarsak:

```CPP
int myrand(int low, int high) // hangi aralıkta rastgele sayı alacağı bilgisini client koddan almak zorunda. Ben ancak buna bu argümanalrı gönderirsem bu aralıkta bir rastgele sayı üretebilir. 
```

> Öyle bir yapı oluşturmak istiyorum ki, fonksiyona argüman göndermiyorum ama fonksiyon hangi aralıkta rastgele sayıo üreteceği bilgisini kendi durumuyla (state) tutacak. Bunu bir function object hanline getirerek yapabilirim. 

## Tür Dönüştürme Operatör Fonksiyonları

- Bir sınıf türünden nesneyi bir başka türe dönüştürmek için kullanacağımız fonksiyonlardır. Yani derleyici durumdan vazife çıkartıp bu fonksionlara çağrı yaparak sınıf türünden nesneyi başka bir türe dönüştürme olanağına sahip olacak. 
**Bir notu hatırlayalım:**
> Normale mümkün olmayan bir dönüşüm eğer bir fonksiyon bildirimiyle, derleyicinin o fonksiyona çağrı yapması halinde gerçekleştiriliyorsa böyle dönüşümlere user-defined conversion deniliyordu. Şimdiye kadar biz user defined conversion un conversion constructorlar ile yapılcabileceğini gördük. Yani derleyici sınıfın conversion constructor ına çağrı yaparak sınıf türünden olmayan bir değeri sınıf türüne dönüştürebiliyordu. 

- Şimdi user defined conversion ın yapılcabileceği ikinci bir yol öğrenceğiz. Sınıf türünden olan bir nesnenin başka bir türe dönüştürülmesini sınıfın tür dönüştürme operator fonksiyonları ile gerekleştirebiliriz. 

**Bir örnek:**

```CPP
class Myclass{

};

int main()
{
    Myclass m;
    int ival = m;
}
```

> Sentaks hatası, Myclass sınıfından int türüne otomatik dönüşümyok. Hata mesajı: cannot convert from Myclass to int 

> Peki ben bir fonksiyon bildirsem derleyici bu fonksiyona çağrı yaparak Myclass türünden bir nesneyi int türüne dönüştürebilir mi? Evet. Bu dönüşümleri gerçekleştirecek fonksiyonlara tür dönüştürme operatör fonksiyonları denir. 

> Peki böyle bir fonksiyon nasıl bildirilecek? Bu da bir opratör fonksiyonu olduğu için yine operator keyword u kullanılacak. Bunun yanına hangi türe dönüşüm gerçekleşecekse o tür yazılcak.

**örnek:**

**Myclass türünden bir nesneyi:**
- int türüne dönüştürecek fonksiyonun ismi operator int
- double türüne dönüştürecek olan operator double
- int * türüne dönüştürecek olan operator operator int*

> operator int fonksiyonunun geri dönüş değeri int. Bu geri dönüş değeri yazılmayacak.

**Örnek bir dönüşüm:**

```CPP
class Myclass {
public:
	operator int(const)
	{
		std::cout << "Myclass::operator int() this =" << this << "\n";
		return 1;
	}
};

int main()
{
	Myclass m;

	int x = m;
}
```
> Bir sentaks hatası yok.

**Aynı örnek üzerinden:**

```CPP
class Myclass {
public:
	operator int(const)
	{
		std::cout << "Myclass::operator int() this =" << this << "\n";
		return 1;
	}
};

int main()
{
	Myclass m;
	double dval;
	dval = m;
}
```
> Burada Myclass nesnesi int e dönüştürülecek sonrasında int double a dönüştürülecek. Birincisi user defined converison ve ikincisi standart conversion.

**Aynı örnek üzerinden:**

```CPP
class Myclass {
public:
	operator int(const)
	{
		std::cout << "Myclass::operator int() this =" << this << "\n";
		return 1;
	}
};

int main()
{
	Myclass m;

	if(m){}
}
```
> Sentaks hatası olmayacak. Derleyici sınıfın operator int fonksiyonunu çağıracak. int türünden de bool türüne dönüşüm olduğu için kod geçerli olacak.

- Bu örtüülü dönüşüm bazen bizim yararımıza olmayabilir. Tür dönüştürme operator fonksiyonları modern CPP öncesinde explicit olamıyordu. 

**Örnek:**

```CPP
class Myclass {
public:
	explicit operator int(const)
	{
		std::cout << "Myclass::operator int() this =" << this << "\n";
		return 1;
	}
};
```
> burada explicit yapıp yapmamak bizim seçeneğimiz. Bu dömüşümün otomatik olarak gerçekleşmesi gerekiyorsa explicit yapılmayacak. Ama birçok örnekte explicit olasında fayda var çünkü isteğimiz dışında tür dönüşümü gerçekleştirebilir.

**Örnek:**

```CPP
class Myclass {
public:
	explicit operator int(const)
	{
		std::cout << "Myclass::operator int() this =" << this << "\n";
		return 1;
	}
};

int main()
{
	int x = 5;
	Myclass m;

	x = m;
}
```

> Artık kod legal değil çünkü tür dönüştürme operatörü explicit. Burada örtülü dönüşüm sentaks hatası ama biz kendimiz static_cast operatörü ile dönüşüm gerçekleştirebiliriz.

```CPP
x = static_cast<int>(m);
```

**Bir Öneri:**
Makul bir neden olmadıkça tür dönüştürme operatörlerini explicit yapınız.

- Bir sınıf türü bool gerektiren hiçbir yerde kullanılamaz. Ama sınıfın bool türüne dönüşüm yapan bir fonksiyonu varsa kullanılabilir. 

**Örnek:**

```CPP
class Nec {
public:
	operator int()const;
};

int main()
{
	Nec nec1, nec2;
	!nec1;
	nec1&& nec2;
	nec1 || nec2;
	nec1 ? 10 : 20;
	if (nec1);
}
```
> Kodların hepsi geçerli oldu. Derleyici artık boolean değer beklenen yerde sınıfın operator int fonksiyonunu çağırdı ve bunu geri dönüş değerini de standart conversion ile bool türüne dönüştürdü. 

**Örnek:**

```CPP
class Nec {
public:
	operator bool()const;
};

int main()
{
	Nec mynec;

	int x = mynec;

	if (mynec) {

	}
}
```

> Burada kod geçerli. Önce bool türüne dönüşecek ardından bool türünden int türüne dönüşecek. If kısmında ise derleyici sınıfın operator bool fonksiyonunu çağıracak. 

**Ama explicit yaptığım zaman:**

```CPP
class Nec {
public:
	explicit operator bool()const;
};

int main()
{
	Nec mynec;

	int x = mynec;

	if (mynec) {

	}
}
```

> if deyimi geçerliliğini koruyacak çünkü boolean context ama bir üstteki sentaks hatası. 
- Bazı C++ standart kütüphanesinin sınıfları operator bool fonksiyonuna sahip ve bunlar explicit. Yani boolean context varsa dönüşüm sağlıyorlar ama boolean contexct dışında dönüşüm sağlamıyorlar.

**Bir mülakat sorusu:**
```CPP
class Nec {
public:
	operator bool()const
	{
		return true;
	}
};

int main()
{
	Nec x, y;
	auto val = x + y;
	std::cout << "val =" << val << "\n";
}
```

> val değişkeninin değeri int Ama değeri 2. operator bool fonksiyonu explicit olsaydı sentaks hatası olacaktı. 

**Örnek:**

```CPP
int main()
{
	using namespace std;

	unique_ptr<string> up;

	if (up) {
		std::cout << "not empty!\n";
	}
	else {
		std::cout << "empty!\n";
	}
}
```
> if parantezi içinde unique_ptr nesnesini kullanıdım zaman unique_ptr nesnesinin oıperator bool fonksiyonu çağırılıyor. Bu fonksiyon true ya da false döndürecek. True demek, unique_ptr nesnesinin hayatını kontrol etmekte olduğu dinamik ömürlü bir string söz konusu. Eğer false döndürürse unique_ptr nesnesi boş. Aslında derleyici if içindeki ifadeyi operator bool fonksiyonuna yapılan çağrıya dönüştürdü. unique_ptr nin operator bool fonksiyonu explicit bir fonksiyondur. Gerektiği yerde (if içinde) dönüştürüldü.

## İsim alanları

- C dilinde kod yazıyor olsaydık bir global kod alanımız vardı ve bu alandaki isimler birbiriyle çatışma riskindeydi. Örneğin 2 ayrı başlık dosyasını include ettiğimizde bu başlık dosyalarından gelen isimlerde bir çakışma olması durumunda sentaks hatası olacak. Hatta bunlar ayrı kaymak dosyalarda ise compile time da değil, link time da yaşanacak bu problem. 

- C++ dilinde isim çakışmasını engellemek için C dilindeki yöntemler akılcı değil. Dilin bu konuda bir araca ihtiyacı var. Bu yüzden C++ dilinde namespace denilen araç var. Namespace, global isim alanındaki isimleri diğer isimlerden gizlemeye yönelik bir araç.

> İsmi global isim alanına doğrudan koymak yerine böyl bir korumalı isim alanına koymak bu ismin diğer isimler ile çakışmasını engelliyor. Kısaca isim alanı global isim alanındaki isimlerin birbiriyle çakışmasını engelleyen ama isimleri bir arada tutan bir araç. 

**Dikkat:** İsim alanı içinde oluşturulan isimler de C bakış açısıyla yine globaldir. Statik ömürlüdür. Yani isim alanı diğer özelliklerini değiştirmiyor sadece  yeni bir scope oluşturmuş oluyorsunuz. C'deki file scope un yerini namespace scope terimini kullanıyoruz.

- Namespace ler global isim alanı içinde veya bir kaşka namespace içinde olabilir.

```CPP
double x;

namespace nec {
	int x = 5;
}

namespace erg {
	void x();
}
```
> Geçerli Kod

```CPP
namespace nec {
	int x = 5;
	class Date {

	};
	enum Color {blue, black, red};
}

int main()
{
	nec::blue;
}
```
> İsmin bir namespace de aranıp bulunması için ismin namespace ismi ile nitelenmesi gerekiyor

- Standart kütüphanenin bildirdiği tüm isimler ismi std olan bir namespace içinde geliyor. Vector, string, bitset C++ standart kütüphanesinin birer sısnıf şablonları. Cout standart kütüphanenin tanımladığı global bir değişkenin ismi. Ostream standart kütüphanenin tanımladığı bir sınıf şablonunun ismi, bir tür eş ismi. 
- Tüm bunları kullanmak için başlık dosyasını include etmemiz yeterli değil.

```CPP
int main()
{
	std::cout;
}
```

- Namespaceler için bir access konrolü yok. Yani bir namespace oluştursam bunun içinde public, private, protected kullanamam. (namespace in kendisi için)

```CPP
namespace nec {
	namespace erg {
		int ival;
	}
}

int main()
{
	nec::erg::ival;
}
```

```CPP
namespace nec {
	int a, b, c;
}
namespace nec {
	double x, y;
}
```
> Derleyici bunları aynı namespace olarak alıyor.  Yani bir namespace bildirimi ayrı ayrı bildirimler şeklinde de yapılabilir. Anlamsal açıdan ve sonuç açısından bir fark yok. Neden böyle bir kural var?

> Eğer böyle bir kural olmasaydı bir kütüphanedeki bildirimleri farklı başlık dosyalarına bölünemezdi. Örneğin:

```CPP
#include <vector>
#include <string>
#include <iostream>

int main()
{
	std::vector<int>x;
	std::string s;
	std::cout;
}
```
> Farklı başlık dosyalarından gelen isimler aynı namespace içinde.

- Bir namespace içindeki ismi ancak niteleyerek kullanabiliyorum. Öyle araçlar var ki bir ismi namespace ismi ile nitelemesem dahi derleyici o ismi o namespace te yine arayacak. 3 tane darklı araç var.

1. using decleration
2. Using nameapce (directive) decleration
3. ADL (arguıment dependant lookup)

# Ders 17

**Örnek:**

```CPP
void func();

namespace nec {
	void foo()
	{
		func();
	}
}
```
> Hatasız kod. İsim globalde bulunacak. Biraz daha zorlaştıralım.

```CPP
void func();

namespace nec {
	void bar();

	void foo()
	{
		bar();
		baz();
		nec::baz();
	}
	void baz();
}
```
> 'baz': identifier not found, daha aşağıya bakmıyor.

> nec::baz(); diye belirtsek bile isim aramayı kendi yukarısında yapıyor. Yine sentaks hatası.

1. using decleration
2. Using nameapce (directive) decleration
3. ADL (argument dependant lookup)

- Bunların üçü de ayrı araçlardır. 

### 1. using Bildirimi

- C++ dilinin en fazla overload edilen anahtar sözcüklerinden biri using. Sınıf içinde, tür eş ismi bildiriminde, enum bildirimlerinde ... kullanılıyor.

```CPP
using std::cout;
```
> cout std namespace indeki bir isim olduğnuu derleyiciye söylüyoruz. 

> Bu bir bildirimdir ve her bildirimdeki gibi bunun da bir kapsamı vardır. Global isim alanı. Globalde bu isim visible. Bu ne demek?

```CPP
using std::cout;

void func()
{
	cout << 1;
}
void foo()
{
	cout << 1;
}
```
> Burada cout ismi nitelenmeden kullanıldı fakat sentaks hatası değil çünkü üstteki bildirimin kapsamı içinde kullanıldı. Bildirimi func fonksiyonunun içine alsam:

```CPP
void func()
{
	using std::cout;
	cout << 1;
}
void foo()
{
	cout << 1;
}
```
> Sentaks hatasıdır. Derleyici bu noktada using bildirimini görmüyor. Using bildiriminin kapsamını dar tutmak daha iyidir.

**Not:** 
- using bildirimi ile sunulan isim bildirimin yapıldığı isim alanına enjekte edilir. Bu ne demek?

```CPP
int x = 10;

int main()
{
	int x = 20;
}
```
> Burada sentaks hatası yok. Ayrı scopetaki isimler. Şimdi biraz değiştirelim.

```CPP
namespace nec {
	int x = 10;
}

int main()
{
	using nec::x;
	int x = 20;
}
```
> Kod hatalı. using bildirimi ile ben o ismi main içine enjekte ettim. Yani ismin bu scope ta adeta bildirilmiş etkisi oluyor. Burada isim aynı scope ta ikinci kez bildirilmiş oldu.

> using bildirimi ile tanıtılan isim o kapsama enjekte edilir. (O kapsamda bildirilmiş etkisi yapar)

**Örnek:**
```CPP
int x = 10;

namespace ali {
	using ::x;
}

int main()
{
	ali::x = 10;
}
```
> Geçerli.

```CPP
namespace ali {
	int x = 4;
}
namespace can {
	int x = 4;
}
namespace eda {
	int x = 4;
}

int main()
{
	eda::x = 5;
}
```
> Geçerli

```CPP
namespace ali {
	void func(int)
	{
		std::cout << "ali::func\n";
	}
}

namespace can {
	void func(int, int)
	{
		std::cout << "can::func\n";
	}
}
void func()
{
	std::cout << "::func()\n";
}

int main()
{
	using ali::func;	//geçerli
	using can::func;	//geçerli
	func(12);		//geçerli
	func(1, 2); 	//geçerli
	func();		//geçersiz
}
```
> global func ismi gizlenmiş durumda. ::func(); olarak çağırsaydım hata olmazdı.

Not: C++ 17 ile using bildirimi için homo seperated list kullanılamıyordu. Yani:

```CPP
using std::cout, std::endl;
```
> C++17 ile bu mümkün hale geldi.

**Başka bir örnek:**
```CPP
namespace nec {
	int a, b, c;

	namespace erg {
		double x, y;
	}
}

int main()
{
	using nec::erg::x;
}
```

## 2. using namespace bildirimi 

- using namespace std
- using namespacew boost

> Bu dildirimin de bir kapsamı vardır.

```CPP
// namespace nec {
	int a, b, c;
// }
```
> Öyle bir araç olsun ki sanki bu isimler bu isim alanı içinde değil de, bu isim alanının bildirildiği isim alanı içinde bildirilmiş gibi görülür olsun.

> Diğer bir deyişle bu namaspace içindeki isimler sank bu namespace iöinde değil de onu kapsayan namespace içinde tanımlanmış gibi visible duruma gelecek. İşte bu araç using namespace bildirimi.

**Örnek:**

```CPP
namespace nec {
	int x, y;
	void foo();
}

int main()
{
	nec::x = 1;
	nec::y = 2;
	nec::foo();
}
```
> Bu koda bir ekleme yapacağım ve bakalım neler değişecek:

```CPP
// namespace nec {
	int x, y;
	void foo();
// }

int main()
{
	using namespace nec;
	nec::x = 1;
	nec::y = 2;
	nec::foo();
}
```
> using namespace nec eklediğim zaman nec namespace içindeki isimler sanki nec içinde değil de onu kapsayan namespace içnde bildirilmiş gibi görünür olsunlar.

**Not:** Using namespace bildirimi using bildiriminden farklı olarak isimleri bildirimin yapılkdığı alana enjekte etmiyor. 

```CPP
namespace nec {
	int x, y;
	int foo();
}

using namespace nec;

void func()
{
	x = 5;
}
void foo()
{
	y = 10;
}
```
> Hatasız kod.

```CPP
namespace nec {
	int x, y;
	int foo();
}
void func()
{
	y = 45;
	using namespace nec;
	x = 5;
}
```
> Sentaks hatası

**Örnek:**

```CPP
namespace ali {
	int x = 456;
}
namespace eda {
	double x = 4.9;
}
using namespace ali;
using namespace eda;
```

> Burada herhangi bir hata yok. Çünkü isimleri enjekte etmiyor. Ama soru şöyle sorulsaydı:

```CPP
namespace ali {
	int x = 456;
}
namespace eda {
	double x = 4.9;
}
using namespace ali;
using namespace eda;

int main()
{
	x = 45;
}
```
> Sentaks hatası. Çünkü her ikisi de görülür durumda olduğu için ambiguity var.

> Bu kod anlamsız çünkü globalde bu şekilde yapılan using namespace bildirimleri isim alanının varlık nedeni ortadan kalmış oluyor. İsimler yine çakışıyor.

**using namespace özeti:**
```CPP
using namespace ali;
```
> Ali namespace içindeki isimler aranırsa bu isimleri sanki onun içinde değil de onu kapsayan isim alanı içindeymiş gibi düşüneceksin, diyor derleyiciye.

**Başka bir örnek:**
```CPP
namespace ali {
	void func(int)
	{
		std::cout << "ali::func\n";
	}
}

using namespace ali;

void func(double)
{
	std::cout << "::func\n";
}

int main()
{
	func(12);
	func(1.2);
}
```
> using namespace ile function overloading. 

### 3. ADL (Argument Dependant Lookup)

- C++ dilinin en sık kullanılan akronimlerinden birisi. Argümana bağlı isim arama.

**Örnek üzerinden gidelim:**

```CPP
namespace nec {
	void func();
}

int main()
{
	func();
}
```
> Burada basitçe görüldüğü gibi sentaks hatası var. Kodu biraz değiştirelim:

```CPP
namespace nec {
	class Neco {
		//..
	};
	void func(Neco);
}

int main()
{
	nec::Neco x;
	func(x);
}
```
> Hiçbir sentaks hatası yok. 

> **Eğer bir fonksiyon çağrısında argüman olan bir ifadede yer alan bir isim bir isim alanı içinde bildirilen bir türe ilişkin ise fonksiyon ismi o isim alanında da aranır.**

> Yani burada x isminin türü nec isim alanında tanımlanan Neco sınıfı türünden olduğu için derleyici bu ismi normalde aradığı yerlerin dışında bu namespace içinde de arayacak.

**Başka bir örnek:**

```CPP
namespace nec {
	enum Color {blue, black};
	void func(Color);
}

int main()
{
	func(nec::black);
}
```
> Sentaks hatası yok. func içindeki ifade nec namespace içindeki bir türe ilişkin.

**Başka bir örnek:**

```CPP
namespace nec {
	class Neco {
		//...
	};
	void func(std::vector<Neco>);
}

int main()
{
	std::vector<nec::Neco> x;
	func(x);
}
```
> Hatasız kod. Burada func fonksiyonuna gönderdiğim argüman nec namespace'i içinde değil. std namespace i içinde. 

**Örnek:**
```CPP
namespace nec {
	class A {

	};
	void func(A);
}
void func(nec::A);

int main()
{
	nec::A a;

	func(a);
}
```
> Hangi func çağırılır? Ambiguity var. ADL isim aramada 2. yol değil. Yani "önce normal aranıyor sonra ADL ile aranıyor" veya "önce ADL ile aranıyor sonra normal aranıyor" değil. Aramada öncelik yok. Burada ambiguity var.

**Örnek:**

```CPP
#include <vector>

namespace nec {
	class A {

	};
	void func(A);
}


int main()
{
	nec::A a;

	void func(int);
	func(10);
	func(a);
}
```
> Hatalı kod. no suitable conversion function from "nec::A" to "int".  Burada name hiding söz konusu.

- Biraz daha ADL'den bahsedelim. Operator overloading mekanizması için kaçınılmaz gerekli.

**Örnek:**

```CPP
int main()
{
	std::cout << "hello world";
}
```
> Burada ADL var. Peki nasıl?

> Burada çağırılan bir fonksiyon var. Operator fonksiyonu. Bu operator fonksiyonu cout değişkeninin ait olduğu sınıfın bir global operator fonksiyonu. Global olduğuna göre aslında şöyle çağırılıyor:

```CPP
// std::cout << "hello world";
operator<<(std::cout, "hello world");
```
> Yukarıdakininin aşağıdakinden bir farkı yok. Operator <<, std namespace içinde yer alan bir fonksiyon. std namespace içinde yer alan bir fonksiyonu std::operator... şeklinde nitelenmesi gerekyior ama nitelemedim. Çünkü operator fonksiyonuna gönderdiğim cout, std namespace içinde olduğundan, operator<< ismi std namepace içinde de arandı. Yani burada ADL var.

**Başka bir örnek:**

```CPP
int main()
{
	std::cout << endl;
}
```
> Burada hata var. Burada çağırılan fonksiyon global bir fonksiyon değil. Aslında çağırılan fonksiyon şu:

```CPP
std::cout.operator<<(endl);
```
> Bunu ADL ile bir alakası yok. Yani endl isminin aranması ile ADL nin bir alakası yok. endl nin kendisi argüman. Ama şöyle deseydik hata olmayacaktı.

```CPP
std::cout.operator<<(std::endl);
```

**Başka Bir Soru:**
```CPP
int main()
{
	endl(std::cout);
}
```
> Hata yok. Buradaki endl global bir fonksiyon. Global fonksiyona cout nesnesi ile çağrı yaptım. endl fonksiyonu std namespace içinde olduğundan, endl ismi std namespace içinde arandı.

**Başka Bir Örnek:**
```CPP
int main() 
{
	std::vector<int> ivec(100);
	sort(begin(ivec), end(ivec));
}
```
>  sort, begin ve end isimleri nitelendirilmemiş fakat hiçbir hata yok. Bunun nedeni ADL. ivec, std namespace içindeki bir sınıfa ilişkin. Dolayısıyla begin ve end fonksiyonlarının std namespace içinde aranıp bulunmasının sebebi bu. Fakat sort nasıl bulunuyor? begin(ivec) fonksiyonunun geri dönüş değeri türü de yine std namespace içinde. Doalyısıyla sort'a gönderilen argüman olan ifadenin türü std namespace deki bir türe ilişkin olduğu için sort ismi de std namespace içinde aranıyor.

**Örnek:**

```CPP
//myclass.h

class Myclass {
public:
	void func();
};

void foo(Myclass);

int main()
{
	Myclass m;

	m.func();
	foo(m);
}
```
> Bu kodda bir hata yok. Şimdi bunu bir namespace içinde düşünelim:

```CPP
//myclass.h
namespace nec {
	class Myclass {
	public:
		void func();
	};
	void foo(Myclass);
}

int main()
{
	nec::Myclass m;

	m.func();
	foo(m);
}
```
> Yine sentaks hatası olmadı. Böylece func ismini nasıl nitelemek zorunda kalmıyorsam, foo ismini de nitelemek zorunda kalmıyorum.

### Unnamed namespaces

- Bir namespace in ismi olmayabilir. Buna unnamed namespaces deniliyor. Eğer bir kaynak dosyada isimlendirilmemiş bir isim alanı oluşturulursa bunun içindeki varlıklar doğrudan iç bağlantıda oluyor. Bu ne demek?

> Eğer bazı ögerlerin sadece klendi kaynak dosyamızda kullanımasını istiyorsak ve diğer kaynak dosyalarda bu isimlerin başka varlıkların isimleri olmasına izin vermek istiyorsak. (normalde bunu C'de yapmanın yolu static anahtar sözcüğü) 

**Unnamed namespace içindeki isimleri nasıl kullanıyorum?**

```CPP
namespace xyz{
	int x = 10;
	void func()
	{

	}

	class Myclass {

	};
}

using namespace xyz;
```

> Burada derleyici sanki namespace ismi xyz imiş gibi ve çıkışında using namespace xyz yazılmış gibi davranıyor.

- Yani isimsiz isim alanı içindeki isimleri nitelemek zorunda değiliz:

```CPP
namespace {
	int x = 10;
	void func()
	{

	}

	class Myclass {

	};
}
int main()
{
	x= 45;
	::x=45;
}
```
> İki türlü de yazılabilir. Kümülatif olma özelliği isimsiz isim alanları için de geçerlidir.

**Not:** ADL modern C++ tan önce de vardı ve yoğun olarak kullanılıyordu. ADL modern C++ ta gelmedi fakat  ADL ilişkin bazı özellikler geldi. 

**Bir Soru:** Bir class ı kaynak dosyada iç bağlantı yapmanın tek yolu bu mudur?
**Cevap:** Bir sınıf iç bağlantıda olmaz. Bir isim iç bağlantıda olabilir. Ama bir sınıf bir unnamed namespace içinde olmadığı zaman bu projeyi oluşturan başka bir kaynak dosyada yine aynı isimli class sınıfı global düzeyd oluşturulmuş olsaydı ve bunlar token by token aynı olmasaydı **One definition Rule** ihlal edilecekti. Ama unnamed namespace ile ihlal etmeyecek.

**ADL hakkında bir bilgi:**
- Eskiden ADL e koenig Lookup deniliyordu. Andrew Koenig'in bunu standartlara dahil ettiği konusunda bir algı vardı. Ama kendisi bulmamıştır(Kendi beyanına göre).

```CPP
using std::cout, std::endl;
```
> C++17 ile bu özellik eklendi. Öncesinde aradaki virgül kabul edilmiyor.

### Nested namespaceler için eklenen kurallar:

- Bir nested namespace oluşturabilmek için onu kapsayan namespace içine yazmak zorundaydık. Örnek:

```CPP
namespace ali::veli::can {
	int c = 10;
}

namespace ali {
	int a;
}

namespace ali::veli {
	int v;
}

int main()
{
	ali::a = 1;
	ali::veli::v = 2;
	ali::veli::can::c = 3;
}
```
> Bu şekilde nested namespace bildirmek C++17 ile dile eklenen bir araç.

### inline namespace için eklenen özellikler:

- Inline nerelerde kullanılıyordu?
> Inline fonksiyonlarda, inline variable ve inline namespace çıktı son olarak.

**Kural:**

```CPP
namespace ali {
	namespace veli {
		int x;
	}
}

int main()
{
	ali::veli::x;
}
```
> Burada x'e erişmek için böyle bir kod gerekiyor. Bu kodu using namespace kullanarak değiştirelim:

```CPP
namespace ali {
	namespace veli {
		int x;
	}
	using namespace veli;
}

int main()
{
	ali::x;
}
```
> using kullanarak x'e bu şekilde de erişebiliriz. Fakat şimdi inline kullanarak x'e farklı bir yoldan erişeceğiz.

```CPP
namespace ali {
	inline namespace veli {
		int x;
	}
}

int main()
{
	ali::x;
}
```
> Burada inline bildirdiğimiz namespace içindeki isimler az önceki örnektye olduğu gibi using namespace bildirimi varmış gibi onu içine alan namespace içinde visible hale geliyor. Standart kütüphanede bazı nested nanemspaceler de böyle inline namespaceler. Peki neden böyle bir şey yapayım? 

> x ismi hala veli namespace içinde ama aynı zamanda ali namespace içinde de visible durumda.

- Inline namespace in dile eklenmesinin nedenlarınden biri ADL'nin daha önce bazı senaryolarda inline namespaceler için devreye girmemesi.
- Bir diğer nedenleden birisi de versiyon kontrolü. 

```CPP
namespace nec {

#ifdef ver1
inline
#endif
	namespace version_1 {
		class Myclass {
			///
		};
	}
#ifdef ver2
inline
#endif
	namespace version_2 {
		class Myclass {

		};
	}
}

int main()
{
	nec::Myclass m;
}
```
> Burada kodda artık sadece hangi makroyu define edileceğine bağlı olarak müşteri kodların hangi versiyonu kullanacağını ayarlayabiliriz. 

- C++ 20 standartları ile eklenen:

```CPP
namespace A::B:: inline C{
	int x;
}

int main()
{
	A::B::x = 5;
}
```
> Bu şekilde nested namespace i bir kerede bildirip onu inline olarak bildirmemiz de mümkün.

### namespace alias (İsim alanı eş ismi)
- C++ ilk çıktığından beri var.

- Bir namespace e verilenm eş isim. Adeta typedef bildirimi gibi ama türe değil bir isim aalanına eş isim veriyoruz.

- İsim alanı isim çakışmasına karşı bir önlem. Fakat namespace in kendi ismi de global isim alanında. Yani biz namespace ile başka modüller, başka kodlardan gelen isimler ile çakışmasını engelliyoruz ama namespace isminin çakışmasını engellemiyoruz. Bunun da çakışmaması gerekiyor.

**Örnek:**

```CPP
namespace siemens_pro_xyz_lib {
	int a;
}

namespace sms = siemens_pro_xyz_lib;

int main()
{
	siemens_pro_xyz_lib::a = 5;
	sms::a;
}
```

```CPP
namespace ali {
	namespace veli {
		namespace proj {
			class Myclass{};
		}
	}
}

int main()
{
	namespace pro = ali::veli::proj;
	pro::Myclass;
}
```

### Nested Classes

```CPP
class Nec {
	class Nested {
		static void foo();
	};
	void f()
	{
		Nested::foo();
	}
};
```
> Nec sınıfı Nested in private bölümüne erişebilir mi? Hayır erişemez, sentaks hatası. Eğer böyle bir şey istiyorsak friend bildirimine ihtiyaç var.

> Bunun tersi geçerli midir?

```CPP
class Nec {
private:
	int mx;
	static void foo();

	class Nested {
		void bar()
		{
			auto sz = sizeof(mx);
			Nec::foo();
		}
	};
};
```
> Burada erişimde bir sorun yok. Nested type, visible olan private ögelere erişebiliyor.

```CPP
class Nec {
private:
	class Nested{};
public:
	static Nested foo();
};

int main()
{
	Nec:Nested nx = Nec::foo();
}
```
> Nec::Nested, private olduğu için hata.

- Aynı örnekte küçük bir değpişiklik yapalım:

```CPP
class Nec {
private:
	class Nested{};
public:
	static Nested foo();
};

int main()
{
	auto nx = Nec::foo();
}
```
> Sentaks hatası değil. Erişim kontrolüne takılmıyor. Çünkü erişim kontrolü identifier kullnaımına ilişkin. Ortada doğrudan kullanılan bir identifier yoksa erişim kontrolünden bahsetmek mümkün değil. Yani isim yoksa erişim kontrolü de yok.


























