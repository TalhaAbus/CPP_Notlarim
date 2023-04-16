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

# Pimple Idiom

- Pimple idiom, C++ dilinde kullanılan ve "pointer to implementation" (uçtan uca uygulama) olarak da bilinen bir teknik olup, sınıf uygulamasını saklamak için kullanılır. Bu teknik, sınıfın dışa dönük API'sini ve iç uygulamasını ayırmaya yardımcı olur. Bu sayede, kullanıcılar sınıfın kullanımına odaklanabilir ve iç uygulama detaylarından kaçınabilirler. Pimple idiom, aşağıdaki avantajlara sahiptir:


1. **Gizlilik:** Pimple idiom, sınıfın iç yapısını ve uygulamasını gizleyerek kullanıcının sınıfın dışa dönük API'sine odaklanmasını sağlar. Bu, daha temiz ve anlaşılabilir bir kullanıcı deneyimi sunar.
2. **Kütüphane Bağımsızlığı:** Sınıfın iç uygulamasının gizlenmesi, kütüphane bağımlılıklarını sınırlar ve kodu daha taşınabilir hale getirir.
3. **Derleme Sürelerini Azaltma:** İç uygulama detaylarını gizlemek, derleme sürelerini azaltarak daha hızlı geliştirme süreçleri sağlar.
4. **Sürdürülebilirlik:** Sınıfın iç yapısını ve uygulamasını gizleyerek, geliştiriciler sınıfın iç yapısını değiştirebilir ve dışa dönük API'sini etkilemeden iyileştirmeler yapabilirler.

- Pimple idiom'un uygulanması, genellikle iki sınıf kullanarak gerçekleştirilir: dış sınıf (sınıfın dışa dönük API'sini sağlayan) ve iç sınıf (sınıfın gerçek uygulamasını içeren). İç sınıf, dış sınıfta bir özel alan (unique_ptr gibi) ile saklanır. İşte bir örnek:

```CPP
// Örnek sınıfın ön tanımı
class OrnekSinif {
public:
    OrnekSinif(); // Kurucu
    ~OrnekSinif(); // Yıkıcı

    void islemYap(); // Sınıfın dışa dönük API'sini temsil eden bir işlev

private:
    class OrnekSinifImpl; // İç sınıfın ön tanımı
    std::unique_ptr<OrnekSinifImpl> pimpl; // İç sınıfın örneklemesi
};

// OrnekSinifImpl sınıfının uygulanması
class OrnekSinif::OrnekSinifImpl {
public:
    void islemYap() {
        // Gerçek işlem kodu burada olacak
    }
};

// OrnekSinif sınıfının uygulanması
OrnekSinif::OrnekSinif() : pimpl(std::make_unique<OrnekSinifImpl>()) {}

OrnekSinif::~OrnekSinif() = default;

void OrnekSinif::islemY

```

# Association - Aggregation - Composition
- Association, Aggregation ve Composition, nesne yönelimli programlamada kullanılan üç temel ilişki türüdür. Bu ilişkiler, sınıflar arasındaki bağlantıları ve etkileşimleri temsil eder. İşte her biri hakkında detaylı bilgi:

1. **Association (İlişkilendirme):**
Association, iki sınıf arasındaki genel bir bağlantıyı temsil eder. İki sınıfın birbirine bağlı olduğunu, ancak bir sınıfın diğerinin yaşam döngüsünden bağımsız olduğunu belirtir. Bu tür bir ilişki, genellikle iki sınıfın birbiriyle etkileşime girdiği, ancak birbirlerinin varlığından tamamen bağımsız olduğu durumlar için kullanılır.

> Örnek olarak, bir "Öğrenci" sınıfı ve bir "Ders" sınıfı düşünelim. Bir öğrenci, bir veya birden fazla derse kaydolabilir ve bir dersin de birden fazla öğrencisi olabilir. Bu durumda, Öğrenci ve Ders arasında bir association ilişkisi vardır.

2. **Aggregation (Toplulaştırma):**
Aggregation, "whole/part" (bütün/parça) ilişkisini temsil eden özel bir association türüdür. Aggregation, bir sınıfın diğer sınıfların örneklerini içerdiğini, ancak bu örneklerin yaşam döngülerinin bağımsız olduğunu belirtir. Başka bir deyişle, ana nesnenin yok olması, içerdiği nesnelerin yok olmasına neden olmaz.

> Örnek olarak, "Üniversite" ve "Öğrenci" sınıflarını düşünelim. Üniversite, Öğrenci nesnelerinden oluşan bir koleksiyona sahip olabilir, ancak Üniversite nesnesi ortadan kalktığında Öğrenci nesneleri hala var olabilir. Bu durumda, Üniversite ve Öğrenci arasında bir aggregation ilişkisi vardır.

3. **Composition (Bileşim):**
Composition, aggregation'dan daha güçlü bir "whole/part" ilişkisini temsil eder. Composition, bir sınıfın diğer sınıfların örneklerini içerdiğini ve bu örneklerin yaşam döngülerinin ana nesneye bağlı olduğunu belirtir. Başka bir deyişle, ana nesnenin yok olması, içerdiği nesnelerin de yok olmasına neden olur.

> Örnek olarak, "Araba" ve "Motor" sınıflarını düşünelim. Bir arabanın bir motoru vardır ve motorun yaşam döngüsü arabanın yaşam döngüsüne bağlıdır.

# Copy on Write

- Copy-on-Write (CoW) tekniği, nesne yönelimli programlama, veri yapıları ve bellek yönetimi gibi bilgisayar bilimlerinin çeşitli alanlarında kullanılan bir optimizasyon stratejisidir. CoW, bir veri öğesinin birden fazla kullanıcı tarafından paylaşılmasına izin verir ve bu öğeye yazma işlemi yapılmadan önce, verinin bir kopyasını oluşturarak güvenli bir şekilde yazılmasını sağlar. Bu teknik, bellek kullanımını ve gereksiz veri kopyalama işlemlerini azaltmaya yardımcı olur.

- **Copy-on-Write, aşağıdaki avantajlara sahiptir:**

1. Bellek Kullanımını Optimize Etme: CoW, verinin sadece yazma işlemi yapılırken kopyalandığı için bellek kullanımını önemli ölçüde azaltır. Bu sayede, daha fazla bellek, diğer işlemler ve veri yapıları için kullanılabilir.
2. Performans Artışı: CoW, yazma işlemlerini sadece gerçekten gerekli olduğunda gerçekleştirerek gereksiz veri kopyalama işlemlerini önler. Bu, performansı artırır ve daha hızlı işlem süreleri sağlar.
3. Güvenli Paylaşılan Veri: CoW, birden fazla kullanıcının veriyi güvenli bir şekilde paylaşmasına olanak tanır. Bir kullanıcı veriyi değiştirmeye çalıştığında, verinin bir kopyası oluşturulur ve değişiklikler bu kopyada yapılır. Bu, diğer kullanıcıların etkilenmemesini sağlar ve veri bütünlüğünü korur.

- İşte Copy-on-Write tekniğinin uygulandığı basit bir örnek:
```CPP
class CowString {
public:
    CowString(const std::string& str) : data_(std::make_shared<std::string>(str)) {}

    // Yazma işlemi gerçekleştirilmeden önce verinin kopyasını oluşturan fonksiyon
    void Write(size_t pos, char c) {
        if (!data_.unique()) {
            data_ = std::make_shared<std::string>(*data_);
        }
        (*data_)[pos] = c;
    }

    const std::string& Read() const {
        return *data_;
    }

private:
    std::shared_ptr<std::string> data_;
};

```
> Bu örnekte, CowString sınıfı, std::string verisini std::shared_ptr kullanarak paylaşır. Write fonksiyonu, veriye yazma işlemi yapılırken verinin kopyasını oluşturarak, diğer kullanıcıların etkilenmemesini sağlar. Bu şekilde, veri yazma işlemlerinde güvenli bir şekilde paylaşılır ve bellek kullanımı optimize edilir.

# Data Constructor

