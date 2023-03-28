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

# deque (Default) Containers

- std::deque (double-ended queue) bir C++ standart kütüphanesi veri yapısıdır. "Double-ended" ifadesi, veri yapısının hem ön hem de arka tarafında eleman eklemeye ve çıkarmaya izin verir.

- std::deque bir sıra olarak düşünülebilir, ancak sadece ön veya arka tarafından eleman ekleme veya çıkarma yapmakla sınırlı kalmaz. std::deque aynı zamanda, bir vektörün yapabileceği gibi, arka arkaya bellek alanlarına elemanlar yerleştirmek için yeniden boyutlandırılabilir.

# exception (Default)

- Bu sınıf, istisnai durumlar için bir temel sınıf olarak kullanılır ve programcıların hata mesajları oluşturması için bir arayüz sağlar.

- std::exception sınıfı, what adında bir üye işlevi sağlar. Bu işlev, bir const char* türündeki bir hata mesajı döndürür ve genellikle try-catch bloklarında kullanılır. what işlevi, hata nedenini açıklayan bir metin dizesi döndürür.

# execution (C++17)

- execution başlık dosyası, C++'da paralel algoritmaların tasarımı için bir dizi araç sağlar.

- Bu başlık dosyasındaki ana öğe, std::execution::par ve std::execution::seq adında iki politika sınıfıdır. Bu politika sınıfları, std::for_each, std::transform, std::reduce, std::sort gibi STL algoritmalarının paralel sürümlerinde kullanılabilir.

- std::execution::par politikası, STL algoritmasının paralel sürümünü yürütürken, paralelleştirme yoluyla performans artışı elde etmek için birden fazla iş parçacığı kullanılmasına izin verir. std::execution::seq politikası ise sıralı bir şekilde yürütülür.

# expected  (C++23)
-  başarılı bir sonuç veya bir hata durumunu temsil etmek için kullanılacak std::expected sınıfını tanımlar. Bu sınıf, bir işlemin sonucunu veya hatayı temsil etmek amacıyla kullanılabilir ve genellikle hatalı durumları işlemek için kullanılan özel durum mekanizmasının (exception) bir alternatifidir.

# filesystem (C++17)

- dosya ve dizin işlemleri için güçlü ve esnek bir arayüz sağlar. C++17 standardıyla birlikte tanıtılan bu kütüphane, dosyaları ve dizinleri oluşturma, kopyalama, taşıma, yeniden adlandırma, silme ve özelliklerini sorgulama gibi işlemleri gerçekleştirmenize olanak tanır.

# format (C++20)

- biçimlendirilmiş çıktılar oluşturmak için kullanılan fonksiyonlar ve sınıflar içerir. Bu başlık dosyası, printf() ve C stilinde biçimlendirilmiş çıktılar yerine tip güvenliği ve okunaklılığı arttırmak amacıyla C++ standart kütüphanesi tarafından sunulan modern bir alternatiftir.

# forward_list (C++11) Containers

- <forward_list> başlık dosyası, tek yönlü bağlı liste olarak adlandırılan bir veri yapısını sağlayan sınıf şablonu std::forward_list'i tanımlar.

- std::forward_list, std::list'in tek yönlü bir sürümüdür. Tek yönlü bağlı liste, her elemanın sadece bir sonraki elemanını bilen bir liste türüdür. Bu özellik, bir öğenin listeye eklendiğinde, sadece bir sonraki öğenin adresi ayarlanır ve önceki öğenin adresi saklanmaz. Bu nedenle, std::forward_list daha hafif ve daha az yer kaplayan bir liste türüdür ve belirli bir senaryoda tercih edilebilir.

# fstream (Default) 

- dosya işlemleri yapmak için kullanılır. std::fstream, hem girdi hem de çıktı işlemleri için kullanılabilir.

