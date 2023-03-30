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
- **mismatch()** 
> iki aralık arasındaki ilk farklı öğeleri bulmak için kullanılır. Bu algoritmanın amacı, iki aralık arasındaki farklılıkları bulmak istediğinizde kullanımı kolay bir seçenek sunmaktır.
- **find()**
> C++ algoritması, bir aralıkta belirli bir öğenin varlığını kontrol etmek için kullanılır. Bu algoritmanın amacı, belirli bir öğenin varlığını kontrol etmek istediğinizde kullanımı kolay bir seçenek sunmaktır.
- **find_if()**
> işlevi, bir aralık ve belirli bir özelliğe sahip olan bir işlev nesnesi verildiğinde, aralıkta öğenin var olup olmadığını kontrol eder.
- **find_if_not()**
> belirli bir özelliğe sahip olmayan öğeleri aramak için kullanılır.
- **find_end()**
> bir aralıkta belirli bir alt aralığın son konumunu bulmak için kullanılır. Bu algoritmanın amacı, belirli bir alt aralığın varlığını kontrol etmek istediğinizde kullanımı kolay bir seçenek sunmaktır.
- **find_first_of()** 
> bir aralıkta belirli bir öğeler kümesinin ilk konumunu bulmak için kullanılır. Bu algoritmanın amacı, belirli bir öğeler kümesinin varlığını kontrol etmek istediğinizde kullanımı kolay bir seçenek sunmaktır.
- **adjacent_find()**
> bir aralıkta ardışık öğeler arasında bir özellik veya eşleşme aramak için kullanılır. Bu algoritmanın amacı, ardışık öğelerin varlığını kontrol etmek istediğinizde kullanımı kolay bir seçenek sunmaktır.
- **search()**
> bir aralıkta belirli bir alt aralığı aramak için kullanılır. Bu algoritmanın amacı, bir aralıkta alt aralığın varlığını kontrol etmek istediğinizde kullanımı kolay bir seçenek sunmaktır.
- **search_n()**
> bir aralıkta ardışık bir öğe dizisi aramak için kullanılır. Bu algoritmanın amacı, ardışık öğe dizisinin varlığını kontrol etmek istediğinizde kullanımı kolay bir seçenek sunmaktır.

# Modifying sequence operations

- **copy()**
> bir aralıktaki öğeleri başka bir aralığa kopyalamak için kullanılır. Bu algoritmanın amacı, bir aralıktaki öğeleri başka bir aralığa taşımak istediğinizde kullanımı kolay bir seçenek sunmaktır.
- **copy_if()**
> bir aralıktaki öğeleri belirli bir koşulu sağlayan öğeleri başka bir aralığa kopyalamak için kullanılır. Bu işlevin kullanımı, std::copy() işlevine benzerdir, ancak kopyalanacak öğeler için bir koşul belirtilir.
- **copy_n()**
> bir aralıktan belirli bir sayıda öğeyi başka bir aralığa kopyalamak için kullanılır. Bu algoritmanın amacı, bir aralıktan belirli bir sayıda öğe kopyalamak istediğinizde kullanımı kolay bir seçenek sunmaktır.
- copy_backward()
> bir aralıktaki öğeleri başka bir aralığa sondan başlayarak kopyalamak için kullanılır. Bu algoritmanın amacı, bir aralıktaki öğeleri sondan başlayarak başka bir aralığa taşımak istediğinizde kullanımı kolay bir seçenek sunmaktır.
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

# mismatch

- std::mismatch() C++ algoritması, iki aralık arasındaki ilk farklı öğeleri bulmak için kullanılır. Bu algoritmanın amacı, iki aralık arasındaki farklılıkları bulmak istediğinizde kullanımı kolay bir seçenek sunmaktır.

- std::mismatch() işlevi, iki aralık verildiğinde, aralıkların ilk farklı öğesinin konumunu döndürür. İşlevin sözdizimi şu şekildedir:

