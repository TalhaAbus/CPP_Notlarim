# std::functional nedir

- std::functional C++ standart kütüphanesinde yer alan bir başlık dosyasıdır. Bu başlık dosyası, C++ dilindeki fonksiyonel programlama araçlarını sağlayan bir dizi sınıf ve fonksiyonlar içerir.

- std::functional başlık dosyasında tanımlanan sınıflar ve fonksiyonlar arasında, aşağıdakiler yer alır:

- std::function: İşlev nesnelerinin genel amacı için kullanılan bir sınıftır. Bu sınıf, işlevleri nesneler olarak taşıyabilir ve işlevlerin parametreleri ve dönüş değerleri hakkında bilgi sahibi olabilir.
- std::bind: İşlevlere argümanlar bağlamak için kullanılan bir fonksiyondur. Bu fonksiyon, argümanlarınızı işlevin parametrelerine bağlayabilir ve bağlı işlevi bir işlev nesnesi olarak döndürebilir.
- std::mem_fn: Sınıf üyelerinin işlev nesneleri olarak taşınması için kullanılan bir fonksiyondur. Bu fonksiyon, sınıfın bir üye işlevini bir işlev nesnesi olarak döndürebilir.
- std::reference_wrapper: Referansları nesneler olarak taşıyabileceğiniz bir sınıftır. Bu sınıf, bir işlevin argümanları olarak kullanılabilen bir referansı nesne olarak taşır.
- Bu araçlar, C++ dilinde fonksiyonel programlama yapmayı kolaylaştıran araçlar sunar. Özellikle, std::function sınıfı, işlevleri bir nesne olarak taşıyabilme özelliğiyle, kodun daha okunaklı ve esnek hale gelmesine yardımcı olabilir. std::bind fonksiyonu, işlevlere argümanlar bağlayarak, işlev çağrılarını daha okunaklı hale getirebilir. std::mem_fn fonksiyonu ise, sınıf üyelerinin işlev nesneleri olarak taşınması için kullanılan bir araçtır.

- Özetle, std::functional başlık dosyası, C++ dilinde fonksiyonel programlama araçlarını sağlayan bir dizi sınıf ve fonksiyon içerir.

- Aşağıda, std::function ve std::bind kullanarak basit bir hesap makinesi uygulaması için örnek bir kod verilmiştir:

```CPP
#include <iostream>
#include <functional>

using namespace std;

int add(int a, int b) {
    return a + b;
}

int subtract(int a, int b) {
    return a - b;
}

int multiply(int a, int b) {
    return a * b;
}

int divide(int a, int b) {
    return a / b;
}

int main() {
    int a = 10, b = 5;
    
    // İşlev nesnelerini tanımla
    function<int(int, int)> add_fn = add;
    function<int(int, int)> subtract_fn = subtract;
    function<int(int, int)> multiply_fn = multiply;
    function<int(int, int)> divide_fn = divide;
    
    // İşlemleri bağla
    auto add_op = bind(add_fn, a, b);
    auto subtract_op = bind(subtract_fn, a, b);
    auto multiply_op = bind(multiply_fn, a, b);
    auto divide_op = bind(divide_fn, a, b);
    
    // Sonuçları ekrana yazdır
    cout << "Addition: " << add_op() << endl;
    cout << "Subtraction: " << subtract_op() << endl;
    cout << "Multiplication: " << multiply_op() << endl;
    cout << "Division: " << divide_op() << endl;
    
    return 0;
}

```
- Bu kodda, add(), subtract(), multiply() ve divide() işlevleri tanımlanmıştır. Daha sonra, bu işlevleri std::function sınıfı kullanarak işlev nesnelerine dönüştürülür. std::bind fonksiyonu kullanılarak, bu işlev nesneleri, a ve b değişkenlerine bağlanarak, işlemler için hazırlanır.

- Son olarak, add_op(), subtract_op(), multiply_op() ve divide_op() işlevleri çağrılarak, sonuçlar ekrana yazdırılır.

- Bu örnek, std::function ve std::bind kullanarak işlevlerin parametrelerini ve geri dönüş değerlerini bağlama işleminin nasıl yapılacağını göstermektedir.
