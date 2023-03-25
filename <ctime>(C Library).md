- <ctime> başlık dosyası, C standard library'sinde yer alan bir başlık dosyasıdır. Bu başlık dosyası, zaman ve tarih işlemleri için gerekli olan fonksiyonları ve yapıları içerir.

- Başlık dosyası, aşağıdaki yapıları içerir:

- **time_t:** Unix epoch'tan (1 Ocak 1970) itibaren geçen saniye sayısını tutan tamsayı veri türüdür.
- **struct tm:** zamanı belirlemek için kullanılan yapıdır. Bu yapı, yıl, ay, gün, saat, dakika, saniye ve haftanın günü gibi unsurları içerir.
Başlık dosyası, aşağıdaki fonksiyonları içerir:

- **time():** Şu anki tarih ve saati, Unix epoch'tan itibaren geçen saniye cinsinden döndürür.
- **difftime():** İki zaman arasındaki farkı saniye olarak döndürür.
- **mktime():** struct tm tipindeki bir zamanı, Unix epoch'tan itibaren geçen saniye sayısına dönüştürür.
- **localtime():** Unix epoch'tan itibaren geçen saniye sayısını, yerel saatteki zaman bilgisine dönüştürür.
- **gmtime():** Unix epoch'tan itibaren geçen saniye sayısını, UTC (Koordinatlı Evrensel Saat) zaman bilgisine dönüştürür.
- **strftime():** struct tm tipindeki bir zamanı, belirtilen biçimlendirme dizesine göre biçimlendirir ve karakter dizisi olarak döndürür.
Aşağıdaki örnek, zaman işlemleri için <ctime> başlık dosyasının kullanımını göstermektedir:

```CPP
#include <iostream>
#include <ctime>

int main() {
    // Şu anki zamanı al
    time_t now = time(nullptr);

    // time_t veri türünden struct tm veri türüne dönüştür
    tm* local_time = localtime(&now);

    // struct tm veri türünü karakter dizisine dönüştür
    char time_str[50];
    strftime(time_str, 50, "%c", local_time);

    // Sonuçları yazdır
    std::cout << "Şu anki zaman: " << time_str << std::endl;

    return 0;
}

```
> Bu örnekte, <ctime> başlık dosyasının time(), localtime() ve strftime() fonksiyonları kullanılarak şu anki zamanın yerel saatteki değeri, belirli bir biçimde karakter dizisine dönüştürülmüş ve yazdırılmıştır.







