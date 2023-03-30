- array başlık dosyası, C++11 standartlarıyla birlikte standart kütüphaneye eklenmiştir. Bu başlık dosyası, boyutu sabit olan diziler için bir veri türü sunar. Dizi boyutu, dizi nesnesi oluşturulurken belirtilir ve değiştirilemez.

- std::array sınıfı, sabit boyutlu dizileri yönetmek için kullanılır. Bir std::array nesnesi, C++ dilindeki normal diziler gibi davranır, ancak bazı ek özellikler sunar. std::array sınıfı, normal dizilerin aksine bir geçici nesne olarak değil, bir değer olarak geçirilebilir ve fonksiyonlardan geri döndürülebilir.

- std::array sınıfı, C-style dizilerin çoğu dezavantajını giderir. Dizinin boyutu, dizi nesnesi oluşturulurken belirtilir ve çalışma zamanında değiştirilemez. Bu nedenle, std::array sınıfı kullanarak, dizi boyutuna ilişkin hataların önüne geçilebilir.

- Ayrıca, std::array sınıfı, diğer standart kütüphane sınıfları ile birlikte kullanılabilecek birçok fonksiyon ve özellik sağlar. Örneğin, std::array nesneleri, sıralama ve arama gibi işlemler için std::algorithm sınıfındaki fonksiyonlarla birlikte kullanılabilir.

# Classes

- **array**
> std::array, sabit boyutlu dizileri C++ standart kütüphanesi ile kullanmak için sağlanan bir sınıftır. 
- **tuple_size**
> std::tuple_size işlevi, std::tuple gibi bir sınıfın boyutunu, yani kaç eleman içerdiğini sağlar. İşlev, bir sınıfın std::tuple gibi öğelerinin sayısını hesaplamak için kullanılabilir.
- **tuple_element**
> std::tuple_element sınıf şablonu, bir std::tuple veya std::array nesnesinin belirli bir konumundaki elemanın türünü elde etmek için kullanılır.

# Functions
- **operator==**
- **operator<=>**
- **std::swap**
> std::swap işlevi, std::array sınıfı için de desteklenir. Bu işlev, iki std::array nesnesinin elemanlarını birbirleriyle değiştirir.
- **to_array**
> std::to_array işlevi, bir C-style dizi, std::initializer_list veya std::array nesnesini std::array sınıfının bir örneğine dönüştürmek için kullanılır.
- **std::get**
> std::get işlevi, std::array sınıfının bir örneğindeki belirli bir öğeye erişmek için kullanılır. Bu işlev, C++11 standardında tanıtılmıştır ve std::tuple ile kullanımı benzerdir.

# Range Access
- **begin**
- **cbegin**
> begin ve cbegin işlevleri, bir dizi veya başka bir aralığın başlangıç noktasına (yani ilk elemanına) bir işaretçi veya bir sabit işaretçi döndürürler.
- **end**
- **cend**
> end ve cend işlevleri, bir dizi veya başka bir aralığın sonuna (yani son elemanından sonra gelen ilk elemana) bir işaretçi veya bir sabit işaretçi döndürürler.
- **rbegin**
- **crbegin**
> rbegin ve crbegin işlevleri, bir dizi veya başka bir aralığın sondan başlayarak ilk elemanına (yani son elemanına) bir ters işaretçi veya bir sabit ters işaretçi döndürürler.
- **rend**
- **crend**
> rend ve crend işlevleri, bir dizi veya başka bir aralığın sondan başlayarak ilk elemanına (yani son elemanına) bir ters işaretçi veya bir sabit ters işaretçi döndürürler. 
- **size** 
- **ssize**
>  bir koleksiyonun veya bir dizi gibi bir sıralı veri yapısının öğe sayısını döndürür.
- **empty**
> bir koleksiyonun veya bir dizi gibi bir sıralı veri yapısının boş olup olmadığını kontrol etmek için kullanılır. Eğer koleksiyon boşsa, true döndürür; aksi takdirde false döndürür.
- **data**
> bir koleksiyonun veya bir dizinin bellek adresini döndürür. Bu işlev, koleksiyonun veya dizinin bellek bloğuna erişmek için kullanılabilir.
# ÖRNEKLER

