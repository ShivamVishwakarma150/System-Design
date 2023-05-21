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