- Data constructor terimi, genellikle bir veri yapısının veya sınıfın, belirli bir veri ile başlatılması için kullanılan yapılandırıcıları ifade eder. Bu tür yapılandırıcılar, veri yapısını veya sınıfı oluştururken veri alır ve bu veriyi nesnenin başlangıç durumu olarak kullanır. Örneğin, std::string için data constructor:

```CPP
std::string s1("data");

```
# Range Constructor
- Range constructor, bir aralık (başlangıç ve bitiş değerleri) kullanarak veri yapısı veya sınıfı başlatan yapılandırıcıları ifade eder. Bu tür yapılandırıcılar, genellikle başlangıç ve bitiş yineleyicileri (iterators) arasındaki değerlerle veri yapısını doldurur. Örneğin, std::vector için range constructor:
```CPP
std::vector<int> vec1 = {1, 2, 3, 4};
std::vector<int> vec2(vec1.begin(), vec1.end());

```
# Initializer List Constructor
- Initializer list constructor, C++11'de tanıtılan bir özellik olan initializer list (başlatıcı liste) kullanarak veri yapısı veya sınıfı başlatan yapılandırıcıları ifade eder. Bu tür yapılandırıcılar, C++'daki liste başlatma sözdizimi ile uyumlu olup, nesnenin başlangıç durumunu belirlemek için bir liste kullanır. Örneğin, std::vector için initializer list constructor:
```CPP
std::vector<int> vec3 = {1, 2, 3, 4, 5};

```

# Few Constructor
- Bu terim, genellikle belirli bir sayıda parametre alan yapılandırıcıları ifade eder. "Few" kelimesi, parametre sayısının az veya sınırlı olduğunu vurgular. Ancak, bu terim yaygın bir C++ terimi değildir ve burada verilen tanım, genel anlamda verilmiştir.
# Substring Constructor
- Substring constructor, bir dizenin (string) bir alt dizgesini (substring) kullanarak başka bir dizeyi oluşturan yapılandırıcıları ifade eder. Bu tür yapılandırıcılar, bir dizenin belirli bir bölümünü başka bir dizeye kopyalamak için kullanılır. Örneğin, std::string için substring constructor:
```CPP
std::string s2("hello, world!");
std::string s3(s2, 0, 5); // "hello" ile başlatır
```
# If with Initializer

- "If with initializer" (başlatıcı ile if) C++11 standardıyla birlikte eklenen bir özelliktir. Bu özellik, if bloğuna bir başlatıcı eklemeyi mümkün kılar. Bu şekilde, if bloğuna başlamadan önce bir değişken tanımlayabilir ve bu değişkeni if bloğu içinde kullanabilirsiniz.
**Örneğin:**

```CPP
if (int x = foo(); x > 0) {
    // x, foo() fonksiyonunun değerini tutar
    // x, sadece bu if bloğu içinde görülebilir
    // ...
}

```
> Bu kodda, "x" adında bir değişken tanımlanır ve "foo()" fonksiyonunun değeri, "x" değişkenine atanır. Daha sonra, if bloğu içinde "x" değişkeni kullanılabilir. Bu yapı, kodun okunabilirliğini artırır ve kodun daha kısa ve anlaşılır olmasını sağlar.

- "If with initializer", özellikle küçük bloklarda kullanışlıdır. Ayrıca, bazı durumlarda, kodun performansını da artırabilir. Örneğin, bir dizi üzerinde işlem yaparken, her seferinde bir dizi elemanını kontrol etmek yerine, bir değişkende dizinin uzunluğunu saklayabilir ve bu değişkeni if bloğunda kullanabilirsiniz.

- Özetle, "if with initializer", C++11 standardıyla birlikte gelen bir özelliktir ve if bloğuna başlatıcı eklemeyi mümkün kılar. Bu yapı, kodun okunabilirliğini artırır ve kodun daha kısa ve anlaşılır olmasını sağlar.

# Inheritance 
- Inheritance (kalıtım), nesne yönelimli programlama (OOP) konseptlerinden biridir ve bir sınıfın başka bir sınıftan özellikler (değişkenler ve metotlar) ve davranışlar devralmasına olanak tanır. Kalıtım, kodun yeniden kullanılabilirliğini artırır ve sınıflar arasındaki ilişkileri düzenler. Ayrıca, hiyerarşik yapılar oluşturarak, genel ve özelleştirilmiş sınıflar arasındaki soyutlamayı geliştirir.
- Inheritance, ana sınıflardan (üst sınıflar veya temel sınıflar olarak da adlandırılır) türetilen sınıflara (alt sınıflar veya türetilmiş sınıflar olarak da adlandırılır) özelliklerin aktarılmasıyla gerçekleşir. Türetilen sınıflar, temel sınıfın özelliklerini ve davranışlarını devralır ve bunlara ek özellikler veya davranışlar ekleyerek özelleştirilebilir.
- C++ dilinde, kalıtım şu şekilde gerçekleştirilir:

```CPP
class TemelSinif {
public:
    void genelFonksiyon() {
        // Temel sınıfta tanımlanan genel bir fonksiyon
    }
};

class TuretilmisSinif : public TemelSinif {
public:
    void ozelFonksiyon() {
        // Türetilmiş sınıfta tanımlanan özel bir fonksiyon
    }
};

```

> Bu örnekte, TuretilmisSinif, TemelSinif sınıfından türetilmiştir ve public erişim belirleyicisi ile kalıtım gerçekleştirilmiştir. Bu durumda, TuretilmisSinif hem genelFonksiyon() hem de ozelFonksiyon() fonksiyonlarına sahip olacaktır.
- **Inheritance türleri:**

1. Tek (Single) Inheritance: Bir alt sınıfın yalnızca bir temel sınıftan özellikler devraldığı durumdur. Bu, C++'da en yaygın kullanılan kalıtım türüdür.
2. Çoklu (Multiple) Inheritance: Bir alt sınıfın birden fazla temel sınıftan özellikler devraldığı durumdur. C++ bu tür kalıtımı destekler, ancak dikkatli kullanılması gerekir çünkü bazı karmaşıklıklar ve elmas problemi gibi sorunlar ortaya çıkabilir.

- Inheritance, nesne yönelimli programlamadaki diğer önemli kavramlarla (ör. soyutlama, enkapsülasyon ve polimorfizm) birlikte çalışarak, kodun daha modüler, düzenli ve yeniden kullanılabilir olmasını sağlar.

# Upcasting - Downcasting
- Upcasting ve downcasting, nesne yönelimli programlama (OOP) dillerinde, özellikle kalıtım ve polimorfizm kullanıldığında sıklıkla karşılaşılan iki işlemdir. Bu işlemler, temel ve türetilmiş sınıflar arasındaki nesnelerin tür dönüşümlerini ifade eder.

1. **Upcasting:**
- Upcasting, bir alt sınıf nesnesinin temel sınıf türüne dönüştürülmesi işlemidir. Bu işlem, genellikle hiyerarşik yapılar arasındaki nesnelerin türlerini değiştirmek için kullanılır. Upcasting, C++ ve diğer nesne yönelimli dillerde güvenli ve otomatik olarak gerçekleştirilir.

**Upcasting örneği:**

```CPP
class TemelSinif { /* ... */ };

class TuretilmisSinif : public TemelSinif { /* ... */ };

int main() {
    TuretilmisSinif* turetilmisPtr = new TuretilmisSinif();

    // Upcasting: Türetilmiş sınıfın işaretçisi temel sınıfın işaretçisine atanır
    TemelSinif* temelPtr = turetilmisPtr;
}

```

2. **Downcasting:**
- Downcasting, bir temel sınıf nesnesinin türetilmiş sınıf türüne dönüştürülmesi işlemidir. Downcasting işlemi, upcasting işlemine kıyasla daha risklidir ve dikkatli kullanılmalıdır. C++'da, downcasting işlemi, dynamic_cast veya static_cast gibi döküm (casting) operatörleri kullanılarak gerçekleştirilir.

**Downcasting örneği:**