- std::fstream sınıfı, std::ifstream ve std::ofstream sınıflarının birleşiminden oluşur ve hem okuma hem de yazma işlemlerini aynı anda yapabilir. std::fstream, dosya işlemleri için kullanılan en temel sınıflardan biridir ve bir dosyanın içeriğini okumak veya yazmak için sıklıkla kullanılır.

# functional (Default)

- Bu başlık dosyası, C++ dilindeki fonksiyonel programlama araçlarını sağlayan bir dizi sınıf ve fonksiyonlar içerir.

# future (C++11)

- C++ programlarında çoklu iş parçacıklı programlamayı kolaylaştırmak için kullanılır. Bu başlık dosyası, std::async ve std::future gibi sınıfları tanımlar.

# initializer_list (C++11) 
- C++'ta özellikle inisyalizasyon listeleri kullanılırken yararlıdır. Bu başlık dosyası, std::initializer_list sınıfını ve bu sınıfın özelliklerini içerir.

- std::initializer_list sınıfı, C++11'de tanıtılmış bir özel sınıftır ve bir liste gibi kullanılabilen bir sabit boyutlu bir dizidir. Bu sınıf, kullanıcının programda sabit bir liste oluşturmasına olanak tanır ve bu liste, programın farklı yerlerinde kullanılabilir.

- std::initializer_list sınıfı, bir nesne dizisi oluşturarak kullanıcılara bir sabit liste sağlar. Bu nesne dizisi, programcının listeyi döndürmesi, kopyalaması veya başka amaçlar için kullanmasına olanak tanır. Bu sınıfın kullanımı, inisyalizasyon listeleri ile uyumludur ve birçok farklı C++ türü için kullanılabilir.

- std::initializer_list sınıfı, bir liste olarak kullanılabildiği gibi, aynı zamanda diğer C++ sınıflarının veya fonksiyonların inisyalizasyon parametreleri olarak da kullanılabilir.

- Özetle, <initializer_list> başlık dosyası, programcılara C++11 ile birlikte tanıtılan std::initializer_list sınıfını ve bu sınıfın sağladığı özellikleri sunar.

# iomanip (Default)
- Bu başlık dosyası, girdi/çıktı işlemlerinde kullanılan manipülatörler (manipulators) olarak adlandırılan özel işlevleri içerir.

- Manipülatörler, girdi/çıktı işlemlerinin formatını ayarlamak için kullanılırlar. Örneğin, sayıları belirli bir genişlikte ve belirli bir hassasiyetle yazdırmak, ondalık ayraçların ve diğer ayraçların yerini belirlemek gibi işlemler manipülatörler aracılığıyla gerçekleştirilir.

# list (Default) Containers

- çift yönlü bağlı liste yapısını tanımlayan std::list sınıfını içerir.

- std::list sınıfı, elemanları çift yönlü bir bağlı liste şeklinde tutan bir veri yapısıdır. Listeler, elemanların ekleme ve çıkarma işlemlerinde daha hızlıdır ancak elemanlara rastgele erişimde (örneğin, dizilerdeki gibi) daha yavaştırlar.

- std::list sınıfı, elemanları push_front, push_back, pop_front ve pop_back gibi işlevlerle ekleyip ve çıkarabilen bir arayüz sağlar. Elemanlara doğrudan erişim mümkün değildir, ancak begin() ve end() işlevleri aracılığıyla liste üzerinde döngüler oluşturulabilir.

# locale (Default)

- std::locale, C++ standart kütüphanesinde yer alan bir sınıftır ve yerel ayarlar (locale settings) ile ilgili bilgileri içerir. Yerel ayarlar, çeşitli özellikleri tanımlayan ve değişen bir sıralama, karakter çevirimi, tarih ve saat biçimi, para birimi, sayı biçimi gibi birçok kültürel özelliklerdir. std::locale sınıfı, bu yerel ayar bilgilerini tutar ve C++ girdi/çıktı işlemlerinde bu ayarları kullanarak karakterlerin kodlamasını, sıralamasını, tarih/saat biçimini vb. belirleyebilir.

