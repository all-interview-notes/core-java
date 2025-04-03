### **Polymorphism in Java**

#### **What is Polymorphism?**
Polymorphism in Java is the ability of an object to take many forms. It allows a single method, interface, or class to operate in different ways based on the context. There are two main types of polymorphism:

1. **Compile-time Polymorphism (Method Overloading)**
2. **Runtime Polymorphism (Method Overriding)**

---

### **Method Overloading**
**Definition:**
Method Overloading is a process where multiple methods have the same name but different parameters within the same class.

**Key Points:**
- It happens in the same class.
- The method name remains the same, but the parameters (number, type, or both) differ.
- It is an example of **Compile-time Polymorphism**.
- It does not require inheritance.

**Example:**
```java
class MathOperations {
    int add(int a, int b) {
        return a + b;
    }
    double add(double a, double b) {
        return a + b;
    }
}
```

---

### **Method Overriding**
**Definition:**
Method Overriding is a process where a method from the parent class is redefined in the child class with the same name and parameters but a different implementation.

**Key Points:**
- It happens in different classes (parent-child relationship).
- The method name and parameters remain the same, but the implementation is different.
- It is an example of **Runtime Polymorphism**.
- Inheritance is required.

**Example:**
```java
class Parent {
    void show() {
        System.out.println("This is the parent class.");
    }
}
class Child extends Parent {
    void show() {
        System.out.println("This is the child class.");
    }
}
```

---

### **Difference Between Method Overloading and Method Overriding**

| Feature           | Method Overloading | Method Overriding |
|------------------|------------------|------------------|
| **Definition**   | Multiple methods with the same name but different parameters. | Redefining a method from the parent class in the child class. |
| **Where It Occurs** | Within the same class. | In a parent-child class relationship. |
| **Parameters**   | Must be different. | Must be the same. |
| **Return Type**  | Can be different. | Must be the same (or a covariant return type). |
| **Inheritance**  | Not required. | Required. |
| **Polymorphism Type** | Compile-time Polymorphism. | Runtime Polymorphism. |

---

### **Rules of Method Overriding**
1. **Access Modifiers:**
   - The access modifier of the overridden method in the child class **must be the same or more accessible** than the parent class method.
   - Example: If the parent method is `protected`, the child method can be `protected` or `public`, but **not** `private`.
   - **Private methods cannot be overridden.**

