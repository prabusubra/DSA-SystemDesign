# Circuit Breaker Pattern

The **Circuit Breaker Pattern** prevents cascading failures in microservices by detecting failures and stopping further requests until the service recovers.

---

## 🔹 Why is Circuit Breaker Needed?
Imagine a **payment service** that calls an **external bank API**. If the bank API goes **down**, repeated requests will:
- ✅ **Increase latency** (waiting for timeouts)
- ✅ **Overload the system** (flooding it with failed requests)
- ✅ **Cause cascading failures** (other services depending on it also fail)

The **Circuit Breaker** prevents this by **blocking requests** when failures are detected and automatically **resumes** when the system stabilizes.

---

## 🔹 How Circuit Breaker Works?

### **1️⃣ Closed State (Normal Operation)**
- All requests are **allowed**.
- If failures occur, the system counts them.

### **2️⃣ Open State (Failure Detected)**
- If failures exceed a threshold, the breaker **trips to OPEN**.
- Requests are **blocked immediately** to prevent overloading.

### **3️⃣ Half-Open State (Recovery Phase)**
- After a **cool-off period**, the breaker **allows a few test requests**.
- If successful, it **closes** (back to normal).
- If failures persist, it **stays open** (blocking requests again).

---

## 🔹 Example: Implementing Circuit Breaker in Java (Spring Boot + Resilience4j)

### **🔸 Step 1: Add Dependencies**
```xml
<dependency>
    <groupId>io.github.resilience4j</groupId>
    <artifactId>resilience4j-spring-boot2</artifactId>
    <version>1.7.1</version>
</dependency>
```

### **🔸 Step 2: Configure Circuit Breaker**
```yaml
resilience4j.circuitbreaker:
  instances:
    paymentService:
      failureRateThreshold: 50  # If 50% requests fail, open circuit
      waitDurationInOpenState: 10000ms  # Time before checking recovery
      permittedNumberOfCallsInHalfOpenState: 5  # Allow 5 test requests
      slidingWindowSize: 10  # Monitor last 10 requests
```

### **🔸 Step 3: Apply Circuit Breaker to a Service**
```java
import io.github.resilience4j.circuitbreaker.annotation.CircuitBreaker;
import org.springframework.stereotype.Service;
import org.springframework.web.client.RestTemplate;

@Service
public class PaymentService {
    private final RestTemplate restTemplate = new RestTemplate();
    
    @CircuitBreaker(name = "paymentService", fallbackMethod = "fallbackPayment")
    public String processPayment() {
        return restTemplate.getForObject("http://bank-api.com/pay", String.class);
    }

    public String fallbackPayment(Exception e) {
        return "Payment service is down. Please try later.";
    }
}
```

### **🔸 Step 4: Call Payment Service**
```java
@RestController
@RequestMapping("/orders")
public class OrderController {
    @Autowired
    private PaymentService paymentService;

    @GetMapping("/pay")
    public String makePayment() {
        return paymentService.processPayment();
    }
}
```

---

## 🔹 Real-World Use Cases

1️⃣ **Netflix** – Uses Circuit Breaker to **handle API failures** between services.  
2️⃣ **E-Commerce** – Prevents failures in **Payment Gateway** from affecting Order Processing.  
3️⃣ **Banking Apps** – Avoids cascading failures if **external banking APIs** are down.  

---

## 🔹 Key Benefits
✅ **Improves System Stability** – Prevents failed services from affecting the entire system.  
✅ **Reduces Load on Failing Services** – Stops unnecessary traffic to broken components.  
✅ **Faster Recovery** – Automatically rechecks when the service becomes healthy.  

---


