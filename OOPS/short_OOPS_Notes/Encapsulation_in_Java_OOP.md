# Encapsulation in Java OOP

> **Encapsulation is one of the four fundamental pillars of Object-Oriented Programming (OOP), along with Inheritance, Polymorphism, and Abstraction.**

---

## 1. What is Encapsulation?

**Encapsulation** means:

> **Bundling data and the methods that operate on that data into a single class, while restricting direct access to the data and providing controlled access through methods.**

In Java, encapsulation is commonly achieved by:

- Declaring variables as `private`
- Providing `public` methods to access or modify them
- Adding validation inside those methods when required

### Basic structure

```java
class Student {

    private String name;
    private int age;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        if (age >= 0) {
            this.age = age;
        }
    }
}
```

Here:

- `name` and `age` are **private data**
- `getName()` and `getAge()` are **getters**
- `setName()` and `setAge()` are **setters**
- `setAge()` also performs **validation**

---

# 2. Why Do We Need Encapsulation?

Consider this class:

```java
class Student {

    public String name;
    public int age;
}
```

Because the variables are `public`, anyone can directly modify them:

```java
Student s = new Student();

s.age = -500;
```

Java will allow this because there is no restriction.

But a student having an age of `-500` is not exactly a groundbreaking new education model.

The problem is that the class has **no control over its own data**.

With encapsulation:

```java
class Student {

    private int age;

    public void setAge(int age) {

        if (age >= 0) {
            this.age = age;
        }
    }

    public int getAge() {
        return age;
    }
}
```

Now the outside code cannot directly modify `age`.

Instead:

```java
Student s = new Student();

s.setAge(-500);
```

The value can be rejected because the class controls how its data is changed.

---

# 3. The Role of `private`

The `private` keyword is extremely important for encapsulation.

```java
class Student {

    private int age;
}
```

`private` means:

> The variable can be directly accessed only from within the same class.

Therefore, this is not allowed:

```java
Student s = new Student();

s.age = 21;
```

Instead, the class provides controlled methods:

```java
public void setAge(int age) {
    this.age = age;
}

public int getAge() {
    return age;
}
```

So the general pattern is:

```text
private data
     ↓
No direct access from outside
     ↓
Public methods
     ↓
Controlled access
```

---

# 4. Getters and Setters

Getters and setters are methods commonly used to access private variables.

## Getter

A getter is used to **read** a value.

```java
public int getAge() {
    return age;
}
```

Usage:

```java
System.out.println(s.getAge());
```

## Setter

A setter is used to **modify** a value.

```java
public void setAge(int age) {
    this.age = age;
}
```

Usage:

```java
s.setAge(21);
```

### Quick reference

| Method | Purpose |
|---|---|
| `getAge()` | Reads `age` |
| `setAge()` | Modifies `age` |

---

# 5. Setters Are Not Compulsory

A common misconception is:

> Every private variable must have a getter and setter.

That is **not true**.

You should expose only the operations that make sense.

For example:

```java
class BankAccount {

    private double balance;

    public double getBalance() {
        return balance;
    }

    public void deposit(double amount) {

        if (amount > 0) {
            balance += amount;
        }
    }
}
```

There is no:

```java
setBalance()
```

Why?

Because we don't want outside code to arbitrarily change the balance.

Instead, balance changes through meaningful operations:

```java
deposit()
withdraw()
```

This provides stronger control over the object's state.

---

# 6. Encapsulation Through a Real-World Example

Think about a **bank account**.

You don't directly access the bank's database and write:

```text
balance = 1,000,000
```

Instead, you use controlled operations:

```text
Deposit money
Withdraw money
Check balance
```

The same idea is represented in Java:

```java
class BankAccount {

    private double balance;

    public void deposit(double amount) {

        if (amount > 0) {
            balance += amount;
        }
    }

    public void withdraw(double amount) {

        if (amount > 0 && amount <= balance) {
            balance -= amount;
        }
    }

    public double getBalance() {
        return balance;
    }
}
```

Usage:

```java
BankAccount account = new BankAccount();

account.deposit(5000);
account.withdraw(1000);

System.out.println(account.getBalance());
```

The outside code **does not directly manipulate `balance`**.

Instead, it asks the `BankAccount` object to perform operations.

---

# 7. What Exactly Is Being Encapsulated?

Consider:

```java
class Car {

    private int speed;

    public void accelerate() {
        speed += 10;
    }

    public int getSpeed() {
        return speed;
    }
}
```

Here we have:

### Data

```java
private int speed;
```

### Methods that operate on the data

```java
accelerate()
getSpeed()
```

Both are bundled inside:

```java
class Car
```

Therefore:

> **Encapsulation bundles data and the behavior associated with that data inside a class.**

---

# 8. Data Hiding

**Data hiding** means preventing direct access to an object's internal data.