```CPP
template <class InputIt1, class InputIt2>
std::pair<InputIt1, InputIt2> mismatch(InputIt1 first1, InputIt1 last1, InputIt2 first2);

```
> Bu işlevin ilk iki parametresi, karşılaştırılan ilk aralığın başlangıç ve sonunu gösteren işaretçilerdir. Son parametre, karşılaştırılan ikinci aralığın başlangıç konumunu gösteren bir işaretçidir. İşlev, iki aralık arasında ilk farklı öğeyi bulduğunda, bir std::pair nesnesi döndürür ve bu nesnenin first elemanı ilk aralıktaki farklı öğenin konumunu, second elemanı ise ikinci aralıktaki farklı öğenin konumunu gösterir.

- İşte bir örnek kod parçası, std::mismatch() işlevinin nasıl kullanılabileceğini gösteriyor:

```CPP
#include <iostream>
#include <algorithm>
#include <vector>

int main() {
  std::vector<int> my_vec1 {1, 2, 3, 4, 5};
  std::vector<int> my_vec2 {1, 2, 3, 5, 4};

  auto mismatch_pair = std::mismatch(my_vec1.begin(), my_vec1.end(), my_vec2.begin());

  if (mismatch_pair.first != my_vec1.end()) {
    std::cout << "İlk farklı öğe: " << *mismatch_pair.first << " ve " << *mismatch_pair.second << std::endl;
  } else {
    std::cout << "Aralıklar eşleşiyor" << std::endl;
  }

  return 0;
}

```
> Bu örnek kod, std::mismatch() işlevinin kullanımını göstermektedir. İki std::vector  int türünde vektör oluşturuyoruz ve std::mismatch() işlevini kullanarak iki vektör arasındaki ilk farklı öğeyi buluyoruz. İlk vektördeki 5 ve ikinci vektördeki 4 öğeleri farklı olduğu için std::mismatch() işlevi bir std::pair nesnesi döndürür ve bu nesnenin first elemanı 5'in konumunu, second elemanı ise 4'ün konumunu gösterir.

- Bu işlevin kullanımı, iki aralık arasındaki farklılıkları kontrol etmek için oldukça yaygındır. Örneğin, iki dosya arasındaki farklılıkları bulmak veya iki veritabanı arasındaki farklılıkları kontrol etmek için kullanılabilir.

### find - find_if - find_if_not

- std::find() C++ algoritması, bir aralıkta belirli bir öğenin varlığını kontrol etmek için kullanılır. Bu algoritmanın amacı, belirli bir öğenin varlığını kontrol etmek istediğinizde kullanımı kolay bir seçenek sunmaktır.

- std::find() işlevi, bir aralık ve aranacak öğenin değeri verildiğinde, aralıkta öğenin var olup olmadığını kontrol eder. İşlevin sözdizimi şu şekildedir:

```CPP
template <class InputIt, class T>
InputIt find(InputIt first, InputIt last, const T& value);

```
- Bu işlevin ilk iki parametresi, aralığın başlangıç ve sonunu gösteren işaretçilerdir. Son parametre, aranacak öğenin değeridir. İşlev, aralıktaki öğeleri arar ve öğe bulunduğunda öğenin konumunu gösteren bir işaretçi döndürür. Öğe bulunamadığında ise son öğeyi gösteren bir işaretçi döndürülür.

- std::find_if() ve std::find_if_not() işlevleri, belirli bir özelliğe sahip olan veya sahip olmayan öğeleri aramak için kullanılır. std::find_if() işlevi, bir aralık ve belirli bir özelliğe sahip olan bir işlev nesnesi verildiğinde, aralıkta öğenin var olup olmadığını kontrol eder. std::find_if_not() işlevi ise, belirli bir özelliğe sahip olmayan öğeleri aramak için kullanılır.

- İşte örnek bir kod parçası, std::find() işlevinin nasıl kullanılabileceğini gösteriyor:

