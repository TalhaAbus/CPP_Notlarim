```CPP
#include <iostream>

class Myclass {
public:
    Myclass()
    {
        std::cout << "default ctor this:" << this << '\n';
    }
    ~Myclass()
    {
        std::cout << "destructor this:" << this << '\n';
    }
};

Myclass g1;
Myclass g2;
Myclass g3;

int main()
{
    std::cout << "main basladi\n";
    std::cout << "main sonra eriyor\n";
}
```

```CPP
#include <iostream>

class Myclass {
public:
    Myclass()
    {
        std::cout << "default ctor this:" << this << '\n';
    }
    ~Myclass()
    {
        std::cout << "destructor this:" << this << '\n';
    }
};

void foo()
{
    std::cout << "foo cagrildi";
    static Myclass m;
}

int main()
{
    std::cout << "main basladi\n";
    foo();
    foo();
    foo();
    foo(); 
    foo();
    std::cout << "main sonra eriyor\n";
}
```

```CPP
#include <iostream>

class Myclass {
public:
    Myclass()
    {
        std::cout << "Myclass default ctor\n";
    }
    ~Myclass()
    {
        std::cout << "Myclass destructor\n";
    }
};


int main()
{
    std::cout << "main basladi\n";

    if (1) {
        Myclass m;
        std::cout << "main devam ediyor\n";
        (void)getchar();
    }
    std::cout << "main devam ediyor\n";
    
    std::cout << "main sona eriyor\n";

}
```

```CPP
#include <iostream>

class Myclass {
public:
    Myclass()
    {
        std::cout << "Myclass default ctor\n";
    }
    ~Myclass()
    {
        std::cout << "Myclass destructor\n";
    }
    void func()
    {
        std::cout << "Nec::func()\n";
    }
};


int main()
{
    std::cout << "main basladi\n";
    auto p = new Myclass;
    p->func();

    delete p;

    std::cout << "main devam ediyor\n";

}
```
