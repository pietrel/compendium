# CQS and CQRS

## Command Query Separation (CQS)

Command Query Separation is a design principle in software engineering that suggests separating methods that modify state (commands) from methods that return results without modifying state (queries). The idea is to keep operations that change the system's state distinct from operations that simply retrieve data. This separation helps in designing clearer, more maintainable code and can enhance the predictability of how changes affect the application. 
In short, individual methods in an object or service, stating that a method should either be a command (change the system's state) or a query (retrieve data) but not both.
It is the foundational principle behind CQRS.

## Introduction to Command Query Responsibility Separation (CQRS)
[Command Query Responsibility Segregation (CQRS)](https://doc.rust-cqrs.org/theory_cqrs.html)

Command Query Responsibility Segregation (CQRS) is an architectural pattern that separates the read and write operations of a data model into distinct interfaces. This approach can significantly enhance the performance, scalability, and security of an application. In this chapter, we will explore how to implement CQRS in a PHP environment, focusing on practical applications and benefits.

Core Concepts of CQRS
1. **Commands**: Actions that modify state. In PHP, commands are usually implemented as classes that encapsulate all the information needed to perform an action.
2. **Queries**: Requests for information. Unlike commands, queries do not modify any data.
3. **Command Handlers**: Logic to handle the execution of commands.
4. **Query Handlers**: Logic to retrieve data in response to queries.

```
              --------------          ---------------
     -------> |  Commands  | -------> |             | 
              --------------          |  CQRS       |
              --------------          |  Framework  |
     <------- |  Queries   | <------- |             |
              --------------          ---------------
```

## Implementing Command Query Responsibility Segregation (CQRS) in PHP

```php
class CreateUserCommand {
    public string $username;
    public string $email;
    public string $password;

    public function __construct(string $username, string $email, string $password) {
        $this->username = $username;
        $this->email = $email;
        $this->password = $password;
    }
}
```

```php
class CreateUserHandler {
    private UserRepository $userRepository;

    public function __construct(UserRepository $repository) {
        $this->userRepository = $repository;
    }

    public function handle(CreateUserCommand $command): void {
        $user = new User($command->username, $command->email, $command->password);
        $this->userRepository->save($user);
    }
}
```

```php
class FindUserByEmailQuery {
    public string $email;

    public function __construct(string $email) {
        $this->email = $email;
    }
}
```

```php
class FindUserByEmailHandler {
    private UserRepository $userRepository;

    public function __construct(UserRepository $repository) {
        $this->userRepository = $repository;
    }

    public function handle(FindUserByEmailQuery $query): ?User {
        return $this->userRepository->findByEmail($query->email);
    }
}
```