```CPP
class TemelSinif { /* ... */ };

class TuretilmisSinif : public TemelSinif { /* ... */ };

int main() {
    TemelSinif* temelPtr = new TuretilmisSinif();

    // Downcasting: Temel sınıfın işaretçisi türetilmiş sınıfın işaretçisine atanır (dynamic_cast kullanarak)
    TuretilmisSinif* turetilmisPtr = dynamic_cast<TuretilmisSinif*>(temelPtr);

    // Eğer dönüşüm başarılı olmazsa, turetilmisPtr NULL olacaktır
    if (turetilmisPtr) {
        // Downcasting başarılı, turetilmisPtr kullanılabilir
    } else {
        // Downcasting başarısız
    }
}

```
- Downcasting işlemi, tür dönüşümünün geçerli olup olmadığını kontrol etmek için dynamic_cast kullanılması önerilir. Eğer dönüşüm geçerli değilse, dynamic_cast başarısız olur ve NULL işaretçisi döndürür.

# Access Control
- C++ dilinde "access control" (erişim kontrolü), sınıfların ve yapıların içindeki öğelerin (değişkenler, fonksiyonlar ve iç sınıflar) erişilebilirliğini düzenleyen bir mekanizmadır. Erişim kontrolü, nesne yönelimli programlamada enkapsülasyon ilkesinin bir parçasıdır ve programın farklı bölümlerinde kullanılacak üye öğelerin görünürlüğünü sınırlandırmaya yardımcı olur.
- C++ dilinde erişim kontrolü, üç ana erişim belirleyici (access specifier) ile gerçekleştirilir:

1. **public:** Public erişim belirleyici, üye öğelerin sınıfın dışından erişilebilir olduğunu belirtir. Bu, herhangi bir nesne veya fonksiyon tarafından bu üye öğelere erişilebileceği anlamına gelir. Genellikle, sınıfın dış dünya ile etkileşimde bulunması gereken üye fonksiyonlar public olarak tanımlanır.

2. **private:** Private erişim belirleyici, üye öğelerin yalnızca sınıfın içinden erişilebilir olduğunu belirtir. Bu, sınıfın dışından bu öğelere doğrudan erişilemeyeceği anlamına gelir. Private üye öğeler, sınıfın iç işleyişinde kullanılır ve dış dünya ile etkileşime girmeden sınıfın iç durumunu yönetir.

3. **protected:** Protected erişim belirleyici, üye öğelerin sınıfın içinden ve türetilmiş sınıflardan erişilebilir olduğunu belirtir. Bu, temel sınıftan türetilen sınıfların, temel sınıfın protected üye öğelerine erişebileceği anlamına gelir. Protected üye öğeler, genellikle alt sınıflar tarafından kullanılması amaçlanan özellikler ve işlemler için kullanılır.

- Erişim belirleyicileri kullanma örneği:

```CPP
class OrnekSinif {
public:
    // Public üye fonksiyon
    void publicFonksiyon() {
        // ...
    }

private:
    // Private üye değişken
    int privateDegisken;

    // Private üye fonksiyon
    void privateFonksiyon() {
        // ...
    }

protected:
    // Protected üye değişken
    int protectedDegisken;

    // Protected üye fonksiyon
    void protectedFonksiyon() {
        // ...
    }
};

```
- Erişim kontrolü, C++ programlarının modülerliğini ve güvenliğini artırarak, sınıf üyelerinin uygun şekilde kullanılmasını sağlar. Bu sayede, kodun daha düzenli ve anlaşılır olması sağlanır ve hataların önlenmesine yardımcı olur.

# Runtime Polimorphism

- Çalışma zamanı polimorfizmi (runtime polymorphism), nesne yönelimli programlama (OOP) dillerinde, farklı sınıf nesnelerinin aynı arayüz veya temel sınıf işaretçisi aracılığıyla çalışma zamanında çağrılabilen farklı uygulamalarını ifade eder. Runtime polimorfizmi, genellikle soyut sınıflar ve sanal fonksiyonlar kullanılarak gerçekleştirilir.

- Çalışma zamanı polimorfizmi, kodun daha genişletilebilir ve esnek olmasına yardımcı olur. Ayrıca, kodu daha modüler ve düzenli hale getirir, çünkü çalışma zamanında nesnelerin gerçek türlerine göre doğru fonksiyonun çağrılmasını sağlar.

- C++ dilinde, çalışma zamanı polimorfizmini kullanmak için genellikle şu adımlar izlenir:

1. Temel sınıfta, sanal fonksiyonlar tanımlayarak ortak bir arayüz oluşturun.
2. Türetilmiş sınıflarda, temel sınıftaki sanal fonksiyonları uygulayarak ve gerektiğinde özelleştirin.
3. Temel sınıf işaretçileri veya referansları kullanarak, çalışma zamanında gerçek nesne türlerine göre doğru fonksiyonları çağırın.

- Aşağıda, çalışma zamanı polimorfizminin bir örneği verilmiştir:

```CPP
#include <iostream>

// Temel sınıf
class Hayvan {
public:
    virtual void sesCikar() const {
        std::cout << "Bir hayvan sesi çıkarıyor." << std::endl;
    }
};

// Türetilmiş sınıf 1
class Kopek : public Hayvan {
public:
    void sesCikar() const override {
        std::cout << "Hav! Hav!" << std::endl;
    }
};

// Türetilmiş sınıf 2
class Kedi : public Hayvan {
public:
    void sesCikar() const override {
        std::cout << "Miyav! Miyav!" << std::endl;
    }
};

// Hayvanların ses çıkarma fonksiyonunu çağıran işlev
void hayvanSesCikar(const Hayvan& hayvan) {
    hayvan.sesCikar();
}

int main() {
    Kopek kopek;
    Kedi kedi;

    // Hayvan türüne göre doğru ses çıkarma fonksiyonunu çağırır
    hayvanSesCikar(kopek); // Çıktı: "Hav! Hav!"
    hayvanSesCikar(kedi);  // Çıktı: "Miyav! Miyav!"
}

```

- Bu örnekte, Hayvan temel sınıfında sesCikar adlı sanal bir fonksiyon tanımlanmıştır. Kopek ve Kedi türetilmiş sınıfları, bu fonksiyonu kendi özel uygulamalarıyla geçersiz kılar (override). Bu durum, farklı Hayvan türlerinin kendi seslerini çıkarmasına izin verir.
- hayvanSesCikar işlevi, Hayvan temel sınıfının bir referansını alır ve bu referans üzerinden sesCikar fonksiyonunu çağırır. Bu işlevi kullanarak, çalışma zamanında geçirilen gerçek nesne türüne göre doğru sesCikar fonksiyonunun çağrılması sağlanır. Bu, çalışma zamanı polimorfizminin temelidir.

- Yukarıdaki örnekte, main fonksiyonunda Kopek ve Kedi nesneleri oluşturulur ve hayvanSesCikar işlevine gönderilir. İşlev, çalışma zamanında geçirilen nesnenin gerçek türünü belirleyerek doğru sesCikar fonksiyonunu çağırır.

- Çalışma zamanı polimorfizmi, OOP dillerindeki temel bir kavramdır ve kodun daha düzenli, anlaşılır ve esnek olmasına yardımcı olur. Bu sayede, farklı nesne türlerinin aynı arayüz üzerinden çalışma zamanında dinamik olarak kullanılabilmesi sağlanır.

# Abstract Class
- Abstract class (soyut sınıf), nesne yönelimli programlama dillerinde, doğrudan örneklenemeyen ve türetilmiş sınıflar için temel olarak kullanılan bir sınıf türüdür. Soyut sınıflar, genellikle ortak işlevselliği ve yapıyı paylaşan türetilmiş sınıflar arasında bir şablon sağlar.

- Soyut sınıfların temel amacı, ortak arayüzler ve işlevselliği tanımlamak ve paylaşmaktır. Soyut sınıflar, bir veya birden fazla soyut metod (sanal fonksiyon) içerebilir ve bu metodlar, türetilmiş sınıflarda uygulanmalıdır. Soyut sınıflar aynı zamanda uygulanmış (non-abstract) metodlar da içerebilir, bu sayede türetilmiş sınıfların bu metodları doğrudan kullanmalarına veya geçersiz kılmalarına (override) olanak sağlar.

