# Object-Oriented Programming (OOP) Notes

## Table of Contents

- [🧠 OOP Overview](#-oop-overview)
- [🔧 Core OO Concepts](#-core-oo-concepts)
- [📦 Encapsulation](#-encapsulation)
- [🔐 Data Hiding](#-data-hiding)
- [🎭 Abstraction](#-abstraction)
- [📐 OO Principles](#-oo-principles)
- [🧰 Design Patterns](#-design-patterns)
- [🔎 OOA vs OOD vs OOP](#-ooa-vs-ood-vs-oop)
- [🏗️ Constructors & Destructors](#️-constructors--destructors)
- [📌 Const, Static, and Friend](#-const-static-and-friend)
- [👪 Inheritance](#-inheritance)
- [🔀 Polymorphism](#-polymorphism)
- [➕ Operator Overloading](#-operator-overloading)
- [🧠 Memory Notes](#-memory-notes)
- [📚 Exam Notes](#-exam-notes)
- [🎓 Interview Questions](#-interview-questions)

---

## 🧠 OOP Overview

### 🌐 OO Paradigm

A **way of thinking / structuring** programs based on:

- **Objects**
- **Functions**
- Their **interactions**

---

## 🔧 Core OO Concepts

- **Class**
- **Object**
- **Encapsulation**
- **Abstraction**
- **Polymorphism**
- **Inheritance**

---

## 📦 Encapsulation

> **Encapsulation = Capsule**

Group data members + member functions inside a **single capsule (class)**.

---

## 🔐 Data Hiding

- Use **access modifiers**: `public` / `private`
- **Private section** hides details from the user
- **Good design**: reveal as little as possible

### ✅ Why Data Hiding?

- Prevent corruption of data
- Protect object integrity
- Reduces system complexity

### 🆚 Data Hiding vs. Encapsulation

| Concept | Description |
|---------|-------------|
| **Encapsulation** | Mechanism for wrapping code and data into a single unit |
| **Data Hiding** | Prevents access to implementation details (via `private`) |

- Encapsulation can exist without data hiding (e.g. structs)
- Data hiding **requires** encapsulation

---

## 🎭 Abstraction

> Focus on **what** an object does, not **how**.

- Hide **unwanted** details, show **essential** ones
- **Separate interface (what) from implementation (how)**
- Only expose **relevant functionality**
- Many "how" implementations later (polymorphism)

### 🧩 Accessors & Mutators

- **Accessor (Getter):** Read-only access
- **Mutator (Setter):** Change internal data

### ⚠️ Tips

- Don't auto-generate setters/getters for everything
- Setters can inject wrong data
- Getters may expose implementation
- **Best practice:** Let object do the work, not expose raw data

> *"Don't ask for info to do the work; ask the object to do it."* – Allen Holub

---

## 📐 OO Principles

### 🔷 SOLID Principles

- **S** – Single Responsibility (SRP)
- **O** – Open/Closed Principle (OCP)
- **L** – Liskov Substitution (LSP)
- **I** – Interface Segregation (ISP)
- **D** – Dependency Inversion (DIP)

### 💡 Other Principles

- **DRY** – Don't Repeat Yourself
- **KISS** – Keep it Simple, Stupid!
- **YAGNI** – You Ain't Gonna Need It

---

## 🧰 Design Patterns

> Solutions to **common software problems**

- Used for repetitive design challenges
- Examples: **Singleton**, **Factory**, etc.
- [🔗 Ref: 7 Most Important Patterns](https://learningdaily.dev/the-7-most-important-software-design-patterns-d60e546afb0e)

---

## 🔎 OOA vs OOD vs OOP

| Phase | Description |
|-------|-------------|
| **OOA** (Object-Oriented Analysis) | Analysis phase for requirements<br/>📤 Output: Use cases + Object conceptual model (tech-independent) |
| **OOD** (Object-Oriented Design) | Design phase<br/>🎯 Takes hardware/software, scalability, budget, etc. into account |
| **OOP** (Object-Oriented Programming) | Implementation phase<br/>🛠 Uses specific OOP languages and features |

---

## 🏗️ Constructors & Destructors

### Constructor

A **constructor** is a special method in a class that runs automatically when you create an object.

- Its job: initialize fields or set up the object
- It has **the same name as the class** and doesn't have a return type
- **Default Constructor**: No parameters
- **Parameterized Constructor**: With parameters

### Destructor

- Auto-called when object goes out of scope
- Used to release memory (e.g. delete pointers)

### 🔁 Copy Constructor

#### Types

- **Shallow Copy** → Same memory (dangerous)
- **Deep Copy** → Own independent memory (safe)

#### Uses

- Initialize one object from another
- Pass object **by value** to a function
- Return object from function

---

## 📌 Const, Static, and Friend

### 🧊 Const

| Declaration | Can Modify? | Meaning |
|-------------|-------------|---------|
| `const Rectangle* ptr` | ❌ Data<br/>✅ Pointer | Pointer to const data |
| `Rectangle* const ptr` | ✅ Data<br/>❌ Pointer | Const pointer to modifiable data |
| `const Rectangle* const ptr` | ❌ Data<br/>❌ Pointer | Const pointer to const data |

- `const` before function = won't modify member variables
- `const` before object = can only call const methods
- ❗ Avoid `const` member variables (not recommended)

### 📍 Static

- **Static Variable**: Shared among all instances
  - Exists even if no object is created
  - Must define it outside the class
- **Static Function**: Can access static members only

### 🔓 Friend

- **Friend Class**: Can access private members of another class
- **Friend Function**: Only specific function has access to private members

---

## 👪 Inheritance

- **Overloading**: Same class, same name, **different parameters**
- **Overriding**: Superclass ↔ Subclass, same name, **same parameters**

```cpp
class Child : private Base  // => member variables become in private section for child class
```

---

## 🔀 Polymorphism

> "Many Forms"

- Method is resolved based on **pointer type**
- If function is marked **virtual**, it checks the **object's actual type**

### ✅ Use Case

- Write **generic code**
- Use **pure virtual** functions for incomplete classes

```cpp
virtual int area() = 0;
```

> Such a class **can't** have an object instantiated

---

## ➕ Operator Overloading

> Extend built-in operators (like +, -, ==) to work with your custom class objects

### Example:

```cpp
class Complex {
  int real, imag;
public:
  Complex(int r = 0, int i = 0) : real(r), imag(i) {}
  
  Complex operator + (const Complex& obj) {
    return Complex(real + obj.real, imag + obj.imag);
  }
};
```

### 🔑 Key Points:

- Function name: `operator+`, `operator-`, etc.
- Must be a **member** or **friend** function
- You can't overload:
  - `.` (dot)
  - `::` (scope resolution)
  - `.*` (pointer to member)
  - `sizeof`
  - `?:` (ternary)

---

## 🧠 Memory Notes

- **Member Variables** are **per-object** (each object has its own copy)
- **Member Functions** are **shared** (only one copy in memory)

---

## 📚 Exam Notes

### C++ Default Arguments Rule

**Rule:** Once you provide a default value for a parameter, ALL subsequent parameters (to the right) must also have default values.

#### ❌ Invalid:

```cpp
void myFunc(int x=3, int y);  // Error: y has no default after x
```

#### ✅ Valid:

```cpp
void myFunc(int x, int y=5);        // OK: default only at end
void myFunc(int x=3, int y=5);      // OK: all after first default have defaults
void myFunc(int x=3);               // OK: only one parameter
```

#### Why?

Prevents ambiguity in function calls:

- `myFunc(5)` would be unclear with `myFunc(int x=3, int y)`
- Is it `myFunc(5, ?)` or `myFunc(3, 5)`? 🤔

---

### C++ Copy Constructor Signature

**Standard Signature:**

```cpp
ClassName(const ClassName& other);
```

#### Key Points:

- **Parameter:** Must be a **reference** (`&`) to avoid infinite recursion
- **const:** Should be `const` since we're only reading from the source object
- **Same class:** Parameter type must be the same class

#### ✅ Correct Examples:

```cpp
class Student {
public:
    Student(const Student& other);        // Standard copy constructor
    Student(const Student& s);            // Different parameter name, still correct
};
```

#### ❌ Incorrect Examples:

```cpp
class Student {
public:
    Student(Student other);               // Error: pass by value causes infinite recursion
    Student(Student& other);              // Works but not const-correct
    Student(const Student* other);        // Error: pointer instead of reference
};
```

#### Why Reference?

- Pass by value would call the copy constructor → infinite recursion
- Reference allows direct access to the original object without copying

---

### C++ Pointer vs Object Constructor

**Key Point:** Pointers don't automatically create objects!

```cpp
class M {
    N* ptr;  // Just a pointer - N's constructor NOT called
public:
    M() { /* Only M's constructor runs */ }
};
```

**Constructor of N runs only when:**

- `ptr = new N();` (explicit object creation)
- `N obj;` (direct object declaration)

**Remember:** Pointer declaration ≠ Object creation

> **Note:** You can inherit from a class with a private constructor **only if** the derived class is marked as a `friend`. Otherwise, it won't compile.

---

### Static Members Rule

**Static variables must be defined outside the class, not in constructors.**

#### Wrong ❌

```cpp
class Parent {
    static int z;
public:
    Parent() { z = 0; }  // Compilation error
};
```

#### Right ✅

```cpp
class Parent {
    static int z;
};
int Parent::z = 0;  // Define outside class
```

**Why:** Static members belong to the class, not instances. Constructors can't initialize class-wide data.

---

### Access Table: Full Compilation

| Access Specifier in Base | Inheritance Type | Accessible in Base | Accessible in Child | Accessible in `main()` |
|--------------------------|------------------|-------------------|---------------------|------------------------|
| **private** | public | ✅ Yes | ❌ No | ❌ No |
| **private** | protected | ✅ Yes | ❌ No | ❌ No |
| **private** | private | ✅ Yes | ❌ No | ❌ No |
| **protected** | public | ✅ Yes | ✅ Yes | ❌ No |
| **protected** | protected | ✅ Yes | ✅ Yes | ❌ No |
| **protected** | private | ✅ Yes | ✅ Yes | ❌ No |
| **public** | public | ✅ Yes | ✅ Yes | ✅ Yes |
| **public** | protected | ✅ Yes | ✅ Yes | ❌ No |
| **public** | private | ✅ Yes | ✅ Yes | ❌ No |

---

### Class Relationships Summary

- **Association:** One class uses or refers to another. Both can exist independently.  
  *Example:* Teacher uses Students.

- **Aggregation:** A whole-part relationship where parts can exist independently of the whole.  
  *Example:* Library has Books (Books can exist without Library).

- **Composition:** A strong whole-part relationship where parts cannot exist without the whole.  
  *Example:* House is composed of Rooms (Rooms don't exist if House is destroyed).

- **Inheritance:** One class inherits from another, representing an "is-a" relationship.  
  *Example:* Dog is an Animal.

---

### Nested Classes in C++

#### Definition
A **nested class** is defined inside another class.  
It does **not** auto-access the outer class's private members (and vice versa) unless `friend` is used.

#### Syntax
```cpp
class Outer {
public:
    class Inner { };
};
Outer::Inner obj;
```

#### Key Points
- Access via `Outer::Inner`
- `public` affects visibility, not access rights
- Use `friend` to allow private/protected access

#### Access Rules
- No `friend` → ❌ No private access
- `friend class Inner` in Outer → ✅ Inner can access Outer's private members
- `friend class Outer` in Inner → ✅ Outer can access Inner's private members

#### Example
```cpp
class Outer {
private: 
    int secret = 42;
public:
    friend class Inner;
    class Inner { 
    public: 
        void show(Outer& o) { 
            cout << o.secret; 
        } 
    };
};
```

✅ **Exam Tip:** Nested ≠ automatic access. Use `friend` if needed.

---

## 🎓 Interview Questions

### Virtual Destructor

**Virtual Destructor – Short Note**  
A **virtual destructor** ensures that when deleting a derived object through a base class pointer, **both the derived and base destructors** run in the correct order.  
Use it in base classes meant for **polymorphism** to avoid resource leaks.

#### Example:

```cpp
class Base { 
public: 
    virtual ~Base() {} 
};

class Derived : public Base { 
public: 
    ~Derived() {} 
};

Base* obj = new Derived();
delete obj; // calls Derived::~Derived(), then Base::~Base()
```

**Rule:** Always make base destructors `virtual` if the class will be used **polymorphically**.

---

### ❓ Interview Question

> What happens if you delete a derived object through a base pointer without a virtual destructor?

### 💡 Answer

If a base class destructor is **not** declared `virtual` and you delete a derived object through a base pointer:

1. **Only the base destructor runs** – the derived destructor is skipped
2. **Memory for the whole object is still freed**, so there's no guaranteed memory leak *unless* the derived class manages dynamic resources
3. **This is undefined behavior** in C++, and can cause resource leaks (e.g., file handles, sockets, heap memory)

#### ✅ Correct Practice

If a class will be used polymorphically, **always** make its destructor `virtual`, even if empty:

```cpp
class Base {
public:
    virtual ~Base() {}
};

class Derived : public Base {
public:
    ~Derived() {}
};

Base* obj = new Derived();
delete obj; // Calls Derived::~Derived(), then Base::~Base()
```

#### 📝 Key Points for Interview

- Without `virtual`, only the base destructor runs
- With `virtual`, the **entire destructor chain** runs in the correct order
- It prevents subtle, hard-to-detect resource leaks