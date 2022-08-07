# SOLID PRINCIPLES

  

# Introduction 


Software design is a process that provides an implementation by transforming a client's requirements as described in the SRS document into a form that helps the programmer in software coding and implementation. The design must meet the scalability, correctness, completeness, efficiency, consistency, and maintainability. It is not an easy task to identify the feasibility of the client's requirements. To achieve scalability, a designer should concentrate on a few factors in designing software. These factors include rigidity, fragility, immobility, and viscosity. Rigidity specifies the difficulty measure of changing the software. Fragility is the tendency of the software to break every time it is changed. Immobility is the inability to reuse software from other projects or parts of the software from the same project. Viscosity is the inability to preserve the design that can degrade if a proper solution is not incorporated relevant to changes in the system requirement.These four factors result in poor architecture and bad design. To handle these factors, a concept called SOLID principles was developed by Robert C. Martin, also known as Uncle Bob.

SOLID  principles are the design principles that enable us to manage most software design problems. SOLID is an acronym that stands for five design principles: single responsibility principle, open-closed principle, Liskov substitution principle, interface segregation principle, and dependency inversion principle.

The broad goal of the SOLID principles is to reduce dependencies so that engineers change one area of software without impacting others and make designs easier to understand, maintain, and extend. Ultimately, using these design principles makes it easier for software engineers to avoid issues and to build adaptive, effective, and agile software.
- - - 
# Overview of SOLID Principles
## S : Single Responsibility Principle (SRP)


>“ A class should have one, and only one, reason to change.”
Each class and module should focus on a single task at a time.


Everything in the class should be related to that single purpose.
There can be many members in the class as long as they related to a single responsibility.

with SRP, classes become smaller and cleaner and code is less fragile.
SRP helps in meeting the maintainability, Testability, Flexibility and Extensability, Parallel development and loose coupling.

```java
class Book {
    private String bookName;
    private String author;
    private String text;
    
    //related to Book's property
    public boolean findNyAuthor(String authName)
    {
        return author.contains(authNmae);
    }

    //related to Book's property
    public boolean findByName( String book_Name)
    {
        return book_Name.contains(bookName)
    }

    //printing it on console
    void printToConsole()
    {

    }
}

```
The above example violates the single responsibility principle because it contains a ``` printToConsole() ``` method that is not related to property of class Book.

The SRP states that class should have only a single reason to change. In the above example the reason is ``` printToConsole() ``` . And it can be resolved by creating new class for ``` printToConsole() ``` method.

``` java
class Book {
    private String bookName;
    private String author;
    private String text;
    
    public Book(String bookName, String author, String text)
    {
        this.bookName=bookName;
        this.author=author;
        this.text=text;
    }

    //related to Book's property
    public boolean findNyAuthor(String authName)
    {
        return author.contains(authNmae);
    }

    //related to Book's property
    public boolean findByName( String book_Name)
    {
        return book_Name.contains(bookName)
    }
}

class BookPrinter{

    //method for outputting text
    //printing it on console
    Book book;
    public BookPrinter(Book book)
    {
        this.book=book;
    }

    void printToConsole()
    {
        System.out.println(book.text);
    }

}
```
Now the above example obeys the single responsibility principle and every class is responsible for one aspect of our application.


## O : Open - Closed Principle (OCP)

> “You should be able to extend a class’s behavior without modifying it.”

The idea of the open-closed principle is that existing, well-tested classes will need to be modified when something needs to be added. Yet, changing classes can lead to problems or bugs. Instead of changing the class, you simply want to extend it.

Your class complies with this principle if it is:
Open for extension, meaning that the class’s behavior can be extended; and
Closed for modification, meaning that the source code is set and cannot be changed.

By using  interfaces and abstraction classes, new functionalities can be added without touching or modifying the existing functionality.


lets consider an example:

``` java
    public class Operation
    {
        public double calculate(double d1, double d2, String operationType)
        {
            switch(operationType)
            {
                case "+" :
                {
                    return d1+d2;
                }
                case "-" :
                {
                    return d1-d2;
                }
                default:

            }
            return 0;
        }
    }

```
The above example consists  a method ``` double calculate(double d1, double d2, String operation)```. It performs addition and subtraction of two numbers. To support other Airthmetic operations the ```switch-block ``` can be implemented as below.

