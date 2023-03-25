- <csignal> başlık dosyası, C++ standart kütüphanesi içinde yer alan bir başlık dosyasıdır. Bu başlık dosyası, C dilindeki <signal.h> başlık dosyası ile benzer işlevleri yerine getirir. Programcılar, bu başlık dosyasını kullanarak sinyal işlemleri gerçekleştirebilirler.

- Bu başlık dosyası, öncelikle sinyal işlemleri için kullanılan fonksiyon ve makrolar içerir. Bunlar arasında SIGINT, SIGABRT, SIGFPE, SIGILL, SIGSEGV, SIGTERM gibi sinyallerin yakalanması için kullanılan fonksiyonlar, sinyal işleyicilerin tanımlanması ve sinyal işleyicilerin kaldırılması için kullanılan fonksiyonlar ve sinyal maskesi işlemleri için kullanılan fonksiyonlar yer alır.

- Ayrıca, bu başlık dosyası <cstddef> başlık dosyasına da bağımlıdır ve NULL makrosunu kullanmak için std::nullptr_t tipini içerir.

- Örnek olarak, aşağıdaki kod, SIGINT sinyalini yakalayan bir sinyal işleyici tanımlar:

```CPP
#include <csignal>
#include <iostream>

void signal_handler(int signal) {
    std::cout << "Caught signal: " << signal << std::endl;
}

int main() {
    std::signal(SIGINT, signal_handler);
    std::cout << "Signal handler registered for SIGINT." << std::endl;
    while (true) {}
    return 0;
}

```

> Bu örnekte, std::signal() fonksiyonu kullanılarak SIGINT sinyali için bir sinyal işleyici belirleniyor. Ardından, sonsuz bir döngü başlatılıyor ve program, SIGINT sinyali yakalandığı zaman sinyal işleyicinin çalıştırılmasını bekler.

# ben neden bu başlık dosyasını kullanayım?  

- <csignal> başlık dosyası, C++ programlarında sinyal işleme ile ilgili işlemleri gerçekleştirmek için kullanılır. Sinyaller, bir işlemde veya programda beklenmedik bir durum ortaya çıktığında oluşan hatayı işaret etmek için kullanılır ve bu hataların izlenmesi ve programın yönetilmesi için kullanılır.

- Bu başlık dosyası, sinyalleri işlemek için çeşitli fonksiyonlar sağlar. Örneğin signal() fonksiyonu, bir sinyalin belirtilen işlev tarafından ele alınmasını sağlar. raise() fonksiyonu, bir sinyal oluşturur ve belirtilen işlemdeki veya programdaki bir işlev tarafından ele alınabilir.

- Bu başlık dosyası ayrıca, işlemin sinyalleri nasıl işleyeceğine ilişkin bazı sabitler de tanımlar. Örneğin, SIGINT sabiti, bir kullanıcının Ctrl-C tuşlarına basması durumunda ortaya çıkan sinyali temsil eder.

- Bu başlık dosyası özellikle, düşük seviyeli bir işlem API'sine sahip işletim sistemlerinde kullanışlıdır. Sinyallerin nasıl ele alınacağını belirlemek için sinyal işleme mekanizmasını kullanan programlar için gereklidir.

- Örnek olarak, aşağıdaki kod parçası SIGINT sinyalini işleyerek programı sonlandırır:

```CPP
#include <csignal>
#include <iostream>
#include <unistd.h>

void signalHandler(int signum) {
    std::cout << "Interrupt signal (" << signum << ") received.\n";

    // Programı sonlandır
    exit(signum);
}

int main() {
    // SIGINT sinyalini işlemek için signal() fonksiyonunu kullan
    signal(SIGINT, signalHandler);

    // Sonsuz döngü
    while(1) {
        std::cout << "Program çalışıyor...\n";
        sleep(1);
    }

    return 0;
}

```
> Bu örnek kodda, signalHandler() fonksiyonu, SIGINT sinyalini yakalar ve programı sonlandırır. signal() fonksiyonu, SIGINT sinyalinin işleneceği işlevi belirlemek için kullanılır. Sonsuz döngüde Program çalışıyor... mesajı yazdırılır ve sleep() fonksiyonu ile 1 saniye beklenir. Ctrl-C tuşlarına basarak SIGINT sinyalini gönderebilirsiniz ve program, sinyal işleyicisi fonksiyonu çalıştırdıktan sonra sonlanacaktır.