```CPP
#include <iostream>
#include <algorithm>
#include <vector>

int main() {
  std::vector<int> my_vec {1, 2, 3, 4, 5};

  auto it = std::find(my_vec.begin(), my_vec.end(), 3);

  if (it != my_vec.end()) {
    std::cout << "Öğe bulundu: " << *it << std::endl;
  } else {
    std::cout << "Öğe bulunamadı" << std::endl;
  }

  return 0;
}

```

> Bu örnek kod, std::find() işlevinin kullanımını göstermektedir. std::vector int türünde bir vektör oluşturuyoruz ve vektörde 3 sayısının olup olmadığını kontrol etmek için std::find() işlevini kullanıyoruz. std::find() işlevi, vektörde 3 sayısının var olduğunu tespit eder ve sonuç olarak 3 sayısının konumunu gösteren bir işaretçi döndürür.

- std::find_if() ve std::find_if_not() işlevlerinin kullanımı da benzerdir. İşlevin ilk iki parametresi aralık işaretçilerdir ve son parametre, bir işlev nesnesidir. İşlev nesnesi, belirli bir özelliğe sahip olan veya sahip olmayan öğeleri tanımlar. İşlev, aralıktaki öğeleri arar ve öğe bulunduğunda öğenin konumunu gösteren bir işaretçi döndürür. Öğe bulunamadığında ise son öğeyi gösteren bir işaretçi döndürülür.

- İşte örnek bir kod parçası, std::find_if() işlevinin nasıl kullanılabileceğini gösteriyor:

```CPP
#include <iostream>
#include <algorithm>
#include <vector>

bool is_even(int num) {
  return num % 2 == 0;
}

int main() {
  std::vector<int> my_vec {1, 3, 5, 7, 8};

  auto it = std::find_if(my_vec.begin(), my_vec.end(), is_even);

  if (it != my_vec.end()) {
    std::cout << "İlk çift sayı: " << *it << std::endl;
  } else {
    std::cout << "Çift sayı bulunamadı" << std::endl;
  }

  return 0;
}

```

> Bu örnek kod, std::find_if() işlevinin kullanımını göstermektedir. std::vector int türünde bir vektör oluşturuyoruz ve vektördeki ilk çift sayıyı bulmak için is_even() işlevini kullanıyoruz. std::find_if() işlevi, vektördeki ilk çift sayıyı tespit eder ve sonuç olarak çift sayının konumunu gösteren bir işaretçi döndürür.

- std::find_if_not() işlevinin kullanımı da benzerdir, ancak belirli bir özelliğe sahip olmayan öğeleri aramak için kullanılır.

- Bu işlevlerin kullanımı, bir aralıkta belirli bir öğenin varlığını veya belirli bir özelliğe sahip olan veya sahip olmayan öğeleri bulmak için oldukça yaygındır. Örneğin, bir kelime içinde belirli bir karakterin var olup olmadığını kontrol etmek veya bir dosyada belirli bir kelimeyi içeren satırı bulmak için kullanılabilir.

### find_end

- std::find_end() C++ algoritması, bir aralıkta belirli bir alt aralığın son konumunu bulmak için kullanılır. Bu algoritmanın amacı, belirli bir alt aralığın varlığını kontrol etmek istediğinizde kullanımı kolay bir seçenek sunmaktır.

- std::find_end() işlevi, birinci aralık ve ikinci alt aralık verildiğinde, ikinci alt aralığın son konumunu bulur. İşlevin sözdizimi şu şekildedir:

```CPP
template <class ForwardIt1, class ForwardIt2>
ForwardIt1 find_end(ForwardIt1 first1, ForwardIt1 last1, ForwardIt2 first2, ForwardIt2 last2);

```

