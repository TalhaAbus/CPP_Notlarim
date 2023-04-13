# Short Circuit Behaviour

- Short circuit behavior (kısa devre davranışı), mantıksal operatörlerin (genellikle && ve || olarak temsil edilir) değerlendirilmesi sırasında, sonucun zaten belirlendiği durumda kalan ifadelerin değerlendirmesinin atlanmasına denir. Bu özellik, bazı durumlarda performansı artırır ve yan etkileri olan fonksiyonların gereksiz yere çağrılmasını önler.

- Kısa devre davranışı şu şekilde çalışır:

1. && (AND) operatörü için: İlk ifade yanlış (false) olduğunda, sonuç kesinlikle yanlış olacağı için ikinci ifade değerlendirilmeye gerek kalmaz ve atlanır.

```CPP
bool a = false;
bool b = true;

if (a && b) { // a false olduğu için b değerlendirilmeyecek ve kısa devre oluşacaktır.
    // ...
}

```

2. || (OR) operatörü için: İlk ifade doğru (true) olduğunda, sonuç kesinlikle doğru olacağı için ikinci ifade değerlendirilmeye gerek kalmaz ve atlanır.

```CPP
bool a = true;
bool b = false;

if (a || b) { // a true olduğu için b değerlendirilmeyecek ve kısa devre oluşacaktır.
    // ...
}
```

# Type Conversion

- Type conversion (tür dönüşümü), bir veri türünün başka bir veri türüne dönüştürülmesi işlemidir. C++ gibi programlama dillerinde, bazı durumlarda veri türleri arasında dönüşüm yapmak gerekebilir. Tür dönüşümleri genellikle iki şekilde gerçekleştirilir: implicit (bilinçsiz) ve explicit (bilinçli) dönüşümler

1. **Implicit type conversion (bilinçsiz tür dönüşümü):** Bu dönüşüm, derleyici tarafından otomatik olarak gerçekleştirilir ve programcının müdahalesi gerektirmez. Bu tür dönüşüm, genellikle daha geniş veya daha yüksek hassasiyette bir türe dönüşüm yaparken meydana gelir. 

**Örneğin:**

```CPP
int a = 10;
double b = a; // implicit dönüşüm: 'a' int türünden double türüne dönüşür.
```

2. **Explicit type conversion (bilinçli tür dönüşümü):** Bu dönüşüm, programcının açıkça talep ettiği ve belirttiği bir dönüşüm şeklidir. C++'da, bu tür dönüşümler genellikle C stilinde veya static_cast, dynamic_cast, const_cast ve reinterpret_cast gibi C++ cast operatörleri ile gerçekleştirilir. 

**Örneğin:**
```CPP
double x = 3.14;
int y = static_cast<int>(x); // explicit dönüşüm: 'x' double türünden int türüne dönüşür.
```
> Tür dönüşümleri, farklı veri türleri arasında uyum sağlamak ve işlemleri gerçekleştirmek için önemlidir. Ancak, uyumsuz türler arasında dönüşüm yaparken veya hassasiyet kaybı yaşanabilecek durumlarda dikkatli olunması gerekir.

# Reference Collapsing

- Reference collapsing, C++ dilinde şablonlar ve tür çıkarımı ile ilgili özel bir kuraldır. Bu kural, birden fazla referans seviyesi olan bir türe uygulandığında, bu referansların nasıl birleştirileceğini belirtir. Başka bir deyişle, iki referansın bir araya gelmesi durumunda sonuç türünün ne olacağını açıklar.

- Reference collapsing kuralı, şu şekildedir:

1. T& & → T&
2. T& && → T&
3. T&& & → T&
4. T&& && → T&&

> Burada T, herhangi bir veri türünü temsil eder. İki lvalue referansı (T& &) veya bir lvalue ve bir rvalue referansı (T& && veya T&& &) bir araya geldiğinde, sonuç her zaman bir lvalue referansıdır (T&). İki rvalue referansı (T&& &&) bir araya geldiğinde ise, sonuç bir rvalue referansıdır (T&&).

- Bu kural, özellikle C++11 ve sonrasında tanıtılan std::move, perfect forwarding ve rvalue referanslar gibi özelliklerle ilgilidir. Aşağıda, bu kuralı gösteren bir örnek verilmiştir:

```CPP
template <typename T>
void foo(T&& t) {
    // ...
}

int a = 10;
int& b = a;

foo(a); // T = int&, T&& = int& &&, reference collapsing: int& && → int&
foo(b); // T = int&, T&& = int& &&, reference collapsing: int& && → int&
```
- Reference collapsing kuralı, C++'daki ileri düzey özellikler ve şablon metaprogramlama ile çalışırken önemli bir rol oynar.

# Default Argument

- Default argument, bir işlevin çağrılmasında, belirtilmeyen bir argümanın değerini belirlemek için kullanılır. Bu argüman, işlevin tanımında belirtilen varsayılan değerle otomatik olarak atanır.

