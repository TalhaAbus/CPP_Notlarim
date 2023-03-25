- <cwctype> başlık dosyası, C programlama dilinde bulunan <ctype.h> başlık dosyasına benzer bir işlevi yerine getiren C++ başlık dosyasıdır. Ancak <cwctype> başlık dosyası, karakterlerin genişletilmiş (multibyte) karşılıklarının yanı sıra geniş karakterler (wide characters) için de işlevler sağlar.

- Bu başlık dosyasında, wide karakterlerin belirli özelliklerini ve özelliklerine göre sınıflandırılmasını sağlayan işlevler bulunur. Örneğin, iswalpha işlevi, bir geniş karakterin alfabede bulunan bir harf olup olmadığını belirlemek için kullanılır. Ayrıca, towupper ve towlower işlevleri, verilen bir geniş karakterin büyük/küçük harfe dönüştürülmesini sağlar.

- <cwctype> başlık dosyası, standart C başlık dosyası <wctype.h> ile benzerdir. Ancak, <cwctype> başlık dosyası C++'ın geniş karakter dizeleri (wide character strings) üzerinde çalışan işlevler içerirken, <wctype.h> başlık dosyası sadece tek geniş karakterler üzerinde çalışan işlevler içerir.

- Örnek kullanımı aşağıdaki gibi olabilir:

```CPP
#include <iostream>
#include <cwctype>

int main() {
    wchar_t ch = L'é';
    if (iswalpha(ch)) {
        std::wcout << L"'" << ch << L"' is an alphabetic character.\n";
    }
    else {
        std::wcout << L"'" << ch << L"' is not an alphabetic character.\n";
    }

    std::wcout << L"The uppercase of " << ch << L" is " << towupper(ch) << L".\n";

    return 0;
}

```

> Bu örnekte, wchar_t veri tipinde bir geniş karakter tanımlanmıştır. Ardından, iswalpha işlevi kullanılarak geniş karakterin bir alfabedeki bir harf olup olmadığı kontrol edilir. towupper işlevi ise, belirtilen geniş karakterin büyük harfe dönüştürülmüş halini döndürür.






- Tabii, aşağıdaki örnekte <cwctype> başlık dosyasında yer alan iswupper ve iswlower fonksiyonlarını kullanarak girilen bir metnin büyük harf ve küçük harf sayısını hesaplayabiliriz:


```CPP
#include <iostream>
#include <cwctype>

int main() {
    std::wstring text = L"Hello World!";
    int upper_count = 0, lower_count = 0;

    for (wchar_t c : text) {
        if (std::iswupper(c)) {
            upper_count++;
        } else if (std::iswlower(c)) {
            lower_count++;
        }
    }

    std::wcout << L"Text: " << text << std::endl;
    std::wcout << L"Uppercase count: " << upper_count << std::endl;
    std::wcout << L"Lowercase count: " << lower_count << std::endl;

    return 0;
}

```
> Bu örnekte, iswupper ve iswlower fonksiyonları wstring tipindeki text değişkeni içerisindeki her karakteri tek tek kontrol ederler ve büyük harf mi, küçük harf mi olduklarını tespit ederler. Daha sonra bu sayıları ayrı ayrı hesaplayarak ekrana yazdırırız.