# map (Default)[Containers]

- std::map, C++ standart kütüphanesinde bulunan bir ilişkisel veri yapısıdır. std::map bir anahtar-değer çiftleri koleksiyonudur ve anahtarlar benzersizdir. Bu özellik, std::map'i bir anahtarın değerini hızlı bir şekilde aramak için kullanışlı hale getirir.

- std::map veri yapısı, kırmızı-siyah ağaçlar kullanılarak gerçekleştirilir. Bu nedenle, std::map'in performansı, en kötü durumda bile logaritmiktir ve arama, ekleme ve silme işlemleri için O(log n) zaman karmaşıklığına sahiptir. Ancak, bu performans avantajı, std::map'in bir anahtar-değer çiftleri koleksiyonu olarak kullanılmasının yanı sıra, bir sıralı liste gibi de kullanılabileceği anlamına gelir.

- std::map sınıfı, std::pair sınıfından oluşan bir anahtar-değer çiftleri koleksiyonu tutar. Anahtar-değer çiftleri, std::pair sınıfından türetilen std::map::value_type sınıfı ile temsil edilir. std::map sınıfı, bir anahtarın değerine hızlı bir şekilde erişmek için std::map::find işlevini sağlar. std::map ayrıca, std::map::insert işlevi kullanılarak yeni anahtar-değer çiftleri eklemek için de kullanılabilir.

# memory (Default)

- C++ standart kütüphanesinde yer alan bir bellek yönetimi kütüphanesidir. Bu kütüphane, bellek yönetimine ilişkin bazı standart işlevler, akıllı işaretçiler ve bellek arayüzleri sağlar.

- Bellek yönetimi, C++ programlamasında oldukça önemlidir ve doğru bir şekilde yönetilmediğinde hafıza sızıntıları veya bellek hataları gibi sorunlara neden olabilir. std::memory kütüphanesi, C++ programcılarının bu tür sorunları önlemelerine ve bellek yönetimini daha kolay hale getirmelerine yardımcı olur.

# memory_resource (C++17)

- <memory_resource> başlık dosyası, özelleştirilebilir bellek yönetimi için araçlar sağlar. Özellikle, C++17'te tanıtılan bu başlık dosyası, bellek tahsisi işlemlerinde performans ve özelleştirme açısından daha iyi esneklik sunar.

- <memory_resource> başlık dosyası, aşağıdaki sınıfları içerir:

- std::pmr::memory_resource: Bu soyut sınıf, bellek tahsis ve serbest bırakma işlemlerini gerçekleştirir. std::pmr::new_delete_resource gibi öntanımlı işlevler sağlar, ancak bu işlevler, özelleştirilmiş bellek yönetimi için yerine getirilebilir.

# mutex (C++11)

- mutex başlık dosyası, çoklu iş parçacığı programlamada eşzamanlılığı sağlamak için kullanılan kilitleme mekanizmalarını sağlar. Mutex, bir iş parçacığının başka bir iş parçacığı tarafından kullanılmaması gereken bir kaynağa eriştiği yerlerde kullanılır.


# new (Default)

- <new başlık dosyası C++ standart kütüphanesinde yer alır ve bellek yönetimi işlemleri için gerekli olan std::bad_alloc istisna sınıfını ve new ve delete operatörlerini içerir.

- new operatörü, bir bellek bloğu için istek gönderir ve bu bloğun oluşturulması için gerekli bellek miktarını sağlar. new operatörü tarafından oluşturulan nesnelerin bellekleri, delete operatörü kullanılarak serbest bırakılabilir. Bellek yönetimi işlemleri doğru şekilde yapılmazsa, bellek sızıntılarına veya hatalı bellek kullanımına neden olabilirler.

