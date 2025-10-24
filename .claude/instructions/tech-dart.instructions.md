---
description: Core Dart development standards and best practices for all Dart frameworks
applyTo: "**/*.dart"
---

# Dart Development Standards

## 🏗️ Architecture & Navigation
- **Root Standards**: [General Coding Standards](./tech-general-coding.instructions.md)
- **Security Guidelines**: [Security & OWASP](./security-owasp.instructions.md)
- **Performance Guidelines**: [Performance Optimization](./tech-performance-optimization.instructions.md)
- **Framework Extensions**: [Flutter](./tech-flutter.instructions.md)

---

## 🎯 Dart-Specific Context

- **Dart Version**: 3.x+ (prefer latest stable for new projects)
- **Code Style**: Effective Dart Style Guide, Dart lints
- **Build Tools**: pub (Dart package manager), build_runner for code generation
- **Architecture Patterns**: Clean Architecture, MVVM, BLoC, Repository Pattern
- **Common Frameworks**: Flutter, AngularDart, shelf (backend), serverpod

## 🔧 Dart Language Standards

### Code Quality & Modern Dart Features
- **Dart Version**: Use Dart 3+ features (records, patterns, sealed classes, class modifiers)
- **Null Safety**: Leverage sound null safety (`?`, `!`, late, required)
- **Access Modifiers**: Use underscores (`_`) for private members, keep public API minimal
- **Immutability**: Prefer `final` for variables, use `const` constructors when possible
- **Type Safety**: Explicit types for public APIs, `var` for local variables when type is obvious
- **Modern Features**: Use records, pattern matching, and sealed classes for better type safety

### Object-Oriented Design
- **SOLID Principles**: Apply Single Responsibility, Open/Closed, Liskov Substitution, Interface Segregation, Dependency Inversion
- **Design Patterns**: Use appropriate patterns (Factory, Builder, Strategy, Observer) when they solve real problems
- **Composition over Inheritance**: Prefer composition and mixins over deep inheritance hierarchies
- **Encapsulation**: Keep implementation details private (use `_` prefix), expose behavior through well-defined interfaces
- **Mixins**: Use mixins for shared behavior across unrelated classes
- **Extensions**: Use extension methods to add functionality to existing types

### Collections & Iterables
- **Collections Framework**: Use appropriate collection types (List, Set, Map, Queue) based on use case
- **Iterable Operations**: Leverage map, where, fold, reduce for data processing
- **Immutable Collections**: Use `const` for immutable collections (`const [1, 2, 3]`)
- **Spread Operators**: Use spread (`...`) and null-aware spread (`...?`) for collection manipulation
- **Collection If/For**: Use collection if and for for conditional and iterative collection building
- **Performance**: Be aware of collection performance (List vs Set lookup, growable vs fixed-length)

### Asynchronous Programming
- **Future & Stream**: Use `Future` for single async values, `Stream` for sequences of async values
- **Async/Await**: Prefer async/await over raw Future callbacks for readability
- **Error Handling**: Use try-catch with async/await, handle errors in Stream subscriptions
- **Stream Controllers**: Properly close StreamControllers to prevent memory leaks
- **Isolates**: Use isolates for CPU-intensive operations to avoid blocking the main thread
- **Async Generators**: Use async* and sync* for creating streams and iterables

### Exception Handling
- **Exception Types**: Throw and catch specific exception types (Exception, Error subclasses)
- **Custom Exceptions**: Create specific exception types for different error scenarios
- **Error vs Exception**: Use Error for programming mistakes, Exception for runtime issues
- **Finally Blocks**: Ensure proper resource cleanup in finally blocks
- **Stack Traces**: Preserve stack traces when rethrowing exceptions

## 📁 Project Structure