### std::array

- std::array, sabit boyutlu dizileri C++ standart kütüphanesi ile kullanmak için sağlanan bir sınıftır. std::array sınıfı, C tarzı dizilerin birçok dezavantajını giderir ve STL algoritmaları ve işlevleriyle uyumlu çalışabilmesi için bir dizi STL tarzı arayüz sağlar.

- std::array sınıfı, birinci öğe türü ve boyutu verilen sabit bir boyutlu dizi oluşturur. Örneğin, aşağıdaki kod parçası, üç elemanlı bir std::array nesnesi oluşturur:

```CPP
#include <array>

std::array<int, 3> arr = {1, 2, 3};

```
- Burada, std::array sınıfı int türünden ve 3 elemandan oluşan bir sabit boyutlu dizi oluşturmak için kullanılır.

- std::array sınıfı, C tarzı dizilerden farklı olarak, eleman sayısını (boyutu) takip eder ve öğelerine erişmek için özel bir arayüz sağlar. Örneğin, aşağıdaki kod parçası, std::array sınıfının elemanlarına erişmek için kullanılabilir:

```CPP
std::array<int, 3> arr = {1, 2, 3};
std::cout << arr[0] << '\n'; // prints "1"
std::cout << arr[1] << '\n'; // prints "2"
std::cout << arr[2] << '\n'; // prints "3"

```
- std::array sınıfı, birçok C++ standart kütüphanesi işlevi ile uyumlu çalışır ve C tarzı dizilerin birçok dezavantajını giderir. Bunlar arasında sınıfın boyutunu takip etmesi, dizilerin kopyalanabilmesi, başka bir std::array nesnesiyle takas edilebilmesi ve daha pek çok özellik bulunur.

### std::tuple_size

- std::tuple_size işlevi, std::array sınıfı için de kullanılabilir. std::array sınıfı, std::tuple sınıfına benzer şekilde, sabit bir boyutta sıralı bir dizi elemanı içerir.

- Aşağıdaki örnek, std::tuple_size işlevinin bir std::array nesnesinin boyutunu hesaplamak için nasıl kullanılabileceğini göstermektedir:

```CPP
#include <array>
#include <iostream>
#include <tuple>

int main() {
    std::array<int, 4> myArray;
    std::cout << std::tuple_size<decltype(myArray)>::value << '\n'; // 4

    return 0;
}

```

> Bu örnekte, std::tuple_size işlevi decltype(myArray) ile çağrılır ve 4 elemanlı bir std::array nesnesinin boyutunu döndürür. value sabiti, std::tuple_size'ın döndürdüğü sabit boyut değerine karşılık gelir.

### std::tuple_element

- std::tuple_element sınıf şablonu, bir std::tuple veya std::array nesnesinin belirli bir konumundaki elemanın türünü elde etmek için kullanılır. Sınıf şablonu, bir tamsayı sabiti (yani, elemanın sırasını) ve std::tuple veya std::array türünü şablon parametresi olarak alır.

- Aşağıdaki örnek, bir std::array nesnesinin belirli bir konumdaki elemanının türünü std::tuple_element kullanarak elde eder:


```CPP
#include <array>
#include <iostream>
#include <tuple>

int main() {
    std::array<int, 4> myArray;
    std::tuple_element<2, decltype(myArray)>::type myElement; // equivalent to int myElement;

    return 0;
}

```

> Bu örnekte, std::tuple_element sınıf şablonu, decltype(myArray) ile birlikte kullanılarak 2 numaralı elemanın türünü int olarak belirler. type üye özelliği, belirli konumdaki elemanın türüne karşılık gelir.



# Functions

### std::swap()

- std::swap işlevi, std::array sınıfı için de desteklenir. Bu işlev, iki std::array nesnesinin elemanlarını birbirleriyle değiştirir.

- Aşağıdaki örnek, iki std::array nesnesinin elemanlarını std::swap işlevi kullanarak birbirleriyle değiştirir:


