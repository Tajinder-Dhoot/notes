## Dependency Inversion Principle


```markdown
## e.g. 1

### Before Applying Dependency Inversion
```

```csharp
public class EmailSender
{
    public void SendEmail(string message)
    {
        Console.WriteLine($"Email sent: {message}");
    }
}

public class NotificationService
{
    private EmailSender _emailSender = new EmailSender(); // Direct dependency

    public void Notify(string message)
    {
        _emailSender.SendEmail(message); // Tightly coupled
    }
}
```

```markdown
### After Applying Dependency Inversion
```

```csharp
public class Program
{
    public static void Main()
    {
        var email = new EmailSender();
        email.Send("Meeting is scheduled at 10am.");

        var sms = new SMSSender();
        sms.Send("Meeting is scheduled at 10am.");

        var emailNotification = new NotificationService(email);
        var smsNotification = new NotificationService(sms);

        emailNotification.Notify("You have a meeting in 15 mins.");
        smsNotification.Notify("You have a meeting in 15 mins.");
    }

    // Step 1: Define an abstraction
    public interface INotificationSender
    {
        void Send(string message);
    }

    // Step 2: Implement concrete classes
    public class EmailSender : INotificationSender
    {
        public void Send(string message)
        {
            Console.WriteLine($"Email sent: {message}");
        }
    }

    public class SMSSender : INotificationSender
    {
        public void Send(string message)
        {
            Console.WriteLine($"SMS sent: {message}");
        }
    }

    // Step 3: Depend on abstraction in the high-level module
    public class NotificationService
    {
        private readonly INotificationSender _notificationSender;

        // Dependency injection via constructor
        public NotificationService(INotificationSender notificationSender)
        {
            _notificationSender = notificationSender;
        }

        public void Notify(string message)
        {
            _notificationSender.Send(message); // Works with any INotificationSender
        }
    }
}
```

```markdown
## e.g. 2

### Before Applying Dependency Inversion
```

```csharp
// High-level module
public class UserService
{
    private UserRepository _userRepository;

    public UserService()
    {
        _userRepository = new UserRepository();
    }

    public void SaveUser(User user)
    {
        _userRepository.Save(user);
    }
}

// Low-level module
public class UserRepository
{
    public void Save(User user)
    {
        // Save user to database
    }
}
```

```markdown
### After Applying Dependency Inversion
```

```csharp
// High-level module
public class UserService
{
    private readonly IUserRepository _userRepository;

    public UserService(IUserRepository userRepository)
    {
        _userRepository = userRepository;
    }

    public void SaveUser(User user)
    {
        _userRepository.Save(user);
    }
}

// Low-level module
public interface IUserRepository
{
    void Save(User user);
}

public class UserRepository : IUserRepository
{
    public void Save(User user)
    {
        // Save user to database
    }
}
```