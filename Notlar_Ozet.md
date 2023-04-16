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

## User Defined Conversion

- User-defined conversion (kullanıcı tanımlı dönüşüm), C++ programlama dilinde, sınıf türlerinin birbirine veya temel türlerle dönüşümünü sağlayan özel fonksiyonlar kullanarak gerçekleştirilen tür dönüşümüdür. Bu tür dönüşümler, sınıfın üye fonksiyonları veya dış fonksiyonlar olarak tanımlanabilen dönüşüm operatörleri ile sağlanır.

1. **Conversion operator (dönüşüm operatörü):** Sınıfın üye fonksiyonu olarak tanımlanır ve sınıf türünün başka bir türe dönüşümünü sağlar. Dönüşüm operatörleri, operator anahtar kelimesi ile başlar ve dönüştürülecek türü belirtir. Örneğin:

```CPP
class MyClass {
    int x;
public:
    MyClass(int a) : x(a) {}

    // Kullanıcı tanımlı dönüşüm operatörü: MyClass türünden int türüne dönüşüm
    operator int() const {
        return x;
    }
};

int main() {
    MyClass obj(10);
    int a = obj; // Kullanıcı tanımlı dönüşüm operatörü kullanılır: MyClass -> int
    std::cout << a << std::endl; // 10
}

```

2. **Conversion constructor (dönüşüm yapıcı fonksiyonu):** Bir sınıfın başka bir türden değer alarak oluşturulabilmesini sağlayan yapıcı fonksiyondur. Bu tür yapıcı fonksiyonlar, genellikle tek parametre alır ve explicit anahtar kelimesi ile belirtilmediği sürece, derleyici tarafından otomatik olarak kullanılabilir. Örneğin:

```CPP
class MyClass {
    int x;
public:
    // Dönüşüm yapıcı fonksiyonu: int türünden MyClass türüne dönüşüm
    MyClass(int a) : x(a) {}

    int getValue() const {
        return x;
    }
};

int main() {
    int a = 10;
    MyClass obj = a; // Dönüşüm yapıcı fonksiyonu kullanılır: int -> MyClass
    std::cout << obj.getValue() << std::endl; // 10
}

```
> Kullanıcı tanımlı dönüşümler, sınıflar arasında veya sınıflar ile temel türler arasında uyumluluk sağlamaya yardımcı olur..

# Inline Expension

- Inline expansion (satır içi genişleme), C++ derleyicisinin, performansı artırmak amacıyla, belirli bir fonksiyonun kodunu çağrıldığı yerde doğrudan yerleştirme sürecidir. Bu işlem, fonksiyon çağrısı ile ilgili yükü ortadan kaldırarak, kodun hızını artırır. Inline expansion, özellikle küçük ve sıkça kullanılan fonksiyonlar için etkilidir.

- inline anahtar kelimesi, fonksiyonun önünde kullanılarak derleyiciye fonksiyonun inline expansion için uygun olduğunu bildirir. Ancak, bu sadece bir öneridir ve derleyici, uygun görmediği durumlarda bu öneriyi görmezden gelebilir.

```CPP
inline int add(int a, int b) {
    return a + b;
}

```
- Inline fonksiyonların avantajları ve dezavantajları şunlardır:

**Avantajlar:**
1. **Performans artışı:** Fonksiyon çağrısı maliyeti ortadan kaldırılarak, kodun hızı artar.
2. **Kod optimizasyonu:** Derleyici, inline fonksiyonları daha etkili bir şekilde optimize edebilir.

**Dezavantajlar:**
1. **Kod boyutunun artması:** Fonksiyonun kodu çağrıldığı her yerde yerleştirildiğinden, bu işlem toplam kod boyutunu artırabilir.
2. **İşlem süresinin artması:** Inline expansion, derleme süresini uzatabilir.
3. **Taşınabilirlik:** Farklı derleyicilerin ve platformların, inline fonksiyonları farklı şekilde ele alması nedeniyle, taşınabilirlik sorunları yaşanabilir.

- Inline expansion, aşağıdaki durumlarda dikkatli kullanılmalıdır:

1. **Büyük fonksiyonlar:** Kod boyutunu önemli ölçüde artırabileceğinden büyük fonksiyonlar için kullanılmamalıdır.
2. **Özyinelemeli (recursive) fonksiyonlar:** Inline fonksiyonlar özyinelemeli olmamalıdır, çünkü bu durum kodun anlaşılırlığını ve optimizasyonunu olumsuz etkileyebilir.
3. **Sanal (virtual) fonksiyonlar:** Sanal fonksiyonlar, genellikle çağrı zamanında bağlanır, bu nedenle inline expansion için uygun değildir.

> Sonuç olarak, inline expansion, performansı artırmak için kullanılabilecek bir tekniktir. Ancak, uygun durumlar dışında kullanımı kodun boyutunu ve karmaşıklığını artırabilir. Inline fonksiyonlar, küçük ve sıkça kullanılan fonksiyonlar için etkili olabilirken, büyük ve özyinelemeli fonksiyonlar için uygun değildir.

# Dead Code Elimination

- Dead code elimination (Ölü kod elemesi), bir programda çalıştırılmayan kod bloklarının (özellikle fonksiyonlar, değişkenler, dallanma ifadeleri ve döngüler) derleyici veya optimizasyon aracı tarafından tanınarak kaldırılması işlemidir. Bu işlem, kodun boyutunu küçültür ve çalışma süresini hızlandırır.

- Dead code elimination, genellikle bir programın optimizasyon aşamasında gerçekleştirilir. Derleyiciler, kodun etkileşimli analiziyle çalıştırılmayan kodları tanıyabilirler. Bu analiz işlemi, kodun içerisindeki kontrol akışı (control flow) ve veri akışı (data flow) gibi özellikleri inceleyerek gerçekleştirilir.

- Ölü kod tanımlama, programın çalıştırılabilir kod bloklarının önceden belirlenmesiyle yapılır. Bu belirleme, programın doğal çalışma düzenine göre belirlenir. Örneğin, bir fonksiyon hiçbir zaman çağrılmazsa, o fonksiyon ölü kod olarak tanımlanır ve programın derlenmiş versiyonundan kaldırılır.

> Özetle, Dead code elimination, programın çalıştırılmayan kodlarının derleyici veya optimizasyon aracı tarafından kaldırılması işlemidir. Bu işlem, programın boyutunu küçültür, çalışma süresini hızlandırır ve bellek kullanımını optimize eder.

# Loop Unrolling

- Loop unrolling (döngü açma), program optimizasyonu için kullanılan bir tekniktir. Bu teknik, döngü içindeki işlemleri tekrar ederek döngü sayısını azaltmayı amaçlar. Bu sayede, döngü kontrol yapılarının ve dallanmaların maliyeti azaltılır, böylece programın hızı ve performansı artar.

- Loop unrolling, derleyici tarafından otomatik olarak gerçekleştirilebilir veya programcı tarafından manuel olarak yapılabilir. İşte basit bir örnek:

```CPP
// Basit döngü
for (int i = 0; i < 10; ++i) {
    doSomething(i);
}

// Loop unrolling ile döngünün açılması
for (int i = 0; i < 10; i += 2) {
    doSomething(i);
    doSomething(i + 1);
}

```

> İkinci döngü, "for (int i = 0; i < 10; i += 2)" ifadesiyle tanımlanmıştır. Bu döngü de "i" değişkeninin 0'dan başlayarak 9'a kadar olan sayılarda arttırılması ile çalışır. Ancak, her döngü adımında, "doSomething(i)" ve "doSomething(i+1)" fonksiyonları sırayla çağrılır. Bu, döngünün her bir adımında iki kez işlem yapılması anlamına gelir. Bu teknik, loop unrolling olarak adlandırılır.

> Loop unrolling, döngü süresini azaltır ve programın hızını arttırır. Bunun nedeni, döngüdeki kontrol ifadelerinin sayısının azaltılması ve işlemlerin optimize edilmesidir. Ancak, bu teknik aynı zamanda programın bellek kullanımını artırabilir. Çünkü, döngüdeki her bir adım için ayrı bir değişken bellekte ayrılmalıdır.

- Loop unrolling'in avantajları ve dezavantajları şunlardır:

**Avantajlar:**

1. Performans artışı: Döngü kontrol yapılarının ve dallanmaların maliyeti azaltılarak programın hızı artar.
2. Pipelining optimizasyonu: Modern işlemcilerde, loop unrolling sayesinde pipelining ve süper skalar işlemci teknolojilerinden daha etkili bir şekilde yararlanılabilir.

**Dezavantajlar:**
1. Kod boyutunun artması: Döngü içindeki işlemler tekrar edildiğinden, toplam kod boyutu artar.
2. Önbellek (cache) performansının etkilenmesi: Kod boyutunun artması nedeniyle, önbellek performansı olumsuz etkilenebilir.
3. Döngü sayısının sabit olmaması: Döngü sayısının sabit olmaması durumunda, loop unrolling uygulanması zor olabilir ve kod karmaşıklığı artabilir.

- Loop unrolling, aşağıdaki durumlarda dikkatli kullanılmalıdır:

1. Büyük döngüler: Kod boyutunu önemli ölçüde artırabileceğinden, büyük döngüler için kullanılmamalıdır.
2. Koşullu işlemler içeren döngüler: Koşullu işlemler içeren döngülerde, loop unrolling ile performans artışı garanti edilemez ve kod karmaşıklığı artabilir

# Generic Programming

- Generic programming (genel programlama), yazılımın türden bağımsız olarak yazılmasını sağlayarak yeniden kullanılabilirlik, modülerlik ve kodun anlaşılırlığını artıran bir programlama yaklaşımıdır. C++ dilinde, generic programming öncelikle şablonlar (templates) kullanılarak gerçekleştirilir. Şablonlar, derleyiciye belirli türlerle çalışacak kod üretmesi için parametreler sağlar ve böylece aynı kodun farklı türlerle çalışabilmesi sağlanır.

- Şablonlar, iki ana kategoride kullanılabilir: **sınıf şablonları** ve **fonksiyon şablonları**.

1. **Sınıf şablonları (Class templates):** Türler üzerinde parametreli sınıflar tanımlamak için kullanılır. Sınıf şablonları, türden bağımsız veri yapıları ve algoritmalar oluşturmak için kullanılabilir. Örneğin, bir vector sınıf şablonu:

```CPP
template <typename T>
class Vector {
    T* data;
    int size;

public:
    Vector(int size) : data(new T[size]), size(size) {}

    T& operator[](int index) {
        return data[index];
    }
};

int main() {
    Vector<int> int_vector(10);
    Vector<double> double_vector(5);
}

```

2. **Fonksiyon şablonları (Function templates):** Türler üzerinde parametreli fonksiyonlar tanımlamak için kullanılır. Fonksiyon şablonları, türden bağımsız fonksiyonlar oluşturmak için kullanılabilir. Örneğin, iki değeri takas etmek için kullanılan bir fonksiyon şablonu:

```CPP
template <typename T>
void swap(T& a, T& b) {
    T temp = a;
    a = b;
    b = temp;
}

int main() {
    int x = 1, y = 2;
    swap(x, y);

    double a = 3.14, b = 2.71;
    swap(a, b);
}
```

- Generic programming, aşağıdaki avantajları sağlar:

1. **Yeniden kullanılabilirlik:** Türden bağımsız olarak yazılmış şablonlar, kodun farklı türlerle çalışabilmesini ve yeniden kullanılabilirliğini sağlar.
2. **Modülerlik:** Şablonlar sayesinde, türler arasında bağımsız ve soyutlanmış kod parçaları oluşturulabilir.
3. **Kod anlaşılırlığı:** Şablonlar kullanılarak yazılan kod, türlerin belirsizliğinden arındırılarak daha anlaşılır hale getirilir.

- Generic programming kullanırken dikkate alınması gereken bazı hususlar şunlardır:

