# CQRS

[Command Query Responsibility Segregation (CQRS)](https://doc.rust-cqrs.org/theory_cqrs.html) 

## Introduction to CQRS

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
