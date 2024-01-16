```CPP
const char* str = "Merhaba Dünya";
```
> Burada str pointeri const char* türündedir ve const anahtar kelimesi gösterilen karakterlerin sabit oldğunu ve değiştirilemeyeceğini belirtir. Ancak C dilinde const kullanımı zorunlu değildir ve bazı eski kodlarda bu kullanım vardır. Bu durumda da string literalini değiştirmek tanımsız davranışa yol açar.

> C++ dilinde bu const kullanımı zorunludur ve modern C++ ta  her zaman const char* kullnılmıştır.

> Özetle C ve C++ dillerinde string literallerini değiştirmeye çalışmak tanımsız davranışa yol açar.

### Array to Pointer conversion (Array decay)
- Bir dizi ismi, dizinin ilk elemanının adresini gösteren bir pointera otomatik dönüşmesidir.

```CPP
int arr[] = {1, 2, 3, 4, 5};
```
> Burada arr ifadesi direkt olarak int* türünden bir pointera dönüşür. Bu pointer ilk ifadenin adresini gösterir.

```CPP
#include <iostream>

using namespace std;

void printArray(int* arr, int size)
{
	for (int i = 0; i < size; ++i)
	{
		printf("%d\n", arr[i]);
	}
}

int main()
{
	int arr[] = { 1,2,3,4,5 };
	printArray(arr, 5);
	return 0;
}
```
> Burada kullandığımız arr ifadesi otomatik olarak int* türünden bir adrese dönüşüyor ve fonksiyona dizinin başlangıç adresini geçiyor.

**2 İstisna hariç bu dönüşüm otomatik gerçekleşir:**
1. sizeof operatörünün operandının dizi olması.
2. Adres operatörünün operandının bir dizi olması.

**Örnekler:**
```CPP
int a[10] = { 1,5,7 };
```
- **a'nın türü:** int[10]
- **a'nın adresi olan tür:** int(*)[10]

# Referans Semantiği

- C++'ta referans semantiği, pointer kullanımının bir alternatifidir.

1. **LValue Reference:** Bellekte sabit bir konuma sahip nesneleri temsil eder. Yani bir ifadenin Lvalue olması, o ifadenin bellekteki bir nesneye işaret ettiği anlamına gelir. Atama işlecinin hem sol hem de sağ tarafında yer alabilirler.

```CPP
int a = 10;
int& ref = a;  // 'a' değişkenine bir lvalue referansı
```
2. **Rvalue Reference:(&&)** C++ 11 ile gelene ve geçici değerleri referans alan türdür. Bir ifadenin Rvalue olması, bellekte kalıcı yeri olmayan  ve bir ifadenin değerini hesaplamak için oluşturulan ifade demektir. Atama işlecinin yalnızca sağ tarafında yer alabilirler.
3. **Forwarding Reference:** (Universal Reference) C++ 11'in **auto** ve **declytype** özellikleriyle birlikte gelen tür.

```CPP
template<typename T>
void func(T&& arg) {
    // arg, forwarding reference
}
```

**Not:**
- C dilinde poniter kullanımı çokça var. Fakat C++ dilinde  pointer kullanımı C diline göre çok daha az. Bunun sebebi C++ dilinde pointer ihtiyacını karşılamaya yönelik olarak reference semantiği var.

## Static Ömürlü Nesneler
- Programın başından sonuna kadar yaşam süresi olan nesnelerdir. Program çalıştığında oluşturulur ve program sonlanınca yok edilir.
1. Global Değişkenler
2. Static anahtar sözcüğü ile tanımlanan yerel değişkenler
3. String Literalleri (String literalleri için oluşturulan char diziler)

**Neden modern C++ ilk değer verme biçimi olarka {} getirdi?**
- **Uniform** olması. Yani neye ilk değer verirsen ver küme parantezi kullanabiliyorsun.
- **Daraltıcı dönüşümleri engeller.** Eğer {} kullanıp daraltıcı dönüşüm yaparsak sentaks hatası alırız.

**C++ dilinde bunların hepsi aynı anlamda:**
- int a1[4] = {0};
- int a2[4] = {};
- int a3[4]{};
> Hepsi zero initialize edilmiş oluyor. C dilinde boşluğun içi dolu olmak zorunda ama burada boş bırakılabilir.








