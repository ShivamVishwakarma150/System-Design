# SOLID Priciples


The SOLID principles are a set of design principles that help developers create software that is easy to understand.

<br/>
<br/>

## Single Responsibility Principle (SRP) :

<br/>

The Single Responsibility Principle (SRP) states that a class should have only one reason to change, meaning it should have only one responsibility. This principle promotes high cohesion and ensures that each class is focused on a specific task, making the code easier to understand, maintain, and extend.

Let's consider an example to understand SRP in detail:

Suppose we are building a system to manage a library. We have a `Book` class that represents a book in the library. The `Book` class has various properties and methods related to books, such as `title`, `author`, `ISBN`, `checkOut()`, `checkIn()`, etc. However, the `Book` class is violating the SRP because it has multiple responsibilities: managing book data and handling check-in/check-out operations.

To refactor the code and adhere to the SRP, we can split the responsibilities into two separate classes: `Book` and `LibraryManager`.

1. The `Book` class will be responsible for maintaining book data:

```java
class Book {
    private String title;
    private String author;
    private String ISBN;

    // Getters and setters for book properties

    // Other methods related to book data
}
```

The `Book` class now focuses solely on managing book properties and related methods. It has a single responsibility: to encapsulate book data.

2. The `LibraryManager` class will handle check-in/check-out operations:

```java
class LibraryManager {
    public void checkOut(Book book, String borrower) {
        // Check out the book and update the status
    }

    public void checkIn(Book book) {
        // Check in the book and update the status
    }
}
```

The `LibraryManager` class takes care of the check-in/check-out operations. It no longer contains book-related properties or methods, as they have been moved to the `Book` class. The `LibraryManager` class now has a single responsibility: managing the library operations.

With this refactoring, we have adhered to the SRP. The `Book` class is responsible for book data, and the `LibraryManager` class is responsible for library operations. If there are any changes required in the book data or the library operations, we only need to modify the respective class, ensuring that changes are localized and do not affect other parts of the system.

As for a diagram representing the SRP, you can use a UML class diagram to illustrate the classes and their responsibilities. Here's a simplified representation:

```
----------------------
|      Book          |
----------------------
| - title: String    |
| - author: String   |
| - ISBN: String     |
----------------------
| + getTitle()       |
| + getAuthor()      |
| + getISBN()        |
| + setTitle()       |
| + setAuthor()      |
| + setISBN()        |
| + otherMethods()   |
----------------------

----------------------
|   LibraryManager   |
----------------------
| + checkOut()       |
| + checkIn()        |
----------------------
```

In the diagram above, the `Book` class has its properties and methods related to book data, while the `LibraryManager` class has methods for managing library operations. The separation of responsibilities is clearly depicted, indicating adherence to the SRP.

Remember, the SRP promotes a modular and maintainable design by ensuring that each class has a single responsibility. It simplifies code understanding, testing, and modification, making the system more robust and flexible.

<br/>
<br/>
<br/>

## Open-Closed Principle (OCP):

The Open-Closed Principle (OCP) states that software entities should be open for extension but closed for modification, focusing on the behavior of interfaces rather than specific classes. This principle encourages the creation of interfaces that define the desired behavior and allow for the addition of new implementations without modifying existing code.

Let's consider an example to understand the OCP in the context of interface behavior:

```java
interface Shape {
    double calculateArea();
}
```

In this example, we have an interface called `Shape` that defines a single method `calculateArea()`. The `Shape` interface encapsulates the behavior of calculating the area of different shapes without specifying the details of individual shapes.

Now, let's implement two concrete shape classes, `Circle` and `Rectangle`, that adhere to the `Shape` interface:

```java
class Circle implements Shape {
    private double radius;

    public Circle(double radius) {
        this.radius = radius;
    }

    @Override
    public double calculateArea() {
        return Math.PI * radius * radius;
    }
}

class Rectangle implements Shape {
    private double width;
    private double height;

    public Rectangle(double width, double height) {
        this.width = width;
        this.height = height;
    }

    @Override
    public double calculateArea() {
        return width * height;
    }
}
```

Both the `Circle` and `Rectangle` classes implement the `calculateArea()` method according to their respective formulas. By adhering to the `Shape` interface, they ensure that they provide the necessary behavior without modifying the existing interface or other implementations.

The key point here is that the `Shape` interface defines a contract for the behavior of calculating the area, allowing for new shapes to be added by implementing the `Shape` interface:

```java
class Triangle implements Shape {
    private double base;
    private double height;

    public Triangle(double base, double height) {
        this.base = base;
        this.height = height;
    }

    @Override
    public double calculateArea() {
        return 0.5 * base * height;
    }
}
```

We introduced a new shape, `Triangle`, by implementing the `Shape` interface without modifying the existing code. This demonstrates the open-closed nature of the OCP, where the system can be extended with new behavior (shapes) through the implementation of existing interfaces.

The focus on interface behavior ensures that the system is flexible and extensible, allowing for the addition of new implementations without modifying existing code. This promotes code reuse, maintainability, and stability.

