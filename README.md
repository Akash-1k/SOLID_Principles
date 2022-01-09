## SOLID Principles
### Description
SOLID is an acronym for the first five object-oriented design (OOD) principles by Robert C. Martin (also known as Uncle Bob).
These principles establish practices that lend to developing software with considerations for maintaining and extending as the project grows. Adopting these practices can also contribute to avoiding code smells, refactoring code, and Agile or Adaptive software development.

SOLID stands for:
* Single-responsiblity Principle
* Open-closed Principle
* Liskov Substitution Principle
* Interface Segregation Principle
* Dependency Inversion Principle

#### Single Responsibility Principle
The Single Responsibility Principle states that a class should have only one primary responsibility and should not take other responsibilities. Robert C. Martin explains this as “A class should have only one reason to change”

```python
class Shopping:
    def __init__(self):
        pass
    def viewItems(self):
        pass
# only Responsibility to add into cart
class AddToCart:
    def addToCart(self, item):
        pass
# only Responsibility to view items in cart 
class ViewCart:
    def viewCartItems(self, cart_items: Cart):
        pass
```

### Open Closed Principle
Open Closed Principle was first conceptualized by Berterd Meyer in 1988. Robert C. Martin mentioned this as “the most important principle of object-oriented design”. Open Closed Principle states that “Software entities (classes, modules, functions, etc.) should be open for extension, but closed for modification.”

### Liskov Substitution Principle
Liskov Substitution Principle was one of the toughest principles for me to understand and I had to look at various examples on the internet to understand it correctly. But I feel that once understood properly, it is one of the easiest principles to adhere to while designing Object-Oriented Applications.

Liskov Substitution Principle states that "Objects in a program should be replaceable with instances of their subtypes without altering the correctness of that program."

```python
from abc import ABC, abstractmethod
class Discount(ABC):
    def __init__(self, customer):
        self.customer = customer
        self.discount = 1   
    @abstractmethod
    def set_discount(self, price, no_Of_items):
        pass
    def get_discount(self):
        pass
 
class RegularDiscount(Discount):
    def set_discount(self, price, no_Of_items):
        pass
    def get_discount(self):
        return self.discount

class GreatIndianFestival(Discount):
    def set_discount(self, price, no_Of_items):
        pass
    def get_discount(self):
        return self.discount
```
If your code follows the Open-Closed Principle and Liskov Substitution Principle, then it will be implicitly aligned to be compliant to the Dependency Inversion Principle also.
Above example satisfes Open Closed Principle, Liskov Substitution Principle and Dependency Inversion Principle also.

### Interface Segregation Principle
The Interface Segregation Principle states that “No client should be forced to depend on methods it does not use”. The Interface Segregation Principle was introduced by Robert C Martin while he was consulting for Xerox. The Interface Segregation Principle suggests creating smaller interfaces known as “role interfaces” instead of a large interface consisting of multiple methods. By segregating the role-based methods into smaller role interfaces, the clients would depend only on the methods that are relevant to it.


```python
# The Interface Segregation Principle (ISP)
class BuyUsingMoney(ABC):
  @abstractmethod
  def useMoney():
    pass

class BuyUsingSuperCoin(ABC):
  @abstractmethod
  def useSuperCoin():
    pass

class RegularStore(BuyUsingMoney, BuyUsingSuperCoin):
  def useMoney(self):
    pass
  def useSuperCoin(self):
    pass 

class OneRsStore(BuyUsingSuperCoin):
  def useSuperCoin(self):
    pass 
```

## Dependency Inversion Principle
The Dependency Inversion Principle states that:
- a). High level module should not depend on low level modules. Both should depend on abstractions
- b). Abstractions should not depend on details. Details should depend on abstractions.
The first part of this principle reverses traditional OOP software design. Without DIP, programmers often construct programs to have high-level (less detail, more abstract) components explicitly connected with low-level (specific) components to complete tasks.

DIP decouples high and low-level components and instead connects both to abstractions. High and low-level components can still benefit from each other, but a change in one should not directly break the other.

The advantage of this part of DIP is that decoupled programs require less work to change. Webs of dependencies across your program mean that a single change can affect many separate parts.