```CPP
#include <array>
#include <iostream>

int main() {
    std::array<int, 4> arr1{1, 2, 3, 4};
    std::array<int, 4> arr2{5, 6, 7, 8};

    std::cout << "Before swap: arr1 = ";
    for (auto elem : arr1) {
        std::cout << elem << " ";
    }
    std::cout << " arr2 = ";
    for (auto elem : arr2) {
        std::cout << elem << " ";
    }
    std::cout << '\n';

    std::swap(arr1, arr2);

    std::cout << "After swap: arr1 = ";
    for (auto elem : arr1) {
        std::cout << elem << " ";
    }
    std::cout << " arr2 = ";
    for (auto elem : arr2) {
        std::cout << elem << " ";
    }
    std::cout << '\n';

    return 0;
}

```

> Bu örnekte, std::swap işlevi kullanılarak arr1 ve arr2 nesnelerinin elemanları birbirleriyle değiştirilir. arr1 ve arr2 nesneleri tekrar yazdırılırken, elemanların birbirleriyle değiştirildiği görülür.

### to_array()

- std::to_array işlevi, bir C-style dizi, std::initializer_list veya std::array nesnesini std::array sınıfının bir örneğine dönüştürmek için kullanılır. Bu işlev, C++17 standardında tanıtılmıştır.

Aşağıdaki örnek, bir C-style dizisi ve bir std::initializer_list nesnesini std::array sınıfının bir örneğine dönüştürmek için std::to_array işlevini kullanır:

```CPP
#include <array>
#include <iostream>

int main() {
    int cStyleArray[] = {1, 2, 3, 4};
    auto myArray1 = std::to_array(cStyleArray);

    auto myArray2 = std::to_array({5, 6, 7, 8});

    std::cout << "myArray1 = ";
    for (auto elem : myArray1) {
        std::cout << elem << " ";
    }
    std::cout << '\n';

    std::cout << "myArray2 = ";
    for (auto elem : myArray2) {
        std::cout << elem << " ";
    }
    std::cout << '\n';

    return 0;
}

```
> Bu örnekte, std::to_array işlevi kullanılarak, cStyleArray C-style dizisi ve {5, 6, 7, 8} std::initializer_list nesnesi, her biri 4 elemana sahip olan iki ayrı std::array nesnesine dönüştürülür. Dönüştürülmüş diziler, ilgili döngüler aracılığıyla yazdırılır.

### std::get()
- std::get işlevi, std::array sınıfının bir örneğindeki belirli bir öğeye erişmek için kullanılır. Bu işlev, C++11 standardında tanıtılmıştır ve std::tuple ile kullanımı benzerdir.

- std::get işlevi, iki argüman alır: std::array örneği ve istenen öğenin sıfır-tabanlı dizini. İşlev, öğeyi döndürür veya std::out_of_range istisnasını fırlatır.

- Aşağıdaki örnek, std::get işlevinin kullanımını gösterir:

```CPP
#include <array>
#include <iostream>

int main() {
    std::array<int, 5> arr{1, 2, 3, 4, 5};

    std::cout << "arr[2] = " << std::get<2>(arr) << '\n';

    return 0;
}

```
> Bu örnekte, arr adlı std::array nesnesinin 2. öğesi std::get işlevi kullanılarak yazdırılır. std::get<2>(arr) ifadesi, arr nesnesinin 2. öğesini döndürür, yani 3 değerini döndürür.

# Range access

### begin() - cbegin()

- begin ve cbegin işlevleri, bir dizi veya başka bir aralığın başlangıç noktasına (yani ilk elemanına) bir işaretçi veya bir sabit işaretçi döndürürler. Aralık sabitse veya işlev tarafından değiştirilmemesi gerekiyorsa, cbegin işlevi kullanılmalıdır. cbegin işlevi, işaretçinin sabit olduğunu garanti altına alır ve böylece işaretçi üzerinde yapılan işlemlerin aralığın kendisini değiştirmesine izin vermez.

