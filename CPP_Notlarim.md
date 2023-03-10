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

# Ders 18

## Nested Type

- Bildirimi sını tanımı içinde yapılıyor. Bir enum türü, tür eş ismi, sınıf olabilir.
- Neden bir türü doğrudan namespace içinde değil de bir sınıfın içinde bildiriyoruz?

1. O türün içine alan sınıfla mantıksal ilişkisi vurgulanıyor. Türü içeren sınıf o türü işlemlerinde kullanacak.
2. Class scope a giriyor ve isim arama kuralları değişiyor.
3. Erişim kontrolü geliyor. 

- Standart kütüphanenin en önemli bileşeni olan **STL** çok sayıda nested type kullanıyor. Bu nested typelar generic programlama tarafında önemli rol oynuyorlar.

**Hatırlatma:**

- class Nested private bir nested type olabilir. Ama sınıfın static bir fonksiyonu Nested döndürebilir. (Bildirimin daha yukarıda olması gerek)

```CPP
class Myclass {


private:
	class Nested {

	};
public:
	static Nested foo();
};

int main()
{
	// Nested x = Myclass::foo();	// hatalı kod
	auto x = Myclass::foo();	// Legal kod

}
```

## Pimple Idiom (Pointer Implementation)

- Bu teknik sınıfın private bölümünü gizlemeye yönelik. Bu ne demek?

```CPP
class Myclass {
private:
	// data members
	// private functions
};
```
> Sınıfın private bölümünün başlık dosyasında yer alması bazen bir takım dezavantajlar oluşturuyor.

> Neden sınıfın private bölümünü neden gizliyoruz?

```CPP
// myclass.h

#include <string>
#include "date.h"
#include "falanca.h"

class Myclass {
private:
	std::string str;
	Date date;
	Falanca f;
};
```
> Bizim başlık dosyamızı (myclass.h) iclude eden client kodlar, bizim dosyamızda include edilen başlık dosyalarını da include edecekler. Bunun zararlarından birisi compile time uzaması.

> private bölümü gizlemenin bir faydası daha var. Başlık dosyası bir text dosyası. Bunun derlenmiş hali yok, belki bunun da görüülmesini istemiyoruz.

## Containment (Composition)

**Association - Aggregation - Composition**

### Association
- 2 sınıf birlikte çalışarak bir işi gerçekleştiriyorlar. Association ın bir biçimi de aggregation. Her aggrehation bir association ama her association bir aggregation değil.
- Bir association bir aggregation ise nesnelerden biri diğerin sahibi konumunda. Bir nesne diğerini sahipleniyor ve onu kullanarak işini görüyor. 
- Aggregation ın özel bir biçimine de composition deniliyor.
- Composition onlduğunda bir sahiplik ilişkisi var fakat ömürsel bir birliktelik te olması gerekiyor. Yani sahip olan nesne hayta geldiğinde sahip olacağı nesne de hayata geliyor ve ömrü bititğinde de ikisi de bitiyor. 

**Özet:** 
- Composition nedir?

>  Compsition bir aggregation dır.  Aggregation da bir association dur. Eğer iki nesneden biri diğerinin sahibiyse, bu nesne işlerini sahibi olduğu nesneyi kullanarak görüyorsa ve bunlar arasında ömürsel bir birliktelik varsa bunlar composition ilişksii içinde.

## Initilizaton

- bir sınıf nesnesi hayata geldiğinde o sınıf nesnesinin elemanı olan sınıf nesne ya da nesneleri de bildirimdeki sırayla hayata gelir. Onları hayata getiren, constructorlara yapılan çağrı.
- Eğer sınıfın default ctor'ı derleyici taafından yazılırsa veri elemanlarını da default initilize ediyordu. Bu ne demek:
- Veri elemanlarının default initialzie edilmesi, veri elemanalrının sınıf türünden olması durumunda sınıfın default constructor ı çağırılıyor demek. 

```CPP
class Member {
public:
	Member()
	{
		std::cout << "member default ctor\n";
	}
	~Member()
	{
		std::cout << "member destructor\n";
	}
};

class Owner {
private:
	Member m;
};

int main()
{
	Owner x;
}
```
> Owner sınıfının  default constructor ı var. Implicityly declared. Yani derleyicinin yazdığı default constructor, elemanın default constructor ıyla elemanı hayata getiriyor.

> Owner ın destructor ı var. Sınıfın dest. olamma ihtimali yok. Deleted, defaulted, user declared olabilir ama not declared olamaz.

# Ders 19 

- String sınıfı C++ standart kütüphanesinin en sık kullanbılan ilk 2 sınıfından biri. İlk ikisi vector ve string olabilir. Bu iki sınıf aslında aynı veri yapısını implemente eden sınıflar. Her ikisi de veri yapısı olarak baktığımızda dinamik dizi sınıfı. Aradaki fark, vector genel amaçlı bir dinamik dizi sınıfı iken; string, yazı işlemleri için özelleştirilmiş, özel yazı işlemlerine yönelik arayüzü olan bir sınıf. 
- Her ikisi de C++ dili kurallarına göre birer standart STL container ı. 
- STL: Standart Template Library  (C++ dili stndart kütüphanesinin en önemli bileşeni)
- STL'in amacı: Veri yapılarını ve algoritmaları generic programlama paradigmasında ifade etmek.

> STL ve C++ standart kütüphanesi aslında tamamen aynı şeyler değil. STL standart kütüphanenin bir bileşeni ama çok büyük çoğunluğunu oluşturan bir bileşen olduğu için günümüzde aynı anlamda kullanılıyor.

> STL generic bir kütüphane, türden bağımsız.

- STL şablonlardan oluşuyor (Template). Doalyısıyla string sınıfının da sbir sınıf şablonu olduğunu belirtirsek, aslında string sınıfı da generic prohgramlama teknikleri ile implemente edilmiş bir sınıf. 

**Dinamik Dizi ne demekti?**
- Öyle bir veri yapısı ki ögeler bellekte ardışık oalrak tutuluyor ve sondan ekleme ve silme işlemlerinin karmaşıklığı O-1. Constant type.
- String'in dinamik diziyi kullanma amacı yazının karakterlerini tutmak.


- Aslında dinamik diziyi temsil eden sınıf nesnesi içnde 3 tane pointer tutuyor.

