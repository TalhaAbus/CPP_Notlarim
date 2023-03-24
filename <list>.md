# std::list

- <list başlık dosyası, C++ standart kütüphanesinde yer alan bir başlık dosyasıdır ve çift yönlü bağlı liste yapısını tanımlayan std::list sınıfını içerir.

- std::list sınıfı, elemanları çift yönlü bir bağlı liste şeklinde tutan bir veri yapısıdır. Listeler, elemanların ekleme ve çıkarma işlemlerinde daha hızlıdır ancak elemanlara rastgele erişimde (örneğin, dizilerdeki gibi) daha yavaştırlar.

- std::list sınıfı, elemanları push_front, push_back, pop_front ve pop_back gibi işlevlerle ekleyip ve çıkarabilen bir arayüz sağlar. Elemanlara doğrudan erişim mümkün değildir, ancak begin() ve end() işlevleri aracılığıyla liste üzerinde döngüler oluşturulabilir.

- Örneğin, aşağıdaki kodda std::list sınıfı kullanılarak bir liste oluşturulur ve liste üzerinde döngü kullanarak elemanlar ekrana yazdırılır:

```CPP
#include <iostream>
#include <list>

int main() {
  std::list<int> my_list = {1, 2, 3, 4, 5};
  for (auto it = my_list.begin(); it != my_list.end(); ++it) {
    std::cout << *it << ' ';
  }
  std::cout << '\n';
  return 0;
}

```

> Bu kodda, std::list sınıfı kullanılarak my_list adında bir liste oluşturulur ve begin() ve end() işlevleri kullanılarak listenin elemanları üzerinde bir döngü oluşturulur. Döngüdeki her bir eleman, *it ifadesi ile elde edilir ve ekrana yazdırılır. Sonuç olarak, çıktı şu şekilde olur:

```CPP
1 2 3 4 5

```


- <list başlık dosyası, std::list sınıfının yanı sıra std::forward_list sınıfını da içerir. std::forward_list, elemanları tek yönlü bir bağlı liste şeklinde tutan bir sınıftır ve std::list sınıfına kıyasla daha düşük bellek kullanımı ve daha hızlı ekleme/çıkarma işlemleri sağlar. Ancak, elemanlara rastgele erişim mümkün değildir.