- new başlık dosyası, bellek tahsisi işlemi sırasında std::bad_alloc istisna sınıfını fırlatır. std::bad_alloc istisna sınıfı, bellek tahsis işlemi sırasında bellek tükenmesi durumunda fırlatılır ve bu durumda programın normal çalışması devam edemez.

# numbers (C++20)

- C++20 ile birlikte, başlık dosyası eklendi ve matematiksel sabitler ve işlevler için standart bir kütüphane sağlandı. Bu başlık dosyası, özellikle bilimsel hesaplama, fizik, matematik ve diğer hesaplama yoğun uygulamaları için yararlıdır.

# numeric (Default)
- sayısal algoritmalar için bir dizi işlev sağlar. Bu başlık dosyası, çeşitli aritmetik işlemler yapmak ve sayısal verileri işlemek için işlevler içerir. 

# optional (C++17)

- Bu başlık dosyası, bir nesnenin belirli bir durumda olup olmadığını belirlemek için kullanılan bir şablon sınıfı olan "optional" sınıfını tanımlar.

# queue (Default)[Containers]

- queue başlık dosyası, C++ standart kütüphanesinde bulunan bir sıra veri yapısı olan queue sınıfını tanımlar. queue sınıfı, bir koleksiyonun başına eleman eklemek ve sonundan eleman çıkarmak için kullanılır.

# random (C++11)

- rasgele sayı oluşturma işlemleri için kullanılır. Bu başlık dosyası, rastgele sayı üreteçleri, dağılımlar ve diğer ilgili araçlar gibi birçok sınıfı içerir.

# ranges (C++20)

- ranges başlık dosyası, aralıklar üzerinde çalışmak için kullanılan bir dizi işlev ve sınıfı içerir. Bu işlevler, mevcut algorithm başlık dosyasında yer alan birçok işlevin yerini alarak, verimli aralık işlemleri yapmayı kolaylaştırır.

# ratio (C++11)

- başlık dosyası, rasyonel sayıların sabit ifadelerini sağlar. C++11'de tanıtılan bir başlık dosyasıdır. Bir rasyonel sayı, iki tamsayının oranıdır. Örneğin, 1/2, 2/3 gibi.
- Bu başlık dosyası ile, rasyonel sayılarla çalışırken işlemler yapmak daha kolay hale gelir. İki rasyonel sayıyı çarpmak, bölmek, toplamak veya çıkarmak için kullanabilirsiniz.

# regex (C++11)

- regex başlık dosyası, C++11'de tanıtılan bir başlık dosyasıdır ve düzenli ifadeler (regular expressions) için destek sağlar. regex sınıfı, düzenli ifade tabanlı arama için kullanılan ana sınıftır. Bu sınıf, bir düzenli ifadeyi tanımlamanıza, metin dizilerinde arama yapmanıza ve eşleşmeleri bulmanıza olanak tanır.

# scoped_allocator

- scoped_allocator başlık dosyası, C++11 standartlarından itibaren mevcut olan öncelikli tahsis ediciler (allocator) kullanımını kolaylaştıran bir araçtır. Bu başlık dosyası, C++11 öncesi sürümlerde yerleşik olmayan bir özellik olan scoped_allocator_adaptor sınıfını tanıtır.

# semaphore (C++20) 

- başlık dosyası, senkronizasyonu ve iş parçacığı arasındaki işbirliğini kolaylaştıran semafor nesnelerini tanımlar. Bu başlık dosyası, semaforlar aracılığıyla senkronizasyonu sağlamak için bir dizi fonksiyon ve sınıf sağlar.

- Bu başlık dosyasındaki en önemli sınıf, semafor sınıfıdır. Bu sınıf, bir iş parçacığının, bir başka iş parçacığının belirli bir noktada durmasını sağlamasına ve daha sonra devam etmesine izin veren bir senkronizasyon aracıdır. Semaforlar, sıkı bir senkronizasyon ihtiyacı olan çoklu iş parçacığı programlamasında yaygın olarak kullanılır.

