---
title: "Statische Typen und Defaultargumente in C++"
date: 2019-02-17
lastmod: 2019-10-19
tags: ['C++']
vgwort: 'd6a08a318bbf4d75983a2b8d62e32c74'
---
Quiz. Was gibt dieses Programm aus?

```c++
#include <iostream>

class Vehicle
{
public:
  virtual void FillUp(int amount = 20)
  {
      std::cout << "Filling up the vehicle with "
                << amount << " gallons of gas" << std::endl;
  };
};

class Car : public Vehicle
{
public:
  virtual void FillUp(int amount = 10)
  {
    std::cout << "Filling up the car with "
              << amount << " gallons of gas" << std::endl;
  };
};

int main(void)
{
  Vehicle *v = new Car;

  v->FillUp();

  return 0;
}
```

Wenn Sie gedacht haben, die Ausgabe werde „Filling up the car with 10 gallons of gas“ sein, sind Sie in guter Gesellschaft, liegen aber dennoch daneben. Die tatsächliche Ausgabe lautet „Filling up the car with 20 gallons of gas“.

Doch wie kann das sein? Das ist so, als ob eine völlig neue, erfundene Methode aufgerufen wurde, die aus Teilen von `Vehicle::FillUp` und Teilen von `Car::FillUp` zusammengestückelt worden ist.

Der C++-Standard verlangt dies aber tatsächlich. Viele C++-Programmierer wissen nicht, daß sie sich in manchen Situationen darüber klar sein müssen, daß Objekte nicht nur einen Typ besitzen, sondern zwei: einen dynamischen Typ und einen statischen Typ. Eine solche Situation ist, wenn sie Defaultargumente von in einer Klassenhierarchie überschriebenen Methoden ändern.

Treten wir einen Schritt zurück. Was ist ein statischer Typ?

```c++
int a;
```

`a` ist ein Objekt vom statischen Typ `int`. Das war einfach.

```c++
// [...Vehicle and Car defined as above...]

int main(void)
{
  Vehicle v;
  Car c;

  v = c;

  v.FillUp();
}
```

Dies ist gültiges C++. Das `Car c` wird „geslicet“ zu einem `Vehicle` und `v` zugewiesen. `v` hat den statischen Typ `Vehicle`.

Jeder würde erwarten, daß die Ausgabe „Filling up the vehicle with 20 gallons of gas“ lautete, und hätte damit auch recht.

Nun zum schwierigeren Teil:

```c++
// [...Vehicle and Car defined as above...]

int main(void)
{
  Vehicle *v = new Car;
  
  v->FillUp();

  return 0;
}
```

In diesem Beispiel, in dem `v` ein Zeiger ist, ist `v` nach wie vor vom statischen Typ `Vehicle` (so steht es in der Deklaration), aber vom dynamischen Typ `Car` (das hat die Zuweisung ergeben – die auch zur Laufzeit erfolgen kann, hier hat sie bereits statisch bei der Initialisierung stattgefunden).

Die Methodenauswahl erfolgt in C++ anhand des dynamischen Typs, daher wird `Car::FillUp` ausgewählt.

Aus Performancegründen haben die C++-Designer sich aber entschieden, für die Auswahl, welche Defaultargumente zur Compilezeit an die formalen Parameter der Methode gebunden werden, den statischen Typ zugrundezulegen.

Und deshalb ist die Intuition, daß hier zwei verschiedene Methoden vermischt werden, tatsächlich richtig. Der Körper der Methode stammt von der Kindklasse, aber die Defaultargumente stammen von der Elternklasse.