- C++ dilinde soyut sınıf tanımlamak için, en az bir sanal fonksiyonun "= 0" ile işaretlenmesi gerekir. Bu, fonksiyonun soyut olduğunu ve türetilmiş sınıflarda uygulanması gerektiğini belirtir. İşte bir soyut sınıf örneği:

```CPP
class Sekil {
public:
    virtual double alan() const = 0; // Soyut metod
    virtual double cevre() const = 0; // Soyut metod

    void sekilBilgisi() const { // Uygulanmış metod
        std::cout << "Alan: " << alan() << ", Cevre: " << cevre() << std::endl;
    }
};

```
- Yukarıdaki örnekte, Sekil adlı soyut bir sınıf tanımlanmıştır. Bu sınıf, alan ve cevre adlı iki soyut metod içerir. Türetilmiş sınıfların bu metodları uygulaması beklenir. Ayrıca, sekilBilgisi adlı uygulanmış bir metod da içerir ve bu metod türetilmiş sınıflar tarafından doğrudan kullanılabilir.

- Soyut sınıflar, nesne yönelimli programlamada temel bir kavramdır ve kodun daha düzenli, anlaşılır ve esnek olmasına yardımcı olur. Soyut sınıflar sayesinde, ortak işlevsellik ve yapıyı paylaşan sınıflar arasında modülerlik ve yeniden kullanılabilirlik sağlanır.

# Virtual Dispatch
- Virtual dispatch (sanal gönderim), çalışma zamanında nesnelerin türlerine göre doğru fonksiyonun çağrılmasını sağlayan bir mekanizmadır. Bu mekanizma, nesne yönelimli programlama dillerinde, özellikle de C++ dilinde, polimorfizmi gerçekleştirmek için kullanılır.

- Sanal fonksiyonlar (virtual functions) ve virtual dispatch arasında doğrudan bir ilişki vardır. Sanal fonksiyonlar, temel sınıf ve türetilmiş sınıflar arasında aynı imzaya sahip, ancak farklı uygulamaları olan fonksiyonlardır. Virtual dispatch, çalışma zamanında gerçek nesne türlerine göre doğru sanal fonksiyonların çağrılmasını sağlar.
- C++ dilinde, sanal fonksiyonlar virtual anahtar kelimesi ile tanımlanır ve türetilmiş sınıflarda bu fonksiyonlar geçersiz kılınabilir (override). Virtual dispatch, çalışma zamanında türetilmiş sınıflardan doğru sanal fonksiyonu çağırmak için işaretçi veya referanslar kullanarak gerçekleştirilir.

- İşte virtual dispatch kullanarak polimorfizmi gösteren bir örnek:

```CPP
#include <iostream>

class Hayvan {
public:
    virtual void sesCikar() const {
        std::cout << "Bir hayvan sesi çıkarıyor." << std::endl;
    }
};

class Kopek : public Hayvan {
public:
    void sesCikar() const override {
        std::cout << "Hav! Hav!" << std::endl;
    }
};

class Kedi : public Hayvan {
public:
    void sesCikar() const override {
        std::cout << "Miyav! Miyav!" << std::endl;
    }
};

void hayvanSesCikar(const Hayvan& hayvan) {
    hayvan.sesCikar(); // Virtual dispatch kullanılıyor
}

int main() {
    Kopek kopek;
    Kedi kedi;

    hayvanSesCikar(kopek); // Çıktı: "Hav! Hav!"
    hayvanSesCikar(kedi);  // Çıktı: "Miyav! Miyav!"
}

```
> Bu örnekte, Hayvan temel sınıfında sesCikar adlı bir sanal fonksiyon tanımlanmıştır. Kopek ve Kedi türetilmiş sınıfları, bu fonksiyonu geçersiz kılarak kendi uygulamalarını sağlar. hayvanSesCikar işlevi, Hayvan temel sınıfının referansını alarak çalışma zamanında geçirilen nesnenin türüne göre doğru sesCikar fonksiyonunu çağırır. Bu işlem, virtual dispatch ile gerçekleştirilir.

- Virtual dispatch, nesne yönelimli programlamada önemli bir kavramdır ve çalışma zamanı polimorfizminin temelidir. Bu sayede, farklı nesne türlerinin aynı arayüz üzerinden çalışma zamanında dinamik olarak kullanılabilmesi sağlanır. Virtual dispatch, kodun daha düzenli, anlaşılır ve esnek olmasına yardımcı olur.
- Virtual dispatch, C++'ta sanal fonksiyon tablosu (vtable) aracılığıyla gerçekleştirilir. Vtable, her sınıf için derleyici tarafından oluşturulan bir tablodur ve sınıftaki sanal fonksiyonların adreslerini içerir. Bir nesnenin işaretçisi veya referansı üzerinden sanal bir fonksiyon çağrıldığında, vtable'daki ilgili fonksiyon adresine gidilir ve çalışma zamanında doğru fonksiyon çağrılır.
- Virtual dispatch, biraz performans maliyetine sahiptir, çünkü işlem sırasında ekstra işaretçi dereferanslamaları gerçekleştirilir ve bu durum fonksiyon çağrılarını doğrudan çağırmaktan daha yavaş hale getirir. Ancak bu maliyet, genellikle kodun modülerlik, esneklik ve anlaşılabilirlik avantajlarıyla dengelenir.

- Sonuç olarak, virtual dispatch ve sanal fonksiyonlar, çalışma zamanı polimorfizmini sağlayarak nesne yönelimli programlama dillerinde, özellikle C++ dilinde, kodun daha düzenli, esnek ve anlaşılır olmasına yardımcı olur. Bu mekanizma, ortak arayüzler ve işlevselliği paylaşan sınıflar arasında modülerlik ve yeniden kullanılabilirlik sağlar.

# Override
- Override (geçersiz kılma), nesne yönelimli programlama dillerinde kullanılan bir terimdir. Temel sınıfta tanımlanan bir fonksiyonun, türetilmiş sınıflarda yeniden tanımlanarak değiştirilmesi işlemine denir. Bu sayede, türetilmiş sınıflar temel sınıfın fonksiyonlarını kendi ihtiyaçlarına göre özelleştirebilir ve genişletebilir.

- Override işlemi, genellikle sanal fonksiyonlar ile birlikte kullanılır. Sanal fonksiyonlar, temel sınıfta virtual anahtar kelimesi ile tanımlanır ve türetilmiş sınıflar bu fonksiyonları geçersiz kılabilir. C++ dilinde, override anahtar kelimesi kullanarak türetilmiş sınıflarda bir fonksiyonun temel sınıftaki sanal fonksiyonu geçersiz kıldığını belirtebiliriz. Bu, hem kodun okunabilirliğini artırır, hem de derleyici tarafından doğru şekilde geçersiz kılma işleminin kontrol edilmesini sağlar.

- İşte bir örnek:
```CPP
#include <iostream>

class Hayvan {
public:
    virtual void sesCikar() const {
        std::cout << "Bir hayvan sesi çıkarıyor." << std::endl;
    }
};

class Kopek : public Hayvan {
public:
    void sesCikar() const override { // temel sınıftaki 'sesCikar' fonksiyonunu geçersiz kılma
        std::cout << "Hav! Hav!" << std::endl;
    }
};

class Kedi : public Hayvan {
public:
    void sesCikar() const override { // temel sınıftaki 'sesCikar' fonksiyonunu geçersiz kılma
        std::cout << "Miyav! Miyav!" << std::endl;
    }
};

```
> Yukarıdaki örnekte, Hayvan adlı temel sınıfta sesCikar adlı bir sanal fonksiyon tanımlanmıştır. Kopek ve Kedi adlı türetilmiş sınıflar, bu fonksiyonu override anahtar kelimesi ile geçersiz kılarak kendi uygulamalarını sağlar. Bu şekilde, her türetilmiş sınıf kendi özelleştirilmiş sesCikar fonksiyonunu kullanabilir.

