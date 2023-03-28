# Algorithm
- STL için kullanılan bir dizi algoritma fonksiyonu sağlar.
- STL'nin temel container sınıfları olan vector, list, set, map gibi sınıflarla birlikte kullanılabilir.

# Any (C++17)

- Degiskenlerin turu bilinmeden depolanmasini saglar.
- Herhangi bir ture sahip nesnenin depolanmasini ve erisimini saglar.
- Tur ve deger ayri depolandigi icin turu bilinmeyen nesnelerin degeri degistirilebilir ya da turu donusturulebilir.

# Array (C++11) [Containers]

- Boyutu sabit olan diziler için bir veri türü sunar. Dizi boyutu, dizi nesnesi oluşturulurken belirtilir ve değiştirilemez.
- Sabit boyutlu dizileri yönetmek için kullanılır.
- Normal dizilerin aksine bir geçici nesne olarak değil, bir değer olarak geçirilebilir ve fonksiyonlardan geri döndürülebilir.

# Atomic (C++11)
- atomic islemler: Coklu thread tarafindan ayni anda erisilen belleklerin okunmasi ve yazilmasi islemlerini guvenli gerceklestirir.

# Barrier (C++20)

- Senkronizasyon için bir bariyer mekanizması sağlar. Bir bariyer, bir grup thread'in bir noktada toplanması ve burada senkronize bir şekilde çalışmasını sağlar.
- Bir bariyer, bir veya daha fazla thread'in bir noktada toplanması ve devam etmek için diğer thread'lerin tamamlanmasını beklemesi gerektiği senaryolarda kullanışlıdır.

# Bit (C++20)

- bit manipülasyonu yapmak için kullanılır. Bu başlık dosyası, özellikle bit işlemleri gerektiren uygulamalar için yararlıdır.
- başlık dosyası, C dilindeki bit işlemleri için tanımlanan işaretli ve işaretsiz tamsayı veri türlerine karşılık gelen C++ tamsayı veri türlerinin yanı sıra, bit işlemleri için kullanılacak fonksiyonlar ve sabitler de tanımlar.

# Bitset (Default)
- Bu sınıf, bir bit dizisi temsil eder ve birçok bit işlemi yapmak için kullanılabilir.
- sabit boyutlu bir bit dizisini temsil eder ve bu boyut compile-time'da belirtilir. Yani, std::bitset nesneleri oluşturulduktan sonra boyutları değiştirilemez.

# Cassert (C library)
- programın çeşitli hatalarını kontrol etmek için kullanılan fonksiyon ve makroları içerir.
- İçerdiği fonksiyon ve makrolarla, programcıların kodlarında belirledikleri koşulların doğru olup olmadığını kontrol etmelerine imkan sağlar.
- başlık dosyasında yer alan en yaygın kullanılan fonksiyon, "assert" fonksiyonudur. Bu fonksiyon, belirtilen koşulun doğru olup olmadığını kontrol eder. Eğer koşul yanlışsa, program derhal sonlandırılır ve bir hata mesajı yazılır.

# cctype (C library)
- karakter işleme işlevlerinin yer aldığı bir başlık dosyasıdır. Bu işlevler, bir karakterin özelliklerini belirlemek için kullanılır. Bu işlevler, karakterlerin harf, rakam, büyük harf, küçük harf vb. olup olmadığını kontrol etmek için kullanılır.

# cerrno (C library)

- hata kodlarını işlemek için kullanılan bir başlık dosyasıdır. Bu başlık dosyası, hata kodlarının sayısal değerleriyle ilişkili sabitleri tanımlar ve bu kodların tanımlanmasına, atılmasına ve işlenmesine yardımcı olur.
- Başlık dosyası, programın hata kodlarını elde etmesi, bunları okuması ve hata kodlarına uygun şekilde işlemesi için kullanılan birkaç farklı fonksiyonu içerir.

# cfloat (C library)
- ondalık sayılarla ilgili sabitlerin tanımlandığı bir C++ başlık dosyasıdır. Bu sabitler, kayan nokta sayılarının sınırlarını belirleyen minimum ve maksimum değerleri temsil eder.

- Bu başlık dosyası, genellikle sayısal hesaplamalar ve işlemler için kullanılır. Özellikle, sayısal hesaplamalar sırasında sınırları aşma durumlarının kontrolü için kullanılabilir.

# charconv (C++20)

- sayısal verilerin karakter dizilerine dönüştürülmesi ve karakter dizilerinin sayısal verilere dönüştürülmesi için kullanılan işlevleri içerir.
- Özellikle, std::from_chars ve std::to_chars işlevleri, sayısal veri tipleri ve karakter dizileri arasında dönüştürmeler yapmak için kullanılır. Bu işlevler, önceki C++ standartlarında yer alan atoi, atof, sprintf ve sscanf işlevlerine kıyasla daha güvenlidir.

