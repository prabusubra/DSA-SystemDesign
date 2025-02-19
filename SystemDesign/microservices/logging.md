# Centralized Logging in Microservices

In a microservices architecture, multiple independent services generate logs. Without centralized logging, debugging and monitoring can become a nightmare, as logs are scattered across different services.

💡 **What is Centralized Logging?**

Centralized logging is the practice of aggregating logs from all microservices into a single location, making it easier to ***search, analyze, and monitor*** logs.

## Spring Boot Logging (Logback + SLF4J)

## Log Aggregation Tools

| Tool                        | Purpose                    | Works With |
|-----------------------------|---------------------------|------------|
| Elasticsearch + Logstash + Kibana (ELK) | Full-text search, UI logs in Kibana, REST API | Elasticsearch, Logstash, Kibana |
| Loki + Promtail + Grafana   | Lightweight log aggregation | Grafana |
| Fluentd                     | Log collector & forwarder  | Elasticsearch, Cloud |

## Real-Time Monitoring with Prometheus & Grafana

| Component              | Spring Cloud Solution                  |
|------------------------|--------------------------------------|
| Centralized Logging    | Logback + Logstash + ELK             |
| Tracing Requests      | Spring Cloud Sleuth + Zipkin         |
| Real-Time Monitoring   | Micrometer + Prometheus + Grafana   |
| Log Streaming to UI    | WebSockets or REST API              |
| Security & Compliance  | Secure log storage & auditing       |