- Override, nesne yönelimli programlamada temel bir kavramdır ve çalışma zamanı polimorfizminin gerçekleştirilmesine yardımcı olur. Bu sayede, farklı nesne türlerinin aynı arayüz üzerinden çalışma zamanında dinamik olarak kullanılabilmesi sağlanır.

# V-Table

- v-table (sanal fonksiyon tablosu), C++ dilinde çalışma zamanında polimorfizm sağlamak için kullanılan bir mekanizmadır. v-table, sanal fonksiyonlar (virtual functions) için kullanılan bir araçtır ve her sınıfın sanal fonksiyonlarının adreslerini içeren bir tablodur. v-table, çalışma zamanında doğru sanal fonksiyonun çağrılması için kullanılır.

- v-table nasıl çalışır?

1. Derleyici, her sınıf için sanal fonksiyonlarını içeren bir v-table oluşturur. Bu tablo, sanal fonksiyonların adreslerini içerir ve sınıfın tüm nesneleri tarafından paylaşılır.

2. Bir sınıfın nesnesi oluşturulduğunda, nesnenin içinde bir işaretçi (_vptr) bulunur ve bu işaretçi sınıfın v-table'ına işaret eder.

3. Sanal bir fonksiyon çağrıldığında, v-table kullanılarak fonksiyonun adresine erişilir ve fonksiyon çalıştırılır.

```CPP
class Hayvan {
public:
    virtual void sesCikar() {
        // ...
    }
};

class Kopek : public Hayvan {
public:
    void sesCikar() override {
        // ...
    }
};

```

- Yukarıdaki örnekte, Hayvan sınıfında bir sanal fonksiyon olan sesCikar tanımlanmıştır ve Kopek sınıfı bu fonksiyonu geçersiz kılar (override). Derleyici, Hayvan ve Kopek için iki ayrı v-table oluşturur:

```
Hayvan sınıfının v-table'ında, Hayvan::sesCikar fonksiyonunun adresi bulunur.
Kopek sınıfının v-table'ında ise, Kopek::sesCikar fonksiyonunun adresi bulunur.
```
- Eğer bir Hayvan işaretçisi veya referansı üzerinden sesCikar fonksiyonu çağrılırsa, v-table kullanılarak doğru fonksiyonun (örneğin, Hayvan::sesCikar veya Kopek::sesCikar) adresine gidilir ve fonksiyon çalıştırılır.

- v-table, çalışma zamanında polimorfizm sağlamak için kullanılan önemli bir mekanizmadır. Bu mekanizma, temel sınıfın işaretçi veya referansları üzerinden doğru türetilmiş sınıfın sanal fonksiyonlarının çağrılmasını sağlar. Bununla birlikte, v-table kullanımı, bir miktar performans maliyetine sahiptir, çünkü sanal fonksiyon çağrıları sırasında ekstra işaretçi dereferanslamaları gerçekleştirilir. Ancak bu maliyet, genellikle polimorfizmin sağladığı avantajlar ile dengelenir ve kodun modülerlik, esneklik ve anlaşılabilirlik sağlamasına yardımcı olur.

- Daha detaylı olarak inceleyelim:

```CPP
#include <iostream>

class Hayvan {
public:
    virtual void sesCikar() const {
        std::cout << "Bir hayvan sesi çıkarıyor." << std::endl;
    }
};

class Kopek : public Hayvan {
public:
    void sesCikar() const override {
        std::cout << "Hav! Hav!" << std::endl;
    }
};

int main() {
    Hayvan* hayvan = new Kopek(); // 'hayvan' işaretçisi, 'Kopek' nesnesini işaret ediyor
    hayvan->sesCikar(); // v-table kullanılarak doğru fonksiyon çağrılır, çıktı: "Hav! Hav!"
    delete hayvan;
}

```
> Yukarıdaki örnekte, Hayvan temel sınıfından türetilmiş olan Kopek sınıfının bir nesnesi oluşturuluyor ve hayvan adlı bir Hayvan işaretçisi bu nesneyi işaret ediyor. Bu durumda, hayvan->sesCikar() ifadesi çalıştırıldığında, v-table kullanılarak işaret edilen nesnenin gerçek türüne (Kopek) göre doğru sesCikar fonksiyonu çağrılır.

**Bu örnekte v-table nasıl çalışır:**
1. Hayvan ve Kopek sınıfları için iki ayrı v-table oluşturulur. Hayvan v-table'ında Hayvan::sesCikar fonksiyonunun adresi, Kopek v-table'ında ise Kopek::sesCikar fonksiyonunun adresi bulunur.

2. Kopek nesnesi oluşturulduğunda, nesnenin içindeki _vptr işaretçisi Kopek sınıfının v-table'ına işaret eder.

3. hayvan->sesCikar() ifadesi çalıştırıldığında, _vptr işaretçisi üzerinden Kopek v-table'ına gidilir ve Kopek::sesCikar fonksiyonunun adresine erişilir. Ardından bu fonksiyon çağrılır ve "Hav! Hav!" çıktısı elde edilir.

- v-table, çalışma zamanında polimorfizm sağlamak için kullanılan temel bir mekanizmadır ve C++ dilinde önemli bir rol oynar. Bu mekanizma, sanal fonksiyonları doğru şekilde çağırmak için temel sınıfın işaretçi veya referansları üzerinden gerçekleştirilen işlemleri destekler. V-table kullanımı, kodun daha modüler, esnek ve anlaşılır olmasına yardımcı olur ve nesne yönelimli programlama paradigmalarının avantajlarından yararlanmayı sağlar.

# Clone Idiom

- Clone idiom, C++ dilinde kopyalama işlemlerini gerçekleştirmek için kullanılan bir programlama modelidir. Clone idiom, temelde bir sınıfın nesnelerini kopyalamak için özelleştirilmiş bir kopyalama mekanizması sağlar. Bu mekanizma, genellikle sanal bir kopyalama fonksiyonu (örneğin, clone()) ile gerçekleştirilir ve çalışma zamanında polimorfizm sayesinde doğru türetilmiş sınıfın kopyalama işlemi yapılabilir.

- Clone idiom, özellikle temel sınıfın işaretçi veya referansları üzerinden kopyalama işlemi yapılması gereken durumlarda kullanılır. Bu durum, temel sınıfın destrüktörünün sanal olduğu ve temel sınıfın işaretçi veya referansları üzerinden doğru türetilmiş sınıfın destrüktörlerinin çağrılması gerektiği nesne yönelimli programlama senaryolarında sıkça karşılaşılan bir ihtiyaçtır.

**Clone idiom'un uygulanması için genellikle aşağıdaki adımlar izlenir:**

1. Temel sınıfta, clone() adlı sanal bir fonksiyon tanımlanır. Bu fonksiyon, temel sınıfın nesnesinin kopyasını oluşturmak için kullanılacaktır.

2. Türetilmiş sınıflarda, clone() fonksiyonu geçersiz kılınarak (override) sınıfa özgü kopyalama işlemi sağlanır. Bu fonksiyonlar, genellikle türetilmiş sınıfın kopya yapıcılarını kullanarak kopya nesneler oluşturur.

3. Temel sınıfın işaretçi veya referansları üzerinden kopyalama işlemi yapılırken, clone() fonksiyonu kullanılarak çalışma zamanında doğru türetilmiş sınıfın kopyalama işlemi gerçekleştirilir.

- İşte bir örnek:

```CPP
#include <iostream>

class Hayvan {
public:
    virtual ~Hayvan() = default; // Sanal destrüktör

    virtual Hayvan* clone() const = 0; // Sanal clone fonksiyonu
};

class Kopek : public Hayvan {
public:
    Kopek* clone() const override { // Kopek sınıfı için clone fonksiyonu geçersiz kılma
        return new Kopek(*this); // Kopya yapıcı kullanarak yeni bir Kopek nesnesi oluşturma
    }
};

int main() {
    Hayvan* hayvan = new Kopek();
    Hayvan* hayvanKopya = hayvan->clone(); // 'clone()' fonksiyonu kullanarak doğru kopyalama işlemi yapılır

    delete hayvan;
    delete hayvanKopya;
}

```
> Yukarıdaki örnekte, Hayvan temel sınıfında clone() adlı sanal bir fonksiyon tanımlanmıştır. Bu fonksiyon, çalışma zamanında polimorfizm sayesinde türetilmiş sınıfların kopyalama işlemlerini gerçekleştirmek için kullanılacaktır. Kopek sınıfı, clone() fonksiyonunu geçersiz kılarak kendi kopyalama işlemini sağlar. Bu örnekte, Kopek sınıfının kopya yapıcısı kullanılarak yeni bir Kopek nesnesi oluşturulur.

