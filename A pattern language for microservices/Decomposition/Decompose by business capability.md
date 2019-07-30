# Pattern: Decompose by business capability

[![npm](https://img.shields.io/badge/version-2019.30-brightgreen.svg)]()



## 상황

당신은 크고 복잡한 애플리케이션을 개발하는 중이며 마이크로서비스 아키텍처를 적용하려고 합니다. 마이크로서비스 아키텍처는 애플리케이션을 느슨하게 결합한 서비스들의 집합으로 구조화합니다. 마이크로서비스 아키텍처의 목표는 CI/CD를 가능하게 함으로써 소프트웨어 개발을 가속화 하는 것입니다.

![img](https://microservices.io/i/successtriangle.png)

마이크로서비스 아키텍처는 다음 두 가지 방법으로 이를 수행합니다.

1. 테스트를 간소화하고 컴포넌트들을 독립적으로 배포할 수 있게 합니다.
2. 엔지니어링 조직을 소규모(6~10 명)으로 구성하고 자율 팀을 구성하며 각 팀은 하나 또는 그 이상의 서비스를 담당합니다.

이러한 혜택은 자연스레 얻어지는 것이 아닙니다. 대신에 응용 프로그램을 서비스 단위로 세분화하여 기능을 수행해야만 이러한 혜택을 취할 수 있습니다.

하나의 서비스는 작은 팀에서 개발하고 쉽게 테스트를 할 수 있을만큼 작아야합니다. OOD(Object-Oriented Design)의 유용한 지침 중 [SRP(Single Responsibility Principle)](http://www.objectmentor.com/resources/articles/srp.pdf)이 있습니다. SRP는 클래스의 책임을 변경해야 할 이유로 정의하고 클래스에는 변경해야 할 한 가지 이유만 있어야 한다고 명시합니다. SRP를 서비스 디자인에 적용하고 일관성 있는 서비스를 설계하고 강력하게 관련된 작은 기능 세트를 구현하는 것이 이치에 맞습니다.

또한 애플리케이션은 보통 새롭거나 수정된 요구사항이 단일 서비스에만 영향을 미치도록 분해됩니다. 이는 여러 서비스에 영향을 미치는 변경 사항이 여러 팀간에 조정을 필요로 함으로써 개발 속도를 느려지게 만들기 때문입니다. OOD의 또 다른 유용한 지침 중 하나는 CCP(Common Closure Principle)입니다. 동일한 이유로 변경되는 클래스는 동일한 패키지에 있어야 합니다. 예를 들어, 두 클래스는 동일한 비즈니스 규칙의 다른 측면을 구현합니다. The goal is that when that business rule changes developers, only need to change code in a small number - ideally only one - of packages. 이러한 종류의 사고는 서비스를 설계할 때 각 변경 사항이 하나의 서비스에만 영향을 미치도록 보장하기 때문에 의미가 있습니다.



## 문제

애플리케이션을 어떻게 서비스들로 분해할 것인가?



## Forces

- 아키텍처는 안정적이어야 합니다.
- 서비스는 응집력이 있어야 합니다. 서비스는 강하게 관련된 기능의 작은 집합을 구현해야 합니다.
- 서비스는 공통 변경 원칙(Common Closure Principle)을 준수해야 합니다. 변경 사항은 함께 포장되어야 하며 각 변경 사항은 하나의 서비스에만 영향을 줘야 합니다.
- 서비스는 느슨하게 결합하여야 합니다. 각 서비스는 구현을 캡슐화하는 API입니다. 클라이언트에 영향을 주지 않고 구현을 변경할 수 있습니다.
- 서비스는 테스트 가능해야 합니다.
- 각 서비스는 "two pizza"팀, 즉 6-10명으로 구성된 팀에 의해 개발 될 만큼 충분히 작아야 합니다.
- 하나 이상의 서비스를 소유하고 있는 각 팀은 자율적이어야 합니다. 팀은 다른 팀과 최소한의 협업을 통해 서비스를 개발하고 배포할 수 있어야 합니다.



## 해결책

비즈니스 기능에 해당하는 서비스를 정의하십시오. 비즈니스 기능은 비즈니스 아키텍처 모델링의 개념입니다. 가치 창출을 위해 비즈니스가 하는 일입니다. 아래와 같이 비즈니스 기능은 종종 비즈니스 객체에 해당합니다.

- *Order Management*는 주문에 대한 책임을 가집니다.
- *Customer Management*는 고객에 대한 책임을 가집니다.

Business capabilities are often organized into a multi-level hierarchy. For example, an enterprise application might have top-level categories such as *Product/Service development*, *Product/Service delivery*, *Demand generation*, etc.(??)



## 예제

온라인 쇼핑몰은 다음과 같은 비즈니스 기능을 포함합니다.

- Product catalog management
- Inventory management
- Order management
- Delivery management
- …

해당 마이크로서비스 아키텍처는 이러한 각 기능에 해당하는 서비스를 제공합니다.

![img](https://microservices.io/i/decompose-by-business-capability.png)



## 예상되는 상황

이 패턴은 다음과 같은 이점이 있습니다.

* 비즈니스 기능이 비교적 안정적이기 때문에 아키텍처가 안정적입니다.
* 개발 팀은 기술적 기능보다는 비즈니스 가치를 제공하기 위해 [cross-functional](https://perfectial.com/blog/make-a-cross-functional-team-work/)하고 자율적으로 구성됩니다.

- 서비스는 응집력이 있고 느슨하게 결합됩니다.



## 이슈

아래는 해결해야할 이슈입니다.

* **어떻게 비즈니스 기능을 식별할 것인가?** 비즈니스 역량 및 서비스를 식별하려면 비즈니스에 대한 이해가 필요합니다. 조직의 비즈니스 기능은 조직의 목적, 구조, 비즈니스 프로세스 및 전문 분야를 분석하여 식별됩니다. 바운디드 컨텍스트는 반복 프로세스를 사용하여 가장 잘 식별됩니다. 비즈니스 기능을 식별하기 좋은 출발점은 다음과 같습니다.
  * organization structure - 조직 내의 서로 다른 그룹들은 비즈니스 기능 또는 비즈니스 기능 그룹에 해당할 수 있습니다.
  * high-level domain model - 비즈니스 기능은 종종 도메인 객체에 해당합니다.



## 관련 패턴

- [Decompose by subdomain](https://microservices.io/patterns/decomposition/decompose-by-subdomain.html) 패턴을 대안으로 사용할 수 있습니다.





> **참고 문헌**
>
> 본 문서는 [Microservices.io](https://microservices.io)에서 작성한 [A pattern language for microservices](https://microservices.io/patterns/index.html)를 번역한 문서입니다.
>
> **Reference**
>
> This document is a translation of [A pattern language for microservices](https://microservices.io/patterns/index.html) written by [Microservices.io](https://microservices.io).
