# Common Software Patterns Reference

This reference documents common patterns to look for and apply during project analysis and development.

## Architectural Patterns

### MVC (Model-View-Controller)

**Structure:**
```
app/
├── Models/          # Data and business logic
├── Views/           # Presentation templates
└── Controllers/     # Request handling
```

**Characteristics:**
- Models handle data and business rules
- Views handle presentation
- Controllers coordinate between Model and View
- Clear separation of concerns

**Common in:** Laravel, Rails, Django, ASP.NET MVC

### Clean Architecture / Hexagonal

**Structure:**
```
src/
├── Domain/          # Core business logic (entities, value objects)
├── Application/     # Use cases, application services
├── Infrastructure/  # External concerns (DB, APIs, frameworks)
└── Presentation/    # UI, API endpoints
```

**Characteristics:**
- Dependencies point inward
- Domain has no external dependencies
- Infrastructure depends on domain, not vice versa
- Testable business logic

### Repository Pattern

**Structure:**
```
src/
├── Entities/
│   └── User.php
├── Repositories/
│   ├── UserRepositoryInterface.php
│   └── UserRepository.php
└── Services/
    └── UserService.php
```

**Interface:**
```php
interface UserRepositoryInterface {
    public function find(int $id): ?User;
    public function findAll(): array;
    public function save(User $user): void;
    public function delete(User $user): void;
}
```

**Benefits:**
- Abstracts data access
- Testable with mock repositories
- Decouples business logic from storage

### Service Layer

**Structure:**
```
src/
├── Services/
│   ├── UserService.php
│   ├── OrderService.php
│   └── PaymentService.php
```

**Characteristics:**
- Encapsulates business operations
- Coordinates between multiple repositories
- Transaction management
- Single entry point for business logic

## Design Patterns

### Factory Pattern

```typescript
// Factory Interface
interface UserFactory {
    createUser(data: UserData): User;
    createAdmin(data: AdminData): Admin;
}

// Implementation
class ConcreteUserFactory implements UserFactory {
    createUser(data: UserData): User {
        return new User(data.name, data.email);
    }
    
    createAdmin(data: AdminData): Admin {
        const admin = new Admin(data.name, data.email);
        admin.setPermissions(data.permissions);
        return admin;
    }
}
```

**Use when:**
- Object creation is complex
- Need to create different types of objects
- Want to decouple creation from usage

### Dependency Injection

```typescript
// Without DI (tightly coupled)
class UserService {
    private repository = new UserRepository(); // Hard dependency
}

// With DI (loosely coupled)
class UserService {
    constructor(private repository: UserRepositoryInterface) {}
}

// Usage
const service = new UserService(new UserRepository());
// Or for testing
const service = new UserService(new MockUserRepository());
```

**Benefits:**
- Testability
- Flexibility
- Loose coupling
- Easier to maintain

### Observer Pattern

```typescript
interface Observer {
    update(event: Event): void;
}

interface Subject {
    attach(observer: Observer): void;
    detach(observer: Observer): void;
    notify(event: Event): void;
}

class EventEmitter implements Subject {
    private observers: Observer[] = [];
    
    attach(observer: Observer): void {
        this.observers.push(observer);
    }
    
    notify(event: Event): void {
        for (const observer of this.observers) {
            observer.update(event);
        }
    }
}
```

**Use when:**
- Need to notify multiple objects of changes
- Event-driven architecture
- Decoupled communication

### Strategy Pattern

```typescript
interface PaymentStrategy {
    pay(amount: number): PaymentResult;
}

class CreditCardPayment implements PaymentStrategy {
    pay(amount: number): PaymentResult {
        // Credit card processing
    }
}

class PayPalPayment implements PaymentStrategy {
    pay(amount: number): PaymentResult {
        // PayPal processing
    }
}

class PaymentProcessor {
    constructor(private strategy: PaymentStrategy) {}
    
    processPayment(amount: number): PaymentResult {
        return this.strategy.pay(amount);
    }
}
```

**Use when:**
- Need interchangeable algorithms
- Want to avoid conditionals
- Behavior varies by context

