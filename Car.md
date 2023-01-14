Car.h dosyası

#include <iostream>
#include <random>

using namespace std;

class Car {
public:
	virtual void start() {
		std::cout << "car has startedé\n";
	}
	virtual void run() {
		std::cout << "car is running now!\n";
	}
	virtual void stop() {
		std::cout << "car has jsut stapped!\n";
	}
};

class Fiat : public Car {
public:
	void start() {
		std::cout << "Fiat has startedé\n";
	}
	void run() {
		std::cout << "Fiat is running now!\n";
	}
	void stop() {
		std::cout << "Fiat has jsut stapped!\n";
	}
};

class Audi : public Car {
public:
	void start() {
		std::cout << "Audi has startedé\n";
	}
	void run() {
		std::cout << "Audi is running now!\n";
	}
	void stop() {
		std::cout << "Audi has jsut stapped!\n";
	}
};

class Mercedes : public Car {
public:
	void start() {
		std::cout << "Mercedes has startedé\n";
	}
	void run() {
		std::cout << "Mercedes is running now!\n";
	}
	void stop() {
		std::cout << "Mercedes has jsut stapped!\n";
	}
};

class Volvo : public Car {
public:
	void start() {
		std::cout << "Volvo has startedé\n";
	}
	void run() {
		std::cout << "Volvo is running now!\n";
	}
	void stop() {
		std::cout << "Volvo has jsut stapped!\n";
	}
};


class Skoda : public Car {
public:
	void start() {
		std::cout << "Skoda has startedé\n";
	}
	void run() {
		std::cout << "Skoda is running now!\n";
	}
	void stop() {
		std::cout << "Skoda has jsut stapped!\n";
	}
};

class Opel : public Car {
public:
	void start() {
		std::cout << "Opel has startedé\n";
	}
	void run() {
		std::cout << "Opel is running now!\n";
	}
	void stop() {
		std::cout << "Opel has jsut stapped!\n";
	}
};

class Bmw : public Car {
public:
	void start() {
		std::cout << "Bmw has startedé\n";
	}
	void run() {
		std::cout << "Bmw is running now!\n";
	}
	void stop() {
		std::cout << "Bmw has jsut stapped!\n";
	}
};

Car* create_random_car()
{
	static std::mt19937 eng{ std::random_device{}() };
	static std::uniform_int_distribution dist{ 0,6 };

	switch (dist(eng)) {
	case 0: return new Mercedes;
	case 1: return new Audi;
	case 2: return new Fiat;
	case 3: return new Opel;
	case 4: return new Volvo;
	case 5: return new Bmw;
	case 6: return new Skoda;
	default: return nullptr;
	}
}
