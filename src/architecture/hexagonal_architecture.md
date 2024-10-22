# Hexagonal Architecture

## Introduction

[Hexagonal Architecture](https://alistair.cockburn.us/hexagonal-architecture/) is an architectural pattern that aims to create a flexible and maintainable software system by decoupling the core business logic from the external interfaces. This approach is particularly useful for applications that require a high degree of modularity and testability. In this chapter, we will explore how to implement Hexagonal Architecture in a PHP environment, focusing on practical applications and benefits.

## Core Concepts of Hexagonal Architecture

1. **Core Business Logic**: The heart of the application, containing the domain-specific rules and operations.
2. **Ports and Adapters**: Interfaces that define how the core business logic interacts with the external world.
3. **Primary Ports**: Interfaces that expose the core business logic to the external world.
4. **Secondary Ports**: Interfaces that allow the core business logic to interact with external services and resources.
5. **Adapters**: Implementations of the ports that connect the core business logic to the external world.

```
               --------------          ---------------
      -------> |  Primary   | -------> |             | 
               |  Ports     |          |  Hexagonal  |
      <------- |            | <------- |  Architecture|
               --------------          |             |
               --------------          ---------------
      -------> |  Secondary | -------> |             | 
               |  Ports     |          |             |
      <------- |            | <------- |             |
               --------------          ---------------
```

## Implementing Hexagonal Architecture in PHP

### Defining Primary Ports

Primary ports define the interfaces through which the core business logic interacts with the external world. These interfaces should be technology-agnostic and focused on the domain-specific operations.

```php
interface UserRepository {
    public function findById(int $id): ?
    public function save(User $user): void;
}
```

```php
interface EmailService {
    public function sendEmail(string $to, string $subject, string $body): void;
}
```

### Defining Secondary Ports

Secondary ports define the interfaces through which the core business logic interacts with external services and resources. These interfaces should abstract away the implementation details of external dependencies.

```php
interface UserGateway {
    public function getUserById(int $id): ?User;
    public function saveUser(User $user): void;
}
```

```php
interface EmailGateway {
    public function send(string $to, string $subject, string $body): void;
}
```

### Implementing Adapters

Adapters are concrete implementations of the ports that connect the core business logic to the external world. These adapters handle the translation between the domain-specific operations and the external interfaces.

```php
class UserRepositoryAdapter implements UserRepository {
    private UserGateway $userGateway;

    public function __construct(UserGateway $userGateway) {
        $this->userGateway = $userGateway;
    }

    public function findById(int $id): ?User
    {
        return $this->userGateway->getUserById($id);
    }

    public function save(User $user): void
    {
        $this->userGateway->saveUser($user);
    }

}
```

```php
class EmailServiceAdapter implements EmailService {
    private EmailGateway $emailGateway;

    public function __construct(EmailGateway $emailGateway) {
        $this->emailGateway = $emailGateway;
    }

    public function sendEmail(string $to, string $subject, string $body): void
    {
        $this->emailGateway->send($to, $subject, $body);
    }
}
```

### Wiring Everything Together

In the application bootstrap process, we wire the core business logic with the adapters for the primary and secondary ports.

```php
$userGateway = new DatabaseUserGateway();
$userRepository = new UserRepositoryAdapter($userGateway);

$emailGateway = new SmtpEmailGateway();
$emailService = new EmailServiceAdapter($emailGateway);

$application = new Application($userRepository, $emailService);
```

### Benefits of Hexagonal Architecture

1. **Modularity**: The separation of concerns between the core business logic and the external interfaces allows for easier maintenance and updates.
2. **Testability**: The decoupling of the core logic from the external dependencies makes it easier to write unit tests and integration tests.
3. **Flexibility**: The ability to swap out adapters for different implementations without affecting the core logic provides flexibility in choosing external services and resources.
4. **Scalability**: The modular design of Hexagonal Architecture makes it easier to scale the application by adding new features or adapting to changing requirements.
5. **Security**: The clear separation of concerns reduces the risk of security vulnerabilities by limiting the exposure of the core logic to external interfaces.
6. **Maintainability**: The clean and organized structure of Hexagonal Architecture makes it easier to understand and maintain the codebase over time.
7. **Extensibility**: The flexibility of Hexagonal Architecture allows for easy extension of the application with new features and functionalities.
8. **Isolation**: The isolation of the core business logic from external dependencies reduces the risk of cascading failures and improves fault tolerance.
9. **Reusability**: The modular design of Hexagonal Architecture promotes code reuse and reduces duplication of logic across different parts of the application.
10. **Adaptability**: The ability to adapt to changing requirements and technologies by swapping out adapters for different implementations.
11. **Consistency**: The consistent structure and separation of concerns in Hexagonal Architecture lead to a more maintainable and predictable codebase.
12. **Performance**: The modular design of Hexagonal Architecture can improve performance by allowing for more efficient interactions with external services and resources.
13. **Documentation**: The clear separation of concerns in Hexagonal Architecture makes it easier to document and understand the application's design and functionality.
14. **Collaboration**: The modular design of Hexagonal Architecture facilitates collaboration among team members by providing clear boundaries between different components of the application.