The SOLID principles are a set of guidelines aimed at improving software development practices, making code more extensible, logical, and easier to read. Each principle represents a best practice for object-oriented programming. Here's an overview of each principle with examples in Java:

### 1. **Single Responsibility Principle (SRP)**
   - **Principle**: A class should have only one reason to change, meaning it should have only one job or responsibility.
   - **Example**:
     ```java
     public class OrderProcessor {
         public void processOrder(Order order) {
             // logic to process the order
         }
     }

     public class OrderStorage {
         public void saveOrder(Order order) {
             // logic to save order to a database
         }
     }
     ```
     Here, `OrderProcessor` handles the processing of orders, and `OrderStorage` handles database storage, adhering to SRP by separating concerns.

### 2. **Open/Closed Principle (OCP)**
   - **Principle**: Software entities should be open for extension but closed for modification.
   - **Example**:
     ```java
     public abstract class Discount {
         public abstract double applyDiscount(double price);
     }

     public class SeasonalDiscount extends Discount {
         public double applyDiscount(double price) {
             return price * 0.9; // 10% discount
         }
     }

     public class ClearanceDiscount extends Discount {
         public double applyDiscount(double price) {
             return price * 0.7; // 30% discount
         }
     }
     ```
     `Discount` is an abstract class that can be extended by different types of discounts, but the existing discount classes do not need to be modified to add new types.

### 3. **Liskov Substitution Principle (LSP)**
   - **Principle**: Objects of a superclass shall be replaceable with objects of its subclasses without affecting the correctness of the program.
   - **Example**:
     ```java
     public class Bird {
         public void fly(){
             // implementation for flying
         }
     }

     public class Duck extends Bird {
         @Override
         public void fly() {
             // Ducks flying behavior
         }
     }

     public class Ostrich extends Bird {
         @Override
         public void fly() {
             throw new UnsupportedOperationException("Ostrich cannot fly");
         }
     }
     ```
     This example violates LSP because `Ostrich` cannot substitute `Bird` without altering the behavior expected from `Bird`. This should be redesigned so that `fly` is not an assumed ability of all `Birds`.

### 4. **Interface Segregation Principle (ISP)**
   - **Principle**: No client should be forced to depend on methods it does not use.
   - **Example**:
     ```java
     public interface Animal {
         void eat();
     }

     public interface FlyingAnimal {
         void fly();
     }

     public class Eagle implements Animal, FlyingAnimal {
         public void eat() {
             // implementation of eat
         }

         public void fly() {
             // implementation of fly
         }
     }

     public class Dog implements Animal {
         public void eat() {
             // Dogs eating behavior
         }
     }
     ```
     `Dog` does not need to implement `fly`, thus adhering to ISP by separating `Animal` and `FlyingAnimal` interfaces.

### 5. **Dependency Inversion Principle (DIP)**
   - **Principle**: High-level modules should not depend on low-level modules. Both should depend on abstractions. Abstractions should not depend on details.
   - **Example**:
     ```java
     public interface PaymentMethod {
         void processPayment(double amount);
     }

     public class CreditCardPayment implements PaymentMethod {
         public void processPayment(double amount) {
             // Process payment using credit card
         }
     }

     public class PaymentProcessor {
         private PaymentMethod paymentMethod;

         public PaymentProcessor(PaymentMethod paymentMethod) {
             this.paymentMethod = paymentMethod;
         }

         public void process(double amount) {
             paymentMethod.processPayment(amount);
         }
     }
     ```
     `PaymentProcessor` depends on the `PaymentMethod` interface rather than concrete implementations, following DIP.

These principles help in creating maintainable and scalable software systems in Java and other object-oriented programming languages.
