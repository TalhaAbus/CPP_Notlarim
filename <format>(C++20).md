- C++20 standardıyla birlikte tanıtılan <format> başlık dosyası, biçimlendirilmiş çıktılar oluşturmak için kullanılan fonksiyonlar ve sınıflar içerir. Bu başlık dosyası, printf() ve C stilinde biçimlendirilmiş çıktılar yerine tip güvenliği ve okunaklılığı arttırmak amacıyla C++ standart kütüphanesi tarafından sunulan modern bir alternatiftir.

- Bu başlık dosyasında bulunan en önemli öğeler şunlardır:

- **format() fonksiyonu:** Biçimlendirilmiş bir çıktı oluşturmak için kullanılır. İlk argüman olarak bir format dizesi alır ve bunun yerine getirilecek olan değerleri sırasıyla diğer argümanlar olarak alır.
- **format_to() fonksiyonu:** Biçimlendirilmiş bir çıktıyı bir çıktı arabelleğine yazmak için kullanılır.
- **format_to_n() fonksiyonu:** Biçimlendirilmiş bir çıktıyı belirli bir uzunlukta bir çıktı arabelleğine yazmak için kullanılır.
- **format_error sınıfı:** Biçimlendirme hatası oluştuğunda kullanılan özel bir hata sınıfıdır.
- Aşağıda, <format> başlık dosyası kullanarak bir örnek verilmiştir:

```CPP
#include <iostream>
#include <format>

int main() {
    std::string name = "John";
    int age = 30;
    std::cout << std::format("My name is {} and I am {} years old.", name, age) << std::endl;
    return 0;
}

```
- Bu kod, "My name is John and I am 30 years old." şeklinde bir çıktı üretir.

- Başka bir örnek:

```CPP
#include <iostream>
#include <format>
#include <vector>

int main() {
    std::vector<int> numbers = {1, 2, 3, 4, 5};
    std::cout << std::format("Numbers: [{0}, {1}, {2}, {3}, {4}]", numbers[0], numbers[1], numbers[2], numbers[3], numbers[4]) << std::endl;
    return 0;
}

```

- Bu kod, "Numbers: [1, 2, 3, 4, 5]" şeklinde bir çıktı üretir.

- C++20'de eklenen <format> başlık dosyası, formatlama işlemleri yapmak için kullanılır. Bu başlık dosyası, verilen bir formatlama dizesini kullanarak verileri biçimlendirmek için kullanılabilen sınıflar ve işlevler sağlar. Bu, özellikle çıktı yazdırma işlemlerinde faydalıdır.

- <format> başlık dosyası, iki ana sınıf içerir: std::format_arg_store ve std::basic_format. std::format_arg_store, formatlama argümanlarını saklamak için kullanılır. Bu sınıfın kullanımı, argümanları saklamak ve std::basic_format sınıfı tarafından kullanılmak üzere biçimlendirme dizesine göre ayarlamak için kullanılır.

- std::basic_format sınıfı ise, biçimlendirme dizesini temsil eder. Bu sınıfın format işlevi, biçimlendirme dizesini ve formatlama argümanlarını alır ve sonuç olarak biçimlendirilmiş dizeyi döndürür. Bu sınıfın kullanımı, biçimlendirme dizesini belirlemek, biçimlendirme argümanlarını tanımlamak ve sonucu elde etmek için kullanılır.

- Aşağıda bir örnek verilmiştir:

```CPP
#include <iostream>
#include <format>

int main() {
    std::string name = "Alice";
    int age = 30;
    double height = 1.75;

    std::string output = std::format("My name is {0}, I am {1} years old and {2:.2f} meters tall.", name, age, height);

    std::cout << output << std::endl;
}

```

- Bu örnekte, std::format işlevi kullanılarak bir biçimlendirme dizesi oluşturulmuştur. Biçimlendirme dizesinde, sırasıyla {0}, {1} ve {2:.2f} yer tutucuları kullanılmıştır. Bu yer tutucular, std::format işlevinin ikinci parametresinde tanımlanan name, age ve height değişkenlerinin değerleriyle değiştirilir. Sonuç olarak, output değişkeni, biçimlendirilmiş bir dizeyi içerir. Bu dize, "My name is Alice, I am 30 years old and 1.75 meters tall." şeklinde olacaktır.

- Bu örnekte, std::format işlevi kullanılarak basit bir biçimlendirme işlemi gerçekleştirilmiştir. Ancak, std::format işlevi, daha karmaşık biçimlendirme işlemleri için de kullanılabilir. Örneğin, tarih, saat veya para birimi gibi özel veri türleri için biçimlendirme seçenekleri de mevcuttur.

# Ben neden format'ı kullanayım? Başka türlü çıkış veremez miyim?

- Evet, elbette format yerine başka yöntemler de kullanabilirsiniz. Örneğin C'nin printf fonksiyonu ile de çıkış verebilirsiniz. Ancak printf fonksiyonu birçok farklı biçimlendirme belirteci içerir ve bunların doğru kullanımı oldukça dikkat gerektirir. Ayrıca biçimlendirme belirtecini, çıktıda görülecek veri türüne göre belirlemek gerekir. Bu durumda, özellikle karmaşık formatlama işlemleri için printf kullanmak hata yapma olasılığını artırabilir.

- <format> başlık dosyası, biçimlendirme işlemlerini daha kolay ve okunaklı hale getirmek için birçok kolaylık sağlar. Bu şekilde, biçimlendirme işlemlerini yapmak için daha az kod yazmak gerekir ve kodun okunması ve bakımı daha kolay hale gelir.

- Ayrıca, <format> başlık dosyası, biçimlendirme işlemlerini yaparken veri türleriyle ilgili hataların önlenmesine de yardımcı olur. Örneğin, biçimlendirme belirteci bir int türünde bir değişken için kullanılıyorsa, ancak o değişken yerine yanlışlıkla bir float türünden bir değişken kullanılmışsa, hata almadan beklenmedik sonuçlar elde edilebilir. <format> başlık dosyası, bu tür hataları önlemek için tür uyumunu kontrol eder ve hataları derleme zamanında yakalar.

- Sonuç olarak, <format> başlık dosyası, biçimlendirme işlemlerini daha kolay, okunaklı ve güvenli hale getirir.