# chrono (C++11)

- chrono başlık dosyası, zaman ölçme ve zaman aralıklarını hesaplama işlemleri için C++11'den itibaren kullanılabilen bir standart kütüphanedir. Bu başlık dosyasında, zamanı temsil etmek için kullanılan sınıflar, zaman aralıkları arasında dönüşümler yapmak için kullanılan ölçek faktörleri ve zamanla ilgili diğer yararlı araçlar yer almaktadır.

# climits (C library)
- Bu başlık dosyası, C++ programlamasında kullanılan temel tamsayı tip boyutları hakkında bilgi veren ve bu boyutlar için sabit değerler sağlayan makro tanımlamaları içerir.
- Bu başlık dosyası, herhangi bir platformda tam sayı türlerinin boyutlarına ilişkin bilgiler sağlamak için kullanılabilir. Bu bilgiler, sizeof operatörü ile sorgulanabilir.

- Bu başlık dosyası ayrıca, tamsayı türlerinin maksimum ve minimum değerlerini belirten makroları içerir.

# clocale (C library)

- C programlama dilinde yer alan locale.h başlık dosyasının C++ standart kütüphanesi karşılığıdır. Bu başlık dosyası, C++ programları için yerel ayarların yönetimine olanak sağlar.

- Bu başlık dosyası, C fonksiyonlarını C++ diline uyarlamak için kullanılır:

# cmath (C library)

- matematiksel fonksiyonları içerir. Bu fonksiyonlar, programlama sırasında sıkça kullanılan trigonometrik, logaritmik, üs, karekök, trigonometrik invers, hiperbolik trigonometrik, radyan/derece dönüşümü gibi işlemleri yapmamızı sağlar.

# compare (C++20)

- karşılaştırma işlemleri için üç yöntem sağlar: strong_order, weak_order ve partial_order. Bu yöntemlerin her biri, karşılaştırılan nesnelerin sıralanabilirliği durumunda geri döndürülecek sonucu belirler.
- başlık dosyası, farklı türlerin karşılaştırılması için kullanılan üç yöntemi içerir: strong ordering, partial ordering ve weak ordering.

# complex (Default)

- kompleks sayıları temsil etmek için kullanılır. Kompleks sayılar, gerçek ve sanal bileşenlere sahip sayılardır ve matematiksel işlemlerde sıklıkla kullanılır.

- d::complex sınıfı, bir gerçek sayı ve bir sanal sayı olmak üzere iki bileşenden oluşur. Bu bileşenler, genellikle std::complex<double, std::complex<float veya std::complex<long double türlerinde tanımlanırlar.

# concepts (C++20)
- dilin şablon özelliklerini daha güçlü ve anlaşılır kılmak için tasarlanmış bir özelliktir. C++20 ile birlikte tanıtılmıştır ve şablon metaprogramlama dünyasında büyük bir etki yaratmıştır. Kavramlar, şablon parametrelerinin beklenen özelliklerini ve davranışlarını açıkça belirtmenize olanak tanır. Bu sayede, daha anlaşılır hata mesajları ve daha güçlü tip denetimi sağlar

# condition_variable (C++11)

- condition_variable başlık dosyası, çoklu iş parçacığı uygulamaları için senkronizasyon araçları sağlayan C++11 standardı ile tanıtılan bir başlık dosyasıdır. Bu başlık dosyası, C++11'de tanıtılan "std::thread" sınıfı gibi diğer C++11 çoklu iş parçacığı araçlarıyla birlikte kullanılabilir.

# coroutine (C++20)

- dilde eşzamanlı programlama için koşut çalıştırma ve asenkron çalıştırma sağlayan yeni bir mekanizma olan coroutine'leri kullanmak için gerekli sınıf ve fonksiyonları içerir. Coroutine'ler, iş parçacıklarının maliyetlerine katlanmadan daha etkin eşzamanlı programlama yapmaya yardımcı olur.

# csetjmp (C library)

- setjmp ve longjmp işlevlerini içerir. Bu işlevler, C dili kodu içinde hatayla başa çıkmak veya program akışını programcı tarafından belirlenmiş bir noktaya atlamak için kullanılır.

- setjmp işlevi, programın belirli bir noktasından "geri dönüş noktası" adı verilen bir yerden yapılan çağrılarla kullanılabilen bir özel durum atma mekanizması oluşturur. setjmp işlevi, özel bir yapı olan jmp_buf türünden bir nesne ile birlikte kullanılır. setjmp çağrısı, jmp_buf nesnesine geçerli program durumunu kaydeder ve ardından belirli bir değer döndürür. Bu işlev, longjmp işlevi çağrıldığında geri dönüş noktasına atlamak için kullanılır.

