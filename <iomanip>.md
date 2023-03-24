# iomanip nedir

- <iomanip, C++ standart kütüphanesinde yer alan bir başlık dosyasıdır. Bu başlık dosyası, girdi/çıktı işlemlerinde kullanılan manipülatörler (manipulators) olarak adlandırılan özel işlevleri içerir.

- Manipülatörler, girdi/çıktı işlemlerinin formatını ayarlamak için kullanılırlar. Örneğin, sayıları belirli bir genişlikte ve belirli bir hassasiyetle yazdırmak, ondalık ayraçların ve diğer ayraçların yerini belirlemek gibi işlemler manipülatörler aracılığıyla gerçekleştirilir.

- <iomanip başlık dosyasındaki bazı yaygın manipülatörler şunlardır:

- std::setw(int width): Çıktı alanının genişliğini ayarlar.
- std::setprecision(int precision): Çıktıdaki ondalık sayıların hassasiyetini belirler.
- std::fixed ve std::scientific: Çıktıdaki ondalık sayıların gösterim biçimini belirler.
- std::left ve std::right: Çıktıdaki verilerin hizalamasını belirler.
- std::setfill(char fillchar): Alanın boşluklarını doldurmak için kullanılan karakteri belirler.
- Örneğin, aşağıdaki C++ kodu, bir ondalık sayının hassasiyetini ayarlar ve onu belirli bir genişlikte yazdırır:

```CPP
#include <iostream>
#include <iomanip>

int main() {
    double x = 3.14159;
    std::cout << std::fixed << std::setprecision(2) << std::setw(10) << x << std::endl;
    return 0;
}

```
> Bu kod, std::fixed ve std::setprecision manipülatörlerini kullanarak x değerinin ondalık kısmının iki basamağını yazdırır. std::setw manipülatörü, çıktı alanının genişliğini 10 karakter olarak ayarlar.
