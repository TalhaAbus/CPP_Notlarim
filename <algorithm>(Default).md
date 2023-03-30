# algorithm

- Algorithm C++ standart kütüphanesinde bir container değildir. Tam tersine, algorithm sınıfı, C++ standart kütüphanesinde bulunan bir header dosyasıdır ve STL (Standard Template Library) için kullanılan bir dizi algoritma fonksiyonu sağlar.

- Bu algoritma fonksiyonları, STL'nin temel container sınıfları olan vector, list, set, map gibi sınıflarla birlikte kullanılabilir. algorithm sınıfı, bu container sınıflarının içeriğinde gezinmek ve bu içerikler üzerinde çeşitli işlemler yapmak için kullanılır.

- Örneğin, std::sort, std::find, std::count_if, std::transform gibi algoritma fonksiyonları, bir vector veya list gibi bir container içeriğindeki verileri sıralamak, aramak, saymak veya dönüştürmek için kullanılabilir.

- İşte std::sort algoritma fonksiyonunun bir örneği:

```CPP
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> vec { 5, 3, 1, 4, 2 };

    // Vector'un elemanlarını sıralama
    std::sort(vec.begin(), vec.end());

    // Sıralanmış vektörü yazdırma
    std::cout << "Sıralanmış vektör: ";
    for (int i : vec) {
        std::cout << i << " ";
    }
    std::cout << std::endl;

    return 0;
}

```

- Bu kodda, önce bir std::vectorint oluşturulur ve bu vektörün içine beş sayı eklenir. Daha sonra, std::sort algoritma fonksiyonu, vec.begin() ve vec.end() aralığında bulunan elemanları sıralar. Son olarak, for döngüsü ile sıralanmış vektör yazdırılır.

- Benzer şekilde, std::find, std::count_if, std::transform gibi diğer algoritma fonksiyonları da bir container içeriğindeki verileri aramak, saymak veya dönüştürmek için kullanılabilir. Örneğin:

```CPP
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> vec { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };

    // Vector'deki tek sayıların sayısını bulma
    int tek_sayi_sayisi = std::count_if(vec.begin(), vec.end(), [](int x) { return x % 2 != 0; });

    // Vector'deki her elemanı iki katına çıkarma
    std::transform(vec.begin(), vec.end(), vec.begin(), [](int x) { return x * 2; });

    // Yeni vektörü yazdırma
    std::cout << "Yeni vektör: ";
    for (int i : vec) {
        std::cout << i << " ";
    }
    std::cout << std::endl;

    return 0;
}

```
> Bu kodda, önce bir std::vectorint oluşturulur ve bu vektörün içine 1'den 10'a kadar olan sayılar eklenir. Daha sonra, std::count_if algoritma fonksiyonu, vec.begin() ve vec.end() aralığında bulunan elemanlar arasında gezinerek, tek sayıların sayısını hesaplar. std::transform algoritma fonksiyonu ise, vec.begin() ve vec.end() aralığındaki her elemanı iki katına çıkarır. Son olarak, for döngüsü ile yeni vektör yazdırılır.

# Fonksiyolar

- **std::all_of(first, last, pred):** aralıktaki tüm öğelerin pred işlevi tarafından belirtilen özelliğe sahip olup olmadığını kontrol eder. first ve last aralığın başlangıç ve sonunu gösteren işaretçilerdir, pred ise kontrol edilecek özelliği belirten bir işlev nesnesidir.
- **std::any_of(first, last, pred):** aralıktaki en az bir öğenin pred işlevi tarafından belirtilen özelliğe sahip olup olmadığını kontrol eder.
- **std::none_of(first, last, pred):** aralıktaki hiçbir öğenin pred işlevi tarafından belirtilen özelliğe sahip olup olmadığını kontrol eder.
- **std::for_each()** işlevi, bir işlev nesnesi ve bir aralık verildiğinde, aralıktaki her öğe için işlevi çağırır. 
- for_each_n
- count
- count_if
- mismatch
- find
- find_if
- find_if_not
- find_end
- find_first_of
- adjacent_find
- search
- search_n

# Modifying sequence operations

- copy
- copy_if
- copy_n
- copy_backward
- move
- move_backward
- fill
- fill_n
- transform
- generate
- generate_n
- remove
- remove_if
- remove_copy
- remove_copy_if
- replace
- replace_if
- replace_copy
- replace_copy_if
- swap
- swap_ranges
- iter_ranges
- iter_swap
- reverse
- reverse_copy
- rotate
- rotate_copy
- shift_left
- shift_right
- random_shuffle
- shuffle
- sample
- unique
- unique_copy

# Partitioning operations

- is_pratitioned
- partition
- partition_copy
- stable_partition
- partition_point

# Sorting Operations

- is_sorted
- is_sorted_until
- sort
- partial_sort
- partial_sort_copy
- stable_sort
- nth_element

# Binary Search Operations (On Sorted Ranges)
- lower_bound
- upper_bound
- binary_search
- equal_range

# Other Operations on Sorted Ranges
- merge
- inplace_merge

# Set Operations (On Sorted Ranges)
- includes
- set_difference
- set_intersections
- set_symmetric_difference
- set_union

# Heap Operations
- is_heap
- is_heap_until
- make_heap
- push_heap
- pop_heap
- sort_heap

# Minimum/ Maximum Operations
- max
- max_element
- min
- min_element
- minmax
- minmax_element
- clamp