# csignal (C Library)

- Bu başlık dosyası, C dilindeki <signal.h> başlık dosyası ile benzer işlevleri yerine getirir. Programcılar, bu başlık dosyasını kullanarak sinyal işlemleri gerçekleştirebilirler.

Bu başlık dosyası, öncelikle sinyal işlemleri için kullanılan fonksiyon ve makrolar içerir. Bunlar arasında SIGINT, SIGABRT, SIGFPE, SIGILL, SIGSEGV, SIGTERM gibi sinyallerin yakalanması için kullanılan fonksiyonlar, sinyal işleyicilerin tanımlanması ve sinyal işleyicilerin kaldırılması için kullanılan fonksiyonlar ve sinyal maskesi işlemleri için kullanılan fonksiyonlar yer alır.

# cstdarg (C Library)

- C++'ta gösterilen değişken sayısına göre değişen işlevler oluşturmak için kullanılan değişken argüman listesi işlevleri sağlar. Bu başlık dosyası, işlevlerin esnekliğini arttırır ve programcılara çeşitli değişken argüman listesi işlevleri sağlar.

- Bu başlık dosyası, öncelikle va_list türü, va_start, va_arg, va_end ve va_copy gibi işlevlerin tanımlanmasıyla ilgilidir.

# cstddef  (C Library)

- Bu başlık dosyası, C++ dilinde temel veri türleri ve sabitlerle ilgili makroları tanımlayan <stddef.h> başlık dosyasının C++ standart uyumlu bir sürümüdür.

# cstdio (C Library)

- C dilinde standart girdi/çıktı işlemlerini gerçekleştirmek için kullanılır. C++'ta ise, C++'ın standart I/O kütüphanesi bu işlemleri gerçekleştirmek için kullanılır. Ancak hala C dilinde yazılmış uygulamaların C++'ta derlenmesi için kullanılabilir.

- başlık dosyası bir dizi fonksiyon ve makro tanımlarına sahiptir. Bu fonksiyonlar, klavyeden veya dosyadan girdi okuma, dosyaya veya ekrana yazma ve dosya konum ayarlamaları gibi işlemleri gerçekleştirmek için kullanılır.

# cstdlib (C Library)

-  Bu başlık dosyası, C dili standart kütüphanesi <stdlib.h> başlık dosyasının C++ diline uygun hale getirilmiş halidir. başlık dosyası, programların çalışma zamanında ihtiyaç duyabileceği, bellek yönetimi, sayısal dönüşümler, rastgele sayı üretimi, çevre değişkenleri, program sonlandırma ve diğer bazı işlemler için fonksiyonlar ve sabitler sağlar.

# cstring (C Library)

- C string işlevlerini tanımlayan C++ standart kütüphanesi başlık dosyasıdır. Bu başlık dosyası, C dilindeki string işlevleri için bir C++ arabirimi sağlar.

- Bu başlık dosyası, karakter dizilerinin işlenmesi için bir dizi fonksiyon içerir.

# ctime (C Library)

- Bu başlık dosyası, zaman ve tarih işlemleri için gerekli olan fonksiyonları ve yapıları içerir.

# cwchar (C Library)

- C standardı için genişletilmiş geniş karakter işleme işlevleri sağlayan C++ başlık dosyasıdır. Bu başlık dosyası, C dilindeki <wchar.h> başlık dosyasına karşılık gelir ve Unicode karakterleri destekleyen genişletilmiş C++ karakter işleme işlevleri sağlar.

# cwctype (C Library)

- C programlama dilinde bulunan <ctype.h> başlık dosyasına benzer bir işlevi yerine getiren C++ başlık dosyasıdır. Ancak başlık dosyası, karakterlerin genişletilmiş (multibyte) karşılıklarının yanı sıra geniş karakterler (wide characters) için de işlevler sağlar.

# deque (Default)[Containers]

- std::deque (double-ended queue) bir C++ standart kütüphanesi veri yapısıdır. "Double-ended" ifadesi, veri yapısının hem ön hem de arka tarafında eleman eklemeye ve çıkarmaya izin verir.

- std::deque bir sıra olarak düşünülebilir, ancak sadece ön veya arka tarafından eleman ekleme veya çıkarma yapmakla sınırlı kalmaz. std::deque aynı zamanda, bir vektörün yapabileceği gibi, arka arkaya bellek alanlarına elemanlar yerleştirmek için yeniden boyutlandırılabilir.