- Bu işlevler C++11'de tanıtılmıştır ve C++17'de, bir dizi veya bir aralıkta değişiklik yapmak istemeyen durumlarda cbegin işlevi kullanımı zorunlu kılmak için const türünün algılanabilirliğini artıracak şekilde düzenlendi.

- Aşağıdaki örnek, begin ve cbegin işlevlerinin kullanımını gösterir:

```CPP
#include <iostream>
#include <array>

int main() {
    std::array<int, 5> myArray{1, 2, 3, 4, 5};

    // begin() kullanımı
    for (auto it = myArray.begin(); it != myArray.end(); ++it) {
        std::cout << *it << ' ';
    }
    std::cout << '\n';

    // cbegin() kullanımı
    for (auto it = myArray.cbegin(); it != myArray.cend(); ++it) {
        std::cout << *it << ' ';
    }
    std::cout << '\n';

    return 0;
}

```
> Bu örnekte, myArray adlı std::array nesnesinin öğeleri, begin() ve cbegin() işlevleri kullanılarak sırasıyla değiştirilir. begin() işlevi, işaretçinin aralığın üzerinde değişiklik yapmasına izin verirken, cbegin() işlevi aralık sabitse veya işlev tarafından değiştirilmemesi gerekiyorsa kullanılır.

### end() - cend()

- end ve cend işlevleri, bir dizi veya başka bir aralığın sonuna (yani son elemanından sonra gelen ilk elemana) bir işaretçi veya bir sabit işaretçi döndürürler. Aralık sabitse veya işlev tarafından değiştirilmemesi gerekiyorsa, cend işlevi kullanılmalıdır. cend işlevi, işaretçinin sabit olduğunu garanti altına alır ve böylece işaretçi üzerinde yapılan işlemlerin aralığın kendisini değiştirmesine izin vermez.

- Bu işlevler C++11'de tanıtılmıştır ve C++17'de, bir dizi veya bir aralıkta değişiklik yapmak istemeyen durumlarda cend işlevi kullanımı zorunlu kılmak için const türünün algılanabilirliğini artıracak şekilde düzenlendi.

- Aşağıdaki örnek, end ve cend işlevlerinin kullanımını gösterir:

```CPP
#include <iostream>
#include <array>

int main() {
    std::array<int, 5> myArray{1, 2, 3, 4, 5};

    // end() kullanımı
    for (auto it = myArray.begin(); it != myArray.end(); ++it) {
        std::cout << *it << ' ';
    }
    std::cout << '\n';

    // cend() kullanımı
    for (auto it = myArray.cbegin(); it != myArray.cend(); ++it) {
        std::cout << *it << ' ';
    }
    std::cout << '\n';

    return 0;
}

```
> Bu örnekte, myArray adlı std::array nesnesinin öğeleri, end() ve cend() işlevleri kullanılarak sırasıyla değiştirilir. end() işlevi, işaretçinin aralığın üzerinde değişiklik yapmasına izin verirken, cend() işlevi aralık sabitse veya işlev tarafından değiştirilmemesi gerekiyorsa kullanılır.



### rbegin() - crbegin()

- rbegin ve crbegin işlevleri, bir dizi veya başka bir aralığın sondan başlayarak ilk elemanına (yani son elemanına) bir ters işaretçi veya bir sabit ters işaretçi döndürürler. Aralık sabitse veya işlev tarafından değiştirilmemesi gerekiyorsa, crbegin işlevi kullanılmalıdır. crbegin işlevi, işaretçinin sabit olduğunu garanti altına alır ve böylece işaretçi üzerinde yapılan işlemlerin aralığın kendisini değiştirmesine izin vermez.

- Bu işlevler C++11'de tanıtılmıştır ve C++17'de, bir dizi veya bir aralıkta değişiklik yapmak istemeyen durumlarda crbegin işlevi kullanımı zorunlu kılmak için const türünün algılanabilirliğini artıracak şekilde düzenlendi.

- Aşağıdaki örnek, rbegin ve crbegin işlevlerinin kullanımını gösterir:

