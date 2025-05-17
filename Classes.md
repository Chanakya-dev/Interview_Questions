# Nested Classes in Java

A **nested class** is a class defined **within another class**. Nested classes are useful to logically group classes that are only used in one place, increase encapsulation, and improve readability.

---

## Types of Nested Classes

1. **Static Nested Class**
2. **Inner Class (Non-static Nested Class)**
3. **Local Class**
4. **Anonymous Class**

---

## 1. Static Nested Class

* Declared **static** inside an outer class.
* Behaves like a static member of the outer class.
* Can access **static members** of the outer class directly.
* Cannot access **non-static members** of the outer class directly.
* Does **not** have a reference to an instance of the outer class.
* Created using the syntax: `OuterClass.StaticNestedClass obj = new OuterClass.StaticNestedClass();`

### Example:

```java
class Outer {
    static int data = 30;
    
    static class StaticNested {
        void display() {
            System.out.println("Static nested class: data = " + data);
        }
    }
}

public class Test {
    public static void main(String[] args) {
        Outer.StaticNested nested = new Outer.StaticNested();
        nested.display();
    }
}
```

---

## 2. Inner Class (Non-static Nested Class)

* Non-static nested class.
* Has access to **all members** (including private) of the outer class.
* Requires an instance of the outer class to be instantiated.
* Maintains a reference to the **outer class instance**.
* Created using the syntax: `OuterClass.InnerClass obj = outerObj.new InnerClass();`

### Example:

```java
class Outer {
    private int data = 10;
    
    class Inner {
        void display() {
            System.out.println("Inner class: data = " + data);
        }
    }
}

public class Test {
    public static void main(String[] args) {
        Outer outer = new Outer();
        Outer.Inner inner = outer.new Inner();
        inner.display();
    }
}
```

---

## 3. Local Class

* A class declared **inside a method** (or constructor).
* Only visible within the block where it is declared.
* Can access final or effectively final variables from the method.
* Useful for grouping helper classes used only inside one method.

### Example:

```java
class Outer {
    void display() {
        class Local {
            void show() {
                System.out.println("Local class inside method");
            }
        }
        
        Local local = new Local();
        local.show();
    }
}

public class Test {
    public static void main(String[] args) {
        Outer outer = new Outer();
        outer.display();
    }
}
```

---

## 4. Anonymous Class

* A **local class without a name**.
* Used to instantiate objects with certain modifications or implementations on the fly.
* Typically used to implement interfaces or extend classes in-place.
* Syntax uses `{}` right after `new` keyword.

### Example: Anonymous class implementing interface

```java
interface Hello {
    void greet();
}

public class Test {
    public static void main(String[] args) {
        Hello obj = new Hello() {
            public void greet() {
                System.out.println("Hello from anonymous class");
            }
        };
        obj.greet();
    }
}
```

---

## Summary Table

| Nested Class Type   | Static/Non-Static | Access to Outer Class Members   | Requires Outer Instance  | Use Case                                      |
| ------------------- | ----------------- | ------------------------------- | ------------------------ | --------------------------------------------- |
| Static Nested Class | Static            | Only static members             | No                       | Group related static classes                  |
| Inner Class         | Non-static        | All members                     | Yes                      | Associated with an instance of outer class    |
| Local Class         | Non-static        | Final or effectively final vars | No (local to method)     | Helper classes within methods                 |
| Anonymous Class     | Non-static        | Final or effectively final vars | No (local to expression) | Quick implementation of interface or subclass |