For example:

```java
class Employee {

    private int salary;
}
```

Outside code cannot do:

```java
employee.salary = -100000;
```

because `salary` is private.

Instead:

```java
public void setSalary(int salary) {

    if (salary >= 0) {
        this.salary = salary;
    }
}
```

Now the class can control what values are accepted.

---

# 9. Encapsulation = Data Hiding + Controlled Access

A useful way to remember encapsulation is:

```text
             ENCAPSULATION
                   |
          ┌────────┴────────┐
          ↓                 ↓
    Data Hiding       Controlled Access
          |                 |
       private          methods
       variables       getters/setters
                           |
                      validation
```

Therefore:

> **Data hiding is one mechanism used to achieve encapsulation.**

Encapsulation is broader than simply making variables private.

---

# 10. Validation and Encapsulation

One of the biggest advantages of encapsulation is that we can validate data before modifying the object's state.

Example:

```java
class Person {

    private int age;

    public void setAge(int age) {

        if (age >= 0 && age <= 150) {
            this.age = age;
        }
    }

    public int getAge() {
        return age;
    }
}
```

Now:

```java
Person p = new Person();

p.setAge(21);
```

is valid.

But:

```java
p.setAge(-10);
```

can be rejected.

The important idea is:

> **The class controls its own state.**

---

# 11. A Complete Example

```java
class Person {

    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {

        if (age >= 0 && age <= 150) {
            this.age = age;
        }
    }
}
```

### Using the class

```java
public class Main {

    public static void main(String[] args) {

        Person p = new Person("Shivangi", 21);

        System.out.println(p.getName());
        System.out.println(p.getAge());

        p.setAge(22);

        System.out.println(p.getAge());
    }
}
```

### What is happening?

When we write:

```java
p.setAge(22);
```

the outside code is not directly changing:

```java
age
```

Instead:

```text
Main
 |
 | setAge(22)
 ↓
Person object
 |
 ↓
setAge()
 |
 ↓
Validation
 |
 ↓
age = 22
```

The class remains in control of its internal data.

---

# 12. Why Is Encapsulation Useful?

## 1. Data Protection

Private variables cannot be directly modified from outside the class.

```java
private double balance;
```

---

## 2. Validation

Methods can check whether data is valid.

```java
if (age >= 0) {
    this.age = age;
}
```

---

## 3. Better Control

Instead of exposing internal variables, a class can expose meaningful operations.

Instead of:

```java
setBalance()
```

we can use:

```java
deposit()
withdraw()
```

This is more representative of how a bank account actually works.

---

## 4. Maintainability

The internal implementation can change without necessarily changing how other classes interact with the object.

For example, other classes may continue using:

```java
getAge()
```

even if the internal representation of age changes later.

---

## 5. Reduced Coupling

Other classes do not need to know the internal implementation of an object.

They only interact through the methods exposed by the class.

---

# 13. Encapsulation and Access Modifiers

Java provides four main access levels:

```text
private
default
protected
public
```

For encapsulation, `private` is particularly important.

## `private`

Accessible only within the same class.

```java
class Student {

    private int marks;
}
```

## `public`

Can be accessed from outside the class, subject to the normal Java access rules.

```java
public int getMarks() {
    return marks;
}
```

Therefore, a common encapsulation pattern is:

```java
private variable
      +
public method
```

---

# 14. Encapsulation vs Data Hiding

These concepts are closely related but are **not exactly identical**.

### Data Hiding

Focuses on:

> Preventing direct access to internal data.

Example:

```java
private int salary;
```

### Encapsulation

Focuses on:

> Bundling data and related behavior together and controlling how the data can be accessed or modified.

Therefore:

```text
Data Hiding
     ↓
Restrict direct access
     ↓
private fields
```

while:

```text
Encapsulation
     ↓
Data + Methods
     ↓
Controlled Access
     ↓
Validation / Protection
```

### Interview statement

> **Data hiding is a mechanism used to achieve encapsulation.**

---

# 15. Encapsulation vs Abstraction

This is a very common interview question.

## Encapsulation

Focuses on:

> **How do I protect and control my data?**

Example:

```java
private double balance;
```

with:

```java
deposit();
withdraw();
getBalance();
```

---

## Abstraction

Focuses on:

> **What should the user see, and what implementation details should be hidden?**

For example:

```java
abstract class Vehicle {

    abstract void start();
}
```

The user knows:

```java
vehicle.start();
```

but does not necessarily need to know the internal implementation of how the engine starts.

### Difference

| Encapsulation | Abstraction |
|---|---|
| Protects and controls data | Hides implementation complexity |
| Focuses on data + access | Focuses on essential behavior |
| Commonly uses `private` fields and methods | Commonly uses abstract classes/interfaces |
| Controls access | Hides unnecessary implementation details |

### Easy memory trick