1. **Kullanım karmaşıklığı:** Şablonlar, özellikle ileri düzey kullanımlarda karmaşık hale gelebilir ve kodun anlaşılırlığını azaltabilir. Bu nedenle, şablonların mümkün olduğunca basit ve düzenli kullanılması önemlidir.
2. **Derleme süresi:** Şablonlar, derleme süresinde kod üretmeye dayandığından, geniş kullanımlarda derleme süresini uzatabilir.
3. **Hata mesajlarının karmaşıklığı:** Şablonlarla ilgili hatalar, genellikle karmaşık ve uzun hata mesajlarına yol açabilir. Bu nedenle, şablonları kullanırken dikkatli olmak ve hataları daha kolay çözümlemek için kodun düzenli ve anlaşılır olması önemlidir.
4. **Derleyici uyumluluğu ve taşınabilirlik:** Farklı C++ derleyicileri, şablonların belirli özelliklerini farklı şekillerde destekleyebilir. Bu nedenle, geniş çaplı projelerde ve farklı platformlarda çalışırken, taşınabilirliği sağlamak için derleyici uyumluluğuna dikkat etmek önemlidir.

> **Sonuç olarak,** generic programming, C++ programlama dilinde güçlü ve esnek bir yöntemdir. Şablonlar sayesinde, türden bağımsız ve yeniden kullanılabilir kodlar yazarak, kodun anlaşılırlığını ve modülerliğini artırabilirsiniz. Bu yaklaşım, geniş çaplı projelerde ve karmaşık veri yapılarıyla çalışırken önemli ölçüde fayda sağlar.

# Inline Functions

- Inline fonksiyonlar, C++ programlama dilinde kullanılan performans optimizasyon tekniklerinden biridir. İnline fonksiyonlar, fonksiyon çağrılarının maliyetini azaltarak, programın hızını ve performansını artırmayı amaçlar. Bu, derleyicinin belirli bir fonksiyonun kodunu çağrıldığı yerde doğrudan yerleştirerek gerçekleştirilir (inline expansion olarak da bilinir).

- inline anahtar kelimesi, fonksiyonun önünde kullanılarak derleyiciye fonksiyonun inline expansion için uygun olduğunu bildirir. Ancak, bu sadece bir öneridir ve derleyici, uygun görmediği durumlarda bu öneriyi görmezden gelebilir.

```CPP
inline int add(int a, int b) {
    return a + b;
}

```

- Inline fonksiyonların avantajları ve dezavantajları şunlardır:

**Avantajlar:**

1. **Performans artışı:** Fonksiyon çağrısı maliyeti ortadan kaldırılarak, kodun hızı artar.
2. **Kod optimizasyonu:** Derleyici, inline fonksiyonları daha etkili bir şekilde optimize edebilir.

**Dezavantajlar:**
1. **Kod boyutunun artması:** Fonksiyonun kodu çağrıldığı her yerde yerleştirildiğinden, bu işlem toplam kod boyutunu artırabilir.
2. **İşlem süresinin artması:** Inline expansion, derleme süresini uzatabilir.
3. **Taşınabilirlik:** Farklı derleyicilerin ve platformların, inline fonksiyonları farklı şekilde ele alması nedeniyle, taşınabilirlik sorunları yaşanabilir.

# Complete - Incomplete Type

- Tam veri türleri, derleyicinin tüm bilgiye sahip olduğu türlerdir. Bu türlerin tam tanımları, veri türü bildiriminde yer alır ve boyutları belirtilmiştir. Tam bir tür kullanıldığında, işlemler doğru bir şekilde gerçekleştirilir ve türdeki değişkenler bellekte doğru bir şekilde yerleştirilir.

- Eksik veri türleri ise, tam tanımı olmayan türlerdir. Bu türlerin tanımı, veri türü bildiriminde tamamlanmamıştır ve derleyicinin yalnızca belirli bilgileri vardır. Bu türler genellikle, bir sınıfın ya da yapının ileri bildiriminde kullanılırlar. Eksik bir tür kullanıldığında, derleyici hata verir ve kod derlenemez.

- Bir veri türünün tam ya da eksik olması, o türün nasıl kullanılabileceğini belirler. Tam bir tür, o türdeki herhangi bir değişkenin tanımlanmasına izin verirken, eksik bir tür sadece bir işaretçi tanımlamaya izin verir. Tam bir türün tüm işlevleri ve üye değişkenleri kullanılabilirken, eksik bir türün yalnızca sınıfın veya yapının adı kullanılabilir.

- Örneğin, aşağıdaki örnekte, "A" sınıfının ileri bildirimi (forward declaration) yapılırken, sınıfın eksik bir tür olarak tanımlanması gösterilmiştir:

```CPP
class A; // "A" sınıfının ileri bildirimi

class B {
public:
    void doSomething(A& a); // "A" sınıfı eksik tür olarak kullanılır
};

class A {
public:
    int x;
};

void B::doSomething(A& a) {
    // "A" sınıfının tam tanımı burada kullanılır
    a.x = 5;
}

int main() {
    A a;
    B b;
    b.doSomething(a);
    return 0;
}

```
> Bu örnekte, "A" sınıfı ileri bildirimi yapılarak eksik bir tür olarak tanımlanmıştır. "B" sınıfında "doSomething" fonksiyonunda, "A" sınıfı işaretçi olarak kullanılır. Ancak, "A" sınıfının tam tanımı, fonksiyonun tanımının altında yer almaktadır. Bu nedenle, "A" sınıfının eksik tür olarak tanımlanması, "B" sınıfının derlenmesine izin verir.

# Constexpr Keyword

- constexpr anahtar kelimesi, C++ dilinde sabit ifadeler ve sabit ifade fonksiyonları tanımlamak için kullanılır. constexpr kullanarak, derleme süresinde değerlendirilebilecek sabit ifadeler ve fonksiyonlar oluşturarak, programın hızını ve performansını artırabilirsiniz.

1. **Constexpr değişkenler:** constexpr anahtar kelimesi, bir değişkenin değerinin derleme süresinde sabit olduğunu belirtir. Bu, derleyici tarafından derleme süresinde değerlendirilir ve böylece derleyici kodu daha iyi optimize edebilir.

```CPP
constexpr int x = 42; // x, derleme süresinde sabit bir değere sahiptir.

```
2. **Constexpr fonksiyonlar:** constexpr anahtar kelimesi, fonksiyonların derleme süresinde değerlendirilebileceğini belirtmek için kullanılabilir. Bu fonksiyonlar, sadece sabit ifadelerle çalışır ve sadece tek bir dönüş ifadesi içerir. Constexpr fonksiyonların avantajı, derleme süresinde değerlendirildiğinden, fonksiyon çağrısı maliyetinin ortadan kalkması ve kodun hızının artmasıdır.

```CPP
constexpr int pow2(int n) {
    return (n <= 0) ? 1 : 2 * pow2(n - 1);
}

int main() {
    constexpr int result = pow2(5); // Derleme süresinde değerlendirilir ve result = 32 olur.
}
```

- C++14'ten itibaren, constexpr fonksiyonlar daha karmaşık hale gelmiştir ve birden çok ifade ve döngü içerebilir. Bu, constexpr fonksiyonların daha geniş bir yelpazede kullanılabilmesini sağlar.

- Constexpr anahtar kelimesinin avantajları şunlardır:

1. **Performans artışı:** Derleme süresinde değerlendirilerek, fonksiyon çağrısı maliyeti azaltılır ve programın hızı artar.
2. **Kod optimizasyonu:** Derleyici, constexpr değişkenleri ve fonksiyonları daha etkili bir şekilde optimize edebilir.
3. **Daha güvenli ve hızlı sabitler:** Constexpr, daha güvenli ve hızlı sabit değerler oluşturmak için kullanılabilir.

- Constexpr fonksiyonlar ve değişkenler kullanırken dikkate alınması gereken bazı hususlar şunlardır:

1. **Derleme süresinin artması:** Constexpr fonksiyonlar, derleme süresinde değerlendirildiğinden, geniş kullanımlarda derleme süresini uzatabilir.
2. **Sınırlı kullanım:** Constexpr fonksiyonlar, sadece sabit ifadelerle çalışabileceğinden, tüm durumlar için uygun olmayabilir.

# Member Functions

- C++ dilinde, bir sınıfın üye fonksiyonları (member functions), sınıfın verileri üzerinde işlem yapmak için kullanılan özel fonksiyonlardır. Bir sınıfın üye fonksiyonları, sınıfın public, private ve protected bölümlerinde tanımlanabilir.
- Üye fonksiyonlar, sınıfın içinde tanımlanır ve sınıfın nesneleri tarafından çağrılabilir. Üye fonksiyonlar, sınıfın verilerine doğrudan erişebilirler ve sınıfın özelliklerini kullanarak veriler üzerinde işlem yapabilirler. Ayrıca, üye fonksiyonlar, sınıfın diğer fonksiyonlarına ve verilerine erişebilirler.
- Üye fonksiyonlar, genellikle sınıfın davranışlarını ve özelliklerini belirlemek için kullanılırlar. Örneğin, bir sınıfın "Rectangle" adlı üye fonksiyonu, dikdörtgenin alanını ve çevresini hesaplayabilir. Bir başka örnek olarak, bir sınıfın "BankAccount" adlı üye fonksiyonu, hesap bakiyesini artırabilir ya da azaltabilir.
- Üye fonksiyonlar, sınıfın yapısına göre farklılık gösterebilirler. Örneğin, bir sınıfın yapısı, yapıcısı (constructor) ve yıkıcısı (destructor) gibi özel üye fonksiyonları içerebilir. Ayrıca, bir sınıfın üye fonksiyonları, sabit bir fonksiyon olarak (const member function) tanımlanabilir. Sabit bir üye fonksiyon, sınıfın verilerini değiştirmediği ve sadece okuma işlemleri gerçekleştirdiği için, sınıfın nesneleri tarafından sabit bir fonksiyon olarak çağrılabilir.

# Redecleration

- Redeclaration, C++ dilinde aynı isimli bir değişkenin, fonksiyonun ya da sınıfın birden fazla kez bildirilmesidir. Yani, bir öğe bir kez bildirildikten sonra tekrar aynı isimle bildirilirse, bu bir redeclaration olarak kabul edilir.
- Redeclaration, bir değişkenin, fonksiyonun ya da sınıfın birden fazla dosyada kullanılması gerektiği durumlarda sıklıkla kullanılır. Örneğin, bir sınıfın üye fonksiyonlarının tanımları, sınıfın tanımından ayrı dosyalarda bulunabilir. Bu durumda, her bir dosyada üye fonksiyonlarının tekrar bildirilmesi gereklidir.

- Redeclaration, aynı isimli öğelerin aynı dosyada birden fazla kez tanımlanması durumunda hata verebilir. Örneğin, aşağıdaki kodda, "x" değişkeni, aynı dosyada birden fazla kez tanımlanmıştır ve hata verecektir:

```CPP
int x;
int x; // Redeclaration hatası

```

- Ancak, aynı isimli öğelerin farklı dosyalarda bildirilmesi durumunda, redeclaration hatası vermezler. Örneğin, aşağıdaki örnekte, "Rectangle" sınıfının üye fonksiyonları farklı dosyalarda tekrar bildirilmiştir:
```CPP
// Rectangle.h
class Rectangle {
public:
    void setWidth(int width);
    void setHeight(int height);
    int getArea();
private:
    int width_;
    int height_;
};

// Rectangle.cpp
#include "Rectangle.h"

void Rectangle::setWidth(int width) {
    width_ = width;
}

void Rectangle::setHeight(int height) {
    height_ = height;
}

int Rectangle::getArea() {
    return width_ * height_;
}

```

> Burada, "Rectangle" sınıfının üye fonksiyonları, "Rectangle.h" başlık dosyasında bildirilmiş ve "Rectangle.cpp" kaynak dosyasında yeniden bildirilmiştir. Bu durumda, bir redeclaration hatası verilmez.

# This Keyword
- C++ dilinde, this anahtar kelimesi, bir sınıfın üye fonksiyonları içinde kullanılarak, fonksiyonun çağrıldığı nesnenin adresini temsil eden bir işaretçidir. this işaretçisi, üye fonksiyonlar içerisinde, nesnenin üye değişkenlerine ve fonksiyonlarına erişmek için kullanılabilir. Bu, sınıfın özelliklerini ve davranışlarını doğru bir şekilde yönetmek için önemlidir.

- this anahtar kelimesinin kullanımı ve avantajları şunlardır:

1. **Üye değişkenlerin ve fonksiyonların belirginleştirilmesi:** this anahtar kelimesi, üye fonksiyonlar içinde, üye değişkenlerin ve fonksiyonların yerel değişkenlerden ayırt edilmesine yardımcı olur.

