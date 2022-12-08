```CPP
#include <iostream>

class Nec {
public: 
	Nec()
	{
		std::cout << "default ctor\n";
	}
	~Nec()
	{
		std::cout << "destructor\n";

	}
};

void foo(Nec x)
{

}

int main()
{
	Nec mynec;

	foo(mynec);
}
```
Cikti:
default ctor
destructor
destructor

Foo fonksiyonu cagirildiginda fonksiyonun parametre degiskeni olan nesne de hayata geliyor. 
Yani program akisi foo fonksiyonunun ana blogunun sonuna geldiginde parametre degiskeni olan nesnenin hayati bitecek ve bunun icin destructor cagirilacak. Ama 2. destructor mynec degiskeni icin cagirilacak.


```CPP
#include <iostream>

class Nec {
public: 
	Nec()
	{
		std::cout << "default ctor\n";
	}
	~Nec()
	{
		std::cout << "destructor\n";

	}
};

void foo(Nec x)
{

}

int main()
{
	Nec mynec;

	foo(mynec);
    (void)getchar();
}
```

Burada ise getchar koyduk yani 2. destructor in mainden ciktiktan sonra olustugunu gorelim diye.


Ayni ornek uzerinden :


```CPP
#include <iostream>

class Nec {
public: 
	Nec()
	{
		std::cout << "default ctor this" << this << "\n";
	}
	~Nec()
	{
		std::cout << "destructor this" << this << "\n";
	}
};

void foo(Nec x)
{

}

int main()
{
	Nec mynec;

	foo(mynec);
	(void)getchar();
}

```
Cikti :

default ctor this000000E5338FF854
destructor this000000E5338FF830

destructor this000000E5338FF854

Peki burada fonksiyonun parametre degiskeni icin destructor cagirildi ama constructor cagirilmadi, neden?

Cevap: onun icin de constructor cagirildi, onunu icin cagirilan cosntructor default constructor degil. Copy constructor.