```
lib/
├── main.dart                              # Application entry point
├── app.dart                               # Root application configuration
├── core/                                  # Core functionality
│   ├── constants/
│   │   ├── app_constants.dart
│   │   └── api_constants.dart
│   ├── config/
│   │   ├── app_config.dart
│   │   └── environment.dart
│   ├── errors/
│   │   ├── exceptions.dart
│   │   └── failures.dart
│   ├── network/
│   │   ├── api_client.dart
│   │   └── network_info.dart
│   └── utils/
│       ├── logger.dart
│       ├── validators.dart
│       └── extensions.dart
├── features/                              # Feature modules
│   ├── authentication/
│   │   ├── data/
│   │   │   ├── models/                   # Data models
│   │   │   │   ├── user_model.dart
│   │   │   │   └── auth_response_model.dart
│   │   │   ├── datasources/              # Data sources
│   │   │   │   ├── auth_remote_datasource.dart
│   │   │   │   └── auth_local_datasource.dart
│   │   │   └── repositories/             # Repository implementations
│   │   │       └── auth_repository_impl.dart
│   │   ├── domain/
│   │   │   ├── entities/                 # Domain entities
│   │   │   │   └── user.dart
│   │   │   ├── repositories/             # Repository interfaces
│   │   │   │   └── auth_repository.dart
│   │   │   └── usecases/                 # Business logic
│   │   │       ├── login_usecase.dart
│   │   │       └── register_usecase.dart
│   │   └── presentation/
│   │       ├── providers/                # State management
│   │       │   └── auth_provider.dart
│   │       ├── widgets/                  # UI components
│   │       │   └── login_form.dart
│   │       └── screens/                  # Full screens
│   │           └── login_screen.dart
│   ├── home/
│   └── profile/
├── shared/                                # Shared across features
│   ├── models/
│   │   └── api_response.dart
│   ├── widgets/
│   │   ├── buttons/
│   │   └── inputs/
│   └── services/
│       ├── storage_service.dart
│       └── analytics_service.dart
└── l10n/                                  # Localization
    └── app_localizations.dart

test/
├── unit/                                  # Unit tests
│   ├── core/
│   │   └── utils/
│   │       └── validators_test.dart
│   └── features/
│       └── authentication/
│           ├── domain/
│           │   └── usecases/
│           │       └── login_usecase_test.dart
│           └── data/
│               └── repositories/
│                   └── auth_repository_impl_test.dart
├── widget/                                # Widget tests (Flutter)
│   └── features/
│       └── authentication/
│           └── presentation/
│               └── widgets/
│                   └── login_form_test.dart
├── integration/                           # Integration tests
│   └── authentication_flow_test.dart
├── fixtures/                              # Test data
│   └── test_data.json
└── helpers/                               # Test utilities
    └── test_helpers.dart
```

## 🧪 Dart Testing Standards

### Testing Framework & Tools
- **Primary Framework**: `test` package for unit tests
- **Widget Testing**: `flutter_test` for Flutter widget tests (if applicable)
- **Mocking**: `mockito` or `mocktail` for mocking dependencies
- **Coverage**: `coverage` package with minimum 80% coverage on critical paths
- **Integration Testing**: `integration_test` package for end-to-end tests
- **Test Data**: Use builders or factories for complex test objects

### Test Organization
- **Test Structure**: Mirror source package structure in test directory
- **Test Naming**: `should_returnX_when_givenY` or descriptive test names
- **Test Groups**: Use `group()` to organize related tests
- **Test Categories**: Unit, Widget, Integration tests in separate directories
- **Mock Strategy**: Mock external dependencies, use real objects for domain logic
- **Test Data**: Use fixtures and const values for consistent test data

### Testing Best Practices
```dart
// Good: Descriptive test with proper structure
test('should return User when login is successful', () async {
  // Arrange
  final mockAuthRepository = MockAuthRepository();
  final usecase = LoginUsecase(mockAuthRepository);
  final credentials = LoginCredentials(
    email: 'test@example.com',
    password: 'password123',
  );
  
  when(() => mockAuthRepository.login(any()))
      .thenAnswer((_) async => Right(User(id: '1', email: 'test@example.com')));
  
  // Act
  final result = await usecase(credentials);
  
  // Assert
  expect(result.isRight(), true);
  result.fold(
    (failure) => fail('Should not return failure'),
    (user) => expect(user.email, 'test@example.com'),
  );
  verify(() => mockAuthRepository.login(credentials)).called(1);
});

// Good: Group related tests
group('LoginUsecase', () {
  late LoginUsecase usecase;
  late MockAuthRepository mockAuthRepository;
  
  setUp(() {
    mockAuthRepository = MockAuthRepository();
    usecase = LoginUsecase(mockAuthRepository);
  });
  
  test('should return User when credentials are valid', () async {
    // Test implementation
  });
  
  test('should return Failure when credentials are invalid', () async {
    // Test implementation
  });
  
  tearDown(() {
    // Cleanup if needed
  });
});
```

