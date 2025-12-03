# Currency Conversion Microservices Project

💡 Overview
A distributed Spring Boot microservices project demonstrating service discovery, API gateway routing, Feign-based inter-service communication, Redis caching, Zipkin tracing, and centralized monitoring.

🚀 Tech Stack
Component	Technology
☕ Backend Framework	Spring Boot 3+
🔗 Inter-Service Communication	OpenFeign
⚙️ Service Discovery	Netflix Eureka
🌉 API Gateway	Spring Cloud Gateway (WebFlux)
🧠 Caching	Redis
📡 Distributed Tracing	Zipkin + Micrometer
🧾 Monitoring	Spring Boot Admin
🗃️ Database	MySQL
🧰 Build Tool	Maven
🐳 Runtime	Java 17+

```
## 📁 **Folder Structure**

Currency-microservices/
│
├── eureka-server/                    # Service Discovery (Eureka)
│   ├── src/main/java/com/sathya/eureka/
│   └── src/main/resources/application.properties
│
├── api-gateway/                      # Gateway Routing Layer (Spring Cloud Gateway + WebFlux)
│   ├── src/main/java/com/sathya/gateway/
│   └── src/main/resources/application.properties
│
├── currency-exchange-service/        # Provides exchange rate data
│   ├── src/main/java/com/sathya/exchange/
│   │   ├── controller/
│   │   ├── service/
│   │   ├── repository/
│   │   └── model/
│   └── src/main/resources/application.properties
│
├── currency-conversion-service/      # Uses Feign to call Exchange + Redis cache for results
│   ├── src/main/java/com/sathya/conversion/
│   │   ├── controller/
│   │   ├── service/
│   │   ├── repository/
│   │   ├── dto/
│   │   └── config/                   # CacheConfig.java
│   └── src/main/resources/application.properties
│
├── redis-cache-service/              # (optional standalone Redis setup or Docker config)
│   └── Dockerfile or redis.conf
│
├── admin-server/                     # Spring Boot Admin dashboard for monitoring
│   ├── src/main/java/com/sathya/admin/
│   └── src/main/resources/application.properties
│
├── zipkin-server/                    # Distributed tracing collector (Zipkin)
│   └── docker-compose.yml
│
├── pom.xml                           # Parent POM (if using multi-module)
├── README.md                         # Project Documentation
└── screenshots/                  # Optional: add images of Zipkin & Admin dashboards

```

🧩Microservice Architecture
Service	Port	Responsibility
🗺️ Eureka Server	8761	Service Discovery & Registration
🌉 API Gateway	8080	Routes requests to downstream services
💱 Currency Exchange Service	8005	Provides currency exchange rates
🔄 Currency Conversion Service	8006	Converts currency using Feign + Redis Cache
🧰 Redis Cache Server	6379	Stores cached conversion results
📈 Zipkin Server	9411	Distributed tracing for all microservices
🖥️ Spring Boot Admin Server	9000	Monitors and manages all microservices

⚙️ Project Flow
Request hits API Gateway → /api/v1/conversion
Routed to Currency Conversion Service
Feign Client calls Currency Exchange Service
Result calculated and cached in Redis
Tracing sent to Zipkin, health to Admin Server

🧮 Caching Behavior
First request: DB + Redis store
Subsequent requests: Redis cache
TTL: 10 minutes (configurable)

🖼️ Screenshots

# Eureka Server

<img width="1920" height="1080" alt="eureka-server" src="https://github.com/user-attachments/assets/038e640d-02e5-4967-bf25-01d1cc489a0a" />

# Admin Server

<img width="1920" height="1080" alt="admin-server-2" src="https://github.com/user-attachments/assets/9bbe90ac-32dc-4f97-9d0d-cf03c7c862d0" />

# Conversion Service (Postman Test)

<img width="1920" height="1080" alt="conversion-postman" src="https://github.com/user-attachments/assets/a4d9979d-e4d4-4d04-934b-5b3b6d0dde1a" />

# Zipkin Server

<img width="1920" height="1080" alt="zipkin-server" src="https://github.com/user-attachments/assets/4b90fe40-d52a-4a87-afd3-84dc46a31df1" />


##⚡ How to Run Locally

Start Eureka Server

mvn spring-boot:run -pl eureka-server

Start Config Server

mvn spring-boot:run -pl config-server

Start other microservices (Currency, Conversion, Gateway, Admin, Zipkin) Each service will automatically register with Eureka and use config from GitHub.

Access Services:

Service URL Eureka Dashboard http://localhost:8761

Config Server http://localhost:8888

API Gateway http://localhost:8080

Currency Service http://localhost:8005

Conversion Service http://localhost:8006

Admin Server http://localhost:9000

Zipkin Server http://localhost:9411 🧾 Example API Calls

Currency Service Example:

GET http://localhost:8005/currency/USD

Conversion Service Example:

GET http://localhost:8006/conversion/from/USD/to/INR/amount/100

Through Gateway:

GET http://localhost:8080/conversion-service/conversion/from/USD/to/INR/amount/100

🧩 Monitoring and Tracing

View all services in Spring Boot Admin Dashboard

View API call traces in Zipkin UI

All logs are traced automatically using management.zipkin.tracing.endpoint

🏁 Future Enhancements

🔹 Add JWT authentication for secured endpoints 🔹 Integrate Grafana + Prometheus for advanced monitoring 🔹 Dockerize all services for containerized deployment

👨‍💻 Author

Imran Attar 📧 Developer | Spring Boot Enthusiast
