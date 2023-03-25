- <cstdarg>, C++'ta gösterilen değişken sayısına göre değişen işlevler oluşturmak için kullanılan değişken argüman listesi işlevleri sağlar. Bu başlık dosyası, işlevlerin esnekliğini arttırır ve programcılara çeşitli değişken argüman listesi işlevleri sağlar.

- Bu başlık dosyası, öncelikle va_list türü, va_start, va_arg, va_end ve va_copy gibi işlevlerin tanımlanmasıyla ilgilidir.

- va_list türü, değişken argüman listesi işlevlerinde kullanılan bir türdür. va_start işlevi, değişken argüman listesi işlevleriyle ilgili herhangi bir işlem yapmadan önce va_list türünde bir nesneyi başlatır. va_arg işlevi, değişken argüman listesi işlevlerinde, sıradaki argümanı geri döndürür ve argüman listesinin bir sonraki argümanına geçer. va_end işlevi, va_start işlevi tarafından başlatılan değişken argüman listesi işlevinin işlemesini sonlandırır. va_copy işlevi, bir va_list nesnesinin başka bir va_list nesnesine kopyalanmasını sağlar.

- Aşağıda, bir va_list nesnesi kullanılarak değişken sayıda argüman alabilen bir işlevin örneği verilmiştir:

```CPP
#include <cstdarg>
#include <iostream>

double average(int count, ...) {
    va_list args;
    va_start(args, count);

    double sum = 0;
    for (int i = 0; i < count; i++) {
        sum += va_arg(args, double);
    }

    va_end(args);

    return sum / count;
}

int main() {
    double avg = average(4, 2.5, 3.0, 4.5, 5.5);
    std::cout << "Average is " << avg << std::endl;
    return 0;
}

```

> Bu örnekte, average() işlevi va_list türünde bir nesne kullanarak değişken sayıda argüman alır. İşlev, argüman sayısını ve değişken argüman listesini işler ve sonuç olarak ortalama değerini döndürür.

- <cstdarg> başlık dosyası, C dilinde var olan stdarg.h dosyasının C++ karşılığıdır. Bu başlık dosyası, fonksiyonlara değişken sayıda argüman geçirme gibi işlemleri gerçekleştirmek için kullanılır.

- Özellikle, C++'ta printf ve scanf gibi fonksiyonlarda değişken sayıda argüman geçirme işlemleri va_list ve ilgili fonksiyonlarla gerçekleştirilir. <cstdarg> dosyası, bu fonksiyonların C++'ta da kullanımını mümkün kılar.

- Örneğin, aşağıdaki kod bloğunda, printf fonksiyonuna va_list kullanarak değişken sayıda argüman geçiriliyor:

```CPP
#include <cstdio>
#include <cstdarg>

void print(int count, ...) {
    va_list args;
    va_start(args, count);
    for (int i = 0; i < count; ++i) {
        int arg = va_arg(args, int);
        printf("%d ", arg);
    }
    va_end(args);
}

int main() {
    print(3, 1, 2, 3);
    return 0;
}

```

> Bu kod bloğu, print fonksiyonunu tanımlar ve va_list, va_start, va_arg ve va_end fonksiyonlarını kullanarak değişken sayıda argüman geçirme işlemi gerçekleştirir.














