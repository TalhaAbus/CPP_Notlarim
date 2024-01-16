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
3. **Forwarding Reference:**
