- Bunun yanı sıra, bu başlık dosyası iki adet standart fonksiyon olan binary_semaphore ve counting_semaphore fonksiyonlarını da içerir. binary_semaphore fonksiyonu, yalnızca iki olası durumla ilişkili olan semaforlar için tasarlanmıştır. counting_semaphore fonksiyonu ise, belirli bir sayıda olası durumla ilişkili olan semaforlar için tasarlanmıştır.

# set (Default)[Containers] 
- std::set sınıfı, C++ standart kütüphanesinde bulunan bir veri yapısıdır ve elemanları sıralı bir şekilde tutar. Bu sınıf, elemanların eşsiz (unique) olduğu bir koleksiyon (collection) tanımlamak için kullanılır, yani aynı eleman birden fazla kez eklenemez.

- std::set sınıfı, sıralama kriteri olarak varsayılan olarak "küçükten büyüğe" sıralamayı kullanır, ancak kullanıcı tanımlı sıralama işlevleri de kullanılabilir. Bu, elemanların türüne bağlı olarak, farklı sıralama kriterleri kullanarak elemanların sıralanmasını sağlamak için oldukça yararlıdır.

- std::set sınıfı, elemanların ekleme, çıkarma ve arama işlemlerini hızlı bir şekilde gerçekleştirir. Bu sınıfın bir diğer avantajı da, elemanları eklemeden önce sıralı bir şekilde tutmasıdır, bu sayede elemanlar her zaman sıralı bir şekilde tutulur ve sıralama işlemi yapılmak zorunda kalmaz.

- std::set sınıfı, standart kütüphanenin diğer bileşenleriyle birlikte kullanılarak birçok algoritma ve veri yapısı problemini çözmek için kullanılabilir. Örneğin, bir sözlük yapmak, elemanları sıralı bir şekilde tutmak, öğrencilerin notlarını saklamak gibi birçok kullanım alanı vardır.

- Ayrıca, std::set sınıfı, elemanların var olup olmadığını kontrol etmek, elemanları sıralı bir şekilde göstermek veya aralıklar halinde elemanları göstermek gibi birçok işlevsellik sağlar.

# shared_mutex (C++14)

-  C++11'de tanıtılan std::shared_mutex sınıfını içerir. Bu sınıf, aynı anda birden fazla okuma işlemine izin veren bir kilit mekanizması sağlar, ancak yazma işlemlerini yalnızca tek bir thread'e izin verir.

- Bu sınıf, std::mutex sınıfının bir uzantısıdır ve birçok iş parçacığı uygulamasında kullanışlıdır. Özellikle, paylaşılan bir kaynağa birden fazla okuyucu thread'in aynı anda erişebilmesi gereken senaryolarda kullanılır.

# source_location (C++20)
- C++ kodunun kaynak konumunu temsil etmek için kullanılır. Bu başlık dosyasında yer alan sınıflar ve fonksiyonlar, kodun hangi dosya, satır ve sütunlarda yazıldığını, hangi işlevin hangi satırında çağrıldığını veya hangi kaynak dosyasından dahil edildiğini tanımlamak için kullanılır.

# span (C++20)

- bellekteki bir veri bloğuna sıfır veya daha fazla öğe için "bir aralık" (span) tanımlar ve bu aralığın işlem yapılmasına izin verir. Bu aralık, std::array, std::vector, C tarzı diziler, önbelleğe alınmış bellek (pinned memory), dosya belleği veya diğer bellek bölgelerindeki veri blokları gibi diğer bellek türleriyle çalışmak için kullanılabilir.

# stack (Default)[Containers]

- <stack başlık dosyası, std::stack sınıfını tanımlar. Bu sınıf, önceden tanımlanmış bir veri yapısı olan yığıtın (stack) bir sarmalayıcısıdır. Yığıt veri yapısı, verilerin yalnızca en üstünden (top) eklenmesine ve çıkarılmasına izin verir.

