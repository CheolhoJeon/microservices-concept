# A pattern language for microservices

[![npm](https://img.shields.io/badge/version-2019.29-brightgreen.svg)]()

> **참고 문헌**
>
> 본 문서는 [Microservices.io](https://microservices.io)에서 작성한 [A pattern language for microservices](https://microservices.io/patterns/index.html)를 번역한 문서입니다.
>
> **Reference**
>
> This document is a translation of [A pattern language for microservices](https://microservices.io/patterns/index.html) written by [Microservices.io](https://microservices.io).



## Application architecture patterns

애플리케이션을 개발하기 위해 어떤 설계 기법을 채택할 것인가?

- [Monolithic architecture](https://microservices.io/patterns/monolithic.html) - 애플리케이션을 하나의 배포 가능한 단위로 설계합니다
- [Microservice architecture](https://microservices.io/patterns/microservices.html) - 애플리케이션을 느슨하게 결합된 서비스들의 집합으로 설계합니다



## Decomposition

어떻게 애플리케이션을 서비스 단위로 분해할 것인가?

- [Decompose by business capability](https://microservices.io/patterns/decomposition/decompose-by-business-capability.html) - 서비스를 비즈니스 기능에 일치하게 정의합니다
- [Decompose by subdomain](https://microservices.io/patterns/decomposition/decompose-by-subdomain.html) - 서비스를 DDD 하위 도메인에 일치하게 정의합니다



## Deployment patterns

How to deploy an application’s services?

- [Multiple service instances per host](https://microservices.io/patterns/deployment/multiple-services-per-host.html) - deploy multiple service instances on a single host
- [Service instance per host](https://microservices.io/patterns/deployment/single-service-per-host.html) - deploy each service instance in its own host
- [Service instance per VM](https://microservices.io/patterns/deployment/service-per-vm.html) - deploy each service instance in its VM
- [Service instance per Container](https://microservices.io/patterns/deployment/service-per-container.html) - deploy each service instance in its container
- [Serverless deployment](https://microservices.io/patterns/deployment/serverless-deployment.html) - deploy a service using serverless deployment platform
- [Service deployment platform](https://microservices.io/patterns/deployment/service-deployment-platform.html) - deploy services using a highly automated deployment platform that provides a service abstraction



## Cross cutting concerns

How to handle cross cutting concerns?

- [Microservice chassis](https://microservices.io/patterns/microservice-chassis.html) - a framework that handles cross-cutting concerns and simplifies the development of services
- [Externalized configuration](https://microservices.io/patterns/externalized-configuration.html) - externalize all configuration such as database location and credentials



## Communication patterns

### Style

Which communication mechanisms do services use to communicate with each other and their external clients?

- [Remote Procedure Invocation](https://microservices.io/patterns/communication-style/rpi.html) - use an RPI-based protocol for inter-service communication
- [Messaging](https://microservices.io/patterns/communication-style/messaging.html) - use asynchronous messaging for inter-service communication
- [Domain-specific protocol](https://microservices.io/patterns/communication-style/domain-specific.html) - use a domain-specific protocol



### External API

How do external clients communicate with the services?

- [API gateway](https://microservices.io/patterns/apigateway.html) - a service that provides each client with unified interface to services
- [Backend for front-end](https://microservices.io/patterns/apigateway.html) - a separate API gateway for each kind of client



### Service discovery

How does the client of an RPI-based service discover the network location of a service instance?

- [Client-side discovery](https://microservices.io/patterns/client-side-discovery.html) - client queries a service registry to discover the locations of service instances
- [Server-side discovery](https://microservices.io/patterns/server-side-discovery.html) - router queries a service registry to discover the locations of service instances
- [Service registry](https://microservices.io/patterns/service-registry.html) - a database of service instance locations
- [Self registration](https://microservices.io/patterns/self-registration.html) - service instance registers itself with the service registry
- [3rd party registration](https://microservices.io/patterns/3rd-party-registration.html) - a 3rd party registers a service instance with the service registry



### Reliability

How to prevent a network or service failure from cascading to other services?

- [Circuit Breaker](https://microservices.io/patterns/reliability/circuit-breaker.html) - invoke a remote service via a proxy that fails immediately when the failure rate of the remote call exceeds a threshold



### Transactional messaging

How to publish messages as part of a database transaction?

- [Transactional outbox](https://microservices.io/patterns/data/application-events.html)
- [Transaction log tailing](https://microservices.io/patterns/data/transaction-log-tailing.html)
- [Polling publisher](https://microservices.io/patterns/data/polling-publisher.html)



## Data management

어떻게 데이터의 일관성을 유지하고 쿼리를 구현할 것인가?

- [Database per Service](https://microservices.io/patterns/data/database-per-service.html) - 각 서비스 별로 프라이빗 데이터베이스를 소유합니다
- [Shared database](https://microservices.io/patterns/data/shared-database.html) - 각 서비스들이 하나의 데이터베이스를 공유합니다
- [Saga](https://microservices.io/patterns/data/saga.html) - use sagas, which a sequences of local transactions, to maintain data consistency across services
- [API Composition](https://microservices.io/patterns/data/api-composition.html) - implement queries by invoking the services that own the data and performing an in-memory join
- [CQRS](https://microservices.io/patterns/data/cqrs.html) - implement queries by maintaining one or more materialized views that can be efficiently queried
- [Event sourcing](https://microservices.io/patterns/data/event-sourcing.html) - persist aggregates as a sequence of events



## Security

How to communicate the identity of the requestor to the services that handle the request?

- [Access Token](https://microservices.io/patterns/security/access-token.html) - a token that securely stores information about user that is exchanged between services



## Testing

How to make testing easier?

- [Consumer-driven contract test](https://microservices.io/patterns/testing/service-integration-contract-test.html) - a test suite for a service that is written by the developers of another service that consumes it
- [Consumer-side contract test](https://microservices.io/patterns/testing/service-integration-contract-test.html) - a test suite for a service client (e.g. another service) that verifies that it can communicate with the service
- [Service component sest](https://microservices.io/patterns/testing/service-component-test.html) - a test suite that tests a service in isolation using test doubles for any services that it invokes



## Observability

How to understand the behavior of an application and troubleshoot problems?

- [Log aggregation](https://microservices.io/patterns/observability/application-logging.html) - aggregate application logs
- [Application metrics](https://microservices.io/patterns/observability/application-metrics.html) - instrument a service’s code to gather statistics about operations
- [Audit logging](https://microservices.io/patterns/observability/audit-logging.html) - record user activity in a database
- [Distributed tracing](https://microservices.io/patterns/observability/distributed-tracing.html) - instrument services with code that assigns each external request an unique identifier that is passed between services. Record information (e.g. start time, end time) about the work (e.g. service requests) performed when handling the external request in a centralized service
- [Exception tracking](https://microservices.io/patterns/observability/exception-tracking.html) - report all exceptions to a centralized exception tracking service that aggregates and tracks exceptions and notifies developers.
- [Health check API](https://microservices.io/patterns/observability/health-check-api.html) - service API (e.g. HTTP endpoint) that returns the health of the service and can be pinged, for example, by a monitoring service
- [Log deployments and changes](https://microservices.io/patterns/observability/log-deployments-and-changes.html)new



## UI patterns

How to implement a UI screen or page that displays data from multiple services?

- [Server-side page fragment composition](https://microservices.io/patterns/ui/server-side-page-fragment-composition.html) - build a webpage on the server by composing HTML fragments generated by multiple, business capability/subdomain-specific web applications
- [Client-side UI composition](https://microservices.io/patterns/ui/client-side-ui-composition.html) - Build a UI on the client by composing UI fragments rendered by multiple, business capability/subdomain-specific UI components