Certainly! Here's a diagram illustrating the Open-Closed Principle (OCP) with a focus on interface behavior:

```
----------------------
|        Shape       |
----------------------
| + calculateArea()  |
----------------------
       ^      ^ 
       |      |
----------------------
|      Circle        |
----------------------
| - radius: double   |
----------------------

----------------------
|     Rectangle      |
----------------------
| - width: double    |
| - height: double   |
----------------------

----------------------
|      Triangle      |
----------------------
| - base: double     |
| - height: double   |
----------------------
```

In the diagram above, we have the `Shape` interface at the top, which defines the behavior of calculating the area through the `calculateArea()` method. The `Circle`, `Rectangle`, and `Triangle` classes implement the `Shape` interface and provide their own implementations of the `calculateArea()` method. Each class represents a specific shape and encapsulates its own data and behavior.

This diagram demonstrates how the OCP allows for the extension of behavior through new implementations of the `Shape` interface without modifying the existing code. New shapes, such as `Triangle`, can be added by implementing the `Shape` interface and providing the necessary calculations for their area, adhering to the contract defined by the interface.

The diagram emphasizes the separation between the interface and the concrete implementations, highlighting the focus on behavior rather than specific classes. This design enables the system to be open for extension, as new shapes can be added without modifying the existing code that depends on the `Shape` interface.

By adhering to the OCP and designing interfaces that capture desired behaviors, you create a flexible and extensible system that can accommodate new implementations and changes without impacting existing code.


<br/>
<br/>
<br/>

## Liskov Substitution Principle (LSP)

The Liskov Substitution Principle (LSP) states that objects of a superclass should be replaceable with objects of its subclasses without affecting the correctness of the program. In other words, subclasses must be substitutable for their base (super) class without altering the behavior of the system.

To understand LSP, let's consider an example of a `Shape` hierarchy, similar to the previous examples:

```java
class Shape {
    protected int width;
    protected int height;

    public void setWidth(int width) {
        this.width = width;
    }

    public void setHeight(int height) {
        this.height = height;
    }

    public int calculateArea() {
        return width * height;
    }
}
```

The `Shape` class represents a basic shape with width and height attributes and provides a method `calculateArea()` to calculate the area based on those dimensions.

Now, let's define two subclasses, `Rectangle` and `Square`, which inherit from `Shape`:

```java
class Rectangle extends Shape {
    // Inherits width, height, and calculateArea()

    // Additional methods and attributes specific to Rectangle
}

class Square extends Shape {
    // Inherits width, height, and calculateArea()

    @Override
    public void setWidth(int width) {
        super.setWidth(width);
        super.setHeight(width);
    }

    @Override
    public void setHeight(int height) {
        super.setWidth(height);
        super.setHeight(height);
    }

    // Additional methods and attributes specific to Square
}
```

In this example, both `Rectangle` and `Square` are subclasses of `Shape` and inherit the `width`, `height`, and `calculateArea()` behavior from the superclass.

According to LSP, any code that works with `Shape` objects should also work correctly with `Rectangle` and `Square` objects. This means that objects of the `Shape` class should be replaceable with objects of its subclasses without affecting the functionality of the system.

Let's see an example code snippet that demonstrates the usage of LSP:

```java
public void printArea(Shape shape) {
    shape.setWidth(5);
    shape.setHeight(10);
    int area = shape.calculateArea();
    System.out.println("Area: " + area);
}

// Usage
Shape rectangle = new Rectangle();
printArea(rectangle);

Shape square = new Square();
printArea(square);
```

In the code above, we have a `printArea()` method that accepts a `Shape` object as a parameter. It sets the width and height of the shape and calculates the area using the `calculateArea()` method. This method can be called with objects of both `Rectangle` and `Square` without any issues.

The LSP guarantees that substituting a `Rectangle` or `Square` object for a `Shape` object will not impact the correctness of the `printArea()` method. The behavior of the method remains consistent regardless of the specific subclass being used.

As for the diagram, it would be similar to the one used in the previous examples, illustrating the class relationships between `Shape`, `Rectangle`, and `Square`, showcasing the inheritance hierarchy and the substitution relationship.

```
----------------------
|        Shape       |
----------------------
| # width: int       |
| # height: int      |
----------------------
| + setWidth()       |
| + setHeight()      |
| + calculateArea()  |
----------------------

----------------------
|      Rectangle     |
----------------------
|                 |
| (inherits Shape)  |
----------------------

----------------------
|        Square      |
----------------------
|                 |
| (inherits Shape)  |
----------------------
```

The diagram above depicts the `Shape` class as the base class, with `Rectangle` and `Square` as its subclasses. Both subclasses

 inherit the behavior and attributes of the `Shape` class. The diagram emphasizes the substitution relationship, showing that objects of `Rectangle` and `Square` can be substituted for `Shape` objects, adhering to the Liskov Substitution Principle.

By adhering to LSP, you ensure that the substitutability of objects is maintained, enabling code reuse, extensibility, and maintaining correctness throughout the system.