### Test Independence & Best Practices
- **Test Independence**: Each test should be independent and repeatable
- **Setup/Teardown**: Use `setUp()` and `tearDown()` for test initialization and cleanup
- **Assertions**: Use meaningful assertions with descriptive failure messages
- **Test Doubles**: Prefer mocks over stubs, avoid over-mocking
- **Async Testing**: Properly handle async operations with `async` and `await`
- **Coverage Focus**: Focus on business logic, critical paths, and edge cases

## 🚫 Dart Anti-Patterns

### Code Smells to Avoid
- **God Classes**: Avoid classes with too many responsibilities (use composition)
- **Primitive Obsession**: Use custom classes/records instead of primitives for domain concepts
- **Magic Strings**: Use enums or constants instead of hardcoded strings
- **Ignoring Null Safety**: Don't use `!` carelessly, handle nullability properly
- **Exception Swallowing**: Never catch and ignore exceptions without proper handling
- **Mutable State Everywhere**: Prefer immutable objects with final fields

### Common Mistakes
- **Improper `==` operator**: Always override `==` and `hashCode` consistently (or use `Equatable`)
- **Memory Leaks**: Don't forget to close Streams, dispose controllers, and cancel subscriptions
- **Synchronization Issues**: Understand async/await, avoid mixing sync/async code incorrectly
- **Resource Leaks**: Always close files, sockets, database connections
- **Performance Issues**: Avoid premature optimization, profile with DevTools before optimizing
- **Late Variable Misuse**: Don't use `late` when `final` with initialization is possible

### Dart-Specific Anti-Patterns
```dart
// ❌ Bad: Using ! carelessly
final user = getUserFromDatabase()!; // Can throw if null

// ✅ Good: Handle null properly
final user = getUserFromDatabase();
if (user == null) {
  throw UserNotFoundException();
}

// ❌ Bad: Not closing streams
final controller = StreamController<int>();
controller.add(1); // Never closed - memory leak

// ✅ Good: Properly close streams
final controller = StreamController<int>();
try {
  controller.add(1);
} finally {
  await controller.close();
}

// ❌ Bad: Ignoring async
Future<void> saveData() {
  database.save(data); // Fire and forget - error prone
}

// ✅ Good: Properly await async operations
Future<void> saveData() async {
  await database.save(data);
}

// ❌ Bad: Mutable classes
class User {
  String name;
  User(this.name);
}

// ✅ Good: Immutable classes
class User {
  final String name;
  const User(this.name);
  
  User copyWith({String? name}) => User(name ?? this.name);
}
```

## 🎯 Dart Best Practices

### Modern Dart Features
```dart
// ✅ Use records for multiple return values
(String, int) getUserInfo() {
  return ('John Doe', 30);
}

final (name, age) = getUserInfo();

// ✅ Use pattern matching
String describeUser(User user) => switch (user) {
  User(age: < 18) => 'Minor',
  User(age: >= 18 && < 65) => 'Adult',
  User(age: >= 65) => 'Senior',
  _ => 'Unknown',
};

// ✅ Use sealed classes for exhaustive matching
sealed class Result<T> {}
class Success<T> extends Result<T> {
  final T data;
  Success(this.data);
}
class Failure<T> extends Result<T> {
  final String error;
  Failure(this.error);
}

String handleResult(Result<String> result) => switch (result) {
  Success(data: var value) => 'Success: $value',
  Failure(error: var error) => 'Error: $error',
};

// ✅ Use extension methods
extension StringExtensions on String {
  bool get isValidEmail => RegExp(r'^[\w-\.]+@([\w-]+\.)+[\w-]{2,4}$').hasMatch(this);
}

// ✅ Use collection if/for
final numbers = [
  1,
  2,
  if (includeThree) 3,
  for (var i = 4; i < 7; i++) i,
];
```

### Development Workflow
- **Code Quality Gates**: Use `dart analyze` and linting rules (flutter_lints, very_good_analysis)
- **Documentation**: DartDoc for all public APIs with meaningful documentation
- **Dependency Management**: Keep dependencies up-to-date in `pubspec.yaml`, use `dependency_overrides` sparingly
- **Build Automation**: Use `pub get`, `dart run build_runner build` for code generation
- **Code Review**: Focus on design, business logic, null safety, and maintainability
- **Static Analysis**: Run `dart analyze` as part of CI/CD pipeline