- Bu işlevin ilk iki parametresi, aralığın başlangıç ve sonunu gösteren işaretçilerdir. Son iki parametre ise alt aralığın başlangıç ve sonunu gösteren işaretçilerdir. İşlev, ilk aralıkta ikinci alt aralığın son konumunu bulduğunda, öğenin konumunu gösteren bir işaretçi döndürür. Alt aralık bulunamadığında ise son öğeyi gösteren bir işaretçi döndürülür.

- İşte örnek bir kod parçası, std::find_end() işlevinin nasıl kullanılabileceğini gösteriyor:

```CPP
#include <iostream>
#include <algorithm>
#include <vector>

int main() {
  std::vector<int> my_vec {1, 2, 3, 4, 5, 1, 2, 3};

  std::vector<int> sub_vec {1, 2, 3};

  auto it = std::find_end(my_vec.begin(), my_vec.end(), sub_vec.begin(), sub_vec.end());

  if (it != my_vec.end()) {
    std::cout << "Alt aralık son konumu: " << std::distance(my_vec.begin(), it) << std::endl;
  } else {
    std::cout << "Alt aralık bulunamadı" << std::endl;
  }

  return 0;
}

```
> Bu örnek kod, std::find_end() işlevinin kullanımını göstermektedir. std::vector int türünde bir vektör oluşturuyoruz ve vektördeki alt aralığın son konumunu bulmak için std::find_end() işlevini kullanıyoruz. İkinci vektör, alt aralığı temsil eder. std::find_end() işlevi, vektördeki alt aralığın son konumunu tespit eder ve sonuç olarak alt aralığın son konumunu gösteren bir işaretçi döndürür.

- Bu işlevin kullanımı, bir aralıkta belirli bir alt aralığın son konumunu bulmak için oldukça yaygındır. Örneğin, bir dosyadaki belirli bir kelimeyi içeren son satırın konumunu bulmak veya bir veritabanındaki belirli bir kaydın son konumunu bulmak için kullanılabilir.

### find_first_of

- std::find_first_of() C++ algoritması, bir aralıkta belirli bir öğeler kümesinin ilk konumunu bulmak için kullanılır. Bu algoritmanın amacı, belirli bir öğeler kümesinin varlığını kontrol etmek istediğinizde kullanımı kolay bir seçenek sunmaktır.

- std::find_first_of() işlevi, birinci aralık ve ikinci öğeler kümesi verildiğinde, ikinci öğeler kümesindeki herhangi bir öğenin ilk konumunu bulur. İşlevin sözdizimi şu şekildedir:

```CPP
template <class InputIt, class ForwardIt>
InputIt find_first_of(InputIt first1, InputIt last1, ForwardIt first2, ForwardIt last2);

```
- Bu işlevin ilk iki parametresi, aralığın başlangıç ve sonunu gösteren işaretçilerdir. Son iki parametre, öğeler kümesinin başlangıç ve sonunu gösteren işaretçilerdir. İşlev, ilk aralıkta ikinci öğeler kümesindeki herhangi bir öğenin ilk konumunu bulduğunda, öğenin konumunu gösteren bir işaretçi döndürür. Öğeler kümesindeki öğeler aranırken, her bir öğe için arama işlemi aralıktaki öğelerin sırasıyla taranmasıyla gerçekleştirilir. Eğer hiçbir öğe bulunamazsa son öğeyi gösteren bir işaretçi döndürülür.

- İşte örnek bir kod parçası, std::find_first_of() işlevinin nasıl kullanılabileceğini gösteriyor:

```CPP
#include <iostream>
#include <algorithm>
#include <vector>

int main() {
  std::vector<int> my_vec {1, 2, 3, 4, 5};

  std::vector<int> search_vec {4, 5, 6};

  auto it = std::find_first_of(my_vec.begin(), my_vec.end(), search_vec.begin(), search_vec.end());

  if (it != my_vec.end()) {
    std::cout << "İlk eşleşen öğe: " << *it << std::endl;
  } else {
    std::cout << "Eşleşen öğe bulunamadı" << std::endl;
  }

  return 0;
}

```
> Bu örnek kod, std::find_first_of() işlevinin kullanımını göstermektedir. std::vector int  türünde bir vektör oluşturuyoruz ve vektördeki belirli bir öğeler kümesinin ilk konumunu bulmak için std::find_first_of() işlevini kullanıyoruz. İkinci vektör, öğeler kümesini temsil eder. std::find_first_of() işlevi, vektördeki öğeler kümesindeki ilk eşleşen öğeyi tespit eder ve sonuç olarak öğenin konumunu gösteren bir işaretçi döndürür.

