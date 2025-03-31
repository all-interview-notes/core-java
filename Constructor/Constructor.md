**Java Constructors and Important Concepts**

---

## **1. Default and Parameterized Constructors**

### **Definition**
A constructor is a special method in Java that is automatically called when an object is created. It initializes the object's properties.

- **Default Constructor**: A constructor without parameters.
- **Parameterized Constructor**: A constructor that takes arguments to initialize an object with specific values.

```java
class Object {
    Object() {
        System.out.println("Object Default constructor called");
    }
    Object(int a, int b) {
        System.out.println("Object Parameterized constructor called with a: " + a + " b: " + b);
    }
}
class Student extends Object {
    Student() {
        super(20, 30); // Calls parameterized constructor of Object class
        System.out.println("Student Default constructor called");
    }
}
public class Main {
    public static void main(String[] args) {
        Student s1 = new Student();
    }
}
```

**Output:**

```
Object Parameterized constructor called with a: 20 b: 30
Student Default constructor called
```

---

## **2. `this` Keyword Example**

### **Definition**
- `this` keyword refers to the current instance of the class.
- It is used to differentiate between instance variables and parameters.

```java
class Program1 {
    int a = 10; // Instance variable in Program1

    void disp() {
        System.out.println("Program1 a: " + a);
    }
}

class Program2 extends Program1 {
    int a = 20; // Instance variable in Program2

    void disp() {
        System.out.println("Program2 a: " + a);
        System.out.println("Using super.a to access Program1's a: " + super.a);
    }
}

public class Main {
    public static void main(String[] args) {
        Program2 obj = new Program2();
        obj.disp();
    }
}
```

**Output:**

```
Program2 a: 20
Using super.a to access Program1's a: 10
```

---

## **3. `super` Keyword Example**

### **Definition**
- `super` is used to refer to the immediate parent class.
- It helps in accessing parent class variables and methods.

```java
class Program1 {
    int a = 10; // Instance variable in Program1

    void disp() {
        System.out.println("Program1 a: " + a);
    }
}

class Program2 extends Program1 {
    int a = 20; // Instance variable in Program2

    void disp() {
        System.out.println("Program2 a: " + a);
        System.out.println("Using super.a to access Program1's a: " + super.a);
    }
}

public class Main {
    public static void main(String[] args) {
        Program2 obj = new Program2();
        obj.disp();
    }
}
```

**Output:**

```
Program2 a: 20
Using super.a to access Program1's a: 10
```

---

## **4. Copy Constructor**

### **Definition**
A copy constructor is used to create a new object by copying values from an existing object.

```java
class Student {
    String name;
    int age;

    // Normal Constructor
    Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // Copy Constructor
    Student(Student s) {
        this.name = s.name;
        this.age = s.age;
    }

    void display() {
        System.out.println("Name: " + name + ", Age: " + age);
    }
}

public class Main {
    public static void main(String[] args) {
        Student s1 = new Student("Alice", 20); // Original object
        Student s2 = new Student(s1);          // Copy object using copy constructor

        s1.display();
        s2.display();
    }
}
```

**Output:**

```
Name: Alice, Age: 20
Name: Alice, Age: 20
```

---

## **5. Private Constructor & Singleton Pattern**

### **Definition**
- A **private constructor** prevents the creation of multiple instances of a class.
- Used in **Singleton Pattern**, where only one instance of the class exists.

```java
class Singleton {
    private static Singleton instance; // Single instance

    // Private Constructor
    private Singleton() {
        System.out.println("Private Constructor Called");
    }

    // Static method to get the only instance
    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}

public class Main {
    public static void main(String[] args) {
        Singleton obj1 = Singleton.getInstance(); // ✅ Allowed
        Singleton obj2 = Singleton.getInstance();

        System.out.println(obj1 == obj2); // Output: true (Both are the same instance)
    }
}
```

**Output:**

```
Private Constructor Called
true
```

---

## **6. Constructor Chaining**

### **Definition**
- Constructor chaining allows one constructor to call another constructor in the same or parent class.

```java
class A {
    A() {
        System.out.println("Constructor A called");
    }
}

class B extends A {
    B() {
        super(); // Calls parent class constructor
        System.out.println("Constructor B called");
    }
}

public class Main {
    public static void main(String[] args) {
        B obj = new B();
    }
}
```

**Output:**

```
Constructor A called
Constructor B called
```

---

## **7. Anonymous Object**

```java
class Student {
    void study() {
        System.out.println("Student is studying.");
    }
}

public class Main {
    public static void main(String[] args) {
        new Student().study(); // Anonymous object
    }
}
```

**Output:**

```
Student is studying.
```

---

## **8. Actual vs Formal Parameters**

```java
public class Main {
    static void add(int a, int b) { // Formal parameters
        System.out.println("Sum is: " + (a + b));
    }
    public static void main(String[] args) {
        add(10, 20); // Actual parameters
    }
}
```

**Output:**

```
Sum is: 30
```

