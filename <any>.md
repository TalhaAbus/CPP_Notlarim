- <any> başlık dosyası, değişkenlerin türü bilinmeden depolanmasına ve yönetilmesine olanak tanıyan bir sınıf şablonu olan std::any sınıfını sağlar.

- std::any sınıfı, herhangi bir türe sahip bir nesne depolamak için kullanılabilir ve daha sonra depolanan nesneye erişmek için kullanılabilir. std::any sınıfı, içinde depolanan nesnenin türünden bağımsız olarak çalışır ve kullanıcı tarafından belirtilen türlerle hiçbir şekilde etkileşime girmez.

- std::any sınıfı, bir nesnenin türü ve değeri birbirinden ayrı olarak depolandığı için, türü bilinmeyen bir nesneyi değiştirme veya başka bir türe dönüştürme işlemi yapabilirsiniz.

- Örneğin:

```CPP
#include <iostream>
#include <any>

int main() {
    std::any a = 5;
    std::cout << std::any_cast<int>(a) << '\n'; // 5

    a = 3.14;
    std::cout << std::any_cast<double>(a) << '\n'; // 3.14

    a = std::string("Hello, world!");
    std::cout << std::any_cast<std::string>(a) << '\n'; // Hello, world!

    return 0;
}

```
- Yukarıdaki örnekte, std::any sınıfı kullanılarak herhangi bir türde değişkenler depolanıyor ve daha sonra ilgili türe dönüştürülüyor.

- Tabii, şöyle bir örnek verebilirim:

```CPP
#include <iostream>
#include <any>
#include <string>
#include <vector>

int main() {
  std::vector<std::any> myVector;
  
  myVector.push_back(5);
  myVector.push_back(std::string("Hello"));
  myVector.push_back(3.14);
  
  for (const auto& elem : myVector) {
    if (elem.type() == typeid(int)) {
      std::cout << "Integer element: " << std::any_cast<int>(elem) << std::endl;
    }
    else if (elem.type() == typeid(std::string)) {
      std::cout << "String element: " << std::any_cast<std::string>(elem) << std::endl;
    }
    else if (elem.type() == typeid(double)) {
      std::cout << "Double element: " << std::any_cast<double>(elem) << std::endl;
    }
  }
  
  return 0;
}

```
- Bu örnekte, std::any sınıfının kullanımı gösterilmiştir. std::any, farklı türde verileri tutabilen bir sınıftır. Bu örnekte, farklı türlerdeki verileri bir std::vector<std::any> içinde tutuyoruz ve sonrasında bu vektörün elemanlarına erişerek her birini kendi türünde bastırıyoruz. Bu şekilde, farklı türlerdeki verileri aynı vektörde tutabilir ve sonrasında bu verilere istediğimiz şekilde erişebiliriz.
















