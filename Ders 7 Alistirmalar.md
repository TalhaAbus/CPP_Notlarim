# Ders 7 Alıştırmalar

**Soru 1: İncele**

```CPP
#include <iostream>
#include <cstdint>


void func(int *)
{
    std::cout << "int *\n";
}

void func(const int *)
{
    std::cout << "const int *\n";
}

int main()
{
    const int cx = 5;
    func(&cx);
}
```
**Cevap:**
> Burada eğer 2. fonksiyon olmasaydı bu çağrı legal olmazdı.

> Eğer gödnerdiğimiz nesne const t* derğil de t* olsaydı, fonksiyonlardan herhangi biri tek başına olsaydı kod her türlü legal olcaktı. Çünkü int* dan const int* a tür dönüşümü var.

> Bunun faydası, const olan nesneler ve const olmayan nesneler için 2 ayrı kod oluşturup compile time'da derleyicinin bu seçimi yapmasını sağlayacağız.

**Soru 2: Function overloading var mıdır?**

```CPP
#include <iostream>

int foo(int);

int main()
{
	int foo(double);
}
```
**Cevap:**
> Function overloading yok çünkü blockscope'ları farklı. Burada namehiding olur.

**Soru 3: Function overloading var mıdır?**

```CPP
#include <iostream>

int foo(int);
double foo(int);
int main()
{
	
}
```
**Cevap:**
> Function overloading yok, aynı zamanda bu kod dilin kurallarına aykırı.Bir fonksiyon yeniden bildirilmiş ve geri dönüş değeri farklı.

**Soru 3: Function overloading var mıdır?**

```CPP
#include <iostream>

int foo(int);
int foo(int,int);
int main()
{
	
}
```
**Cevap:**
> Overloading var. Scopeları aynı imzaları ayrı. 

**Soru 4: Function overloading var mıdır?**

```CPP
#include <iostream>

int foo(int);
int foo(const int);
int main()
{
	
}
```
**Cevap:**
> Overloading yok. Parametrenin kendisinin const olması bir imza farklılığı kabul edilmiyor. Bu bir redecleration. Derleyici gözüyle alttaki bildirim üstteki fonskiyonun bildiriminin tekrarı.

> Eğer aynı fonksiyon 2 kez tanımlanırsa sentaks hatası olur. Eğer overloading ise derleyici aynı kaynak dosyada farklı fonksiyon tanımı olamsını kabul eder. Eğer overloading yok ise derleyici hata verir.

> Burada sentaks hatası da yok, function redecleration var. 

**Soru 5: Function overloading var mıdır?**

```CPP
#include <iostream>

int foo(int);
int foo(const int);
int main()
{
	
}
```
**Cevap:**
> Function Overloading var. Buradaki parametreler farklı türdeler. Bu şekilde yapılan overloadinge "const overloading deniliyor".

**Soru 6: Function overloading var mıdır?**

```CPP
#include <iostream>

void f(double* const p);
void f(double* p);
int main()
{
	
}
```
**Cevap:**
> Overloading değil. Redecleration var. Önceki örnekteki low level const fakat burada top level const var. Doalyısıyla parametre değişkeninin kendisinin constluğu imza farkı yaratmaz.


**Soru 7: Function overloading var mıdır?**

```CPP
#include <iostream>

void func(int&);
void func(cont int&);
int main()
{
	
}
```
**Cevap:**
> Overloading var. Önceki örneklerdeki pointer semantiği yerine referans semantiği kullanılmış. 
> Standart kütüphanenin en sık kullandığı overloading yapılarından biri.

**Soru 8: Function overloading var mıdır?**

```CPP
typedef double flt_type;

void f(double);
void f(flt_type);

int main()
{

}
```
**Cevap:**
> Overloading değil. Typedef farklı bir tür anlamına gelmiyor. Sentaks hatasıda yok. Redecleration var.

**Soru 9: Kaç adet fucntion overloading var?**

```CPP
void f(char);
void f(signed char);
void f(unsigned char);

int main()
{

}

```
**Cevap:**
> 3 adet. Char türü implementation defined. İşaretli de olabilir, işaretsiz de olabilir. Ama tür sistemi içinde bunlar farklı türler.


**Soru 10: Kaç adet fucntion overloading var?**

```CPP
void f(int *);
void f(int **);
void f(int ***);

int main()
{

}
```
**Cevap:**
> 3 adet. Hepsi ayrı türler.

**Soru 11: Function overloading var mıdır?**

```CPP
void f(int &);
void f(int &&);

int main()
{

}

```
**Cevap:**
> Evet. Birinin parametresi sol taraf referansı, diğerinin sağ taraf referansı.

**Soru 12: Kaç adet fucntion overloading var?**

