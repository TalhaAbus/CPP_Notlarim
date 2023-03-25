- <memory_resource> başlık dosyası, özelleştirilebilir bellek yönetimi için araçlar sağlar. Özellikle, C++17'te tanıtılan bu başlık dosyası, bellek tahsisi işlemlerinde performans ve özelleştirme açısından daha iyi esneklik sunar.

- <memory_resource> başlık dosyası, aşağıdaki sınıfları içerir:

- std::pmr::memory_resource: Bu soyut sınıf, bellek tahsis ve serbest bırakma işlemlerini gerçekleştirir. std::pmr::new_delete_resource gibi öntanımlı işlevler sağlar, ancak bu işlevler, özelleştirilmiş bellek yönetimi için yerine getirilebilir.

- std::pmr::polymorphic_allocator: Bu sınıf, memory_resource sınıfını kullanan sınıflar için özelleştirilmiş bir tahsisatçıdır. Bu, örneğin std::vector'ün bellek tahsisi işlemlerini özelleştirmek için kullanılabilir.

- std::pmr::monotonic_buffer_resource: Bu sınıf, bir bellek havuzunu yönetir. Havuzun bellek alanı, oluşturulurken belirtilen bellek bloğuna tahsis edilir ve tahsis edilen bellek bloğu boyutu değiştirilemez.

- std::pmr::synchronized_pool_resource: Bu sınıf, bir dizi bellek havuzunu yönetir. Havuzların her biri, verilen boyut aralığındaki nesneler için kullanılır.

- Bu başlık dosyasının kullanıldığı senaryolar, özelleştirilmiş bellek yönetimi gerektiren uygulamalardır. Örneğin, özelleştirilmiş bellek havuzları kullanarak bellek yönetimini optimize edebilirsiniz. Ayrıca, belirli bir bellek havuzunu paylaşan birden fazla iş parçacığı tarafından erişilen nesnelerin bellek tahsisini yönetmek için de kullanılabilir.

- Aşağıda örnek bir kod parçası verilmiştir. Bu kod parçasında pmr::polymorphic_allocator sınıfı kullanılarak bellek yönetimi yapılmaktadır. Önce, pmr::new_delete_resource() ile bir polymorphic memory resource oluşturulur. Daha sonra, bu resource kullanılarak bir pmr::monotonic_buffer_resource nesnesi yaratılır. Bu nesne, bir hafıza havuzu olarak davranır ve içindeki bellek blokları monotonik olarak büyür. Son olarak, pmr::vector sınıfı kullanılarak bu hafıza havuzunda öğeler saklanır.

```CPP

#include <iostream>
#include <vector>
#include <memory_resource>

int main() {
  // create a polymorphic memory resource
  auto my_resource = std::pmr::new_delete_resource();
  
  // create a memory pool with the polymorphic resource
  std::pmr::monotonic_buffer_resource pool(1024, my_resource);

  // create a vector with the memory pool
  std::pmr::vector<int> v(&pool);
  
  // add some elements to the vector
  for (int i = 0; i < 10; ++i) {
    v.push_back(i);
  }

  // print the elements of the vector
  for (auto i : v) {
    std::cout << i << " ";
  }
  std::cout << std::endl;

  return 0;
}

```

- Bu örnekte, önce pmr::new_delete_resource() kullanılarak bir polymorphic memory resource oluşturulmuştur. Daha sonra, pmr::monotonic_buffer_resource sınıfı kullanılarak 1024 byte boyutunda bir hafıza havuzu yaratılmıştır. Son olarak, pmr::vector sınıfı kullanılarak bu hafıza havuzunda öğeler saklanmıştır. pmr::vector sınıfı, standart std::vector sınıfına benzer şekilde davranır, ancak öğelerin saklandığı bellek havuzu, pmr::monotonic_buffer_resource sınıfının yönettiği bellek havuzudur.

# ne zaman bu kaynak dosyasina ihtiyac duyarim 

- <memory_resource> başlık dosyasına ihtiyaç duyduğunuz durumlar, bellek yönetimini özelleştirmek istediğiniz zamanlardır. Örneğin, özel bellek yönetimi gerektiren uygulamalar geliştirirken bu başlık dosyasını kullanabilirsiniz. Böylece bellek yönetimi işlemlerinde özelleştirilmiş bir davranış elde edebilirsiniz.

- <memory_resource> başlık dosyası, STL konteynerlerinde bellek yönetimini özelleştirmek için de kullanılabilir. Bu sayede farklı bellek yönetimi stratejileri uygulayarak, performans ve verimlilik açısından daha iyi sonuçlar elde edebilirsiniz.

# bellek yonetimini ozellestirmek ne demek bir ornek ver

- Bellek yönetimini özelleştirmek, programın ihtiyacına göre bellek yönetimini uyarlamak anlamına gelir. Bu genellikle, standart bellek tahsis işlemlerinin program ihtiyaçlarına tam olarak uygun olmadığı durumlarda kullanılır. Örneğin, bir programın büyük miktarda bellek ihtiyacı varsa ve bu bellek, standart bellek tahsis yöntemleriyle yeterince verimli bir şekilde tahsis edilemiyorsa, özel bellek tahsis işlevleri kullanılabilir.

- Bir örnek olarak, özel bir bellek havuzu kullanarak bellek tahsisini özelleştirmek verilebilir. Bu, programın bellek ihtiyacına göre dinamik olarak boyutlandırılabilen bir bellek havuzu sağlar ve standart bellek tahsis yöntemlerine kıyasla daha verimli bir bellek kullanımı sağlar.

- Örneğin, aşağıdaki örnek bir özel bellek havuzu kullanarak bellek yönetimini özelleştirir:

```CPP
#include <memory_resource>
#include <vector>
#include <iostream>

int main() {
    // Özel bellek havuzu oluştur
    std::pmr::monotonic_buffer_resource pool{1024};

    // Özel bellek havuzunu kullanan bir std::vector oluştur
    std::pmr::vector<int> vec{&pool};

    // Bellek havuzunu kullanarak std::vector'e elemanlar ekle
    for (int i = 0; i < 10; ++i) {
        vec.push_back(i);
    }

    // std::vector'ün elemanlarını yazdır
    for (const auto& elem : vec) {
        std::cout << elem << ' ';
    }

    return 0;
}

```
- Bu örnek, monotonic_buffer_resource sınıfını kullanarak bir özel bellek havuzu oluşturur. Daha sonra, pmr::vector sınıfını kullanarak bu bellek havuzunu kullanan bir std::vector oluşturur. Bellek havuzunu kullanarak std::vector'e elemanlar ekler ve son olarak std::vector'ün elemanlarını yazdırır. Bu örnekte, özel bellek tahsis yöntemlerinin kullanımı, daha verimli bellek yönetimi sağlar.


















































