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