- std::stack sınıfı, yığıt veri yapısını uygulamak için bir dizi işlev ve özellik sağlar. push() işlevi, yığıtın üstüne yeni bir öğe eklerken, pop() işlevi en üstteki öğeyi çıkarır. top() işlevi, en üstteki öğeye başvurmanızı sağlar. empty() işlevi, yığının boş olup olmadığını kontrol ederken size() işlevi, yığında kaç öğe olduğunu belirler.

# stdexcept (Default)

- C++ standart kütüphanesinde yer alan hata sınıflarını ve bunlara ilişkin özelleştirilmiş istisna türlerini tanımlar. Bu başlık dosyası, temel hata sınıflarının yanı sıra özelleştirilmiş hata sınıfları tanımlamak için de kullanılır.

# stop_token (C++20)

- C++'ta asenkron işlemleri kontrol etmek için kullanılır. <stop_token> başlık dosyası, , ve <condition_variable> gibi diğer C++ başlık dosyalarıyla birlikte kullanılabilir.

- <stop_token> başlık dosyası, stop_source ve stop_token sınıflarını içerir. stop_source, bir senaryonun tamamlanması için kullanılan bir araçtır ve stop_token, bir senaryonun çalıştırılmasını durdurmak için kullanılır.

- stop_source sınıfı, bir senaryonun durdurulmasını isteyen kod bloklarında oluşturulur. stop_token sınıfı, durdurma sinyalinin kontrolünü sağlayan bir arayüz sağlar. stop_token sınıfı, başka bir sınıfın bir parçası olarak veya bir iş parçacığı tarafından kullanılabilir.

# streambuf (Default)

- streambuf başlık dosyası, C++ standart kütüphanesindeki girdi/çıktı işlemleri sınıflarının temelini oluşturan veri deposu sınıflarını tanımlar. Bu sınıfların amacı, girdi/çıktı işlemlerinin yapılacağı verilerin bellekteki yerini yönetmektir.

- Bir streambuf nesnesi, C++ standart kütüphanesindeki girdi/çıktı işlemlerinde verilerin okunup/yazılacağı yerin yönetimini sağlayan temel sınıftır. Bu sınıf, örneğin std::fstream, std::stringstream veya std::cout gibi diğer sınıfların temelini oluşturur.

# string (Default)

- string başlık dosyası, std::string sınıfını ve onunla ilgili işlevleri tanımlayan standart C++ başlık dosyasıdır. Bu sınıf, C++ programlama dilinde metin verilerini depolamak, işlemek ve manipüle etmek için kullanılır.

# string_view (C++17)

- string_view başlık dosyası, std::string gibi bir karakter dizisi türünün bir parçasını gösteren, ancak kendi bellek yönetimine sahip olmayan bir sınıf olan std::string_view sınıfını tanımlar. std::string_view, karakter dizisi işleme işlevleri için kullanılabilir ve aynı zamanda diğer işlevler tarafından da kullanılabilir.

# strstream (Default)

- strstream başlık dosyasında tanımlanan sınıflar, C++98 standardı öncesinde kullanılan ve artık tavsiye edilmeyen iki sınıftır: istrstream ve ostrstream. Bu sınıflar, C++11'de sstream> başlık dosyasında tanımlanan istringstream, ostringstream ve stringstream sınıflarına benzer işlevlere sahiptir, ancak daha düşük bir performans sunarlar. Bu nedenle, bu sınıflar yerine sstream> başlık dosyasındaki sınıflar kullanılması önerilir.

başlık dosyası, C++'ta karakter dizileri üzerinde işlem yapmak için kullanılan bir başlık dosyasıdır. Bu başlık dosyası, C stilindeki karakter dizileri üzerinde işlem yapmak için stringstream ve istringstream sınıflarını sağlar.

# syncstream (C++20) 

- C++20'de tanıtılan başlık dosyası, çoklu iplikli uygulamalarda standart çıkış akışlarının güvenli bir şekilde kullanımını sağlamak için bir dizi senkronizasyonlu akış sınıfı içerir. 

