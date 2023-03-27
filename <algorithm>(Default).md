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


# Ornek: (sort - reverse - *max_element - *min_element - accumulate)  

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

# Ornek (count - find)

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








