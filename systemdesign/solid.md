# 🧱 SOLID Principles in Object-Oriented Design

The **SOLID** principles are a set of five design principles intended to make software designs more understandable, flexible, and maintainable. These principles are the foundation of clean object-oriented software architecture.

---

## 🔠 What is SOLID?

SOLID is an acronym representing:

- **S** – Single Responsibility Principle
- **O** – Open/Closed Principle
- **L** – Liskov Substitution Principle
- **I** – Interface Segregation Principle
- **D** – Dependency Inversion Principle

---

## 1. 🧍 Single Responsibility Principle (SRP)

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
