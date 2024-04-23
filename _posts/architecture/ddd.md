---
layout: post
title: "DDD for ADHD people"
tags: ["DDD", "architecture"]
---

This is a short explanation of DDD pattern, ideally for ADHD.

![DDD or Clean Architecture](https://i.imgur.com/KBOfGhS.png)

Dependency Rule and implementing a layered architecture to create systems that are independent, testable, and adaptable to change.

## Architectural Concepts

Hexagonal Architecture, Onion Architecture, Screaming Architecture, DCI, and BCE are discussed as different architectural approaches for system design. These architectures aim to achieve separation of concerns and consist of layers for business rules and interfaces.

## Common Characteristics

- Systems built using these architectures are independent of frameworks, making them flexible and adaptable.
- They are highly testable as business rules can be tested independently from UI, database, or other external elements.
- UI, database, and other external components can be easily replaced without impacting the core business logic.

## Dependency Rule

- The Dependency Rule dictates that source code dependencies can only point inward, ensuring that inner layers remain unaware of outer layers.
- Data formats and naming conventions are kept consistent within each layer to maintain separation of concerns.

## Layered Approach

### Entities

Encapsulate enterprise-wide business rules and are independent of application-specific details.

### Use Cases

Use cases contain application-specific business logic and orchestrate interactions between entities.

### Interface Adapters

Convert data between internal and external formats, facilitating communication with databases, user interfaces, and other external systems.

### Frameworks and Drivers 

Those form the outermost layer and contain implementation details such as web frameworks and databases.

## Crossing Boundaries

- Interfaces and inheritance relationships are used to cross layer boundaries while adhering to the Dependency Rule.

- Dynamic polymorphism allows source code dependencies to oppose the flow of control, maintaining separation of concerns.

## Data Handling

- Data crossing layer boundaries should be simple and isolated, avoiding dependencies that violate the Dependency Rule.
- Passing simple data structures ensures flexibility and maintainability of the system.

## Conclusion

- Adhering to these architectural principles simplifies system design and maintenance, making systems testable and adaptable to changes in external components.

## References

[^1]: [The Clean Architecture](https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html).
