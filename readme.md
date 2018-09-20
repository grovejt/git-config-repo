# Microservices Training and Proof of Concept project

Work in progress.
Proof of concept type project to experiment with various microservice technologies.

Goals to accomplish:
* Include design artifacts simulating how Domain Driven Design using Event Storming sessions
might have been used to do initial design and requirements gathering were this a real project.
* Implement multiple microservice projects and user interfaces.
* Some specific technologies to incorperate:
** Continous Deliverery and Deployment to AWS, Google Cloud, Pivotal Cloud
** Auto scaling, Erueka naming server, Ribbon
** Netflix OSS Components - hystrix, ...
** Dockerized containers, Kubernetes orchestration
** Github web and issue trakcking
** Zuul, Spring Cloud Sleuth
** Spring, Spring Boot, Spring Cloud Config Server, Spring Data, Spring Cloud Slueth
** In-memory Databases, MySQL, Postgres
** Feign Rest Client
** Zuul API Gateway
** UI's - Thymeleaf, Anglular, React
** Messaging - RabbitMQ, Kafka
** Distributed Tracing, Zipkin
** Spring cloud bus
** Fault Tolerance with Hystrix


## Tentative Ports

|     Application       |     Port          |
| ------------- | ------------- |
| Limits Service | 8080, 8081, ... |
| Spring Cloud Config Server | 8888 |
|  |  |
| Currency Exchange Service | 8000, 8001, 8002, ..  |
| Currency Conversion Service | 8100, 8101, 8102, ... |
| Netflix Eureka Naming Server | 8761 |
| Netflix Zuul API Gateway Server | 8765 |
| Zipkin Distributed Tracing Server | 9411 |


## Tentative URLs

|     Application       |     URL          |
| ------------- | ------------- |
| Limits Service | http://localhost:8080/limits POST -> http://localhost:8080/actuator/refresh|
|Spring Cloud Config Server| http://localhost:8888/limits-service/default http://localhost:8888/limits-service/dev |
|  Currency Converter Service - Direct Call| http://localhost:8100/currency-converter/from/USD/to/INR/quantity/10|
|  Currency Converter Service - Feign| http://localhost:8100/currency-converter-feign/from/EUR/to/INR/quantity/10000|
| Currency Exchange Service | http://localhost:8000/currency-exchange/from/EUR/to/INR http://localhost:8001/currency-exchange/from/USD/to/INR|
| Eureka | http://localhost:8761/|
| Zuul - Currency Exchange & Exchange Services | http://localhost:8765/currency-exchange-service/currency-exchange/from/EUR/to/INR http://localhost:8765/currency-conversion-service/currency-converter-feign/from/USD/to/INR/quantity/10|
| Zipkin | http://localhost:9411/zipkin/ |
| Spring Cloud Bus Refresh | http://localhost:8080/bus/refresh |