```CPP
#include <iostream>
#include <array>

int main() {
    std::array<int, 5> myArray{1, 2, 3, 4, 5};

    // rbegin() kullanımı
    for (auto it = myArray.rbegin(); it != myArray.rend(); ++it) {
        std::cout << *it << ' ';
    }
    std::cout << '\n';

    // crbegin() kullanımı
    for (auto it = myArray.crbegin(); it != myArray.crend(); ++it) {
        std::cout << *it << ' ';
    }
    std::cout << '\n';

    return 0;
}

```
> Bu örnekte, myArray adlı std::array nesnesinin öğeleri, rbegin() ve crbegin() işlevleri kullanılarak sırasıyla ters çevrilir. rbegin() işlevi, işaretçinin aralığın üzerinde değişiklik yapmasına izin verirken, crbegin() işlevi aralık sabitse veya işlev tarafından değiştirilmemesi gerekiyorsa kullanılır.

### rend() - crend()

- rend ve crend işlevleri, bir dizi veya başka bir aralığın sondan başlayarak ilk elemanına (yani son elemanına) bir ters işaretçi veya bir sabit ters işaretçi döndürürler. Aralık sabitse veya işlev tarafından değiştirilmemesi gerekiyorsa, crend işlevi kullanılmalıdır. crend işlevi, işaretçinin sabit olduğunu garanti altına alır ve böylece işaretçi üzerinde yapılan işlemlerin aralığın kendisini değiştirmesine izin vermez.

- Bu işlevler C++11'de tanıtılmıştır ve C++17'de, bir dizi veya bir aralıkta değişiklik yapmak istemeyen durumlarda crend işlevi kullanımı zorunlu kılmak için const türünün algılanabilirliğini artıracak şekilde düzenlendi.

- Aşağıdaki örnek, rend ve crend işlevlerinin kullanımını gösterir:

```CPP
#include <iostream>
#include <array>

int main() {
    std::array<int, 5> myArray{1, 2, 3, 4, 5};

    // rend() kullanımı
    for (auto it = myArray.rend(); it != myArray.rbegin(); --it) {
        std::cout << *(it - 1) << ' ';
    }
    std::cout << '\n';

    // crend() kullanımı
    for (auto it = myArray.crend(); it != myArray.crbegin(); --it) {
        std::cout << *(it - 1) << ' ';
    }
    std::cout << '\n';

    return 0;
}

```
> Bu örnekte, myArray adlı std::array nesnesinin öğeleri, rend() ve crend() işlevleri kullanılarak sırasıyla ters çevrilir. rend() işlevi, işaretçinin aralığın üzerinde değişiklik yapmasına izin verirken, crend() işlevi aralık sabitse veya işlev tarafından değiştirilmemesi gerekiyorsa kullanılır.

### size() - ssize()
- size() işlevi, bir koleksiyonun veya bir dizi gibi bir sıralı veri yapısının öğe sayısını döndürür. Eğer koleksiyon sabitse, işlev sabit bir referans olarak alınabilir.

Öte yandan, ssize() işlevi, bir koleksiyonun veya bir dizi gibi bir sıralı veri yapısının öğe sayısını std::ptrdiff_t türünde döndürür. ssize() işlevi, başlangıç ve son arasındaki farkın türünden bağımsız olarak kullanılabilir.

Örnek kullanımlar:

```CPP
#include <iostream>
#include <vector>

int main() {
    std::vector<int> v = {1, 2, 3, 4, 5};

    std::cout << "v.size(): " << v.size() << '\n';      // Output: 5
    std::cout << "ssize(v): " << ssize(v) << '\n';      // Output: 5

    const std::vector<int>& cv = v;

    std::cout << "cv.size(): " << cv.size() << '\n';    // Output: 5
    std::cout << "ssize(cv): " << ssize(cv) << '\n';    // Output: 5

    return 0;
}

```
> Bu örnekte, bir std::vector nesnesi v oluşturulur ve size() ile ssize() işlevleri kullanılarak eleman sayısı yazdırılır. İkinci iki cout ifadesinde, cv adlı sabit bir std::vector nesnesi kullanılır. size() işlevi, burada da kullanılabilir, ancak ssize() işlevi de geçerlidir.