## Coding Conventions by Language

### JavaScript/TypeScript

**Naming:**
- `camelCase` for variables and functions
- `PascalCase` for classes and types
- `UPPER_SNAKE_CASE` for constants
- `kebab-case` for file names (or `camelCase`)

**File Organization:**
```
src/
├── components/     # UI components
├── services/       # Business logic
├── utils/          # Utility functions
├── types/          # TypeScript types
├── hooks/          # React hooks
└── constants/      # Constants
```

### Python

**Naming (PEP 8):**
- `snake_case` for variables, functions, methods
- `PascalCase` for classes
- `UPPER_SNAKE_CASE` for constants
- `_private` prefix for private members

**File Organization:**
```
src/
├── models/
├── services/
├── utils/
├── exceptions/
└── __init__.py
```

### PHP

**Naming (PSR-1/PSR-12):**
- `PascalCase` for classes
- `camelCase` for methods
- `$camelCase` for variables
- `UPPER_SNAKE_CASE` for constants

**File Organization:**
```
src/
├── Models/
├── Services/
├── Repositories/
├── Exceptions/
└── Utils/
```

## Testing Patterns

### AAA Pattern (Arrange-Act-Assert)

```typescript
describe('Calculator', () => {
    it('should add two numbers correctly', () => {
        // Arrange
        const calculator = new Calculator();
        const a = 5;
        const b = 3;
        
        // Act
        const result = calculator.add(a, b);
        
        // Assert
        expect(result).toBe(8);
    });
});
```

### Test Doubles

**Mock** - Verifies interactions
```typescript
const mockRepository = {
    save: jest.fn(),
};
service.createUser(userData);
expect(mockRepository.save).toHaveBeenCalledWith(expectedUser);
```

**Stub** - Provides canned responses
```typescript
const stubRepository = {
    find: () => ({ id: 1, name: 'Test User' }),
};
```

**Fake** - Working implementation for testing
```typescript
class FakeUserRepository implements UserRepositoryInterface {
    private users: Map<number, User> = new Map();
    
    save(user: User): void {
        this.users.set(user.id, user);
    }
    
    find(id: number): User | undefined {
        return this.users.get(id);
    }
}
```

## Error Handling Patterns

### Custom Exception Hierarchy

```typescript
class AppError extends Error {
    constructor(
        message: string,
        public code: string,
        public statusCode: number = 500
    ) {
        super(message);
        this.name = 'AppError';
    }
}

class ValidationError extends AppError {
    constructor(message: string, public field?: string) {
        super(message, 'VALIDATION_ERROR', 400);
    }
}

class NotFoundError extends AppError {
    constructor(resource: string, id: string | number) {
        super(`${resource} with id ${id} not found`, 'NOT_FOUND', 404);
    }
}

class UnauthorizedError extends AppError {
    constructor(message: string = 'Unauthorized') {
        super(message, 'UNAUTHORIZED', 401);
    }
}
```

### Result Pattern (Alternative to Exceptions)

```typescript
type Result<T, E = Error> = 
    | { success: true; value: T }
    | { success: false; error: E };

function divide(a: number, b: number): Result<number, string> {
    if (b === 0) {
        return { success: false, error: 'Division by zero' };
    }
    return { success: true, value: a / b };
}

// Usage
const result = divide(10, 2);
if (result.success) {
    console.log(result.value); // 5
} else {
    console.error(result.error);
}
```

## API Design Patterns

### RESTful Conventions

| Method | Path | Action |
|--------|------|--------|
| GET | /users | List users |
| GET | /users/:id | Get user |
| POST | /users | Create user |
| PUT | /users/:id | Replace user |
| PATCH | /users/:id | Update user |
| DELETE | /users/:id | Delete user |

### Response Format

```json
{
    "data": { ... },
    "meta": {
        "page": 1,
        "perPage": 20,
        "total": 100
    }
}
```

### Error Response Format

```json
{
    "error": {
        "code": "VALIDATION_ERROR",
        "message": "Invalid input",
        "details": [
            {
                "field": "email",
                "message": "Invalid email format"
            }
        ]
    }
}
```