```CPP
void f(int &);
void f(const int &);
void f(int &&);

int main()
{

}
```
**Cevap:**
> 3 adet.

**Soru 13: Function overloading var mıdır?**

```CPP
void f(std::int32_t);
void f(int);

int main()
{

}
```
**Cevap:**
> Derleyiciye bağlı. Implementation defined. int32_t türü bir türe verilen eş ismi. Başka bir derleyicide bu eş isim farklı bir türe ait eş isim ise burada overloading vardır.

**Soru 14: Kaç adet overload var**

```CPP
void foo(int p[]);
void foo(int p[20]);
void foo(int *p);

int main()
{

}
```
**Cevap:**
> 1 adet overload var. Bunların hepsi aynı bildirim. Burada array decay var. Fonksiyonun parametresi pointerdır. Hepsinin türü int* 

**Soru 14: Overloading mi redecleration mı?**

```CPP
void foo(int (int));
void foo(int(*)(int));

int main()
{
    
}
```
**Cevap:**
> Redecleration var. Aşağıdaki tür yukarıdaki türden bir fonksiyonun adresi olan bir tür.

> Üstteki "function type", alttaki "function pointer type". 

```CPP
(int (int))     // function type
(int(*)(int)    // function pointer type
```

> Yani fonksiyonun parametre türü bir fonksiyon türü olamaz.

**Soru 15: Kaç adet overload var?**

```CPP
void foo(int (*)[5]);
void foo(int (*)[6]);
void foo(int (*)[7]);
void foo(int (*)[8]);


int main()
{
    
}
```
**Cevap:**
> 4 adet. Birisi 5 elemanlı dizi pointerı türü, diğeri 6 elemanlı dizi pointerı türü.

**Soru 16: Bu iki fonksiyon viable mı?**

```CPP
void func(double *);

int main()
{
    func(2);
}
```
**Cevap:**
> Viable değil. int türünden pointer türüne dönüşüm yok.

**Soru 17: Bu iki fonksiyon viable mı?**

```CPP
void func(double *);

int main()
{
    func(0);
}
```
**Cevap:**
> Viable. Null pointer convertion var. Tam sayı sabiti 0 null pointer a dönüşecek.

**Soru 18: Kod geçerli midir?**

```CPP
void func(bool);

int main()
{
    int x{};
	func(&x);
}
```
**Cevap:**
> Evet. Bu tür doğrudan pointer türü. Pointer türlerinden bool türüne dönüşüm var ne null pointer ise false, null deilse true yapılcak.

**Soru 19: Kod geçerli midir?**

```CPP
void func(void *);

int main()
{
    int x{};
	double f{};

	func(&x);
	func(&f);
}
```
**Cevap:**
> İkisi de geçerli. Çünkü void* türüne dönüşüm var.

**Soru 20: Kod geçerli midir?**

```CPP
void func(char *);

int main()
{
    func("talha abus");
}
```
**Cevap:**
> Geçersiz kod. Çünkü string literali const char* türüne decay olacak ma fonksiyonun parametresi char*

**Soru 21: Kod geçerli midir?**

```CPP
enum pos {on, off, hold};
enum class color{yellow, deak_blue};

void f(pos);
void g(color);

int main()
{
    f(1);
	f(2);
}
```
**Cevap:**
> Geçersiz kod. Aritmetik türlerden enum türlerine dönüşüm yok. 

**Soru 22: Kod geçerli midir?**

```CPP
enum pos {on, off, hold};
enum class color{yellow, deak_blue};

void f(int);

int main()
{
    f(color::yellow);
	f(off);
}
```
**Cevap:**
> 2 çağrı geçerli. ilk çağrı geçersiz. scoped enum enumeratorlerinden int türüne dönüşüm yok.

> Hata kodu: "class türündeki bağımsız değişken int türü parametre ile uyumsuz"

**Soru 23:**

```CPP
void f(int *);
void f(int, int);
void f(int);
void f(double);

int main()
{
	double d{};
	f(&d);
}
```
**Cevap:**
> Alınan hata kodu: no instance of overloaded function "f" matches the argument list

**Soru 23: Conversion tanımla**

```CPP
void f(int);
void f(double);
void f(long);

int main()
{
	f(3.4); 
}

Cevap : 
f(3.4); 	// Exact match
f(12); 		// Exact match
f(12u);		// Ambiguity, üçü arasında ambiguity var. Türlerden üçü de seçilebilir ama seçilemiyor.
f(2.3L);	// Argüman long double. int, double ve long'a conversion. Dolayısıyla ambiguity.
f(2.3f);	// Float'tan double'a conversion var. double dönüşür.
f('A');		// Karakter sabiti türü char fakat char'dan int'e promotion olacak.
```
