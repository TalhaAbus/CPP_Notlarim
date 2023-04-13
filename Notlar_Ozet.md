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