# system_error (C++11)

- <system_error> başlık dosyası, hata kodları ve hata kategorileri gibi hata işleme araçları sağlayan C++ standart kütüphanesinin bir parçasıdır. Bu başlık dosyası, özellikle işletim sistemi işlevleri gibi sistem çağrıları sırasında oluşabilecek hataları işlemek için kullanılır.

# thread (C++11) 

- başlık dosyası, çoklu iş parçacıklı programlama için C++11 standartlarına uygun bir araç sağlar. Bu başlık dosyası, C++11 öncesi standartlarda yerleşik bir çoklu iş parçacıklı desteği yoktu, ancak C++11 ile birlikte gelen başlık dosyası sayesinde, birbirinden bağımsız birden fazla iş parçacığı oluşturulabilir ve her biri aynı anda çalıştırılabilir.

- Bu başlık dosyası, std::thread sınıfını içerir ve bu sınıf, bir iş parçacığı temsil eder. Bu sınıf sayesinde bir iş parçacığı oluşturulabilir ve bu iş parçacığına bir işlev (fonksiyon) atanabilir. Bu işlev, ayrı bir iş parçacığında çalıştırılır ve ana programın işlevselliği bundan etkilenmez.

# tuple (C++11)

- başlık dosyası, C++'da çoklu öğeleri tek bir veri yapısı altında tutmak için kullanılan bir sınıf olan tuple sınıfını tanımlar.

- Tuple, farklı türlerden öğeleri, belirtilen sıraya uygun bir şekilde depolayan bir sınıftır. Tuple sınıfı, bir struct veya sınıf nesnesine benzer şekilde öğeleri tutar, ancak tuple'lar farklı türlerdeki öğeleri tutabilir.

# type_index (C++11)

- başlık dosyası, type_info nesnelerinin isimlerinin, türlerinin ve diğer özelliklerinin depolanmasına, karşılaştırılmasına ve kullanımına yönelik araçlar sağlar.

- typeindex sınıfı, bir type_info nesnesinin özelliklerini depolar ve karşılaştırma işlemleri için kullanılabilir. Ayrıca, type_info nesnelerine erişmek için kullanılan type_index türü ile değiştirilebilir.

# type_traits (C++11)

- C++ programlamada tür bilgilerini sorgulamak için kullanılan bir başlık dosyası olan <type_traits>, SFINAE (Substitution Failure Is Not An Error) tekniği ile birlikte kullanılarak, tür şablonlarında koşullu durumlar oluşturmak için yararlı özellikler sağlar.

- Bu başlık dosyası altında tanımlanan type_traits sınıfı, türlerin özelliklerini sorgulamak için kullanılan bir dizi fonksiyon ve sınıf sağlar. Örneğin, std::is_pointer sınıfı bir türün bir işaretçi olup olmadığını belirlemek için kullanılabilir.

# typeinfo (Default)

- typeinfo başlık dosyası, C++ programlama dilinde tür bilgilerine erişim sağlayan std::type_info sınıfını tanımlar. Bu sınıfın temel amacı, çalışma zamanında nesnelerin türlerine erişim sağlamaktır.

- typeinfo başlık dosyası, C++'ta tür bilgisi hakkında bilgi toplama ve işleme işlevleri sağlar.

# unordered_map (C++11)[Containers] 

- unordered_map başlık dosyası, C++'ta hash tablolarının bir uygulamasını içerir. Bu başlık dosyasında, unordered_map sınıfı ve bununla ilgili diğer sınıflar ve yapılar tanımlanmıştır.

- unordered_map veri yapısı, key-value çiftlerini depolar. Key ve value değerleri istenen türde olabilir. Bu veri yapısı, ekleme, silme ve arama işlemleri için sabit bir süre gerektirir.

