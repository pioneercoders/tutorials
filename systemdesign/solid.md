#### 🧱 SOLID Principles in Object-Oriented Design

The **SOLID** principles are a set of five design principles intended to make software designs more understandable, flexible, and maintainable. These principles are the foundation of clean object-oriented software architecture.

**🔠 What is SOLID?**

SOLID is an acronym representing:

- **S** – Single Responsibility Principle
- **O** – Open/Closed Principle
- **L** – Liskov Substitution Principle
- **I** – Interface Segregation Principle
- **D** – Dependency Inversion Principle

---

**1. 🧍 Single Responsibility Principle (SRP)**

**A class should have only one reason to change.**

### ✅ Good Design
Each class or module should focus on a **single task or responsibility**.

### ❌ Bad Example
```java
class UserService {
    void registerUser() { ... }
    void generateReport() { ... } // violates SRP
}
```

✅ Good Example

```java
class Employee {
    public void calculateSalary() { /* logic */ }
}

class EmployeeRepository {
    public void save(Employee employee) { /* logic */ }
}
```

**O - Open/Closed Principle (OCP)**
Software entities should be open for extension but closed for modification.
❌ Bad Example

```java
class NotificationService {
    public void send(String type) {
        if (type.equals("email")) {
            // send email
        } else if (type.equals("sms")) {
            // send sms
        }
    }
}
```
**✅ Good Example**
```java
interface Notification {
    void send();
}

class EmailNotification implements Notification {
    public void send() {
        // send email
    }
}

class SMSNotification implements Notification {
    public void send() {
        // send SMS
    }
}

class NotificationService {
    public void notifyUser(Notification notification) {
        notification.send();
    }
}
```
**L - Liskov Substitution Principle (LSP)**
Subtypes must be substitutable for their base types without altering correctness.
❌ Bad Example
```java
class Bird {
    public void fly() {}
}

class Ostrich extends Bird {
    public void fly() {
        throw new UnsupportedOperationException();
    }
}
```

✅ Good Example
```java
interface Bird {}

interface FlyingBird extends Bird {
    void fly();
}

class Sparrow implements FlyingBird {
    public void fly() { /* logic */ }
}

class Ostrich implements Bird {
    // Doesn't implement fly
}
```

**I - Interface Segregation Principle (ISP)**
Clients should not be forced to depend on methods they do not use.
❌ Bad Example

```java
interface Worker {
    void work();
    void eat();
}

class Robot implements Worker {
    public void work() {}
    public void eat() {
        throw new UnsupportedOperationException();
    }
}
```
✅ Good Example
```java
interface Workable {
    void work();
}

interface Eatable {
    void eat();
}

class Human implements Workable, Eatable {
    public void work() {}
    public void eat() {}
}

class Robot implements Workable {
    public void work() {}
}
```

**D - Dependency Inversion Principle (DIP)**
High-level modules should not depend on low-level modules. Both should depend on abstractions.
❌ Bad Example
```java
class MySQLDatabase {
    public void connect() {}
}

class DataManager {
    MySQLDatabase db = new MySQLDatabase();
    public void loadData() {
        db.connect();
    }
}
```

✅ Good Example
```java
interface Database {
    void connect();
}

class MySQLDatabase implements Database {
    public void connect() {}
}

class DataManager {
    private Database db;

    public DataManager(Database db) {
        this.db = db;
    }

    public void loadData() {
        db.connect();
    }
}
```

✅ Summary
| Principle | Description                                   |
| --------- | --------------------------------------------- |
| SRP       | One class, one responsibility                 |
| OCP       | Open for extension, closed for modification   |
| LSP       | Subclasses should be substitutable for parent |
| ISP       | Use small, specific interfaces                |
| DIP       | Depend on abstractions, not concrete classes  |




