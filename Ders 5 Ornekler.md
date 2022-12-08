```CPP
int main()
{
	int ival = 35;
	int* p = &ival;
	int*& rp = p;	// int* türünden nesneye referans olan rp

	std::cout << "ival = " << ival << "\n";
	*rp = 99;
	std::cout << "ival = " << ival << "\n";

	int x = 44;
	rp = &x;
	std::cout << "*p = " << *p << "\n";
}
```
======================================================
```CPP
#include <iostream>

int main()
{
	int x{ 3 };
	int& r{ x };
	// Buradan sonra r nin scope içinde r yazmak ile x yazmak arasında bir fark yok.
	std::cout << "x = " << x << "\n";

	r = 67;
	std::cout << "x = " << x << "\n";
	++r;
	std::cout << "x = " << x << "\n";

	int a = 10;
	int& r1 = a;
	int& r2 = r1;
	int& r3 = r2;
	std::cout << "x = " << a << "\n";
	std::cout << "x = " << r1 << "\n";
	std::cout << "x = " << r2 << "\n";
	std::cout << "x = " << r3 << "\n";
	++r2;
	std::cout << "x = " << a << "\n";
	++r3;
	std::cout << "x = " << a << "\n";
}
```
================================================
```CPP
#include <iostream>

int main()
{
	int a[]{ 1,3,5,7,9 };
	int* p = a;
	std::cout << "" << *p << "\n";
	++p;
	std::cout << "" << *p << "\n";

	int(&ra)[5] = a;	// ra, a nın yerine geçecek referan oldu. ra demek a demek.
	
	for (int i = 0; i < 5; i++)
		std::cout << ra[i] << " " << a[i] << "\n";
}
```
==========================
```CPP
#include <iostream>

void func(int* p)
{
	*p = 99;
}

int main()
{
	int x = 45;

	std::cout << "x =" << x << "\n";
	func(&x);
	std::cout << "x =" << x << "\n";
}
```
============================
```CPP
#include <iostream>

void func(int p)
{
	p = 99;
}

int main()
{
	int x = 45;

	std::cout << "x =" << x << "\n";
	func(x);
	std::cout << "x =" << x << "\n";
}
```
===============================
```CPP
#include <iostream>

void func(int& r)
{
	r = 99;
}

int main()
{
	int x = 45;

	std::cout << "x =" << x << "\n";
	func(x);
	std::cout << "x =" << x << "\n";
}
```
===============================
```CPP
Hem pointer hem de referans semantiği ile swap fonksiyonu yazalım.

#include <iostream>

void iswap(int& r1, int& r2)
{
	int temp = r1;
	r1 = r2;
	r2 = temp;
}

void iswap(int* p1, int* p2)
{
	int temp = *p1;
	*p1 = *p2;
	*p2 = temp;
}

int main()
{
	int x = 45, y = 77;

	std::cout << "x = " << x << " " << "y = " << y << "\n";
	iswap(x, y);
	std::cout << "x = " << x << " " << "y = " << y << "\n";
	iswap(&x, &y);
	std::cout << "x = " << x << " " << "y = " << y << "\n";
}
```
=========================================
```CPP
#include <iostream>

int g = 5;

int* func()
{
	return &g;
}

int main()
{
	int* ptr = func();

	std::cout << "*ptr =" << *ptr << "\n";
	*ptr = 999;
	std::cout << "g =" << g << "\n";
}
```
===============================
```CPP
Bu kodu referans semantiği ile yazalım.

#include <iostream>

int g = 5;

int& func()
{
	return g;
}

int main()
{
	std::cout << "*g =" << g << "\n";

	func() = 999; // soldaki ifade fonksiyonun geri döndürdüğü nesne anlamına gelecek ve sol taraf değeri olacak, atama yapılabilir.

	std::cout << "*g =" << g << "\n";
}
```
=================================

```CPP
Bizim ornek:

int main()
{
	int x = 10;

	int& dr1 = x;
	const double& dr2 = x;

	std::cout << "x'in adresi" << &x << '\n';
	std::cout << "dr1'in adresi" << &dr1 << '\n';
	std::cout << "dr2'nin adresi" << &dr2 << '\n' << "\n";


	const int y = 5;
	const int& cir1 = y;

	std::cout << "y'nin adresi" << &y << '\n';
	std::cout << "cir'in adresi" << &cir1 << '\n' << "\n";

	int z = 5;
	const int& cir2 = z;

	std::cout << "y'nin adresi" << &y << '\n';
	std::cout << "cir'in adresi" << &cir2 << '\n';
}
```