- unordered_map sınıfının kullanımı, std::map sınıfına benzerdir, ancak std::map'tan daha hızlıdır. unordered_map sınıfı, elemanları hash tablosuna depolar ve elemanlara erişmek için bir anahtarın hash değerini kullanır. Bu, elemanların belirli bir sıraya göre saklanmaması anlamına gelir.

# unordered_set (C++11)[Containers]

- <unordered_set> başlık dosyası, unordered_set adlı sınıfın tanımlanmasını içerir. unordered_set, öğeleri anahtar olarak tutan bir bağlı liste veri yapısına dayalı bir veri koleksiyonudur. Bu sınıf, öğeleri key-value çiftleri olarak saklamak yerine sadece anahtarları saklar. Bu nedenle, her bir anahtar yalnızca bir kez bulunur.

- unordered_set sınıfı, arama, ekleme ve silme işlemleri gibi temel işlemler için O(1) karmaşıklığına sahip bir yapı sunar. Bu sınıf aynı zamanda, set sınıfına benzer bir arayüz sunar ancak set'in sıralanmış olması yerine anahtarların hash değerlerine göre düzensiz olarak saklanması ile farklılık gösterir.

# utility (Default)
- utility başlık dosyası, C++ standart kütüphanesinin bir parçasıdır ve çeşitli faydalı araçlar sağlayan bazı şablon sınıflar, işlevler ve diğer öğeler içerir. İşlevler, özellikle de şablon işlevler, bir argümanın değerini işleyip başka bir değer döndürmek için kullanılabilir. Ayrıca, std::pair sınıfı, bir anahtar-değer çiftini temsil etmek için kullanılabilir. Bu, özellikle bir map yapısı gibi, anahtar-değer çiftlerinin bulunduğu bir koleksiyonda kullanışlıdır. utility başlık dosyası ayrıca bazı tür dönüştürme işlevleri içerir, örneğin std::move işlevi, bir nesnenin sahipliğini başka bir nesneye aktarmak için kullanılır.

# valarray (Default)

- valarray başlık dosyası, "value arrays" olarak adlandırılan matematiksel işlemler için bir dizi sınıf ve işlev sağlar. Bir valarray nesnesi, bellek yerine matematiksel işlemleri vurgulayan verileri depolamak için kullanılır. Bu nesne türleri özellikle büyük veriler üzerinde hızlı ve etkili işlemler gerçekleştirmek için tasarlanmıştır.


# variant (C++17) 

- başlık dosyası, C++17 standartlarına dahil edilmiştir. Bu başlık dosyası, C++ dilinde değişken sayıda veri türleri üzerinde çalışmayı mümkün kılan bir şablon sınıf olan std::variant sınıfını içerir.

- std::variant, özellikle belirli bir noktada farklı veri türlerinin kullanılması gereken, ancak her bir veri türü için ayrı bir değişken tanımlamak istemediğiniz durumlarda faydalıdır. Örneğin, bir XML dosyasındaki bir etiketdeki metni veya bir sayıyı temsil etmek için aynı değişkeni kullanabilirsiniz. 

# vector (Default)[Containers]

- vector başlık dosyası, C++ dilindeki dinamik dizi yapısını sağlayan std::vector sınıfını içerir. std::vector, bellek yönetimi ile ilgilenmek zorunda kalmadan, dizilerle benzer işlevsellik sunar.

- std::vector, C++11 sürümünden sonra standart kütüphanede tanımlanmıştır ve C++ programlama dilinin önemli bir parçasıdır. Genellikle, birçok elemanın depolanması ve dinamik olarak genişletilebilmesi gereken durumlarda kullanılır.

# version (C++20)

- C++20'de yer alan başlık dosyası, derlenen C++ standart sürümüne ilişkin bilgi sağlayan makro tanımları içerir. Bu başlık dosyası, derlenen C++ sürümüne bağlı olarak programda farklı davranışların sergilenmesini sağlayan koşullu derleme işlemlerinde kullanılır.