``` java
    switch(operation)
    {

        case "+" :
        {
            return d1+d2;
        }                case "-" :
       {
            return d1-d2;
        }
        case "/" :
        {
            return d1/d2;
        }
        case "%":
        {
        return d1%d2;
        }   
        default:

     }
```

The above implementaion works fine but it doesn't  obey the Open-Closed principle. Because the exsisting code was modified.

To obey the open-closed priniciple, above code must be implemented by using either interface or abstract class.

``` java

    public interface Operation
    {
        public double calculate(double d1, double d2);
    }

    class AddOperation implements OPeration{
        @override
        public double calculate(double d1, double d2)
        {
            return d1+d2;
        }
    }

    class DivisionOperator implements Operation
    {
        @override
        public double calculate(double d1, double d2)
        {
            return d1/d2;
        }

    }
```
For other airthmetic operations can be added to the above implementation by creating a class that implements the interface. And it doesn't violate the open-closed principle.

## L : Liskov Substitution Principle (LSP)

>" if S is a subtype of T, then objects of type T in a program may be replaced with objects of type S without altering any of the desirable properties of that program."

It’s simply an extension of open-closed principle, as it’s a way of ensuring that derived classes extend the base class without changing behavior.

Derived types must be completely sudstitutable for their base type. When a derived Class cannot perform the same actions as its parent Class, this can cause bugs.

lets consider an example:

``` java
    public interface Vehicle
    {
        public void startEngine()
        {

        }
    }
    class Car implements Vehicle
    {
        @override
        public void startEngine()
        {

        }
    }
    class bicycle implements startEngine()
    {
        pubic void startEngine()
        {
            throw new EngineNotFoundException("Engine Missing");
        }
    }

```
In the above example the base class is Vehicle and the child classes are car and bicycle. The car has the same behaviour as the vechicle but the bicycle doesn't. Because the bycycle has no engine and it throws an Exception. THe above implementaion supports Open-closed principles but violates Liskov substitution principle.

Now observe the below implementation, 

``` java
    public interface VehicleWithEngine
    {
        public void startEngine();
    }
    public interface VehicleWithoutEngine
    {
        public void start();
    }
    class Car implements VehicleWithEngine
    {
        @override
        public void startEngine()
        {

        }
    }
    class bicycle implements VehicleWithoutEngine
    {
        @override
        pubic void start()
        {

       }
    }

```
Now the bicycle belongs to VechicleWithoutEngine category and car belongs to VehicleWithEngine Category. Bicycle doesn't contain ```startEngine()``` method and it doesn't raise any exception. Hence, the above implementation follows the Liskov substitution principle.

## I : Interface Segregation Principle (ISP)

>“Make fine grained interfaces that are client-specific. Clients should not be forced to implement interfaces they do not use.”


For software engineers, this means that you don’t want to just start with an existing interface and add new methods. Instead, start by building a new interface and then let your class implement multiple interfaces as needed. 

Smaller interfaces mean that developers should have a preference for composition over inheritance and for decoupling over coupling. According to this principle, engineers should work to have many client-specific interfaces, avoiding the temptation of having one big, general-purpose interface.

let's consider an example:

``` java

    public interface shape{
        double calculateArea();
        double calculateVolume();
    }
    
    class Cuboid implements Shape
    {
        @override
        public double calculateArea()
        {

        }

        @override
        public double calculateVolume(){

        }
    }

    class Square implements Shape
    {
        @override
        public double calculateArea(){

        }

        @override
        public double calculateVolume(){

            throw new
        }
    }
```
The above implemenation has a Shape interface with two methods named calculateArea() and calculateVolume(). For the square shape its volume can't be calculated and throws an Exception.

lets make a change to the above implementation.

``` java
    interface   TwoDimensionalShape{
        double calculateArea ();
    }

    interface   ThreeDimensionalShape
    {   
        double calculateVolume();
    }

    class cubod impplements TwoDimensionalShape, ThreeDimensionalShape
    {
        @override
        public double calculateArea()
        {

        }

        @override
        public double calculateVolume()
        {

        }
    }

    class Square implements TwoDimensionalShape
    {
        @override
        public double calculateArea()
        {

        }
    }
```

The above code doesn't leads to any error. And implemented sucessfully by Interface segregation.


## D : Dependency Inversion Principle

> “ High level modules should not depend upon low level modules. Both should depend on abstractions.” Further, “abstractions should not depend on details. Details should depend upon abstractions.”

It states that classes should depend upon interfaces or abstract classes instead of concrete classes and functions.

