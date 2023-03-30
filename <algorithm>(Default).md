# algorithm

- Algorithm C++ standart kütüphanesinde bir container değildir. Tam tersine, algorithm sınıfı, C++ standart kütüphanesinde bulunan bir header dosyasıdır ve STL (Standard Template Library) için kullanılan bir dizi algoritma fonksiyonu sağlar.

- Bu algoritma fonksiyonları, STL'nin temel container sınıfları olan vector, list, set, map gibi sınıflarla birlikte kullanılabilir. algorithm sınıfı, bu container sınıflarının içeriğinde gezinmek ve bu içerikler üzerinde çeşitli işlemler yapmak için kullanılır.

- Örneğin, std::sort, std::find, std::count_if, std::transform gibi algoritma fonksiyonları, bir vector veya list gibi bir container içeriğindeki verileri sıralamak, aramak, saymak veya dönüştürmek için kullanılabilir.



# Fonksiyolar

- **all_of(first, last, pred):** 
> aralıktaki tüm öğelerin pred işlevi tarafından belirtilen özelliğe sahip olup olmadığını kontrol eder. first ve last aralığın başlangıç ve sonunu gösteren işaretçilerdir, pred ise kontrol edilecek özelliği belirten bir işlev nesnesidir.
- **any_of(first, last, pred):** 
> aralıktaki en az bir öğenin pred işlevi tarafından belirtilen özelliğe sahip olup olmadığını kontrol eder.
- **none_of(first, last, pred):** 
> aralıktaki hiçbir öğenin pred işlevi tarafından belirtilen özelliğe sahip olup olmadığını kontrol eder.
- **for_each()** 
> işlevi, bir işlev nesnesi ve bir aralık verildiğinde, aralıktaki her öğe için işlevi çağırır. 
- **for_each_n()**  
> belirli bir sayıda öğe üzerinde bir işlev işlevini uygular. 
- **count()** 
> bir aralıktaki öğelerin belirli bir değere eşit olup olmadığını kontrol etmek için kullanılır. Bu algoritmanın amacı, belirli bir öğe sayısını bulmak istediğinizde kullanımı kolay bir seçenek sunmaktır.
- **count_if()** 
> C++ algoritması, bir aralıktaki öğelerin belirli bir özelliğe sahip olup olmadığını kontrol etmek için kullanılır. Bu algoritmanın amacı, belirli bir özelliğe sahip olan öğe sayısını bulmak istediğinizde kullanımı kolay bir seçenek sunmaktır.


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
> Bu örnek kod, std::for_each() işlevinin kullanımını göstermektedir. std::vector int türünde bir vektör oluşturuyoruz ve vektördeki her öğeyi ekrana yazdırmak için print_num() işlevini kullanıyoruz. std::for_each() işlevi, print_num() işlevini her öğe için çağırır ve sonuç olarak 1 2 3 4 5 değerlerini ekrana yazdırır.

- Bu işlevin kullanımı, bir aralıktaki öğeleri bir dizi işlem için kullanmak istediğiniz durumlarda oldukça yaygındır. Örneğin, bir vektördeki tüm öğeleri toplamak veya bir dosyadaki tüm satırları okumak için kullanılabilir.

### for_each_n 

- std::for_each_n() C++ algoritması, belirli bir sayıda öğe üzerinde bir işlev işlevini uygular. 
- std::for_each_n() işlevi, std::for_each() işlevine benzer şekilde çalışır, ancak işlemin uygulanacağı öğe sayısı belirtilir. Bu, özellikle büyük aralıklarda sadece belirli bir sayıda öğe üzerinde işlem yapmak istediğinizde faydalıdır.

- std::for_each_n() işlevi, bir işlev nesnesi ve bir başlangıç konumu ve işlemin uygulanacak öğe sayısı verildiğinde, belirtilen sayıdaki öğeler için işlevi çağırır. İşlev nesnesi, her öğe için çağrılacak işlevi belirtir. İşlevin sözdizimi şu şekildedir:

```CPP
template <class InputIt, class Size, class UnaryFunction>
InputIt for_each_n(InputIt first, Size count, UnaryFunction f);

```

- Bu işlevin ilk parametresi, işlem başlangıç noktasını gösteren bir işaretçidir. İkinci parametre, işlem yapılacak öğe sayısını belirtir. Son parametre, aralıktaki her öğe için çağrılacak işlevi belirten bir işlev nesnesidir. İşlev, belirtilen sayıdaki öğeler için çağrılır ve son öğenin ardından işaretçi döndürülür.

- İşte bir örnek kod parçası, std::for_each_n() işlevinin nasıl kullanılabileceğini gösteriyor:

```CPP
#include <iostream>
#include <algorithm>
#include <vector>

void print_num(int num) {
  std::cout << num << " ";
}

int main() {
  std::vector<int> my_vec {1, 2, 3, 4, 5};

  std::for_each_n(my_vec.begin(), 3, print_num);

  return 0;
}

```
> Bu örnek kod, std::for_each_n() işlevinin kullanımını göstermektedir. std::vectorint türünde bir vektör oluşturuyoruz ve ilk üç öğeyi ekrana yazdırmak için print_num() işlevini kullanıyoruz. std::for_each_n() işlevi, print_num() işlevini ilk üç öğe için çağırır ve sonuç olarak 1 2 3 değerlerini ekrana yazdırır.