- main() fonksiyonunda, Hayvan temel sınıfından türetilmiş olan Kopek sınıfının bir nesnesi oluşturuluyor ve hayvan adlı bir Hayvan işaretçisi bu nesneyi işaret ediyor. Hayvan* hayvanKopya = hayvan->clone(); ifadesi çalıştırıldığında, clone() fonksiyonu kullanılarak işaret edilen nesnenin gerçek türüne (Kopek) göre doğru kopyalama işlemi gerçekleştirilir ve hayvanKopya işaretçisi bu kopya nesneyi işaret eder.

- Clone idiom, nesne yönelimli programlama paradigmalarında sıkça kullanılan bir kopyalama modelidir. Bu idiom, temel sınıfın işaretçi veya referansları üzerinden kopyalama işlemlerini gerçekleştirmek için çalışma zamanında polimorfizmi kullanır ve böylece kodun daha modüler, esnek ve anlaşılır olmasına yardımcı olur. Clone idiom, temel sınıfın destrüktörünün sanal olduğu ve doğru türetilmiş sınıfın destrüktörlerinin çağrılması gerektiği senaryolarda özellikle kullanışlıdır.

# Virtual Destructor
- Virtual destructor (sanal yıkıcı), C++ dilinde nesne yönelimli programlamada kullanılan önemli bir kavramdır. Virtual destructor, bir temel sınıfın işaretçi veya referansları üzerinden doğru türetilmiş sınıfın destrüktörlerinin çağrılması için kullanılır. Bu durum, çalışma zamanında polimorfizm sayesinde gerçekleştirilir ve böylece kodun daha modüler, esnek ve anlaşılır olmasına yardımcı olur.

- Sanal yıkıcıların kullanılması gereken durumlar, genellikle temel sınıfın işaretçi veya referansları üzerinden dinamik olarak türetilmiş sınıf nesnelerinin yaşam sürelerinin yönetildiği nesne yönelimli programlama senaryolarında ortaya çıkar. Sanal yıkıcı kullanılmazsa, temel sınıfın işaretçi veya referansları üzerinden türetilmiş sınıf nesneleri silindiğinde sadece temel sınıfın destrüktörü çağrılır ve türetilmiş sınıfın destrüktörü çağrılmaz. Bu durum, kaynak sızıntılarına ve bellek bozulmalarına neden olabilir.

- Sanal yıkıcılar kullanılarak bu sorun çözülür. İşte bir örnek:

```CPP
#include <iostream>

class Hayvan {
public:
    Hayvan() {
        std::cout << "Hayvan oluşturuldu." << std::endl;
    }

    virtual ~Hayvan() {
        std::cout << "Hayvan silindi." << std::endl;
    }
};

class Kopek : public Hayvan {
public:
    Kopek() {
        std::cout << "Kopek oluşturuldu." << std::endl;
    }

    ~Kopek() {
        std::cout << "Kopek silindi." << std::endl;
    }
};

int main() {
    Hayvan* hayvan = new Kopek();
    delete hayvan;
}

```
> Yukarıdaki örnekte, Hayvan sınıfında sanal bir yıkıcı tanımlanmıştır. Kopek sınıfı ise Hayvan sınıfından türetilmiştir ve kendi yıkıcısını içerir. main() fonksiyonunda, Hayvan işaretçisi üzerinden bir Kopek nesnesi oluşturulur ve silinir. Sanal yıkıcı kullanıldığı için, işaretçinin nesnesini silerken hem Kopek hem de Hayvan sınıflarının yıkıcıları doğru sırada çağrılır. Çıktı şu şekildedir:

```
Hayvan oluşturuldu.
Kopek oluşturuldu.
Kopek silindi.
Hayvan silindi.

```

- Sanal yıkıcılar, temel sınıfın işaretçi veya referansları üzerinden doğru türetilmiş sınıfın yıkıcılarını çağırmak için kullanılır. Bu sayede, nesne yönelimli programlama senaryolarında kaynakların doğru bir şekilde temizlenmesi ve bellek yönetiminin daha güvenli olması sağlanır.

Sanal yıkıcılar, çalışma zamanında polimorfizmi kullanarak doğru türetilmiş sınıfın yıkıcısını çağırır. Bu, türetilmiş sınıfların yıkıcıları temel sınıfın yıkıcısından önce çağrılacağı anlamına gelir, bu da kaynakların doğru sırayla serbest bırakılmasına ve potansiyel bellek sorunlarının önlenmesine yardımcı olur.

- Sanal yıkıcılar kullanılırken dikkat edilmesi gereken bazı hususlar vardır:

1. Sanal yıkıcılar, temel sınıfın işaretçi veya referansları üzerinden nesnelerin yaşam sürelerinin yönetildiği durumlarda kullanılmalıdır. Eğer bu tür bir durum yoksa, sanal yıkıcı kullanmaya gerek yoktur.

2. Sanal yıkıcılar, performans açısından bir maliyete sahiptir. Sanal yıkıcılar, sanal fonksiyon tablosu (vtable) üzerinden çağrıldığı için, normal yıkıcılara göre biraz daha yavaş çalışabilirler. Bu nedenle, performans kritik uygulamalarında bu maliyeti göz önünde bulundurarak karar verilmelidir.

3. Sanal yıkıcılar, sadece temel sınıflarda tanımlanmalıdır. Türetilmiş sınıflar, temel sınıfın sanal yıkıcısını otomatik olarak devralır ve geçersiz kılma işlemi yapılmasına gerek yoktur.

- Sanal yıkıcılar, C++ dilinde nesne yönelimli programlamada kullanılan önemli bir kavramdır. Doğru kullanımı, kodun daha modüler, esnek ve anlaşılır olmasına yardımcı olurken, aynı zamanda kaynakların doğru bir şekilde yönetilmesini ve bellek sorunlarının önlenmesini sağlar.

# Smart - Raw Pointers

- C++'da, işaretçi türleri genellikle iki kategoriye ayrılır: raw (ham) işaretçiler ve smart (akıllı) işaretçiler. İkisi arasındaki temel fark, bellek yönetimi ve özellikleri açısından nasıl çalıştıklarıdır. Şimdi her birini ayrı ayrı inceleyelim.
- **Raw İşaretçiler:**
Raw işaretçiler, C++ dilinin temel özelliklerinden biridir ve C dilinden miras alınmıştır. Raw işaretçiler, bellek adreslerini saklayan ve nesnelere erişmek için kullanılan basit ve düşük seviyeli işaretçilerdir. Raw işaretçiler ile yapılan bellek yönetimi manuel olarak yapılır ve kullanıcının new ve delete operatörlerini kullanarak dinamik bellek tahsis etmesi ve serbest bırakması gerekir.

**Raw işaretçilerin avantajları:**
1. Düşük seviyeli sistem programlaması için uygunluk.
2. Performans açısından düşük maliyet.

**Raw işaretçilerin dezavantajları:**
1. Manuel bellek yönetimi gerekir (new ve delete operatörleri ile).
2. Dangling (sallanan) işaretçi ve bellek sızıntısı gibi potansiyel sorunlara yol açabilir.

**Smart İşaretçiler:**
- Smart işaretçiler, C++ dilinde modern bellek yönetimi için kullanılan daha güvenli ve otomatik bir işaretçi türüdür. C++11 standardı ile birlikte gelen smart işaretçiler, bellek yönetimini otomatikleştirir ve böylece bellek sızıntısı ve dangling işaretçi gibi potansiyel sorunların önüne geçer. Smart işaretçiler, nesnelerin yaşam sürelerini yönetir ve kullanılmayan nesnelerin belleğini otomatik olarak serbest bırakır.