- Bu işlevin kullanımı, bir aralıkta belirli bir öğeler kümesinin varlığını kontrol etmek veya belirli bir öğeler kümesindeki herhangi bir öğenin konumunu bulmak için oldukça yaygındır. Örneğin, bir kelime içinde belirli bir karakter kümesinin ilk konumunu bulmak veya bir veritabanında belirli bir kayıttaki belirli bir alanın değeriyle eşleşen herhangi bir kaydın konumunu bulmak için kullanılabilir.

### adjacent_find

- std::adjacent_find() C++ algoritması, bir aralıkta ardışık öğeler arasında bir özellik veya eşleşme aramak için kullanılır. Bu algoritmanın amacı, ardışık öğelerin varlığını kontrol etmek istediğinizde kullanımı kolay bir seçenek sunmaktır.

- std::adjacent_find() işlevi, birinci ve ikinci parametre olarak aralığın başlangıç ve sonunu gösteren işaretçileri alır. İşlev, ardışık öğeler arasında belirli bir özellik veya eşleşme bulduğunda, öğelerin konumunu gösteren bir işaretçi döndürür. Eşleşme bulunamazsa son öğeyi gösteren bir işaretçi döndürülür.

- İşte örnek bir kod parçası, std::adjacent_find() işlevinin nasıl kullanılabileceğini gösteriyor:

```CPP
#include <iostream>
#include <algorithm>
#include <vector>

bool is_consecutive(int x, int y) {
  return y - x == 1;
}

int main() {
  std::vector<int> my_vec {1, 2, 3, 5, 6, 7, 9};

  auto it = std::adjacent_find(my_vec.begin(), my_vec.end(), is_consecutive);

  if (it != my_vec.end()) {
    std::cout << "Ardışık öğelerin ilk konumu: " << std::distance(my_vec.begin(), it) << std::endl;
  } else {
    std::cout << "Ardışık öğeler bulunamadı" << std::endl;
  }

  return 0;
}

```

> Bu örnek kod, std::adjacent_find() işlevinin kullanımını göstermektedir. std::vector int türünde bir vektör oluşturuyoruz ve vektördeki ardışık öğelerin ilk konumunu bulmak için std::adjacent_find() işlevini kullanıyoruz. İşlev, vektörde ardışık olan 1 ve 2 öğelerini tespit eder ve sonuç olarak öğelerin konumunu gösteren bir işaretçi döndürür.

- Bu işlevin kullanımı, bir aralıkta ardışık öğelerin varlığını kontrol etmek için oldukça yaygındır. Örneğin, bir kelime içinde belirli bir karakter dizisi aramak veya bir veritabanındaki ardışık kayıtları bulmak için kullanılabilir.

### search()
- std::search() C++ algoritması, bir aralıkta belirli bir alt aralığı aramak için kullanılır. Bu algoritmanın amacı, bir aralıkta alt aralığın varlığını kontrol etmek istediğinizde kullanımı kolay bir seçenek sunmaktır.

- std::search() işlevi, birinci ve ikinci parametre olarak aralığın başlangıç ve sonunu gösteren işaretçileri alır. Üçüncü ve dördüncü parametreler, alt aralığın başlangıç ve sonunu gösteren işaretçilerdir. İşlev, alt aralığın ilk konumunu bulduğunda, öğenin konumunu gösteren bir işaretçi döndürür. Alt aralık bulunamazsa son öğeyi gösteren bir işaretçi döndürülür.