- Bir işlevin parametre listesindeki son parametrelerden birine varsayılan bir argüman verildiğinde, bu argümanın sonraki tüm parametrelerine de varsayılan argümanlar verilebilir. Ancak, bir işlevin parametre listesindeki bir parametreye varsayılan bir argüman atanması durumunda, daha önceki parametrelerin her birine de varsayılan bir argüman atanması gereksizdir.

- Örneğin, aşağıdaki örnekte, "foo" işlevinin son parametresine bir varsayılan argüman atanmıştır:

```CPP
void foo(int x, int y, int z = 0); // "z" varsayılan argümana sahiptir

int main() {
    foo(1, 2); // "z" varsayılan olarak atanır ve değeri 0'dır.
    foo(1, 2, 3); // "z" değeri 3'tür.
    return 0;
}
```
> Bu örnekte, "foo" işlevi, üç parametreye sahiptir. Ancak, son parametre "z", varsayılan bir argümana sahiptir ve bu argüman belirtilmezse, değeri 0 olarak atanır. Bu nedenle, "foo(1,2)" ifadesi çağrıldığında, "z" parametresi varsayılan olarak atanır ve değeri 0'dır. "foo(1,2,3)" ifadesi çağrıldığında ise, "z" parametresi belirtilen değere göre atanır ve değeri 3'tür.

# Function Overloading

- Function overloading (fonksiyon aşırı yüklemesi), C++ dilinde aynı isme sahip birden fazla fonksiyonun farklı parametrelerle tanımlanabilmesine olanak sağlayan bir özelliktir. Bu özellik, fonksiyonların farklı türde veya sayıda argümanlarla çağrılabilmesini sağlar, böylece kodun okunabilirliği ve esnekliği artar.

- İşte bir örnek:
```CPP
#include <iostream>

void print(const char* s) {
    std::cout << s << std::endl;
}

void print(int i) {
    std::cout << i << std::endl;
}

int main() {
    print("Hello, World!"); // const char* parametreli fonksiyon çağrılır.
    print(42); // int parametreli fonksiyon çağrılır.
    return 0;
}

```

## Overload Resolution Süreci

- Overload resolution (aşırı yükleme çözümlemesi) süreci, derleyicinin doğru aşırı yüklenmiş fonksiyonu seçmesini sağlayan süreçtir. Bu süreç, şu adımlarla gerçekleşir:

1. **İsim arama (name lookup):** İlk olarak, derleyici fonksiyon adını kullanarak uygun fonksiyonları bulur. Eğer hiçbir uygun fonksiyon bulunamazsa, derleyici bir hata mesajı verir.
2. **Uygun fonksiyonlar listesini daraltma:** Derleyici, çağrılan fonksiyona verilen argümanlarla eşleşen uygun fonksiyonları belirler. Bu aşamada, uygun fonksiyonlar listesi daraltılabilir ve bazı aşırı yüklemeler elenebilir.
3. **En iyi eşleşmeyi belirleme:** Derleyici, fonksiyonlara verilen argümanlarla en iyi eşleşen fonksiyonu seçer. Bu seçim, argümanların dönüşümü gerektiren en az sayıda ve en basit tür dönüşümleri ile gerçekleşir. Eğer birden fazla fonksiyon en iyi eşleşme olarak belirlenirse, derleyici "ambiguity" (belirsizlik) hatası verir ve programcı bu durumu düzeltmelidir.

## Function Signature

- Function signature, bir işlevin parametrelerinin türlerinin ve geri dönüş değerinin türünün birleşimidir. Bu tür, bir işlevin diğer işlevlerden veya değişkenlerden ayırt edilmesine yardımcı olur.

- Function signature, işlevin adı hariç tüm diğer unsurları içerir. C++ dilinde, iki işlev aynı isme sahip olsa bile, parametrelerin sayısı, türleri veya sırası farklı olduğunda farklı bir işlev imzasına sahip olurlar.

- Function signature ayrıca, bir işlevin overload edilmesi (aşırı yüklenmesi) durumunda da önemlidir. Aynı isme sahip birden fazla işlev olduğunda, her bir işlevin farklı bir işlev imzası olmalıdır.

- Örneğin, aşağıdaki örnekte, "foo" işlevi iki kez tanımlanmıştır. İki işlevin de farklı bir işlev imzası vardır, çünkü biri bir "int" parametresi alırken, diğeri bir "double" parametresi alır:

```CPP
void foo(int x) { // birinci işlev
    // ...
}

void foo(double y) { // ikinci işlev
    // ...
}

int main() {
    foo(5); // birinci işlevi çağırır
    foo(3.14); // ikinci işlevi çağırır
    return 0;
}
```
> Bu örnekte, "foo" işlevi iki kez tanımlanmıştır. İki işlevin de farklı bir işlev imzası vardır ve aynı isme sahip olmalarına rağmen, birinci işlev bir "int" parametresi alırken, ikinci işlev bir "double" parametresi alır. Böylece, "foo(5)" ifadesi birinci işlevi, "foo(3.14)" ifadesi ise ikinci işlevi çağırır.





