```CPP
class MyClass {
    int x;

public:
    void setX(int x) {
        this->x = x; // Üye değişkeni "x", fonksiyon parametresi olan "x" ile aynı ada sahip olduğu için, "this->x" şeklinde belirginleştirilir.
    }
};

```
> Fonksiyonun parametresi olan "x", aynı ada sahip olan sınıfın üye değişkeni ile çakışabilir. Bu durumda, üye değişkeni belirginleştirilmelidir. Bu nedenle, "this->" operatörü, üye değişkeninin fonksiyon parametresi olan "x" ile ayrımını sağlamak için kullanılır.

> Bu kodda, "this->x" ifadesi, fonksiyonun parametresi olan "x" ile sınıfın üye değişkeni olan "x" arasındaki farkı açıkça belirtir. Yani, "setX" fonksiyonunun parametresi olan "x", fonksiyonun çalışması sırasında "this->x" ifadesiyle belirtilen sınıfın üye değişkenine atanır.

2. **Zincirleme (chaining) işlemleri:** this işaretçisi, fonksiyonun çağrıldığı nesneyi döndürmek için kullanılabilir. Bu, fonksiyonların zincirleme (chaining) şeklinde çağrılmasını sağlar ve kodun daha sade ve anlaşılır olmasına yardımcı olur.

```CPP
class MyClass {
    int x;

public:
    MyClass& setX(int x) {
        this->x = x;
        return *this; // Nesneyi döndürür.
    }
};

int main() {
    MyClass obj;
    obj.setX(5).setX(10); // Zincirleme fonksiyon çağrısı.
}

```

3. **İç içe (nested) sınıf kullanımı:** this işaretçisi, iç içe (nested) sınıfların dış sınıfın özelliklerine ve fonksiyonlarına erişmesine olanak tanır.

```CPP
class Outer {
    int x;

public:
    class Inner {
    public:
        void setX(Outer& outer, int x) {
            outer.x = x; // Dış sınıfın "x" üye değişkenine erişim.
        }
    };
};

```

# Special Member Functions

- C++ dilinde, özel üye fonksiyonlar (special member functions) olarak adlandırılan beş temel üye fonksiyon vardır. Bu fonksiyonlar, sınıfların temel davranışlarını kontrol eder ve derleyici tarafından otomatik olarak oluşturulabilir. Özel üye fonksiyonlar şunlardır:

1. **Constructor (Yapıcı):** Bir nesne oluşturulduğunda çağrılan fonksiyondur. Yapıcı, nesnenin başlangıç durumunu ayarlamak ve kaynakları başlatmak için kullanılır. Yapıcılar, sınıf adıyla aynı ada sahip olup, herhangi bir dönüş türüne sahip değildir.

```CPP
class MyClass {
public:
    MyClass() {
        // Yapıcı fonksiyon
    }
};

```

2. **Destructor (Yıkıcı):** Bir nesne ömrünü tamamladığında ve bellekten kaldırılmadan önce çağrılan fonksiyondur. Yıkıcı, nesne tarafından kullanılan kaynakları serbest bırakmak ve nesnenin son durumunu temizlemek için kullanılır. Yıkıcılar, sınıf adının önüne bir tilde (~) işareti eklenerek tanımlanır ve herhangi bir dönüş türüne sahip değildir.

```CPP
class MyClass {
public:
    ~MyClass() {
        // Yıkıcı fonksiyon
    }
};

```
3. **Copy Constructor (Kopyalama Yapıcısı):** Bir nesnenin başka bir nesneyi kopyalayarak oluşturulması durumunda çağrılır. Kopyalama yapıcısı, derin kopyalama işlemini yönetmek ve kaynak nesneden yeni nesneye doğru bir şekilde veri aktarmak için kullanılır.

```CPP
class MyClass {
public:
    MyClass(const MyClass& other) {
        // Kopyalama yapıcısı
    }
};

```

4. **Copy Assignment Operator (Kopyalama Atama Operatörü):** Bir nesneye başka bir nesnenin değerini atamak için kullanılır. Kopyalama atama operatörü, derin kopyalama işlemini yönetir ve kaynak nesneden hedef nesneye doğru bir şekilde veri aktarmak için kullanılır.

```CPP
class MyClass {
public:
    MyClass& operator=(const MyClass& other) {
        // Kopyalama atama operatörü
        return *this;
    }
};

```

5. **Move Constructor (Taşıma Yapıcısı) ve Move Assignment Operator (Taşıma Atama Operatörü):** C++11'den itibaren, taşıma semantiği eklenmiştir. Taşıma yapıcısı ve taşıma atama operatörü, nesneler arasında kaynakları etkin bir şekilde taşımak için kullanılır. Bu, büyük veri yapılarını kopyalamak yerine, kaynakları doğrudan bir nesneden diğerine aktararak performansı artırır.

```CPP
class MyClass {
public:
    // Taşıma yapıcısı
    MyClass(MyClass&& other) noexcept {
        // Taşıma yapıcısı içinde kaynakları etkin bir şekilde taşıma işlemini gerçekleştirin
    }

    // Taşıma atama operatörü
    MyClass& operator=(MyClass&& other) noexcept {
        // Taşıma atama operatörü içinde kaynakları etkin bir şekilde taşıma işlemini gerçekleştirin
        return *this;
    }
};

```

> Özel üye fonksiyonlar, C++ dilinde sınıfların temel davranışlarını yönetir. Yapıcı ve yıkıcı fonksiyonlar, nesne ömrü boyunca kaynakları başlatma ve temizleme işlemleri için kullanılırken, kopyalama ve taşıma yapıcıları ve atama operatörleri, nesneler arasında veri ve kaynakları doğru bir şekilde aktarmak için kullanılır. Bu fonksiyonlar, nesne yönelimli programlamada temel performans ve kaynak yönetimi özelliklerini sağlar.

# Static Initialization Fiasco

- Static initialization fiasco, C++ programlarında karşılaşılan bir başlatma sırası problemdir. Bu sorun, birden fazla dosya veya modül içinde bulunan ve birbirine bağımlı olan global veya statik nesnelerin başlatma sırası belirsizliğinden kaynaklanır. Başlatma sırası belirsizliği, programın hatalı veya öngörülemeyen davranışlara yol açmasına neden olabilir.

- Örnek olarak, iki farklı dosya içinde birbirine bağımlı global nesneler düşünelim:

```CPP
// File1.cpp
#include "A.h"
#include "B.h"

A a;
B b(a);

// File2.cpp
#include "A.h"
#include "B.h"

B b2(a);
A a2;

```

> Bu durumda, File1 ve File2 içinde bulunan a, b, a2 ve b2 nesnelerinin başlatma sırası belirsizdir. Böylece, bağımlılıklar nedeniyle b nesnesi, a nesnesi başlatılmadan önce başlatılabilir ve bu da hatalı veya öngörülemeyen davranışlara neden olabilir.

- Static initialization fiasco sorununu çözmek için bazı yöntemler şunlardır:

1. **Construct on first use (İlk kullanımda inşa etme) yöntemi:** Bu yöntem, statik ve global nesnelerin başlatılmasını, ilk kullanım sırasında yaparak belirsizlikten kaçınmayı sağlar. Bu yöntem, fonksiyonlar içinde yerel statik nesneler kullanarak uygulanır.

```CPP
class A;

A& getInstanceA() {
    static A a;
    return a;
}

class B;

B& getInstanceB() {
    static B b(getInstanceA());
    return b;
}

```

2. **Başlatma sırasını kontrol etme:** Başlatma sırası belirsizliğinden kaçınmak için, programın başlangıcında tüm statik ve global nesnelerin başlatılmasını kontrol eden bir başlatma fonksiyonu kullanılabilir. Bu yöntem, daha büyük projelerde uygulanması zor olabilir ve genellikle uygulanması daha karmaşıktır.

- Static initialization fiasco, global ve statik nesnelerin başlatma sırası belirsizliğinden kaynaklanan bir sorundur. Bu sorunun üstesinden gelmek için, nesnelerin başlatılmasını ilk kullanım sırasında yaparak veya başlatma sırasını kontrol eden bir başlatma fonksiyonu kullanarak başlatma sırası belirsizliğinden kaçınabilirsiniz.

# Dinamik Ömürlü Nesne

