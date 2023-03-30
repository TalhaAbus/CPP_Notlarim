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

- all_of 
- any_of
- none_of
- for_each
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

- std::all_of(first, last, pred): aralıktaki tüm öğelerin pred işlevi tarafından belirtilen özelliğe sahip olup olmadığını kontrol eder. first ve last aralığın başlangıç ve sonunu gösteren işaretçilerdir, pred ise kontrol edilecek özelliği belirten bir işlev nesnesidir.
- std::any_of(first, last, pred): aralıktaki en az bir öğenin pred işlevi tarafından belirtilen özelliğe sahip olup olmadığını kontrol eder.
- std::none_of(first, last, pred): aralıktaki hiçbir öğenin pred işlevi tarafından belirtilen özelliğe sahip olup olmadığını kontrol eder.

- Bu işlevler C++11'de tanıtılmıştır ve C++17'de C++ aralık ifadeleri (std::ranges) için de tanıtılmıştır.

- İşte bir örnek kod parçası, bu işlevlerin nasıl kullanıldığını gösteriyor: 











































# sort - reverse - max_element - min_element - accumulate 

```CPP
#include <iostream>
#include <algorithm>
#include <vector>
#include <numeric>

using namespace std;

int main()
{
	int arr[] = { 10,20,5,23,42,15 };
	int numberof_members = sizeof(arr) / sizeof(arr[0]);

	vector<int> vect(arr , arr+numberof_members);

	for (auto element : vect)
		cout << element << " ";

	cout << "\n";

	sort(vect.begin(), vect.end());

	cout << "vector after sorting is:\n";
	for (auto element : vect)
		cout << element << " ";
	cout << "\n";


	cout << "vector after descending order:\n";

	sort(vect.begin(), vect.end(), greater<int>());

	for (auto element : vect)
		cout << element << " ";
	
	cout << "\n";

	reverse(vect.begin(), vect.end());
	
	for (auto element : vect)
		cout << element << " ";
	cout << "\n";


	cout << "max element of vector is:\n";
	cout << *max_element(vect.begin(), vect.end());

	cout << "\n";


	cout << "min element of vector is:\n";
	cout << *min_element(vect.begin(), vect.end());

	cout << "\n";

	cout << "summation of vector is:\n";
	cout << accumulate(vect.begin(), vect.end(), 0);

	cout << "\n";

	cout << "summation of vector is:\n";
	cout << accumulate(vect.begin(), vect.end(), 10);

}
```

# count - find

```CPP
#include <iostream>
#include <algorithm>
#include <vector>
#include <numeric>

using namespace std;

int main()
{
	int arr[] = { 10,20,5,23,20,42,15 };
	int numberof_members = sizeof(arr) / sizeof(arr[0]);

	vector<int> vect(arr , arr+numberof_members);

	cout << "occurrences of 20 in vect:  ";
	cout << count(vect.begin(), vect.end(), 20);

	cout << "\n";

	auto location = find(vect.begin(), vect.end(), 5);

	if (location != vect.end())
	{
		cout << "element found";
	}
	else
		cout << "element not found";

}
```

# binary_search - lower_bound - upper_bound

```CPP
#include <iostream>
#include <algorithm>
#include <vector>

using namespace std;

int main()
{
	//init the vector:

	int arr[] = { 5,10,15,20,20,23,42,45 };
	int numberof_elements = sizeof(arr) / sizeof(arr[0]);

	vector<int> vect(arr, arr + numberof_elements);



	sort(vect.begin(), vect.end());

	cout << binary_search(vect.begin(), vect.end(), 20) << "\n";

	auto low = lower_bound(vect.begin(), vect.end(), 20);
	auto upper = upper_bound(vect.begin(), vect.end(), 20);

	cout << low - vect.begin() << "\n";
	cout << upper - vect.begin() << "\n";

}
```
- std::binary_search ve std::find fonksiyonları, bir sıralı aralık içinde bir öğe arama işlemleri için kullanılır.Ancak aralarındaki fark, arama işleminin nasıl gerçekleştirildiğidir.

- std::binary_search fonksiyonu, sıralı bir aralıkta bir öğenin var olup olmadığını kontrol etmek için kullanılır.Fonksiyon, bir aralık ve aranacak öğe alır ve aralıkta öğenin olup olmadığını kontrol eder.Aralık sıralı olduğu için, arama işlemi hızlı bir şekilde gerçekleştirilebilir.Fonksiyon, aranan öğenin var olması durumunda true, yoksa false değeri döndürür.

