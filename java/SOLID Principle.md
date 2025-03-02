# SOLID Principle

**SOLID** is an acronym that represents **five principles of object-oriented programming** and design that **help create maintainable, scalable, and robust software**. These principles were **introduced by Robert C. Martin (Uncle Bob)** and are widely used in Java development.

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