- C++ dilinde üç ana smart işaretçi türü vardır:

1. **std::unique_ptr:** Bir nesnenin belleğini yalnızca bir unique_ptr tarafından yönetilir ve otomatik olarak serbest bırakılır. Nesnelerin sahipliği, bir unique_ptr'dan diğerine taşınabilir (move) ancak kopyalanamaz.

2. **std::shared_ptr:** Bir nesnenin belleği birden fazla shared_ptr tarafından paylaşılabilir ve nesne, son referansın ortadan kalkmasıyla otomatik olarak serbest bırakılır. shared_ptr'lar kopyalanabilir ve taşınabilir.

3. **std::weak_ptr:** shared_ptr ile birlikte kullanılan ve döngülü referans problemini önlemeye yardımcı olan bir işaretçi türüdür. weak_ptr'lar nesnelerin yaşam sürelerini yönetmez ve kendi başlarına bir nesneye erişemez.

- **Smart işaretçilerin avantajları:**

1. Otomatik bellek yönetimi sağlar, böylece bellek sızıntısı ve dangling işaretçi gibi potansiyel sorunları önler.
2. Nesnelerin yaşam sürelerini yönetir ve kullanılmayan nesnelerin belleğini otomatik olarak serbest bırakır.
3. Modern C++ uygulamalarında bellek yönetimi için önerilen ve kabul gören yöntemdir.

**Smart işaretçilerin dezavantajları:**
1. Raw işaretçilere göre biraz daha fazla maliyete sahiptir, çünkü otomatik bellek yönetimi ve referans sayma işlemleri gerçekleştirirler.
2. Düşük seviyeli sistem programlaması için raw işaretçilere kıyasla daha az uygun olabilirler.
- Özetle, raw işaretçiler ve smart işaretçiler, C++ dilinde farklı amaçlar için kullanılan iki işaretçi türüdür. Raw işaretçiler, düşük seviyeli sistem programlaması ve performans açısından düşük maliyete ihtiyaç duyulan durumlarda kullanılabilir. Ancak, manuel bellek yönetimi gerektirir ve potansiyel bellek sorunlarına neden olabilir.

- Smart işaretçiler ise, modern C++ uygulamalarında bellek yönetimi için önerilen ve daha güvenli olan işaretçi türüdür. Otomatik bellek yönetimi sağlar ve potansiyel bellek sorunlarını önler. Smart işaretçilerin kullanımı, kodun daha güvenli, modüler ve anlaşılır olmasına yardımcı olur.

# Memory - Resource Leak

- Memory leak (bellek sızıntısı) ve resource leak (kaynak sızıntısı) terimleri, bir programın çalışması sırasında kaynakların doğru şekilde serbest bırakılmamasından kaynaklanan sorunları ifade eder. Bu tür sorunlar, programın performansını düşürebilir, sistem kaynaklarının tükenmesine yol açabilir ve hatta programın beklenmedik şekilde çökmesine neden olabilir.

