### **String Handling in Java**  

#### **1. String Basics**  
- Strings in Java are immutable, meaning once created, they cannot be changed.  
- `concat()` method is used to join two strings, but it does not modify the original string.  

```java
String s1 = "Java";
System.out.println(s1);
System.out.println(s1.concat(" is a programming language."));
System.out.println(s1);
```

#### **2. Comparing Strings**  
- `==` compares object references (whether they point to the same memory location).  
- `equals()` compares the actual content of the strings.  
- `equalsIgnoreCase()` compares content while ignoring case differences.  

```java
String s2 = "Java";
String s3 = "Java";
String s4 = new String("java");
if(s4 == s3){
    System.out.println("s1 and s2 are the same object in memory.");
}else{
    System.out.println("s1 and s2 are different objects in memory.");
}
System.out.println(s3.equals(s4));
```

#### **3. Creating Strings**  
- String literals are stored in the **String Pool** to optimize memory.  
- `new String("text")` creates a new object in the heap, even if the same string exists in the pool.  

#### **4. Using `compareTo()` Method**  
- Used to compare strings lexicographically.  
- Returns:
  - `> 0` if the first string is greater  
  - `< 0` if the first string is smaller  
  - `0` if both are equal  

```java
String s5 = "SACHIN";
String s6 = "SAURAV";
int res = s5.compareTo(s6);
if(res > 0){
    System.out.println(s5 + " is greater than " + s6);
}else if(res < 0){
    System.out.println(s5 + " is less than " + s6);
}else{
    System.out.println(s5 + " is equal to " + s6);
}
```

#### **5. Converting Between Character Arrays and Strings**  
- `toCharArray()` converts a string into a character array.  
- A character array can be converted back into a string using `new String(charArray)`.  

```java
char[] ch1 = {'r', 'i', 't', 'i', 'k'};
String s7 = new String(ch1); // converting char array to string
System.out.println(s7);
```

#### **6. String Interning (`intern()`)**  
- `intern()` moves a dynamically created string into the **String Pool**, allowing it to be referenced like a string literal.  

```java
String s8 = new String("richa");
String s9 = s8.intern(); // converts the string to a string literal
String s10 = "richa"; // string literal
if(s9 == s10){
    System.out.println("s8 and s10 are the same object in memory.");
}else{
    System.out.println("s8 and s10 are different objects in memory.");
}
```

#### **7. String Concatenation and Immutability**  
- Modifying a string using `concat()` does not change the original string but creates a new one.  

```java
String s1 = "knowledge";
String s2 = s1; // s2 points to the same "knowledge"
s1 = s1.concat(" base"); // Creates a new String "knowledge base"
System.out.println(s1);
System.out.println(s2); // s2 still points to "knowledge"
```

#### **8. Null Concatenation Issue**  
- Concatenating a `null` value using `concat()` will cause a `NullPointerException`.  

```java
String s1 = "knowledge base";
String s2 = s1.concat(null); // Throws NullPointerException
System.out.println(s2);
```