2. **Return Type:**
   - The return type must be **the same** or a **covariant return type** (i.e., a subclass of the parent class's return type).
   - Example:
     ```java
     class Parent {
         Parent display() { return new Parent(); }
     }
     class Child extends Parent {
         Child display() { return new Child(); }
     }
     ```

3. **Final Methods:**
   - Methods declared as `final` in the parent class **cannot** be overridden.

4. **Static Methods:**
   - Static methods **cannot be overridden**; they are method-hidden instead.

5. **Constructor Overriding:**
   - **Constructors cannot be overridden**, but they can be accessed using `super()` in the child class.

6. **Exception Handling:**
   - If the parent method declares an exception, the child class method **can only declare the same exception or its subclass**.

**Examples of Method Overriding Rules:**

1. **Access Modifier Rule** (Valid Overriding):
```java
class Program1 {
    protected void display() {
        System.out.println("Parent class method");
    }
}
class Program2 extends Program1 {
    public void display() { // Allowed: Increasing visibility
        System.out.println("Child class method");
    }
}
```

2. **Private Method Overriding (Invalid - Compilation Error):**
```java
class Parent {
    private void display() {
        System.out.println("Parent class method");
    }
}
class Child extends Parent {
    void display() { // Error: Cannot override a private method
        System.out.println("Child class method");
    }
}
```

3. **Final Method Overriding (Invalid - Compilation Error):**
```java
class Parent {
    final void show() {
        System.out.println("Final method in Parent");
    }
}
class Child extends Parent {
    void show() { // Error: Cannot override final method
        System.out.println("Trying to override final method");
    }
}
```

4. **Static Method Overriding (Not Allowed - Method Hiding Instead):**
```java
class Parent {
    static void display() {
        System.out.println("Static method in Parent");
    }
}
class Child extends Parent {
    static void display() { // This is method hiding, not overriding
        System.out.println("Static method in Child");
    }
}
```

---

### **Key Takeaways:**
- **Method Overloading** allows multiple methods with the same name but different parameters.
- **Method Overriding** allows a child class to modify a method from the parent class.
- **Overriding requires inheritance**, while overloading does not.
- **Rules of Overriding** ensure proper method redefinition, including access modifiers, return types, and exceptions.

🚀 **Understanding these concepts is crucial for mastering Java's OOP principles!**



![image](https://github.com/user-attachments/assets/84c6ad91-51ef-4a42-ac94-6c0b5515e2e0)

### **Polymorphism and Casting in Java**  

#### **1. What is Casting?**  
Casting is the process of creating a child object and assigning it to a parent type reference variable. This allows us to use a child class object with a reference of its parent class.

#### **2. What is Polymorphism?**  
Polymorphism means "many forms." It allows one interface (or method) to be used for different types of objects. In Java, polymorphism is achieved through **method overriding** and **upcasting**.

#### **3. Types of Casting in Java**  
- **Upcasting (Implicit Casting)**: Assigning a child class object to a parent class reference.
- **Downcasting (Explicit Casting)**: Assigning a parent class reference back to a child class object (requires explicit casting).

#### **4. Advantages of Polymorphism**  
- **Code Flexibility**: A single reference type can be used to call different child class methods.
- **Code Reusability**: No need to write separate code for each child class.
- **Extensibility**: New child classes can be added without modifying existing code.

#### **5. Example of Polymorphism using Upcasting and Method Overriding**  
```java
// Parent class
class Teacher {
    void teach() {
        System.out.println("Teaching general subjects");
    }
    
    void project() {
        System.out.println("Guiding a general project");
    }
}

// Child class: JavaTeacher
class JavaTeacher extends Teacher {
    @Override
    void teach() {
        System.out.println("Teaching Java");
    }
    
    @Override
    void project() {
        System.out.println("Guiding a Java project");
    }
}

// Child class: SQLTeacher
class SQLTeacher extends Teacher {
    @Override
    void teach() {
        System.out.println("Teaching SQL");
    }
    
    @Override
    void project() {
        System.out.println("Guiding an SQL project");
    }
}

// Main Application class
public class TeacherApp {
    public static void main(String[] args) {
        // Upcasting: Parent class reference holding a child class object
        Teacher t1 = new JavaTeacher();
        t1.teach();  // Calls overridden method of JavaTeacher
        t1.project();

        Teacher t2 = new SQLTeacher();
        t2.teach();  // Calls overridden method of SQLTeacher
        t2.project();
    }
}
```
#### **6. Explanation of the Code**  
- **Upcasting is used** (`Teacher t1 = new JavaTeacher();`).
- **Method Overriding is used** (Child classes override the `teach()` and `project()` methods).
- The **parent class reference** calls methods from the child class dynamically.

### **Conclusion**  
- **Casting** helps in achieving **polymorphism** in Java.
- **Polymorphism increases flexibility** by allowing a single reference type to call different implementations of methods.
- **Method Overriding** ensures that child class implementations are used dynamically.

```
// Parent class
class Teacher {
    void teach() {
        System.out.println("Teaching general subjects");
    }
    
    void project() {
        System.out.println("Guiding a general project");
    }
}

// Child class: JavaTeacher
class JavaTeacher extends Teacher {
    @Override
    void teach() {
        System.out.println("Teaching Java");
    }
    
    @Override
    void project() {
        System.out.println("Guiding a Java project");
    }
}

// Child class: SQLTeacher
class SQLTeacher extends Teacher {
    @Override
    void teach() {
        System.out.println("Teaching SQL");
    }
    
    @Override
    void project() {
        System.out.println("Guiding an SQL project");
    }
}

// Main Application class
public class TeacherApp {
    // Static method to call Teacher references
    static void teacherInfo(Teacher teacher) {
        teacher.teach();
        teacher.project();
    }
    
    public static void main(String[] args) {
        // Calling static method with different teacher objects
        teacherInfo(new JavaTeacher());
        teacherInfo(new SQLTeacher());
    }
}
```

### **Polymorphism, Casting, and Downcasting in Java**

#### **1. What is Downcasting?**

Downcasting is the process of converting a parent class reference to a child class reference explicitly. This allows access to child-specific methods that are not available in the parent class.

- **Instance of Operator (********`instanceof`********\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*)**: Before performing downcasting, the `instanceof` operator is used to check if an object belongs to a particular class. This prevents runtime errors such as `ClassCastException`.

#### **2. Example of Downcasting in Java**

```java
// Parent class
class Developer {
    void project() {
        System.out.println("Working on a project");
    }
    
    void attendMeeting() {
        System.out.println("Attending a developer meeting");
    }
}

// Child class: BackendDeveloper
class BackendDeveloper extends Developer {
    void backendTeam() {
        System.out.println("Working with backend team");
    }
    
    @Override
    void project() {
        System.out.println("Developing backend services");
    }
}

// Main Application class
public class DeveloperApp {
    public static void main(String[] args) {
        // Upcasting: Parent reference holding a child class object
        Developer dev = new BackendDeveloper();
        dev.attendMeeting(); // Calls inherited method
        dev.project();  // Calls overridden method
        
        // Trying to call child-specific method (not accessible with parent reference)
        // dev.backendTeam();  // This will cause a compilation error
        ((BackendDeveloper)(dev)).backendTeam();
        // Downcasting: Converting parent reference back to child reference
        if (dev instanceof BackendDeveloper) {
            BackendDeveloper backendDev = (BackendDeveloper) dev;
            backendDev.backendTeam(); // Now we can call child-specific method
        }
    }
}
```

#### **3. Explanation of the Code**

- **Upcasting is performed** (`Developer dev = new BackendDeveloper();`).
- **Inherited method ************************`attendMeeting()`************************ is called** from the parent class.
- **Overridden method ************************`project()`************************ is called**, which executes the child class's version.
- **Directly calling ************************`backendTeam()`************************ using ************************`dev`************************ is not possible**, as `dev` is a `Developer` type.
- **Downcasting is performed** using explicit casting (`(BackendDeveloper) dev`), allowing access to `backendTeam()`.
- **`instanceof`**\*\* operator ensures safe downcasting\*\*, preventing runtime exceptions.

### **4. Conclusion**

- **Downcasting enables access to child-specific methods** when using parent-type references.
- **`instanceof`**\*\* operator helps prevent \*\*\*\*`ClassCastException`\*\*.
- **Method overriding ensures that the correct method is invoked at runtime**, even with an upcasted reference.



```
// Parent class
class Developer {
    void project() {
        System.out.println("Working on a project");
    }
    
    void attendMeeting() {
        System.out.println("Attending a developer meeting");
    }
}

// Child class: BackendDeveloper
class BackendDeveloper extends Developer {
    void backendTeam() {
        System.out.println("Working with backend team");
    }
    
    @Override
    void project() {
        System.out.println("Developing backend services");
    }
}

// Child class: FrontendDeveloper
class FrontendDeveloper extends Developer {
    void frontendTeam() {
        System.out.println("Working with frontend team");
    }
    
    @Override
    void project() {
        System.out.println("Developing frontend applications");
    }
}

// Main Application class
public class DeveloperApp {
    // Static method to check developer type
    static void web(Developer dev) {
        dev.attendMeeting(); // Calls inherited method
        dev.project();  // Calls overridden method

        if (dev instanceof BackendDeveloper) {
            BackendDeveloper backendDev = (BackendDeveloper) dev;
            backendDev.backendTeam(); // Calls backend-specific method
        } else if (dev instanceof FrontendDeveloper) {
            FrontendDeveloper frontendDev = (FrontendDeveloper) dev;
            frontendDev.frontendTeam(); // Calls frontend-specific method
        }
    }
    
    public static void main(String[] args) {
        Developer backendDev = new BackendDeveloper();
        Developer frontendDev = new FrontendDeveloper();
        
        web(backendDev);
        web(frontendDev);
    }
}
```

### **Aggregation and Composition in Java**

#### **1. What is Aggregation?**
Aggregation is a process of achieving a "has-a" relationship between objects where they are loosely coupled. This means that one object can exist independently of the other. For example, a `Car` has an `Engine`, but the `Engine` can exist separately from the `Car`.

#### **2. Example of Aggregation in Java**
```java
// Aggregation Example: Driver and Car
class Car {
    String model;
    
    Car(String model) {
        this.model = model;
    }
}

class Driver {
    String name;
    Car car; // Aggregation: Driver has a Car
    
    Driver(String name, Car car) {
        this.name = name;
        this.car = car;
    }
    
    void showDetails() {
        System.out.println(name + " is driving " + car.model);
    }
}

public class AggregationExample {
    public static void main(String[] args) {
        Car car1 = new Car("Tesla Model S");
        Driver driver1 = new Driver("John", car1);
        driver1.showDetails();
    }
}
```

#### **3. Explanation of Aggregation Code**
- `Driver` and `Car` have a "has-a" relationship.
- The `Car` object can exist independently of the `Driver`.
- The `Driver` object contains a reference to the `Car` object, representing a loose coupling.

---

#### **4. What is Composition?**
Composition is a stronger form of aggregation where the contained object cannot exist independently. When the parent object is created or destroyed, the child object is also created or destroyed. For example, an `Engine` is an essential part of a `Vehicle`, and if the `Vehicle` is destroyed, the `Engine` is destroyed too.

#### **5. Example of Composition in Java**
```java
// Composition Example: Vehicle and Engine
class Engine {
    Engine() {
        System.out.println("Engine created");
    }
    void start() {
        System.out.println("Engine started");
    }
}

class Vehicle {
    private final Engine engine; // Composition: Vehicle has an Engine
    
    Vehicle() {
        engine = new Engine(); // Engine is created with Vehicle
    }
    
    void startVehicle() {
        engine.start();
        System.out.println("Vehicle is running");
    }
}

public class CompositionExample {
    public static void main(String[] args) {
        Vehicle vehicle = new Vehicle();
        vehicle.startVehicle();
    }
}
```

#### **6. Explanation of Composition Code**
- `Vehicle` and `Engine` have a strong "has-a" relationship.
- The `Engine` is part of the `Vehicle` and is created inside it.
- When the `Vehicle` is destroyed, the `Engine` is also destroyed.
- The `Engine` cannot exist independently of the `Vehicle`.

---

### **7. Differences Between Aggregation and Composition**
| Feature | Aggregation | Composition |
|---------|------------|------------|
| Relationship Type | Loosely Coupled | Strongly Coupled |
| Object Dependency | Child object can exist independently | Child object cannot exist independently |
| Example | Driver and Car | Vehicle and Engine |
| Lifecycle | Parent and child have independent lifecycles | Child depends on the parent’s lifecycle |

### **8. Conclusion**
- **Aggregation** allows objects to have independent existence while being associated.
- **Composition** creates a stronger dependency, ensuring that the child object only exists within the parent.
- Both concepts help in designing flexible and maintainable object-oriented applications.

![image](https://github.com/user-attachments/assets/e95ef50e-73b1-46db-bd61-c8d6c3692136)

### **Understanding Java Program Execution: JVM, Static, and Non-Static Elements**

#### **1. How Java Program Execution Starts**
- The execution starts when the **Operating System (OS)** sends control to the **Java Virtual Machine (JVM)**.
- The JVM loads the main class and passes control to the **Class Loader**.
- The **Class Loader** loads the class and initializes:
  - **Static variables**
  - **Static methods**
  - **Static blocks**
- The control is then passed back to the JVM, which:
  - Allocates memory for static variables.
  - Executes static blocks.
  - Executes the `main()` method.

#### **2. Rules for Static and Non-Static Elements**
- **Static variables** can be accessed inside static blocks, static methods, non-static methods, and constructors.
- **Non-static variables** can only be accessed inside non-static blocks, non-static methods, and constructors.
- **Non-static blocks** are executed before the constructor when an object is created.
- **Constructors** are executed after non-static blocks during object creation.
- **Static methods** belong to the class and can be accessed without creating an object.
- **Non-static methods** require an object instance to be accessed.

#### **3. Java Program Demonstrating Static and Non-Static Elements**
```java
// Main class
public class Main {
    public static void main(String[] args) {
        // Calling static method without object creation
        Program.display1(); 
        
        // Creating an object of Program class
        Program p = new Program();
        
        // Calling non-static method using object reference
        p.display2();
    }
}

// Program class
class Program {
    // Static variables
    static int a, b;
    
    // Static block - executes once when class is loaded
    static {
        System.out.println("Inside static block");
        a = 10;
        b = 20;
    }
    
    // Static method
    static void display1() {
        System.out.println("Inside static method display1()");
        System.out.println(a);
        System.out.println(b);
    }
    
    // Instance variables (Non-static variables)
    int x, y;
    
    // Non-static block - executes before constructor when object is created
    {
        System.out.println("Inside non-static block");
        a = 100;
        b = 200;
        x = 300;
        y = 400;
    }
    
    // Non-static method
    void display2() {
        System.out.println("Inside non-static method display2()");
        System.out.println(a);
        System.out.println(b);
        System.out.println(x);
        System.out.println(y);
    }
    
    // Constructor
    Program() {
        System.out.println("Inside constructor");
        a = 1000;
        b = 2000;
        x = 3000;
        y = 4000;
    }
}
```

#### **4. Explanation of the Code**
- **Static Block:** Executes once when the class is loaded and initializes static variables.
- **Static Method:** Can be called without an object and prints static variables.
- **Non-Static Block:** Executes before the constructor and initializes instance variables.
- **Constructor:** Runs after the non-static block when an object is created.
- **`display1()` (Static Method):** Prints static variables.
- **`display2()` (Non-Static Method):** Prints both static and instance variables.
- **Main Method Execution:**
  1. Calls `display1()` before creating an object.
  2. Creates an object of `Program`, triggering the non-static block and constructor.
  3. Calls `display2()` to access instance variables.

#### **5. Summary**
- **JVM executes static blocks, variables, and methods before calling the `main()` method.**
- **Static elements are associated with the class, while non-static elements are associated with an object instance.**
- **Static methods can be called without an object, while non-static methods require an object.**
- **Non-static blocks run before the constructor during object creation.**
- **Understanding the execution flow helps in designing efficient Java applications.**

```
public class Main{
    public static void main(String[] args) {
         // static variables
         // non-static variables (instance variables)
 
         // static methods
         // non-static methods (instance methods)
 
         // static blocks
         // non-static blocks (instance blocks)
 
         // constructors
    }
}
```


```
// Professional class
class Professional {
    private static String universityName = "Global University";
    private static int totalProfessors = 0;
    
    private int professorID;
    private String subject;
    
    // Static block
    static {
        System.out.println("Welcome to " + universityName);
    }
    
    // Non-static block
    {
        totalProfessors++;
        professorID = totalProfessors;
    }
    
    // Constructor
    public Professional(String subject) {
        this.subject = subject;
    }
    
    // Method to display professor details
    public void displayDetails() {
        System.out.println("Professor ID: " + professorID + ", Subject: " + subject);
    }
    
    // Static method to get total number of professors
    public static int getTotalProfessors() {
        return totalProfessors;
    }
    
    public static void main(String[] args) {
        // Creating instances of Professional class
        Professional prof1 = new Professional("Mathematics");
        Professional prof2 = new Professional("Physics");
        
        // Displaying details
        prof1.displayDetails();
        prof2.displayDetails();
        
        // Displaying total number of professors
        System.out.println("Total Professors: " + Professional.getTotalProfessors());
    }
}

```