### Null Safety Best Practices
```dart
// ✅ Use required for non-nullable parameters
class User {
  final String name;
  final String email;
  
  User({required this.name, required this.email});
}

// ✅ Use null-aware operators
String? name;
final displayName = name ?? 'Guest'; // Default value
final length = name?.length ?? 0; // Null-aware access

// ✅ Use late for lazy initialization
class ExpensiveService {
  late final String config = _loadConfig(); // Initialized on first access
  
  String _loadConfig() {
    // Heavy computation
    return 'config';
  }
}

// ✅ Use nullable types explicitly
User? findUser(String id) {
  // Returns null if not found
  return null;
}

// ❌ Avoid: Don't use ! unless absolutely certain
final user = findUser('123')!; // Dangerous!

// ✅ Better: Handle null case explicitly
final user = findUser('123');
if (user == null) {
  throw UserNotFoundException();
}
```

### Immutability & Value Objects
```dart
// ✅ Use @immutable annotation (Flutter)
@immutable
class User {
  final String id;
  final String name;
  final String email;
  
  const User({
    required this.id,
    required this.name,
    required this.email,
  });
  
  // CopyWith for immutable updates
  User copyWith({String? id, String? name, String? email}) {
    return User(
      id: id ?? this.id,
      name: name ?? this.name,
      email: email ?? this.email,
    );
  }
  
  @override
  bool operator ==(Object other) =>
      identical(this, other) ||
      other is User &&
          runtimeType == other.runtimeType &&
          id == other.id &&
          name == other.name &&
          email == other.email;
  
  @override
  int get hashCode => Object.hash(id, name, email);
}

// ✅ Or use packages for boilerplate reduction
// With equatable package:
class User extends Equatable {
  final String id;
  final String name;
  
  const User({required this.id, required this.name});
  
  @override
  List<Object?> get props => [id, name];
}

// With freezed package (recommended):
@freezed
class User with _$User {
  const factory User({
    required String id,
    required String name,
    required String email,
  }) = _User;
  
  factory User.fromJson(Map<String, dynamic> json) => _$UserFromJson(json);
}
```

### Async/Await Patterns
```dart
// ✅ Proper error handling with async/await
Future<User> fetchUser(String id) async {
  try {
    final response = await apiClient.get('/users/$id');
    return User.fromJson(response.data);
  } on NetworkException catch (e) {
    throw UserFetchException('Network error: ${e.message}');
  } catch (e, stackTrace) {
    logError('Failed to fetch user', error: e, stackTrace: stackTrace);
    rethrow;
  }
}

// ✅ Parallel async operations
Future<Dashboard> loadDashboard() async {
  final results = await Future.wait([
    fetchUser(),
    fetchPosts(),
    fetchNotifications(),
  ]);
  
  return Dashboard(
    user: results[0] as User,
    posts: results[1] as List<Post>,
    notifications: results[2] as List<Notification>,
  );
}

// ✅ Timeout for async operations
Future<User> fetchUserWithTimeout(String id) async {
  return await fetchUser(id).timeout(
    const Duration(seconds: 10),
    onTimeout: () => throw TimeoutException('Request timed out'),
  );
}

// ✅ Stream subscription with proper cleanup
class UserRepository {
  StreamSubscription<User>? _subscription;
  
  void listenToUserUpdates(String userId) {
    _subscription?.cancel(); // Cancel previous subscription
    _subscription = userStream(userId).listen(
      (user) => handleUserUpdate(user),
      onError: (error) => handleError(error),
    );
  }
  
  void dispose() {
    _subscription?.cancel();
  }
}
```

### Production Considerations
- **Logging**: Use `logger` package with appropriate log levels (debug, info, warning, error)
- **Error Tracking**: Integrate crash reporting (Firebase Crashlytics, Sentry)
- **Configuration**: Use environment variables and build configurations
- **Security**: Input validation, secure storage for sensitive data, HTTPS only
- **Performance**: Profile with Dart DevTools, optimize hot paths, lazy loading

## 📚 Reference Links