- İşte örnek bir kod parçası, std::search() işlevinin nasıl kullanılabileceğini gösteriyor:

```CPP
#include <iostream>
#include <algorithm>
#include <vector>

int main() {
  std::vector<int> my_vec {1, 2, 3, 4, 5, 1, 2, 3};

  std::vector<int> sub_vec {1, 2, 3};

  auto it = std::search(my_vec.begin(), my_vec.end(), sub_vec.begin(), sub_vec.end());

  if (it != my_vec.end()) {
    std::cout << "Alt aralık ilk konumu: " << std::distance(my_vec.begin(), it) << std::endl;
  } else {
    std::cout << "Alt aralık bulunamadı" << std::endl;
  }

  return 0;
}

```
> Bu örnek kod, std::search() işlevinin kullanımını göstermektedir. std::vector int türünde bir vektör oluşturuyoruz ve vektörde belirli bir alt aralığı aramak için std::search() işlevini kullanıyoruz. İkinci vektör, alt aralığı temsil eder. std::search() işlevi, vektördeki alt aralığın ilk konumunu tespit eder ve sonuç olarak alt aralığın ilk konumunu gösteren bir işaretçi döndürür.

- Bu işlevin kullanımı, bir aralıkta belirli bir alt aralığın varlığını kontrol etmek veya belirli bir alt aralığı bulmak için oldukça yaygındır. Örneğin, bir dosyada belirli bir kelimeyi içeren satırı bulmak veya bir veritabanında belirli bir kaydı bulmak için kullanılabilir.

### search_n

- std::search_n() C++ algoritması, bir aralıkta ardışık bir öğe dizisi aramak için kullanılır. Bu algoritmanın amacı, ardışık öğe dizisinin varlığını kontrol etmek istediğinizde kullanımı kolay bir seçenek sunmaktır.

- std::search_n() işlevi, birinci ve ikinci parametre olarak aralığın başlangıcını ve sonunu gösteren işaretçileri alır. Üçüncü parametre, ardışık öğe dizisi için gereken öğe sayısıdır. Dördüncü parametre, aranacak öğe değeridir. İşlev, ardışık öğe dizisini bulduğunda, öğelerin konumunu gösteren bir işaretçi döndürür. Ardışık öğe dizisi bulunamazsa son öğeyi gösteren bir işaretçi döndürülür.

- İşte örnek bir kod parçası, std::search_n() işlevinin nasıl kullanılabileceğini gösteriyor:

```CPP
#include <iostream>
#include <algorithm>
#include <vector>

int main() {
  std::vector<int> my_vec {1, 2, 3, 1, 2, 3, 4, 5};

  int count = 2;
  int value = 3;

  auto it = std::search_n(my_vec.begin(), my_vec.end(), count, value);

  if (it != my_vec.end()) {
    std::cout << "Ardışık " << count << " öğe bulundu, ilk konum: " << std::distance(my_vec.begin(), it) << std::endl;
  } else {
    std::cout << "Ardışık öğeler bulunamadı" << std::endl;
  }

  return 0;
}

```

> Bu örnek kod, std::search_n() işlevinin kullanımını göstermektedir. std::vector int türünde bir vektör oluşturuyoruz ve vektörde ardışık bir öğe dizisini bulmak için std::search_n() işlevini kullanıyoruz. count değişkeni, aranacak öğe sayısını ve value değişkeni, aranacak öğe değerini temsil eder. std::search_n() işlevi, vektörde ardışık olan 3 öğelerinin ilk konumunu tespit eder ve sonuç olarak öğelerin konumunu gösteren bir işaretçi döndürür.

- Bu işlevin kullanımı, bir aralıkta ardışık öğelerin varlığını kontrol etmek için oldukça yaygındır. Örneğin, bir dosyada belirli bir karakter dizisi aramak veya bir veritabanında ardışık kayıtları bulmak için kullanılabilir.