- Bu işlevin kullanımı, bir aralıktaki öğelerin belirli bir sayıda öğesine işlem yapmak istediğiniz durumlarda oldukça yaygındır. Örneğin, bir dosyadaki ilk 10 satırı okumak için kullanılabilir.

### count

- std::count() C++ algoritması, bir aralıktaki öğelerin belirli bir değere eşit olup olmadığını kontrol etmek için kullanılır. Bu algoritmanın amacı, belirli bir öğe sayısını bulmak istediğinizde kullanımı kolay bir seçenek sunmaktır.

- std::count() işlevi, bir aralık ve belirli bir değer verildiğinde, aralıktaki öğelerin kaçının belirtilen değere eşit olduğunu sayar. İşlevin sözdizimi şu şekildedir:

```CPP
template <class InputIt, class T>
typename iterator_traits<InputIt>::difference_type count(InputIt first, InputIt last, const T& value);

```

- Bu işlevin ilk iki parametresi, aralığın başlangıç ve sonunu gösteren işaretçilerdir. Son parametre, sayılacak öğelerin değeridir. İşlev, aralıktaki öğelerin kaçının belirtilen değere eşit olduğunu sayar ve sonuç olarak belirtilen değere eşit olan öğe sayısını döndürür.

- İşte bir örnek kod parçası, std::count() işlevinin nasıl kullanılabileceğini gösteriyor:

```CPP
#include <iostream>
#include <algorithm>
#include <vector>

int main() {
  std::vector<int> my_vec {1, 2, 2, 3, 2, 4, 2, 5};

  int count = std::count(my_vec.begin(), my_vec.end(), 2);

  std::cout << "Vektördeki 2 sayısı " << count << " kez geçiyor" << std::endl;

  return 0;
}

```

> Bu örnek kod, std::count() işlevinin kullanımını göstermektedir. std::vector int türünde bir vektör oluşturuyoruz ve vektördeki 2 sayısının kaç kez geçtiğini saymak için std::count() işlevini kullanıyoruz. std::count() işlevi, vektördeki 2 sayısının 4 kez geçtiğini sayar ve sonuç olarak 4 değerini döndürür.

- Bu işlevin kullanımı, bir aralıktaki öğelerin belirli bir değere eşit olup olmadığını kontrol etmek için oldukça yaygındır. Örneğin, bir kelime içinde belirli bir karakterin kaç kez geçtiğini saymak veya bir dosyadaki belirli bir kelime sayısını saymak için kullanılabilir.

### count_if

- std::count_if() C++ algoritması, bir aralıktaki öğelerin belirli bir özelliğe sahip olup olmadığını kontrol etmek için kullanılır. Bu algoritmanın amacı, belirli bir özelliğe sahip olan öğe sayısını bulmak istediğinizde kullanımı kolay bir seçenek sunmaktır.

- std::count_if() işlevi, bir aralık ve belirli bir özelliği kontrol eden bir işlev verildiğinde, aralıktaki öğelerin kaçının belirtilen özelliğe sahip olduğunu sayar. İşlevin sözdizimi şu şekildedir:

```CPP
template <class InputIt, class UnaryPredicate>
typename iterator_traits<InputIt>::difference_type count_if(InputIt first, InputIt last, UnaryPredicate p);

```

- Bu işlevin ilk iki parametresi, aralığın başlangıç ve sonunu gösteren işaretçilerdir. Son parametre, her öğe için çağrılacak bir işlev nesnesidir ve belirli bir özelliği kontrol eder. İşlev, aralıktaki öğelerin kaçının belirtilen özelliğe sahip olduğunu sayar ve sonuç olarak belirtilen özelliğe sahip olan öğe sayısını döndürür.

- İşte bir örnek kod parçası, std::count_if() işlevinin nasıl kullanılabileceğini gösteriyor:

```CPP
#include <iostream>
#include <algorithm>
#include <vector>

bool is_even(int num) {
  return num % 2 == 0;
}

int main() {
  std::vector<int> my_vec {1, 2, 3, 4, 5};

  int count = std::count_if(my_vec.begin(), my_vec.end(), is_even);

  std::cout << "Vektördeki çift sayıların sayısı: " << count << std::endl;

  return 0;
}

```

> Bu örnek kod, std::count_if() işlevinin kullanımını göstermektedir. std::vector int türünde bir vektör oluşturuyoruz ve vektördeki çift sayıların sayısını saymak için is_even() işlevini kullanıyoruz. std::count_if() işlevi, vektördeki çift sayıların sayısını sayar ve sonuç olarak 2 değerini döndürür.

- Bu işlevin kullanımı, bir aralıktaki öğelerin belirli bir özelliğe sahip olup olmadığını kontrol etmek için oldukça yaygındır. Örneğin, bir dosyadaki belirli bir kelimeyi içeren satırların sayısını saymak veya bir dosyadaki belirli bir karakterin sayısını saymak için kullanılabilir.























