# 💉 Dependency Injection (DI)

## What is Dependency Injection?

**Dependency Injection (DI)** is a design pattern that promotes **loose coupling** between components by injecting dependencies rather than hardcoding them inside a class. This makes the code more modular, testable, and maintainable.

Thats a smart way to handle function parameters.

## Example Without Dependency Injection

In this example, the `NotificationService` class directly creates an instance of `EmailService`, making it tightly coupled and difficult to test.

```python
class EmailService:
    def send_email(self, recipient, message):
        print(f"Sending email to {recipient}: {message}")

class NotificationService:
    def __init__(self):
        self.email_service = EmailService()  # Direct dependency creation
    
    def notify(self, user, message):
        self.email_service.send_email(user, message)
 
notification_service = NotificationService()
notification_service.notify("user@example.com", "Hello, Without DI!")
```

### Issues with This Approach
- The `NotificationService` class is **tightly coupled** to `EmailService`, making it hard to replace or mock for testing.
- It **violates the Dependency Inversion Principle** since high-level modules depend on low-level modules.

Imagine changing your email service for any reason and losing your current email provider. To keep your application running, you'll need to integrate a new service. Without a Dependency Injection (DI) approach, your application would require a complete overhaul to adapt to the new service.


## Example With Dependency Injection

Now, refactoring the code to inject the dependency via the constructor.

```python
class EmailService:
    def send_email(self, recipient, message):
        print(f"Sending email to {recipient}: {message}")

class NotificationService:
    def __init__(self, email_service):
        self.email_service = email_service  # Dependency is injected
    
    def notify(self, user, message):
        self.email_service.send_email(user, message)
 
email_service = EmailService()
notification_service = NotificationService(email_service)
notification_service.notify("user@example.com", "Hello, With DI!")
```

### Benefits of Using Dependency Injection
- **Loose coupling:** The `NotificationService` class does not create an instance of `EmailService`, making it easier to change implementations.
- **Improved testability:** We can inject a mock email service for unit testing.
- **Better maintainability and flexibility:** The dependency can be replaced or extended with minimal changes.

## Conclusion
Dependency Injection helps in writing cleaner, more maintainable, and testable code by removing tight dependencies between components. In my opinion, this approach is the most important *SOLID principle* and is widely used in modern software development.

