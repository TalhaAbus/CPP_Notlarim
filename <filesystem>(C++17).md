- C++ dilinde <filesystem> kütüphanesi, dosya ve dizin işlemleri için güçlü ve esnek bir arayüz sağlar. C++17 standardıyla birlikte tanıtılan bu kütüphane, dosyaları ve dizinleri oluşturma, kopyalama, taşıma, yeniden adlandırma, silme ve özelliklerini sorgulama gibi işlemleri gerçekleştirmenize olanak tanır.

- <filesystem> kütüphanesini kullanmak için, kodunuzun başında aşağıdaki gibi bir #include ifadesi eklemeniz gerekir:

```CPP
#include <filesystem>

```

Bu kütüphane, std::filesystem ad alanı içinde tanımlanmıştır ve 
- **std::filesystem::path,** 
- **std::filesystem::directory_iterator,**
- **std::filesystem::recursive_directory_iterator** gibi sınıfları ve 
- **std::filesystem::create_directory,** 
- **std::filesystem::remove,**
- **std::filesystem::rename,** 
- **std::filesystem::exists** gibi işlevleri içerir.

İşte küçük bir örnek:

```CPP
#include <iostream>
#include <filesystem>

namespace fs = std::filesystem;

int main() {
    fs::path p("ornek_dizin");

    if (fs::create_directory(p)) {
        std::cout << "Dizin başarıyla oluşturuldu: " << p << std::endl;
    } else {
        std::cout << "Dizin oluşturulamadı: " << p << std::endl;
    }

    return 0;
}

```

> Bu örnek, "ornek_dizin" adında bir dizin oluşturur ve başarılı olup olmadığını ekrana yazdırır.

- Tabii, aşağıda <filesystem> kütüphanesinin bazı işlevlerini kullanan daha kapsamlı bir örnek veriyorum:

```CPP
#include <iostream>
#include <fstream>
#include <filesystem>

namespace fs = std::filesystem;

int main() {
    // Dizin ve dosya yollarını oluştur
    fs::path dir_path("ornek_dizin");
    fs::path file_path = dir_path / "ornek_dosya.txt";

    // Dizin oluştur
    if (fs::create_directory(dir_path)) {
        std::cout << "Dizin başarıyla oluşturuldu: " << dir_path << std::endl;
    } else {
        std::cout << "Dizin oluşturulamadı: " << dir_path << std::endl;
    }

    // Dosya oluştur ve içeriğini yaz
    std::ofstream file(file_path);
    if (file.is_open()) {
        file << "Merhaba, dosya sistemi!" << std::endl;
        file.close();
        std::cout << "Dosya başarıyla oluşturuldu: " << file_path << std::endl;
    } else {
        std::cout << "Dosya oluşturulamadı: " << file_path << std::endl;
    }

    // Dosya boyutunu al ve ekrana yazdır
    try {
        auto file_size = fs::file_size(file_path);
        std::cout << "Dosya boyutu: " << file_size << " bayt" << std::endl;
    } catch (fs::filesystem_error& e) {
        std::cout << "Hata: " << e.what() << std::endl;
    }

    // Dosyayı yeniden adlandır
    fs::path new_file_path = dir_path / "yeni_dosya.txt";
    try {
        fs::rename(file_path, new_file_path);
        std::cout << "Dosya başarıyla yeniden adlandırıldı: " << new_file_path << std::endl;
    } catch (fs::filesystem_error& e) {
        std::cout << "Hata: " << e.what() << std::endl;
    }

    // Dosyayı ve dizini sil
    try {
        fs::remove(new_file_path);
        std::cout << "Dosya başarıyla silindi: " << new_file_path << std::endl;
    } catch (fs::filesystem_error& e) {
        std::cout << "Hata: " << e.what() << std::endl;
    }

    try {
        fs::remove(dir_path);
        std::cout << "Dizin başarıyla silindi: " << dir_path << std::endl;
    } catch (fs::filesystem_error& e) {
        std::cout << "Hata: " << e.what() << std::endl;
    }

    return 0;
}

```
> Bu örnek, "ornek_dizin" adında bir dizin oluşturur, ardından bu dizin içinde "ornek_dosya.txt" adlı bir dosya oluşturur ve içine metin yazar. Daha sonra dosya boyutunu öğrenir ve ekrana yazdırır. Ardından dosyayı yeniden adlandırır, sonunda dosyayı ve dizini siler.

























