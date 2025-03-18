# E-Commerce Payment Processing Example 

## 1. Overview
This example demonstrates an **e-commerce payment processing system** using a `main` method as the test client. 
It illustrates the use of **inheritance** with an abstract superclass (`Payment`) and concrete subclasses (`CreditCardPayment`, `PayPalPayment`, `CashPayment`).

---

## 2. Implementation

### ✅ Step 1: Abstract Superclass (`Payment`)
```java
import java.util.Date;

// Abstract superclass: Defines common payment attributes
abstract class Payment {
    protected double amount;
    protected Date paymentDate;
    protected String payer;

    public Payment(double amount, String payer) {
        this.amount = amount;
        this.payer = payer;
        this.paymentDate = new Date();
    }

    public void showPaymentDetails() {
        System.out.println("Payment of $" + amount + " from " + payer + " on " + paymentDate);
    }

    // Abstract method: Must be implemented in subclasses
    public abstract void processPayment();
}
```

---

### ✅ Step 2: Concrete Subclasses for Payment Methods
```java
// Specialization: Credit Card Payment
class CreditCardPayment extends Payment {
    private String cardNumber;

    public CreditCardPayment(double amount, String payer, String cardNumber) {
        super(amount, payer);
        this.cardNumber = cardNumber;
    }

    @Override
    public void processPayment() {
        System.out.println("Processing Credit Card payment of $" + amount + " from " + payer);
    }
}
```

```java
// Specialization: PayPal Payment
class PayPalPayment extends Payment {
    private String email;

    public PayPalPayment(double amount, String payer, String email) {
        super(amount, payer);
        this.email = email;
    }

    @Override
    public void processPayment() {
        System.out.println("Processing PayPal payment of $" + amount + " from " + payer + " via " + email);
    }
}
```

```java
// Specialization: Cash Payment
class CashPayment extends Payment {
    public CashPayment(double amount, String payer) {
        super(amount, payer);
    }

    @Override
    public void processPayment() {
        System.out.println("Processing Cash payment of $" + amount + " from " + payer);
    }
}
```

---

### ✅ Step 3: Payment Processor
```java
// Third-party payment processor
class PaymentProcessor {
    public void processTransaction(Payment payment) {
        System.out.println("Initiating transaction...");
        payment.processPayment();
        System.out.println("Transaction completed.\n");
    }
}
```

---

### ✅ Step 4: Main Method (Client)
```java
public class ECommerceApp {
    public static void main(String[] args) {
        // Create different payment methods
        Payment creditCard = new CreditCardPayment(100.0, "Alice", "1234-5678-9012-3456");
        Payment payPal = new PayPalPayment(50.0, "Bob", "bob@example.com");
        Payment cash = new CashPayment(20.0, "Charlie");

        // Create the payment processor
        PaymentProcessor processor = new PaymentProcessor();

        // Process payments
        processor.processTransaction(creditCard);
        processor.processTransaction(payPal);
        processor.processTransaction(cash);
    }
}
```

---

## 3. Running the Code

### **Expected Console Output:**
```
Initiating transaction...
Processing Credit Card payment of $100.0 from Alice
Transaction completed.

Initiating transaction...
Processing PayPal payment of $50.0 from Bob via bob@example.com
Transaction completed.

Initiating transaction...
Processing Cash payment of $20.0 from Charlie
Transaction completed.
```

---

## 4. Key Concepts Demonstrated
| Concept | Explanation |
|---------|-------------|
| **Abstract Class (`Payment`)** | Generalizes attributes (amount, payer, date) and enforces `processPayment()` implementation in subclasses. |
| **Concrete Subclasses** | Implement `processPayment()` differently (CreditCard, PayPal, Cash). |
| **Encapsulation & Extensibility**| `PaymentProcessor` only works with `Payment` objects, ensuring better design. New payment types (e.g., `CryptoPayment`) can be added by simply **extending `Payment`**. |

---

## 5. When to Use Each Approach in Java
| Concept | Suitable Scenario | Example |
|---------|-------------------|---------|
| **Concrete Superclass** | When all subclasses **inherit** both attributes and behaviors. | `Employee → FullTimeEmployee, ContractEmployee` |
| **Abstract Superclass** | When all subclasses **share some behavior but must override specific methods**. | `Payment → CreditCardPayment, PayPalPayment` |
| **Interfaces** | When different classes **should share a behavior but don’t necessarily share an ancestor class** (they might be otherwise unrelated). | `Flyable → Bird, Airplane, Drone` or `Attackable` and `Defendable` for `GameCharacter`|





