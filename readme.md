# Microservices Training and Proof of Concept project

## Overview

git-config-repo

Work in progress.

Proof of concept type project to experiment with various microservice technologies and provide reference for future work.

## High Level Goals and Tentative Plans:
* Include design artifacts simulating how Domain Driven Design using Event Storming sessions, C4 model diagrams
might have been used to do initial design and requirements gathering were this a real project.
* Implement multiple microservice projects and user interfaces.
* Implement event driven messaging architecture (Kafka)
* Spock testing
* Selenium ui testing
* Fully containerized

## Raw Notes on Specific Technologies to incorporate and try out:

  * Eclipse STS IDE
  
  * Gradle builds
  
  * Spring:
    * Spring Boot
    * Spring DevTools - runtime('org.springframework.boot:spring-boot-devtools')
    * Spring Web - compile('org.springframework.boot:spring-boot-starter-web')
    * Spring Test - testCompile('org.springframework.boot:spring-boot-starter-test')
    * Spring Actuator - compile('org.springframework.boot:spring-boot-starter-actuator')
    * Spring Data - compile('org.springframework.boot:spring-boot-starter-data-jpa')
    * Spring Cloud Config - compile('org.springframework.cloud:spring-cloud-starter-config')
    
  * H2 in-memory database - compile('com.h2database:h2')
  
  * Feign Rest Client
    * a declarative HTTP client developed by Netflix that makes calling other microservices much easier.
    * provides integration with Ribbon client side load balancing.
    * https://cloud.spring.io/spring-cloud-netflix/multi/multi_spring-cloud-feign.html
    * https://www.baeldung.com/intro-to-feign
    * compile('org.springframework.cloud:spring-cloud-starter-openfeign')
  
  * Ribbon
    * Netflix component for load balancing.
    * Ribbon is a Inter Process Communication (remote procedure calls) library with built in software load balancers. The primary usage model involves REST calls with various serialization scheme support.
    * https://cloud.spring.io/spring-cloud-netflix/multi/multi_spring-cloud-ribbon.html
    * compile('org.springframework.cloud:spring-cloud-starter-netflix-ribbon')
    * Used in currency-conversion-service to load balance across multiple instances of the currency-exchange service.
  
  * Eureka Naming Server from Netflix
    * Eureka is a REST (Representational State Transfer) based service that is primarily used in the AWS cloud for locating services for the purpose of load balancing and failover of middle-tier servers. 
    * https://spring.io/guides/gs/service-registration-and-discovery/
    * https://github.com/Netflix/eureka/wiki/Eureka-at-a-glance
    * http://www.springboottutorial.com/microservices-with-spring-boot-part-5-eureka-naming-server
    * services register themselves with the naming server when they come up and the naming server provides service discovery to client services.
    * limits-service, currency-calculation-service and currency-exchange-server register with eureka naming server.
    * 	compile('org.springframework.cloud:spring-cloud-starter-netflix-eureka-server')
    * compile('org.springframework.cloud:spring-cloud-starter-netflix-eureka-client')
  
  * Flyway  
  * Continuous Delivery and Deployment to AWS, Google Cloud, Pivotal Cloud
  * Auto scaling, Erueka naming server, Ribbon
  * Netflix OSS Components - hystrix, ...
  * In-memory Redis caching
  * Dockerized containers, Kubernetes orchestration
  * Github web and issue tracking
  * Zuul, Spring Cloud Sleuth
  * Spring, Spring Boot, Spring Cloud Config Server, Spring Data, Spring Cloud Slueth
  * In-memory Databases, MySQL, Postgres
  * Swagger api docs
  * Zuul API Gateway
  * UI's - Thymeleaf, Anglular, React
  * Messaging - RabbitMQ, Kafka
  * Distributed Tracing, Zipkin
  * Spring cloud bus
  * Security concerns, OAuth, facebook and google id's, ...
  * Fault Tolerance with Hystrix
  * Blue/Green and Canary Deployments
  * Try out an AWS lamba serverless implementation of the currency converter.
  * Choas monkey
  * Python service, perhaps some type of machine learning service?


## Tentative Ports

|     Application                   |     Port              |
| --------------------------------  | -------------         |
| Limits Service                    | 8080, 8081, ...       |
| Spring Cloud Config Server        | 8888 |
|                                   |                       |
| Currency Exchange Service         | 8000, 8001, 8002, ..  |
| Currency Conversion Service       | 8100, 8101, 8102, ... |
| Netflix Eureka Naming Server      | 8761                  |
| Netflix Zuul API Gateway Server   | 8765                  |
| Zipkin Distributed Tracing Server | 9411                  |


## Tentative URLs

|     Application                              | URL                     |
| -------------------------------------------- | ----------------------- |
| Limits Service                               | http://localhost:8080/limits POST -> http://localhost:8080/actuator/refresh|
| Spring Cloud Config Server                   | http://localhost:8888/limits-service/default, http://localhost:8888/limits-service/dev, http://localhost:8888/limits-service/qa |
| Currency Converter Service - Direct Call     | http://localhost:8100/currency-converter/from/USD/to/INR/quantity/10|
|  Currency Converter Service - Feign          | http://localhost:8100/currency-converter-feign/from/EUR/to/INR/quantity/10000|
| Currency Exchange Service                    | http://localhost:8000/currency-exchange/from/EUR/to/INR http://localhost:8001/currency-exchange/from/USD/to/INR|
| Eureka                                       | http://localhost:8761/ |
| Zuul - Currency Exchange & Exchange Services | http://localhost:8765/currency-exchange-service/currency-exchange/from/EUR/to/INR http://localhost:8765/currency-conversion-service/currency-converter-feign/from/USD/to/INR/quantity/10|
| Zipkin                                       | http://localhost:9411/zipkin/ |
| Spring Cloud Bus Refresh                     | http://localhost:8080/bus/refresh |
|                                              |                                   |
| H2 Console (currency-exchange-db)            | http://localhost:8000/h2-console  (use jbdc url: 'jdbc:h2:mem:testdb'                     |