### empty()

- empty() işlevi, bir koleksiyonun veya bir dizi gibi bir sıralı veri yapısının boş olup olmadığını kontrol etmek için kullanılır. Eğer koleksiyon boşsa, true döndürür; aksi takdirde false döndürür.

- Örnek kullanımlar:

```CPP
#include <iostream>
#include <vector>

int main() {
    std::vector<int> v1;
    std::vector<int> v2 = {1, 2, 3, 4, 5};

    std::cout << std::boolalpha << "v1.empty(): " << v1.empty() << '\n';    // Output: true
    std::cout << std::boolalpha << "v2.empty(): " << v2.empty() << '\n';    // Output: false

    return 0;
}

```
- Bu örnekte, v1 ve v2 adlı iki std::vector nesnesi oluşturulur ve empty() işlevleri kullanılarak boşluk durumu kontrol edilir. v1 boş bir koleksiyondur, bu nedenle empty() işlevi true döndürür. v2, bazı öğeler içerir, bu nedenle empty() işlevi false döndürür.

- empty() işlevi, özellikle bir koleksiyonun eleman sayısının 0 olduğunu kontrol etmek için kullanışlıdır. Örneğin, bir std::vector'de öğe sayısı 0 ise, begin() ve end() işlevleri arasındaki bir aralığın başlangıcı ve sonu aynı değere sahiptir. Bu durum, işlevlerin "boş bir aralık" olarak kabul edilebilir bir şekilde çalışmasına izin verir.

### data()

- data() işlevi, bir koleksiyonun veya bir dizinin bellek adresini döndürür. Bu işlev, koleksiyonun veya dizinin bellek bloğuna erişmek için kullanılabilir.

Bu işlev, özellikle C tarzı dizilerle çalışırken kullanışlıdır. Örneğin, bir C tarzı dizinin bellek bloğuna doğrudan erişmek için data() işlevi kullanılabilir.

Aşağıda örnek bir kullanım gösterilmiştir:

```CPP
#include <iostream>
#include <array>

int main() {
    std::array<int, 5> arr = {1, 2, 3, 4, 5};

    int* p = arr.data();    // p, arr dizisinin bellek bloğunu gösterir

    std::cout << "arr[0] = " << arr[0] << ", *p = " << *p << '\n';    // Output: arr[0] = 1, *p = 1

    *p = 10;    // arr[0]'ın değerini 10 yapar

    std::cout << "arr[0] = " << arr[0] << ", *p = " << *p << '\n';    // Output: arr[0] = 10, *p = 10

    return 0;
}

```

> Bu örnekte, arr adlı bir std::array nesnesi oluşturulur. data() işlevi, arr dizisinin bellek bloğuna bir işaretçi döndürür. İşaretçi p'ye atanır ve p kullanılarak arr dizisinin ilk elemanına erişilir. p kullanılarak yapılan değişiklikler, arr dizisindeki ilgili elemanlara yansır.



# Örnekler:

- std::array sınıfı, kullanımı kolaydır ve temel bir veri türü olarak düşünülebilir. Örneğin, aşağıdaki kodda, std::array nesnesi arr oluşturulmuştur ve ardından for döngüsü kullanılarak dizinin elemanları yazdırılmıştır:

```CPP
#include <iostream>
#include <array>

int main() {
    std::array<int, 5> arr = {1, 2, 3, 4, 5};

    for (int i = 0; i < arr.size(); i++) {
        std::cout << arr[i] << " ";
    }

    return 0;
}

```

- Bu kod, 1 2 3 4 5 çıktısını verir.

- std::array sınıfının bir başka özelliği, dizi elemanlarını atama veya karşılaştırma gibi işlemler için kullanılabilecek bir dizi operatör sağlamasıdır. Örneğin, aşağıdaki kodda, std::array nesneleri arr1 ve arr2 oluşturulmuş ve ardından bu nesnelerin elemanları karşılaştırılmıştır:

