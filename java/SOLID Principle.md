# SOLID Principle

**SOLID** is an acronym that represents **five principles of object-oriented programming** and design that **help create maintainable, scalable, and robust software**. These principles were **introduced by Robert C. Martin (Uncle Bob)** and are widely used in Java development.

## S – Single Responsibility Principle (SRP)
A class should have only one reason to change, meaning it should have **only one job or responsibility**.
### Example:
```
//Here Class Report has two responsibilities: generateReport and printReport which is not acceptable by 1st Principle.
class Report {
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
```
// Each class has single responsibility and has only one reason to change
class Report {
    void generateReport() {
        // Code to generate a report
    }
}
class ReportPrinter {
    void printReport(Report report) {
        // Code to print the report
    }
}
```
