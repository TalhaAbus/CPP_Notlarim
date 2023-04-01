- <cerrno> başlık dosyası, C ve C++ programlama dillerinde hata kodlarını işlemek için kullanılan bir başlık dosyasıdır. Bu başlık dosyası, hata kodlarının sayısal değerleriyle ilişkili sabitleri tanımlar ve bu kodların tanımlanmasına, atılmasına ve işlenmesine yardımcı olur.

- Başlık dosyası, programın hata kodlarını elde etmesi, bunları okuması ve hata kodlarına uygun şekilde işlemesi için kullanılan birkaç farklı fonksiyonu içerir. Bazı örnekler şunlardır:

- **errno:** errno, son oluşan hata kodunun sayısal değerini tutan bir tamsayı değişkenidir. Hata oluştuğunda bu değer, ilgili hata koduyla güncellenir ve program tarafından okunabilir.
- **perror():** perror(), bir hata kodu için ayrıntılı bir açıklama yazdırır.
- **strerror():** strerror(), bir hata kodu için açıklama dizesini döndürür.
- Aşağıdaki örnek, dosya işlemleri yaparken <cerrno> başlık dosyasındaki errno değişkenini kullanarak hata kodlarını kontrol eder:

```CPP
#include <cstdio>
#include <cerrno>

int main() {
    FILE *fp = fopen("file.txt", "r");
    if (fp == NULL) {
        fprintf(stderr, "Failed to open file: %s\n", strerror(errno));
        return errno;
    }
    // File operations here
    fclose(fp);
    return 0;
}

```
> Bu örnekte, fopen() işlevi başarısız olursa, program perror() veya strerror() işlevlerini kullanarak ayrıntılı bir hata mesajı yazdırır. Ayrıca, program, errno değişkeninde saklanan hata kodunu döndürür.

- Aşağıda, fopen fonksiyonunun hata durumunda nasıl çalıştığını gösteren bir örnek var. Hata durumunda errno değeri değişecektir ve bu duruma göre gerekli işlemler yapılacaktır:

```CPP
#include <cstdio>
#include <cerrno>

int main() {
    FILE *fp = fopen("nonexistent_file.txt", "r");
    if (fp == nullptr) {
        printf("Failed to open file with error: %d\n", errno);
        switch (errno) {
            case ENOENT:
                printf("The file does not exist.\n");
                break;
            case EACCES:
                printf("Access to the file is not permitted.\n");
                break;
            default:
                printf("Unknown error occurred.\n");
                break;
        }
    } else {
        printf("File opened successfully.\n");
        fclose(fp);
    }

    return 0;
}

```

> Bu örnekte, fopen fonksiyonu nonexistent_file.txt dosyasını açamazsa, nullptr değeri döndürür ve errno değeri set edilir. Ardından, errno değeri kontrol edilir ve uygun mesaj yazdırılır. Dosya başarılı bir şekilde açılırsa, fclose fonksiyonu kullanılarak dosya kapatılır.

- Aşağıdaki örnek C++'ta cerrno başlık dosyasının kullanımını gösterir:

```CPP
#include <iostream>
#include <cstdio>
#include <cstring>
#include <cerrno>
 
int main()
{
    FILE* f = fopen("non_existent_file", "r");
    if (!f)
    {
        std::cout << "fopen failed, errno = " << errno << std::endl;
        std::cout << "Error description: " << strerror(errno) << std::endl;
    }
 
    return 0;
}
 
```
> Bu örnekte fopen() fonksiyonu çağrılırken verilen dosya adı mevcut olmadığı için dosya açma işlemi başarısız olacaktır. İşlem başarısız olduğu için fopen() fonksiyonu NULL değeri döndürecektir. !f ifadesi dosya açma işleminin başarısız olup olmadığını kontrol eder. Dosya açma işlemi başarısız olursa errno değişkeni belirli bir hata kodu ile ayarlanacaktır. Bu hata kodu cerrno başlık dosyasında tanımlı olan makrolar kullanılarak alınabilir. strerror() fonksiyonu, hata kodunu kullanarak bir hata açıklaması döndürür.

- Yukarıdaki örnekte strerror() fonksiyonu kullanılarak errno hata kodunun bir açıklaması gösterilmiştir.



