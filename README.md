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

If a Class has many responsibilities, it increases the possibility of bugs because making changes to one of its responsibilities, could affect the other ones without you knowing.
##### Goal
This principle aims to separate behaviours so that if bugs arise as a result of your change, it won’t affect other unrelated behaviours.

```python
# SRP -> The Single-Responsibility Principle

class Shopping:
    items=["Shirt","Jeans","Jacket","Trek Suit"]
    
    def __init__(self):
        self.viewItems()
    
    @staticmethod
    def viewItems():
        print("Items available in store")
        for i in self.items:
            print(i)
        print("\n")

class User:
    loggedin = True
    
    def __init__(self, userid):
        self.userid = userid
    
    def userDetails(self):
        pass

class Cart:
    cart_list = []
    
    def __init__(self, User):
        pass

    def addToCart(self, item):
        self.cart_list.append(item)

    def viewCartItems(self):
        print("Item in cart")
        for i in cart_items.cart_list:
            print(i)
```

### Open Closed Principle 
Open Closed Principle states that “Software entities (classes, modules, functions, etc.) should be open for extension, but closed for modification.”

Changing the current behaviour of a Class will affect all the systems using that Class. If you want the Class to perform more functions, the ideal approach is to add to the functions that already exist NOT change them.
#### Goal
This principle aims to extend a Class’s behaviour without changing the existing behaviour of that Class. This is to avoid causing bugs wherever the Class is being used.

### Liskov Substitution Principle
Liskov Substitution Principle states that "Objects in a program should be replaceable with instances of their subtypes without altering the correctness of that program."

When a child Class cannot perform the same actions as its parent Class, this can cause bugs.
The child Class should be able to process the same requests and deliver the same result as the parent Class or it could deliver a result that is of the same type.
If the child Class doesn’t meet these requirements, it means the child Class is changed completely and violates this principle.
#### Goal
This principle aims to enforce consistency so that the parent Class or its child Class can be used in the same way without any errors.

```python
# The Open-Closed Principle (OCP), The Liskov Substitution Principle (LSP) and The Dependency Inversion Principle (DIP)

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
        if no_Of_items >= 5:
            self.discount = price * 0.7
        else:
            self.discount = price * 0.9

    def get_discount(self):
        return self.discount

class GreatIndianFestival(Discount):
    def set_discount(self, price, no_Of_items):
        if no_Of_items >= 5:
            self.discount = price * 0.6
        else:
            self.discount = price * 0.8

    def get_discount(self):
        return self.discount
```
If your code follows the Open-Closed Principle and Liskov Substitution Principle, then it will be implicitly aligned to be compliant to the Dependency Inversion Principle also.
Above example satisfes Open Closed Principle, Liskov Substitution Principle and Dependency Inversion Principle also.

### Interface Segregation Principle
The Interface Segregation Principle states that “No client should be forced to depend on methods it does not use”. The Interface Segregation Principle suggests creating smaller interfaces known as “role interfaces” instead of a large interface consisting of multiple methods. By segregating the role-based methods into smaller role interfaces, the clients would depend only on the methods that are relevant to it.

When a Class is required to perform actions that are not useful, it is wasteful and may produce unexpected bugs if the Class does not have the ability to perform those actions.
#### Goal
This principle aims at splitting a set of actions into smaller sets so that a Class executes ONLY the set of actions it requires.

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
    print("Pay in Rs") 
  def useSuperCoin(self):
    print("Pay with Supercoin") 

class NintyOneRsStore(BuyUsingSuperCoin):
  def useSuperCoin(self):
    print("Pay with Supercoin and 91Rs") 
```

## Dependency Inversion Principle
The Dependency Inversion Principle states that:
- a). High level module should not depend on low level modules. Both should depend on abstractions
- b). Abstractions should not depend on details. Details should depend on abstractions.
The first part of this principle reverses traditional OOP software design. Without DIP, programmers often construct programs to have high-level (less detail, more abstract) components explicitly connected with low-level (specific) components to complete tasks.

DIP decouples high and low-level components and instead connects both to abstractions. High and low-level components can still benefit from each other, but a change in one should not directly break the other.

The advantage of this part of DIP is that decoupled programs require less work to change. Webs of dependencies across your program mean that a single change can affect many separate parts.
#### Goal
This principle aims at reducing the dependency of a high-level Class on the low-level Class by introducing an interface.
