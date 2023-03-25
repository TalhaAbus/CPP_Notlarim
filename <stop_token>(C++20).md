- <stop_token> başlık dosyası, C++20 ile birlikte eklenen bir özelliktir ve C++'ta asenkron işlemleri kontrol etmek için kullanılır. <stop_token> başlık dosyası, <thread>, <future> ve <condition_variable> gibi diğer C++ başlık dosyalarıyla birlikte kullanılabilir.

- <stop_token> başlık dosyası, stop_source ve stop_token sınıflarını içerir. stop_source, bir senaryonun tamamlanması için kullanılan bir araçtır ve stop_token, bir senaryonun çalıştırılmasını durdurmak için kullanılır.

- stop_source sınıfı, bir senaryonun durdurulmasını isteyen kod bloklarında oluşturulur. stop_token sınıfı, durdurma sinyalinin kontrolünü sağlayan bir arayüz sağlar. stop_token sınıfı, başka bir sınıfın bir parçası olarak veya bir iş parçacığı tarafından kullanılabilir.

- Bir örnek vermek gerekirse, bir dosyanın okunması işlemi bir senaryondur. Eğer kullanıcı okuma işleminden vazgeçmek istiyorsa, bir durdurma sinyali gönderilebilir. Bu senaryoyu <stop_token> kullanarak gerçekleştirebiliriz:

```CPP
#include <iostream>
#include <thread>
#include <stop_token>
#include <fstream>

using namespace std;

void read_file(stop_token st) {
    ifstream file("test.txt");
    if (!file.is_open()) {
        cout << "Could not open file!\n";
        return;
    }

    string line;
    while (getline(file, line)) {
        if (st.stop_requested()) {
            cout << "Reading file has been cancelled.\n";
            return;
        }
        cout << line << '\n';
    }

    file.close();
}

int main() {
    stop_source ss;
    thread t(read_file, ss.get_token());

    this_thread::sleep_for(3s); // 3 saniye bekle

    ss.request_stop();

    t.join();

    return 0;
}

```
> Bu örnekte, read_file işlevi bir dosyanın okunması işlemini gerçekleştirir. Senaryo, okuma işleminden vazgeçmek isteyen bir kullanıcı olduğunda durdurulur. read_file işlevi, stop_token nesnesi tarafından sağlanan stop_requested() işlevini kullanarak durdurma sinyalini kontrol eder.

- Ana iş parçacığı, stop_source nesnesini kullanarak bir durdurma sinyali gönderir. Durdurma sinyali gönderildiğinde, diğer iş parçacığı stop_requested() işlevi tarafından tespit edilir ve okuma işlemi sonlandırılır.

- C++20'de eklenen <stop_token> başlık dosyası, çalışan iş parçacıklarının kesintiye uğramasını sağlar. İş parçacığı bir işi yaparken, durma belirteci işlemi yarıda kesip iş parçacığını durdurabilir. Böylece programın çalışması sonlandırılabilir veya işlem iptal edilebilir.

- std::stop_token sınıfı, iş parçacığının durma belirtecinin durumunu sorgulamasına ve iş parçacığına durdurma sinyalleri göndermesine olanak tanır. std::stop_source sınıfı ise durma belirteci oluşturur ve iş parçacığına sinyal gönderir.

- std::stop_callback sınıfı, belirtilen bir işlevi veya işlev nesnesini, durma belirteci veya durma kaynağı durdurulduğunda otomatik olarak çağırmak için kullanılır.

- Örnek olarak, bir iş parçacığının işi tamamlanmadan önce programın sonlandırılması gerekiyorsa veya belirli bir koşul gerçekleştiğinde işlem iptal edilmek isteniyorsa, std::stop_token kullanılabilir. Aşağıdaki örnek, bir iş parçacığında hesaplama yaparken durma belirteci kullanımını gösterir:

```CPP
#include <iostream>
#include <chrono>
#include <thread>
#include <stop_token>

void do_calculation(std::stop_token token) {
    std::cout << "Calculation started\n";
    int result = 0;
    for (int i = 1; i <= 100; ++i) {
        // Durma belirteci durduruldu mu kontrol et
        if (token.stop_requested()) {
            std::cout << "Calculation cancelled\n";
            return;
        }
        result += i;
        std::this_thread::sleep_for(std::chrono::milliseconds(50));
    }
    std::cout << "Calculation result: " << result << '\n';
}

int main() {
    std::jthread thread(do_calculation); // İş parçacığı oluşturuldu
    std::this_thread::sleep_for(std::chrono::milliseconds(500)); // 0.5 saniye bekle
    thread.request_stop(); // İşlem durduruldu
    thread.join();
    return 0;
}

```
- Bu örnekte, std::jthread sınıfı kullanılarak bir iş parçacığı oluşturulur. do_calculation() işlevi, hesaplama yapmak için 50 ms bekleyerek, işlemin 100'e kadar olan tüm sayıları toplar. İş parçacığı oluşturulduktan 0.5 saniye sonra request_stop() fonksiyonu çağrılarak işlem durdurulur. İş parçacığı durma belirtecinin durumunu kontrol eder ve hesaplama işlemini yarıda keser.