Certainly! Let's consider a stronger scenario where violating the Liskov Substitution Principle (LSP) can lead to serious issues. In this case, we'll focus on a `Shape` hierarchy where the `Rectangle` subclass violates LSP.

## Problem:
Suppose we have a client code that works with objects of the `Shape` class and expects them to have a certain behavior. However, the `Rectangle` class violates LSP by incorrectly implementing the `calculateArea()` method, leading to incorrect results and potential errors when substituting a `Rectangle` object for a `Shape` object.

Let's see the code example:

```java
class Shape {
    public int calculateArea(int width, int height) {
        return width * height;
    }
}

class Rectangle extends Shape {
    @Override
    public int calculateArea(int width, int height) {
        if (width == height) {
            throw new UnsupportedOperationException("Cannot calculate area of a square");
        }
        return width * height;
    }
}
```

In the above code, the `Shape` class has a `calculateArea()` method that takes the width and height as parameters and returns the area calculated by multiplying them.

The `Rectangle` class extends `Shape` and overrides the `calculateArea()` method. However, it introduces a check to determine if the given rectangle is actually a square. If the width and height are equal, it throws an `UnsupportedOperationException` indicating that the area calculation is not supported for squares.

Now, let's see how this violation of LSP can cause serious issues:

```java
public class Main {
    public static void main(String[] args) {
        Shape rectangle = new Rectangle();
        int width = 5;
        int height = 5;
        int area = rectangle.calculateArea(width, height);
        System.out.println("Area: " + area);
    }
}
```

In the `Main` class, we create a `Rectangle` object and assign it to a variable of type `Shape`. This demonstrates substitutability, where a `Rectangle` object is treated as a `Shape` object.

When calling the `calculateArea()` method on the `rectangle` object with equal width and height, it throws an `UnsupportedOperationException` because the `Rectangle` class does not support calculating the area for squares.

This violation of LSP leads to incorrect behavior and potential errors in the client code. The client code assumes that any `Shape` object, including a `Rectangle`, can correctly calculate the area. However, due to the LSP violation in the `Rectangle` class, it throws an exception and prevents the calculation of the area, causing unexpected program behavior and potentially crashing the application.

To resolve this LSP violation, we should ensure that the behavior of the base class (`Shape`) is preserved in the subclass (`Rectangle`). The `Rectangle` class should correctly calculate the area without introducing any additional constraints or exceptions.

By adhering to LSP, we can avoid such serious problems and ensure that substituting a `Rectangle` object for a `Shape` object does not introduce unexpected behavior or errors in the client code.

Certainly! Let's discuss the solution to the problem where the `Rectangle` class violates the Liskov Substitution Principle (LSP) in the `Shape` hierarchy.

## Solution:
To adhere to LSP, we need to design our classes in a way that ensures substitutability, meaning that objects of the subclass (`Rectangle`) can be seamlessly substituted for objects of the base class (`Shape`) without affecting the correctness of the program.

In the previous example, the `Rectangle` class introduced an additional constraint and threw an exception when calculating the area for squares. To resolve this, we can modify the design to ensure that the behavior of the base class is preserved in the subclass.

Here's an updated code example that addresses the LSP violation:

```java
abstract class Shape {
    public abstract int calculateArea();
}

class Rectangle extends Shape {
    private int width;
    private int height;

    public Rectangle(int width, int height) {
        this.width = width;
        this.height = height;
    }

    @Override
    public int calculateArea() {
        return width * height;
    }
}
```

In this solution, the `Shape` class is modified to declare the `calculateArea()` method as an abstract method. This enforces that all subclasses must provide their own implementation of the area calculation.

The `Rectangle` class now takes the width and height as constructor parameters and implements the `calculateArea()` method by multiplying the width and height. This ensures that the behavior of calculating the area is consistent throughout the hierarchy.

Now, let's revisit the client code:

```java
public class Main {
    public static void main(String[] args) {
        Shape rectangle = new Rectangle(5, 5);
        int area = rectangle.calculateArea();
        System.out.println("Area: " + area);
    }
}
```

In the updated `Main` class, we create a `Rectangle` object by providing the width and height as constructor arguments. We assign it to a variable of type `Shape`. When calling the `calculateArea()` method on the `rectangle` object, it invokes the overridden implementation from the `Rectangle` class.

As a result, the output will be:

```
Area: 25
```

With this solution, we have adhered to LSP by ensuring that substituting a `Rectangle` object for a `Shape` object does not alter the behavior or correctness of the program. The `Rectangle` object can seamlessly replace a `Shape` object, and the client code can rely on the common behavior defined by the `Shape` class without any unexpected issues.

By preserving the behavior of the base class in the subclass and allowing subclasses to provide their own implementation of the abstract method, we maintain substitutability, code reuse, and the ability to extend the hierarchy without breaking existing code that depends on the common behavior defined by the base class.

Overall, adhering to LSP ensures a consistent and predictable class hierarchy, promoting reusability, extensibility, and the ability to substitute objects of the subclass for objects of the base class without introducing unexpected behavior or constraints.