- Dinamik ömürlü nesneler, C++ programlarında çalışma zamanında (runtime) oluşturulan ve yönetilen nesnelerdir. Dinamik ömürlü nesneler, programcının ihtiyaçlarına göre oluşturulabilir ve yok edilebilir. Bellekteki yeri (heap alanında) ve yaşam süresi, programın akışına bağlı olarak değişir. Dinamik ömürlü nesneler, new ve delete anahtar kelimeleri (C++11'den itibaren new ve delete yerine akıllı işaretçiler (smart pointers) kullanılması önerilir) kullanılarak oluşturulur ve yönetilir.

- Dinamik ömürlü nesnelerin avantajları şunlardır:

1. **Esneklik:** Dinamik ömürlü nesneler, çalışma zamanında programın ihtiyaçlarına göre oluşturulabilir ve yok edilebilir. Bu, bellek kullanımını optimize etmeye ve programın performansını artırmaya yardımcı olur.

2 **Bellek yönetimi:** Dinamik ömürlü nesneler, bellek alanında (heap) yer kaplar ve bu alan, programın çalışması sırasında yönetilir. Bu, programcının bellek kullanımını daha etkili bir şekilde kontrol etmesine olanak tanır.

3 **Büyük nesneler ve veri yapıları:** Dinamik ömürlü nesneler, büyük nesnelerin ve veri yapılarının oluşturulmasını ve yönetilmesini sağlar. Bu nesneler, statik veya otomatik ömürlü nesnelere göre daha esnek ve etkili bir şekilde kullanılabilir.

- Dinamik ömürlü nesnelerin oluşturulması ve yönetilmesi şu şekildedir:

```CPP
// Nesne oluşturma
MyClass* obj = new MyClass();

// Nesne kullanımı
obj->myMethod();

// Nesne yok etme
delete obj;

```

- C++11'den itibaren, akıllı işaretçiler (smart pointers) kullanılarak dinamik ömürlü nesnelerin yönetimi daha güvenli ve kolay hale getirilmiştir. Örneğin, std::unique_ptr ve std::shared_ptr gibi akıllı işaretçiler, otomatik olarak nesnenin yaşam süresini yönetir ve bellek sızıntılarını önlemeye yardımcı olur.

```CPP
// Nesne oluşturma ve yönetme (unique_ptr kullanarak)
std::unique_ptr<MyClass> obj = std::make_unique<MyClass>();

// Nesne kullanımı
obj->myMethod();

// Nesne yok etme (unique_ptr otomatik olarak nesneyi yok eder)

```

> Sonuç olarak, dinamik ömürlü nesneler, C++ programlarında çalışma zamanında oluşturulan ve yönetilen nesnelerdir.

# New ve Delete

- C++ dilinde, new ve delete anahtar kelimeleri, dinamik ömürlü nesnelerin oluşturulması ve yönetilmesi için kullanılır. new ve delete, bellekteki heap alanında nesnelerin yaşam süresini kontrol etmeye yardımcı olur. Dinamik ömürlü nesnelerin kullanımı, çalışma zamanında bellek ayırma ve kullanma esnekliği sağlar.

- **new operatörü:**

1. **Bellek ayırma:** new operatörü, heap üzerinde istenen boyutta bellek ayırır. Bellek ayırma başarılı olduğunda, ayrılan bellek bloğunun başlangıç adresini döndürür. Bellek ayırma başarısız olursa, std::bad_alloc exception'ı fırlatır.
2. **Nesne başlatma:** new operatörü ayrıca, ayrılan bellekte oluşturulan nesnenin başlatılması için uygun yapılandırıcıyı (constructor) çağırır.

- new operatörünün kullanımı şu şekildedir:

```CPP
MyClass* obj = new MyClass(); // Nesne oluşturma ve başlatma

```
- **delete operatörü:**

**Nesne sonlandırma:** delete operatörü, önceden new ile oluşturulan nesnenin sonlandırılması için uygun yıkıcıyı (destructor) çağırır.
**Bellek serbest bırakma:** delete operatörü, nesnenin heap üzerinde kapladığı belleği serbest bırakır.

- delete operatörünün kullanımı şu şekildedir:
```CPP
delete obj; // Nesne sonlandırma ve bellek serbest bırakma

```
- C++11'den itibaren, dinamik ömürlü nesnelerin yönetimi için akıllı işaretçiler (smart pointers) kullanılması önerilir. Akıllı işaretçiler, otomatik olarak nesnenin yaşam süresini yönetir ve bellek sızıntılarını önlemeye yardımcı olur. std::unique_ptr, std::shared_ptr ve std::weak_ptr gibi akıllı işaretçiler kullanarak, new ve delete operatörlerinin doğrudan kullanımı yerine daha güvenli ve otomatik yaşam süresi yönetimi sağlanabilir.

- Özetle, new ve delete operatörleri, C++ programlarında dinamik ömürlü nesnelerin oluşturulması, başlatılması, sonlandırılması ve bellek serbest bırakılması için kullanılır. Bu operatörler, çalışma zamanında bellek ayırma ve kullanma esnekliği sağlar. C++11'den itibaren, akıllı işaretçilerin kullanılmasıyla dinamik ömürlü nesnelerin yönetimi daha güvenli ve kolay hale getirilmiştir.

# Constructor ve Destructor

- Constructor ve destructor, C++ sınıflarında nesnelerin yaşam sürecini yöneten özel üye fonksiyonlardır. Constructor'lar, nesne oluşturulduğunda çağrılır ve nesnenin başlatılmasını sağlar. Destructor'lar ise, nesne ömrünün sonunda çağrılır ve nesnenin kaynaklarını temizlemek için kullanılır.

**Constructor (Yapılandırıcı):**

1. **Başlatma:** Constructor, bir sınıfın nesnesi oluşturulduğunda otomatik olarak çağrılır. Nesnenin veri üyeleri ve bazı durumlarda temel sınıfın veri üyeleri başlatılır.
2. **Overloading:** Constructor'lar birden fazla parametreli ve parametresiz versiyona sahip olabilir. Bu sayede farklı başlatma senaryoları için farklı constructor'lar kullanılabilir.
3. **İsimlendirme:** Constructor'ın adı, sınıfın adıyla aynı olmalıdır. Constructor'lar herhangi bir geri dönüş tipine sahip değildir.
4. **Delegating constructor:** C++11'den itibaren, bir constructor diğer bir constructor'ı çağırarak nesne başlatma işlemini başka bir constructor'a devredebilir.

- Constructor örneği:

```CPP
class MyClass {
public:
    // Parametresiz constructor
    MyClass() {
        // Nesne başlatma işlemleri
    }

    // Parametreli constructor
    MyClass(int value) {
        // Nesne başlatma işlemleri
    }
};

```

**Destructor (Yıkıcı):**

1. **Temizleme:** Destructor, bir sınıfın nesnesi yaşam süresinin sonunda otomatik olarak çağrılır. Nesnenin kaynaklarını serbest bırakma ve temizleme işlemleri için kullanılır.
2. **İsimlendirme:** Destructor'ın adı, sınıfın adıyla aynı olmalıdır, ancak başında bir tilde (~) bulunur. Destructor'lar herhangi bir geri dönüş tipine ve parametreye sahip değildir.
3. **Tekil:** Bir sınıfın yalnızca tek bir destructor'u olabilir.
Destructor örneği:

```CPP
class MyClass {
public:
    // Constructor
    MyClass() {
        // Nesne başlatma işlemleri
    }

    // Destructor
    ~MyClass() {
        // Nesne kaynaklarını temizleme ve serbest bırakma işlemleri
    }
};

```
- Özetle, constructor ve destructor, C++ sınıflarında nesnelerin yaşam sürecini yöneten özel üye fonksiyonlardır. Constructor'lar, nesnenin başlatılması ve veri üyelerinin değer ataması için kullanılırken, destructor'lar nesnenin ömrünün sonunda çağrılır ve kaynakların temizlenmesi ve serbest bırakılması için kullanılır. 

# Move Semantics

- C++ programlama dilinde move semantics (taşıma semantiği), nesnelerin veri içeriğini bir yerden diğerine daha verimli bir şekilde aktarmayı sağlayan bir özelliktir. Move semantics, C++11 standardıyla birlikte tanıtılmıştır ve daha önceki C++ standartlarında yapılan kopyalama işlemlerinin performansını büyük ölçüde artırır. Bu özellik, özellikle büyük veri yapılarını veya kaynakları yöneten nesneler söz konusu olduğunda önemlidir.

- Taşıma semantiği, sınıflar için hareket (move) yapıcıları ve hareket (move) atama operatörlerini tanımlayarak uygulanır. Bu fonksiyonlar, nesnelerin içeriğini başka nesnelere aktarırken, kaynak nesnenin içeriğini hareketsiz (moved-from) bir duruma getirir. Bu, kaynak nesnenin içeriğinin kopyalanmasına gerek kalmadan, başka nesnelere aktarılmasını sağlar.

- Move semantics örneği:

```CPP
#include <iostream>
#include <vector>

class MyBigData {
public:
    std::vector<int> data;

    // Move constructor (hareket yapıcısı)
    MyBigData(MyBigData&& other) noexcept : data(std::move(other.data)) {
        std::cout << "Move constructor called" << std::endl;
    }

    // Move assignment operator (hareket atama operatörü)
    MyBigData& operator=(MyBigData&& other) noexcept {
        if (this != &other) {
            data = std::move(other.data);
            std::cout << "Move assignment operator called" << std::endl;
        }
        return *this;
    }
};

int main() {
    MyBigData obj1;
    obj1.data = {1, 2, 3, 4, 5};

    // Move constructor kullanımı
    MyBigData obj2(std::move(obj1));
    
    // Move assignment operator kullanımı
    MyBigData obj3;
    obj3 = std::move(obj2);

    return 0;
}

```

> Bu örnekte, MyBigData sınıfı için hareket yapıcı ve hareket atama operatörü tanımlanmıştır. Bu sayede, MyBigData nesnelerinin içeriği, kaynak nesnenin içeriğini hareketsiz (moved-from) bir duruma getirerek, başka nesnelere aktarılabilir. Bu, büyük veri yapılarının veya kaynakların yönetimini daha verimli hale getirir.

- Özetle, move semantics (taşıma semantiği), C++ programlama dilinde nesnelerin içeriğini daha verimli bir şekilde başka nesnelere aktarmayı sağlayan bir özelliktir. Bu özellik, özellikle büyük veri yapıları veya kaynakları yöneten nesneler için önemlidir. Taşıma semantiği, hareket yapıcıları ve hareket atama operatörleri kullanarak uygulanır.

# Delegating Constructor

- C++ programlama dilinde delegating constructor (delege eden yapıcı), bir sınıfın diğer yapıcılarından birine yönlendirilmiş olduğu yapıcı fonksiyondur. Bu özellik, C++11 standardıyla birlikte tanıtılmıştır. Delegating constructor, kod tekrarını önlemeye yardımcı olur ve sınıf yapıcılarını daha düzenli ve yönetilebilir hale getirir.

- Bir delegating constructor, başka bir yapıcıyı çağırarak başlar ve diğer yapıcıda tanımlanan ortak işlemleri gerçekleştirir. Bu şekilde, ortak işlemler tek bir yapıcıda tanımlanarak, sınıfın diğer yapıcılarının bu ortak işlemleri tekrar etmesine gerek kalmaz.

- Delegating constructor örneği:

```CPP
#include <iostream>
#include <string>

class Employee {
private:
    std::string name;
    int age;

public:
    // Ortağı Yapıcı (Common constructor)
    Employee(const std::string& name, int age) : name(name), age(age) {
        std::cout << "Common constructor called" << std::endl;
    }

    // Delege Eden Yapıcı (Delegating constructor)
    Employee(const std::string& name) : Employee(name, 0) {
        std::cout << "Delegating constructor called" << std::endl;
    }
};

int main() {
    // Delege eden yapıcı kullanımı
    Employee emp("John Doe");

    return 0;
}

```
> Bu örnekte, Employee sınıfı için bir delege eden yapıcı tanımlanmıştır. Employee(const std::string& name) yapıcısı, ortak yapıcı Employee(const std::string& name, int age)'yi çağırarak başlar. Bu şekilde, ortak yapıcıdaki işlemler, delege eden yapıcı tarafından tekrar edilmeye gerek kalmadan gerçekleştirilir.

- Özetle, delegating constructor (delege eden yapıcı), C++ programlama dilinde bir sınıfın diğer yapıcılarından birine yönlendirilmiş olduğu yapıcı fonksiyondur. Bu özellik, kod tekrarını önlemeye yardımcı olur ve sınıf yapıcılarını daha düzenli ve yönetilebilir hale getirir. Delegating constructor, başka bir yapıcıyı çağırarak başlar ve diğer yapıcıda tanımlanan ortak işlemleri gerçekleştirir.

# Temporary Objects

- C++ programlama dilinde temporary objects (geçici nesneler), fonksiyonlardan dönen değerlerin veya ifadelerin sonuçlarının saklandığı özel nesnelerdir. Geçici nesneler, özellikle fonksiyonların döndüğü değerleri başka nesnelere atamak veya sınıfların ve yapıların birbirleriyle etkileşimlerini yönetmek için kullanılır. Geçici nesneler, kullanımlarının ardından hemen yok edilirler ve bunlar, bellek yönetimi ve performans açısından önemlidir.

- Geçici nesnelerin birkaç önemli özelliği şunlardır:

1. Ömürleri: Geçici nesnelerin ömürleri kısa ve sınırlıdır. Genellikle, ifadelerin sonucu olarak oluşturuldukları satırda yok edilirler. Ancak, bunlar bir referansa bağlanarak ömürleri uzatılabilir.
2. Değişmezlik (constness): Geçici nesneler, genellikle const olarak kabul edilir. Bu, geçici nesnelerin değerlerinin doğrudan değiştirilemeyeceği anlamına gelir. Ancak, bu kısıtlama const_cast ile aşılabilir.
3. Bellek yönetimi: Geçici nesneler, bellek yönetimi ve performans açısından önemlidir. Geçici nesneler, sınıf ve yapı nesnelerinin kopyalarını oluşturmak ve yönetmek için kullanılır. Bu nesneler, değerleri diğer nesnelere atandıktan sonra hemen yok edilir.
- Temporary objects örneği:

```CPP
#include <iostream>
#include <string>

class MyString {
public:
    std::string str;

    MyString(const std::string& s) : str(s) {}
};

MyString getFullName(const std::string& firstName, const std::string& lastName) {
    return MyString(firstName + " " + lastName);
}

int main() {
    // Geçici nesnenin oluşturulması ve kullanılması
    std::string fullName = getFullName("John", "Doe").str;
    std::cout << "Full Name: " << fullName << std::endl;

    return 0;
}

```
> Bu örnekte, getFullName fonksiyonu, MyString sınıfından bir nesne döndürür. Bu nesne, firstName ve lastName değerlerini birleştirerek oluşturulur ve bu işlem sonucu bir geçici nesne olarak döndürülür. Ardından, bu geçici nesnenin str üyesi, fullName değişkenine atanır ve geçici nesne yok edilir.

# Reference Qualifiers

- C++ programlama dilinde reference qualifiers (referans nitelikleri), üye fonksiyonlar için bir özelliktir ve bu özellik, sınıf nesnelerinin hangi tür referanslarla çağrılacağını belirtir. C++11 standardı ile tanıtılan reference qualifiers, üye fonksiyonların sadece lvalue nesneleri veya rvalue nesneleri üzerinde çalışmasını sağlar.

- Bir üye fonksiyonun sonuna & veya && referans nitelikleri eklenerek, bu fonksiyonun yalnızca lvalue veya rvalue referanslarını kabul etmesi sağlanır. Bu şekilde, fonksiyonun sınıf nesneleri üzerinde çalışma şekli daha iyi kontrol edilir ve optimize edilir.

- Reference qualifiers örneği:
```CPP
#include <iostream>

class MyString {
public:
    std::string str;

    MyString(const std::string& s) : str(s) {}

    // Üye fonksiyon için lvalue reference qualifier
    void print() & {
        std::cout << "lvalue version: " << str << std::endl;
    }

    // Üye fonksiyon için rvalue reference qualifier
    void print() && {
        std::cout << "rvalue version: " << str << std::endl;
    }
};

int main() {
    MyString myStr("Hello, World!");

    // lvalue nesne
    myStr.print(); // lvalue versiyonu çağrılır

    // rvalue nesne
    MyString("Temporary").print(); // rvalue versiyonu çağrılır

    return 0;
}

```
> Bu örnekte, MyString sınıfının print üye fonksiyonu için hem lvalue hem de rvalue referans nitelikleri kullanılmıştır. Böylece, print fonksiyonu lvalue nesneleri üzerinde çalışırken farklı bir davranış sergilerken, rvalue nesneleri üzerinde çalışırken başka bir davranış sergilemektedir.

- Özetle, reference qualifiers (referans nitelikleri), C++ programlama dilinde üye fonksiyonlar için bir özelliktir ve bu özellik, sınıf nesnelerinin hangi tür referanslarla çağrılacağını belirtir. Bu sayede, fonksiyonun sınıf nesneleri üzerinde çalışma şekli daha iyi kontrol edilir ve optimize edilir.

# Conversion Constructor

- C++ programlama dilinde conversion constructor (dönüşüm yapıcısı), belirli bir türden başka bir türe otomatik dönüşüm sağlayan özel bir sınıf yapıcısıdır. Dönüşüm yapıcıları, tek parametreli veya belirli varsayılan değerlere sahip daha fazla parametreli yapıcılar olabilir. Bu tür yapıcılar, bir nesnenin bir türden başka bir türe dönüştürülmesi gerektiğinde otomatik olarak çağrılır.

-Dönüşüm yapıcıları, genellikle, bir sınıfın diğer sınıflarla veya temel veri türleriyle daha iyi etkileşime girmesini sağlamak amacıyla kullanılır. C++ dilinde, dönüşüm yapıcısı kullanarak bir sınıf nesnesini başka bir sınıf nesnesine veya temel bir veri türüne dönüştürebiliriz.

**Conversion constructor örneği:**

```CPP
#include <iostream>

class MyInteger {
public:
    int value;

    // Conversion constructor: int -> MyInteger
    MyInteger(int v) : value(v) {}

    // Diğer üye fonksiyonlar...
};

void printMyInteger(const MyInteger& myInt) {
    std::cout << "MyInteger value: " << myInt.value << std::endl;
}

int main() {
    int intValue = 42;

    // Otomatik dönüşüm: int -> MyInteger
    MyInteger myInt = intValue; // MyInteger(int v) dönüşüm yapıcısı çağrılır

    printMyInteger(intValue); // intValue otomatik olarak MyInteger'a dönüşür

    return 0;
}

```

> Bu örnekte, MyInteger sınıfının bir dönüşüm yapıcısı tanımlanmıştır. Bu yapıcı, int türünden MyInteger türüne otomatik dönüşüm sağlar. Bu sayede, int türündeki bir değer MyInteger türündeki bir nesneye doğrudan atanabilir ve fonksiyonlara parametre olarak geçirilebilir.

- Özetle, conversion constructor (dönüşüm yapıcısı), C++ programlama dilinde belirli bir türden başka bir türe otomatik dönüşüm sağlayan özel bir sınıf yapıcısıdır. Bu tür yapıcılar, bir nesnenin bir türden başka bir türe dönüştürülmesi gerektiğinde otomatik olarak çağrılır. Dönüşüm yapıcıları, genellikle, bir sınıfın diğer sınıflarla veya temel veri türleriyle daha iyi etkileşime girmesini sağlamak amacıyla kullanılır.

# Copy Elision

- C++ programlama dilinde copy elision (kopya elenmesi), derleyicinin otomatik olarak kopya oluşturma işlemlerini atlamasına ve doğrudan bir nesnenin değerini başka bir nesneye atamasına olanak tanıyan bir optimizasyon tekniğidir. Bu optimizasyon, kopya yapıcılarının ve atama operatörlerinin çağrılmasını azaltarak programın performansını ve hızını artırır.

**Copy elision, aşağıdaki durumlarda gerçekleşebilir:**

1. Fonksiyon döndürme değeri olarak bir nesne oluşturulduğunda ve bu nesne dışarıda başka bir nesneye atanırken.
2. İç içe geçmiş bir nesne oluşturulduğunda ve bu nesne dışarıdaki nesneye atanırken.
3. Bir nesne, başka bir nesnenin değeriyle başlatıldığında (copy initialization).
4. Bir sınıfın kopya yapıcısının veya atama operatörünün çağrılması gerektiğinde, ancak derleyici bu işlemi doğrudan bir nesnenin değerini başka bir nesneye atayarak yapabilirse.

- C++17 ile birlikte, copy elision için garantiler getirilmiştir. Bu, derleyicinin belirli durumlarda kopya elision gerçekleştirmek zorunda olduğu anlamına gelir. Bu durumlar şunları içerir:

1. Bir nesne, bir fonksiyonun dönüş değeri olarak döndürülürken.
2. Bir nesne, aynı türden başka bir nesnenin değeriyle başlatıldığında.

**Copy elision örneği:**

```CPP
#include <iostream>

class MyInteger {
public:
    int value;

    MyInteger(int v) : value(v) {
        std::cout << "Constructor called" << std::endl;
    }

    MyInteger(const MyInteger& other) : value(other.value) {
        std::cout << "Copy constructor called" << std::endl;
    }
};

MyInteger createMyInteger(int value) {
    return MyInteger(value); // Copy elision: Kopya yapıcı çağrılmayabilir
}

int main() {
    MyInteger myInt = createMyInteger(42); // Copy elision: Kopya yapıcı çağrılmayabilir

    return 0;
}

```
> Bu örnekte, MyInteger sınıfının kopya yapıcısı tanımlanmıştır. Ancak, createMyInteger fonksiyonunun dönüş değeri olarak bir MyInteger nesnesi oluşturulduğunda ve bu nesne myInt adlı nesneye atanırken, derleyici kopya elision gerçekleştirerek kopya yapıcının çağrılmasını atlayabilir.

# Return Value Optimization

- Return Value Optimization (RVO), C++ derleyicilerinde kullanılan bir optimizasyon tekniğidir. Bu teknik, fonksiyonların döndürdüğü nesnelerin kopyalarının oluşturulmasını ve kopya yapıcılarının çağrılmasını önlemeye yöneliktir. RVO'nun amacı, programın performansını ve hızını artırmaktır.

- RVO'nun temel fikri, fonksiyon tarafından döndürülen nesnenin değerini doğrudan çağrı noktasında oluşturulan nesneye aktarmaktır. Böylece, kopya yapıcının çağrılması ve ekstra nesnelerin oluşturulması önlenir. RVO, belirli koşullar altında otomatik olarak derleyici tarafından uygulanabilir ve genellikle programcının müdahalesine gerek duymaz.

- RVO'ya bir örnek olarak şu durumu düşünelim:

```CPP
class MyString {
public:
    MyString(const char* s) { /* ... */ }
    MyString(const MyString& other) { /* ... */ }
    // Diğer üye fonksiyonlar...
};

MyString createMyString() {
    MyString result("Hello, world!");
    return result; // RVO burada uygulanabilir
}

int main() {
    MyString myStr = createMyString(); // RVO burada uygulanabilir
    return 0;
}

```
> Bu örnekte, createMyString fonksiyonu, MyString türünde bir nesne döndürmektedir. Normalde, result nesnesinin değeri bir kopya nesnesine aktarılır ve bu kopya nesne döndürülürdü. Ancak, RVO uygulandığında, derleyici result nesnesinin değerini doğrudan myStr nesnesine aktarabilir. Böylece, kopya yapıcı çağrısı ve ekstra nesne oluşturma işlemi önlenir.

- Özetle, Return Value Optimization (RVO), fonksiyonların döndürdüğü nesnelerin kopyalarının oluşturulmasını ve kopya yapıcılarının çağrılmasını önlemeye yönelik bir optimizasyon tekniğidir. Bu teknik, programın performansını ve hızını artırmaktadır. RVO, belirli koşullar altında otomatik olarak derleyici tarafından uygulanabilir ve genellikle programcının müdahalesine gerek duymaz.

# Static Class Members

- C++ dilinde, statik sınıf üyeleri (static class members), sınıfın tüm nesneleri tarafından paylaşılan sınıf değişkenleri veya fonksiyonlarıdır. Statik sınıf üyeleri, sınıfın her bir nesnesi için ayrı ayrı oluşturulmaz; bunun yerine, tek bir örnek oluşturulur ve tüm nesneler tarafından paylaşılır.

- Statik sınıf üyelerinin kullanımı, aşağıdaki özelliklere sahiptir:

1. **Statik veri üyeleri:** Sınıf içinde static anahtar kelimesiyle tanımlanır. Statik veri üyeleri, sınıfın her bir nesnesi için ayrı ayrı oluşturulmaz, bunun yerine tüm nesneler tarafından paylaşılan tek bir örnek oluşturulur. Bu tür değişkenler, sınıfın tüm nesneleri arasında ortak bir durumu veya değeri temsil etmek için kullanılabilir.

```CPP
class MyClass {
public:
    static int sharedValue; // Statik veri üyesi
};
int MyClass::sharedValue = 0; // Statik veri üyesinin tanımı ve başlatılması

```
2. **Statik üye fonksiyonlar:** Sınıf içinde static anahtar kelimesiyle tanımlanan fonksiyonlardır. Statik üye fonksiyonlar, sınıfın nesnelerinden bağımsız olarak çalışır ve doğrudan sınıf adı üzerinden çağrılabilir. Statik üye fonksiyonlar, sınıfın herhangi bir nesnesi oluşturulmadan önce bile kullanılabilir ve sınıfın statik veri üyelerine erişebilir.

```CPP
class MyClass {
public:
    static int sharedValue;

    static void setSharedValue(int value) { // Statik üye fonksiyonu
        sharedValue = value;
    }
};
int MyClass::sharedValue = 0;

int main() {
    MyClass::setSharedValue(42); // Nesne oluşturulmadan statik üye fonksiyonunu çağırma
    return 0;
}

```

**Statik sınıf üyelerinin önemli özellikleri:**

1. Statik sınıf üyeleri, sınıfın tüm nesneleri tarafından paylaşılır ve sınıfın her bir nesnesi için ayrı ayrı oluşturulmaz.
2. Statik veri üyeleri, sınıfın tüm nesneleri arasında ortak bir durumu veya değeri temsil etmek için kullanılabilir.
3. Statik üye fonksiyonlar, sınıfın nesnelerinden bağımsız olarak çalışır ve doğrudan sınıf adı üzerinden çağrılabilir.
4. Statik üye fonksiyonlar, sınıfın statik veri üyelerine erişebilir, ancak doğrudan this işaretçisine veya sınıfın diğer (statik olmayan) üye değişkenlerine erişemezler.

**Statik sınıf üyelerinin kullanımına ilişkin bazı öneriler ve uygulamalar şunlardır:**

1. Sınıfın tüm nesneleri tarafından paylaşılan ortak bir kaynak veya bilgiyi temsil etmek için statik veri üyeleri kullanılabilir. Örneğin, sınıfın tüm nesneleri için ortak bir sayacı veya yapılandırmayı temsil eden bir değişken olabilir.

2. Sınıfın tüm nesneleri tarafından kullanılacak ortak bir işleve veya algoritmayı tanımlamak için statik üye fonksiyonları kullanılabilir. Bu tür fonksiyonlar, sınıf nesnelerinden bağımsız olarak çalıştığından, sınıfın ortak özelliklerini veya işlevlerini tanımlamak için uygundur.

3. Statik üye fonksiyonlarının sınıfın diğer üye değişkenlerine veya fonksiyonlarına doğrudan erişimi olmadığından, bunları sınıfın genel durumunu veya işlevselliğini etkilemeyecek şekilde tasarlamak önemlidir.

4. Statik sınıf üyelerinin dikkatli kullanılması önemlidir, çünkü doğru kullanıldığında performans ve hafıza kullanımı açısından avantajlar sağlayabilirken, yanlış kullanıldığında sınıfın işlevselliğine ve performansına zarar verebilir.

- Özetle, statik sınıf üyeleri, sınıfın tüm nesneleri tarafından paylaşılan değişkenler veya fonksiyonlar olup, sınıfın her bir nesnesi için ayrı ayrı oluşturulmazlar. Statik veri üyeleri ve statik üye fonksiyonlar, sınıfın ortak durumunu ve işlevselliğini temsil etmek için kullanılabilir. Bu tür üyelerin doğru ve dikkatli kullanılması, programın performansını ve hafıza kullanımını optimize etmeye yardımcı olabilir.

# Inline Variable

- C++17 ile tanıtılan inline değişkenler, birden fazla kaynak dosyasında aynı değişkenin tanımlanmasına ve kullanılmasına izin veren değişkenlerdir. İnline değişkenler, sınıf ve fonksiyon şablonlarındaki ve header-only kütüphanelerindeki kodun organize edilmesini ve genel kullanımını daha iyi hale getirir. İnline değişkenler, inline anahtar kelimesiyle tanımlanır.

**inline değişkenlerin kullanımı, aşağıdaki özelliklere sahiptir:**

1. Tek bir adres: İnline değişkenler, tüm kaynak dosyaları boyunca aynı adresi paylaşır. Bu, birden fazla kaynak dosyasında aynı değişkenin tanımlanmasına ve kullanılmasına olanak sağlar ve bağlayıcı (linker) hatalarını önler.

2. Statik süreli ömür: İnline değişkenler, statik süreli ömre sahiptir. Bu, programın başlangıcından sonuna kadar hayatta kalacakları ve her kaynak dosyasında aynı değeri tutacakları anlamına gelir.

3. İnline değişkenlerin tanımı, tanımlandığı her kaynak dosyasında görünür olmalıdır. Bu, genellikle ilgili değişkenin tanımını bir başlık dosyasında (header file) yaparak sağlanır.

**İnline değişkenlere basit bir örnek şöyledir:**
- my_global.h:

```CPP
#pragma once
#include <iostream>

inline int globalVar = 42;

```
- main.cpp:

```CPP
#include "my_global.h"

int main() {
    std::cout << "Global variable: " << globalVar << std::endl;
    return 0;
}

```

- another_file.cpp:

```CPP
#include "my_global.h"

void someFunction() {
    globalVar++; // İnline değişkeni başka bir kaynak dosyasında kullanma
}

```

- Bu örnekte, globalVar adlı inlinedeğişken, my_global.h başlık dosyasında tanımlanmıştır. Bu değişken, main.cpp ve another_file.cpp kaynak dosyalarında kullanılır ve her iki dosya için de aynı adresi paylaşır.

- Özetle, inline değişkenler, birden fazla kaynak dosyasında aynı değişkenin tanımlanmasına ve kullanılmasına izin veren değişkenlerdir. İnline değişkenler, statik süreli ömre sahiptir ve tüm kaynak dosyaları boyunca aynı adresi paylaşır. İnline değişkenler, sınıf ve fonksiyon şablonlarındaki ve header-only kütüphanelerindeki kodun organize edilmesini ve genel kullanımını daha iyi hale getirir.

# Friend Keyword

- C++'da, friend anahtar kelimesi, bir sınıfın private ve protected üye değişkenlerine ve fonksiyonlarına başka bir sınıfın veya fonksiyonun erişim sağlamasına izin veren bir mekanizma sunar. Bu, sınıflar arasındaki ilişkiyi daha esnek hale getirir ve veri saklama ve işleme için daha etkili yollar sunar. friend kullanımı dikkatli ve ölçülü olmalıdır, çünkü sınıfın dışındaki kodların doğrudan sınıf üyelerine erişmesine izin vererek, sınıfın soyutlamasını ve kapsüllemesini zayıflatabilir.

- friend ilişkisi aşağıdaki şekillerde kurulabilir:

1. **Friend fonksiyonlar:** Bir sınıfın, diğer sınıfların veya global fonksiyonların private ve protected üye değişkenlerine ve fonksiyonlarına erişmesine izin vermek için, bu fonksiyonları sınıfın içinde friend anahtar kelimesi ile tanımlayabilirsiniz.

```CPP
class MyClass {
private:
    int secretData;

public:
    MyClass(int data) : secretData(data) {}

    friend void accessSecretData(MyClass& obj);
};

void accessSecretData(MyClass& obj) {
    std::cout << "Secret data: " << obj.secretData << std::endl;
}
```

> Bu örnekte, accessSecretData fonksiyonu MyClass sınıfının friend fonksiyonu olarak tanımlanmıştır ve böylece MyClass'ın private üye değişkeni olan secretData'ya erişebilir.

2. **Friend sınıflar:** Bir sınıfın, diğer bir sınıfın private ve protected üye değişkenlerine ve fonksiyonlarına erişmesine izin vermek için, ilgili sınıfı friend olarak tanımlayabilirsiniz.

```CPP
class MyClassA {
private:
    int secretData;

public:
    MyClassA(int data) : secretData(data) {}

    friend class MyClassB;
};

class MyClassB {
public:
    void accessSecretData(MyClassA& obj) {
        std::cout << "Secret data: " << obj.secretData << std::endl;
    }
};

```
> Bu örnekte, MyClassB sınıfı, MyClassA sınıfının friend sınıfı olarak tanımlanmıştır ve böylece MyClassA'nın private üye değişkeni olan secretData'ya erişebilir.

- friend anahtar kelimesi kullanılırken dikkatli olunmalıdır, çünkü sınıfın kapsüllemesini zayıflatabilir ve yanlış kullanım durumunda, sınıfın iç yapısını dışarıya açarak olumsuz etkilere yol açabilir. Friend fonksiyonlar ve sınıflar, gerçekten gerektiğinde ve iki sınıf arasında güçlü bir ilişki olduğunda kullanılmaldır. Özetle, friend anahtar kelimesinin kullanımı aşağıdaki avantajlara sahiptir:

1. **Daha iyi performans:** Friend fonksiyonlar ve sınıflar, doğrudan sınıfın private ve protected üyelerine erişebilir, böylece getter ve setter gibi ekstra fonksiyon çağrıları yapmaya gerek kalmadan işlemleri gerçekleştirebilir. Bu, özellikle karmaşık veri yapılarında performansı artırabilir.
2. **Sınıf ilişkilerinin tanımlanması:** Friend ilişkisi, sınıflar arasındaki ilişkileri belirgin hale getirir ve bu, kodun anlaşılmasını ve bakımını kolaylaştırır.
3. **Sınıflar arasında işbirliği:** Friend anahtar kelimesi, sınıfların birbirleriyle veri alışverişi yapmasına ve birbirlerinin üyelerini kullanmasına izin verir. Bu, veri işleme ve saklamada daha etkili ve uyumlu yollar sağlar.

- Ancak, friend mekanizmasını kullanırken aşağıdaki hususlara dikkat etmelisiniz:

1. **Kapsülleme ihlali:** Friend anahtar kelimesi, sınıfın soyutlamasını ve kapsüllemesini zayıflatabilir. Bu nedenle, friend kullanımını gerektiğinde ve kontrollü bir şekilde kullanmak önemlidir.

2. **Kodun bakımı:** Friend ilişkisi, sınıflar arasında daha güçlü bağımlılıklar yaratabilir ve bu, kodun bakımını zorlaştırabilir. Bu nedenle, friend mekanizmasını gerektiğinde ve doğru bir şekilde kullanmak önemlidir.

3. **Sınıf tasarımı:** Friend anahtar kelimesini kullanırken, iyi bir sınıf tasarımı ve uygun veri saklama ve işleme stratejileri uygulamak önemlidir. Friend kullanımı, sınıf tasarımının eksikliklerini veya veri saklama ve işleme stratejilerinin yanlış uygulanmasını gizlememelidir.

- Sonuç olarak, friend anahtar kelimesi, C++'da sınıfların ve fonksiyonların birbirlerinin private ve protected üyelerine erişmesine izin veren güçlü bir mekanizmadır. Friend mekanizması, dikkatli ve ölçülü kullanıldığında, performansı artırabilir, sınıf ilişkilerini belirginleştirebilir ve sınıflar arasında işbirliği sağlayabilir. Ancak, kullanımı kapsüllemeyi zayıflatabilir ve kodun bakımını zorlaştırabilir, bu nedenle dikkatli bir şekilde kullanılması önemlidir.

# Tur Donusturme Operator Fonksiyonlari

- C++'da, tür dönüşümü operatör fonksiyonları (type conversion operator functions), kullanıcı tanımlı sınıfların belirli bir türden başka bir türe dönüştürülmesini sağlar. Bu, bir sınıf nesnesinin başka bir türdeki değeri ifade etmesi için kullanılır ve bu sayede sınıflar arası dönüşümler ve sınıf ile temel türler arasındaki dönüşümler gerçekleştirilir.

- Tür dönüşümü operatör fonksiyonları, sınıfın içinde tanımlanır ve operator anahtar kelimesi ile başlar, ardından dönüştürülecek hedef tür gelir. Bu tür fonksiyonlar, genellikle tek başına kullanılır ve herhangi bir argüman kabul etmez.

- Örnek olarak, bir Complex sınıfınız olduğunu ve bunu double türüne dönüştürmek istediğinizi düşünün:

```CPP
class Complex {
private:
    double real;
    double imag;

public:
    Complex(double r, double i) : real(r), imag(i) {}

    // Tür dönüşümü operatörü (Complex -> double)
    operator double() const {
        return real;
    }
};

int main() {
    Complex c1(3.0, 4.0);

    // Complex sınıfından double türüne dönüşüm
    double d1 = c1;

    std::cout << "Double: " << d1 << std::endl;
}

```
> Bu örnekte, Complex sınıfında tanımlanan operator double() tür dönüşümü operatör fonksiyonu sayesinde, Complex nesnesi double türüne dönüştürülebilir. main fonksiyonunda, Complex nesnesi c1'i double türündeki d1 değişkenine atarken, tür dönüşümü operatörü kullanılır.

- Tür dönüşümü operatörlerinin kullanımı, kodu daha okunaklı hale getirebilir ve kullanıcı tanımlı sınıfların temel türlerle veya diğer sınıflarla doğal ve sezgisel bir şekilde etkileşime girmesini sağlar. Ancak, tür dönüşümü operatörlerini dikkatlice ve ihtiyatla kullanmak önemlidir, çünkü otomatik dönüşümler beklenmedik sonuçlara veya hatalara yol açabilir.

- Tür dönüşümü operatörlerinin dikkatli kullanımı şunları içerir:

1. **Anlamlı dönüşümler:** Yalnızca gerçekten anlamlı ve mantıklı olan tür dönüşümlerini sağlamak önemlidir. Örneğin, Complex sınıfı için yalnızca reel kısmı döndüren bir dönüşüm sağlamak, karmaşık sayının imajiner kısmını göz ardı ettiğinden bazı durumlarda doğru olmayabilir. Bu nedenle, tür dönüşümlerinin kullanım amacına ve sınıfın temsil ettiği değerlere uygun olduğundan emin olun.

2. **Dönüşümün doğruluğunu ve güvenliğini sağlama:** Dönüşüm sırasında veri kaybı yaşanmaması veya değerlerin yanlış yorumlanmaması için dikkatli olun. Özellikle, farklı boyutlara sahip veri türleri arasında dönüşüm yaparken (örneğin, 32 bitlik bir tamsayıdan 64 bitlik bir tamsayıya) bu önemlidir.

3. **Aşırı yükleme çözümlemesine dikkat etme:** Tür dönüşümü operatörlerinin varlığı, fonksiyon aşırı yüklemesinde beklenmedik seçimlere yol açabilir. Bu nedenle, aşırı yüklenmiş fonksiyonların ve tür dönüşümü operatörlerinin bir arada kullanılması durumunda dikkatli olun.

4. **Açık dönüşüm kullanmayı düşünme:** Bazen, otomatik tür dönüşümü yerine açık tür dönüşümü kullanmak daha iyi olabilir. Açık dönüşüm, static_cast, dynamic_cast, const_cast ve reinterpret_cast gibi C++ dilinde mevcut dönüşüm operatörlerini kullanarak gerçekleştirilir. Bu, dönüşümün gerçekleştiği yeri belirgin hale getirir ve potansiyel hataları önlemeye yardımcı olur.

- Sonuç olarak, tür dönüşümü operatör fonksiyonları, kullanıcı tanımlı sınıfların başka bir türe dönüştürülmesine izin veren güçlü bir özelliktir. Bu özellik, kodun okunabilirliğini artırabilir ve sınıfların doğal ve sezgisel bir şekilde etkileşime girmesini sağlar. Ancak, tür dönüşümü operatörlerini dikkatlice ve ihtiyatla kullanmak önemlidir, çünkü otomatik dönüşümler beklenmedik sonuçlara veya hatalara yol açabilir.

# Explicit Keyword

- C++'da explicit anahtar kelimesi, kullanıcı tanımlı bir sınıfın içinde belirli bir tür dönüşümün sadece açıkça belirtildiğinde gerçekleştirilmesini sağlar. Bu, sınıfın temel türlerle veya diğer sınıflarla etkileşimini sınırlandırarak yanlışlıkla gerçekleştirilen tür dönüşümlerini önlemeye yardımcı olur. explicit anahtar kelimesi, sınıfın tek parametreli (veya C++11 ve sonrasında, daha fazla parametreli) yapılandırıcıları ve tür dönüşümü operatörleri ile birlikte kullanılabilir.

- Örnek olarak, bir Complex sınıfınız olduğunu ve bu sınıfın double türünden bir değerle başlatılmasını istemediğinizi düşünün:

```CPP
class Complex {
private:
    double real;
    double imag;

public:
    // Tek parametreli yapılandırıcı, explicit ile işaretlenmiştir
    explicit Complex(double r, double i = 0.0) : real(r), imag(i) {}
};

int main() {
    double d = 3.0;

    // Aşağıdaki satır, yapılandırıcının explicit olduğu için hata verecektir
    // Complex c1 = d; // Hatalı kullanım

    // Aşağıdaki satır, doğru kullanımdır
    Complex c2 = Complex(d); // Açık dönüşüm
}

```
> Bu örnekte, Complex sınıfının tek parametreli yapılandırıcısı explicit anahtar kelimesi ile işaretlenmiştir. Bu nedenle, double değeri ile doğrudan bir Complex nesnesi oluşturulmaya çalışıldığında hata alırsınız. Bunun yerine, açık bir şekilde Complex nesnesi oluşturmanız ve double değerini parametre olarak vermeniz gerekir.

- Benzer şekilde, tür dönüşümü operatörleri için de explicit anahtar kelimesi kullanılabilir:

```CPP
class Complex {
    // ...
public:
    // Tür dönüşümü operatörü, explicit ile işaretlenmiştir
    explicit operator double() const {
        return real;
    }
};

```
- Bu durumda, Complex nesnesini double türüne dönüştürmek için açık bir dönüşüm kullanmanız gerekir:

```CPP
Complex c1(3.0, 4.0);

// Aşağıdaki satır, tür dönüşümü operatörünün explicit olduğu için hata verecektir
// double d1 = c1; // Hatalı kullanım

// Aşağıdaki satır, doğru kullanımdır
double d2 = static_cast<double>(c1); // Açık dönüşüm

```
- explicit anahtar kelimesinin kullanımı, beklenmedik tür dönüşümlerini önlemeye yardımcı olarak, kodun güvenliğini ve doğruluğunu artırır. C++ programlarında, explicit anahtar kelimesini dikkatlice kullanarak, sınıflar arası etkileşimi kontrol etmek ve hatalı dönüşümlerden kaynaklanabilecek sorunları önlemek mümkündür. Bu nedenle, explicit anahtar kelimesi, güçlü bir C++ özelliğidir ve profesyonel düzeyde kod yazarken bu özelliği uygun şekilde kullanmak önemlidir.

- Özetle, explicit anahtar kelimesi:

1 . Yanlışlıkla gerçekleştirilen tür dönüşümlerini önlemeye yardımcı olur.
2. Açık tür dönüşümlerini zorunlu kılarak, kodun okunabilirliğini ve anlaşılabilirliğini artırır.
3. Sınıfların temel türlerle veya diğer sınıflarla etkileşimini sınırlandırarak, daha güvenli ve doğru kodlar yazılmasına olanak tanır.

- explicit anahtar kelimesinin kullanımı, profesyonel düzeyde C++ programlama bilgisi için önemli bir yönüdür ve iyi düzenlenmiş, güvenli ve doğru kodlar yazarken bu özelliği kullanmayı düşünmelisiniz.

# Using namespace

- C++ dilinde, using namespace ifadesi, belirli bir ad alanında (namespace) tanımlanan tüm isimleri ve sembolleri mevcut kapsama alanına (scope) dahil etmeyi sağlar. Bu sayede, ad alanında tanımlanan sınıflara, fonksiyonlara ve değişkenlere, tam adlarını kullanmadan erişilebilir. using namespace ifadesi, kodun okunabilirliğini artırabilir ve tekrar eden kodları azaltabilir, ancak doğru kullanılmadığında ad çakışması gibi sorunlara yol açabilir.

- Bir ad alanının kullanılmasıyla ilgili profesyonel düzeyde detaylar şunları içerir:

1. Ad alanları (Namespaces): Ad alanları, isim çakışmalarını önlemeye yardımcı olan ve kodu düzenleyen bir C++ özelliğidir. Bir ad alanı içinde, sınıflar, fonksiyonlar ve değişkenler tanımlanabilir ve bu semboller, ad alanının adı ile birlikte kullanılabilir.

**Örnek:**
```CPP
namespace MyNamespace {
    void foo() {
        // ...
    }
}

int main() {
    MyNamespace::foo(); // Ad alanını kullanarak foo() fonksiyonunu çağırma
}

```
2. **using namespace kullanımı:** using namespace ifadesi, bir ad alanının tüm isimlerini ve sembollerini mevcut kapsama alanına dahil eder. Bu, ad alanı içinde tanımlanan sınıflara, fonksiyonlara ve değişkenlere, tam adlarını kullanmadan erişmeyi sağlar.

**Örnek:**

```CPP
namespace MyNamespace {
    void foo() {
        // ...
    }
}

int main() {
    using namespace MyNamespace;
    foo(); // using namespace sayesinde, MyNamespace::foo() olarak yazmaya gerek kalmaz
}

```

3. **Dikkatli kullanım:** using namespace ifadesi, ad çakışması gibi sorunlara yol açabileceği için dikkatli kullanılmalıdır. Özellikle, iki veya daha fazla ad alanının aynı kapsama alanında dahil edilmesi ve aynı isimlerle semboller içermesi durumunda, bu tür çakışmalar meydana gelebilir.

- Bu nedenle, using namespace ifadesini küresel kapsamda kullanmaktan kaçının ve yerine fonksiyon veya sınıf düzeyinde kullanmayı düşünün. Ayrıca, kullanımını sınırlamak için belirli sembolleri dahil etmek için using deyimini kullanabilirsiniz:
```CPP
namespace MyNamespace {
    void foo() {
        // ...
    }
}

int main() {
    using MyNamespace::foo;
    foo(); // Sadece foo fonksiyonu dahil edilir, diğer MyNamespace sembolleri dahil edilmez
}

```

# ADL Argument Dependant Lookup

- ADL (Argument Dependent Lookup) veya Koenig Lookup olarak da bilinen, C++ dilinde kullanılan bir isim çözümleme yöntemidir. ADL, bir fonksiyon çağrısı sırasında, fonksiyonun adını çözmek için fonksiyonun parametrelerine bağlı olarak tanımlanmış ad alanlarını (namespaces) arar. Bu sayede, uygun fonksiyonun doğru ad alanında tanımlanmış olduğundan emin olunabilir ve isim çakışmaları önlenmiş olur.

**ADL'nin profesyonel düzeyde detayları şunları içerir:**

1. **ADL'nin amacı:** C++ dilinde, fonksiyonlar ve sınıflar ad alanları içinde tanımlanabilir. ADL, bir fonksiyon çağrısı sırasında, fonksiyonun parametrelerinin türlerine bağlı olarak belirli ad alanlarında arama yaparak, doğru fonksiyonu bulmayı amaçlar. Bu, özellikle aşırı yüklenmiş fonksiyonlar ve sınıf şablonları ile çalışırken yararlıdır.

2. **ADL nasıl çalışır:** ADL, bir fonksiyon çağrısında kullanılan parametrelerin türlerine bakarak, ilgili ad alanlarını belirler. Daha sonra, bu ad alanları içinde fonksiyonun adını arar ve uygun olanı bulursa, fonksiyonu çağırır.

**Örnek:**

```CPP
namespace MyNamespace {
    class MyClass {};

    void foo(MyClass obj) {
        // ...
    }
}

int main() {
    MyNamespace::MyClass obj;
    foo(obj); // ADL sayesinde, MyNamespace::foo() fonksiyonu çağrılır
}

```

3. **ADL ve using deyimi:** using deyimi kullanılarak, belirli bir ad alanı içindeki isimler ve semboller mevcut kapsama alanına dahil edilebilir. Bu durumda, ADL'nin kullanılması gerekmez. Ancak, ADL, doğru fonksiyonun çağrılmasını garantilemek için kullanılan güçlü bir mekanizma olarak kullanılabilir.

4. **ADL'nin sınırlamaları ve dikkatli kullanım:** ADL, isim çözümleme sürecini basitleştirmeye yardımcı olur ve doğru fonksiyonun çağrılmasını sağlar. Ancak, birden fazla ad alanında aynı isimli fonksiyonların bulunması durumunda, ADL kullanılarak hangi fonksiyonun çağrılacağı belirsiz olabilir. Bu nedenle, ADL'yi kullanırken dikkatli olunmalı ve uygun ad alanlarını ve sembolleri kullanarak isim çakışmalarını önlemek için kodun düzenli bir şekilde organize edilmesi önemlidir.

- Sonuç olarak, ADL, C++ dilinde fonksiyyon çağrıları sırasında doğru fonksiyonu bulmak için kullanılan önemli bir isim çözümleme mekanizmasıdır. Özellikle, sınıflar ve fonksiyonlar arasındaki ilişkileri yönetirken ve aşırı yüklenmiş fonksiyonlar ve sınıf şablonlarıyla çalışırken yararlıdır. ADL'nin doğru kullanımı ve anlaşılması, C++ kodunun doğru ve verimli çalışmasını sağlamaya yardımcı olur.

**ADL ile ilgili bazı ek detaylar ve ipuçları şunlardır:**

1. **ADL ve aşırı yüklenmiş operatörler:** ADL, aşırı yüklenmiş operatörlerin çözümlemesi için de kullanılır. Özellikle, sınıf türlerine özgü operatörler için, ADL kullanılarak doğru operatörün çağrılması sağlanır.

2. **ADL ve şablonlar:** ADL, şablonlu fonksiyonlar ve sınıflar için de çalışır. Şablonlu fonksiyonlar, şablon parametrelerinin türlerine bağlı olarak doğru ad alanlarında aranabilir ve çağrılabilir.

3. **ADL ve sınıf yöntemleri:** ADL, sınıf üyesi fonksiyonları için kullanılmaz, çünkü sınıf üyesi fonksiyonları doğrudan sınıf adı veya nesne adı üzerinden çağrılır. Bununla birlikte, sınıf üyesi olmayan fonksiyonlar için, ADL kullanılarak doğru fonksiyonun çağrılması sağlanır.

4. **ADL ve standart kütüphane:** C++ standart kütüphanesi, birçok ad alanında tanımlanan sınıflar ve fonksiyonlar içerir. ADL, standart kütüphane fonksiyonlarının çağrılmasında da rol oynar ve bu sayede uygun fonksiyonların doğru şekilde kullanılmasını sağlar.

5. **ADL ve isim çakışmalarını önleme:** ADL, isim çakışmalarını önlemeye yardımcı olan bir yöntemdir, ancak dikkatli kullanılmalıdır. Aynı adlı birden fazla fonksiyonun farklı ad alanlarında tanımlanması durumunda, ADL ile hangi fonksiyonun çağrılacağı belirsiz olabilir. Bu nedenle, uygun ad alanlarını ve sembolleri kullanarak isim çakışmalarını önlemek için kodun düzenli bir şekilde organize edilmesi önemlidir.

# Unnamed Namespace

- Unnamed namespaces, C++ dilinde kullanılan özel bir tür ad alanıdır (namespace) ve isimsiz olarak tanımlanır. Unnamed namespaces, içinde tanımlanan değişkenlerin ve fonksiyonların sadece tanımlandığı dosya (translation unit) içinde erişilebilir olmasını sağlar. Bu, bağlantı süresinde bağlantı hatalarını önlemeye ve kodun daha güvenli ve bakımı kolay hale getirilmesine yardımcı olur.

- Unnamed namespaces, namespace anahtar kelimesi kullanılarak ve ad belirtmeden oluşturulur:

```CPP
namespace {
    // İsimsiz ad alanında tanımlanan değişkenler ve fonksiyonlar
    int myVariable;
    void myFunction() {
        // ...
    }
}

```

- Unnamed namespaces'in kullanımı ve avantajları şunlardır:

1. **Dosya özelinde global değişkenler ve fonksiyonlar:** Unnamed namespaces, global değişkenlerin ve fonksiyonların dosya özelinde sınırlanmasına olanak tanır. Bu sayede, diğer dosyalardaki aynı isimli global değişkenler ve fonksiyonlarla isim çakışması riski ortadan kalkar.
2. **Bağlantı hatalarını önleme:** Unnamed namespaces, bağlantı sürecindeki hataları önlemeye yardımcı olur. Unnamed namespaces içinde tanımlanan değişkenler ve fonksiyonlar, bağlantı süresinde diğer dosyalardaki isimlerle çakışmayacağından, bağlantı hataları azalır.

3. **Kod güvenliği ve bakımı:** Unnamed namespaces, kod güvenliğini ve bakımını artırır. Dosya özelinde tanımlanan değişkenler ve fonksiyonlar, sadece ilgili dosyada kullanılabilir olduğundan, yanlışlıkla başka dosyalardaki kod parçalarını etkileme riski azalır.

4. **C dili için statik bağlantı özelliğinin yerini alır:** C++'ta unnamed namespaces, C dilinde kullanılan static anahtar kelimesinin işlevine benzer şekilde çalışır. C dilinde, static anahtar kelimesi ile tanımlanan global değişkenler ve fonksiyonlar, yalnızca tanımlandığı dosya içinde erişilebilir olur. Unnamed namespaces, C++'ta bu işlevselliği sağlar.
- Unnamed namespaces, C++ kodunun düzenli ve güvenli bir şekilde organize edilmesine yardımcı olan önemli bir özelliktir. Bu özellik sayesinde, global değişkenler ve fonksiyonlar daha iyi yönetilir ve potansiyel hataların önüne geçilir.

# Translation Unit

- Translation unit (TU), C++ derleyicisinin işlem yapacağı kod parçalarının en temel birimidir. Genel olarak, bir translation unit, bir kaynak dosyası (.cpp) ve bu dosyaya dahil edilen tüm başlık dosyaları (.h, .hpp) içerir. Derleyici, her translation unit'i bağımsız olarak derler ve sonrasında bağlayıcı (linker) bu bağımsız derlenen objeleri bir araya getirerek nihai çalıştırılabilir programı oluşturur.

- Translation unit işleyişi ve önemi ile ilgili temel noktalar şunlardır:

1. **Kaynak ve başlık dosyaları:** Bir translation unit, bir kaynak dosyası (.cpp) ve bu dosyaya dahil edilen tüm başlık dosyalarını içerir. Bu dosyalar, C++ derleyicisi tarafından işlenir ve derlenir.

2. **Bağımsız derleme:** Derleyici, her translation unit'i bağımsız olarak derler. Bu, derleme sürecinin paralel ve daha hızlı olmasını sağlar, ayrıca her bir translation unit'teki hataların, diğer translation unit'lere etki etmeyeceği anlamına gelir.

3. **Bağlayıcı (linker):** Derleme işlemi tamamlandıktan sonra, bağlayıcı devreye girer ve derlenen objeleri (translation unit'ler) bir araya getirerek nihai çalıştırılabilir programı oluşturur. Bu süreçte bağlayıcı, fonksiyon ve değişken tanımlarını çözerek birimler arasındaki bağlantıları sağlar.

4. **Tanımlama ve bildirim:** Translation unit'lerde, tanımlama ve bildirimlerin doğru kullanılması önemlidir. Özellikle, global değişkenler ve fonksiyonlar için tanımlamaların bir translation unit'te yapılması ve diğer translation unit'lere bildirimlerle aktarılması tercih edilir. Bu, bağlantı sürecinde hataları önlemeye yardımcı olur.

5. **Tekrarlayan başlık dosyalarını önleme:** Translation unit'lere dahil edilen başlık dosyalarında, aynı başlık dosyasının birden fazla kez dahil edilmesini önlemek için include guards veya #pragma once yönergeleri kullanılır. Bu, derleme sürecini hızlandırır ve derleyici hatalarını önlemeye yardımcı olur.

6. **Kod organizasyonu ve bakımı:** Translation unit kavramı, C++ kodunun düzenli ve modüler bir şekilde organize edilmesine yardımcı olur. Her translation unit, belirli bir işlevsellik veya modülle ilgili kodları içerebilir, bu da projenin genel bakımını ve yönetimini kolaylaştırır.

# Nested Namespace 

- C++'da, nested namespace (iç içe geçmiş ad alanları), bir ad alanı içinde başka bir ad alanı tanımlamak anlamına gelir. Bu yapı, kodun daha düzenli ve modüler hale getirilmesine yardımcı olarak, kod organizasyonu ve okunabilirliği açısından avantaj sağlar. C++17 ve sonrası sürümlerde, nested namespace'ler için daha kısa ve daha okunabilir bir sözdizimi kullanılabilir.

- Öncelikle, iç içe geçmiş ad alanlarının eski sözdizimine bakalım:

```CPP
namespace Outer {
  namespace Inner {
    void someFunction();
  }
}

```

- Yukarıdaki örnekte, Outer ad alanı içinde Inner ad alanı tanımlanmıştır ve bu iki ad alanı iç içe geçmiştir. someFunction() fonksiyonuna erişmek için şu şekilde kullanılabilir:

```CPP
Outer::Inner::someFunction();

```

- C++17 ile gelen yeni sözdizimi sayesinde, iç içe geçmiş ad alanlarını daha kısa ve daha okunabilir bir şekilde tanımlayabiliriz:

```CPP
namespace Outer::Inner {
  void someFunction();
}

```
- Bu yeni sözdizimi, aynı iç içe geçmiş ad alanları için daha az kod yazmanızı sağlar ve okunabilirliği artırır. Fonksiyon çağrısı için önceki örnekle aynı şekilde kullanılır:

```CPP
Outer::Inner::someFunction();

```
- Nested namespace'ler, daha büyük projelerde kod organizasyonunu iyileştirmeye ve modülerleştirmeye yardımcı olarak, kodun okunabilirliğini ve bakımını kolaylaştırır. Ayrıca, farklı ad alanlarındaki isim çakışmalarını önlemeye yardımcı olur.

# Inline Namespace

- C++11 standardı ile birlikte gelen "inline namespace" özelliği, namespace'leri iç içe kullanma ihtiyacını azaltmak için kullanılır. Bu özellik, kodun okunabilirliğini artırır ve derleyici optimizasyonlarındaki ve bağımlılıklardaki karmaşayı azaltır.

- Normalde, namespace'ler kullanılarak, bir kapsam (scope) içinde birden fazla alt kapsam (sub-scope) oluşturulabilir. Örneğin:

```CPP
namespace A {
    namespace B {
        int x;
    }
}

```

- Bu kodda "A" namespace'i, "B" namespace'i içinde yer alır ve "B" namespace'inde "x" adında bir değişken tanımlanır. "x" değişkenine erişmek için "A::B::x" şeklinde kullanılabilir.

- Inline namespace, bu sorunu çözmek için kullanılır. Bir namespace'in inline olarak tanımlanması, o namespace'in kendisiyle aynı isimde bir iç namespace oluşturduğunu ve bu iç namespace'in o namespace ile aynı kapsamda bulunduğunu ifade eder. Örneğin:

```CPP
namespace A {
    inline namespace B {
        int x;
    }
}

```
- Bu kodda, "A" namespace'i, "B" namespace'i içinde yer alır ve "x" adında bir değişken tanımlanır. Ancak, "B" namespace'i inline olarak tanımlandığından, "x" değişkenine erişmek için "A::x" şeklinde kullanılabilir.

- Bir inline namespace, diğer namespace'ler gibi kullanılır. Örneğin, bir fonksiyonun inline bir namespace içinde tanımlanması, diğer namespace'lerde tanımlanmış olan fonksiyonların yerini alabilir. Böylece, kodun okunabilirliği artırılır ve alt kapsamların kullanımından kaynaklanan sorunlar azaltılır.

- Özetle, inline namespace, namespace'leri iç içe kullanma ihtiyacını azaltmak için kullanılır. Bu özellik, kodun okunabilirliğini artırır ve derleyici optimizasyonlarındaki ve bağımlılıklardaki karmaşayı azaltır. Bir inline namespace, diğer namespace'ler gibi kullanılır ve içindeki unsurlar, dış namespace ile birleştirilerek kullanılır.

# Nested Class 
- C++ programlama dilinde "nested class" (iç içe sınıf) olarak da bilinen "inner class" (iç sınıf) olarak adlandırılan yapı, bir sınıfın başka bir sınıfın üyesi olarak tanımlanmasına izin verir.

- Bir iç sınıf, diğer sınıflar gibi tüm C++ veri türü kurallarına sahiptir. İç sınıflar, dış sınıfın private, protected veya public üyelerine erişebilirler ve aynı zamanda kendi üyelerine de sahip olabilirler. İç sınıflar, ayrı bir bağımsız sınıf olarak tanımlanabilecekleri gibi, dış sınıfın üyesi olarak tanımlanabilirler.

**Örneğin:**

```CPP
class OuterClass {
public:
    class InnerClass {
    public:
        void doSomething();
    };
private:
    int x;
};

void OuterClass::InnerClass::doSomething() {
    // ...
}

```

> Bu kodda "InnerClass", "OuterClass" sınıfının bir üyesi olarak tanımlanmıştır. "InnerClass", "doSomething" adında bir fonksiyona sahip olan ayrı bir sınıf olarak tanımlanabilir. Bu durumda, "doSomething" fonksiyonunun tanımı, sınıfın dışındaki bir yerde tanımlanmalıdır.

- Inner class, dış sınıfın private veya protected üyelerine erişebilir ve ayrıca kendi üyelerine de sahip olabilir. Örneğin, "InnerClass" aşağıdaki gibi tanımlanabilir:

```CPP
class OuterClass {
public:
    class InnerClass {
    public:
        void doSomething() {
            x = 5; // OuterClass'ın private üyesine erişim
        }
    private:
        int y;
    };
private:
    int x;
};

```
> Bu kodda, "InnerClass" sınıfı, "OuterClass" sınıfının private üyesine ("x") erişebilir ve kendi private üyesine ("y") sahiptir.

- Inner class, dış sınıfın bir parçası olduğu için, dış sınıfın private veya protected üyelerine erişebilir. Ancak, Inner class'ın private üyelerine erişim yalnızca dış sınıfın üyeleri tarafından gerçekleştirilebilir.

- Inner class, sınıf hiyerarşisindeki bazı problemleri çözmek için kullanılabilir. Örneğin, bir sınıfın bir örneği oluşturulduğunda, iç sınıfın da otomatik olarak oluşturulması mümkündür. İç sınıflar ayrıca, dış sınıfın üyelerine erişimi sınırlamak ve kapsüllemeyi artırmak için de kullanılabilir.

- Özetle, inner class, bir sınıfın üyesi olarak tanımlanan ve ayrı bir bağımsız sınıf olarak tanımlanabilen bir yapıdır. Inner class, dış sınıfın private veya protected üyelerine erişebilir ve ayrıca kendi private, protected veya public üyelerine de sahip olabilir. Inner class, sınıf hiyerarşisindeki bazı problemleri çözmek için kullanılabilir ve dış sınıfın üyelerine erişimi sınırlamak ve kapsüllemeyi artırmak için de kullanılabilir.

- Inner class'ın bir diğer avantajı, kodun okunabilirliğini artırmasıdır. Inner class'lar, bir sınıfın kullanılmasının anlamlı olmadığı durumlarda kullanılabilir ve ayrıca bir sınıfın birden fazla parçasını bir arada gruplandırmak için de kullanılabilir.

- Inner class'lar, STL kütüphanesinde sıkça kullanılır. Örneğin, std::list sınıfı, std::list::iterator adında bir iç sınıf kullanır. Bu iç sınıf, std::list sınıfının öğelerine erişmek ve onları dolaşmak için kullanılır.

- Inner class'lar, C++ dilindeki diğer özelliklerle birlikte kullanılabildiği gibi, template'ler, inheritance (miras) ve generic programming (genel programlama) gibi diğer programlama teknikleriyle de birlikte kullanılabilir.

- Özetle, inner class, bir sınıfın üyesi olarak tanımlanan ve ayrı bir bağımsız sınıf olarak tanımlanabilen bir yapıdır. Inner class, dış sınıfın private veya protected üyelerine erişebilir ve ayrıca kendi private, protected veya public üyelerine de sahip olabilir. Inner class, sınıf hiyerarşisindeki problemleri çözmek için kullanılabilir ve kodun okunabilirliğini artırır.


