```CPP
#include <iostream>
#include <array>

int main() {
    std::array<int, 3> arr1 = {1, 2, 3};
    std::array<int, 3> arr2

```

# std::array ile neler yapabiliriz? Ne zaman kullanmalıyım?

- std::array sınıfı, sabit boyutlu bir dizi veriyi yönetmek için kullanılır. std::array sınıfı C dizilerine benzer, ancak birçok farklılıkları vardır. std::array, boyutu derleme zamanında bilinen bir dizi verisi için daha güvenli bir alternatiftir. C dizilerine göre birçok avantajı vardır, örneğin:

- **Sınıf yapısı nedeniyle, std::array ile C dizilerindeki gibi bellek sınırlarını aşmak mümkün değildir.**
- **Dizinin boyutu bilindiğinden, std::array'nin elemanlarına doğrudan erişebilirsiniz. Elemanları doğrudan erişebilmek, C dizilerindeki gibi bir dizide gezinmekten daha hızlı ve verimlidir.**
- **std::array sınıfı, C dizilerindeki gibi pointer aritmetiği kullanılmaz, bu nedenle hatalı dizinlere erişme riski yoktur.**
- **std::array sınıfı, C dizilerine göre daha kolay okunabilir ve daha özgüvenle kullanılabilir. Ayrıca, standart kütüphanenin diğer bileşenleriyle birlikte daha uyumlu çalışır.**
- std::array kullanımı özellikle boyutu sabit olan diziler için uygundur. Örneğin, sabit boyutlu matrisler, önceden belirlenmiş sütun ve satırlarla belirli bir boyuta sahip vektörler veya bir histogramda sayılan öğe sayısı gibi durumlarda kullanılabilir.**

- std::array sınıfının, dizi elemanlarına erişme, sıralama, arama, toplama ve benzeri işlemleri yapabilen bir dizi fonksiyonu vardır. Ayrıca, C++11'de eklenen özellikler olan begin() ve end() fonksiyonları sayesinde, C++11 öncesi sürümlerdeki C++ kodlarında bulunan for döngüleri gibi yerlerde de kullanılabilir.

# Ben neden std::vector yerine std::array kullanayım?

- std::vector ve std::array farklı yapılar olduğu için, hangisinin kullanılacağına karar vermek ihtiyaca göre değişir.

- std::array'ler statik bir boyuta sahipken, std::vector'ler dinamik olarak boyutlandırılabilirler. Yani, eğer sabit bir boyutlu bir veri kümesine ihtiyacınız varsa, std::array kullanmak uygun olabilir. Ancak, eğer veri kümeniz değişken bir boyuta sahip olacaksa, o zaman std::vector kullanmak daha uygun olacaktır.

- std::array'in avantajları arasında, boyutunun sabit olması nedeniyle, bellekte daha küçük bir ayak izi ve daha hızlı erişim zamanı bulunurken, std::vector'un boyutu dinamik olduğundan, daha esnek bir yapıya sahiptir ve dinamik olarak boyutlandırılabilir.

- Özetle, sabit bir boyuta sahip veri kümesi için std::array kullanmak daha uygunken, değişken bir boyuta sahip veri kümesi için std::vector kullanmak daha uygun olabilir.

# sabit boyutlu bir dizide std::vector kullandığımız zaman verimsiz bir kod yazmış mı oluruz çünkü dinamik bellek yömnetimi devreye giriyor

- Evet, doğru bir değerlendirme. Sabit boyutlu bir dizide std::vector kullanmak, gereksiz bir dinamik bellek yönetimi işlemi olduğu için verimsiz bir kod yazmış olabilirsiniz. Sabit boyutlu bir dizi için std::array kullanmak, bellek yönetimini daha verimli bir şekilde yapmanıza olanak tanır. Ayrıca, std::array'ın boyutu, derleme zamanında sabit olduğu için çalışma zamanında bellek boyutunu değiştirmeniz mümkün değildir. Bu nedenle, eğer sabit boyutlu bir diziye ihtiyacınız varsa, std::array'ı tercih etmek daha uygun olacaktır.












