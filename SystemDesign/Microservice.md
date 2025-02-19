# Design Patterns

  - ### Gateway Pattern
      - Handle centralized autentication, loadbalancing and routing logics
      - Example: WSO2 API gateway, AWS API Gateway, Spring Cloud API Gateway
  
  - ### Service Registry Pattern
    
      An e-commerce app dynamically discovers microservices (Cart Service, Payment Service) without hardcoding IPs.
    
      - Client-Side
        
        - Eureka (Netflix OSS)
          
      - Server-Side
          - Consul and Zookeeper
        
  - ### [Circuit Breaker](https://github.com/prabusubra/DSA-SystemDesign/blob/main/SystemDesign/microservices/circuitbreakers.md)
      - The Circuit Breaker Pattern is used to prevent cascading failures in microservices by detecting failures and stopping further requests until the service recovers.
      - Example: Resilient4J
          #### States:
            1. Closed State
                  All the requests are allowed.
            2. Open State
                  If failures exceed a threshold, the breaker trips to OPEN.
                  Requests are blocked immediately to prevent overloading.
            3. Half-Open State
                  After a cool-off period, the breaker allows a few test requests.
                  If successful, it closes (back to normal).
                  If failures persist, it stays open (blocking requests again).


  - ### SAGA Pattern
  - ### CQRS Pattern
  - ### Bulkhead Pattern
  - ### Sidecar pattern
  - ### API Composition Pattern
  - ### Event-Driven Pattern
  - ### Database Per Service Pattern
  - ### Retry Pattern
  - ### Configuration Externalization Pattern
  - ### Strangler Fig Pattern
  - ### Leader Election Pattern
  - ### [Centralized Logging](file///SystemDesign/microservices/logging.md)
