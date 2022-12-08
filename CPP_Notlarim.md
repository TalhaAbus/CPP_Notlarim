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





















































