# SOLID Principle

**SOLID** is an acronym that represents **five principles of object-oriented programming** and design that **help create maintainable, scalable, and robust software**. These principles were **introduced by Robert C. Martin (Uncle Bob)** and are widely used in Java development.

**SOLID** Stands for: 
– Single Responsibility Principle (SRP)
– Open/Closed Principle (OCP)
– Liskov Substitution Principle (LSP)
- Interface Segregation Principle (ISP)
- Dependency Inversion Principle (DIP)

## S – Single Responsibility Principle (SRP)
A class should have only one reason to change, meaning it should have **only one job or responsibility**. 
### Example:
- Here Class Report has two responsibilities: generateReport and printReport which is not acceptable by 1st Principle.
```
class Report {
    private String name;
    private String ReportDetails; 
    void generateReport() {
        // Code to generate a report
    }
        // This method violates SRP because printing should be handled separately
    void printReport() {
        // Code to print the report
    }
}
```
### Refactored (Following SRP):
- Each class has single responsibility and has only one reason to change.
```
class Report {
    private String name;
    private String ReportDetails;
    // constructor, getter and setter
}
class ReportGenerator {
    private Report report;
    void generateReport() {
    // Code to generate a report
    }
}
class ReportPrinter {
    private Report report;
    void printReport(Report report) {
    // Code to print the report
    }
}
```
## O – Open/Closed Principle (OCP)
A class should be open for extension but closed for modification.
### Example (Violation):
```
class PaymentProcessor {
    void processPayment(String paymentType) {
        if (paymentType.equals("CreditCard")) {
            // Process credit card payment
        } else if (paymentType.equals("PayPal")) {
            // Process PayPal payment
        }
    }
}
```
### Refactored (Following OCP using polymorphism):
```
interface Payment {
    void processPayment();
}
class CreditCardPayment implements Payment {
    public void processPayment() {
        // Process credit card payment
    }
}
class PayPalPayment implements Payment {
    public void processPayment() {
        // Process PayPal payment
    }
}
class PaymentProcessor {
    void process(Payment payment) {
        payment.processPayment();
    }
}
```

## L – Liskov Substitution Principle (LSP)
Subtypes should be substitutable for their base types without affecting the correctness of the program.

### Example (Violation):
```
class Bird {
    void fly() {
        System.out.println("Bird is flying");
    }
}
class Penguin extends Bird {
    void fly() {
        throw new UnsupportedOperationException("Penguins cannot fly");
    }
}
```
### Refactored (Following LSP by using better abstraction):
```
abstract class Bird { }
interface Flyable {
    void fly();
}
class Sparrow extends Bird implements Flyable {
    public void fly() {
        System.out.println("Sparrow is flying");
    }
}
class Penguin extends Bird {
    // Penguins do not implement Flyable
}
```
## I – Interface Segregation Principle (ISP)
A class should not be forced to implement interfaces it does not use.
### Example (Violation):
```
interface Worker {
    void work();
    void eat();
}
class Robot implements Worker {
    public void work() {
        System.out.println("Robot working...");
    }

    public void eat() {
        throw new UnsupportedOperationException("Robot doesn't eat");
    }
}
```
### Refactored (Following ISP by splitting interfaces):
```
interface Workable {
    void work();
}
interface Eatable {
    void eat();
}
class HumanWorker implements Workable, Eatable {
    public void work() {
        System.out.println("Human working...");
    }

    public void eat() {
        System.out.println("Human eating...");
    }
}
class Robot implements Workable {
    public void work() {
        System.out.println("Robot working...");
    }
}
```
## D – Dependency Inversion Principle (DIP)
High-level modules should not depend on low-level modules. Both should depend on abstractions.
### Example (Violation):
```
class MySQLDatabase {
    void connect() {
        System.out.println("Connected to MySQL");
    }
}
class Application {
    private MySQLDatabase database;

    public Application() {
        this.database = new MySQLDatabase();
    }

    void start() {
        database.connect();
    }
}
```
### Refactored (Following DIP using dependency injection):
```
interface Database {
    void connect();
}
class MySQLDatabase implements Database {
    public void connect() {
        System.out.println("Connected to MySQL");
    }
}
class PostgreSQLDatabase implements Database {
    public void connect() {
        System.out.println("Connected to PostgreSQL");
    }
}
class Application {
    private Database database;

    public Application(Database database) {
        this.database = database;
    }

    void start() {
        database.connect();
    }
}
```
### Usage:
```
public class Main {
    public static void main(String[] args) {
        Database db = new MySQLDatabase(); // Or new PostgreSQLDatabase()
        Application app = new Application(db);
        app.start();
    }
}
```
By following the SOLID principles in Java, we ensure that our code is modular, testable, and scalable, making it easier to maintain and extend over time.

