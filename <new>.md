# new

- <new başlık dosyası C++ standart kütüphanesinde yer alır ve bellek yönetimi işlemleri için gerekli olan std::bad_alloc istisna sınıfını ve new ve delete operatörlerini içerir.

- new operatörü, bir bellek bloğu için istek gönderir ve bu bloğun oluşturulması için gerekli bellek miktarını sağlar. new operatörü tarafından oluşturulan nesnelerin bellekleri, delete operatörü kullanılarak serbest bırakılabilir. Bellek yönetimi işlemleri doğru şekilde yapılmazsa, bellek sızıntılarına veya hatalı bellek kullanımına neden olabilirler.

- new başlık dosyası, bellek tahsisi işlemi sırasında std::bad_alloc istisna sınıfını fırlatır. std::bad_alloc istisna sınıfı, bellek tahsis işlemi sırasında bellek tükenmesi durumunda fırlatılır ve bu durumda programın normal çalışması devam edemez.

<new başlık dosyasındaki diğer bellek yönetimi işlevleri şunlardır:

- **std::align**: C++11 ile tanıtılan bu işlev, verilen uygunluk gereksinimlerine sahip yeni bir bellek bloğu oluşturmak için kullanılır. İşlev, istenen uygunluk gereksinimlerini karşılayan ve belirtilen boyutta bir bellek bloğu için bir işaretçi döndürür. İşlev ayrıca, yeni bloğun başlangıç adresinin yanı sıra blok boyutunu da geri döndürür.

- **std::get_temporary_buffer:** Bu işlev, belirtilen boyutta geçici bir bellek bloğu için bellek tahsis eder. İşlev, blok boyutu ve blok sayısı gibi parametreler alır ve uygun bir bellek bloğu için bir işaretçi ve blok sayısı ile birlikte bir std::pair nesnesi döndürür. Geçici bellek bloğu, std::return_temporary_buffer işlevi kullanılarak serbest bırakılabilir.

- **std::return_temporary_buffer:** Bu işlev, std::get_temporary_buffer işlevi tarafından tahsis edilen geçici bellek bloklarını serbest bırakır.

- Bu işlevler, özellikle bellek yönetimi için ihtiyaç duyulan daha ayrıntılı ve özelleştirilmiş bir yaklaşım gerektiğinde kullanılabilir. Ancak, tipik C++ programlaması sırasında genellikle ihtiyaç duyulmaz ve temel new ve delete operatörleri kullanılabilir.

- Aşağıdaki örnek, <new başlık dosyasının new ve delete operatörlerinin kullanımını göstermektedir:
  
```CPP
#include <iostream>
#include <new>

int main() {
    int* p;

    try {
        p = new int[10];
        for (int i = 0; i < 10; i++) {
            p[i] = i;
        }
    } catch (std::bad_alloc& e) {
        std::cerr << "Allocation failed: " << e.what() << std::endl;
        return 1;
    }

    for (int i = 0; i < 10; i++) {
        std::cout << p[i] << " ";
    }
    std::cout << std::endl;

    delete[] p;

    return 0;
}

```

- Bu örnekte, new operatörü kullanılarak 10 tane int tipinde bir dizi için bellek tahsis edilir. Bellek tahsis işlemi try-catch bloğu içinde gerçekleştirilir ve std::bad_alloc istisna sınıfı fırlatılır. Bellek tahsis işlemi başarılı olursa, diziye elemanlar eklenir ve delete operatörü kullanılarak bellek serbest bırakılır.

- <new başlık dosyası, bellek tahsis işlemleri sırasında daha fazla kontrol yapmak ve bellek yönetimi ile ilgili özelleştirmeler yapmak için de kullanılabilir.

- new ve delete operatörlerini kullanmak için <new başlık dosyasını dahil etmek zorunlu değildir, ancak diğer bellek yönetimi işlevlerini kullanmak istediğinizde <new> başlık dosyasını dahil etmeniz gerekir. <new başlık dosyası, dinamik bellek yönetimi işlemleri için birçok farklı fonksiyon, sınıf ve sabit tanımlar içerir. Bunlar arasında std::bad_alloc sınıfı, std::nothrow nesnesi, std::align() işlevi ve std::get_temporary_buffer() ile std::return_temporary_buffer() işlevleri gibi bellek yönetimi işlevleri bulunur. Bu işlevler, bellek yönetimi işlemlerinin daha ayrıntılı ve özelleştirilmiş bir şekilde yapılmasını sağlar ve C++ programlama dilinde dinamik bellek yönetimi için önemli bir rol oynar.

- <new başlık dosyası, ayrıca, operator new ve operator delete fonksiyonları için deklarasyonları içerir. Bu fonksiyonlar, C++ programlama dilinde dinamik bellek yönetimi için kullanılır. operator new fonksiyonu, programın çalışma zamanında bellek alanı ayırmak için kullanılırken, operator delete fonksiyonu, önceden ayırdığımız bellek alanını geri vermeye yöneliktir. Bu operatörlerin ayrıntılı tanımları için <new> başlık dosyasını dahil etmek gerekmez, ancak new veya delete operatörlerinin özelleştirilmiş sürümlerini oluşturmak istediğimizde, <new başlık dosyasını dahil etmek gerekebilir



  

  

  

  

  

 

  






























