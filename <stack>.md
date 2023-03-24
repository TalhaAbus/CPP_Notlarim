# Stack

- <stack başlık dosyası, std::stack sınıfını tanımlar. Bu sınıf, önceden tanımlanmış bir veri yapısı olan yığıtın (stack) bir sarmalayıcısıdır. Yığıt veri yapısı, verilerin yalnızca en üstünden (top) eklenmesine ve çıkarılmasına izin verir.

- std::stack sınıfı, yığıt veri yapısını uygulamak için bir dizi işlev ve özellik sağlar. push() işlevi, yığıtın üstüne yeni bir öğe eklerken, pop() işlevi en üstteki öğeyi çıkarır. top() işlevi, en üstteki öğeye başvurmanızı sağlar. empty() işlevi, yığının boş olup olmadığını kontrol ederken size() işlevi, yığında kaç öğe olduğunu belirler.

- Aşağıda std::stack sınıfının basit bir kullanım örneği verilmiştir:

```CPP
#include <iostream>
#include <stack>

int main() {
    std::stack<int> myStack;

    myStack.push(10);
    myStack.push(20);
    myStack.push(30);

    std::cout << "Top element: " << myStack.top() << std::endl;
    std::cout << "Stack size: " << myStack.size() << std::endl;

    myStack.pop();
    std::cout << "Top element: " << myStack.top() << std::endl;

    return 0;
}

```

- Bu örnekte, std::stack sınıfı bir int türünde yığıt oluşturur. push() işlevi kullanılarak yığının üstüne üç öğe eklenir. top() işlevi kullanılarak en üstteki öğe alınırken size() işlevi yığıtta kaç öğe olduğunu belirler. pop() işlevi kullanılarak en üstteki öğe çıkarılır.
- std::stack sınıfı, son giren ilk çıkar (Last-In-First-Out) veri yapısı olarak adlandırılan ve birçok problemde kullanılan bir veri yapısını temsil eder. Bu veri yapısı, bir öğenin yalnızca en üstündeki öğeyi değiştirerek veya kaldırarak erişilebilir olduğu senaryolarda faydalıdır.

- Örneğin, geri alma işlevselliğinin uygulandığı bir metin düzenleyicisi düşünelim. Kullanıcı, yaptığı değişikliklerin bir yığında saklandığı ve geri alma işlemi yaparken en son yapılan değişikliklerin en önce geri alındığı bir yığın kullanarak değişiklikleri geri alabilir. Bu senaryoda, std::stack veri yapısı yararlı bir araç olabilir.

- Benzer şekilde, web tarayıcılarda "geri" ve "ileri" butonları da son giren ilk çıkar veri yapısının bir uygulamasıdır.
















