![image](https://user-images.githubusercontent.com/75746171/211778245-91025802-72bf-47e7-8914-3d0ba4263cde.png)

1. Birisi alocate edilen (edinilen) bellek bloğunun adresini
2. Bellek bloğunun bittiği noktayı.
3. Sondan ekleme yapılırsa eklemenin nereden devam edeceği bilgisi

> 1, pointer olabilir. 2 ve 3 pointer yerine tam sayı da olabiliir. (Pointer + tam sayı yaparak adrese erişilebilir)

> Size ve capacity eşit olduğunda artık alocate edilmiş bellek alanında bir nesne daha ekleyemem. Bu durumda yeni bir bellek alanının alocate edilmesi ve eski bellek alanındaki verilerin yeni bellek bloğuna kopyalanması veya taşınması gerekecek. Bu maliyetli bir işlem.

- String sınıfındaki fark, tutulan ögelerin yazının karakterleri olması. Yani necati yazısı tutulacaksa aslında necati yazısının karakterlerinin kodlarının tutuyor olacağım.

**Not:** Sınıfları küçük tutmak, nesneye yönelik programlamada önemli.

- string sınıfı bir sınıf şablonudur. (Class Template): Generic programlama aracı, türden bağımsız. Std namespace'i içinde tanımlanmış bir sınıf şablonu.

- Aslında bu sınıf şablonuun ismi **basic_string**

```CPP
std::basic_string<
```
> Bu sınıf şablonu; yazının karakteri olan tür, Karakter işlmelerinin nasıl yapılacağını belirleyen tür ve bellek alanlarının ne şeklide elde edileceğini belirleyen türe göre template hale getirilmiş.

```CPP
int main()
{
	std::basic_string<char, std::char_traits<char>, std::allocator<char>>;
}
```
> Aslında string sınıfı türünden bir nesne oluşturduğumuz zaman bu yukarıdaki sınıf türüden bir nesne oluşturmuş oluyoruz. Sadece strin yazmak  yeterli.

```CPP
int main()
{
	using namespace std;

	string s;
}
```
> Default initialize etmiş oluyorum ve bu nesne için default constructor çağırılacak.

**Char dizilerde yazı tutma olayı:**
> C++ dilinde de bu yapılabilir ama özel oalrak yapılması gereken bir senaryo yoksa gerek yok. Zaten char dizi static. Yani dizinin karakter sınırı var.  Yazının programın çalışma zamanı içinde büyütülme ihtiyacı varsa char dizi bizim işimizi görmeyecek fakat string sınıfı dinamik olarakyazının uzunluğununu arttırılıp azaltılabileceği bir sınıf. 

- Yazılar ile işlem yaparken string sınıfının üye fonksiyonlarını kullancağız (Member functions). Aynı zamanda global fonksiyonları (free functions) da kullancağız.

**Bir soru: Yazının tutulması için dinamik bellek alanının (Free store'un) kullanılması maliyet açısından bir dezavantaj değil mi?**

> Kesinlikle. İşlem maliyeti artıyor. Dinamik bellek alanı elde edilmesi, geri verilmesi.. bunlar maliyetli işlemler. Ama string string sınıflarının implementasyonlarında kullanılan bir teknik var: SSO (Small string optimization). Bu teknik ile küçük yazılar için dinamik bellek alanı elde etme gerekli olmayabiliyor.

- Bizim derleyicimizdeki stirng ve char* sizeof değerlerine bakalım:

```CPP
int main()
{
	using namespace std;
	std::cout << "sizeof(char*) = " << sizeof(char*) << "\n";
	std::cout << "sizeof(string) = " << sizeof(string) << "\n";
}
```
> Çıktı olarak 8 ve 40 aldık. Neden?

> Günümüzdeki modern string implementasyonları 3 tane pointer tutmak yerine nesnenin içinde asynı zamanda bir buffer tutuyorlar. Bu yüzden Small Buffer Optimization (SBO-SSO) deniyor. Eğer string nesnesinin tutacağı yazı belirli bir uzunluktan küçükse hiçbir dinamik bellek alanı alocate etmiyor. Bunun yerine yazıyı doğrudan string sınıf nesnesinin içinde tutuyor. Bunun iin ayrılan alan yetersiz olduğu zaman (Yazıyı büyütmek istediğimiz zaman arka plandaki implementasyon kodları o zaman bir bellek alanı alocate ediyor) 

![image](https://user-images.githubusercontent.com/75746171/211795038-0d778c0a-bd1e-4810-9fae-f17da7964536.png)

### string denildiğinde ne kastediliyor?

- Sonunda null karakter olan, bir bellek alanında tutulan bir yazı mı?
```CPP
aliemrekoc\0
```
> c string ya da NTBS (Null terminated byte stream)

- string sınıfı türüden bir nesne mi?
```CPP
and object of std::string
```
> std::string

- KAynak kodda derleyicinin gördüğü, derleme zamanında ne olduğu belli olan bir yazı mı?
```CPP
"Muratcan"
```
> string Literal (Bunun sonunda da null karakter var ama bu compile time da derleyicinin gördüğü bir yazı, static ömürlü ve const anahtar sözcüğü klkullnaılmasa da const olduğunu biliyoruz)

String sınıfı nasıl bir sınıf?

> Bir template'in açılımı, Bir tür eş ismi...

- Çok sayıda üye fonksiyonu var ve bunlar çoğunlukla overload edilmiş. Operator overloading mekanizmasından faydalanan bir sınıf. 

- **Container hatırlatma:** Aynı türden ögeleri bir bellekte oluşturulmuş düzenekte bir arada tutan sınıflara container sınıflar deniyor. String aynı zamanda bir container sınıf.

- String sınıfı modern C++ ile ciddi değişime uğrayan sınıflardan. Taşıma semantiği yoktu. 

- Bazı sınıflar da string sınıfı ile doğrudan ilişkili ama bunlar standart kütüphanenin ayrı sınıfları. 

> string_wiev, regex

- Bazi parametrik yapilari iyi anlamamiz gerekiyor:

- Bazi fonksiyonlarin parametrik yapisi const char* . Bu ne demek?

> Bizden bir adres istiyor ama istedigi adresteki yazinin sonunda null karakter istiyor. (Null terminated byte stream). Boyle bir fonksiyona bir adres gecersek ve gectigimiz adres:

1. Null pointer olursa
2. Sonunda null karakter olmazsa

> tanimsiz davranis olur.

### Tipik parametrik yapilar
```CPP
cstring parametre	const char*
```
> Sonunda null karakter bekliyor, eğer yoksa tanımsız davranış.
```CPP
data			const chat*	size_t n  (null karakterin bir önmemi yok)
```
> Bu adresten başlayarak bu kadar tane karakter. Taşma tanımsız davranış. Bull pointer tanımsız davranış
```CPP
fill			size_t char
```
> Bu kaadar tane bu karakterden
```CPP
char			char
```
> Doğrudan char
```CPP
std::initializer_list	{'a', ','}
```
>  initializer_list sınıfı türünden bir nesne istiyor.
```CPP
range	parameter	str	str + 5
```
> 2 tane adres istiyor.
```CPP
std::string parameter		std::string 
```
> Doğrudan başka bir string parametre istiyor.
```CPP
sub-string parameter		std::string, size_t idx
```
> Bu string'in bu indexinden başlayarak geriye kalan tüm karakterler. 

>string s{"akif gulsoy"}(s,1) : k'dan başlayarak sonuna kadar tüm karakterlerin oluşturduğu yazıyı argüman aolarak gönderecek.
```CPP
substring parameter		std::string, size_t idx, size_t n
```
> Bu stringin bu indexinden başlayarak bu kadar tane karakter

**Soru:*
- Bir std::string nesnesi 20 null karakterden oluşan bir yazı tutabilir mi?
> Evet

### size fonksiyonu

```CPP
	string::size_type string::size()const;
	string::size_type string::length()const;
```
- size veya length aynı değeri döndürecek aralarında fark yok. O zaman neden 2 tane fonksiyon var? Generic programlama paradigması ile ilgili. 
> Containerların bir ortak arayüzü var, o arayüzün bir bileşeni size. Bir container haricinde tüm containerların size fonksiyonu var. Containerların size fonksiyonu containerlarda tutulan üye sayısını döndürüyor.

> Yazının length'i olur ama container'in size'ı olur. Generic kodlarda sorun olmasın diye size eklemişler ama aynı zamanda length var. Generic programlama tarafında size kullanılmalı(Kullanılsa daha uygun). Ama yazılan kodu generic programlama ile alakası yoksa, amaç sadece yazının uzunluğunu elde etmek ise o zaman length.

```CPP
int main()
{
	using namespace std;

	string s{ "levent ercan" };

	auto len = s.length();
	
	cout << "uzunluk =" << s.length() << '\n';
	cout << "uzunluk =" << s.size() << '\n';
}
```
> Çıktılar aynı, uzunluğu tutmak için auto len.

**Not:** size aynı zmaanda diğer STL container larında da olan bir arayüz. Bunun gibi olan bir başka fonksiyon "empty". Boş mu sorusunu soruyor.

```CPP
str.empty();
str.size() == 0;
```
> Aynı anlamda 2 kod.

**Örnek:**

```CPP
int main()
{
	using namespace std;

	string s{ "ali yasar" };

	cout << s.size() << 'n';
	cout << s.capacity() << 'n';
}
```
> Çıktılar 9 ve 15. Yani 6 karakter daha ekleyebilirim. 7. karakteri eklediğimde reallocation olacak demektir. 

```CPP
int main()
{
	using namespace std;

	string s{ "necati ergin" };
	auto cap = s.capacity();

	for (;;) {
		s.push_back('.');
		if (s.capacity() > cap) {
			cout << "size =" << s.size() << "capacity =" << s.capacity() << '\n';
			(void)getchar();
			cap = s.capacity();
		}
	}

}
```
> Bu kod ile reallocation'ı gözlemleyebiliriz. 

- Reallocation takes time
- Reallocation invalidates pointers

> Reallocation olduğunda, eski bellek bloğunu gösteren pointerlar dangling duruma geliyor. 

**Örnek:**
```CPP
std::string str(1000, 'A');

int main()
{
	using namespace std;

	std::string str(1000, 'A'); 
}
```
> Main içindekine göre 1000 adet A karakteri free store'da (Dinamik bellek alanında) tutuluyor. str'nin kendisi stack'te tutuluyor, otomatik ömürlü bir nesne.

> Globaldekinde ise yine A karakterleri dinamik bellek alanında tutuluyor olacaktı ama str nesnesi statik ömürlü olduğu için data segment'te tutulacaktı.

```CPP
int main()
{
	using namespace std;

	auto p = new string (1000, 'A'); 
}
```
> Burada ise yine A karakterleri heap'te tutuluyor str nesnesinin kendisi de heap'te tutuluyor. Yani heap'teki string nesnesi ile yazının tutulduğu bellek alanı birbiri ile karıştırılmamalı.

### Copy on write tekniği

- Date x1;

> Bu nesneden birçok sayıda olduğunu düşünün ve değerleri aynı. "Programın gözlenebilir davranışında değişiklik olmaz" fikri ile nesneden 1 tane oluşturup aynı değeri kullansın diye düşünebiliriz. Ama nesnelerden birisi değişirse  ozaman 2. nesneyi yaratın. **Bu teknik modern C++'ta kesinlikle yasaklanıyor** Yani Standartlar bunun kullanımını engelliyor.

```CPP
int main()
{
	const char* p1 = "nihat";
	const char* p2 = "nihat";

	if (p1 == p2)
	{
		std::cout << "evet dogru aynı adres\n";
	}
	else
		std::cout << "hayır yanlıs farklı adres\n";
}
```
> Burada unspecified behaviour. Bu string literaller ile ilgili, karakter sabiti değil.

```CPP
int main()
{
	using namespace std;

	string s;

	cout << "s.size()=" << s.size() << "\n";
	cout << "s.length()=" << s.length() << "\n";
	cout << "s.empty()=" << s.empty() << "\n";
}
```
> Array haricinde tüm containerlarların hepsininin defaıult constructor'ı boş bir container nesnesi oluşturur. Yani burada da boş bir yazı oluşuyor, empty true değer verecek.

```CPP
int main()
{
	using namespace std;

	string s1{ "nacati ergin" };
	string s2 = s1;
}
```
> Copy constructor çağırılacak ve eski ile yeninin değerini aynı yapacak. Fakat move constructor diğer nesnenin hayatını çalıyor.

```CPP
int main()
{
	using namespace std;

	string s1{ 100, 'A'};
	string s2 = std::move(s1);
}
```
> Burada = sağındaki X value expression dolayısıyla R value expression olduğu için move constructor çağırılacak s1 in kaynağımnı çalacak. Kaynağı çalınan nesne geçerli bir durumda olacak fakat durumunun ne olcağı konusunda bir garanti verilmeyecek. Ama genel olarak kaynağı çalınan bir string nesnesi default init edilmiş hale dönüyor. Tekrar atama yapılarak kullanılabilir. 

**Soru:** String uzunluğunun veri sınırı var mı?
> Var. Bütün containerların max_size isimli bir fonksiyonu var. Maksimuım öge miktarını döndüürüyor. 

```CPP
int main()
{
	using namespace std;

	string s;
	cout << s.max_size() << "\n";
}
```
> max yazı uzunluğunu döndürdü. Bu uzunluğun üzerinde yazı oluşturmaya yönelik bir işlem yaparsam ne olur? 

> Tipik olarak exception throw ediyor (Length error).

### Data constructor

- Bir adres ve tam sayı istiyor o adresten başlayarak bu kadar karakterlik bir yazıyla başlatmak istiyoruz.

```CPP
int main()
{
	using namespace std;

	char str[] = "ekrem kanberoglu";

	string s1(str, 5);
	cout << "|" << s1 << "|\n";
	
	string s2(str + 3, 2);
	cout << "|" << s2 << "|\n";
}
```

### range constructor 

```CPP
int main()
{
	using namespace std;

	char str[] = "polat ersoz";

	string s(str, str + 5);
	cout << "|" << s << "|\n";
}
```

- Şu üçünü birbirine karıştırma 

```CPP
	const char* p;
	const char* p, size_t n;
	const char* p1, const char* p2;
```

### initializer_list constructor

```CPP
int main()
{
	using namespace std;

	string s{ 'a','l','i' };
	cout << "(" << s << ")\n";
}
```

> Virgüller ile ayırırsan birleşecek. Başka bir örnek:

```CPP
int main()
{
	using namespace std;

	string s{65,66,67,68};
	cout << "(" << s << ")\n";
}
```
> ABCD çıktısı alınır.

### Few constructor
```CPP
int main()
{
	using namespace std;

	size_t n;

	cout << "kac tane:";
	cin >> n;

	cout << string(n, '*') << "\n";
}
```

**Başka birt örnek:**

```CPP
int main()
{
	using namespace std;
	
	for (int i = 1; i < 100; ++i)
	{
		cout << string(i, '*') << '\n';
	}
}
```
> Her satıra bir fazla yıldız basmış olduk.

**Bir sınav sorusu:**

```CPP
int main()
{
	using namespace std;
	
	string s1(49, 'A');
	cout << s1 << '\n';
	string s2(49, 'A');
	cout << s2 << '\n';
}
```
> Birinde küme parantezi diğerinde normal. Küme parantezi söz konusu olduğunda initializer_list parametreli constructor öncelkik kazanıyor (Overload resolution). Yani burada küme parantezi olduğu için few constructor değil initializer_list constructor devreye giriyor.

> Burada

**Bunun başka bir örneği**

```CPP
#include <string>
#include <iostream>

using namespace std;

class Nec {
public:
	Nec(int)
	{
		std::cout << "int\n";
	}
	Nec(initializer_list<int>)
	{
		std::cout << "initializer list\n";

	}
};

int main()
{
	Nec x(12);
	Nec{ 12 };
}
```
> Parantez kullanıldığında int parametreli constructor çağırıldı ama küme parantezi kullanılınca initializer_list parametreli constructor çağırıldı.

**Dikkat:** String sınıfının char parametreli bir constructor'ı yok. Bir char ile string'i başlatamazsın. Peki bunu nasıl yapabilirim?

```CPP
string s1("a");		// csting constructor
string s2(1, 'b');	//few constructor
string s3('c');		// initializer_list constructor
```

### substring constructor

```CPP
int main()
{
	string name{ "necatiergin" };
	string str(name, 6);
	cout << "[" << str << "]\n";
}
```
> 6 indexinden başlayarak geriye kalan karakterlerin hepsi, anlamına geliyor.

**Aynı örnek üzerinde değişiklik yapalım:**
```CPP
int main()
{
	string name{ "necatiergin" };
	string str(name, 6, 40);
	cout << "[" << str << "]\n";
}
```
> Normalde hata olması beklenir ama well defined. Tanımsız davranış değil. 

### Bir yazının karakterlerine nasıl erişebiliriz?

- [] operator fonksiyonu ile yazının karakterlerine erişilebilir. Bu operatore fonksiyonu const overload edilmiş. 

```CPP
int main()
{
	string str{ "mert" };
	str[0] = 's';
}
```
> Yazı değişti.

**Örnek:**
```CPP
int main()
{
	const string str{ "mert" };
	cout << str[20] << '\n';
}
```
> Tanımsız davranış. [] operatörü indeksi geçerliliğini sınamıyor.

> string sıbıfında bir de at fonksiyonu var. Bu da [] operatorü ile aynı görevi görüyor ama indeksin geçersiz olduğu durumda exception throw ediyor. 

```CPP
int main()
{
	string str{ "mert" };

	try {
		auto c = str.at(20);
	}
	catch (const std::exception& ex) {
		std::cout << "exception caught:" << ex.what() << '\n';
	}
}
```
> Çıktı: exception caught:invalid string position

- String türünden char* ya da const char* türüne örtülü dönüşüm yok. Şu kod her zaman sentaks hatası:

```CPP
using namespace std;

int main()
{
	string str{ "mustafa" };

	const char* p = str;
}
```
> Fakat bunu legal hale getirebiliriz. c_str fonsksiyonu yazının adresinin cstring olarak veriyor:

```CPP
using namespace std;

int main()
{
	string str{ "mustafa" };

	const char* p = str.c_str();
}
```
> Ama c_str char* değil const char* döndürüyor. Bu kod legal.

### Atama Operator Fonksiyonları

```CPP
using namespace std;

int main()
{
	string str{ "murathan" };
	string s;

	s = str;		// copy assignment
	s = move(str);	// move assignment
	s = '+';		// char parametreli assignment
	s = { 'a', 'k' };	//initializer_list parametreli assignment
}
```

### String nesnesini değiştirecek diğer operasyonlar:

- Sondan ekleme fonksiyonu pushback:

```CPP
using namespace std;

int main()
{
	string s{ "ali" };

	cout << s << "\n";
	s.push_back('m');
	cout << s << "\n";
}
```

- Sondan ekleme işlemi için += operator fonksiyonu da var.

```CPP
using namespace std;

int main()
{
	string s{ "ali" };

	cout << s << "\n";
	s += 'm';
	cout << s << "\n";
	s += "can";
	cout << s << "\n";

	s += {'o', 'g', 'l', 'u'};
	cout << s << "\n";
}
```
- Diğer bir ekleme yapma yolu da **append** fonksiyonunu çağırmak:

```CPP
using namespace std;

int main()
{
	string s{ "ali" };

	s.append(10, 'x');
}
```

**String sınıfının constexpr static bir veri elemanı var:** Bu veri elemanı size_type'ın en büyük değerini alıyor.

```CPP
int main()
{
	cout << "string::npos =" << string::npos << "\n";
}
```
- Bu ne işe yarıyor? Neden string npos u kullanıyoruz?

> 2 yerde kullnaılıyor:

1. Arama fonksiyonları
- C'nin arama  fonksiyonları adres döndürüyor. Aranan bulunursa adresinin bulunmazsa null pointer döndürüyorlar. Fakat string sınıfının arama fonksiyoınları adres değil indeks döndürüyor.

```CPP
string::size_type find(char)const;
```
> Aranan varlığı bulursa bulduğu yerin indeksini döndürüyor bulamazsa npos değerini döndürüyor. En büyük değer uızunluk değeri olabilir ama geçerli bir indeks olamaz. Dolayısıyla arama fopnksiyonlar npos döndürdüğünde o değer zaten geçerli olmayan bir indeks. Bu bir özel değer olarak kullanılıyor.

```CPP
using namespace std;

int main()
{
	string str{ "nihatuygar" };

	auto idx = str.find('k');

	cout << "idx =" << idx << "\n";
}
```
> npos değerini döndürecek. Yani buradan if kullanarak kodu düzenleyelim:

```CPP
using namespace std;

int main()
{
	string str{ "nihatuygar" };

	auto idx = str.find('k');

	if (idx != string::npos) {

	}
}
```
> Bulunduysa veya bulunamadıysa if içine giriyoruz.

# Ders 20 

### if with initializer

- C++ 17 ile dile eklenen yeni if deyimi.

```CPP
using namespace std;

int main()
{
	string str;
	cout << "bir yazı girin";
	getline(cin, str);	// Yazının içindeki boşluk karakterleri ile birlikte standart inputtan gelen karakterlerden oluşan bir string haline getirecek bizim nesnemizi
	cout << "[" << str << "]\n";
	
	if (auto idx = str.find('k'); idx != string::npos) {
		cout << "bulundu idx =" << idx << '\n';
	}
	else {
		cout << "bulunamadi\n";
	}

}
```
> if with initializer: noktalı virgülden önceki statementta bir değişken tanımlanabiliyor. Conditional expression, noktalı virgülden sonraki ifade. 

> Scope leakage engelliyor.

- Modern C++ ta if with initializer en sık kullanılan  kontrol deyimlerinden biri haline geldi. Scope daraltmak istediğimiz noktalawrda kullanabiliriz.

### Reserve Fonksiyonu

- Sınıfın reserve fonksiyonu kapasiteyi reserve eder. Reallocation minimize etmek veya bu ihtiyacı ortadan kaldırmak için kullanılabilecek bir fonksiyon. 

- Bir yazının runtime'da büyüyeceğini düşünelim:

```CPP
using namespace std;

int main()
{
	string s;

	for (int i = 0; i < 10000; ++i)
	{
		s += 'a';
	}
}
```
> Böyle yazarsak döngü bitene kadar defalarca reallocation olacak. Ben yazının büyüyeceğini zaten biliyorsam kodu değiştiriyorum:

```CPP
using namespace std;

int main()
{
	string s;

	s.reserve(10000);
	for (int i = 0; i < 10000; ++i)
	{
		s += 'a';
	}
}
```
> Kapasiteyi rezerve ettim. Size büyümeyecek. Yani bu kapasite yettiği sürece bir realocation yapılmayacak. 

- Diyelim ki yazımız çok büyüdü 50000 karakter oldu. Daha sonra sildik ve 10 karakter oldu. Yazının uzunluğu düşünce kapasite otomatik düşmeyecek. Eğer yine de kapasitenin küçülmesini istiyorsak bile o kapasite bloke edilmiş durumda.

```CPP
using namespace std;

int main()
{
	string s(300'000u, 'a');

	cout << "lenght =" << s.length() << '\n';
	cout << "capacity =" << s.capacity() << '\n';

	s.erase(1);
	
	cout << "lenght =" << s.length() << '\n';
	cout << "capacity =" << s.capacity() << '\n';
}
```
- **Çıktı:**

```CPP
lenght =300000
capacity =300015
lenght =1
capacity =300015

```

- Fazla kapasiteyi geri vermek istersek:

```CPP
using namespace std;

int main()
{
	string s(300'000u, 'a');

	cout << "lenght =" << s.length() << '\n';
	cout << "capacity =" << s.capacity() << '\n';

	s.erase(1);
	
	cout << "lenght =" << s.length() << '\n';
	cout << "capacity =" << s.capacity() << '\n';

	s.shrink_to_fit();
}
```

> Kapasiteyi uygun bir değere büzüyor. (Kendi stratejisine göre)

- STL containerlarında bir iterator interface var. Bu konum tutaun bir nesne. Pointerın üstünde daha yüksek seviyede bir soyutlama. Pointer adres tutan bir değişken ama bir iterator adres tutmak zorunda değil. iterator bir veri yapısından tutulan ögelerden birinin konumunu tutna bir varlık.

- Containerların iterator sınıfları tipik olarak nested type. Örneğin vector bir container. Ama vectordeki ögelerin konumunu tutan bir değişkene ihtiyacım olduğunda vector'un int açılımının iteratorü türünü kullanıyorum. 

```CPP
vector<int>::iterator
```

- String sınıfı da bir container olduğundan strinhg sınıfı türünden bir nesnenin yine bize iterator veren fonksiyonları var.

```CPP
string s{"hakan ozer"};
//string::iterator iter = s.begin();
auto iter = s.begin();
```

> Container begin fonksiyonu çağırıldığında bu fonksiyon container boş değilse container'daki ilk ögenin konumunu veriyor. Yukarıda begin fonksiyonu string'deki ilk ögenin konumunu döndürdü.

```CPP
using namespace std;

int main()
{
	string s{ "hakan ozer" };
	auto iter = s.begin();
	cout << *iter << '\n';
}
```
> İlk karakter olan h çıktı. ++iter yapıtığımda tıpkı pointerlarda olduğu gibi iterator containerdaki kendisinden sonra gelen ögenin konumunu tutma durumuna geçiyor.

```CPP
using namespace std;

int main()
{
	string s{ "hakan ozer" };
	auto iter = s.begin();
	cout << *iter << '\n';
	++iter;
	cout << *iter << '\n';
}
```
> h ve a yazdı.

- Bir başka sınıfın iterator veren fonksiyonunun ismi **end**. Son ögenin konumunu döndürmüyor. Sonuncudan sonraki olmayan ögenin konumunu döndürüyor. Böyle değerlere sentinal deniyor.
- Yani begin fonksiyonunun döndürdüğü iteratorü döngüsel yapıda sürekli arttırırsak end fonksiyonunun döndürdüğü konuma eşit olacak.

- Yani şöyle yazarsam yazının karakterlerini tek tek kullanmış olcağım:

```CPP
int main()
{
	string s{ "hakan ozer" };

	for (auto iter = s.begin(); iter != s.end(); ++iter) {
		cout << *iter << " ";
	}
}
```
> Aslında burada böyle bir döngü deyimi yazmak yerine derleyicinin bu döngü deyimini yazmasını sağlayacak bir döngü deyimi yazıyoruz. Bu da range based for loop. (İterator döngüsü)

- Ve bunun gibi uzun yazmak yerine Kısaca şöyle yazıtyoruz.
```CPP
using namespace std;

int main()
{
	string s{ "hakan ozer" };

	for (auto c : s) {

	}
}
```
- **algorithm** başlık dosyasında ismine algoritma denilen global fonksiyon şablonları programlamada en sık ihtyaç duyulan algoritmaları implemente ediyorlar. (Algorithm sözcüğü C++ dilinde 2 ayrı anlamda kullnaılıyor. Birisi programlamadaki altgoritmanın karşılığı, diğeri standart kütüphanenin başlık dosyalarında verilen global fonksiyon şablonları)

- Ama algoritmalar argüman olarak container nesnesi almak yerine range alıyorlar. Yani 2 tane konum.

- Diziyi büyükten küçüğe sıralayalım:

```CPP
using namespace std;

int main()
{
	int a[] = { 199, 3, 4123, 6,7,8, 13,788 };
	sort(a, a + sizeof(a) / sizeof(*a));

	for (auto i : a)
		std::cout << i << " ";
}
```

- string de bir STL container'ı. String'in de iterator, begin veren fonksiyonları var. O zaman ben bir string nesnesi üzerinden istediğim işlemi yapılmasını sağlayacak bir algoritmaya çağrı yapabilirim.

- Yazı işlemlerinin tamamı string sınıfı ile yapılmıyor. Bu yüzden yazı işlemkleri ile alakalı fınksiyonların hepsi string sınıfında değil. Bir string nesnesini sıralayalım:

```CPP
using namespace std;

int main()
{
	string str;

	std::cout << "bir yazı girin: ";
	getline(cin, str);
	cout << '|' << str << "|\n";

	//sort(str.begin(), str.end());  // aynı anlamda
	sort(begin(str), end(str));

	cout << '|' << str << "|\n";
}
```

- Yazıyı ters çevirmek istiyorum. string sınıfının reverse üye fonksiyonu yok ama reverse algoritması var.

```CPP
using namespace std;

int main()
{
	string str;

	std::cout << "bir yazı girin: ";
	getline(cin, str);
	cout << '|' << str << "|\n";

	reverse(str.begin(), str.end());

	cout << '|' << str << "|\n";
}
```
> STL algoritmasıyla yaptık.

**Not:** Reverse sadece string'ler için kullanılmadığından dolayı string sınıfında değil. Birçok reverse edilecek tür olduğu için. Generic zaten bu demek.

- string aslında hem bir container hem de yazı tutan bir nesne. O yüzden string sınıfında kullanımı kolaylaştımak için bir index interface i var. ama diğer taraftan bir container olduğu içiçn index interface yanı sıra bir iterator interface'i var. Burada bir karışıklık var çünkü bazı işlemleri her iki interface ile de yapabiliyor. 

## Insert İşlevleri

- Insert işlevleri hem index interface hem iterator interface kullnaıyor.

- Insert fonksiyonlarının iterator isteyen tüm overloadlarının özelliği, ilk parametreye iterator istiyor.

```CPP
#include <string>
using namespace std;

int main()
{
	string str{ "mustafa" };
	
	cout << str << "\n";
	str.insert(str.begin(), '!');
	cout << str << "\n";
	str.insert(str.begin(), 5, 'A');
	cout << str << "\n";
	str.insert(str.begin(),{'x', 'y', 'z'});
	cout << str << "\n";

}
```

### Index Parametreli Insert Fonksiyonları 

- 3 indeksine 5 tane x karakteri ekle
```CPP
using namespace std;

int main()
{
	string str{ "mustafa" };
	cout << str << "\n";

	str.insert(3, 5, 'X'); //3 indeksine 5 tane x karakteri ekle
	cout << str << "\n";
}
```

- Yazının başına sadece A karakteri ekle

```CPP
using namespace std;

int main()
{
	string str{ "mustafa" };
	cout << str << "\n";

	str.insert(0, 1, 'A'); 
	cout << str << "\n";
}
```

- s2'in bir kısmına s1'in tamamını insert et :

```CPP
using namespace std;

int main()
{
	string s1{ "muratkaymaz" };
	string s2{ "NECATI" };
 
	cout << s2 << "\n";

	s2.insert(5, s1);

	cout << s2 << "\n";

} 
```
- Bir tane daha argüman geçiyorum:

```CPP
using namespace std;

int main()
{
	string s1{ "muratkaymaz" };
	string s2{ "NECATI" };
 
	cout << s2 << "\n";

	s2.insert(3, s1, 7);

	cout << s2 << "\n";
}
```
> s2'nin 3 indeksine s1 stringinin 7 indeksinden başlayarak karakterleri yerleştirecek.

- string sınıfının üye fonksiyonlarının bir kısmı **void**, bir kısmı **idx** döndürüyor, bir kısmı **string&**, bir kısmı da iterator döndürüyor.

## Silme İşlemleri

- İlk ögeyi siliyorum:

```CPP
using namespace std;

int main()
{
	string str{ "mustafaaskopru" };

	cout << str << "\n";

	str.erase(str.begin());
	cout << str << "\n";
}
```

### Range Arrays
```CPP
using namespace std;

int main()
{
	string str{ "mustafa" };

	cout << str << "\n";

	str.erase(str.begin(), str.begin() + 3); // range
	cout << str << "\n";
}
```
> Belli bir aralığı sildik.

### Index ile silme işlemi:

```CPP
using namespace std;

int main()
{
	string str{ "ABCDRFGHI" };
	
	cout << "|" << str << "|\n";
	
	str.erase();
	cout << "|" << str << "|\n";
}
```
> Tümünü sildi. Kodu değiştirelim:

```CPP
using namespace std;

int main()
{
	string str{ "ABCDRFGHI" };
	
	cout << "|" << str << "|\n";
	
	str.erase(4);
	cout << "|" << str << "|\n";
}
```
> 4 indeksinden sonuna kadar sildi. Yine dğeiştirelim:

```CPP
using namespace std;

int main()
{
	string str{ "ABCDRFGHI" };
	
	cout << "|" << str << "|\n";
	
	str.erase(3, 4);
	cout << "|" << str << "|\n";
}
```
> Indeks 3'ten başlayıp 4 karakter sildi.

### Bir stringi tamamen silmek 

```CPP
using namespace std;

int main()
{
	string str{ "ABCDRFGHI" };
	cout << str.size() << "\n";

	str.erase(str.begin(), str.end());
	str.erase();
	str.clear();
	str.resize(0);
	str = "";
	str = {};
	str = string{};		// default init edilmiş bir string boyutu sıfırdır.
}
```

**Örnek:**

```CPP
using namespace std;

int main()
{
	string str;

	cout << "bir yazi gir";

	getline(cin, str);

	cout << "[" << str << "]\n";
}
```
> Newline gelene kadar tüm karakterleri string'e alacak. Buna bir parametre daha girersek: 3. parametre ile karşılaştırğında tamamlanacak:

```CPP
using namespace std;

int main()
{
	string str;

	cout << "bir yazi gir";

	getline(cin, str, ',');

	cout << "[" << str << "]\n";
}
```
> 3. bir karakter var ve bu newline karakteri gibi..

- Yazının her döngüde bir karakterini silelim:

```CPP
using namespace std;

int main()
{
	string str;

	cout << "bir yazi gir";

	getline(cin, str);

	cout << "[" << str << "]\n";

	while (!str.empty()) {
		cout << str << "\n";
		str.erase(str.begin());
	}
}
```
## String Sınıfının Arama Fonksiyonları

```CPP
		str.find
		str.rfind
		str.rfind_first_of
		str.rfind_first_not_of
		str.find_last_of
		str.find_not_last_of
		str.starts_with	//C++20
		str.ends_with	//C++20
		str.contains	//C++23
```

- **str.find**: Doğrudan bir varlığı arıyor. Bu varlık karakter, cstring, başka bir string, data parametre, substring parametre olabilir.
- **str.rfind**: Aramayı sondan başa doğru yapıyor. Find ile aynı işi yapıyor.
- **str.rfind_first_of**: Yazının içinde bir karakter grubundaki karakterlerden ilkini buluyor. Örneğin yazıdaki ilk sesli harfi bulacaksak fonksiyona ariou karaktewrlerinin argüman olarak geçeriz.
- **str.rfind_first_not_of**: Find first of'un tersi. Karakterlerden birinin olmadığı ilk konumu döndürecek.
- **str.find_last_of:**: Karakterlerden biriyle karşılaşılan son konumu verecek.
- **str.find_not_last_of:** Find first not of'un sondan başa çalıştırılmış hali.

- **str.starts_with:** Boolean döndürüyor. Başlangıçta veya sonda var mı?
- **str.ends_with**
- **str.contains:** Var mı yok mu? Yazıda ali yazısı var mı yok mu? Boolean döndürüyor

**Not:** Find geçen tüm fonksiyonların aranan değer bulunamazsa döndürdüğü değer npos. Başarılı olursa Index döndürecek.

**Örnek:**
```CPP
int main()
{
	string str{ "can dedi ki bana can dedi ki bana can dedi" };

	cout << str.length() << "\n";
	cout << str.rfind("can") << "\n";
}
```
> Uzunluk 42 ve bulunduğu yer 37 olarak döndü.

**Örnek:**
```CPP
int main()
{
	string str{"cemtopkaya"};

	cout << str.find_first_of("mxytz") << "\n";
}
```

**Örnek:**
```CPP
int main()
{
	string str{"cemtopkaya"};

	cout << str.find_first_not_of("mxycetz") << "\n";
}
```

**Örnek:**
```CPP
int main()
{
	string str{"cemtopkaya"};

	cout << str.find_last_of("mxycetz") << "\n";
}
```
**Örnek:**
```CPP
int main()
{
	string str{"cemtopkaya"};

	cout << str.find_last_not_of("pyaku") << "\n";
}
```
**Örnek:** Dosya ismi ali ile başlıyormu?

```CPP
int main()
{
	string filename;

	cout << "bir dosya ismi girin:";
	cin >> filename;

	if (filename.starts_with("ali"))
		cout << "evet\n";
	else
		cout << "hayır\n";
}
```

**Örnek:** Dosya ismi jpg ile bitiyor mu?

```CPP
int main()
{
	string filename;

	cout << "bir dosya ismi girin:";
	cin >> filename;

	if (filename.ends_with(".jpg"))
		cout << "evet\n";
	else
		cout << "hayır\n";
}
```

### substring operations

- Stringlerde en fazla ihtiyaç duyulan işlemlerden biri, bir yazının belirli bir kısmını (substring'ini) elde edip o substring üzerinde işlemler yapmak. Ama bu pahalı bir operasyon, büyük yazılar için doğrudan substr fonksiyonu ile yapmayın.

```CPP
int main()
{
	string str{ "murathan aksoycan"};

	cout << "|" << str.substr(5, 5) << "|\n";
}
```
> 9 indeksinden başlayarak 5 karakterlik bir substring elde edeceğim. Burada 2. parametre default argüman olarak string-npos alıyor. Yani tek argüman ile çağırırsam verdiğim endeksten sonuna kadar elde ediyorum.

- Burada str nin çok uzun bir string olduğunu varsayalım. 

```CPP
cout << "|" << str.substr(4000, 1000) << "|\n";
```
> Burada aslında 1000 kakrakterlik yeni bir string oluşturuyoruz. Bunun ciddi bir maliyeti var. Eğer bu substring üzerinde salt okulmaya yönelik bir işlem yapılacaksa: bir string view nesnesi oluşturuyoruz.

```CPP
string_view sv; 
```
> Aslında içinde 2 tane pointer tutuyor. Bu pointerlar bellek alanındaki pointerlar. 

- String sınıfının non-modifying bütün sınıfları aslında SV sınıfında da var. Yani biz string sınıfı türünden yeni bie nesne oluşturmak yerine SV sınıfı türünden oluşturduğumuzda aslında başka bir bellek alanı tarafından tutulan bir yazının belirli bir kısmını göslemci olarak kullanıyoruz. Gereksiz kopyalamanın önüne geçmiş oluyoruz.

## Karşılaştırma İşlemleri

- String neslelerini birbirleriyle ya da cstring nesneleriyle karşılaştırmak operator overloading ile mümkün. 

```CPP
int main()
{
	string str{ "necati ergin"};

	str.compare("ali");
}
```

**Bir örnek:**

```CPP
int main()
{
	string s1(100'000, 'a');
	string s2(200'000, 'b');

	auto temp = s1;
	s1 = s2;
	s2 = temp;
}
```
> Bu çok kötü bir kod. Çünkü 2 string i bu şekilde swap ederseniz, temp için copy constructor çağırılır, s1 ve s2 için copy assignment cağırılır. Yani daha temp oluşurken 100bin byte lık bir bellek alanı alocate edip kopyalıyoruz. Buna gerek yok. 2 string i swap etmek istiyorsam içindeki pointerları swap edebilirim. Yani dinamik bellek bloğundaki karakterlere dokunmış oluıp sadece içindeki pointerları swap edicem. İşte üye fonksiyonu olan swap foınksiyonu çağırınca bu oluyor.

```CPP
int main()
{
	string str{ "tolgahan" };
	cout << "[" << str << "]\n";

	str.replace(2, 4, "XYZ");
	cout << "[" << str << "]\n";
}
```

### Toplama

```CPP
int main()
{
	string s1{ "hasan" };
	string s2{ "can" };

	cout << s1 + s2 << "\n";
	// cout << operator+(s1, s2) << "\n";
}
```
> Burada yapılan işlem aslında operator+'yı çağırıp ona s1 ve s2 yi argüman olarak gönderiyorum

### Dönüştürme Fonksiyonları

```CPP
int main()
{
	string str{ "874325mehmet" };

	auto ival = stoi(str);

	cout << "ival = " << ival << "\n";
}
```

```CPP
int main()
{
	string str{ "12ali" };

	size_t idx;

	auto ival = stoi(str, &idx, 16);

	cout << "ival = " << ival << "\n";
	cout << "idx = " << idx << "\n";
}
```

```CPP
int main()
{
	int ival = 3567;
	
	auto s = "necati" + to_string(ival) + ".jpeg";

	cout << s << "\n";
}
```
> int değerini string e dönüştürdük.

** Örnek:** Yazıdaki ilk a karakterini silecek kodu yazın

```CPP
int main()
{
	string str;

	cout << "biraz yazı girin";
	getline(cin, str);

	cout << "[" << str << "]\n";

	if (const auto idx = str.find('a'); idx != string::npos) {
		// str.erase(idx, 1);
		str.erase(str.begin() + idx);
		cout << "[" << str << "]\n";
	}
	else {
		cout << "bulunamadi\n";
	}
}
```

# Ders 21 

## Inheritance (Kalıtım)

- C++ dilinde kalıtım, nesne yönelimli programlamadaki kalıtımı aşan bir kavram çünkü farklı amaçlarla da kulanılıyor. Nesne yönelimli programlamada kalıtım sınıflar araısndaki ilişkiyi implemente eden araç olarak ele alınmalı. 

**Kalıtım:** Bir sınıf aynı zamanda başka bir sınıf türünden kabul edilecek. Bir sınıf başka bir sınıfın public interface'ini tamamen kendisine katmış olacak. Yani her varlığıun aynı zamanda daha genelleştirilmiş bir varlık cinsinden olduğunu belirtiyoruz aslında. (Her mercedes bir arabadır, Her C++ programcısı bir programcıdır.) {Is a relationship}

- Nesne yönelimli programlamada kalıtım programın çalışma zamanıytla ilgili. Fakat C++ ta kalıtımı generic programlama tarafında, Programın çalışma zamanından bağımsız, derleme zamanına yönelik te kullanıyoruz. 

**C++ dilinde kalıtım:** 
1. Eski kodların değişiklik yapılmadan yeni kodları kullanabilmesi. Yani kod sisteminde bir değişiklik yapılması gerektiğinde eski kodları değiştirmeden yeni kodların eski kodları kullanabilmesini sağlamak. Yani eski kodları daha alt seviyedeki kodlara bağımlı değil. C gibi bir dilde eski kodlar daha alt seviyedeki kodları kullanmak zorunda.
2. Kodların yeniden kullanımı (Code reuse) 

- Kalıtımda kaynak olarak kullanacağımız sınıf: parent class, super class.

- Car sınıfından Mercedes sınıfını kalıtım yoluyla elde ettiğimizde burada parent class var sınıfı. Yani artık araba gereken her yerde mercedes kullanılabilir diyebiliriz.

- Kalıtım aracı 3 ana kategoriye ayrılıyor:

1. public inheritance
2. private inheritance
3. protected inheritance

- Kalıtımda kullanılacak taban sınıfın complete type olması gerekiyor.

```CPP
class Base {
public:
	void f1();
	void f2();
};

class Der : public Base {

};

class Der : private Base {

};

class Der : protected Base {

};
```

**Not:** Bir anahtar sözcük kullanmadığımız zaman default olarak private inherritance. 

- Eğer kalıtımda oluşturğumuz sınıf class anahtar sözcüğü ile değil de struct ile oluşturulsaydı, kalıtım biçimi public olacaktı.

```CPP
class Base {
public:
	void f1();
	void f2();
};

struct Der : Base { // public inheritance

};
```
> Her **Der** nesnesi aynı zamanda **Base** türünden bir nesnedir. 

![image](https://user-images.githubusercontent.com/75746171/212338569-6f77588c-f5ed-418a-9056-2d8d9476b8e3.png)

- A'nın içinde bir B nesnesi var. Ya A'nın B türünden bir elemanı vardır ya da A, B sınıfından kalıtım yoluyla elde edilmiştir.

**Eğer A'nın B türünden bir elemanı varsa:**

```CPP
class A {
	int x, y;
};

class B {
private:
	A ma;
};

int main()
{
	constexpr auto sz = sizeof(B);
}
```
> sizeof değerleri aynı.

**A, B sınıfından kalıtım yoluyla elde edilmişse:**

```CPP
class A {
	int x, y;
};

class B : public A {
private:
};

int main()
{
	constexpr auto sz = sizeof(B);
}
```
> Yine aynı değerdeler.

- Taban sınıfın ve türemiş sınıfın scope'u ayrı. 

```CPP
class Base {
public:
	void func(int);
};

class Der : public Base {
public:
	void func(double);
};
```
> Function overloading yok. Scopelar farklı.

- Nokta operatörünün ya da ok operatörünün sağında kullanılan isim eğer sol operand türemiş sınıf türünden ise önce türemiş sınıfta, bulunmaz ise taban sınıfta aranır.

```CPP
class Base {
public:
	void foo(int);
};

class Der : public Base {
public:
	void foo(int, int);
};

int main()
{
	Der myder;

	myder.foo(10);
}
```
- İsim arama bittikten sonra fonksiyonun uygun olmadığı anlaşılıyor ve sentaks hatası veriyor.

```CPP
using namespace std;

class Base {
public:
	void foo(int);
};

class Der : public Base {
public:
	void foo(int, int);
};

int main()
{
	Der myder;

	myder.foo(12, 34);
	myder.Base::foo(12);
}
```
> Maskelemeyi bu şekilde aşabiliriz.

```CPP
using namespace std;

class Base {
public:
	void foo();
};

class Der : public Base {
public:
	void func()
	{
		foo();  // Base::foo();
	}
};
```
> İki türlü de çağırabliriz.

- Car > Mercedes > Mercedes_S500 

> Mercedes sınıfı mercedes_S500 ün direct base class'ı

> Car sınıfı mercedes_S500'ün indirect base base class

**Hatırlatma:** Taban sınıfının üye fonksiyonu ile türemiş sınıfın üye fonksiyonu birbirini overload etmiyor.

### Erişim kontrolü
- Türemiş sınıf taban sınıfın public ve protected bölümüne erişebilir. Ama private bölümüne erişemez.

**Public:** Her koda açık
**Protected:** Kalıtım yoluyla elde edilecek sınıflara açık
**Private:** TÜm kodlara kapalı.

**Örnek:**

```CPP
class Base {
public:
	void foo(int);
};

class Der : public Base {
private:
	void foo(double);
};

int main()
{
	Der myder;

	myder.foo(12);
}
```
> Hatanın sebebi erişim kontrolü. Der sınıfında isim bulundu fakat erişim kontrolüne takıldı.

- Türemiş sınıf türünden bir nesne aynı zamanda taban sınıfı türünden kabu ledildiği için, türemiş sınıf türünden taban sınıf türüne örtülü dönüşüm var. 

**Upcasting:** Türemiş sınıftan taban sınıfa yapılan dönüşüm. Örtülü.

**Örnek:**

```CPP
class Base {

};

class Der : public Base {

};

int main()
{
	Der myder;

	Base* ptr = &myder; //upcasting
	Base& basaref = myder;  /aynısını referans ile yaptık
}
```

**Downcasting:** Taban sınıftan türemiş sınıfa yapılan dönüşüm.

**Türemiş sınıf nesnesi içindeki taban sınıf nesnesinin hayata gelme ve sonlanma durumu:**

- Bir türemiş sınıf nesnesi hayata geldiğinde önce onun taban sınıf nesnesi hayata geliyor. 

- Eğer türemiş sınıf default ctor'ı derleyici tarafından default ediliyor ise derleyici türemiş sınıf nesnesi içindeki taban sınıf nesnesi için default ctor çağıracak. 

```CPP
class Base {
public:
	Base()
	{
		std::cout << "Base default ctor\n";
	}
};

class Der : public Base {
public:

};

int main()
{
	Der myder;
}
```

> Der sınıfı için defaukl ctor'ı derleyici yazdı. Derleyici yazdığı default constructorda der içindeki alan sınıfı nesnesini, base sınıfının default ctor'ına çağrı yaparak hayata getirdi.

- Base'in default değil de int parametreli constructor olsaydı:

```CPP
class Base {
public:
	Base(int)
	{
		std::cout << "Base(int) ctor\n";
	}
};

class Der : public Base {
public:

};

int main()
{
	Der myder;
}
```
> Hatalı kod. Eğer derleyici bir sınıf için bir special member function yazıyor ise ve yazdığında sentaks hatası oluşuyorsa derleyici default etmesi gereken special member function'ı delete ediyordu. 

```CPP
class Base {
public:
	Base()
	{
		std::cout << "Der ctor\n";
	}
	~Base()
	{
		std::cout << "Base destructor\n";
	}
};

class Der : public Base {
public:
	Der()
	{
		std::cout << "Der ctor\n";
	}
	~Der()
	{
		std::cout << "Der destructor\n";
	}
};

int main()
{
	Der der;
}
```
> Der default ctor çağırıldı. Ama programın akışı Der'in ana bloğunun içine girmeden Base default ctor çağırılacak. Der nesnesinin hayatı bittiğinde destructor'ı çağırılacak. Önce destrcutor ana bloğu içinmdeki kodlar çalışacak. Bundan sonra derleyicinin eklediği taban sınıfın destructor'ına yapılan çağrı var.

> Yani sırayla **Der ctor - Base ctor - Der destructor - Base destructor**

```CPP
using namespace std;

class Member {
public:
	Member()
	{
		std::cout << "Member Default ctor \n";
	}
	~Member()
	{
		std::cout << "Member destructor\n";

	}
};

class Base {
public:
	Base()
	{
		std::cout << "Der ctor\n";
	}
	~Base()
	{
		std::cout << "Base destructor\n";
	}
};

class Der : public Base {
public:
	Der()
	{
		std::cout << "Der ctor\n";
	}
	~Der()
	{
		std::cout << "Der destructor\n";
	}
private:
	Member mx;
};

int main()
{
	Der der;
}
```

- Diyelim ki burada der'in default cosntructor yok. Sadece int parametreli var. Der sınıfını base sınbıfından elde edicem: 

```CPP
class Base {
public:
	Base(int)
	{
		std::cout << "Base(int)\n";
	}

};

class Der : public Base {
public:
	Der()
	{
		std::cout << "Der ctor\n";
	}
};
```
> Sentaks hatası. Default etmedik. Kendimiz yazdık.

![image](https://user-images.githubusercontent.com/75746171/212399476-7e5bfa0f-9514-46b2-b846-2993d8cb671e.png)

**Soru:** Mercedes_S500'ün ctor'nı ben yazıyorsam constructor initlizer list ile var sınıfının constructorına çağrı yapabilir miyim?
- Hayır. Doğrudan taban sınıfdının constructorını çağırmalıyım.

**Kalıtımda Diğer Özel Fonksiyonların Durumu**

- Sınıfın copy constructor'ı derleyici tarafından yazılırsa, Derleyicinin yazdığı copy contructor * this in içindeki taban sınıfı nesnesinin copy constructor'ını çağıracak.

```CPP
class Base {
public:
	Base()
	{
		std::cout << "Base default constructor\n";
	}

	Base(const Base& other)	//copy ctor
	{
		std::cout << "Base copy constructor\n";
	}
};

class Der : public Base {

};

int main()
{
	Der d1;
	Der d2 = d1;
}
```
Çıktı:
Base default constructor
Base copy constructor

> Der sınıfının copy constructorını derleyici yazdı. Bu constructor Der nesnesinin içindeki Base'i, Base'in copy constructor'ını çağırarak hayata getirdi.

> Base default cosntructor, d1'in içindeki base için çağırıldı.

> Base copy constructor, d2'in içindeki base için çağırıldı.

- Ama türemiş sınıf için copy constructor'ı biz yazarsak:

```CPP
class Base {
public:
	Base()
	{
		std::cout << "Base default constructor\n";
	}

	Base(const Base& other)	//copy ctor
	{
		std::cout << "Base copy constructor\n";
	}
};

class Der : public Base {
public:
	Der()
	{
		std::cout << "Der default ctor\n";
	}
	Der(const Der&)
	{
		// dikkat taban sınıf nesnesi için copy ctor değil defauult ctor çağırılacak.
		std::cout << "Der copy ctor\n";
	}
};

int main()
{
	Der d1;
	Der d2 = d1;
}
```
> D1 için önce içindeki base için base default ctor çağırılacak sonra der default ctor çağırılacak.

> d2'nin içindeki base için base default ctor çağırılacak. 

> Der için çağırılan copy cosntructor, der'in içindeki base nesnesi için copy ctor'ı çağırmadığından derleyici oraya base için çağırılacak olan default constructor çağrısını ekledi.

- Türemiş sınıf için copy ctor'ı veya move ctor'ı siz yazıyorsanız, taban sınıfı nesnesinin copy ya da move construct edilmesinden siz sorumlusunuz.

**Örnek:**

```CPP
class Base {
public:
	void func(int);
};

class Der : public Base {
public:
	void func(double);
};

int main()
{
	Der myder;

	myder.func(12.5);
	myder.func(45);
}
```
> Burada function overloading yok ama function overloading etkisi yaratmak istiyorsam: Türemiş sınıfa int parametreli bir fonksiyon ekleriz ve bunu taban sınıf fonksiyonunu çağrımasını sağlarız:

```CPP
class Base {
public:
	void func(int)
	{
		std::cout << "Base::func(int x) x =" << x << "\n";
	}
};

class Der : public Base {
public:
	void func(double);
	{
		std::cout << "Der::func(double)\n";
	}

	void func(int x)
	{
		Base::func(x);
	}
};

int main()
{
	Der myder;

	myder.func(12.5);
	myder.func(45);
}
```
> Şimdi fuction overload resolutionda int parametreli fonksiyn çağğırılacak ve o da taban sınıfın fonksiyonunu çağıracak.

- Diğer bir yol: Sınıf tanımı içinde yapılan using bildirimi:

```CPP
class Base {
public:
	void func(int x)
	{
		std::cout << "Base:func(int x) x =" << x << "\n";
	}
};

class Der : public Base {
public:
	using Base::func;
	void func(double)
	{
		std::cout << "Der::func(double)\n";
	}
};

int main()
{
	Der myder;

	myder.func(12.5);
	myder.func(45);
}
```

### Inherited Contructor

- Aslında inherited constructor, diğer üye fonksiyonlar için using bildiriminin yapılması ile aynı anlamda.

```CPP
class Base {
public:
	Base(int);
	Base(int, int);
	Base(double);

};

class Der : public Base {
public:

};

int main()
{
	Der myder(12);
}
```
> Bir sınıfı bir başka sınıftan kalıtım yoluyla elde ettiğimiz zaman, türemiş sınıfın cosntructorları taban sınıfın constructorlarını çağırmak zorunda. Bunu yapmanın yolalrında biri:

> Biz ctor yazıcaz. Bu ctor taba sınıfın ctor ına constructor initilazer list ile çağrı yapacak.

### Runtime Polymorphism (Çalışma zamanı çok biçimliliği)

- Taban sınıfın üye fonksiyonlarını nesneye yönelik programlamasında belirli kategorilere ayırıyoruz.
- İlk sınıf taban sınıfın öyle bir metotu ki türemiş sınıflara hem bir arayüz hem de kod veriyor. Yani eğer taban sınfın öyle birmetotundan bahsediyorsak bu metot kalıtımla elde edilmiş  sınıflara metodun kodlarını veriyor. Yani o fonksiyon çağırıldığında aslında onun kodları çalışacak. He mbir interface hem de bir implementasynon veriyor. 
- Diğer bir sınıf türemiş sınıflara hem bir arayüz hem de default implementasyon veriyor. Yani default bir kod veriyor, isterse o kodu kullanır, isterse kendi bir kod oluşturur.

**Örnek:**
- Airplane -> fly isimli fonksiyonu  (boeing uçağı)

> Kalıtım yolu ile elde edilecek sınıflar airplane'in verdiği kod ile uçabilir veya kendisi ayrı bir kod da oluşturabilir. Bunu biz ayarlyırouz.

- Eğer taban sınıf türemiş sınıfa bir arayüz vermiş aynı zamanda default implementasyon vermişse (Yani implementasyonu istemiyorum, kendim kod oluşturacağım) buna nesne yönelimli programlamada türemiş sınıfın, taban sınıfın o fonksiyonunu override etmesi deniyor.

**Örnek:**
- Taban sınıfın fly fonksiyonunu, türemiş sınıf olan boeing sınıfı override ederse ne demiş oluyor:

> Taban sınıfının fly fonksiyonunun kodu var ama ben o kodu istemiyorum, boeing uçması gereken yerde, boeing'in sağladığı fly fonksiyonunun kodu çalışacak.

**C++ dilinde bunun karşılığı:**

```CPP
class Airplane {
public:
	void take_off();
};

class Boeing : public Airplane {

};
```
> Normalde boeing client'ları take_off u çağırabilecekler ama airplane'in sağladığı kod çalışacak.

```CPP
class Airplane {
public:
	void take_off();	//interface var, implementasyon da aldım
	virtual void fly();	// interface aldım ama default olarak da bir implementasyon aldım.
};

class Boeing : public Airplane {

};
```
> Airplane, kalıtım yolu ile elde edilecek sınıflara fly'ı veriyor. Onlara bir şans tanıyor. İsterseniz bunu kullanın isterseniz kendi kodunuzu kullnaıın. Boeing eğer Airplane'in sağladığı kodu tercih ediyorsa o zaman override etmeyecek. 

```CPP
class Airplane {
public:
	void take_off();	//interface var, implementasyon da aldım
	virtual void fly();	// interface aldım ama default olarak da bir implementasyon aldım.
	virtual void land() = 0; // pure virtual function

};

class Boeing : public Airplane {

};
```
> Bu da **pure virtual function**.  Burada interface aldım, implementasyonm almadım. Ben ancak land için bir kod yazarsam boeing'ler iniş yapabilecekler.

- **fly** Senin kodun değil benim istediğim kod çalışsın.
- **land** boeing'in inişi için gerekli kodu ver. Land fonksiyonu override edilmek zorunda.

# Ders 22

- Taban sınıfın en az bir virtual fonksiyonu varsa böyle sınıflara polimorfik sınıf diyoruz. 
- Eğer bir sınıfın en az 1 subsanal fonksiyonu varsa ya da en az 1 sana fonksiyıonu olan sınıftan kalıtım yoluyla elde edilmişse ama onun subsana fonksiyonlarının hepsini override etmemişse abstract class deniyor:

```CPP
class Airplane {
public:
	void take_off();
	virtual void fly() = 0;
};
```

> Airplane şu anda abstract class. Subsanal fonksiyonu var.

```CPP
class Airplane {
public:
	void take_off();
	virtual void fly() = 0;
};

class Boeing : public Airplane {

};

```
> Boeing sınıfı Airplane sınıfının fly fonksiyonunu override ettiğini varsayarsak o zaman boeing de abstract class. Abstract olmaması için taban sınıfın bütün sanal-subsanal fonksiyonlarını override etmemiz gerekiyor.

- Abstract olmayan sınıflar : Concrete Sınıflar (Somut)

> Abstract sınıflar türünden nesne oluşturmak sentaks hatası.

```CPP
class Airplane {
public:
	virtual void fly() = 0;
	virtual void take_off() = 0;
	virtual void land() = 0;
};

class Boeing : public Airplane {

};

int main()
{
	Airplane a;
}
```
> object of abstract class type is not allowed 

```CPP
class Airplane {
public:
	virtual void fly() = 0;
	virtual void take_off() = 0;
	virtual void land() = 0;
};

class Boeing : public Airplane {

};

int main()
{
	Airplane b;
}
```
> Aynı hatayı verdi. Çünkü Boeing sınıfı Airplane sınıfının Pure virtual fonksiyonlarını override etmedi.

### Virtual Functions

```CPP
class Car {
public:
	void start()
	{
		std::cout << "car has started!\n";
	}

	void run()
	{
		std::cout << "car is running now!\n";
	}

	void stop()
	{
		std::cout << "car has just stopped!\n";
	}

};

class Fiat : public Car {
public:
	void start()
	{
		std::cout << "fiat has started!\n";
	}

	void run()
	{
		std::cout << "fiat is running now!\n";
	}

	void stop()
	{
		std::cout << "fiat has just stopped!\n";
	}
};


class Audi : public Car {
public:
	void start()
	{
		std::cout << "audi has started!\n";
	}

	void run()
	{
		std::cout << "Audi is running now!\n";
	}

	void stop()
	{
		std::cout << "audi has just stopped!\n";
	}
};

class Mercedes : public Car {
public:
	void start()
	{
		std::cout << "Mercedes has started!\n";
	}

	void run()
	{
		std::cout << "Mercedes is running now!\n";
	}

	void stop()
	{
		std::cout << "Mercedes has just stopped!\n";
	}
};

void car_game(Car& cr)
{
	cr.start();
	cr.run();
	cr.stop();

}

int main()
{
	Mercedes m;
	Audi a;
	Fiat f;

	car_game(m);
	car_game(a);
	car_game(f);
}
```
> Çıktılar :

car has started!
car is running now!
car has just stopped!
car has started!
car is running now!
car has just stopped!
car has started!
car is running now!
car has just stopped!


- Bu fonksiynoların bildiriminde virtual kullanalım:

```CPP
class Car {
public:
	virtual void start()
	{
		std::cout << "car has started!\n";
	}

	virtual void run()
	{
		std::cout << "car is running now!\n";
	}

	virtual void stop()
	{
		std::cout << "car has just stopped!\n";
	}

};

class Fiat : public Car {
public:
	void start()
	{
		std::cout << "fiat has started!\n";
	}

	void run()
	{
		std::cout << "fiat is running now!\n";
	}

	void stop()
	{
		std::cout << "fiat has just stopped!\n";
	}
};


class Audi : public Car {
public:
	void start()
	{
		std::cout << "audi has started!\n";
	}

	void run()
	{
		std::cout << "Audi is running now!\n";
	}

	void stop()
	{
		std::cout << "audi has just stopped!\n";
	}
};

class Mercedes : public Car {
public:
	void start()
	{
		std::cout << "Mercedes has started!\n";
	}

	void run()
	{
		std::cout << "Mercedes is running now!\n";
	}

	void stop()
	{
		std::cout << "Mercedes has just stopped!\n";
	}
};

void car_game(Car& cr)
{
	cr.start();
	cr.run();
	cr.stop();

}
```
> Çıktılar: 

Mercedes has started!
Mercedes is running now!
Mercedes has just stopped!
audi has started!
Audi is running now!
audi has just stopped!
fiat has started!
fiat is running now!
fiat has just stopped!

> Bu sefer bizim sınıfların fonksiyonları çağırıldı. Burada mercedes, audi ve fiat sınıfları taban sınıfın sanal fonksiyonlarını overeride etti.

- Biz fonksiyon çağırısını Car referan ya da poniterıyla yaptığımızda hangi fonksiyoınun çağırılacağı artık derleme zamanında değil, programın çalışma zamanında anlaşılacak.

- Derleyici fonksiyon çğaırısı koduna bakarak hangi fonksiyoınun çağırıldığını anlıyorsa (Derleme zamanında) static binding denir. (Early binding)

**Not:** Function overloading'te derleyici 10 tane overload'dan hangisinin çağırılacağını koda bakarak anlıyor. Bu static binding tir. Yani runtime maliyeti yok. 

- Fakat programın çalışma zamanıdna kşan bir kod ile bu anlaşılıyorsa buna dynamic binding (late binding) denir. Az önceki bir dynamic binding durumuydu. 

**Örnek:** Programın çalışma zamanında nesnenin ne olduüğuınu seçelim:

```CPP
class Car {
public:
	virtual void start()
	{
		std::cout << "car has started!\n";
	}

	virtual void run()
	{
		std::cout << "car is running now!\n";
	}

	virtual void stop()
	{
		std::cout << "car has just stopped!\n";
	}

};

class Fiat : public Car {
public:
	void start()
	{
		std::cout << "fiat has started!\n";
	}

	void run()
	{
		std::cout << "fiat is running now!\n";
	}

	void stop()
	{
		std::cout << "fiat has just stopped!\n";
	}
};


class Audi : public Car {
public:
	void start()
	{
		std::cout << "audi has started!\n";
	}

	void run()
	{
		std::cout << "Audi is running now!\n";
	}

	void stop()
	{
		std::cout << "audi has just stopped!\n";
	}
};

class Mercedes : public Car {
public:
	void start()
	{
		std::cout << "Mercedes has started!\n";
	}

	void run()
	{
		std::cout << "Mercedes is running now!\n";
	}

	void stop()
	{
		std::cout << "Mercedes has just stopped!\n";
	}
};

void car_game(Car& cr)
{
	cr.start();
	cr.run();
	cr.stop();

}

Car* create_random_car()
{
	switch (rand() % 3) {
	case 0: return new Mercedes;
	case 1: return new Audi;
	case 2: return new Fiat;
	default: return nullptr;
	}
}
int main()
{
	srand(static_cast<unsigned>(time(0))); // Her defasında farklı bir sayı zinciri için
	for (;;) {
		Car* cp = create_random_car();
		car_game(*cp);
		(void)getchar();
	}
}
```
> Derleme zamanında derleyicinin runtime'da üretebileceği rastgele sayıları bilemeyeceğinme göre öyle bir mekanizma var ki hangi fonksiyonun çağırılıdığı programın çalılma zamanında anlaşılıyor.

```CPP
class Base {
public:
	virtual void func(int);
};

class Der : public Base {
public:
	int func(int);
};
```
> Fonksiyon sanal olduğundan artık türemiş sınıfın aynı imzaya farklı geri dönüş türüne sahip bir fonksiyon bildirmesi sentaks hatası. (Bunun bir istisnası var)

> Taban sınıfın sanal fonksiyonunu override etmek için ismi, imzası, geri dönüş değeri türü aynı olan bir fonksiyon bildirilmek zorunda. 

```CPP
class Base {
public:
	virtual void func(int);
};

class Der : public Base {
public:
	void func(int);
};
```
> Doğru kod.

- Modern C++ ile dile yeni bir anahtar sözcük kategorisi daha eklendi. Contextual keyword. (Bağlamsal anahtar sözcük)

> Yani belirli bir alanda anahtar sözcükl etkisi yapıyor ama o context dışında identifier olarak kullanılabiliyor. Neden böyle bir araç eklendi? 

> Eğer contextual kewword kavramı eklenmeseydi, override direkt keyword yapılsaydı daha eskiden yazılmış kodlarda override identifier olarak kullanılmışsa o  kodlar yeni derleyiciler ile derlendiğinde sentaks hatası verecekti.  Override ve final keyword leri.

- Sanal fonksiyonu overriede etmenin yolu sadece buydu:

```CPP
class Base {
public:
	virtual void func(int);
};

class Der : public Base {
public:
	void func(int);
};
```
- Override ekliyoruz:

```CPP
class Base {
public:
	virtual void func(int);
};

class Der : public Base {
public:
	void func(int)override;
};
```
Sentakjs açısından mecburiyet değil ama kullanın.

**Örnek:**

```CPP
class Base {
public:
	virtual void func(int);
	virtual void func(int, int);
	virtual void func(double);
};

class Der : public Base {
public:
	virtual void func(int, int);
};
```
> Yukarıdaki 3 fonksiyon function overloading var ve aşağıda sadece bunlardan 1 tanesinin overriding'i var.

- Eğer türemiş sınıfın sanal olmayan bir fonksiyonu taban sınıfın sanal fonksiyonuna çağrı yapıyorsa virtual dispatch mekanizması devreye girecek. Yani foo fonksiyonu hangi türden sınıf nesnesi ile çağırılmışsa onun override'ı çalışacak: 

**Örnek:**

```CPP
class Base {
public:
	void foo()
	{
		func();
	}
	virtual void func()
	{
		std::cout << "Base::func()\n";
	}
};

class Der : public Base {
public:
	void func()
	{
		std::cout << "Der::func()\n";
	}
};

int main()
{
	Der myder;
	myder.foo();
}
```
> Taban sınıfın sanal olmayan fonksiyonlarını türemiş sınıf nesneleri ile çağırıyoruz.  Ama o fonksiyon taban sınıfın taban fonksiyonunu çağırıyor.

### Override olmasaydı yapılabilecek hatalar

```CPP
class Base {
public:
	void func(int);
};

class Der : public Base {
public:
	void func(int);
};
```
> Hata ile taban sınıfın sanal olmayan fonksiyonunu sanalmış gibi algılayıp bir fonksiyon bildiriyor ve override ettiğini sanıyor. Bu override veya overload değil ama sentaks hatası da değil. 

```CPP
class Base {
public:
	virtual void func(unsigned int);
};

class Der : public Base {
public:
	void func(int);
};
```
> Parametreler unsigned int olsaydı override etmiş olacaktı. Ama şuan ikisi de ayrı fonksiyon. 

**Bir başka yapılan hata:**

```CPP
class Base {
public:
	virtual void func(int);
};
```
- Bu taban sınıfından birçok override yapıldığını düşünelim. Eğer func'ın parametreleri değiştirilirse tüm override lar iptal olcak. Ama sentaks hatası olmayacak. Bu da tehlikeli bir durum.

- Türemiş sınıfta override keyword kullandığım zaman derleyici bu fonksiyonun override'ı olup olmadığını kontrol etmek zoruında.
```CPP
class Base {
public:
	virtual void func(int);
};

class Der : public Base {
public:
	void func(int) override;
};
```
> Şuanda bir hata yok. Ama parametreyi değiştyirseydik derleyici sentaks hatası verecekti:

```CPP
class Base {
public:
	virtual void func(unsigned int);
};

class Der : public Base {
public:
	void func(int) override;
};
```
> Böyle bir fonksiyon olmadığından sentaks hatası veriyor.

> Yani override leyword eklememek sentaks hatası değil ama eklenirse böyle sorunların yaşanma ihtimali ortadan kalkıyor.

**Başka bir örnek:**

```CPP
class Base {
public:
	virtual void func(int);
};

class Der : public Base {
public:
	void func(int) override;
};
```
Aşağıdaki func işlevinde virtual kullansam da kullanmasam da o fonksiyon virtual olacak. Func taban sınıfın fonksiyonunu override eden bir fonksiyon olduğu için func'ın kendisi de virtual.

**Örnekler:**   [Car.h dosyası](https://github.com/TalhaAbus/CPP_Notlarim/blob/main/Car.md)

```CPP
#include <iostream>
#include "car.h"


void car_game(Car* p)
{
	p->start();
	p->run();
	p->stop();
}

int main()
{
	for (int i = 0; i < 100; ++i)
	{
		car_game(create_random_car());
		(void)getchar();
	}
}
```

- Bu örnek üzerinden yeni araçları öğrenelim:

- cargame fonksiyonunun parametreisni referans yapalım ve sana fonksiyona çağıroılan fonksiyonları bu referans isimle yapsaydım virtual dispatch mekanizmasında herhangi bir farklılık olmayacak:

```CPP
#include <iostream>
#include "car.h"


void car_game(Car &r)
{
	r.start();
	r.run();
	r.stop();
}

int main()
{
	for (int i = 0; i < 100; ++i)
	{
		car_game(*create_random_car());
		(void)getchar();
	}
}
```
- Referansı kalşdırıdğımda ise object slicing olacak:

```CPP
#include <iostream>
#include "car.h"


void car_game(Car r)
{
	r.start();
	r.run();
	r.stop();
}

int main()
{
	for (int i = 0; i < 100; ++i)
	{
		car_game(*create_random_car());
		(void)getchar();
	}
}
```
> Çıktı:

car has startedÚ
car is running now!
car has just stapped!

**Örnek:**

```CPP
class Base {
public:
	virtual void vfunc()
	{
		std::cout << "Base::vfunc()\n";
	}
};

class Der : public Base {
private:
	void vfunc()override;
};
```
> Sentaks hatası yok.

**Örnek:**

```CPP
class Base {
public:
	virtual void vfunc()
	{
		std::cout << "Base::vfunc()\n";
	}
};

class Der : public Base {
private:
	void vfunc()override
	{
		std::cout << "Der::vfunc()\n";
	}
};

void gf(Base& r)
{
	r.vfunc();
}
int main()
{
	Der myder;
	gf(myder);
}
```
> Sentaks hatası yok. Virtual dispatch mekanizması devreye girer ve türemiş sınıfın vfunc fonksiyonu çağırılır. Neden hata yok?

- Eğer bir verinin türü derleyicinin koda bakmasıyla anlaşılıyorsa, yani türe ilişkin her şey compile time'da belli oluyorsa bu tür diller static tür kavramına sahip diller. 
- Türün ne olduğu çalışma zamanında belli oluyorsa dinamik tür kavramına sahip türler.
> C++, C#, Java static tür kavramına sahip türler. Ama belirli ölçüde dinamik tür kavramına da destek veriyorlar.

```CPP
void car_game(Car& r)
{
	r.start();
	r.run();
	r.stop();
}
```
> Bu fonksiyonunu parametre değişkeni türünün Car olduğunu derleyici koda bakarak anlıyor. Bu türlere static tür denir. Ama r nesnesinin programın çalışma zamanı açıosında türü, bu nesnenin programıun çalışma zamanındaki davranışını belirliyor. Yani r = Bmw ise, Bmw'nin start fonksiyonu çağırılacak.

- Dinamik türden bahsedebilmemiz için o sınıfın polimorfik sınıfo olması gerekir.

**Örnek:**

```CPP
class Base {
public:
	virtual void func(int x = 10)
	{
		std::cout << "Base::vfunc(int x) x =" << x << '\n';
	}
};

class Der : public Base {
public:
	virtual void func(int x = 20)
	{
		std::cout << "Der::vfunc(int x) x = " << x << '\n';
	}

};

void gf(Base& br)
{
	br.func();
}
int main()
{
	Der myder;
	gf(myder);
}
```
> Çıktı == Der::vfunc(int x) x = 10

**Önemli Bir kural:**

```CPP
class Base {
public:
	Base()
	{
		vfunc();
	}
	virtual void vfunc()
	{
		std::cout << "Base::vfunc()\n";
	}
};


class Der : public Base {
public:
	virtual void vfunc()override
	{
		std::cout << "Der::vfunc()\n";
	}
};

int main()
{
	Der myder;
}
```
> Türemiş sınıf nesnesi içinde bir taban sınıf nesnesi var. Dolayısıyla bir türemiş sınıf nesnesini construct ederken önce onun taban sınıf nesnesi construct olur. Taban sınıfın constructorının parametresi Base*. O zaman burada da sanallık mekanizmasının devreye girmesi gerekir.

> Normalde girmesi gerekir. 

- Eğer taban sınıfın consturctor2ı içinde bir sanal fonksiyona çağrı yaparsanız virtual dispatch mekanizmasına bağlanmaz. Her zaman çağırılan taban sınıfn kendi fonksiyonudur. Constructor için virtual dispatch mekanizması devreye girmiyor. Eğer girseydi felaket olurdu. 

### Clone idiomu 

- Bir fonksiyonun sanal olması için non static ye fonksiyonu olması gerekiyor. Ama sınfıların constructorları sanal olamaz. Ama bazı programlama dillerinde constructor virtual olabiliyor. 

- Taban sınınfa bir fonksiyon yazıyorum.

```CPP
class Car {
public:
	virtual void start() = 0;
	virtual void run() = 0;
	virtual void stop() = 0;
	virtual Car* clone() = 0;
};
```
> Burada clone fonksiyonu virtual olduğuna göre Car sınıfından kalıtım yoluyla elde edilen sınıflar clone fonksiyonunu override edeblirler.

```CPP
class Fiat : public Car {
public:
	void start() {
		std::cout << "Fiat has startedé\n";
	}
	void run() {
		std::cout << "Fiat is running now!\n";
	}
	void stop() {
		std::cout << "Fiat has jsut stapped!\n";
	}
	Fiat* clone()override
	{
		return new Fiat(*this);
	}
};
```
> Clone diğer nesnenin tıpatıp aynısı. Bu yüzden copy constructor'ı çağırmalıyım. Bunun için new ifadesi ile oluşturduğum nesnenin ctor'ına *this* argüman olarak gödnermeliyim. 

```CPP
return new Fiat;
```
> Böyle yazsaydı msentaks hatası olmazdı ama default constructt etmiş olurdum. Yani bizimki diğer nesnenin aynısı değil. 

```CPP
void car_game(Car* p)
{
	Car* carptr = p->clone();
	p->start();
	carptr->start();
}

int main()
{
	for (;;)
	{
		car_game(create_random_car());
		(void)getchar();
	}	
}
```
Bmw has startedÚ
Bmw has startedÚ

> İkisi de aynı. Runtime'da belli olan polimorfik bir nesnenin kopyasını oluşturmamız gerekirse bunu doğrudan yapacak bir araç yok ,clone idiomu kullanıyoruz.

### Virtual Destructor

```CPP
void car_game(Car* p)
{
	Car* carptr = p->clone();
	p->start();
	carptr->start();
}

int main()
{
	for (;;)
	{
		car_game(create_random_car());
		(void)getchar();
	}	
}
```
> Birçok durumda polimorfik nesneleri bu örnekteki gibi taban sınıf pointerı ile yönetiyoruz ve bunlar büyük çoğunlukla dinamik ömürlü nesneler. Burada clone fonksiyonu new ifadesi ile nesneyi oluturdu.

> İşim bittiğinde carptr nesnesini delete etsem: Derleyici delete ifadesindeki pointer'ın ilişkin olduğu türe bakıyor ve bu adresi this pointer olarak kullanıp sınıfın destructor ına çağrı yapıyor. Yani şimdi kar sınıfının destructor'ı çağırılacak.

```CPP
void car_game(Car* p)
{
	Car* carptr = p->clone();
	p->start();
	carptr->start();
	delete carptr;
}

int main()
{
	for (;;)
	{
		car_game(create_random_car());
		(void)getchar();
	}	
}
```
> Fakat eğer buraya gelen bir Bmw ise bmw nin destructor'ının çağırılması gerekir. Eğer bmw yerine car sınıfının destructor ını çağırırsak bu tanımsız davaranış. Aynı zamanda resource leak'e neden olacak.

**Örnek:**
```CPP
class Base {
public:
	~Base()
	{
		std::cout << "Base destructor\n";
	}
};

class Der : public Base {
public:
	~Der()
	{
		std::cout << "Der destructor\n";
	}
};

int main()
{
	Base* baseptr = new Der;
	delete baseptr;
}
```
Der destructor
Base destructor

> Base destructor çağırılmasını sağlayan Der destructor.

- Polimorfik sınıfların destrcutorları ya **public virtual** olacak ya da **protected non-virtual** olacak.

```CPP
class Base {
public:
	~Base()
	{
		std::cout << "Base destructor\n";
	}
	// virtual void foo() = 0;   // base'in polimorfik olduğunu düşünelim.
};

class Der : public Base {
public:
	~Der()
	{
		std::cout << "Der destructor\n";
	}
};

int main()
{
	Base* baseptr = new Der;
	delete baseptr;
}
```
> Base türündene bir poniter a dinamik ömürlü türemiş sınıf nesnesi adresi koyarsanız ve base pointer ile onu delet eederseniz tanımsız davranıştır.

```CPP
class Base {
public:
protected:
	~Base()
	{
		std::cout << "Base destructor\n";
	}
};

class Der : public Base {
public:
	~Der()
	{
		std::cout << "Der destructor\n";
	}
};

int main()
{
	Base* baseptr = new Der;
	delete baseptr;
}
```
> Protected yaptığımızda artık delete operatorünü taban sınıf pointerı ile kullnaığımızda sentaks hatası verecek. Çünkü delete operatörünün operandı taban sınıf türünden pointer, bu durumda taban sınıfın protected destrcutor'ını çağırıyoruz ve access control'e takılıyor. 

- ama türemiş sınıf pointerı ile bunu yaparsam:

```CPP
class Base {
public:
protected:
	~Base()
	{
		std::cout << "Base destructor\n";
	}
};

class Der : public Base {
public:
	~Der()
	{
		std::cout << "Der destructor\n";
	}
};

int main()
{
	Der* derptr = new Der;
	delete derptr;
}
```
> Sentaks hatası ollmayacak. Çünkü derptr'nin türü der*. Der'in destrcutor'ı public ama der'in destructor'ının base destructor ını çağırması bir sentaks hatası değil çünkü protected. Çünkü türemiş sınıflar taban sınıfın protected ögelerini kullanabiliyorlar.  

**Özet:** Polimorfik sınıfların destructor'ı ya virtual ve public olacak ya da non-virtual ve protected olacak.

- Global bir fonksiyon doğrudan virtual olamıyor. Taban sınıf parametreli bir global fonmksiyon yazıp, bu global fonksiyonun taban sınıf türünden pointer veya referans parametreye sahip olmasını sağlayıp, fonksiyonun içinde de bu nesne için bu sanal fonksiyona çağrı yaparsak bu durumda virtual dispatch global fonk. için devreye girmeyecek ama çağırılan sanal fonksiyon içn devreye girecek.

# Ders 23

**Sorular:**  Virtual dispatch olmadan bir çözüm oluştursaydım, programım daha hızlı çalışabilir miydi, daha verimli olabilir miydi?
Eğer ortada ciddi bir verim sorunu varsa, kullanılan bellek alanı azalır mıydı? Eğer ortada bir bellek alanı problemi varsa, değerli içler virtual dispatch mekanizmasını nasıl implemente ediyorlar?

- Bir tane taban sınıfımız olsun. Taban sınıfımıza iki tane intürden eleman koyalım, data member koyalım. Ve bu sınıfın size of değerini, storage ihtiyacını yazdıralım.

```CPP
using namespace std;

class Base {
	int x{};
	int y{};
};

int main()
{
	std::cout << "sizeof(Base) = " << sizeof(Base) << '\n';
}
```
- Şimdi buna bir üye fıonksiyonu ekleyelim. Üya fonksiyonların sınıf nestesinin bellek alanı ile doğrudan bir ilgisi yok.  

```CPP
class Base {
	int x{};
	int y{};
	void func();
};

int main()
{
	std::cout << "sizeof(Base) = " << sizeof(Base) << '\n';
}
```
> Kaç tane non- statik data member eklersem ekleyeyim size of değeri yine aynı olacak. Eklediğimiz fonksiyonu sanal fonksiyonu yapalım ve tekrar size of değerine bakalım:

```CPP
class Base {
	int x{};
	int y{};
	virtual void func();
};

int main()
{
	std::cout << "sizeof(Base) = " << sizeof(Base) << '\n';
}
```
> Gördünüz size of değeri arttı, 12 oldu. Yani dört byte arttı. Peki acaba ben birden fazla virtual function eklersem Daha da artacak mı size of değeriyoksa 12 olarak mı kalacak?

- Bir de kalıtım yapalım:

```CPP
class Base {
	int x{};
	int y{};
	virtual void func();
};

class Der : public Base {

};

int main()
{
	std::cout << "sizeof(Base) = " << sizeof(Base) << '\n';
	std::cout << "sizeof(Der) = " << sizeof(Der) << '\n';
}
```
> Yine 12 byte olduğunu görüyorsunuz. Neden 12 byte oldu? Virtual function olmadığı zaman artmadı da neden virtual function eklediğim zaman arttı?

- En az bir tane virtual function olan sınıflara polymorphik class dendiğini söylemiştik. Polymorphik sınıflar için sınıf türünün storage ihtiyacı beklediğimiz değerin 4 byte 1 pointer fazlısı oldu. Bunun nedeni şu:

> Derleyici virtual dispatch mekanizmasını implemente etmek için aslında taban sınıf nesnesinin içine bizim koyduğumuz memberlerin dışında bir de pointer ekliyor. Yani aslında sınıf nesnesinin örneğin 16 bytes'a derleyicinin yaptığı eklemeyle bir pointer daha fazla örneğin pointer size of 4 bytes'a 20 byte olacak.

> Bütün sınıfların poymorfik sınıfların kalıtımda hangi levelde olursa olsun içinde bir pointer var. Her şey bu pointer'a dayanıyor. Bu pointer'a popüler olarak virtual function table pointer deniyor.

> Bu pointer bir veriyapısının adresini tutuyor.  Siz bir sınıf nesnesine hayata getirdiğinizde eğer bu sınıf nesnesi polimolfikse sizin yazdığınız konstraktör, sınıf nesnesinin elemanlarının ilk değerini veriyor. Ama derleyicinin eklediği kodla o derleyicinin eklediği v pointer'da yine derleyicinin oluşturduğu bir veriyapısının adresini tutuyor.

> Bu pointer programın çalışma zamanında ilk değerini alıyor, programın çalışma zamanında oluşturuluyor.

- Derleyici sınıf yer arşisindeki her sınıf için bir veriyapısı oluşturuyor. Bu veriyapısında sanal fonksiyonların adresleri var.

![image](https://user-images.githubusercontent.com/75746171/212567824-9ebe2eb1-0ec5-400d-9c55-c1b2bc2038cd.png)

- Şimdi soru, kaç tane Toyota nesnesi hayatta olursa olsun hepsinin içinde birer vptr var mı? Ama sanal fonksiyon tablosu bir tane o sınıf için. Yani 10 tane Toyota nesnesi hayattaysa 10 unun içinde de bir pointer var ve hepsinin içindeki pointer da aynı veriyapısının adresini tutuyor. 10 tane polymorfik sınıf varsa her bir sınıf için birer sanal fonksiyon tablosu veriyapısı var. Ama dikkat, Aynı indekste aynı sanal fonksiyonunun override'ının adresi var. 
- Yani Toyota'nın tablosunun iki indeksinde Toyota'nın stop override'ının adresi var iken Volvo'nun sanal fonksiyon tablosunun iki indeksinde Volvo'nun stop fonksiyonunun adresi var. Derliyeci nasıl bu veriyapısını oluşturur da bunun indekslerine aynı overrideların adreslerini yazar?

> Derliyeci bu adresleri zaten koda bakarak görüyor. İndeksi de koda bakarak statik olarak elde ediyor.

**Virtual Dispatch:**  : Bizim virtual dispatch dediğimiz mekanizma aslında derdeyicinin sınıf nesnesinin içindeki sanal fonksiyon tablo göstericisine eriştiren ve oradaki belirli bir indeks'teki fonksiyon adresine  erişimi sağlayan ve o adresdeki fonksiyonu çağıran bir kod.

**Yukarıdaki resimde**: 
- Diyelim ki fiattan elde edilen fiat 124, fiyat sınıfının start fonksiyonunu override etmemiş. Bu durumda yine fiat 124 sanal fonksiyon tablosunda startın adresi olmalı değil mi? Ama o adres Fiat 124'ün override'ının değil de fiatın override'ının adresi olacak. 

- Şimdi gerçekçi bir şekilde maliyeti düşünelim:

> Bir sanal fonksiyon çağırısı bir dereferensing içermek zorunda. Çünkü o nesnenin taban sınıf nesnesinin içindeki sanal fonksiyon tablosunun adresine erişmesi lazım. Ve bir dereferencing daha. Neden? O tablonun da bir dizi olduğunu düşünün, o dizinin bir elemanına erişmek de bir dereferencing.

- Yani normal fonksiyon çağrısına göre sanal fonksiyon çağrısı, herhangi bir optimizasyon olmazsa iki tane ilave D referensin maliyeti içeriyor. Başka maliyetler neler?

- Nasıl elemanlara ilk değer vermek için işlem kolu üretiliyorsa o pointerların initialize edilmesinin de bir maliyeti var. 

Kısaca maliyetler:

1. sınıf nesnesinin içindeki pointer'ın initialize edilmesi
2. sanal fonksiyon tabloların oluşturulması.
3. sanal fonksiyon çağrısı yapıldığında iki kez D referensin yapılması.


- Her sınıf için bir sanal fonksiyon tablosu olacağına göre her sınıf için bir sanal fonksiyon tablosu bellek alanı gerekiyor. Diyelim ki böyle bir veri yapısı için 100-bytlık bir bellek alanı gerekiyorsa bu 100-bytlık bellek alanı her sınıf için alocate edilmek zorunda. **Ama asıl kritik problem şu:**

- Bu nesneler birçok uygulamadı dinamik ömürlü olmak zorunda. Dinamik ömürlü nesne demek, Dinamik ömürlü nesnenin kendisinin de bellek alanı alocate edilmesi demek. Bu ciddi bir maliyet. Otomatik ömürlü bir nesneye  oluşturma maliyetiyle dinamik ömürlü bir nesneyi oluşturma maliyeti arasında 50 kata yakın maliyet fark olduğunu düşünün.
```CPP
	std::vector<Car*> cvec;
```
> container denilen sınıf nesneleri ya da sınıflar pointer tutabiliyor. Ama referans tutamıyor. Ama referance wrapper  sınıfı ile referansı sarmalayarak vectorun vectorlar ile referans  kullanılabiliyor. Bunu öğreneceğiz. 

**smart pointer'la pointer arasında buradaki kullanım uçasından ne fark var?**

- Normal pointer'la dinamik ömür nesneleri yönettiğinizde dinamik ömür nesnenin dili tedilmesinden onun hayatının sonlandırılmasından siz sorumlusunuz. Ama dinamik ömür nesneyi smart pointer'la kontrol ettiğiniz zaman (örneğin bir unique ptr nesnesi ile kontrol ettiğiniz zaman) onun hayatını kontrol etmek artık sizin sorumluluğunuzda değil. unique ptr nesnesinin hayatı bitince hayatını kontrol ettiği nesneyi de delete edecek.

- Mesela şimdi bu vektör nesnesinin hayatı biterse o vektörün tuttuğu pointerlar delete edilmeyecek:

```CPP
	vector<Car*> cvec;
```
> Ama vektör eğer Car* değil de unique ptr'e tutsaydı vektör nesnesinin hayatı bittiğinde vektör nesnesi destruct olduğunda vektörün tuttuğu sınıf nesnelerinin destructorleri çağrılacaktı. Vektörün tuttuğu sınıf nesneleri de unique_ptr olduğu için unique_ptr'nin destructor'u çağrılacaktı. Unique_ptr'nin destructor'u de  hayatını kontrol ettiği nesneyi delete edecekti.

```CPP
#include <iostream>
#include "car.h"
#include <vector>

using namespace std;

for (int i = 0; i < 1000; ++i)
{
	cvec.push_back(create_random_car());
}
for (auto p : cvec) {
	cout << *p << '\n';
	p->start();
	p->run();
	p->stop();
	(void)getchar();
}
```
> Benim vector ile işim bittiğinde bu kod ççok kötü durumda. Çünkü bu dinamik ömürlü nesnelerin hiçbiri delete edilmeyecek, resource leak oluşacak.

## Memory leak ve resource leak kavramları:

- **Memory leak:** bir allocator'ın bellek alanı elde etmesi fakat o bellek alanı kullanımına ihtiyaç kalmamasına karşın o alanın geri verilmemesi. Geri veremediği sürece o bellek artık başka kodlar tarafından kullanılma potansiyelinde olmayacak. Biz orayı bloke etmiş olacağız.

- **Resource Leak:** Sadece bir bellek alanı olmak zorunda değil.  Örneğin bir veri tabanı bağlantısı, bir dosya, bir kilit sistemi, bunların hepsi birer resource olabilir. Constructor tarafından edinilen kaynaklar, destructor tarafından geri veriliyor. 
- Dolayısıyla bir sınıf nesnesini hayata getirdiğimizde konstraktörü çağrılıyor, tipik olarak kaynaklar ediniliyor. Ama o sınıf nesnesinin destraktörünün çağrılmasını engelleyen bir durum söz konusuysa destraktör çağrılmadığı için sınıf nesnesi için ayrılan kaynak geri verilmeyecek.

**Örnek:**  Destraktörün bir dosyayı kapatması gereksin. Destraktör çağrılmazsa dosya kapatılmayacak . Destraktörün bir Muteks unlock etmesi gereksin destraktör çağrılmazsa edilmeyecek. Destraktörün server bağlantısını kapatması gereksin, destraktör çağrılmazsa server bağlantısı kapatılmayacak. **İşte bu resource leak**

## Final Keyword 

- Contextual keyword kavramanın modern C++'la dileğe eklendiğini ve C++11 standardlarıyla başlangıçta iki tane contextual keyword eklendiğini söylemiştik. Bunlar final ve overwrite sözlüklerimiz. Biz override'ı gördük.

- İki tane ayrı kavram var, programlama dilinden bağımsız.  Biri bir sınıfın Final olması, Final Class. Diğeri overwrite edilmiş bir sanal fonksiyonun Final olması.

**Final Class:**: öyle bir sınıf ki artık tasarım açısından, bu sınıftan yeni bir sınıfın kalıtım yoluyla elde edilmesi istenmiyor.

**Final Overrider:** Öyle bir sanal fonksiyon ki override edilmiş ama o override'a sahip sınıftan yeni bir sınıf kalıtımla elde edildiğinde onların override edilmesi istemiyor, yasaklanmış. Yani diyor ki ben bu fonksiyonu override ettim ama benden kalıtım yoluyla elde edecek sınıflar benim implementasyonumu kullanacaklar.

**Örnek:**
```CPP
using namespace std;

class Base {
public:
};


class Der final : public Base {

};

class Nec : public Der {

};
```
> Hata mesajı: a 'final' class type cannot be used as a base class

```CPP
class Base {
public:
	virtual void func();
};


class Der : public Base {
public:
	virtual void func()final override;
};

class Nec : public Der {
public:
	virtual void func()override;
};
```
> cannot override 'final' function
- Final'ın bir başka faydası da,  Derliyci bazı durumlarda sana virtual dispatch uygulaması gereken yerde hangi fonksiyonun çağrıldığını koda bakarak anlayabiliyorsa virtual dispatch kodu üretmek yerine doğrudan o fonksiyonu çağıracak kod üretiyor.

## Private - Protected Inheritance

- Normalde nesne yönelimini programlamada kalıtım; "is a relationship" dediğimiz ilişki biçimini
temsil ediyor, onu implement etmek için kullanıyor. (Her mercedes bir arabadır, her üçgen bir şekildir, her müdür bir çalışandır.) Fakat C++'da kalıtım, sadece "is a relationship, is a" ilişkisini
göstermeye yönelik, temsil etmeye yönelik, implement etmeye yönelik bir araç değil. C++'da kalıtım daha geniş bir araç seti.

**C++'da kalıtıma bakarsak:** kalıtım üç ayrı kategoriye ayrılıyor:
1. public inheritance,
2. private inheritance 
3. protected inheritance.

- Bunlardan sadece public inheritance, C++'daki javadaki kalıtımın karşılığı,
private ve protected inheritance daha az kullanılan daha özel araçlar. Şimdi bunları incelemeye başlayacağız.

### Private Inheritance 

- Public inheritance'ta, sizin taban sınıfınızın public fonksiyonları sizin public bölümünüze ekleniyordu. Taban sınıfınızın protected fonksiyonları, protected bölümünüze ekleniyor.

- Private kalıtımında artık haban sınıfın public bölümü türemiş sınıfın public bölümüne eklenmiyor. Bu ne demek?

```CPP
class Base {
private:
	void pri();
protected:
	void pro();
public:
	void pub();
};

class Der : private Base {
public:

};

int main()
{
	Der myder;
	myder.pub();
}
```
> Public kalıtım olsaydı kod geçerliydi ama şimdi erişim kontrolüne takılacak. Her Der bir Base dir diyemeyiz.

```CPP
class Base {
private:
	void pri();
protected:
	void pro();
public:
	void pub();
};

class Der : private Base {
public:

};

class Nec : public Der {
	void foo()
	{
		pro();
	}
};
```
> Der sınıfı base sınıfının protected bölümünü kendi protected bölümüne değil yine kendi private bölümüne eklemiş oldu. Geçersiz


**Örnek:**
```CPP
class A {
public:
	void foo();
};

class B {
public:
	void func()
	{
		ma.foo();
	}
private:
	A ma;
};
```
> Eğer B, A'nın elemanlarını kullansın istiyorsam böyle yapabilirim. B sınıfı, A sınıfı türünden bir eleman sahibi olabilir. Burada hiçbir şekilde her B bir A değildir. Üye fonksiyonları içinde de bu elemanı kullanabilir. Peki aynı durum acaba private kalıtımıyla yapılabilir mi:

```CPP
class A {
public:
	void foo();
};

class B : private A{
public:
	void func()
	{
		foo();
	}

};
```
> Burada her B bir A'dır. diyebiliriz (Her zaman olmasa da) 

### Protected Inheritance
```CPP
class Base {
protected:
	void foo();
};

class Der : private Base {
	void bar()
	{
		foo();
	}
};

class SDer : public Der {
	void baz()
	{
		foo();
	}
};
```

> SDer sınıfı taban sınıfın protected bölümündeki fonksiyonu çağıramaz çünkü private inheritance'ta taban sınıfın protected fonksiyonu türemiş sınıfıhn protected bölümüne eklenmiyor, private bölümüne ekleniyor.

## Multiple Inheritance

- Multiple inheritance ile Multi-level inheritance'ı birbirinden ayıralım. Multi-level inheritance dendiğinde kast edilen Bir sınıftan başka bir sınıfı kalıtım yoluyla elde ediyoruz

- Ama kalıtım yoluyla elde ettiğimiz sınıftan da başka sınıfları kalıtım yoluyla elde ediyoruz, Burada multi-level inheritance söz konusu. Multi-level inheritance, bir sınıfı doğrudan tek bir kalıtım ile birden fazla taban sınıftan oluşturmak. Yani kalıtımda birden fazla taban sınıfımızın olması.

![image](https://user-images.githubusercontent.com/75746171/212627354-b4c2e138-26cd-42fa-8a0f-cce63bbe423a.png)

> Her der nesnesi aynı zamanda bir BaseX, Her der nesnesi aynı zamanda bir BaseY olarak kullanılabilecek.

```CPP
class A {

};
class B {

};

class C : public A, public B {

};
```

- Var olan bir sınıfa belirli özellikler eklemek için oluşturduğumuz sınıflara programlamada mixing-class'da deniyor. Mixing-class oluşturmanın bir takım teknikleri var Bunlardan bir tanesi de multiple inheritance.

- Şimdi çoklu kalıtımda en önemli noktalardan biri isim çakışması.

```CPP
class A {
public:
	void foo(int);
};
class B {
	void foo(double);
};

class C : public A, public B {

};
int main()
{
	C cx;

	cx.foo(12);
}
```
> Sentaks hatası, Ambiguity var. İsim arama önceliği yok. Hepsinde birden aranıyor.  Derleyici sentaks hatasını foo'nun ne olduğunu daha kararını vermeden veriyor. Çünkü her ikisinde birden arıyor.

```CPP
class A {
public:
	int foo{};
};
class B {
	void foo(double);
};

class C : public A, public B {

};
int main()
{
	C cx;

	cx.foo(12);
}
```
> Yine sentaks hatası. Çünkü problem hangi fonksiyonun çağrılıldığı vesaire değil, varlığın ismin hangi varlığa ilişkin olduğu anlaşılamıyor. Taban sınıfın ismiyle nitenemeden ambigüiti olacak. Niteleyerek kullandığım zaman hiçbir problem yok.

```CPP
class A {
public:
	int foo(int);
};
class B {
public:
	void foo(double);
};

class C : public A, public B {
	void func()
	{
		A::foo(12);
		B::foo(1.2);
	}
};
```
> Hatasız. Peki  A'daki foo yu çağırmanın başka yolu olabilir mi?

```CPP
class A {
public:
	int foo(int);
};
class B {
public:
	void foo(double);
};

class C : public A, public B {
	void func()
	{
		((B*)this)->foo(2.3);
		((A*)this)->foo(3.4);
	}
};
```
> Hatasız.

```CPP
class A {
public:
	int foo(int);
};
class B {
public:
	void foo(double);
};

class C : public A, public B {
public:
	using A::foo;
	using B::foo;
};
int main()
{
	C cx;
	cx.foo(12);
}

```
> function overloading

```CPP
class A {
public:
	A()
	{
		std::cout << "A constructor\n";
	}
};
class B {
public:
	B()
	{
		std::cout << "B constructor\n";
	}
};
class C : public A, public B {
public:

};
int main()
{
	C cx;
}
```
> Bildirildiği sıra ile hataya geliyor. Burada önce A hayata gelecek.

### Diamond formation (DDD) (Dreadful Diamond of Derivation)

- Şöyle bir durum olduğunu düşünün:  Taban sınıftan public kalıtımıyla elde edilen iki tane ayrı sınıf var.

![image](https://user-images.githubusercontent.com/75746171/212632709-7f04ce81-564a-4c0c-91e1-7ea496de3b8b.png)

- Bunların içinde de birer base var. Bu durumda Emder sınıfı türünden nesnenin içinde iki tane ayrı base nesnesi olacak. Biri Mder'in içindeki Der1 içindeki Base diğeri Mder'in içindeki Der2 nesnesinin içindeki base.

- Mder içinde Base'den gelen bir nesne kullandığımda, niteleme yapmadığımda derleyici ambiguity hatası verecek.

```CPP
class Base {
public:
	void foo();
};

class Der1 : public Base {

};

class Der2 : public Base {

};

class MDer : public Der1, public Der2 {

};

int main()
{
	MDer md;

	md.foo();
}
```
> Sentaks hatası. Derleyici Der1 içindeki Base mi yoksa Der2 içindeki base'in adresi mi gelecek bilemez. Ambiguity.

```CPP
int main()
{
	MDer md;

	md.Der1::foo();
	md.Der2::foo();
}
```
> Böyle yazılabilirdi.

**Virtual Inheritance:**

- Çoklu kalıtım yapacağım. Ama çoklu kalıtımda ortak bir taban sınıf varsa, çoklu kalıtımla elde edilecek sınıf türünden nesnelerin içinde o taban sınıfların ortak taban sınıfı türünden bir tane nesne olmasını istiyorsam virtual inheritance denilen aracı kullanmalıyım.

![image](https://user-images.githubusercontent.com/75746171/212640019-214e4776-d38b-4e50-b626-0fb3acc12541.png)

- Standart kütüphanede mirtual inheritance ve multiple iheritance örnekleri. Bizim cout değişkenimiz basic_ostream türünden. Cin nesnemiz basic_istream türünden. (cin cout global)
- Şimdi eğer buradaki kalıtım virtual olmasaydı yukarıdaki taban sınıflardan ikişer tane olacaktı. Oysa bu taban sınıf içindeki operasyonlar okuma ve yazmadan bağımsız her ikisi içinde kullanılıyor.
- Yani çoklu kalıtımla elde edilmiş sınıf nesneleri içinde sadece bir tane basic_ios var.

# Ders 24

## Exception Handling

- Program çalışırken, bir takım hatalar olabilir. Bunun programı çalışırken işini yapamamasının iki farklı nedeni olabilir. 

1. Kodun yanlış olması.
2. Programın çalışma zamanında beklenmeyen bazı durumlarının oluşması nedeniyle programın işini yapamaması

- Eğer amaçımız, programın çalışamaması, işini yapamamasının nedeni olan kodlama hatalarını bulmaksa, onlar için kullandığımız araçlar farklı.  Ama kodda bir hata olmamasına karşın, programın çalışma zamanında başka nedenlerden program işini yapamıyorsa, onlarla mücadele etmek için kullandığımız araçlar farklı.

- Kendi hatalarımızı bulmaya yönelik kodlara programlamada popular olarak assertion kodları deniyor.

1. static assertion 
2. Dynamic assertion

Örnek: Benim progrmaının çalışması için int türünün 2 byte tan daha büyük olması gereksin. Bunu derleme zamanında derleyicinin kontrolüne bırakabiliriz ve derleyici sizeof int 2 byte olduğunu gördüğünde bana bir hata mesajı verebilir. Bu static assertion.

- C' de statik assertion önemli ama C++'ta olduğu kadar değil. Çünkü bizim önümüzdeki günlerde tanışacağımız generic programlama paradigması var.

**Dynamic assertion:**  Program çalışma zamanında yapılan doğrulamalar. 

**Exception Handling:**  Dilin içine gömülü, programın çalışma zamanına yönelik hatalarla başa çıkmaya yönelik dilin sağladığı araç seti. Bir fonksiyonun işini programın çalışma zamanında oluşan koşullar nedeniyle gerçekleştirememesi.

- **C gibi bir dilde programın çalışma zamanına yönelik hataları yönetme, kontrol etme:** fonksiyonlar kendisini çağıran koda işlerini yapamadıkları zaman bir şekilde işlerini yapamadıklarını belli eden bir bilgi iletiyorlar. Bu geleneksel hata işleme yöntemleri. Exception handling araçlarının avantajlarını anlayabilmek için önce geleneksel hata işleme yöntemlerinin dezavantajlarını konuşmamız gerekiyor. Geleneksel hata işleme yöntemleri derken ne kastediriyor?

**Bir yöntem:** Fonksiyonun geri dönüş değeriyle işini yapamayacağı bilgisini çağıran koda iletmek. En çok kullanılan yöntem: fonksiyonun geri dönüş değeri mekanizmasıyla işini yapamadığı durumunu çağıran koda iletmesi.

- Aslında gelenenksel yöntemlerin ortak noktası, çağıran koda bir değer iletilmesi. C++ dilinde bu bazı durumlarda mümküno lmayabilir (Constructor'ın geri dönüş değeri yok)


> f1 => f2 => f3 => F4 => F5 .....  iç içer fonksiyonlarda hata olduğu bilgisinin geri döndürülme aşamaları buna benzer.
- **Burada verimli olan yöntem:** 
> Programın akışı, programın çalışma zamanında hatayı tespit eden, işini yapamayacağını anlayan koddan o hataya müdahale etme isteği yetkisi olan koda aktarılması.  Yani aradaki fonksiyonlar adeta devre dışı kalacak. Bir hata oluşması durumunda programın akışını hatayı tespit eden koddan doğrudan hatayı işleyen koda çekebileceğiz.

- Bu durum C'de yapılamaz değil, ama hazır bir araç yok. 

- Edxception handling ile ilgili 3 tane anahtar sözcüğümüz var:

1. thwrow: throw statement oluşturulmasına kullanılıyor
2. try
3. catch

- Beni hangi fonksiyonlar çağırmışsa, (beni çağıran, beni çağıranı çağıran) ben işimi yapamıyorum. İşimi yapamadığıma ilişkin bir bilgiyi oluşturdum size gönderiyorum. Kim ki bu hataya müdahale etmek isterse bunu yakalasın ve o hataya müdahale etsin.

```CPP
try{
	foo();
}
```
**Try:**  Bir block olmak zorunda. **Bu bloğun anlamı:** Sevgili derliyeci, sevgili okuyucu, bu block içinde çalışan kodlardan herhangi biri bir hata nesnesi gönderdiğinde ben o hatayı yakalayıp ona müdahale etmeye adayım demiş oluyorsunuz.

**Catch:** Catch blockları hatayı işleyecek, ona müdahale edecek kodu içeren blocklar. (exception'ı handle edecek kod)

```CPP
catch (int x) {

}
```
> eğer try block'unun içinde çalışan kodlardan gönderilen hata nesnesinin türü int ise programın akışı bu catch block'una çekilecek yani catch parametresi olan tür aslında bizim müdahale etmek istediğimiz hatayı temsil eden tür.

- Her tyr bloğundan sonra bir catch bloğu olmak zorunda. 

```CPP
int x = 10;

throw x;
```
> throw statement'daki throw expression kendisi bir l value expression olsa da yukarıya gönderilen nesne bu nesnenin kendisi değil. Derliyici trove expression'dan faydalanarak kendisi bir nesne hayata getiriyor. Yani aslında yukarıya gönderilen nesne derliyicinin oluşturduğu nesne. Throw ifadesinde yer alan nesne değil.

```CPP
void foo()
{
	int x = 13;
	throw x;
}
```
> eğer gönderilen nesne x'in kendisi olsaydı bu nesnenin hayatı bittiğinde hatayı yakalayacak kod, hayatı bitmiş bir nesneyi kullanma girişimin de bulunacaktı. Bu bir tanımsız davranış. 

```CPP
void foo()
{
	throw ???
}

```
> İşinizi yapamamanızın nedeninin ne olduğunu tipik olarak yukarıdaki koda iletmek istiyorsunuz. Çoğu durumda işinizi yapamamanızın nedeninin ne olduğunu yukarıya bildiriyorsunuz ki yukarıdaki kodlar bu nedenlerin neler olduğuna bağlı olarak hataayı yakalayıp müdahale etmek istiyor. Mesela bir kod **bellek yetersizliği** hatasına müdahale etmek isterken bir başka kod **matematiksel bir hata** söz konusuysa ona müdahale etmek isteyebilir. İşte burada hatayla ilgili bilgi vermenin iki tane önemli aracı var.

1. Doğrudan true ifadesinin türü:

- Mesela **"date exception"** isimli bir sınıf tarih işlemleriyle ilgili oluşan bir hatayı temsil etmek için tanımlanmışsa sizin true ifadenizin date exception sınıfı türünden olması, **ben tarih işlemleriyle ilgili bir hata olduğu için işimi yapamadım** bilgisini iletiyor. İşinizi yapamamanızın nedeni bambaşka bir hata ise o zaman ona yönelik bir tür kullanıyorsunuz. Türün kendisi hatanın genel niteliğini belirtiyor ve kalıtımdan faydalanarak bunu hiyerarşik bir şekilde yapılandırabiliyorsunuz. 

**Örnek:**

```CPP
NecException

MathError

DivideByZero
```

- NecException sınıfımız var. Bu hata sınıfından yapılan kalıttımlarla elde ettiğim sınıflardan biri **MathError** sınıfı olsa, meterör sınıfından da daha detaylı hata bitimlemeleri için divide by zero error sınıf oluşturursam.

> O zaman diyeceğiz ki her divide by zero error aynı zamanda bir MathError dur. Ama her MathError de aynı zamanda bir
set exception türüdür. 

**throw statement yürütüldüğünde ne oluyor?**

- Programın akışı o fonksiyondan çıkacak hatayı yakalayan koda yönlendirilecek. Ya bu hata yakalanmazsa? Buna uncot exception deniyor. Bir exception gönderilmişse fakat yakalanmamışsa, (yani uncot exception durumu oluşmuşsa) derleyicinin oluşturduğu kod standard kütüphanenin terminate isimli bir fonksiyonunu çağırıyor. Terminate fonksiyonunun default davranışı, yine standard kütüphanenin abort fonksiyonunu çağırmak. Yani yakalanamayan bir hata söz konusu olduğunda abort çağırılır, programın çalışması sonlandırılır. Hata akımına Abortun çağırıldığını gösteren bir yazı da yazılacak. 

- Terminate fonksiyonun dışında bir de ismi set_terminate olan ikinci bir fonksiyon var. Bu terminate'in default davranışını değiştiriyor. Yani siz eğer terminate'in abortu çağırması yerine sizin belirlediğiniz bir fonksiyonu çağırmasını istiyorsanız, set_terminate fonksiyonuna (argüman olarak) çağırılmasını istediğiniz fonksiyonun adresini geçiyorsunuz. 

```CPP
#include <iostream>

#define		st()	(std::cout << __func__ << "starts\n")
#define		end()	(std::cout << __func__ << "ends\n")

void f4()
{
	st();
	end();
}
void f3()
{
	st();
	f4();
	end();
}
void f2()
{
	st();
	f3();
	end();
}
void f1()
{
	st();
	f2();
	end();
}

int main()
{
	f1();
	end();
}
```
> Çıktılar:

f1starts
f2starts
f3starts
f4starts
f4ends
f3ends
f2ends
f1ends
mainends

```CPP
void f4()
{
	st();
	throw 1;
	end();
}
```
> Eğer böyle yazsaydık runtime'da progrmaın akışı f4'ten çıkacak ve abort fonksiyonu çağırılacak. Ama abortu çağıran aslında kim? Standart kütüphanenin terminate isimli fonksiyonu.

```CPP
using terminate_handler = void(*)(void);
```
- Bu durumda terminate handler. Hangi türün eşismi? Geri dönüş değeri olmayan, parametresi olmayan fonksiyon adresi türünün eş ismi.

```CPP
terminate_handler set_terminate(terminate_handler);
```
> Set terminate diyor ki, bana bir fonksiyonun adresini gönder, ben adresini gönderdiğim fonksiyonu kayıt edeceğim. Böylece terminate fonksiyonu abortu çağırmak yerine senin, adresini gönderdiğin fonksiyonu çağıracak. Geri dönüş değeride bu işlem yapılmadan önce default olarak hangi fonksiyon çağırılıyorsa ya da önce hangi fonksiyonu set edilmişse onun adresi.

**Bu nasıl implemente ediliyor?**
- Global bir değişken var. Terminate_handler. Abortun adresiyle ilk değer verilmiş.

```CPP
terminate_handler gfp = &abort;

void terminate()
{
	gfp();
}
```
- Siz terminate'i çağırdığınızda terminate'in abortu çağırmasının nedeni terminate'in fonksiyon çağırısında kullandığı fonksiyon pointer'ının değerinin abortun adresi olması. 

**Set terminate ne yapıyor?**
```CPP
terminate_handler set_terminate(terminate_handler f)
{
	auto ftemp = gfp;
	gfp = f;
	return ftemp;
}
```

> Set terminate parametresine gelen adresi, bu global fonksiyon göstericisini set etmek için kullanıyor. Global fonksiyon göstericisinin değerini bir pointer'da saklıyor. Global fonksiyon göstericisinin değerini set ediyor ve eski değeri get ediyor.

- Exception yakalanmadığı zaman çağırılan fonksiyon olan terminate'in abortu çağırması yerine sizin istediğiniz bir fonksiyonu çağırmasını istiyorsanız o zaman set terminate fonksiyonuna çağrı yaparak fonksiyonunuzu kayda alacaksınız. İşte böylece set terminate aslında terminate'in çağıracağı fonksiyonu sizin kayıt ettiğiniz fonksiyon yapacak. Böylece terminate çağırdığınızı da sizin istediğiniz fonksiyonu çağıracak.

**Örnek:**

```CPP
void myabort()
{
	std::cout << "myabort function called!!!\n";
	std::exit(EXIT_FAILURE);
}

int main()
{
	set_terminate(myabort);
	// Bu noktadan sonra terminate çağırılırsa abort'u çağırmak yerine, 
	// benim fonksiyonum olan my abort'u çağıracak.
	st();
	f1();
	end();
}
```

- Bizim birinci amacımız uygulamada herhangi bir şekilde bir exception gönderildiğinde o exception'a müdahale etmek.

**exception safety:** Ne şekilde exception gönderilirse gönderirsin bu exception yakalanıyor.

- Birçok durumda exception'ın yakalanması resumtif olarak kullanıyor. Yani resume etmek için. Yani siz exception'ı yakalıyorsunuz, gerekenleri yapıyorsunuz ve programın çalışması devam ediyor. Üstelik kalıcı bir zarar olmadan, bir kaynak sızıntısı olmadan devam ediyor. Tamamen durumun ne olduğuna bağlı olarak, stratejinin ne olduğuna bağlı olarak exception yakalandığında bir takım önlemler alınıp program sonlandırılabilir ya da çoğu zaman olduğu gibi resumtif bir mekanizma söz konustur. Exception yakalanır, handle edilir. Ama herhangi bir kayıp olmadan, hiçbir kaynak sızıntısı olmadan işini görmeye devam eder.

- Öyle programlar var ki, programın sonlandırılıp tekrar başlatılması ya kabul edilebilir bir durum değil ya da bu durumda ciddi kayıplar oluşuyor. Mesela bir borsayı yönlendiren programın çalışırken sonlandığını düşünün. Tekrar başlatılacak ama o süre içinde işlemler yapılamayacak.  O işlemlerin yapılamaması milyonlarca hatta duruma göre milyarlarca dolar zarar verebilir.
 
- Ya da öyle yerler var ki exception handling araçları kullanılmıyor. Çünkü onların kullanılması durumundaki
işlemlerin zaman almasından dolayı kabul edilebilir bir yapı değil. Mesela gerçek zamanlı programlama sistemlerinde bir çok durumda exception handling kullanılması tamamen devredişi bırakılıyor, yasaklanıyor. 

**Bir exception yakalamak için nasıl try bloğu oluşturuyoruz:**

- Bir exception'ı yakalamak için öncelikle bir try bloğu oluşturmak zorundayız. Oluşturduğumuz try bloğu bildiğimiz bir blok. Örneğin bir try bloğu içinde bir değişken tanımlarsanız bu değişken yine blok scope kurallarına uyuyor.

- Exception'ın yakalanması ve programın akışının try balloonu izleyen catch bloklarından birine çekilebilmesi için gönderilen exception'ın türüyle catch balloonun parametresinin türünün tamamen aynı olması gerekiyor. Yani burada tür dönüştürme kuralları geçer de değil.

- İstisnaî bazı dönüşümler var. Onun dışında hiçbir örtürü dönüşüm yok. Türemiş sınıftan,
taban sınıfa doğru yapılan dönüşüm. Yani ben türemiş sınıf türünden bir exception gönderirsemi is a relationship ile public kalıtımında her türemiş sınıf nesnesi aynı zamanda taban sınıf türünden kabul edildiği için onu taban sınıf türünden bir catch parametresine sahip catch bloğuyla yakalayabilirim.

**Özet:** gönderilen bir hata nesnesini yakalamak için ya aynı türden bir catch parametresine ihtiyacımız var ya da tür dönüşümü yapılmıyor.  Örneğin int türden bir hata nesnesi gönderilirse parametresi double olan bir catch bloğu parametresiyle yakalayamıyoruz. Ama publik kalıtımında türemiz sınıf türünden gönderdiğimiz bir hata nesnesini onun taban sınıflarından biri türünden referans parametreye sahip bir catch bloğu ile yakalamamız mümkün.

**Notlar:** Eğer çok özel bir durum yoksa hemen her zaman catch parametrelerini referans türü yapıyoruz. Bunun iki tane nedeni var. 1. Eğer referans türü yapmazsak object slicing devreye girer. Virtual dispatch mekanizması
çalışmaz. 2. amacınız virtual dispatch uygulamak olmasa da bu durumda catch parametresi için de copy constructor çağrılacak ve bu durumda copy construct'rın kendisinin de tekrar bir exception gönderme, ihtimali söz konusu olacak.

- O yüzden programın akışının catch bloğuna çekilmesinde catch parametresi için copy construct'rın çağrılması yerine  referans semantiği kullandığımızda çağrılan bir copy construct'r olmayacak. Öyle bir risk almamış olacağız. Bir diğer yandan runtime polymorphizminden faydalanmış olacağız.

```CPP
int main()
{
	set_terminate(myabort);

	try {
		f1();
	}
	catch (int) {
		std::cout << "int\n";
	}
	catch (double) {
		std::cout << "double\n";
	}
	catch (char) {
		std::cout << "char\n";
	}
}
```
> Gönderilen hata nesnesi int, double,char türden olmasına bağlı programın akışı yönlendiriliyor. Bunlardan biri dğeilse de exception yakalanmayacak. 

**Bütün hataları yakalamak teorik olarak mümkün mü?**

- Belirli istisnalar dışında mümkün. Ben en kötü ihtimalle main fonksiyonunun tamamını bir try bloğu için alabilirim. Bu durumda main fonksiyonu içinde çalışan kodlardan gönderilen bütün hataları yakalayabilirim. Ama: 
- Global değişkenler statik ömürlü, aynı şekilde sınıfların statik veri elemanları statik ömürlü. Dolayısıyla global bir sınıf nesnesi oluştursanız ve o sınıf nesnesini hayata getirmek için çağrılan constractor exception throw ederse main fonksiyonunun tamamını bir tryblow içine alsanız dahi o exception'ı yakalama şansınız yok.

**Hangi türden olursa olsun bir exception'ı yakalama şansım var mı?**

- Bunun özel bir sentaksı var. Catch anahtar sözcünü yazdıktan sonra catch parametresi içine elipsiz otomu koyarsanız bu bütün gönderilen hata nesnelerini yakalayacak bir catch bloğudur. Böyle catch bloğuna ingilizcede catch all bloğu deniyor.

```CPP
int main()
{
	set_terminate(myabort);

	try {
		f1();
	}
	catch (int) {
		std::cout << "int\n";
	}
	catch (double) {
		std::cout << "double\n";
	}
	catch (char) {
		std::cout << "char\n";
	}
	catch (...) {
		std::cout << "catch all\n";
	}
}
```
**Catch blocklarının oluşturulma sırası önemli mi?**
- Çünkü derleyicinin ürettiği kodda sınama yukarıdan başlayarak aşağı doğru yapılıyor. Catch all bloğunu en üste koysaydım eğer derleyici buna ilişkin bir diagnostic vermeseydi (ki derleyiciler bu durumda tipik olarak diagnostic verirler) gönderilen hata nesnesi int türden olsa da Catch all bloğu yakalardı:  (handler is masked by default handler) Hatası 

**exception'ı yakaladığımızda neler yapabiliriz exception'ı yakalayıp ne hangi biçimlerde müdahale edebiliriz?**
- Eğer sizi ilgilendirmiyorsa doğrudan yapacak bir şeyiniz yoksa bir exception'ı yakalamaya çalışmayın

> Bir takım işlemler yapıp exit fonksiyonlu çağırabilirsiniz ya da belki duruma göre abort fonksiyonluğa çağırabilirsiniz

> Exception'ı yakalarım ve bir takım işlemleri yapabilirim. Exception'ı tekrar yukarı gönderebilirim. (Aynı exception nesnesi) İşte bu işleme  retroll statement deniyor. 

> Exception'ı yakalayıp bir takım işlemler yaparak ya da yapmadan başka bir türden exception göndermek. Buna da popüler olarak exception'ı translate etmek deniyor.


## Stack Unwinding (Yığının geri sarımı)

- Diyelim ki f1'den 19 a kadar birbirini çağırdı.  f19 fonksiyonu exception trove etti. Peki bu exception f1 fonksiyonunda yakalansa bu arada onlarca yüzlerce sınıf nesnesi hayata gelmiş olabilir. Birçok sınıf nesnesi (string sınıfında olduğu gibi vektor sınıfında olduğu gibi) edindiği kaynağı destructorla geri veriyor. En tehlikeli senaryo bir sınıfın constructor yoluyla edindiği kaynağı destraktıra yapılan çağrıyla geri vermesi yerine destructor'ın hiç çağrılmaması, ve kaynağın geri verilmemesi. Buna gene olarak resource leak dendiğini bir hatırlatalım. 
- Bu durumda exception'ı gönderen kodla exception'ı yakalayan kod arasında onların destraktırılarının çağrılması gerekiyor ki bir kaynak sızıntısı olmasın.

**Örnek:**  Tüm fonksiyonlar birbirini çağırdı ama her fonksiyonun stack frame'inde çeşit çeşit sınıf nesneleri oluşturuldu. Programın akışı exception'ı handle eden koda geldi. Bir daha o sınıf nesnelerini kullanma şansım yok, onlar otomatik ömürlü ama onların da destraktırları çağrılmadı. Destructorlarının çağrılmaması demek onların kaynaklarını geri verememesi demek.

- İşte exception handling mekanizmasının bize sunduğu en büyük nimetlerden biri stack unwinding diye isimlendirilen süreçle, exception'ı gönderen kodla exception'ı handle eden kod arasında farklı stack frame'lerde 
oluşturulan hayata getirilmiş nesnelerin destraktırlarının çağrılma garantisi.

- Yani bütün otomatik sınıf nesneleri için destraktırlar çağrılacak ama bu garanti exception'ın yakalanması durumunda var. 

- Exception yakalanmadığı zaman problem problem sadece programın sonlanmaması değil aynı zamanda farklı stack frame'lerde
oluşturulan sınıf nesnelerinin destraktırlarının çağrılmaması. Belki de o destraktırların çağrılmaması
kalıcı zarar da oluşturabilir. 

- Dolayısıyla program bitirilmek istense de sonlandırılmak istense de program çalıştırılmaya devam ettirilmek istense de bizim bir şekilde stack frame'lerde tekrar kapatılan stack frame'lerde oluşan otomatik ömürlü nesnelerin destraktırlarının çağrılmasını sağlamamız gerekiyor işte bu derliyicinin ürettiği kodla otomatik olarak gerçekleştiriliyor.

```CPP
#include <iostream>

class ResourceUser {
public:
	ResourceUser()
	{
		std::cout << ". kaynak edinildi\n";
	}
	~ResourceUser()
	{
		std::cout << ". kaynak geri verildi\n";
	}
};

void f4()
{
	ResourceUser();
}
void f3()
{
	f4();
	ResourceUser();
}
void f2()
{
	f3();
	ResourceUser();
}
void f1()
{
	f2();
	ResourceUser();
}
int main()
{
	f1();
}
```
> Kaynak edinilip veri verildi. Çünkü scope bittiğinde resourceUser için destructor çağırıldı.

- Şimdi burada f4 fonksiyonu içinde bir exception throw edilse: bu exception yakalanamadığı zaman artık programın akışı buradan çıktığı için ve buralara geri dönmeyeceği için bu nesnelerin destraktörları çağırılmayacak:

```CPP
#include <iostream>

class ResourceUser {
public:
	ResourceUser()
	{
		std::cout << ". kaynak edinildi\n";
	}
	~ResourceUser()
	{
		std::cout << ". kaynak geri verildi\n";
	}
};

void f4()
{
	ResourceUser();
	throw 1;
}
void f3()
{
	f4();
	ResourceUser();
}
void f2()
{
	f3();
	ResourceUser();
}
void f1()
{
	f2();
	ResourceUser();
}
int main()
{
	f1();
}
```
> Kaynakları edinilecek ama bu kaynaklar geri verilmeden program sonlandırılmış olacak. Kodü düzenleyelim:

```CPP
#include <iostream>

class ResourceUser {
public:
	ResourceUser()
	{
		std::cout << ". kaynak edinildi\n";
	}
	~ResourceUser()
	{
		std::cout << ". kaynak geri verildi\n";
	}
};

void f4()
{
	ResourceUser();
	throw 1;
}
void f3()
{
	f4();
	ResourceUser();
}
void f2()
{
	f3();
	ResourceUser();
}
void f1()
{
	f2();
	ResourceUser();
}
int main()
{
	try {
		f1();
	}
	catch (int) {
		std::cout << "catch int";
		(void)getchar();
	}
}
```
> Tek tek her bir stack frame'den çıktığımda destraktörün çağırıldığını göreceğim. Yani programın akışı catch bloğuna girdiği zaman o stack frame'deki bütün otomatik ömürlü nesneler destruct edilecek.

**stack unwinding neden önemli ve bunun rayı idiomuyla ilgisi ne?**

```CPP
void f()
{
	FILE* f = fopen("ali.txt", "w");	// kaynak edinildi

	//code   // ya burada çalışan kodlar exception throw ederse?

	fclose(f);   // kaynak geri verildi.
}
```
> normalde bu fonksiyon çağrıldığında kaynak edinilecek dosya açılacak. Belki dosyaya ilgili işlemler gerçekleştiren kodlar var. Ve en sonda artık o dosyayla işin bittiğimde dosyayı kapatıyorum. Görünmeyen şöyle bir risk var: ya burada çalışan kodlar exception throw ederse? O zaman programın akışı fclose çağrısını görmeyecek, bu kod yürütülmeyecek.

- Bunun yerine ne yapıyoruz, 
```CPP
class File {
	//ctor

	//dtor
};

void f()
{
	File f("ali.txt");
}
```
> Bir nesne kullanarak kaynağı doğrudan pointerlara bağlamak yerine böyle bir sınıf olarak sarmaladığınız zaman elde ettiğiniz avantajlardan biri de artık bu nesnenin kaynağını geri vermesi garanti altında. 

# Ders 25

**Konular:**
- rethrow statement
- ctor'dan exception gönderilmesi
- destructor ve exception
- noexcept operatörü
- nmoexcept specifier
- function try block
- exception dispatcher

**bir exception'ı yakaladığımız zaman tipik araçlarımızdan biri o exception'ı tekrar yukarı göndermek.**

- Tipik olarak exception'ı yakalıyoruz. Kısmı müdahale de bulunuyoruz. Yani kendimiz için gerekli işlemleri gerçekleştiriyoruz. Bunlar loglama işlemleri olabilir, kaynak geri verme vesaire olabilir. Ama daha yukarıdaki kodların da müdahalesini mümkün kılmak için biz de aynı exception'ı yukarıya geri gönderiyoruz. 

**Diyelim ki bir fonksiyon var bu fonksiyon bir exception trove ediyor:**

```CPP
void func()
{
	// code
	throw std::out_of_range{ "aou_of_range" };
}

void foo()
{
	try {
		func();
	}
	catch (const std::exception& ex) {
		std::cout << "exception caught:" << ex.what() << '\n';
		//code
	}
}
```
> Bu hatanın kendisini göndermek için arkadaşlar rethrow statement kullanıyoruz. Retro statement şöyle oluşturuluyor: rethrow sözcüğü var ve rethrow sözcüğünden sonra hiçbir ifade yok.

- throw ve throw ex farkı

```CPP
throw ex; 
```
> Burada yazdığımız deyim retro statement değil kesinlikle. Peki fark ne?

> Derleyici exception throw edildiğinde bir exception nesnesi oluşturuyor değil mi? Bu nesne yani derleyicinin oluşturduğu exception nesnesi yukarıya gönderildi. Biz şimdi "const std::exception& ex" Böyle bir referans ile bunu yakalarsak derleyicinin gönderdiği exception nesnesini kullanmış oluyoruz. Ve rethrow ettiğimizde ayno nesneyi gönderiyor.

> Yani şimdi foo'yu çağıran bir fonksiyonda ben buradan rethrow edilen exception'ı yakalarsam yine aynı nesneyi mi yakalayacağım? Evet. Ama böyle yazarsam:

```CPP
throw ex;
```
> Eğer böyle yazarsam bu durumda buradaki (const std::exception& ex) nesnenin hayatı bitecek. O destroy edilecek. Ama o destroy edilmeden önce copy constructor çağrılarak derleyici yeni bir exception nesnesi oluşturacak.

**Özetle:**

```CPP
throw;
```
> Burada ilk buraya gelen exception nesnesinin kendisi kullanılıyor.

```CPP
throw ex;
```
> Fakat burada ise ilk gönderilen exception nesnesinin hayatı bitmeden copy constructor  yoluyla yeni bir exception nesnesi oluşturuluyor. Yani siz exception sınıfının copy constructor'ını çağırmış oluyorsunuz.

**İkinci bir fark ise:**  
```CPP
throw ex;
```
> Böyle bir kopyalama yaptığınız zaman dinamik tür bilgisini kaybetmiş oluyorsunuz. Yani object slicing oluyor. 

**Object slicing olması ne demek:**
```CPP
const std::exception& ex
```
> Mesela ben bunu exception referansla yakaladım ama buraya gelen aslında out of range değil mi? **throw ex** ile out of range'in kopyasını çıkarttım. Out of range'i göstermesine rağmen **throw ex** ile oluşan nesne artık out of range nesnesi değil. Artık onun arkadaşlar türü std exception. foo'dan gönderilen hatayı out of range'de yakalamak istesem yakalayamayacağım. Çünkü artık o dinamik tür bilgisi kaybedildi.

```CPP
#include <iostream>
#include <cstdio>
#include <string>

void func()
{
	// code
	throw std::out_of_range{ "aou_of_range error" };
}

void foo()
{
	try {
		func();
	}
	catch (const std::exception& ex) {
		std::cout << "exception caught:" << ex.what() << '\n';
		std::cout << &ex << '\n';
		//code
		throw;	//rethrow
	}
}

int main()
{
	try {
		foo();
	}
	catch (const std::exception& ex)
	{
		std::cout << "exception caught in main: " << ex.what() << '\n';
		std::cout << &ex << '\n';
	}
}
```
**Çıktı:**

```CPP
exception caught:aou_of_range error
000000D1A04FF888
exception caught in main: aou_of_range error
000000D1A04FF888
```
> İki nesnenin adresi aynı çıktı. Ama şimdi rethrow statement yerine throw ex yazdım:

```CPP
#include <iostream>
#include <cstdio>
#include <string>

void func()
{
	// code
	throw std::out_of_range{ "aou_of_range error" };
}

void foo()
{
	try {
		func();
	}
	catch (const std::exception& ex) {
		std::cout << "exception caught:" << ex.what() << '\n';
		std::cout << &ex << '\n';
		//code
		//throw;	//rethrow
		throw ex;
	}
}

int main()
{
	try {
		foo();
	}
	catch (const std::exception& ex)
	{
		std::cout << "exception caught in main: " << ex.what() << '\n';
		std::cout << &ex << '\n';
	}
}
```
**Çıktı:**
```CPP
exception caught:aou_of_range error
000000A6E74FF5A8
exception caught in main: aou_of_range error
000000A6E74FF6F8
```
> Nesne'nin adresinin farklı olduğunu görüyorsunuz

- Main fonksiyonu içinde bir catch bloğu daha ekledim. Bu catch bloğunun parametresi const out of range. Ve rethrow statement kulanıyorum:

```CPP
#include <iostream>
#include <cstdio>
#include <string>

void func()
{
	// code
	throw std::out_of_range{ "aou_of_range error" };
}

void foo()
{
	try {
		func();
	}
	catch (const std::exception& ex) {
		std::cout << "exception caught:" << ex.what() << '\n';
		std::cout << &ex << '\n';
		//code
		throw;	//rethrow
		//throw ex;
	}
}

int main()
{
	try {
		foo();
	}
	catch (const std::out_of_range) {
		std::cout << "exception caught in main: std::out_of_range " << ex.what() << '\n';
	}
	catch (const std::exception& ex)
	{
		std::cout << "exception caught in main: std::exception& " << ex.what() << '\n';
	}
}
```
**Çıktı:**
```CPP
exception caught:aou_of_range error
00000040844FFA18
exception caught in main: std::out_of_range
```
> Exception foo'da yakalandı. Yakalanan exception Out of range türünden. Exception rethrow  edildi. Main'de yakaladığında out of range yakaladı. Demek ki dinamik tür korundu. Şimdi alttaki kodu devreye sokalım:

```CPP
#include <iostream>
#include <cstdio>
#include <string>

void func()
{
	// code
	throw std::out_of_range{ "aou_of_range error" };
}

void foo()
{
	try {
		func();
	}
	catch (const std::exception& ex) {
		std::cout << "exception caught:" << ex.what() << '\n';
		std::cout << &ex << '\n';
		//code
		//throw;	//rethrow
		throw ex;
	}
}

int main()
{
	try {
		foo();
	}
	catch (const std::out_of_range) {
		std::cout << "exception caught in main: std::out_of_range\n ";
	}
	catch (const std::exception& ex)
	{
		std::cout << "exception caught in main: std::exception& " << ex.what() << '\n';
	}
}
```
**Çıktı:**
```CPP
exception caught:aou_of_range error
0000003DEF2FF778
exception caught in main: std::exception& aou_of_range error
```
> Az önce main'de yakalayan Out of range parametreye sahip catch bloğuydu. Fakat şimdi main'de yakalayan Exception parametreli catch bloğu. 

> rethrow statement Demek ayrı bir sentaks kuralına tabi.

**Özetle:**
throw: İfadesi olmayan statement. Exception nesnesi. Aynı nesne yukarıya gönderilecek. Burada dinamik türü kaybetmiyoruz. 
throw ex; Exception sınıfının Copy constructları çağrılıyor. Çünkü Derleyici yeni bir nesne oluşturmak zorunda.

**Örnek:**

```CPP
#include <iostream>
#include <cstdio>
#include <string>

class NecException {

};
class ErgException {

};
class CSDException {

};

void handle_exception()
{
	try {
		throw;
	}
	catch (NecException& e) {

	}
	catch (ErgException& e) {

	}
	catch (CSDException& e) {

	}
}
void func()
{
	try {
		//hata
	}
	catch (...) {
		handle_exception();
	}
}
```
> Ben öyle bir yapı oluşturdum ki sadece bu exceptionları işliyorum. Gönderilen hata bu türlerdense bunları yakalayıp handle edeceğim. Yani bu catch blocklara çalışacak ama yakalamazsam  bu da ne demek? Gönderilen hatalar bu türlerden değilse yükselmeye devam edecek. (daha yukarıdaki katmanlar tarafından yakalanma ihtimali olacak)

> Eğer bu yapı birkaç yerde tekrar ediyor olsaydı ben o yerlerin hepsinde catch blocklarını tek tek oluşturmam gerekecekti. Ama şimdi bu ortak kodu bir yerde toplayıp bu şekilde handle exception fonksiyonunu çağırarak birden fazla kaynak kod noktasında aynı şekilde bu hataları yakalamaya çalışabilirim.

### Constructor'dan Exception gönderilmesi
 
- Constructor Exception gönderme ihtimali en yüksek olan fonksiyonlardan biri. Peki ya Constructor kendi koduyla nesneyi hayata getiremeyeceğini anlasa (Runtime'da oluşan istisnaî durumlardan ötürü) bu durumda geleneksel hata işleme yolları da devra dışı kalıyor Çünkü Constructor'ın geri dönüş değeri de yok. Peki Constructor binesneyi hayata getiremeyeceğini anladığında ne yapsın?
- Bu durumda ideali bir exception göndermek. Ama öyle bir domain olabilir ki, öyle bir ortam olabilir ki exception handling araçlarının kullanılması kısıtlanmış olabilir.

- Exception handling olmasa Constructor exception gönderemeyeceğine göre programın akışı bir şekilde Constructor'dan çıkacak, anabloğunun sonuna geldiğinde. Bu durumda nesne oluşmamış olmasına rağmen çağıran kod eğer bunun farkında olmazsa o nesneyi kullanma girişiminde bulunacak. Nesne aslında teknik olarak hayata gelmiş oldu ama fiili olarak kullanabilir durumda değil. Böyle nesneler için kullanılan bir yakıştırma var: **Zombie object**

- Bu durumda şunu yapabiliriz:  Nesnenin aslında Boolean bir veri elemanı olur ya da bir Boolean getiren fonksiyonu olur. Böylece nesneyi oluşturan kodlar nesneyi oluşturduktan sonra onun predicate fonksiyonunu çağırır, (burning is alive, usable vesaire gibi bir isim verebilirsiniz.) O şekilde nesneyi kullanma girişiminde bulunabilir.

- Kullanıcı kodları zombie nesneleri kullanmaya zorlamak yerine üretimde çok daha sık karşılaşacağımız duruma bakalım. **Constructor'ın exception throw etmesi.**

```CPP
#include <iostream>
#include <cstdio>
#include <string>
#include <stdexcept>

class Nec {
public:
	Nec()
	{
		///
		if (true)
		{
			throw std::runtime_error{ "nec exception" };
		}
	}
	~Nec()
	{
		std::cout << "Nec destructor\n";
	}
};

void foo()
{
	Nec x;
}

int main()
{
	try {
		foo();
	}
	catch (const std::exception& ex) {
		std::cout << "exception caught: " << ex.what() << '\n';
	}
}
```
> exception caught: nec exception

> Destructor çağırılmadı. Çünkü Destructor çağırılması için nesnenin hayata gelmiş olması gerekiyor. Hayata gelmedi. C++'ın en önemli kurallarından biri nesnenin hayata gelmiş kabul edilebilmesi için
konstraktırının ana bloğunun kodunun tamamının çalışması.

- Constructordan exception trove ediyorsanız bu exception'ın yakalanması durumunda herhangi bir şekilde hayata gelmemiş neslinin destraktırı çağrılmayacağı için exception'ın gönderildiği noktaya kadar çalışmış kodlar herhangi bir şekilde bir kaynak ediniyorlarsa ve bu kaynak pointerlar ile ya da referanslarla handle ediliyorsa destraktır da bunları geri veremeyecek ve böylece kaynak sızıntısı olacak.

**Örnek:** Programın akışı catch bloğuna çekildiğinde Member'ın destraktörü çalışır mı? Nec destrcutor çalışır mı?

```CPP
#include <iostream>
#include <cstdio>
#include <string>
#include <stdexcept>

class Member {
public:
	Member()
	{
		std::cout << "Member ctor\n";
		throw std::out_of_range{ "hata......" };
	}
	~Member()
	{
		std::cout << "Member destructor\n";
	}
};

class Nec {
public:
	~Nec()
	{
		std::cout << "Nec destrcutor";
	}
private:
	Member mx;
};

void foo()
{
	Nec nx;
}

int main()
{
	try {
		foo();
	}
	catch (const std::exception& ex) {
		std::cout << "exception caught: " << ex.what() << '\n';
	}
}
```

> İkisini de destructor'ı çağırılmaz çünkü ikisi de hayata gelmedi. Ne eleman hayata geldi, ne de programın akışı konstraktörün ana bloğunun sonuna kadar gelmediği için elemana sahip sınıf nesnesi olacak olan, nec nesnesi de hayata gelmedi.

- Şimdi senaryoyu biraz değiştirelim. Ve exception'ın member sınıfının konstraktörü tarafından değil nec sınıfının konstraktörü tarafından gönderildiğini düşünelim.

```CPP
#include <iostream>
#include <cstdio>
#include <string>
#include <stdexcept>

class Member {
public:
	Member()
	{
		std::cout << "Member ctor\n";
		
	}
	~Member()
	{
		std::cout << "Member destructor\n";
	}
};

class Nec {
public:
	Nec()
	{
		std::cout << "Nec constrıuctor\n";
		throw std::out_of_range{ "hata......" };
	}
	~Nec()
	{
		std::cout << "Nec destrcutor";
		
	}
private:
	Member mx;
};

void foo()
{
	Nec nx;
}

int main()
{
	try {
		foo();
	}
	catch (const std::exception& ex) {
		std::cout << "exception caught: " << ex.what() << '\n';
	}
}
```
```CPP
Member ctor
Nec constr²uctor
Member destructor
exception caught: hata......
```

> Programın akışı, konstraktörün ana bloğuna girmişse, sınıfın veri elemanları hayata gelmiş demektir. Member hayatta. Dolayısıyla stack unwinding sürecinde memberin destraktörü çağrılacak bu durumda.

**Örnek:** Burada oluşturulan dinamik ömürlü binesine nasıl oluşturuluyor?
```CPP
#include <iostream>
#include <cstdio>
#include <string>
#include <stdexcept>

class Myclass {
public:
	Myclass()
	{
		std::cout << "Myclass ctor\n";
		throw std::runtime_error{ "hata....." };
	}
private:
	char buffer[1024]{};
};

void foo()
{
	Myclass* p = new Myclass;

	delete p;
}

int main()
{
	std::cout << "sizeof(Myclass) =" << sizeof(Myclass) << '\n';

	try {
		foo();
	}
	catch (const std::exception& ex) {
		std::cout << "exception caught" << ex.what() << '\n';
	}
}
```

> New ifadesi aslında derleyici tarafından adeta iki kademeli bir koda dönüştürülüyor. Birinci aşamada aslında derleyici Operator New fonksiyonunu çağırıyor. (Operator New fonksiyonu mallok benzeri bir fonksiyondu, Void * döndüren parametre size_t olan). Ve aslında o fonksiyon bellek alanı elde ediyor. Sonra derleyici Operator New'in elde ettiği bellek adresi ile konstraktörü çağırıyor. Yani onu dispointer olarak kullanıyor.

> Myclass'ın Constructor'ı exception trove ettiğinde delete edilmeyecek çünkü programın akışı çıkacak. Delete operatörü koduna gelmediği için destraktörü çağırılmayacak.

- Programın akışı delete operatörü ifadesine gelseydi, Delete için derleyici nasıl bir kod üretiyordu? Önce destraktörü çağıracak. Destraktörün kodu çalıştıktan sonra da bu delete operatörün operandı olan adresi operatör delete fonksiyonuna gönderecek.

- Böyle durumlarda destraktır çalışmasa da konstraktırdan exception gönderildiğinde bu exception yakalandığında operatör delete fonksiyonu çağırılıyor.

- **Destraktır hiçbir şekilde exception göndermemeli.**
> Exception'ın throw edilmesi başka, throw edilen exception'ın bu fonksiyondan çıkması, daha yukarıdaki katmanlara doğru yükselmesi başka. İşte İngilizce'de burada iki tane feel kullanıyor:

1. Exception'ın fonksiyonun emit etmesi.
2. Exception'ın fonksiyondan ilgili koldan propagat etmesi

- Bir sınıfın destraktörü hiçbir şekilde exception göndermemeli derken, kast edilen burada ne? Emit etmemeli. Bu da ancak şöyle mümkün: 
> Ya hiç exception göndermeyecek ya da gönderilen bütün exceptionlar destraktör içinde lokal olarak handle edilecek. Yani exception dışarı sızmayacak. Destraktörden bir exception'ın dışarı sızmamasını engellemeniz gerekiyor.

**Destructor neden exception göndermemeli?**
- Bir sınıfın destraktörü iki nedenle çağrılıyor olabilir.

1. bir nesnenin normal olarak hayatı bittiği için
2. Bir exception handle ediliyordur. Programın akışı bir catch close'a girerken stack unwinding sürecinde stack frame'deki nesneler teker teker destru ediliyordur. Yani onların destraktörü çağrılıyordur.

- Eğer bir exception yakalanma süreci içinde stack unwinding gerçekleşirken çağrılan bir destraktör
exception trove ederse o zaman sevgili arkadaşlar terminate çağrılıyor. Biz zaten her şeyi terminate çağrılmasın, programımız ölmesin, çalışmaya devam etsin, abortla program sonlandırılmasın diye yapmıyor muyuz? O zaman bu garanti tamamen kaybedilmiş oluyor. O yüzden destraktörün hiçbir şekilde exception'ı emit etmemesi gerekiyor.

- Geçmişte olan modern C++'da önce deprekeyt edilen, sonra da tamamen dilden kaldırılan bazı araçlar var.  Şimdi önce deprekey edilen ve sonra da dilden tamamen kaldırılan o araç takımını İngilizce'de Dynamic Exception Specification deniyordu. Dynamic Exception Specification Bir fonksiyonun bildiriminde ve veya tanımında o fonksiyonun çalışacak kodunun hangi tür ya da türlerden Exception gönderme ihtimali olduğunu anlatan bir bildirimdi.

```CPP
void func(int) throw(std::out_of_range, std::bad_alloc);
```
> Modern C++ öncesinde exception specification ya da dynamic exception
specification denilen syntax bu şekildeydi. Eğer birden fazla türden hata gönderme ihtimali var ise bunları virgülerle ayrılan listeyle yazıyordunuz. Bu kod Funk fonksiyonunun out of range ya da bad_alloc sınıfları türünden exception
gönderme ihtimalini belirtiyordu.

- Eğer fonksiyonun bildiriminde dynamic exception specification kullanılmamışsa
bu da şu anlama geliyordu: Bu fonksiyonun exception gönderme ihtimali konusunda bir bildirim yapılmıyor. Yani bu exception göndermeme garantisi değil.

- Şimdi artık günümüzde bunların hepsi dilden kapı dışarı edildi. Yani ne dynamic exception specification var.  Ne unexpected fonksiyonu var. Ne de set unexpected fonksiyonu var. Bu konu tamamen bir yanlış deneyimi olarak değerlendirildi ve onun yerine yeni bir araç seti geldi. Bunun yerine gelen bir keyword var. Bu keyword no except keyword.

### noexcept keyword

**noexcept dilim kurallarına göre hem bir specifier hem de bir operatör.**

- Bir fonksiyonun bildiriminde no except specifierini kullanırsanız, bu fonksiyon exception throw etmeme garantisini veriyor demek.

```CPP
void func()noexcept;
```
> No throw guarantee. exception gönderme ihtimali yok.

```CPP
void func();
```
> Fonksiyonu bu şekilde bildirirsem bu exception gönderme ihtimali var demek.

```CPP
void func()noexcept(true);
void func()noexcept;
```
> Bu ikisi aynı anlamda.

```CPP
void func()noexcept(false);
void func();
```
> Bu ikisi dew aynı anlamda. Exception gönderebilir demek.

```CPP
void func()noexcept(sizeof(int) > 2);
```
> Derleyicimde sizeof int 2 den büyük ise burada exception göndermeme garantisi taşıyor. 

- Neden böyle bir araç var?  Compile time'da genelik programlama paradigmasıyla ilgili. Yani yukarıdakiş kodların çok fazla ifadesi olamaz ama generic programlama paradigması söz konusu olduğunda (yani bunlar funksiyon değil de örneğin funksiyon şablonu olsaydı) exception throw etme ihtimalinin olup olmaması, türün ne olduğuna bağlı olarak
derleme zamanda anlaşılacaktı.

```CPP
void f1(); // exception throw edebilir
void f2()noexcept; // exception throw etmeme garantisi
void f3()noexcept(true); // exception throw etmeme garantisi
void f4()noexcept(false); // exception throw edebilir
```

- noexcept aynı zamanda bir operator ve bir compile time operatorü.

```CPP
noxcept(expr);
```
> Bu operatörün parantezi içindeki ifade eğer exception throw etmeme garantisi olan bir ifade ise operatörümüz true değer döndürüyor.

```CPP
void foo();
constexpr bool b = noexcept(foo());
```
> False dönecek.

```CPP
void foo()noexcept;

void func()noexcept(noexcept(foo()));
```
> foo no except garantisi veriyorsa  func'ta veriyor anlamına gelen kod.

**noexcept unevaluated context**

**Bir fonksiyonun no exit garantisi vermesi neden önemli?**
- Bir bilgi iletiyor. Yani her ne yazmak istiyorsan, bu fonksiyonun bir exception göndermeyeceğine güvenebilirsin. Fakat bir de resmin doğrudan görünmeyen bir tarafı var: Derleyicinin Kod seçmesine yardımcı oluyor.

**Örnek:** Öyle durumlar var ki, Örneğin derliyici kod üretirken, Bir fonksiyonun no exit garantisi vermesi ya da vermemesine bağlı olarak Alternatif iki koddan birini seçebiliyor. Örneğin noexcept garantisi varsa taşıma semantini kullanırken, noexcept garantisi yok ise kopyalama semantini kullanabiliyor.

**Örnek:**
![image](https://user-images.githubusercontent.com/75746171/213817892-ef99c67e-7add-4466-9715-ab96da36ff35.png)

> Diyelim ki dinamik dizide  biz Myclass sınıfı türünden nesneler tutuyoruz. Diyelim ki vektorumuzun kapasitesi dörtgen, size da dört. Ben bu vektöre bir eleman daha eklesem Realocation olmak zorunda. Vektör sınıfının ilgili kodu, daha büyük bir bellek alanı alocate etti Ve şimdi artık vektördeki nesnelerin aktarılması lazım.

> Vektörde tutulmakta olan Myclass nesnelerinin buraya aktarılması için iki tane ihtimal var. Biri Taşıma semantinin kullanılması. Diğeri Myclass sınıfının copy konstraktörünün çağrılması. Kaynağın çalınması ile buradaki nesnelerin oluşturulması ciddi bir maliyet farkı yaratır.

- Ya move konstraktör exception throw etme ihtimali taşıyorsa? Bu durumda bu işi yapan fonksiyonun belirli garantileri vermesi için taşıma yapma şansı kalmayacak çünkü taşıma yapması durumunda exception throw etme ihtimali var. Eğer exception throw ederse strong garanti sağlayamayacak. B
- Bu durumda derliyice gidiyor Myclass isimli sınıfın move konstraktörünün exception throw etme garantisi olup olmadığına bakıyor. Exception throw etme garantisi varsa bu taşıma kodunu oluşturuyor. Ama exception throw etmeme garantisi varsa taşıma kodunu kullanıyor.
- Yani burada oluşturulacak nesneler için move konstraktörün çağrılacağı bir kod üretirken eğer my class sınıfının move konstraktörü exception throw etme ihtimalini taşıyorsa o zaman copy konstraktörü kullanıyor.

> Copy konstraktör exception throw ederse eski durumuna geri döndürebilecek bir şekilde kod yazıyor. Ama move konstraktör exception throw ederse artık diğer nesnenin kaynağını çaldığı için eski duruma geri getirmek ihtimali yok.

**Özet:** bir fonksiyonun no except garantisi vermesi aslında hem okuyucuya hem de derliyeceği verilen bir bilgi olduğu için derliyeci bu bilgiden faydalanarak daha uygun daha etkin kod üretme şansına sahip.

- Destructor no except belirteci olmasa da no except belirtecine sahip kabul ediliyor. Yani Destructorun artık modern c++ da default durumu no except. No except belirteceni yazsınız da yazmasanız da.

**Exception göndermeme garantisini taşıyan bir fonksiyonun code runtime'da çalışırken o fonksiyonun çalışan kodundan bir exception gönderilirse stut terminate çağırılıyor.**

# Ders 26

**Hangi fonksiyonlar noexcept olmalı?**

- destrcutor - noexcept
- move ctor - (Aksi yönde bir engel yoksa noexcept yapılmalı, nothrow garantisi vermeli)
- swap - (Aksi yönde bir engel yoksa noexcept yapılmalı, nothrow garantisi vermeli)
- memory dealocate fonksiyonlar

- C++'ın Terminolojisinde Herhangi bir fonksiyonun Exception safety Açısından Verdiği güvenceler var. 
> Bir fonksiyon Eğer Çalışan kodundan Exception-Gönderildiğinde Bir Kaynak Sızıntısı Oluşturma Riski'ni taşıyorsa Bu fonksiyon Hiçbir şekilde bir garanti vermiyor demektir. 

- Bir fonksiyon çağırıldığında Bir Exception-Gönderilirse Fakat Bu fonksiyon içinde Edinilmiş bir kaynak Geri verilmiyor ise Bu durumda bir kaynak sızıntısı var. Bu durumda program exception safe değil. 

**Basic Guarantee:** Bir fonksiyonun kodu çalıştığı zaman, Bir kaynak edinildiği zaman, O kaynak Mutlaka geri veriliyor. Hiçbir şekilde resource leak olmuyor. Basic Garanti sağlamak zorundasınız. 

**Strong Guarantee:** Görevli olduğu işi gerçekleştirmiş olacak,  Eğer o işi gerçekleştiremezse ilk konuma geri döndürecek.

## Generic Programlama Paradigması

- Derleyici bizim için kod yazabilen bir program.

1. bizim doğrudan yazdığımız kodlar
2. Öyle bir kodu yazıyoruz ki Yazdığımız kodun Amacı derleyiciye kodu yazdırmak (Template)

- Template aracıyla biz derleyiciye kod yazdırabiliyoruz. Yani eğer bir kodun Template olduğunu söylüyorsam O kodun amacı Derleyiciye kod yazdırmak. 

1. Function template: Varlık nedeni derleyiciye bir fonksiyonun kodunu yazdırmak.
2. Class Template: Sınıf kodu yazdırmak için kullandığımız kod

- Modern C++'a kadar Templetlerin sadece bu iki kategorisi vardı. Fakat Modern C++'a birlikte 2 tane daha Şablon kategorisi eklendi

3. Variable Template (Derğişken şablonu)
4. Alias Template (Tür eş ismi şablonu)

- C++ stanbdart kütüphanesinin neredeyse tamamına yakını template kodlardan oluşuyor. Mesela string diye bir sınıf yok, aslında bu bir sınıf şablonu. Biz böyle bir nesne tanımladığımızda derleyici o sınıf şablonunun kodundan bir sınıf kodu yazıyor. Yani String Sınıfının kodu Compile Time'da Derlayıcı tarafından yazılıyor.

**Neden böyle bir araç var?**

- Fonksiyonların önemli bir kısmı Algoritmaları implement ediyor. Algoritmalar Çoğunlukla türe bağlı değil

**Mesela iki değişkeni nasıl swap ediyoruz?**

- Bir tanesinin değerini Bir değişkende tutarım, Birinciye ikinciye atarım İkinçye o değişkende tutulmuş Değeri atarım.
> Burada betimlenen algoritmada swap edilecek değişkenlerin türünün ne olduğunun bir farkı yok. Ama kod, c++ c# ve java gibi dillerde statik olarak türebağlı. Dolayısıyla biz aynı algoritmayı farklı türler işçin implemente etmek zorunda kalıyoruz.

- Peki her defasında aynı algoritmayı tekrar türe bağlı olarak yazmak yerine bunu nasıl daha kolay hale getirebiliriz? Generic programlamada bununla ilgili farklı araç setleri var.

1. Nesnelerin türünü göz önüne almayıp onları salt bellek bloıkları olarak görmek. Yani foınksiyonunu aslındatürü bilmeden işi gerçekleştirmesini sağlamak.

**Mesela C dilinde generic bir swap fonksiyonu yazarlım:**

```CPP
void gswap(void* vpx, void* vpy, size_t sz);
```
> Ben bu fonksiyona Swap edilecek nesnelerin adresleri Ve onların bellekte Kaç bytes yer kapladıkları Bilgisini gönderirsem Bu fonksiyon türü bilmeden O iki bellek bloğundaki byte ları takas eder. Böylece bu foksiyonu çağıran kod, double veya int nesnei takas etmek için de çağırabilir. Bunun en tipik örneği C standart kütüphanesinde stdlib stdlib başlık doyasında bildirilen **qsort** fonksiyonu. 

**qsort** fonksiyonu türden bağımsızo larak bir diziyi sarmalıyor.

```CPP
qsort(void *_Base, size_t _NumOfElements, size_t _SizeOfElements,     _CoreCrtNonSecureSearchSortCompareFunction _CompareFunction)
```
> Görüldüğü gibi, ilk parametresi void*, ikinci parametresi sıralanacak dizinin boyutu, üçüncü parametresi bir elemanının sizeof değeri, dördünüc parametresi dizinin iki elemanını karşılaştıracak fonksiyonun adresini istiyor. Qsort işi yapıyor ama sıraladığı dizinin elamanlarının türünün ne olduğunu bilmeden yapıyor. Çünkü ona göre aslında bunlar birer bellek blokları. 

**Diğer bir generic yapı:**
- Ortak bir kodun olması Fakat bu kodun Ortak bir interface i desteklediğini düşünerek yazılması.

**Not:**
- İki tane int nesneyi takas eden Funksiyonun kodunu yazarken Derliyici int* int* Ya da int& int& Parametreyle fonksiyon yazacak. Double türden iki tane nesneyi Takas eden kodu yazmak için Bu seferde derliyici Double&  double& Parametreyle fonksiyon yazacak. Yani derliyicimin yazdığı fonksiyon Compiletime'da O türün ne olduğuna bağlı Olarak, İngilizcesiyle TaylorMade Olarak yazılacak.

**Sınıf şablonu için düşünün:**
- Vektörün int açılımı Dediğimizde derliyici İçinde intler tutulan Bir dinamik dizi Sınıfı kodu yazarken, Vektörün string açılımı Dediğimizde Bu seferde derliyici İçinde stringlerin tutulduğu Bir dinamik dizi sınıfı Kodu yazacak. 

> Derliyicinin Compiletime'da bu kodları yazmasının Bir takım Faydaları da var. (Belki dezavantaj oluşturulan noktalar da var, Örneğin KomparTime'ın uzaması gibi) 

> En önemli avantajlardan biri Çarılmayan fonksiyonların Kodlarının yazılmaması.

**Mesela string sınıfını düşünün:**
- String sınıfının Overloadlarını da düşünürseniz belki 200'e yakın Üye fonksiyonlar. Ama string sınıfı Bir sınıf şablon olduğu için, Siz örneğin String nesnesini tanımladığınız zaman Derliyici sadece Constructor'ın ve destructor'ın kodunu yazıyor. 

```CPP
int main()
{
	using namespace std;
	string str{ "ali" };
}
```
> Örneğin böyle bıraksaydım derleyici sadece const char* parametreli constructor ve destructor yazacaktı. Ama diyeim ki bir başka fonksiyon çağırdık:

```CPP
int main()
{
	using namespace std;
	string str{ "ali" };

	str.length();
}
```
> Bu sefer de length fonksiyonunun kodunu yazıyor.

**Özetle:**

Ben içinde int tutan bir bağlı listeyi nasıl implemente ederim demek yerine, ben bir bağlı listeyi naasıl implemente ederim diye sorguluyoruz. Daha yüksek düzeyde bir soyutlama.

**Buradaki c++ gücü:** Nesni yönelimli programlamaya Destek veriyor, Procedüel programlamaya da destek veriyor, Funksiyonel programlamaya Büyük ölçüde destek veriyor. Ama en güçlü olduğu alan, Hepsiyle birlikte Cenerik programlama paradigmasını desteklemesi.

## Template

```CPP
template <parameter>
```
> Template parametreleri bu kategorilerde olabilir:
> 1. type parameter
> 2. non-type parameter
> 3. template parameter

**Type parameter:** Öyle bir identifier ki derleyiciye ve okuyucuya şunu söylüyor: "Bu isim bir tür temsil ediyor". Yani derleyicinin yazacağı kodda Bu isim yerine Bir tür kullanılmış olacak.  
- Template parametrelerini bildirirken **class** veya **typename** anahtar sözcüklerinden biri kullnaılmak zorunda. 
- Class tür parametresi birden fazla olabilir. 

```CPP
template <typename T, typename U>
```
**Derleyici Kendi yazdığı kodda T'nin ya da U'nun yerine Hangi türü kullanacağını Nereden bilecek?**

1. **(Template argument deduction)** Template parametrelerine karşı Derleyicinin Yazdığı kodda kullanılan gerçek türlere ya da sabitlere template Argümanları deniyor. Template parametresi ve argümanı farklı şeyler. Template argümanı, template parametresine karşılık gelen, derleyicinin yazdığı kodda kullanılan varlık.
2. **(Template explicit arguments)** Explicit olarak template argumentlarının Neler olduğunu Derleyici'ye ben söylüyorum. 

```CPP
func<int>(12)
```
> Func bir template, Onun bir tür parametresi var. Sen bu templateten Funksiyonun kodunu yazarken O tür parametresi yerine int kullanacaksın, anlamına geliyor.

3. **(Default template argument)** Template argument'ın Ne olduğunu Ben derleyiciye söylemediğim zaman Önceden belirlenmiş Bir argument Ya da sabit alınıyor.

```CPP
template <typename T = int>
```
> Bu Şablon'dan kod üretimi Söz konusu olduğu zaman T'ye karşılık gelen template
Argümanı yazılmazsa Sen onun yerine Int'i alacaksın, anlamına geliyor. 

## non-type parameter

```CPP
template<int x>
class Myclass {
	int ival = x;
};
```
> Derleyici, X kullandığım yerde Sen bu sınıfın kodunu yazarken Int türünden bir sabit Kullanacaksın. 

> Yani Derleyici X'in karşılığı olan Template Argümanının 10 olduğunu bilirse Burada 10 değerini Kullanacak, 20 olduğunu bilirse 20 değerini kullanacak.

- Demek ki Template Non-type parametre Demek, bu bir sabit demek. Bir ya da birden fazla yerde Kullanılacak
Bir sabit. Yani buna karşılık gelen Argüman bir sabit olacak.

**Not:** C++20 standartlaırna kadar template non-type parametre sadece tamsayı türlerinden olabiliyordu ama C++ 20 ile birlikte artık gerçek sayı türleri de kullanılabiliyor.

```CPP
#include <iostream>
#include <cstdlib>
#include <bitset>

int main()
{
	using namespace std;
	bitset<16>;
}
```
> Derleyici, bitset sınıf şablonundan bir sınıf kodu yaz. Ama o şablonun non-type parametresi karşılığı 16 sabitini kullan.

**Özet:** non-type parametre bir sabite kaşılık geliyor, type parameter ise bir türe karşılık geliyor.

**Template instantiation:** Derliyici Compile Time'da Bir template kodu kullanarak O template koddan Gerçek kodu üretecek. Örneğin bir fonksiyon şablonundan Bir fonksiyonun kodunu yazacak. Burada fonksiyon şablonu template, Ama Derliyicinin fonksiyon şablonundan Gerçek fonksiyonun kodunu yazması O template'i  etmesi instantiate etmesi.

### Fonksiyon Şablonları

```CPP
template <typename T>
void func(T x);
```
> Böyle bir fonksiyon şablonundan t'yi int olarak alırsa derliyici template argümanının int olduğunu öğrenirse derliyicinin yazdığı fonksiyon böyle bir fonksiyonu olacak:

```CPP
void func(int);
```

> Dolayısıyla aynı fonksiyon şablonundan farklı template argümanlarıyla oluşturulmuş fonksiyonlar doğal olarak birbirlerinin overloadlarıdır. Yani fonksiyon şablonu kullanarak function overloading'de oluşturmuş olabiliriz.

**fonksiyon şablonları overload edilebilir mi?**

```CPP
template <typename T>
void func(T x);

template <typename T>
void func(T x, T y);
```
> bu fonksiyon şablonlarından elde edecek fonksiyonlarda birbirini overload etmiş olacak.

**Template parametreleri karşılığı template argümanlarının ne olması gerektiğini derleyici nasıl anlayacak?**

- Bir fonksiyon şablonu var. Fonksiyon şablonunun bir ya da birden fazla template parametresi var, derleyicinin bu fonksiyon şablonundan gerçek bir fonksiyonun kodunu yazabilmesi için, yani bu template initialize edebilmesi için template parametrelerine karşılık gelen template argümanlarının ne olduğunu bilmesi gerekiyor. Bunun için bir deduction mekanizması var.



- C++ 17'ye kadar parametreler sınıf şablonlarında template argümanının explicit olarak yani açısal parantez içinde bildirilmesi mecburiydi. Fakat C++'ın 2017 standartlarıyla dile çok önemli bir araç eklendi. CTAD araç seti.

```CPP
vector x{ 1,5,5 };
```
> Vektör bir sınıf şablonu olmasına rağmen ben vektör sınıf şablonunda kullanılacak template argümanlarının ne olması gerektiğini derleyeceğe söylemedim. Ona rağmen bir deduction yapıldı. İşte burada yapılan deduction C++ 17'de eklendi.

**Derleyicinin template parametresi karşılığı nasıl bir çıkarım yaptığını compile time'da görme şansım var mı?**

```CPP
template <typename T>
class TypeTeller;

template <typename T>
void func(T)
{
	TypeTeller<T> x;
}
```
> Eğer örneğin derleyici T türünün çıkarımını int olarak yapmışsa, buradaki X, typeteller sınıf şablonunun int açılımı türünden olacak değil mi? 

> Şimdi bu sınıf şablonunun sadece bildirimi yapıldığı için, dolayısıyla oluşturulan sınıflar in-complete type olacağı için, bu şekilde bir nesne oluşturduğumda derleyici tipik olarak bana sentaks hatası verecek. In-complete type türünden nesne oluşturamazsın diyecek. Örnek:

```CPP
template <typename T>
class TypeTeller;

template <typename T>
void func(T)
{
	TypeTeller<T> x;
}

int main()
{
	func(10);
}
```
**Hata:** 'x' uses undefined class 'TypeTeller int '

> Yani T'nin yerine int kullanığını bize söylüyor.

**Kaç çeşit referans vardı?**

```CPP
	int x = 10;	
	int& r1 = x;	// L value ref
	int&& r2 = 20;	// R value ref
	auto&& r3 = 2340;	// Universal Ref
```
**Universal Reference:** Her şey ile ilk değer verebiliriz.

Bu durumda auto yerine gelecek olan tür ifadenin value kategorisine bağlıydı.

```CPP
	auto x = { 3,6,8,7 };
```
> X'in türü initializer list'in int açılımı.

```CPP
	std::initializer_list<int> x = { 3,6,8,7 };
```
> Bu da aynı anlama geliyor.

**template argument deduction ile auto type deduction arasındaki tek bir fark nedir?**

```CPP
	auto x = { 3,6,8,7 };
```
> auto type deduction'da bu şekilde bir Initializer kullandığınızda çıkarım yapılabiliyor. Auto yerine gelen tür initizlizer list.

```CPP
	auto x{ 3,6,8,7 };
```
> Böyle yazdığımızda kural farklı, çıkarım int olarak yapılıyor.

# Ders 27

```CPP
template <typename T>
void func(T, T);

template <typename T>
void foo(T&, T&);

int main()
{
	func("ali", "mert");
	func("ali", "can");
	foo("ali", "mert");
	foo("ali", "can");
}
```
> no instance of function template matches the argument list            argument types are: (const char [4], const char [5])

> Referans dekleratörü olduğu için burada tür çıkarımı artık dizi türü olarak yapılacak. ilk foo çağrısında const char [4], ikincide const char [5] olarak tür çıkarımı yapacak. O zaman bunlar aynı tür olamaz.

```CPP
int foo(int x)
{
	std::cout << "x = " << x << "\n";

	return{};
}

int main()
{
	auto i = foo({});
	std::cout << "i = " << i << "\n";
}
```
> Geçerli kod.

## RTTI (Runtime Type Information)

- C++ dilinde de bir nesnenin dinamik türünün programın çalışma zamanında anlaşılmasına, belirlenmesine yönelik araçlar var. bir nesnenin dinamik türünün programın çalışma zamanında anlaşılması ne demek?

```CPP
#include "car.h"

void func(Car* p)
{
	///
}
```
> Acaba programın çalışma zamanında buraya gelen arabanın, örneğin bir Mercedes olup olmadığını sınama şansımız var mı? Yani nesnenin dinamik türünün ne olduğunu sınamaya yönelik dilin doğrudan aracı var mı?

- Aslında bu sınama işlemi kötü bir tasarım. Çünkü runtime polimorfizminin virtual dispatch mekanizmasının  ana avantajını yitirmiş oluruz. Ana avantajı neydi? Nesnenin gerçek türünü bilmeden onun interface'inde belirli fonksiyonların, belirli operasyonların olduğuna güvenerek onlar üstünde ortak işlem yapmak.

- Fakat öyle durummlar var ki sınamaktan başka yol kalmıyor. Öyle yerler olabilir ki nesnenin dinamik türünün programın çalışma zamanında anlaşılması bana bazı başka avantajlar sağlayabilir.

- Özetle programın çalışma zamanında bir nesnenin türünün anlaşılmasına yönelik C++ dilinde 2 tane operator var.

1. dynamic_cast
2. Typeid

**dynamic_cast** bir tür dönüştürme operatörü. C dilnide doğrudan bir karşılığı yok. down castingin yani aşağı doğru dönüşümün programın çalışma zamanında güvenli olup olmadığını test ediyor. Bu ne demek?

```CPP
#include "car.h"

void func(Car* p)
{
	//
}
```
> Burada p'yi audi* a dönüştürürsem bunu bir Audi nesnesi olarak kullanabilir miyim? Sorusunun cevabı. Bu da aslında şu demek, P'nin gösterdiği nesne gerçekten de bir Audi mi?

> Eğer P'nin gösterdiğin nesne farklı bir araçsa ve ben onu Audi olarak kullanma girişiminde bulunursam Compile Time'daki engelleri aşsam bile Runtime'da tanımsız davranış olacak, Runtime hatası olacak. Bunu bir Audi olarak kullanabilmem için Runtime'da bundan emin olmalıyım. İşte Dynamic Cast Operatörüyle bunu gerçekleştirebiliyorum.

### Typeid operator

**Tür olarak kullanımı:** polimorfik bir tür olmak zorunda değil. 

```CPP
typeid(int)
typeid(Myclass)
typeid(string)
typeid(Base)
typeid(Der)
```
**Operandı ifade olabilir:**
```CPP
typeid(x)
typeid(*ptr)
typeid(12)
```

- typeid operatörüyle oluşturulmuş bir ifade aslında bir type info nesnesine referans.

> typeid(int) bu bir typeinfo sınıfı türünden bir nesne.

- type id operatörüyle eriştiğiniz type info nesnesi belirli bir türü temsil ediyor. Yani örneğin int türünün int türü olduğunu gösteren type info nesnesiyle double türünü temsil eden type info nesnesi ayrı nesneler.

**Template**

```CPP
template <typename T, T x>
class Myclass {

};
```
> T, type parametre, x non-type parametre. Böyle bir template yapısı, t'nin type parametre olduğunu, yani t için bir tür kullanılması gerektiğini, Ama x'in ise t türü'nden bir non type parametre olduğunu söylüyor. Yani t'ye int ise, ikinci template parametresi int turdan bir sabit olacak.

```CPP
template <auto n>
class Myclass {

};

int main()
{
	Myclass<10>;
}
```
> Bu durumda sanki auto yerine x yazılmış kabul edilecek.

**Örnek:**

```CPP
template <typename T>
void func(T x)
{

}
```
```CPP
void func(auto x)
{

}
```
> Bu ikisi de aynı anlamda. C++ 20 ile gelen özezllik. Yazdığımız fonksiyon direkt template oldu.

**Auto return type:**

```CPP
auto func(int x)
{
	return x * x;
}
```
> Fonksiyonun geri dönüş değeri türünü return ifadesinden yap.

- Fonksiyonların c++'da geri dönüş değerinin türü'nü anlatmak için ister template olsun, ister template olmasın, 4 tane yol var.

1. Fonksiyonun geri dönüş değerinin türü'nü açıkça yazmak, c'de olduğu gibi.
2. **trailing return type:**

```CPP
auto foo()->int
{
	return 1;
}
```
> Bu template ler ile ilgili kullanılıyor.

3. auto return type
4. decltype(auto) return type

**Örnek:**

```CPP
template <typename F>
void func(F f)
{
	f(10);
}

void foo(int x)
{
	std::cout << "foo cagrıldı x = " << x << '\n';
}

int main()
{
	func(foo);
}
```
> Derleyici Template argument deduction yaptı. Foo'nun argümanının türünden f'nin türünün void(*)(int) oldugunu anladı. Dolayısıyla bu kod derlendiğinde aslında function pointer olan f'nin gösterdiği fonksiyon foo fonksiyonu çağrılmış oldu.

## Explicit Template Argument

bir fonksiyon şablonunda ben template parametresine karşılık gelen argümanın ne olduğunu çıkarıma bırakmak zorunda değilim. 

```CPP
template <typename T>
void func(T x)
{

}
int main()
{
	func<int>(12);
}
```
> Böyle de çağırabilirim. Burada template'in isminden sonra yazılan açısal parantez içinde kullandığınız varlıklara explicit template argument deniyor. Yani template argument'ın ne olduğunu siz açıkça söylüyorsunuz.

```CPP
template <typename T>
class TypeTeller;

template <typename T>
void func(T)
{
	TypeTeller<T> x;
}

int main()
{
	float f = 3.46f;
	func(f);
}
```
> Burada f float. Şimdi değiştirelim:

```CPP
template <typename T>
class TypeTeller;

template <typename T>
void func(T)
{
	TypeTeller<T> x;
}

int main()
{
	float f = 3.46f;
	func<double>(f);
}
```
> Şimdi f 'nin double olduğunu görüyoruz. Yani artık burada çıkarım yapılmıyor. Siz fiilen template argümanı olarak neyin kullanılması gerektiğini söylüyorsunuz.

- non-type parametre için de bu geçerli: 

```CPP
template <typename T>
class TypeTeller;

template <typename T, int>
void func(T)
{
	TypeTeller<T> x;
}

int main()
{
	float f = 3.46f;
	func<double,10>(f);
}
```
> Böylece birinci template parametresi karşılığı kullanılacak türü argümanının double, ikinci template parametresi non-type parametre karşılığı kullanılacak sabit argümanında "10" olması gerektiğini söylemiş oldunuz. 

- Bir kısmını ben söyleyeyim, bir kısmının çıkarımını derleyici yapsın?

**Örnek:**

```CPP
template <typename T>
class TypeTeller;

template <typename T, typename U,typename W>
void func(U, W)
{
	
}

int main()
{
	float f = 3.46f;
	func<double>(1,4.5);
}
```

- Fonksiyon şablonuyla fonksiyonun bir arada bulunması bir hata değil:

```CPP
template <typename T>
void func(T x)
{
	std::cout << "function template specialization T is" << typeid(T).name() << "\n";
}

void func(int x)
{
	std::cout << "func(int x) x =" << x << "\n";
}

int main()
{
	func(12.4);
}
```
> Bu durumda function overload resolution şöyle yapılacak. Funksiyona gönderdiğim argumandan hareketle template ten elde edilecek fonksiyonun imzasının anlaşılması için substitution dediğimiz süreç gerçekleşecek.

**substitution:** template parametresinin ne olduğu belli. Böylece fonksiyonun parametrik yapısında ve geri dönüş değeri türünde template argümanını yerine koyarak
bir parametrik yapı elde etmek.

**Partial Ordering Rules Örneği:**

```CPP
template <typename T>
void func(T)
{

}
//template <typename T>
//void func(T *)
//{
//
//}

int main()
{
	int x{ 10 };
	func(&x);
}
```
> bu durumda fonksiyonun parametre türü int yıldız olacak. Yani t türünün çıkarımı int * olarak yapılacak.

```CPP
//template <typename T>
//void func(T)
//{
//
//}
template <typename T>
void func(T *)
{

}

int main()
{
	int x{ 10 };
	func(&x);
}
```
> Burada ise T türü int olacak.  Her ikisi birlikte olduğunda ise:

```CPP
template <typename T>
void func(T)
{

}
template <typename T>
void func(T *)
{

}

int main()
{
	int x{ 10 };
	func(&x);
}
```
> burada kullanılan kural setini partial ordering rules deniyor. (hangi templetten specialization yapılacağına yönelik kural seti). Daha spesifik olan seçilecek. Burada daha fazla dekleratöre sahip olan seçilecek. 

```CPP
template <typename T>
void func(T)
{
	std:cout << "func(T)\n";
}
template <typename T>
void func(T *)
{
	std:cout << "func(T*)\n";
}

template <typename T>
void func(T**)
{
	std:cout << "func(T**)\n";
}

int main()
{
	int x{ 10 };
	int* p = &x;

	func(&p);
}
```
> Her bir template uygun. En spesifik olan T** olan seçilecek. 

# Ders 28

- Nasıl bir fonksiyon shablonundan derliyici bir fonksiyon kodu oluşturuyor, böylece biz adeta bir algoritmayı türden bağımsız ifade edebiliyoruz. Zaten fonksiyon şablonlarının ana fikri bu. Türden bağımsız kodları, türden bağımsız bir formatla ifade edip, derliyicinin compile time'da onları türe bağlı hale getirmesi. Böylece daha yüksek düzeyde bir soyutlama sağlıyoruz. Ortak kodu bir yerde topluyoruz. Mesela algoritmada bir değişiklik yapmak istediğimiz zaman bir tek template kodu değiştirip tekrar derlersek, bu seferde bütün farklı türler için yeni kod kullanılacak.

**Örnek: İki string'i bu şekilde swap ettiğimizi düşünelim:**

```CPP
template <typename T>
void Swap(T& x, T& y)
{
	T temp(x); // copy constructor
	x = y;		// Copy assignment
	y = temp;	// Copy assignment
}
```

```CPP
vector<int>
```
> Elemanları int olan bir diziyi temsil ediyor.

- C++ 17'ye kadar template lerde decduction yoktu. Sınıf şablonlarında template argümanlarının yazılması mecburiydi. C++17 ile önemli bir ekleme yapıldı. CTAD: Class TEmplate Argument Deduction. 

```CPP
using namespace std;

int main()
{
	vector x{ 1,3,5,7 };  // vector<int> x{ 1,3,5,7 };
}
```
> vektör bir sınıf olmasına karşın template argümanında vektör isminden sonra gelecek açısal parantezi içinde belirtmeden böyle bir sınıf nesnese oluşturuyorum. CTAD bunu sağlıyor. Derleyici burada bir deduction yapıp 1. template parametresi yerine template argument olarak int kullanılacağını nereden anlıyor? Cevap: Constructor gönderilen argümanlardan. 


**Kısaca CTAD:**  Derleyici bir sınıf şablonundan oluşturulacak sınıf türünden nesnenin
oluşturulduğu bildirime yaparken constructor'a gönderilen argümanların hangi türden olduğuna ya da olduklarına bakarak template argümanlarının ne olduğunun çıkarımını yapıyor.

```CPP
using namespace std;

template <typename T>
class Myclass {
public:
	Myclass(T);
};

int main()
{
	Myclass x(13);
}
```
> Derleyici constructor'a gönderilen argümanın int türden olduğunu gördüğü için x'i
my class'ın int açılımı türünden olması gerektiğini anlıyor.

```CPP
template <typename T>
class Nec {
private:
	T mx;
};
```
> Nec'in int açılımı söz konuusu olduğunda veri elamanı int, double söz konusu olduğunda veri elemanı double olacak.

```CPP
template <typename T>
class Counter {
public:

private:
	T cnt;
};
```
> Counter'ın int açılımında veri elemanı int olacak counter'ın  long açılımında veri elemanı long olacak. Dolayısıyla öyle bir counter türü oluşturmuş olacağız ki bizim sayacımız int, long int, long long int olabilecek.

**Örnek:**
```CPP
template <typename T>
class Counter {
public:
	Counter() = default;
	explicit Counter(T val) : m_cnt{val}{}
	T get()const
	{
		return m_cnt;
	}
private:
	T m_cnt;
};

int main()
{
	Counter c1;
}
```
> Bu durumda sınıf şablonunun hangi açılım olduğu belli değil. Yani sınıf şablonunun kendisini bir sınıfmış gibi kullanma girişiminde bulunursanız sentaks hatası olur.

- Fonksiyonu sınıf dışında tanımlamak istersem nasıl olacak:

```CPP
using namespace std;

template <typename T>
class Counter {
public:
	Counter() = default;
	explicit Counter(T val) : m_cnt{val}{}
	T get()const;
private:
	T m_cnt;
};

template <typename T>
T Counter<T>::get() const
{
	return m_cnt;
}
```

### Pair Sınıfı

- Struct anahtar sözcüğü ile tanımlanmış bir sınıf. Doalyısıyla ögeleri doğrudan public.
- 2 Tane template parametresi var. 

```CPP
	pair<int, double>;
```
- Tutulan ögeler fonksiyon değil. Sınıfın non-static veri elemanları. X'in first'ünü yazdıralım:

```CPP
int main()
{
	pair<int, double>x;
	std::cout << "x.first= " << x.first << "\n";
}
```
> DEfault initilaize edilmesi durumunda igeler default value init ediliyorlar. Yani değerleri sıfır. Bu bir sınıf türü olsaydı default constructor çağırılacak. (Value init edildiğinde)

```CPP
int main()
{
	pair x = { 45,6.7 };
	std::cout << "x.first= " << x.first << "\n";
	std::cout << "x.second= " << x.second << "\n";
}
```
> Derleyici burada constuırctor'a gönderilen argümanlara bakacak ve ilk argümanın int ikincinin doubnle olmasından hareketle bunun, pair'in int-double açılımı olduğunu anlayacak.

```CPP
int main()
{
	pair <double, double>dp;
	pair <int, int>ip{2,5};

	dp = ip;

	std::cout << "x.first= " << x.first << "\n";
	std::cout << "x.second= " << x.second << "\n";
}
```
> Bu atama legal, member template olduğuı için.

```CPP
int main()
{
	pair <string, string>x;
	pair <const char*, const char*>y{"murat", "hakan"};

	x = y;
}
```
> Bu da legal fakat farklı bir tür olsaydı illegal olabilirdi. Legal olması için ögelerin birbirine atanabiliyor olması gerekiyor.

```CPP
	auto p = make_pair(12, Date{ 12,6,1986 });
```
> p'nin türü, pair'in (int,Date) açılımı oldu.

**Bir pair'i çıkış akımına insert edecek kod:**

**inserter:** Operator < fonksiyonunu overload eden fonksiyonlar.

- standart kütüphanenin pair sınıfı için yazılan bir inserter yok.
- Eğer inserter olsaydı:

```CPP
	cout << make_pair(12, 4.5) << "\n";
```
> Eğer inserter olsaydı bunu ekrana yazması gerekirdi ama hata.

**Şimdi herhangi bir pair'i standart output veya çıkış akımına yazdırabilecek bir "operator <" fonksiyonu yazalım.**
> Böylece pair yazdırmamız gerektiğinde bizim fonksiyon şablonumuz kullanılacak.

```CPP
#include <ostream>
#include <utility>

template <typename T, typename U>
std::ostream& operator<<(std::ostream& os, const std::pair<T, U>& p)
{
	return os << '[' << p.first << "," << p.second << ']';
}
```
> böylece bu kodumuz geçerli oldu:

```CPP
int main()
{	
	pair p{ "necati", Date{4,5,1994} };
	cout << p << '\n';
}
```

### Tür eş ismi bildirimleri:

- Modern C++ öncesi bir türe eş isim oluşturmaının tekl you typedef bildirimleriydi. 
- Typedef anahtar sözcüğü ile yapılan tür eş ismi bildirimleri template haline getirilemiyor. 

```CPP
typedef std::pair<int, int> ipair;
```
> Böylece ipar, pair'in int,int açılımının eş ismi oldu.

- Using anahtar sözcüğü ile yapılan tür eş isim bildirimleri template haline getirileiliyor. 

# Ders 29

### explicit specialization
// eksik

### Template Partial Specialization

- Explicit Specialization'dan farklı olarak şimdi belirli tür argümanı ya da argümanları için değil, bir tür argümanı grubu için bir Specialization veriyorsunuz. Pointer türleri için, Dizi türleri için...

- Partial Specialization'da, fonksiyonlar için bu araç kullanamıyor. Yani sadece sınıf şahlonları için kullanabiliyoruz.

**Örnek:**

```CPP
template <typename T>
struct Nec {
	Nec()
	{
		std::cout << "primary template\n";
	}
};

template <typename T>
struct Nec<T*> {
	Nec()
	{
		std::cout << "partial specialization Nec<T*>\n";
	}
};
int main()
{
	Nec<int> n1;
	Nec<double> n2;
	Nec<int *> n3;
	Nec<int **> n4;
}
```
> Pointer türleri söz konusu olduğunda partial specialization kullanılıyor. 

```CPP
template <typename T, typename U>
struct Nec {
	Nec()
	{
		std::cout << "primary template\n";
	}
};

template <typename T>
struct Nec<T, int> {
	Nec()
	{
		std::cout << "partial template\n";
	}
};

int main()
{
	Nec<double, long> n1;
	Nec<int, long> n2;
	Nec<float, char> n3;
}
```
> Hepsi primary template

```CPP
template <typename T, typename U>
struct Nec {
	Nec()
	{
		std::cout << "primary template\n";
	}
};

template <typename T>
struct Nec<T, int> {
	Nec()
	{
		std::cout << "partial template\n";
	}
};

int main()
{
	Nec<double, long> n1;
	Nec<int, long> n2;
	Nec<float, char> n3;
	Nec<float, int> n4;
	Nec<int, int> n5;
}
```
> Burada partial specializaytion da geldi.

```CPP
template <typename T, typename U>
struct Nec {
	Nec()
	{
		std::cout << "primary template\n";
	}
};

template <typename T>
struct Nec<T, T> {
	Nec()
	{
		std::cout << "partial template\n";
	}
};

int main()
{
	Nec<int, char> n1;
	Nec<int, int> n2;
	Nec<char*, char*>n3;
}
```
> Aynı türler olduğunda partial oldu.

```CPP
template <typename T, typename U>
struct Nec {
	Nec()
	{
		std::cout << "primary template\n";
	}
};

template <typename T, typename U, typename V, typename M>
struct Nec<std::pair<T, U>, std::pair<V, M>>
{
	Nec()
	{
		std::cout << "partial specialization\n";
	}
};

int main()
{
	using namespace std;

	Nec<int, double> x;
	Nec<pair<int, double>, pair<char, long>>y;
}
```
> Primary'den daha fazla parametreye sahip olan partia specialization

## Default Template Arguments

-  Dedik ki templatelerin parametreleri var. Ve bu template parametreleri karşılığı template argumentleri var.  Derleyici bir templateten bir specialization oluşturabilmesi için şüphesiz template argumentlarının ne olduğunu bilmesi gerekiyor. Template argumentlerinden ne olduğunun bilinmesi kaç yolda mümkündü?

1. Deduction yoluyla
2. explicit template argument kullanılmasıyla
3. Default template argument ile

### Template parametrelerinin varsayılan argüman alması

**Vector nasil bir sinif sablonu?**

```CPP
template <typename T, typename A = std::allocator<T>>
class Vector {

};
```
> vector boyle bir sinif sablonu. Aslında siz vektörün int açılımı dediğinizde (Vektörün int - allocator'ın int açılımı) demis oluyorsunuz.

```CPP
vector<int> vec;
Vector<int, allocator<int>> vec;
```
> ikisi de derleyici acisindan ayni anlamda.

**Allocator ne demek?**
- Allocator aslında bir kavram. Yani dinamik bellek ihtiyacının karşılanması ve kullanılması işlemlerini gerçekleştiren tür anlamında.
- Container'lar (STL'deki ya da 3. parti kütüphanelerdeki) coğunlukla dinamik bellek yönetimi kullanıyorlar.
**Yani dinamik bir dizi elemanlari nerede tutuyor?**
- Basitce heap te tutuyor diyebiliriz. Aslinda programın çalışma zamanında elde edilen bir bellek alanında tutuyor.
- Peki ya bir gömülü sistem için vektör sınıfını kullanmak istesek? Böyle olduğunda gömülü sistemde heap diye bir alan yok. Programın çalışma zamanında heap ten bir bellek alanı elde edemiyorum. Ama siz şimdi ilgili gömulü sistemde programın çalışma zamanında birbellek alanini kullanır kılan kendiniz bir kod yazabiliriz.
- Container dediğimiz sınıfların  bir allocator parametresi var. Şimdi siz eğer allocator parametresini kendiniz seçmezseniz standart kütüphanenin allocator'ı aslında New ve delete operatörlerini kullanıyor.
- Ama siz allocator'ın işlemlerinin böyle yapılmasını istemiyorsaniz, kendim ayrı bir allocator kullanacağım derseniz gidip bir allocator sınıfa oluşturup sizin sınıfınızın
 dinamik bellek yönetimi kodlarını o sınıfın kodları olarak seçme şansınız oluyor.
> new ve delete operatörlerinin ne zararı var? Bir zararı yok ama  bazı durumlarda
sizin daha etkili, daha efektif bir kod oluşması için verim kritik uygulamalarda ayrı bir allocator kullanmayı tercih edebiliyorsunuz.

- Standart kütüphanenin allocatoru herkese hizmet verecek şekilde yazılmış. Yani siz bin bitlik bir bellek alanı elde etmek isteseniz de 10 bitlik bellek alanı elde etmek isteseniz deaynı allocator kullanılıyor. Yani standart kütüphanenin allocatoru specific belirli bir ihtiyaç için değil.

**Ornek:**
- Biz programımızda sürekli bellek tahsisati yapacağız, dinamik bellek tahsisati. Ama bunu baştan biliyoruz. Bizim allocate edecegimiz bellek blokları hep 4 bit, 8 bit, 2 bit gibi küçük küçük değerler olacak. Simdi bu durumda standart kütüphanenin bu dinamik bellek yonetim sistemi bizim için büyük bir dezavantaj oluşturacak. Neden dezavantaj?

1. Her dinamik tahsaat için bir header kısmı olacak. Orası 8 bytesa sizin kodunuz 4 byte kullanırken orayı yöneten sistemde ilave bir 8 byte daha kullanilacak. Veri yapısına bir enter yapılmak zorunda o da onun da bir maliyeti var.

```CPP
std::set<int, std::less<int>, std::allocator<int>> myset;
```
> Boyle yazmak yerine --

```CPP
std::set<int> myset;
```
> Biz Zaten aradaki tempate argumanlarini istedigimiz icin boyle yaziyoruz. Boylece kalan template parametreleri icin default template argumanlari kullaniliyor.

```CPP
using namespace std;

template <typename Key, typename Comp, typename Alloc>
class Set {

};

int main()
{
	Set<int> myset;
}
```
> Boyle yazdigimda hata verecekti cunku ii+kinci ve ucuncu template parametreleri icin template argumani belirlemedim.

```CPP
using namespace std;

template <typename Key, typename Comp = std::less<Key>, typename Alloc = std::allocator<Key>>
class Set {

};

int main()
{
	Set<int> myset;
}
```
> Boylece set-int, less-int, allocator-int acilimi yapmis olduk. Hata vermedi.

**Not:** 
- C++ bir nesne yönelimli programlama dili değil . C++ dili multi-paradigm bir programlama dili ve birden fazla paradigmayı sizin iş birliği için de kullanmanıza olanak sağlayan araçlar var. 
- C++ data abstraction konusuna özellikle ağırlık vermiş bu özelliğini güçlendirmiş, ama bünyesinde barındırdığı araçlarla (başta nesne yönelimli programlama ve generic programlama olmak üzere) -(fonksiyonel programlama paradigması dahil)- paradigmaların iş birliği için de kullanılmasına olanak veren bir programlama dili o yüzden belki de ciddi bir alternatif yok.

**Dikkat:**
- Fonksiyon şablonlarının varsayılan argüman alması C++ 11 standartları ile eklendi. Daha oncesinde sadece sinif sablonlari varsayilan arguman alabiliyordu.

**Dikkat:** cout, cin, aslinda bunlar da birer sinif sablonlari. cout'un ait oldugu sinif basic_ostream.

```CPP
using namespace std;
basic_ostream<char, char_traits<char>>
```
> basic_ostream bizim sinif sablonumuzun turu. Iki template parametresi var. Birincisi akimdaki karakterlerin turu. Digeri karakterler uzerinde islemlerin nasil yapildigini belirleyen tur.
- Yani ostream sinifin ismi degil. Bir sinif sablonunun belirli tur argumanlariyla olusturulmus specialization'u olan bir sinifin tur es ismi. Sinif sablonunun ismi basic_ostream.

## Perfect Fowarding
- Perfekt forwarding aracın kendisi değil. Perfekt forwarding yapma olanağa sağlayan araçlar C++ 11 standartlarıyla dile eklendi.
- Bir fonksiyon olsun. Siz bu fonksiyonu aslında pekala kendiniz de çağırabilirsiniz. Fakat  öyle yerler var ki kutuphaneyi hazırlayan, bu fonksiyonu doğrudan çağırmanız yerine sizin bu fonksiyonu çağıran bir fonksiyonu çağırmanızı istiyor.

```CPP
using namespace std;

class Myclass {};

void func(Myclass&)
{
	std::cout << "L value ref.\n";
}

void func(const Myclass&)
{
	std::cout << "const L value ref.\n";
}

void func(Myclass&&)
{
	std::cout << "R value ref.\n";
}

int main()
{
	Myclass m;	//L value
	const Myclass c_m;	// const L value 
	
	func(m);
	func(c_m);
	func(Myclass{});
}
```
> Fonksiyonlari tek tek kendimiz cagirdik.

```CPP
using namespace std;

class Myclass {};

void func(Myclass&)
{
	std::cout << "L value ref.\n";
}

void func(const Myclass&)
{
	std::cout << "const L value ref.\n";
}

void func(Myclass&&)
{
	std::cout << "R value ref.\n";
}

int main()
{
	Myclass m;	//L value
	const Myclass c_m;	// const L value 
	
	func(m);
	//call_func(m);

	func(c_m);
	//call_func(c_m);

	func(Myclass{});
	//call_func(Myclass{});
}
```
> Burada call_func yazma ve implemente etme islemine "argumanlari func'a perfect foward etmek" deniyor. 

```CPP
template <typename T>
void call_func(T&&)
{
	func(std::forward<T>(x));
}
```
> Perfect fowarding uygulanmis bir fonksiyon.

```CPP
template<typename T, typename U, typename W>
void call_foo(T&& t, U&& u, W&& w)
{
	foo(std::forward<T>(t), std::forward<U>(u), std::forward<W>(w));

}
```
> call_foo 3 adet forwarding ref parametreye sahip.

### Variadic Template

```CPP
template<typename T>
template<typename T, typename U>
template<typename T, typename U, typename V>
```
> Kac tane template parametresi olmasini istiyorsak, template'i normalde ona gore olusturmak zorundayiz. Fakat variadic template araci bize tek bir template olusturarak, o template'in aslinda cok sayida parametreye sahip template ler olarak kullanilmasini sagliyor. Yani ortada tek bir template olacak ama o template'in parametre sayisi biz ne istersek o  olacak. Iste bunu saglayan arac varidadic template.

```CPP
//template parametre paketi, template type parameter pack
template <typename ...Args>
```
> Bu pakette birden fazla template parametresi var demek.

```CPP
template <typename ...Args>
void func(Args... params)
{

}

//void func();
//void func(int);
//void func(int, double);
//void func(int,double, const char*);

int main()
{
	func();
	func(1);
	func(1, 2.3);
	func(1, 2.3, "alican");
}
```
> Burada fonksiyonun parametrelerinin ne oldugunu derleyici, template argument deduction ile anladi. Derleyici asagida cagirilan fonksiyonlara gore ortadaki fonksiyonlari birer birer kendisi tanimladi. Args (Template parametre paketi) ismi Args olmak zorunda degil. Ama uygulamalarda iki tane  identifier ismi cok sik kullaniliyor. 

> Params = function parameter pack

> Args = Template parameter pack

```CPP
template <typename T, typename U, typename ...Args>
```
> 1 tane parametre paketi olmak zorunda.

# Ders 30

```CPP
template <typename ...Ts>
void func(Ts& ...args)

void func(const int& p1, const double& p2)
{

}

int main()
{
	int x = 324;
	double dval{ 56.24 };

	func(x, dval);
}
```
> Asagidaki cagriya gore bize derleyici ortadaki fonksiyonu yazdi.

### Pack Expansion

- Parametre paketindeki parametrelerin bir kalıba uygun olarak bir kalıba uygun olarak virgülerle ayrılan listeye dönüştürülmesi.
- Yani biz bir parametre paketini ya da fonksiyon parametre paketini ya da templet parametre paketini expand ettiğimizde ya da genişlettiğimizde Virgülerle ayrılan bir liste oluşturuyoruz templetin içinde.

**Ornek:**
```CPP
template<typename ...TS>
class Var
{

};

template <typename ...Types>
class Myclass : public Var<Types...> {
public:
	constexpr static size_t size = sizeof...(Types);
};

int main()
{
	constexpr auto n = Myclass<int, double>::size;
}
```
> Burada dikkat ederseniz ismi Michael'a olan sınıf kalıtım yoluyla var sınıfının bir açılımından elde edilmiş. Şimdi eğer ben Myclass'in  int - double açılımını oluşturursam parametre paketinde iki tane tür olacak. Ve burada da pack expansion yapıldığı için, Var'in int double açılımından elde edilmiş olacak. Myclass'in int - double açılımı aslında Var'ın int - double açılımından kalıtım yoluyla elde edilecek .Bu pack expansion ile basariliyor. (<Types...>)

```CPP
template<typename ...TS>
class Var
{
public:
	Var()
	{
		std::cout typeid(Var).name() << '\n';
	}

};

template <typename ...Types>
class Myclass : public Var<Types*...> {};

int main()
{
	Myclass<int, double, long> x;
}
```
> Var'in, int* - doublr*, long* acilimindan elde edilecek.

**Ornek:**

```CPP
#include <tuple>

template<class A, class B, class... TS>
void func(A arg1, B arg2, TS ...pack)
{
	std::tuple<A, B, TS...> t1;
	//std::tuple<TS..., A, B> t2;
	//std::tuple<A, TS..., B> t3;
}
int main()
{
	func(1, 4.5, 'C', 4.5f, 4L);
}
```
> Bu fonksiyon vagrisinda derleyicinin yazdigi kodda olusturulan tur, tuple'in A,B, parametre paketindeki turlerin acilimi olacak.

```CPP
template <typename ...Ts>
void func(Ts ...args)
{
	foo(args...)
	bar(args)...
	baz(bar(args)...)
}
```
> Nasil uretilecek?

```CPP
foo(p1, p2, p3);
bar(p1), bar(p2), bar(p3);
baz(bar(p1), bar(p2), bar(p3));
```

**Ornek**

```CPP
template <typename ...Ts>
void func(Ts ...args)
{
	{args...}
}
```
> Boyle yazdigimda derleyicinin yazdirdigi fonksiyonun parametrelerinin isimlerini yaziyoruz.

```CPP
template <typename ...Ts>
void func(Ts ...args)
{
	int a[] = { args... };
	//int a[] = { p1,p2,p3 };
}
```
> Bu da ayni anlmaa geliyor.

## STL (Standart Template Library)

- STL != C++ standart kutuphanesi
- Fakat genel olarak ayni anlamda kullaniliyor.
- Kisaca anlami: C++ standart kutuphanesindeki generic ogelerin olusturdugu kume
- STL nesne yonelimli programlama paradigmasina uygun ya da o paradigmayi implemente eden bir kutuphane degil. (Nesne yonelimli programlamanin bazi ozelliklerinden faydalaniyor fakat ozellikle runtime polimorfizmini cok kisitli olarak kullaniyor.) (Kalitim da kullaniliyor fakat statik olarak, compile time'a yonelik olarak kullaniliyor.)
- C#, java gibi dillerde en ufak bir hata, exception gonderilmesine sebep oluyor fakat STL efficiency odakli bir kutuphane oldugu icin hemen her yerde exception throw edilmiyor. Exception handling'ten ziyade sorumluluk programciya birakiliyor. En ufak bir hata exception gonderilmesi yerine tanimsiz davranis olusturuyor.
- Hata mesajlari cok uzun olabiliyor.

**Bircok STL bileseni var:**

![image](https://user-images.githubusercontent.com/75746171/223106402-f79c3774-8eb4-4eac-bcca-f9b0e3da8327.png)

**STL standart container siniflari:**
![image](https://user-images.githubusercontent.com/75746171/223107072-a3afd7f2-0f34-4c79-8880-ff00a38edbcb.png)

**Vector:** Dinamik dizi sinifi, veri yapilari ihtiyacinin cogunu karsiliyor.

**Deque:** Dinamik dizilerin dizisi.

**List:** Cifte bagli liste sinifi

**Forward_list:** Teke bagli liste sinifi

**Array:** C dizilerini sarmalayan bir container sinifi. Bircok durumda C'deki dizileri kullanmak yerine, onlari sarmalayan bu sinifi kullaniyoruz.

**string:** Yazi tutma amacli.

**Associative Containers:** Ikili arama agaclari. Hepsinin ortak ozelligi: Bir anahtar ile arama yapiyorum ve o key'in olup olmadigini sorguluyorum. Mevcut ise ona erisiyorum. 

**Iterators**
- Pointerlarin daha soyutlanmis bicimi.

- Bagli liste veri yapisinda ogeler bellekte ardisik degil. Ogeler dugumlerin icinde tutuluyor. Dugum, veri yapisinda tutulacak degerler ile implementasyon tarafinda kullanilacak pointerlari bir arada tutan nesneler. Yani bagli listenin ilk dugumunun icindeki pointer, bir sonraki ogeyi tutaun dugumu gosterebiliyor. 
- Pointer yerine, pointer gibi davranan bir sinif olsaydi ve pointerlar yerine boyle siniflar turunden nesneleri kullaniyor olsaydik bu durumda operator overloading mekanizmasindan faydalanarak ++p yaptigimizda calistirilacak kod o pointerin degerini bir sonraki  ogeyi tutaun dugumun icindeki nesnenin adresi haline getirebilirdi. Veri yapisini en oldugundan bagimmsiz olarak p'nin bir sonraki ogeyi gostermesini saglayabiliriz. 
- Yani pointer yerine generic programlama araclarindan faydalanarak yeni bir kavram  yaratmis oluyoruz. Bir iterator oyle bir varlik ki, belirli interface'deki operasyonlari destekliyor. ++ operatorunun operandi oldugunda veri yapisindan tutulan bir sonraki ogenin konumunu tutuyor.
- Iteratorler fonksiyon parametreleri yapildiginda, containerlar ustunde genellestirilmis islem yapan fonksiyon sablonlarinin olusturulmasini sagliyorlar. Bunlara da algoritma deniyor. (ornegin sort algorimasi, copy algoritmasi)

**Kisaca algoritmalar:** Tipik olarak parametreleri iterator olan ve bu sayede bir container'in bazi islemlerinin yapilmasini saglayan fonksiyon sablonlari. Yani containerlar sinif sablonlari, iteratorlar, tipik olarak sinif sablonlari, algoritmalar ise sinif sablonlari. 

# Ders 31

- Bütün STL iteratörleri ya da üçüncü parti kütüphanelerdeki iteratörler, ortak bir interface'e sahip ama tamamen aynı da değil. Iteratörlerin kategori dediğimiz bir özelliği var. Bir iteratörün hangi operasyona destek verdiği, hangi operasyonu sağladığı
ve tabii ki hangi operasyonu sağlamadığı o iteratörün kategorisine bağlı.

**Iterator Categories:**
1. input iterator
2. output iterator
3. forward iterator
4. bidirectional iterator
5. random access iterator

- Aşağı doğru indikçe yetenek artıyor. (3. sıradaki, 1 ve 2 yi kapsıyor). Yani forward iterator kategorisindeki bir iterator ile hem input iterator interface'indeki operasyonları hem de output iterator kategorisindeki operasyonları gerçekleştirebilirim. Bir iterator bu kategorilerden birine ilişkin olmak zorunda. 

![image](https://user-images.githubusercontent.com/75746171/223234748-7f57a3ba-ccf8-42d5-bb01-630c212c2b99.png)

> Containerların içinde begin ismi geçen fonksiyonları containerdaki ilk ögenin konumunu veriyor.

> Containerların end fonksiyonu son ögenin değil, bir sonraki (olmayan) ögenin konumunu tutuyor(Sentinel). Yani endin geri dönüş değeri olan konum erişim yapmamız için değil. Zaten bu end fonksiyonun geri dönüş değeri olan iteratörü dereference edersek tanımsız davranış.

- Biz begin fonksiyonunu çağırıp ilk ögenin konumunu alıp, end fonksiyonunun geri dönüş değeri olan konumla karşılaştırıyoruz. Bu değer End'in geri dönüş değeri olan bir iteratör konumuna eşit ise artık konteynerde başka öge olmadığını, bütün ögeleri ziyaret ettiğimizi anlıyoruz.

**Random Access Iterator:** C'deki raw pointer'ların ham pointer'ların yapabildiği her şeyi yapıyor.

![image](https://user-images.githubusercontent.com/75746171/223237293-5e8c3d25-1c7d-46eb-ab08-8e0a7e863876.png)

**Şu sınıfların iteratörleri Random Access Iterator:** (Yani her şeyi yapmaya muktedir)
> Vector, deque, string, array, C Dizileri

> Pointerları nasıl kullanabiliyorsak bunlar da aynı şekil kuulanabiliyoruz.

**Şu sınıfların iteratörleri Bidirectional Iterator kategorisinde:**
> List, set / multiset, map / multimap

> Yani örneğin list'in iteratörü ile bir tam sayıyı toplayamam.

**Örnek:**
```CPP
#include <list>

int main()
{
	using namespace std;

	list<int> mylist(100);
	auto iter1 = mylist.begin();
	auto iter2 = mylist.begin();

	++iter1;
	auto b = iter1 == iter2;
	b = iter1 != iter2;
	--iter1;
	//Buraya kadar hatasız.

	auto x = iter1 + 3; // Burada hata var. 
	// Bunu sadece random access iterator yapabilir.
	iter1 > iter2; //Bu da hata
}
```
**Diğer bir örnek:**

```CPP
#include <forward_list>


int main()
{
	using namespace std;

	forward_list<int> mylist(100);
	auto iter1 = mylist.begin();
	auto iter2 = mylist.begin();

	++iter1; //Hatasız
	--iter1; //Hatalı
}
```

**Bir iteratörün kategorisini nasıl öğrenebiliriz?** (Yani fiilen kodda bunu nasıl tespit edebilirim?)
- İtoratör olan türlerin bazı nested type'leri var. Bu nested type'ları kullanarak özellikleri hakkında compile time'da bilgi edinebiliyoruz.

```CPP
iter_t::iterator_category
```
> Her iteratör türünün "iterator_category" nested type'ı, iteratörün kategorisini bildiriyor. (STL'de tanımlanan bazı empty class'lar iterator_category'i temsil ediyor.) Nedir bu empty class'lar? (Empty class'lar derleme zamanında bilgi edinme konusunda kullanılan temel araçlardan biri.)

```CPP
struct intput_iterator_tag{};
struct output_iterator_tag {};
struct forward_iterator_tag {};
struct bidirectional_iterator_tag {};
struct random_access_iterator_tag {};
```

**Örnek:**

```CPP
using iter_t = std::vector<int>::iterator;

int main()
{
	using namespace std;
	cout << typeid(iter_t::iterator_category).name() << '\n';
}
```
> Çıktıda türünü derleme zamanında görmüş olduk.

**İterator kategorisi neden önemli?**

### std::copy
- Bir range'deki ögeleri başka bir range'e kopyalıyor. 
- Bir bağlı listede bulunan ögeleri bir dinamik diziye kopyalamak istiyoruz. Bu C dilinde standart kütüphaneler ile mümkün değil. Ama std::copy ile faklı containerlar arasında işlemler yapabiliyoruz.

**Örnekler:** sdt::copy
- Bir int dizideki ögeleri başka bir int diziye kopyalayabilirim.
- Bir oyun programındaki fighter sınıfı türünden nesneler bir vektörde tutuluyor. Bu nesneleri ben bağlı listeye taşımak istiyorum. Bu da sdt::copy ile mümkün. İşte bu generic programlama, türden bağımsız. Yani 2-3 satırlık copy algoritması kodu ile (derleyicinin ürettiği gerçek fonksiyon ile) bir veri yapısında tutulduğu sürece her çeşit kopyalamayı yapabiliyoruz.

**Not:** Belirli bir range'e yazan algoritmalar (copy) en son yazdıkları konumdan sonraki konumu döndürürler. Çünkü fonksiyonu çağıran yazılmış range'i kullanabilsin diye.

**Örnek:**
```CPP
#include <iostream>
#include <algorithm>

template <typename InIter, typename OutIter>
OutIter Copy(InIter beg, InIter end, OutIter destbag)
{
	while (beg != end) {
		*destbeg++ = *beg++;
	}
	return destbag;
}

int main()
{
	int a[10] = { 1,2,4,6,7,3,7,23,5,19 };
	int b[10];

	Copy(a, a + 10, b);
}
```

## Arama Algoritmaları

- C'de arama fonksiyonları tipik olarak adres döndürür aranan değer bulunamazsa null pointer döndürür. String sınıfının arama fonksiyonları indeks döndürür. (std sizet). Başarısız ise string'in npos'u döndürüyor.
- STL'deki arama algoritmaları ise iterator döndürüyor. Bulursa ögenin konumunu, bulamazsa range'in end iteratörünün döndürüyor.

**Örnek:**
```CPP
template <typename InIter, typename T>
InIter Find(InIter beg, InIter end, const T& val)
{
	while (beg != end) {
		if (*beg == val)
		{
			return beg;
		}
		++beg;
	}
	return end;
}
```

**Predicate**

- bool döndüren bir callable.

**Unary predicate:** 1 tane parametreye sahip.
**Binary predicate:** 

STL algoritmmalarından bazıları bizden bir predicate istiyor. Örneğin sonu if ile biten algoritmalar.

### find if 
- Bir range de tutulan ögelerden belirli bir koşulu sağlayan ilk ögenin konumunu döndürüyor. Başarısızlıkta range'in end konumunu döndürecek. Kendim iz örnek olarak yazalım.

```CPP
template <typename InIter, typename Pred>
InIter FindIf(InIter first, InIter last, Pred f)
{
	while (first != last) {
		if (f(*first))
		{
			return first;
		}
		++first;
	}
	return last;
}
```

# Ders 32

- Lambda ifadelerini bir algoritmaya argüman olarak gönderiyoruz. Böylece bir callable göndermiş olduk. Algoritma aldığı callable'ı bir ya da birden fazla yerde çağırıyor.

### Reverse iterator

```CPP
	ivec.begin();	// geri dönüş değeri iterator
	ivec.rbegin();	// Geri dönüş değeri reverse iterator
```

**Örnek:**

```CPP
using namespace std;

int main()
{
	vector<int> x;

	cout << typeid(x.begin()).name() << "\n";
	cout << typeid(x.rbegin()).name() << "\n";
}
```
- Çıktı:

```CPP
class std::_Vector_iterator<class std::_Vector_val<struct std::_Simple_types<int> > >
class std::reverse_iterator<class std::_Vector_iterator<class std::_Vector_val<struct std::_Simple_types<int> > > >
```

![image](https://user-images.githubusercontent.com/75746171/223683460-bdf1b2a4-6b25-4de4-9520-1b05c7aa56af.png)

> Normalde iterator böyle çalışıyor. Bgini lk ögenin, end sonuncudan sonrakinin konumunu veriyor. Ama reverse iterator öbyl değil.

![image](https://user-images.githubusercontent.com/75746171/223683678-ee043d88-f656-460b-9e05-6f0f74462624.png)

> rbegin fonksiyonu fiziksel olrak end konumunu tutuyor. Fakat onu dereference ettiğimizde kendi konumundan bir ömnceki konumunu dereferecne ediyor. 

```CPP
template <typename Iter>
void Print(Iter beg, Iter end)
{
	while (beg != end)
		std::cout << *beg++ << " ";
	std::cout << "\n---------------------------\n";
}

**Örnek:**

int main()
{
template <typename Iter>
void Print(Iter beg, Iter end)
{
	while (beg != end)
		std::cout << *beg++ << " ";
	std::cout << "\n---------------------------\n";
}

int main()
{
	using namespace std;

	vector<int> ivec{ 12,56,89,3,57 };
	Print(ivec.begin(), ivec.end());

	auto riter = ivec.rbegin(); 
	// Bu iter içinde bir iterator tutuyor.
	// Aslında bu end konumunu tutuyor.
	// Ben bunu dereferece ettiğimde aslında bir önceki konunumu dereference ediyor.
	// Böylece contaienrdaki son ögeye erişmiş oluyoruz.

	cout << *riter << "\n";
	++riter; // Burada çalışan kod sarmaladığı iteratorün -- operatörünü kullanıyor.
	cout << *riter << "\n";
	// çıktı olarak bir önceki ögeyi görüyoruz

	// riter = ivec.rend(); 
	// Bu da aslında ilk ögenin konumunu tutuyor.
	// Ama ben bunu dereferece etsem tanımsız davranış olacak.
}
```
- O zaman ++ operator fonksiyonu reverse için, sarmaladığı iteratörün -- fonksiyonunu çağırdığına göre, reverse iterator olması için en az bidirectional iterator olması gerekir.
- Reverse iteratorun base isimli bir fonksiyonu var. Sarmaladığı iteratörü döndürüyor. 

```CPP
template <typename Iter>
void Print(Iter beg, Iter end)
{
	while (beg != end)
		std::cout << *beg++ << " ";
	std::cout << "\n---------------------------\n";
}

int main()
{
	using namespace std;

	vector<int> ivec{ 12,56,89,3,57 };

	auto iter = ivec.rend().base();
	cout << *iter << "\n";
}
```
> Bu durumda iter'in türü reverse iterator değil, normal iterator. Ve aslında beg'in konumunu tutuyor. Çalıştırıınca vectordeki ilk ögetye erişmiş olacam.

```CPP
template <typename Iter>
void Print(Iter beg, Iter end)
{
	while (beg != end)
		std::cout << *beg++ << " ";
	std::cout << "\n---------------------------\n";
}

int main()
{
	using namespace std;

	vector<int> ivec{ 12,56,89,3,57 };

	auto beg = ivec.rbegin();
	auto end = ivec.rend();

	// beg end
	Print(beg, end);
	Print(end.base(), beg.base());
}
```
> Elinmizde bir iterator range varsa bu iteratorlerin yerini değiştirin. Ama iteratörün kendisini değil de base fonsiyonunun geri dönüş değerinı kullanın. Bu durumda ayın range'in baştan sona halini kullanmış olacaksınız.

- Advance Fonmksiyonu
- Next fonksiyonu
- Pre fopnksiyonu
- swap fonk. 

## Lambda Expresions (Lambda Funcitons)

- Modern C++ ile dile eklendi.
- C++'ta nested fonksiyon yok ama lambda ifadeleri bunu dolaylı olarak yapılmasını sağlıyor. Yani lambda ifadeleriyle biz aslında bir fonksiyon içinde çağırabileceğimiz bir fonksiyon kullanabiliyoruz.

```CPP
int main()
{
	[]() {}();
}
```
> Minimal bir lambda ifadesi. 
- Bir lambda ifadesi, derleyicinin bir sınıf kodu yazmasını ve ifadenin kendisini de o sınıf türünden geçici bir nesneye dönüştürülmesini sağlıyor.
- () : Derleyiciye yazdırdığımız sınıfınfonksiyon çağrı operatörünün parametre parantezi. İçini boş bırakırsak, derleyiciye yaszdırmak istediğimiz sınıfın fonksiyon çağrı operatör fonksiyonunu parametresinin olmaması demek.

# Ders 33

```CPP
		[](int x, int y)mutable{}	// Uye fonksiyon  non-const olsun
		[](int x, int y)noexcept {}	// bu exception throw etnmmiyor anlamında
		[](int x, int y)constexpr {}	// constexpr olamsını engelleyen bir durumda hata verecek
		[](int x, int y)->int {}	// return ifadesini belirtmek
```
> Bu bir veya birden fazlası olabilir.

**Kullanım biçimleri:**

```CPP
int main()
{
	using namespace std;

		//auto f = [](int x) {return x * x; };
		//auto f([](int x) {return x * x; });
		auto f{ [](int x) {return x * x; } };

		cout << f(12) << '\n';
}
```

- Lambda expressinolar aynı olursa:
```CPP
int main()
{
	using namespace std;

	auto f1 = [](int x) {
		return x * x;
	};

	auto f2 = [](int x) {
		return x * x;
	};
}
```
> f1 ve f2 kesinlikle farklı türler.

**Transform Algorithm** -- Tekrar et

- Lambda ifadeleri en çok kullanıldığı yerler fonksiyon şablonlarına argüman olarak gönderilmesi.
- 2. olarak lambda ifadesinin bulunduğu yerde fonksiyonu çağırmak.


```CPP
class xyz {
public:
	xyz(int a) : x(a) {}
	void foo()
	{
		//
	}
private:
	int x;
};


int main()
{
	int a = 10;
}
```
> Yazdığımız constructor ile sınbıfın veri elemanını constructor a gelen değer ile init ettik. Yani xyz sınbıfından oluşturulan nesnenin foo fonksiyıonu çağırıldığında, foo x'i kullanıdğında aslında a'nın değerini kullanmış oluyoruz. 

> Ve aslında derleyiciye böyle bir kod yazırabiliriz. Bunu yapabilmek için lambda ifadesinde captura close kullanılıyoruz.

```CPP
int main()
{
	int a = 10;

	[a] //Derleyici benim için yazacağı sınıfa 
	// a değişkeninin türünden bir veri elemanı eklyecek. 
	// Ve o veri elemanını benim sınıfımda yazacağın cosnturtor ile init et.
}
```

**Örnek:**
```CPP
using namespace std;

int main()
{
	int a = 10;

	auto f = [a](int x) {
		a *= x;
	};
}
```
> a sentaks hatası verdi. Neden? Yazılan kodda fonksiyonun const üye fonksiyon olması.  Derleyici nasıl bir kod yazdı?

```CPP
using namespace std;

class comp_gnt {
public:
	comp_gnt(int a) : m_a(a) {}
	void operator()(int x) const
	{
		m_a *= x;
	}
private:
	int m_a;
};
```
> yani const olan private içindeki m_a değil. cosnt olan, üye fonksiyon. Üye fonksiyoınun const olmaması için lambda ifadesinde mutable kullanmamız gerekiyor.

```CPP
int main()
{
	int a = 10;

	auto f = [a](int x)mutable {
		a *= x;
	};
}
```

**Örnek:**

```CPP
int main()
{
	auto eng = mt19937{};

	auto f = [eng]() {
		eng.discard(12);
	};
}
```
> Sentaks hatası. Derleyicinin yazıdğı sınıfta, derleyici sınıfa veri elemanı olarak mt19937 nesnesini koydu. Ama derleyicinin yazdığı fonksiyon, cosnt üye fonksiyon. Const üye fonksiyon, elemanlarının const olmayan üye fonksiyonlarını çağıramaz. Buradaki discard, non-cost üye fonksiyon oldğu içiçn sentaks hatası oldu.

```CPP
template <typename T>
void func(T t)
{
	//
}

int main()
{
	func([](int x) {return x + 5; });
	// Böyle çağırırsam fonksiyonun parametre değişkeni türü closure type
	func(+[](int x) {return x + 5; });
	// Böyle çağırırsam fonksiyonun parametre değişkeni türü function pointer
}
```

- Positive lambda
- capture clause
- iife idiom
- overload reloltion
- generalized lambda expression


## STL Containers
- Verileri bir arada tutulup işlenmesini sağlayan düzenekler. Bu iş için oluşturulan sınıflara container sınıfları deniyor.
- Bu containerların varlık nedeni bir değer ile bir ögeye erişmek.

- Sequence Containers:

> std::vector

> std::deque

> std::list : Çifte bağlı liste

> std::forward_list : Tek bağlı liste

> std::string

> std::array : C dizilerini sarmalamak

- Associative Containers:

> std::set : Anahtarın kendisini tutuyor

> std::multiset

> std::map : Anahtar ile ilişkilendirilmiş bir değeri tutuyor.

> std::multimap : Aynı anahtardan birden fazla olabilir.

- Unordered Associative Containers:

> set::unordered_set

> set::unordered_multiset

> set::unordered_map

> set::unordered_multimap

- Container Adapters:

> std::stack

> std::queue

> std::priority_queue

**Notlar:**
- Günümüzdeki birlghisayar sistmeleri için maliyeti en fazla etkileyen mekanizma önbellek mekanizması. Bir veriyi kullanmak istiyoruz ve bu veri kullanmak istediğimiz anda zaten önbelleğe alınmış durumdaysa ona erişme maliyeti düşük. Ama cache'te değilse ona bellekten erişmek gerekiyor ve bunun maliyeti çok daha yüksek.
- Veri yapısındaki ögeyi kullanmöak sitediğimizde bu zaten önbellekte ise buna cache hit deniyor, değilse cache miss.  

# Ders 34

- Containerlar programın çalışma zamanında (array hariç) öge sayısı değişebilen yapıalr.

**Ekleme işlemi naısl yapılıyor?**

- Referans semantiği ile değil. Taşınacak ögenin bir kopyası çıkartılıp kopyası koyuluyor. Falat referans semantiğini kullanma yolları da var.

## std::vector

```CPP
int main()
{

	std::vector<int> ivec;
	std::cout << "ivec.size() = " << ivec.size() << "\n";
	std::cout << std::boolalpha;

	std::cout << ivec.empty() << "\n";
}
```
> Default init. Boş bir vector oluştu.

```CPP
int main()
{

	std::vector<int> ivec(10);
	std::cout << "ivec.size() = " << ivec.size() << "\n";

	std::cout << ivec.empty() << "\n";
}
```
> 10 tane öge ile başlaacak. Bunlar çöp değer değiller. Value init ediliyor. Hepsinin değeri sıfır.

```CPP
int main()
{
	using namespace std;

	initializer_list<int> x{ 1,4,6,7,9 };

	std::cout << "sizeof(x) = " << sizeof(x) << "\n";
}
```
> sizeof(x) çıktısı olarak 8 aldık. Bu nasıl oldu?

> initializer lsito luşturduğunuzda aslında derleyici bir dizi oluşturuyor. 

![image](https://user-images.githubusercontent.com/75746171/223967055-04f9317a-8ade-4b16-a467-770df3fdbb94.png)

- Bu initializer list ile o range'e erişebiliyorum. 
- Yani bir initiazlier list kopyalanarak başka bir initilazier list oluşturulursa, dize diziyle herhangi bir alakalsı yok.

```CPP
int main()
{
	using namespace std;

	initializer_list<int> x{ 1,4,6,7,9 };
	auto y = x;

	cout << boolalpha << (x.begin() == y.begin()) << '\n';
}
```
> true döndü. 

```CPP
	auto x = { 1 }; // çıakrım initializer list olarak yapıldı
	auto x{ 1 };	// çıkarım int olarak yapıldı
```

**resize fonksiyonu**
**pushback fonksiyonu**
**assign fonk.**

**Bir container'ın insert fonksiyonu nasıl çalışıyor?**
- insert fonksiyonlarından bir parametre daime iterator. ve bu ilk parametre. 

![image](https://user-images.githubusercontent.com/75746171/224298838-3a8a7f75-82eb-419c-bf77-b79b5180aa82.png)

> x nesnesi b'ye insert edilirse a ve be arasına giriyor. 

- insert fonksiyonundaki diğer parametreler, insert işleminin farklı şekilde yapılmasını sağlayan overload lar oluşturacak.
```CPP
int main()
{
	using namespace std;
	vector<string> svec{ "ali", "selim", "murat", "serhat" };

	print(svec);
	svec.insert(svec.begin() + 2, "nihal");
	print(svec);
}
```

