### copy

- std::copy() C++ algoritması, bir aralıktaki öğeleri başka bir aralığa kopyalamak için kullanılır. Bu algoritmanın amacı, bir aralıktaki öğeleri başka bir aralığa taşımak istediğinizde kullanımı kolay bir seçenek sunmaktır.

- std::copy() işlevi, birinci ve ikinci parametre olarak kopyalanacak aralığın başlangıcını ve sonunu gösteren işaretçileri alır. Üçüncü parametre, kopyalanacak aralığın başlangıcını gösteren işaretçidir. İşlev, kopyalama işlemini gerçekleştirdikten sonra son konumu gösteren bir işaretçi döndürür.

- İşte örnek bir kod parçası, std::copy() işlevinin nasıl kullanılabileceğini gösteriyor:

```CPP
#include <iostream>
#include <algorithm>
#include <vector>

int main() {
  std::vector<int> src {1, 2, 3, 4, 5};
  std::vector<int> dest(5);

  std::copy(src.begin(), src.end(), dest.begin());

  for (auto it = dest.begin(); it != dest.end(); ++it) {
    std::cout << *it << " ";
  }

  return 0;
}

```

> Bu örnek kod, std::copy() işlevinin kullanımını göstermektedir. İlk olarak, std::vector int türünde src ve dest isimli iki vektör oluşturuyoruz. Ardından, std::copy() işlevini kullanarak src vektöründeki öğeleri dest vektörüne kopyalıyoruz. Son olarak, dest vektöründeki öğeleri yazdırıyoruz.

### copy_if()

- std::copy_if() işlevi, bir aralıktaki öğeleri belirli bir koşulu sağlayan öğeleri başka bir aralığa kopyalamak için kullanılır. Bu işlevin kullanımı, std::copy() işlevine benzerdir, ancak kopyalanacak öğeler için bir koşul belirtilir.

std::copy_if() işlevi, birinci ve ikinci parametre olarak kopyalanacak aralığın başlangıcını ve sonunu gösteren işaretçileri alır. Üçüncü parametre, kopyalanacak aralığın başlangıcını gösteren işaretçidir. Dördüncü parametre, kopyalama koşulunu sağlayan bir işlev veya lambda işlevi olabilir. İşlev, kopyalama işlemini gerçekleştirdikten sonra son konumu gösteren bir işaretçi döndürür.

İşte örnek bir kod parçası, std::copy_if() işlevinin nasıl kullanılabileceğini gösteriyor:

```CPP
#include <iostream>
#include <algorithm>
#include <vector>

bool is_even(int x) {
  return x % 2 == 0;
}

int main() {
  std::vector<int> src {1, 2, 3, 4, 5};
  std::vector<int> dest;

  std::copy_if(src.begin(), src.end(), std::back_inserter(dest), is_even);

  for (auto it = dest.begin(); it != dest.end(); ++it) {
    std::cout << *it << " ";
  }

  return 0;
}

```

> Bu örnek kod, std::copy_if() işlevinin kullanımını göstermektedir. İlk olarak, std::vector int  türünde src ve dest isimli iki vektör oluşturuyoruz. Ardından, std::copy_if() işlevini kullanarak src vektöründeki çift sayıları dest vektörüne kopyalıyoruz. Son olarak, dest vektöründeki öğeleri yazdırıyoruz.

- Bu işlevin kullanımı, bir aralıktaki öğeleri belirli bir koşulu sağlayan öğeleri seçmek için oldukça yaygındır. Örneğin, bir veritabanından belirli bir koşulu sağlayan kayıtları seçmek için kullanılabilir.

### copy_n

- std::copy_n() C++ algoritması, bir aralıktan belirli bir sayıda öğeyi başka bir aralığa kopyalamak için kullanılır. Bu algoritmanın amacı, bir aralıktan belirli bir sayıda öğe kopyalamak istediğinizde kullanımı kolay bir seçenek sunmaktır.