**Memory Leak (Bellek Sızıntısı):**
- Bellek sızıntısı, bir programın dinamik olarak tahsis ettiği belleği (örneğin, C++'da new veya malloc kullanarak) serbest bırakmaması durumunda meydana gelen bir problemdir. Bu durumda, tahsis edilen bellek alanı işe yaramaz hale gelir ve programın çalışması sırasında bellek kullanımı giderek artar. Bellek sızıntıları, uzun süre çalışan uygulamalar için özellikle ciddi sorunlara yol açabilir.
- Bellek sızıntılarından kaçınmak için, dinamik olarak tahsis edilen belleğin uygun şekilde serbest bırakılması gereklidir. C++ dilinde, bu genellikle delete veya free operatörlerini kullanarak yapılır. Modern C++ uygulamalarında, bellek yönetimini kolaylaştırmak ve bellek sızıntılarını önlemek için smart işaretçiler (örneğin, std::unique_ptr ve std::shared_ptr) kullanmak önerilir.

**Resource Leak (Kaynak Sızıntısı):**
- Kaynak sızıntısı, bellek dışındaki sistem kaynaklarının (örneğin, dosya tanıtıcıları, soketler, mutex'ler, veritabanı bağlantıları) doğru şekilde serbest bırakılmaması durumunda meydana gelen bir problemdir. Kaynak sızıntıları, bellek sızıntılarına benzer şekilde, programın performansını düşürebilir, sistem kaynaklarının tükenmesine yol açabilir ve beklenmedik çökmelere neden olabilir.

- Kaynak sızıntılarından kaçınmak için, kullanılan kaynakların uygun şekilde serbest bırakılması ve kapatılması önemlidir. C++ dilinde, bu genellikle kullanılan kaynakları kapatmak veya serbest bırakmak için gerekli fonksiyonları çağırarak yapılır (örneğin, fclose dosya tanıtıcılarını kapatmak için). Modern C++ uygulamalarında, kaynak yönetimini kolaylaştırmak ve kaynak sızıntılarını önlemek için RAII (Resource Acquisition Is Initialization) yöntemi kullanılabilir. Bu yöntemde, kaynakların yaşam süreleri nesnelerin yaşam süreleriyle eşleştirilir ve nesnelerin yıkıcıları kaynakları serbest bırakmak için kullanılır. Bu şekilde, kaynaklar otomatik olarak yönetilir ve kaynak sızıntıları önlenir.

- Özetle, memory leak (bellek sızıntısı) ve resource leak (kaynak sızıntısı), bir programın çalışması sırasında kaynakların doğru şekilde serbest bırakılmamasından kaynaklanan sorunlardır. Bu tür sorunlar, performans düşüşü, sistem kaynaklarının tükenmesi ve beklenmedik çökmelere neden olabilir.

- Bellek sızıntılarından ve kaynak sızıntılarından kaçınmak için, uygun şekilde serbest bırakma ve kapatma işlemleri gerçekleştirilmeli ve modern C++ uygulamalarında yöntemler ve teknikler kullanılmalıdır. Smart işaretçiler ve RAII yöntemi gibi teknikler, bellek ve kaynak yönetimini otomatikleştirerek, bellek sızıntıları ve kaynak sızıntıları riskini azaltır ve daha güvenli, sağlam ve etkili programlar geliştirmeye yardımcı olur.

# Final Keyword

- C++ dilinde final anahtar kelimesi, sınıf hiyerarşisi ve sanal fonksiyonların üzerine yazılmasını (override) kısıtlayarak nesne yönelimli programlama prensipleriyle ilgili kontrolleri sağlamak için kullanılır. final anahtar kelimesi, iki farklı bağlamda kullanılabilir: sınıflar ve sanal fonksiyonlar.

**Sınıflar için final:**

- Bir sınıfın son sınıf (final class) olarak tanımlanması, o sınıftan başka sınıfların türetilmesini önler. Başka bir deyişle, bir sınıfın son sınıf olarak belirtilmesi, o sınıfın miras alınmasını yasaklar. Bu, sınıf hiyerarşisinin belirli bir noktada sonlandırılması gerektiğinde kullanışlıdır. Bir sınıfı final olarak işaretlemek için, sınıf bildiriminin ardından final anahtar kelimesi kullanılır:

```CPP
class MyBaseClass final {
    // ...
};

```
> Bu durumda, MyBaseClass adlı sınıf finaldir ve başka sınıfların bu sınıftan türetilmesine izin verilmez.

**Sanal fonksiyonlar için final:**

- Bir sanal fonksiyonun son fonksiyon (final function) olarak tanımlanması, o fonksiyonun alt sınıflar tarafından üzerine yazılmasını (override) engeller. Böylece, belirli bir sınıfta sanal fonksiyonun davranışını kilitleyebilir ve daha fazla değiştirilmesini önleyebilirsiniz. Bir sanal fonksiyonu final olarak işaretlemek için, fonksiyon bildiriminin ardından final anahtar kelimesi kullanılır:

```CPP
class MyBaseClass {
public:
    virtual void myFunction() final {
        // ...
    }
};

```
> Bu durumda, MyBaseClass adlı sınıftaki myFunction adlı sanal fonksiyon finaldir ve alt sınıflar tarafından üzerine yazılamaz.

- Özetle, C++'daki final anahtar kelimesi, sınıf hiyerarşisi ve sanal fonksiyonların üzerine yazılmasını kısıtlayarak nesne yönelimli programlama prensipleriyle ilgili kontroller sağlar. final anahtar kelimesi, sınıfın son sınıf olarak belirtilmesine ve sanal fonksiyonların daha fazla değiştirilmesini engelleyerek istenmeyen durumların önlenmesine yardımcı olur.

# Diamond Formation

- Diamond problem" ya da "Diamond formation", nesne yönelimli programlama dillerinde, özellikle çoklu kalıtım (multiple inheritance) özelliği bulunan dillerde (örneğin C++) karşılaşılan bir sorundur. Diamond problemi, aynı sınıfın iki veya daha fazla kez bir sınıf hiyerarşisinde ortaya çıktığı durumlarda, türetilen sınıfların hangi temel sınıfın üyesini kullanacağıyla ilgili bir belirsizlik oluşmasıdır.

- Diamond problemi için tipik bir örnek aşağıdaki gibi bir sınıf hiyerarşisi kullanılabilir:

```CPP
       A
      / \
     B   C
      \ /
       D

```
> Bu durumda, sınıflar B ve C, sınıf A'dan türetilmiştir ve sınıf D, hem sınıf B hem de sınıf C'den türetilmiştir. Bu hiyerarşi nedeniyle, sınıf D'nin bir sınıf A nesnesine iki kez sahip olduğu ortaya çıkar. Bu, sınıf D içinde sınıf A üyelerine erişimle ilgili belirsizliklere neden olabilir.

- C++ dilinde, diamond problemine çözüm olarak "sanal kalıtım" (virtual inheritance) kullanılır. Sanal kalıtım, çoklu kalıtımda ortak temel sınıfın yalnızca bir kez miras alınmasını sağlar. Böylece, türetilen sınıflarda ortak temel sınıf üyelerine erişimle ilgili belirsizlikler önlenir.

- Sanal kalıtımı kullanarak diamond problemine bir çözüm uygulamak için, virtual anahtar kelimesi ile kalıtım gerçekleştirilir:

```CPP
class A {
public:
    void someFunction();
};

class B : virtual public A {
    // ...
};

class C : virtual public A {
    // ...
};

class D : public B, public C {
    // ...
};

```
- Bu durumda, hem sınıf B hem de sınıf C, sınıf A'dan sanal olarak türetilir ve sınıf D'nin yalnızca tek bir sınıf A nesnesine sahip olduğunu garanti eder. Böylece, sınıf D içinde sınıf A üyelerine erişimle ilgili belirsizlikler ortadan kalkar.

- Özetle, diamond problemi, çoklu kalıtım özelliği bulunan nesne yönelimli programlama dillerinde ortaya çıkan bir sorundur ve aynı sınıfın birden fazla kez bir sınıf hiyerarşisinde ortaya çıkmasıyla ilgilidir. C++ dilinde, diamond problemine çözüm olarak sanal kalıtım kullanılır ve ortak temel sınıfın yalnızca bir kez miras alınmasını sağlar.

# Virtual Inheritance
- Virtual inheritance (sanal kalıtım), C++ dilinde çoklu kalıtım (multiple inheritance) kullanırken ortaya çıkan bazı sorunları çözmek için kullanılan bir tekniktir. Sanal kalıtım, özellikle diamond problemi olarak bilinen sınıf hiyerarşisindeki belirsizlikleri gidermeye yardımcı olur. Sanal kalıtım, bir sınıfın başka bir sınıftan türetilirken ortak temel sınıfın (base class) yalnızca bir kez miras alınmasını sağlar.

- Sanal kalıtım kullanarak, diamond problemi gibi sorunları önleyebilirsiniz. Diamond problemi, aşağıdaki gibi bir sınıf hiyerarşisinde ortaya çıkar:

```
       A
      / \
     B   C
      \ /
       D

```
> Sınıf B ve sınıf C, sınıf A'dan türetilmiştir ve sınıf D ise hem sınıf B hem de sınıf C'den türetilmiştir. Bu hiyerarşi nedeniyle, sınıf D'nin bir sınıf A nesnesine iki kez sahip olduğu ortaya çıkar. Bu, sınıf D içinde sınıf A üyelerine erişimle ilgili belirsizliklere neden olabilir.

- Sanal kalıtımı kullanarak diamond problemine bir çözüm uygulamak için, virtual anahtar kelimesi ile kalıtım gerçekleştirilir:

```CPP
class A {
public:
    void someFunction();
};

class B : virtual public A {
    // ...
};

class C : virtual public A {
    // ...
};

class D : public B, public C {
    // ...
};

```
- Bu durumda, hem sınıf B hem de sınıf C, sınıf A'dan sanal olarak türetilir ve sınıf D'nin yalnızca tek bir sınıf A nesnesine sahip olduğunu garanti eder. Böylece, sınıf D içinde sınıf A üyelerine erişimle ilgili belirsizlikler ortadan kalkar.

- Özetle, virtual inheritance (sanal kalıtım), C++ dilinde çoklu kalıtım kullanırken ortaya çıkan belirsizlikleri ve sorunları çözmek için kullanılan bir tekniktir. Sanal kalıtım, ortak temel sınıfın yalnızca bir kez miras alınmasını sağlayarak, sınıf hiyerarşisindeki belirsizlikleri giderir ve kodun daha güvenli ve anlaşılır olmasına katkıda bulunur.

# Exception Handling

- Exception handling (istisna yönetimi), programlarınızdaki hataların ve beklenmedik durumların etkili bir şekilde ele alınmasını sağlamak için kullanılan bir programlama teknikidir. C++ dilinde, exception handling mekanizması, istisnaları temsil eden nesnelerle çalışarak ve istisnaları yakalayarak ve uygun şekilde işleyerek bu tür durumları yönetir.

- C++ exception handling, temelde üç anahtar kelimeyle gerçekleştirilir: try, catch ve throw.

1. try: try bloğu, istisna oluşturabilecek kod parçacıklarını içeren bloktur. Bu blok, hata oluşabilecek potansiyel kodları sarmalar ve eğer bir istisna fırlatılırsa (throw), bu istisnayı yakalayan (catch) uygun bloğa geçiş yapar.

- catch: catch bloğu, try bloğundan fırlatılan (throw) istisnaları yakalayarak ve ele alarak çalışır. Birden fazla catch bloğu bulunabilir ve farklı istisna türlerini işleyebilir. İstisna yakalandığında, catch bloğu içindeki kod çalıştırılır ve istisna ile ilgili uygun eylemler gerçekleştirilir.

- throw: throw anahtar kelimesi, bir istisna fırlatmak (oluşturmak) için kullanılır. İstisna nesneleri, temel veri türleri, sınıf nesneleri veya özel olarak tanımlanmış istisna sınıflarının nesneleri olabilir.

- Basit bir exception handling örneği:

```CPP
#include <iostream>

int main() {
    try {
        int a = 10;
        int b = 0;
        if (b == 0) {
            throw "Division by zero error";
        }
        int result = a / b;
        std::cout << "Result: " << result << std::endl;
    }
    catch (const char* error_msg) {
        std::cerr << "Exception caught: " << error_msg << std::endl;
    }

    return 0;
}

```
> Bu örnekte, try bloğu içinde bir bölme işlemi gerçekleştirilmektedir. Eğer bölen (b) sıfır ise, bir istisna fırlatılır (throw) ve bu durumda istisna nesnesi olarak bir C-string kullanılır. catch bloğu, bu türden bir istisna nesnesini yakalar ve hatayı ekrana yazdırır.

- Özetle, exception handling, programlarda beklenmedik durumların ve hataların yönetilmesi için kullanılan bir tekniktir. C++ dilinde, try, catch ve throw anahtar kelimeleri kullanılarak istisna yönetimi sağlanır. 
























