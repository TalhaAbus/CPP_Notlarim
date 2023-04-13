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



