### Official Documentation
- [Dart Language Tour](https://dart.dev/guides/language/language-tour)
- [Effective Dart Style Guide](https://dart.dev/guides/language/effective-dart/style)
- [Dart API Reference](https://api.dart.dev/stable/)
- [Dart Null Safety](https://dart.dev/null-safety)

### Essential Tools & Packages
- [pub.dev](https://pub.dev/) - Dart package repository
- [Dart Test Package](https://pub.dev/packages/test)
- [Mockito](https://pub.dev/packages/mockito) or [Mocktail](https://pub.dev/packages/mocktail)
- [Equatable](https://pub.dev/packages/equatable) - Value equality
- [Freezed](https://pub.dev/packages/freezed) - Code generation for immutable classes
- [Logger](https://pub.dev/packages/logger) - Logging utility

## 📝 Code Organization and Architecture

### Package Structure
- Organize code by feature/domain rather than by layer for better maintainability
- Use standard Dart package naming conventions (lowercase_with_underscores)
- Separate concerns: keep business logic, data access, and presentation layers distinct
- Create utility classes with static methods or extension methods

### Dependency Management
```dart
// ✅ Use constructor injection for dependencies
class UserService {
  final UserRepository _repository;
  final Logger _logger;
  
  const UserService(this._repository, this._logger);
  
  Future<User> getUser(String id) async {
    _logger.info('Fetching user: $id');
    return await _repository.findById(id);
  }
}

// ✅ Use abstract interfaces for testability
abstract class UserRepository {
  Future<User?> findById(String id);
  Future<void> save(User user);
}

class UserRepositoryImpl implements UserRepository {
  final ApiClient _apiClient;
  
  const UserRepositoryImpl(this._apiClient);
  
  @override
  Future<User?> findById(String id) async {
    // Implementation
  }
  
  @override
  Future<void> save(User user) async {
    // Implementation
  }
}
```

### Design Patterns
- Follow separation of concerns principles
- Use DTOs/Models for data transfer between layers
- Avoid God classes or putting too much logic in single classes
- Organize code by feature/module rather than technical layers
- Implement proper abstraction and encapsulation with private fields

## 🔍 Data Handling and Validation

### Input Validation
```dart
// ✅ Create validation utilities
class Validators {
  static String? email(String? value) {
    if (value == null || value.isEmpty) {
      return 'Email is required';
    }
    final emailRegex = RegExp(r'^[\w-\.]+@([\w-]+\.)+[\w-]{2,4}$');
    if (!emailRegex.hasMatch(value)) {
      return 'Invalid email format';
    }
    return null;
  }
  
  static String? password(String? value) {
    if (value == null || value.isEmpty) {
      return 'Password is required';
    }
    if (value.length < 8) {
      return 'Password must be at least 8 characters';
    }
    return null;
  }
}

// ✅ Use validation in models
class LoginCredentials {
  final String email;
  final String password;
  
  LoginCredentials({required this.email, required this.password}) {
    _validate();
  }
  
  void _validate() {
    final emailError = Validators.email(email);
    if (emailError != null) {
      throw ValidationException(emailError);
    }
    
    final passwordError = Validators.password(password);
    if (passwordError != null) {
      throw ValidationException(passwordError);
    }
  }
}
```

### Data Serialization
```dart
// ✅ Manual JSON serialization
class User {
  final String id;
  final String name;
  final String email;
  
  const User({
    required this.id,
    required this.name,
    required this.email,
  });
  
  factory User.fromJson(Map<String, dynamic> json) {
    return User(
      id: json['id'] as String,
      name: json['name'] as String,
      email: json['email'] as String,
    );
  }
  
  Map<String, dynamic> toJson() {
    return {
      'id': id,
      'name': name,
      'email': email,
    };
  }
}

// ✅ Better: Use json_serializable for code generation
@JsonSerializable()
class User {
  final String id;
  final String name;
  final String email;
  
  const User({
    required this.id,
    required this.name,
    required this.email,
  });
  
  factory User.fromJson(Map<String, dynamic> json) => _$UserFromJson(json);
  Map<String, dynamic> toJson() => _$UserToJson(this);
}
```

## 📊 Logging and Error Tracking

### Logging Standards
```dart
// ✅ Use logger package consistently
class UserService {
  final Logger _logger = Logger();
  
  Future<User> getUser(String id) async {
    _logger.d('Fetching user with id: $id'); // Debug
    try {
      final user = await _repository.findById(id);
      _logger.i('Successfully fetched user: $id'); // Info
      return user;
    } catch (e, stackTrace) {
      _logger.e('Failed to fetch user', error: e, stackTrace: stackTrace); // Error
      rethrow;
    }
  }
}

// ✅ Configure logger for production
final logger = Logger(
  printer: PrettyPrinter(
    methodCount: 2,
    errorMethodCount: 8,
    lineLength: 120,
    colors: true,
    printEmojis: true,
    printTime: true,
  ),
  level: kReleaseMode ? Level.warning : Level.debug,
);

// ❌ Never use print() in production
print('Debug message'); // Bad!

// ✅ Use proper logging
_logger.d('Debug message'); // Good!
```

### Exception Hierarchy
```dart
// ✅ Create meaningful exception hierarchy
abstract class AppException implements Exception {
  final String message;
  final StackTrace? stackTrace;
  
  const AppException(this.message, [this.stackTrace]);
  
  @override
  String toString() => 'AppException: $message';
}

class NetworkException extends AppException {
  const NetworkException(super.message, [super.stackTrace]);
}

class ValidationException extends AppException {
  final Map<String, String> errors;
  
  const ValidationException(super.message, this.errors, [super.stackTrace]);
}

class NotFoundException extends AppException {
  const NotFoundException(super.message, [super.stackTrace]);
}

// ✅ Use specific exceptions
throw NotFoundException('User with id $id not found');
throw NetworkException('Connection timeout');
throw ValidationException('Invalid input', {'email': 'Invalid format'});
```

## 🔒 Security Considerations

### Secure Coding Practices
```dart
// ✅ Sanitize user inputs
String sanitizeInput(String input) {
  return input
      .replaceAll(RegExp(r'[<>]'), '')
      .trim();
}

// ✅ Use parameterized queries (if using SQL)
Future<User?> findUserById(String id) async {
  final db = await database;
  final results = await db.query(
    'users',
    where: 'id = ?', // Parameterized query
    whereArgs: [id],
  );
  return results.isNotEmpty ? User.fromMap(results.first) : null;
}

// ✅ Store sensitive data securely
class SecureStorage {
  final FlutterSecureStorage _storage = const FlutterSecureStorage();
  
  Future<void> saveToken(String token) async {
    await _storage.write(key: 'auth_token', value: token);
  }
  
  Future<String?> getToken() async {
    return await _storage.read(key: 'auth_token');
  }
}

// ❌ Never hardcode secrets
const apiKey = 'secret_key_123'; // Bad!

// ✅ Use environment variables
final apiKey = const String.fromEnvironment('API_KEY');
```

## ✅ Patterns to Follow

### Constructor Patterns
```dart
// ✅ Named constructors for different initialization paths
class User {
  final String id;
  final String name;
  final String email;
  
  const User({
    required this.id,
    required this.name,
    required this.email,
  });
  
  // Named constructor for guest user
  User.guest()
      : id = 'guest',
        name = 'Guest User',
        email = 'guest@example.com';
  
  // Factory constructor for JSON
  factory User.fromJson(Map<String, dynamic> json) {
    return User(
      id: json['id'] as String,
      name: json['name'] as String,
      email: json['email'] as String,
    );
  }
}
```

### Factory Pattern
```dart
// ✅ Use factory constructors for conditional object creation
abstract class Shape {
  factory Shape(String type) {
    switch (type) {
      case 'circle':
        return Circle();
      case 'square':
        return Square();
      default:
        throw ArgumentError('Unknown shape type: $type');
    }
  }
  
  double calculateArea();
}

class Circle implements Shape {
  @override
  double calculateArea() => 3.14 * 10 * 10;
}

class Square implements Shape {
  @override
  double calculateArea() => 10 * 10;
}
```

### Builder Pattern
```dart
// ✅ Use builder pattern for complex object construction
class HttpClientBuilder {
  Duration _timeout = const Duration(seconds: 30);
  Map<String, String> _headers = {};
  String? _baseUrl;
  
  HttpClientBuilder setTimeout(Duration timeout) {
    _timeout = timeout;
    return this;
  }
  
  HttpClientBuilder addHeader(String key, String value) {
    _headers[key] = value;
    return this;
  }
  
  HttpClientBuilder setBaseUrl(String baseUrl) {
    _baseUrl = baseUrl;
    return this;
  }
  
  HttpClient build() {
    if (_baseUrl == null) {
      throw StateError('Base URL is required');
    }
    return HttpClient(
      baseUrl: _baseUrl!,
      timeout: _timeout,
      headers: _headers,
    );
  }
}

// Usage
final client = HttpClientBuilder()
    .setBaseUrl('https://api.example.com')
    .setTimeout(const Duration(seconds: 60))
    .addHeader('Authorization', 'Bearer token')
    .build();
```

## 🚫 Patterns to Avoid

### Anti-Patterns
```dart
// ❌ Don't expose mutable state
class Counter {
  int value = 0; // Mutable state exposed
}

// ✅ Encapsulate state
class Counter {
  int _value = 0;
  int get value => _value;
  
  void increment() => _value++;
  void decrement() => _value--;
}

// ❌ Don't ignore errors
Future<void> saveData() async {
  try {
    await database.save(data);
  } catch (e) {
    // Ignored - bad!
  }
}

// ✅ Handle or rethrow errors
Future<void> saveData() async {
  try {
    await database.save(data);
  } catch (e, stackTrace) {
    _logger.e('Failed to save data', error: e, stackTrace: stackTrace);
    rethrow;
  }
}

// ❌ Don't use dynamic unnecessarily
dynamic processData(dynamic input) { // Bad!
  return input.toString();
}

// ✅ Use proper types
String processData(Object input) {
  return input.toString();
}
```

## 🧪 Testing Best Practices

### Test Structure
```dart
// ✅ Organize tests with groups
void main() {
  group('UserRepository', () {
    late MockApiClient mockApiClient;
    late UserRepository repository;
    
    setUp(() {
      mockApiClient = MockApiClient();
      repository = UserRepositoryImpl(mockApiClient);
    });
    
    group('findById', () {
      test('should return user when API call succeeds', () async {
        // Arrange
        final userId = '123';
        final userData = {'id': userId, 'name': 'John', 'email': 'john@example.com'};
        when(() => mockApiClient.get('/users/$userId'))
            .thenAnswer((_) async => Response(data: userData, statusCode: 200));
        
        // Act
        final result = await repository.findById(userId);
        
        // Assert
        expect(result, isNotNull);
        expect(result?.id, userId);
        expect(result?.name, 'John');
        verify(() => mockApiClient.get('/users/$userId')).called(1);
      });
      
      test('should throw NotFoundException when user not found', () async {
        // Arrange
        final userId = '123';
        when(() => mockApiClient.get('/users/$userId'))
            .thenThrow(NotFoundException('User not found'));
        
        // Act & Assert
        expect(
          () => repository.findById(userId),
          throwsA(isA<NotFoundException>()),
        );
      });
    });
    
    tearDown(() {
      // Cleanup if needed
    });
  });
}
```

## 🚀 Build and Quality Assurance

### Build Process
```bash
# Get dependencies
dart pub get

# Run analyzer
dart analyze

# Format code
dart format .

# Run tests
dart test

# Run tests with coverage
dart test --coverage=coverage
dart pub global run coverage:format_coverage --lcov --in=coverage --out=coverage/lcov.info --report-on=lib

# Build runner for code generation
dart run build_runner build --delete-conflicting-outputs

# Check for outdated packages
dart pub outdated
```

### Quality Gates
- Run `dart analyze` with zero errors/warnings
- Maintain test coverage above 80% for business logic
- Format code with `dart format` before committing
- Use linting rules (flutter_lints, very_good_analysis)
- Review code for null safety violations

## 🔗 Framework Integration
- For Flutter specific patterns, see tech-flutter.instructions.md
- For backend applications, consider using shelf or serverpod
- Framework-specific patterns should be documented in their respective files
- This file covers language-level Dart patterns that apply across all frameworks

## 📖 References

- [Dart Language Specification](https://dart.dev/guides/language/spec)
- [Effective Dart](https://dart.dev/guides/language/effective-dart)
- [Dart Style Guide](https://dart.dev/guides/language/effective-dart/style)
- [Dart Test Package](https://pub.dev/packages/test)
- [Mockito Documentation](https://pub.dev/packages/mockito)
- [Dart Null Safety](https://dart.dev/null-safety)
- [Dart Language Tour](https://dart.dev/guides/language/language-tour)
- [Dart Patterns and Records](https://dart.dev/language/patterns)

---

*Last Updated: 2025*
*Based on Dart 3.x with sound null safety*
*Adapted from Java best practices for the Dart ecosystem*