- std::find fonksiyonu ise, bir aralıkta belirtilen öğenin var olup olmadığını kontrol eder ve öğenin konumunu(bir iterator) döndürür.Aralık sıralı olmak zorunda değildir, yani bu fonksiyon sıralama gerektirmez.Bu fonksiyon da arama işlemi gerçekleştirir ancak lineer zaman karmaşıklığına sahiptir, yani büyük aralıklarda performans sorunlarına neden olabilir.

- Özet olarak, std::binary_search bir sıralı aralıkta bir öğenin var olup olmadığını kontrol etmek için kullanılırken std::find fonksiyonu bir aralıkta belirtilen öğeyi bulmak için kullanılır ve aralığın sıralı olması gerekli değildir.

- std::binary_search() işlevi, sıralanmış bir aralıkta belirli bir değerin var olup olmadığını belirlemek için kullanılır.Fonksiyon, arama işlemini gerçekleştirmeden önce aralığı sıralamaz.Bu nedenle, sıralanmamış bir aralık üzerinde std::binary_search() işlevini çağırdığınızda, sonuç beklenmeyen bir şekilde yanlış olabilir.

- Bununla birlikte, std::binary_search() işlevi, aralık öğelerinin sıralanmasını gerektirir.Eğer aralık sıralanmamışsa, işlev yanlış sonuçlar verebilir.Bu nedenle, std::binary_search() işlevini kullanmadan önce, aralığı sıralamak için önce std::sort() işlevini çağırmak gerekir

# erase - unique

```CPP
// C++ program to demonstrate working
// of erase
#include <algorithm>
#include <iostream>
#include <vector>
using namespace std;

int main()
{
    // Initializing vector with array values
    int arr[] = { 5, 10, 15, 20, 20, 23, 42, 45 };
    int n = sizeof(arr) / sizeof(arr[0]);
    vector<int> vect(arr, arr + n);

    cout << "Given Vector is:\n";
    for (int i = 0; i < n; i++)
        cout << vect[i] << " ";

    vect.erase(find(vect.begin(), vect.end(), 10));
    cout << "\nVector after erasing element:\n";
    for (int i = 0; i < vect.size(); i++)
        cout << vect[i] << " ";

    vect.erase(unique(vect.begin(), vect.end()),
        vect.end());
    cout << "\nVector after removing duplicates:\n";
    for (int i = 0; i < vect.size(); i++)
        cout << vect[i] << " ";

    return 0;
}
```

# next_permutation - prev_permutation

```CPP
// C++ program to demonstrate working
// of next_permutation()
// and prev_permutation()
#include <algorithm>
#include <iostream>
#include <vector>
using namespace std;

int main()
{
	// Initializing vector with array values
	int arr[] = { 5, 10, 15, 20, 20, 23, 42, 45 };
	int n = sizeof(arr) / sizeof(arr[0]);
	vector<int> vect(arr, arr + n);

	cout << "Given Vector is:\n";
	for (int i = 0; i < n; i++)
		cout << vect[i] << " ";

	for (int i = 0; i <= 5; i++)
	{
		// modifies vector to its next permutation order
		next_permutation(vect.begin(), vect.end());
		cout << "\nVector after performing next permutation:\n";
		for (int i = 0; i < n; i++)
			cout << vect[i] << " ";
	}

	cout << "\n\n\n";

	for (int i = 0; i <= 5; i++)
	{
		// modifies vector to its next permutation order
		prev_permutation(vect.begin(), vect.end());
		cout << "\nVector after performing next permutation:\n";
		for (int i = 0; i < n; i++)
			cout << vect[i] << " ";
	}

	return 0;
}


```

#  distance

```CPP
#include <algorithm>
#include <iostream>
#include <vector>
using namespace std;

int main()
{
	int arr[] = { 5,7,3,8,5,16,5,87 };
	int size = sizeof(arr) / sizeof(arr[0]);

	vector <int> vect(arr, arr + size);

	cout << distance(min_element(vect.begin(),vect.end()),
		max_element(vect.begin(), vect.end()));
}
```