```text
Encapsulation → HOW data is protected
Abstraction   → WHAT details are exposed
```

---

# 16. Encapsulation vs Inheritance

These concepts solve different problems.

### Encapsulation

```java
class Student {

    private int marks;
}
```

Protects the object's internal state.

### Inheritance

```java
class Dog extends Animal {
}
```

Allows a class to inherit properties and behavior from another class.

### Remember

```text
Encapsulation → Protect / Control
Inheritance   → Reuse / Extend
```

---

# 17. Encapsulation vs Polymorphism

### Polymorphism

Allows one reference or interface to represent different implementations.

Example:

```java
Animal a = new Dog();

a.sound();
```

The actual implementation of `sound()` can depend on the object's runtime type.

### Encapsulation

Controls access to an object's internal state.

```text
Encapsulation → How data is protected
Polymorphism  → How behavior can vary
```

---

# 18. Four Pillars of OOP

Encapsulation is one of the four fundamental pillars of Java OOP.

```text
                 OOP
                  |
      ┌───────────┼───────────┐
      ↓           ↓           ↓
Encapsulation  Inheritance  Polymorphism
      |
      ↓
Abstraction
```

A cleaner way to remember all four:

| Pillar | Main Purpose |
|---|---|
| Encapsulation | Protect and control data |
| Abstraction | Hide unnecessary implementation details |
| Inheritance | Reuse and extend existing functionality |
| Polymorphism | Allow the same interface to behave differently |

---

# 19. Important Interview Questions

## Q1. What is encapsulation in Java?

**Answer:**

> Encapsulation is an OOP principle that bundles data and the methods operating on that data inside a class while restricting direct access to the data and providing controlled access through methods.

---

## Q2. How is encapsulation achieved in Java?

**Answer:**

> Encapsulation is commonly achieved by declaring fields as `private` and providing controlled access through public methods such as getters, setters, or business methods. Validation can be added inside these methods to maintain a valid object state.

---

## Q3. Why are variables declared private?

**Answer:**

> Variables are declared private to prevent direct access and modification from outside the class. This allows the class to control how its internal state is accessed and changed.

---

## Q4. Are getters and setters necessary for encapsulation?

**Answer:**

> No. Getters and setters are common ways to provide controlled access, but they are not mandatory. A class should expose only the operations that make sense for its data.

---

## Q5. What is data hiding?

**Answer:**

> Data hiding is the practice of restricting direct access to an object's internal data. In Java, this is commonly achieved using the `private` access modifier.

---

## Q6. What is the relationship between encapsulation and data hiding?

**Answer:**

> Data hiding is one mechanism used to achieve encapsulation. Encapsulation is the broader concept of bundling data and behavior together while controlling access to the object's internal state.

---

# 20. Best Example to Remember

The **BankAccount** example is excellent for interviews:

```java
class BankAccount {

    private double balance;

    public void deposit(double amount) {

        if (amount > 0) {
            balance += amount;
        }
    }

    public void withdraw(double amount) {

        if (amount > 0 && amount <= balance) {
            balance -= amount;
        }
    }

    public double getBalance() {
        return balance;
    }
}
```

### Why is this encapsulation?

```text
balance
   ↓
private
   ↓
Cannot be directly accessed
   ↓
deposit(), withdraw(), getBalance()
   ↓
Controlled access
   ↓
Validation
```

The object's internal state is protected, while useful operations are exposed.

---

# 21. Final Mental Model

Whenever you see:

```java
class Student {

    private int marks;

    public void setMarks(int marks) {

        if (marks >= 0 && marks <= 100) {
            this.marks = marks;
        }
    }

    public int getMarks() {
        return marks;
    }
}
```

Think:

```text
                CLASS
                  |
          ┌───────┴───────┐
          ↓               ↓
        DATA           METHODS
          |               |
     private marks    getMarks()
                      setMarks()
                          |
                          ↓
                     Validation
                          |
                          ↓
                   Controlled Access
```

### The core idea

> **Don't let outside code directly control your object's internal state. Let the object control how its data is accessed and changed.**

---

# 22. One-Line Revision

> **Encapsulation = wrapping data and related methods inside a class + hiding the data using access control + providing controlled access through methods.**

### Short formula

```text
ENCAPSULATION
=
DATA HIDING
+
CONTROLLED ACCESS
+
DATA + RELATED METHODS
```

---

## Quick Revision Example

```java
class Student {

    private int marks;

    public void setMarks(int marks) {

        if (marks >= 0 && marks <= 100) {
            this.marks = marks;
        }
    }

    public int getMarks() {
        return marks;
    }
}
```

### Remember:

- `private` → hides the data
- `public` methods → provide controlled access
- Getter → reads data
- Setter → modifies data
- Validation → prevents invalid state
- Class → bundles data and behavior
- Encapsulation → protects and controls the object's state
