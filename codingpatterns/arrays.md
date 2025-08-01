# 🔢 Array Operations: Deletion & Dynamic Expansion

This guide explains how to handle **element deletion** in arrays and how to **add new elements** once an array reaches its maximum capacity. These operations are crucial for building dynamic, scalable data structures.

---

## 🗑️ Deleting an Element from an Array

### ✅ Problem Statement
Given a fixed-size array, delete the element at a specified index and maintain the remaining element order.

### 🧠 Design Approach
- Shift all elements one position to the left after the deletion index.
- Optionally set the last position to a default value (`0`, `null`, etc.).