- std::copy_n() işlevi, birinci parametre olarak kopyalanacak aralığın başlangıcını gösteren bir işaretçi alır. İkinci parametre, kopyalanacak öğe sayısını belirten bir tamsayıdır. Üçüncü parametre, kopyalanacak öğelerin başlangıcını gösteren işaretçidir. Dördüncü parametre, kopyalama işleminin yapılacağı hedefin başlangıcını gösteren işaretçidir. İşlev, kopyalama işlemini gerçekleştirdikten sonra son konumu gösteren bir işaretçi döndürür.

- İşte örnek bir kod parçası, std::copy_n() işlevinin nasıl kullanılabileceğini gösteriyor:

```CPP
#include <iostream>
#include <algorithm>
#include <vector>

int main() {
  std::vector<int> src {1, 2, 3, 4, 5};
  std::vector<int> dest(3);

  std::copy_n(src.begin(), 3, dest.begin());

  for (auto it = dest.begin(); it != dest.end(); ++it) {
    std::cout << *it << " ";
  }

  return 0;
}

```
> Bu örnek kod, std::copy_n() işlevinin kullanımını göstermektedir. İlk olarak, std::vector int  türünde src ve dest isimli iki vektör oluşturuyoruz. Ardından, std::copy_n() işlevini kullanarak src vektöründen ilk üç öğeyi dest vektörüne kopyalıyoruz. Son olarak, dest vektöründeki öğeleri yazdırıyoruz.

- Bu işlevin kullanımı, bir aralıktan belirli bir sayıda öğe kopyalamak için oldukça yaygındır. Örneğin, bir dosyadan belirli bir sayıda karakter kopyalamak veya bir veritabanından belirli bir sayıda kayıt kopyalamak için kullanılabilir.

### copy_backward

- std::copy_backward() C++ algoritması, bir aralıktaki öğeleri başka bir aralığa sondan başlayarak kopyalamak için kullanılır. Bu algoritmanın amacı, bir aralıktaki öğeleri sondan başlayarak başka bir aralığa taşımak istediğinizde kullanımı kolay bir seçenek sunmaktır.

- std::copy_backward() işlevi, birinci ve ikinci parametre olarak kopyalanacak aralığın başlangıcını ve sonunu gösteren işaretçileri alır. Üçüncü parametre, kopyalanacak aralığın sonunu gösteren işaretçidir. Dördüncü parametre, kopyalama işleminin yapılacağı hedefin sonunu gösteren işaretçidir. İşlev, kopyalama işlemini gerçekleştirdikten sonra son konumu gösteren bir işaretçi döndürür.

- İşte örnek bir kod parçası, std::copy_backward() işlevinin nasıl kullanılabileceğini gösteriyor:

```CPP
#include <iostream>
#include <algorithm>
#include <vector>

int main() {
  std::vector<int> src {1, 2, 3, 4, 5};
  std::vector<int> dest(src.size());

  std::copy_backward(src.begin(), src.end(), dest.end());

  for (auto it = dest.begin(); it != dest.end(); ++it) {
    std::cout << *it << " ";
  }

  return 0;
}

```

> Bu örnek kod, std::copy_backward() işlevinin kullanımını göstermektedir. İlk olarak, std::vector<int> türünde src ve dest isimli iki vektör oluşturuyoruz. Ardından, std::copy_backward() işlevini kullanarak src vektöründeki öğeleri sondan başlayarak dest vektörüne kopyalıyoruz. Son olarak, dest vektöründeki öğeleri yazdırıyoruz.

- Bu işlevin kullanımı, bir aralıktaki öğeleri sondan başlayarak başka bir aralığa taşımak için oldukça yaygındır. Örneğin, bir dosyada sondan başlayarak belirli bir karakter dizisi aramak veya bir veritabanında sondan başlayarak belirli bir sayıda kayıtları kopyalamak için kullanılabilir.























