# Comparison Operations
- equal
- lexicographical_compare
- lexicographical_compare_three_way

# Permutation Operations
- is_permuatation
- next_permutation
- prev_permutation

# IMPLEMENTATIONS

## Fonksiyolar 

### all_of - any_of - none_of

- Bu üç C++ algoritması, bir aralıktaki öğelerin belirli bir özelliğe sahip olup olmadığını kontrol etmek için kullanılır. İşlevlerin sözdizimi şu şekildedir:

- **std::all_of(first, last, pred):** aralıktaki tüm öğelerin pred işlevi tarafından belirtilen özelliğe sahip olup olmadığını kontrol eder. first ve last aralığın başlangıç ve sonunu gösteren işaretçilerdir, pred ise kontrol edilecek özelliği belirten bir işlev nesnesidir.
- **std::any_of(first, last, pred):** aralıktaki en az bir öğenin pred işlevi tarafından belirtilen özelliğe sahip olup olmadığını kontrol eder.
- **std::none_of(first, last, pred):** aralıktaki hiçbir öğenin pred işlevi tarafından belirtilen özelliğe sahip olup olmadığını kontrol eder.

- Bu işlevler C++11'de tanıtılmıştır ve C++17'de C++ aralık ifadeleri (std::ranges) için de tanıtılmıştır.

- İşte bir örnek kod parçası, bu işlevlerin nasıl kullanıldığını gösteriyor: 

```CPP
#include <iostream>
#include <algorithm>
#include <vector>

int main() {
  std::vector<int> my_vec {1, 2, 3, 4, 5};

  if (std::all_of(my_vec.begin(), my_vec.end(), [](int i){return i > 0;})) {
    std::cout << "Tüm öğeler pozitif" << std::endl;
  } else {
    std::cout << "Tüm öğeler pozitif değil" << std::endl;
  }

  if (std::any_of(my_vec.begin(), my_vec.end(), [](int i){return i % 2 == 0;})) {
    std::cout << "En az bir öğe çift" << std::endl;
  } else {
    std::cout << "Hiçbir öğe çift değil" << std::endl;
  }

  if (std::none_of(my_vec.begin(), my_vec.end(), [](int i){return i < 0;})) {
    std::cout << "Hiçbir öğe negatif değil" << std::endl;
  } else {
    std::cout << "En az bir öğe negatif" << std::endl;
  }

  return 0;
}

```
> Bu örnek kod, std::all_of(), std::any_of() ve std::none_of() işlevlerinin kullanımını göstermektedir. std::vectorint türünde bir vektör oluşturuyoruz ve bu vektörün öğelerinin pozitif, çift veya negatif olup olmadığını kontrol ediyoruz.

> Her işlev, belirtilen özelliğe sahip olan öğe sayısına göre true veya false değeri döndürür. Yukarıdaki kodda, std::all_of() işlevinin sonucu true olarak döndürür çünkü tüm öğeler pozitiftir. std::any_of() işlevi, en az bir çift sayı içeren vektörde true döndürürken, std::none_of() işlevi, herhangi bir negatif öğe içermeyen bir vektörde true döndürür.

Bu işlevlerin kullanımı, bir aralıktaki öğelerin özelliklerini kontrol etmek için oldukça yaygındır ve STL algoritmalarının güçlü bir parçasıdır.

### for_each

- std::for_each() C++ algoritması, bir aralıktaki öğeler üzerinde bir işlev işlevini uygular. Bu algoritmanın amacı, bir dizi işlemi bir aralık üzerinde uygulamak istediğinizde kullanımı kolay bir seçenek sunmaktır.

- std::for_each() işlevi, bir işlev nesnesi ve bir aralık verildiğinde, aralıktaki her öğe için işlevi çağırır. İşlev nesnesi, aralıktaki her öğe için çağrılacak işlevi belirtir. İşlevin sözdizimi şu şekildedir:

```CPP
template <class InputIt, class UnaryFunction>
UnaryFunction for_each(InputIt first, InputIt last, UnaryFunction f);

```
- Bu işlevin ilk iki parametresi, aralığın başlangıç ve sonunu gösteren işaretçilerdir. Son parametre, aralıktaki her öğe için çağrılacak işlevi belirten bir işlev nesnesidir. İşlev, aralıktaki her öğe için çağrıldığında işlevin geri dönüş değeri kullanılmaz.

- İşte bir örnek kod parçası, std::for_each() işlevinin nasıl kullanılabileceğini gösteriyor:

```CPP
#include <iostream>
#include <algorithm>
#include <vector>

void print_num(int num) {
  std::cout << num << " ";
}

int main() {
  std::vector<int> my_vec {1, 2, 3, 4, 5};

  std::for_each(my_vec.begin(), my_vec.end(), print_num);

  return 0;
}

```
> Bu örnek kod, std::for_each() işlevinin kullanımını göstermektedir. std::vector<int> türünde bir vektör oluşturuyoruz ve vektördeki her öğeyi ekrana yazdırmak için print_num() işlevini kullanıyoruz. std::for_each() işlevi, print_num() işlevini her öğe için çağırır ve sonuç olarak 1 2 3 4 5 değerlerini ekrana yazdırır.

- Bu işlevin kullanımı, bir aralıktaki öğeleri bir dizi işlem için kullanmak istediğiniz durumlarda oldukça yaygındır. Örneğin, bir vektördeki tüm öğeleri toplamak veya bir dosyadaki tüm satırları okumak için kullanılabilir.






























