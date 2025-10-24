---
description: Flutter development standards and framework-specific best practices
applyTo: "**/*.dart"
---

# Flutter Development Standards

## 🏗️ Architecture & Navigation
- **Root Standards**: [General Coding Standards](./tech-general-coding.instructions.md)
- **Language Standards**: [Dart Development](./tech-dart.instructions.md)
- **Security Guidelines**: [Security & OWASP](./security-owasp.instructions.md)
- **Performance Guidelines**: [Performance Optimization](./tech-performance-optimization.instructions.md)

---

## 📱 Flutter-Specific Context

- **Flutter Version**: 3.x+ with Dart 3.x+ for optimal performance and null safety
- **Target Platforms**: iOS, Android, Web, Desktop (Windows, macOS, Linux)
- **State Management**: Provider, Riverpod, Bloc, GetX, or MobX
- **Architecture Patterns**: Clean Architecture, MVVM, BLoC Pattern, Feature-First
- **Material Design**: Material 3 (Material You) for modern UI components

## 🔧 Flutter Framework Standards

### Project Setup & Configuration
- **Package Management**: Use `pubspec.yaml` for dependency management
- **Flutter SDK**: Pin Flutter SDK version in project for consistency
- **Platform Configuration**: Configure platform-specific settings in respective directories
- **Environment Variables**: Use `.env` files with `flutter_dotenv` for configuration
- **Asset Management**: Organize assets properly and declare them in `pubspec.yaml`
- **Localization**: Implement i18n using `flutter_localizations` and `intl` package

### State Management & Architecture
- **State Management Choice**: Select appropriate state management solution based on app complexity
  - **Provider/Riverpod**: Recommended for most applications (dependency injection + state, similar to React Context)
  - **BLoC**: For complex state logic with business layer separation (similar to Redux pattern)
  - **GetX**: For rapid development with less boilerplate
  - **setState**: Only for local, simple widget state (similar to React useState)
- **State Colocation**: Keep state as close to where it's used as possible (avoid prop drilling)
- **State Normalization**: Structure state data efficiently to avoid redundancy
- **Dependency Injection**: Use `get_it`, `injectable`, or state management DI capabilities
- **Architecture Layers**: Separate presentation, domain, and data layers (Clean Architecture)
- **Immutability**: Prefer immutable data models with `@immutable` annotation
- **Repository Pattern**: Abstract data sources behind repository interfaces
- **Custom Hooks Equivalent**: Create reusable widget logic through custom widgets or mixins

### Widget Architecture & Composition
- **Widget Composition**: Build complex UIs from simple, reusable widgets (similar to React component composition)
- **Single Responsibility**: Each widget should have a single, well-defined purpose
- **Stateless vs Stateful**: Use `StatelessWidget` by default, `StatefulWidget` only when needed
- **Widget Separation**: Extract widgets into separate files/classes for reusability and testability
- **Const Constructors**: Use `const` constructors whenever possible for performance (equivalent to React.memo)
- **BuildContext Usage**: Pass `BuildContext` appropriately, avoid storing it in fields or state
- **Keys**: Use `Key`, `ValueKey`, `ObjectKey`, `GlobalKey` appropriately for widget identity
- **Widget Hierarchy**: Organize widgets in logical hierarchies with clear data flow (props down, events up)
- **Composition Over Inheritance**: Prefer widget composition over inheritance for flexibility

### Navigation & Routing
- **Navigation Strategy**: Choose between Navigator 1.0 or Navigator 2.0 (Router API)
- **Named Routes**: Define named routes for better maintainability
- **Route Management**: Use packages like `go_router`, `auto_route`, or `beamer` for complex routing
- **Deep Linking**: Implement deep linking for web and mobile platforms
- **Route Guards**: Implement authentication guards and navigation logic
- **Screen Transitions**: Use custom transitions appropriately, avoid over-animation

### Data Layer & Networking
- **HTTP Client**: Use `dio` or `http` package for network requests
- **API Integration**: Create service classes for API communication with clear interfaces
- **Error Handling**: Implement proper error handling with custom exceptions and failure classes
- **Serialization**: Use `json_serializable` or `freezed` for model serialization
- **Data Fetching Patterns**: Implement loading, error, and success states (similar to React Query)
- **Request Cancellation**: Handle race conditions and request cancellation properly
- **Optimistic Updates**: Implement optimistic UI updates for better user experience
- **Local Storage**: Use appropriate storage solutions:
  - `shared_preferences` for simple key-value storage
  - `hive` or `isar` for local database (NoSQL)
  - `sqflite` for SQLite (SQL)
  - `flutter_secure_storage` for sensitive data
- **Caching Strategies**: Implement intelligent caching for offline support and performance
- **Offline Support**: Handle offline scenarios and network errors gracefully
- **Data Normalization**: Structure cached data efficiently to avoid duplication

### Styling & Theming
- **Theme Management**: Use `ThemeData` for consistent app-wide theming
- **Design System**: Implement a design system with consistent spacing, typography, and colors
- **Custom Themes**: Create custom themes for light/dark mode support
- **Theme Extensions**: Use theme extensions for custom theme properties
- **Color Schemes**: Define color schemes following Material Design 3 guidelines
- **Typography System**: Establish consistent text styles with `TextTheme`
- **Spacing System**: Use consistent spacing values (8dp grid system)
- **Responsive Theming**: Adapt themes based on screen size and platform
- **CSS-like Variables**: Use theme data as single source of truth (similar to CSS variables)
- **Style Reusability**: Create reusable style constants and theme extensions
- **Platform Adaptivity**: Use `Theme.of(context).platform` for platform-specific styling
- **Accessibility Colors**: Ensure proper color contrast ratios for accessibility

### Responsive & Adaptive Design
- **Screen Sizes**: Support multiple screen sizes and orientations
- **Responsive Layouts**: Use `LayoutBuilder`, `MediaQuery`, `OrientationBuilder`
- **Adaptive Widgets**: Use platform-adaptive widgets when appropriate
- **Breakpoints**: Define consistent breakpoints for responsive design
- **Safe Areas**: Handle safe areas, notches, and system UI overlays
- **Accessibility**: Implement proper semantic labels and accessibility features

### Forms & Input Validation
- **Controlled Inputs**: Use `TextEditingController` for controlled form inputs (similar to React controlled components)
- **Form Validation**: Implement proper form validation with `Form` widget and validators
- **Validation Libraries**: Use packages like `form_builder_validators` or `formz` for complex validation
- **Form State**: Use `GlobalKey<FormState>` for form state management
- **Debounced Validation**: Implement debounced validation for better user experience (use `debounce` package)
- **Error States**: Display clear, user-friendly error messages
- **Submit Handling**: Handle form submission with proper loading and error states
- **Accessibility**: Ensure forms have proper labels, hints, and error announcements
- **Auto-validation**: Use `autovalidateMode` appropriately (onUserInteraction, always, disabled)
- **File Uploads**: Handle file uploads and complex form scenarios with proper packages

## 📁 Flutter Project Structure

```
lib/
├── main.dart                                 # Application entry point
├── app.dart                                  # Root application widget
├── core/                                     # Core functionality
│   ├── constants/
│   │   ├── app_constants.dart
│   │   ├── api_constants.dart
│   │   └── asset_constants.dart
│   ├── config/
│   │   ├── app_config.dart
│   │   ├── environment.dart
│   │   └── router_config.dart
│   ├── themes/
│   │   ├── app_theme.dart
│   │   ├── app_colors.dart
│   │   └── app_text_styles.dart
│   ├── utils/
│   │   ├── logger.dart
│   │   ├── validators.dart
│   │   └── extensions.dart
│   ├── errors/
│   │   ├── exceptions.dart
│   │   └── failures.dart
│   └── network/
│       ├── api_client.dart
│       ├── interceptors.dart
│       └── network_info.dart
├── features/                                 # Feature modules
│   ├── authentication/
│   │   ├── data/
│   │   │   ├── models/
│   │   │   │   ├── user_model.dart
│   │   │   │   └── auth_response_model.dart
│   │   │   ├── datasources/
│   │   │   │   ├── auth_remote_datasource.dart
│   │   │   │   └── auth_local_datasource.dart
│   │   │   └── repositories/
│   │   │       └── auth_repository_impl.dart
│   │   ├── domain/
│   │   │   ├── entities/
│   │   │   │   └── user.dart
│   │   │   ├── repositories/
│   │   │   │   └── auth_repository.dart
│   │   │   └── usecases/
│   │   │       ├── login_usecase.dart
│   │   │       ├── logout_usecase.dart
│   │   │       └── register_usecase.dart
│   │   └── presentation/
│   │       ├── providers/                    # State management
│   │       │   └── auth_provider.dart
│   │       ├── screens/
│   │       │   ├── login_screen.dart
│   │       │   └── register_screen.dart
│   │       └── widgets/
│   │           ├── login_form.dart
│   │           └── auth_button.dart
│   ├── home/
│   │   ├── data/
│   │   ├── domain/
│   │   └── presentation/
│   └── profile/
│       ├── data/
│       ├── domain/
│       └── presentation/
├── shared/                                   # Shared across features
│   ├── widgets/
│   │   ├── buttons/
│   │   │   ├── primary_button.dart
│   │   │   └── secondary_button.dart
│   │   ├── inputs/
│   │   │   └── custom_text_field.dart
│   │   ├── loading/
│   │   │   └── loading_indicator.dart
│   │   └── dialogs/
│   │       └── custom_dialog.dart
│   ├── models/
│   │   └── api_response.dart
│   └── services/
│       ├── analytics_service.dart
│       ├── storage_service.dart
│       └── notification_service.dart
└── l10n/                                     # Localization files
    ├── app_en.arb
    ├── app_fr.arb
    └── l10n.dart

assets/
├── images/
│   ├── logo.png
│   └── icons/
├── fonts/
│   └── custom_font.ttf
└── animations/
    └── loading.json

test/
├── unit/
│   ├── features/
│   │   └── authentication/
│   │       ├── domain/
│   │       │   └── usecases/
│   │       │       └── login_usecase_test.dart
│   │       └── data/
│   │           └── repositories/
│   │               └── auth_repository_impl_test.dart
│   └── core/
│       └── utils/
│           └── validators_test.dart
├── widget/
│   └── features/
│       └── authentication/
│           └── presentation/
│               └── screens/
│                   └── login_screen_test.dart
├── integration/
│   └── authentication_flow_test.dart
└── fixtures/
    └── test_data.json

android/                                      # Android platform specific
ios/                                          # iOS platform specific
web/                                          # Web platform specific
linux/                                        # Linux platform specific
macos/                                        # macOS platform specific
windows/                                      # Windows platform specific
```

## 🧪 Flutter Testing Standards

### Testing Framework & Types
- **Unit Tests**: Test business logic, use cases, and utilities
- **Widget Tests**: Test individual widgets and their behavior
- **Integration Tests**: Test complete user flows and feature interactions
- **Golden Tests**: Visual regression testing for UI consistency
- **Test Coverage**: Aim for 80%+ code coverage on critical paths

### Testing Tools & Packages
- **flutter_test**: Built-in testing framework
- **mockito**: For mocking dependencies
- **mocktail**: Alternative modern mocking library
- **bloc_test**: For testing BLoC state management
- **integration_test**: For end-to-end testing
- **golden_toolkit**: For golden/snapshot testing

### Testing Best Practices
- **User-Centric Testing**: Test widgets from the user's perspective, not implementation details
- **Behavior Testing**: Focus on behavior rather than implementation (similar to React Testing Library)
- **Widget Finding**: Use semantic finders (find.text, find.byIcon, find.byType) appropriately
- **Test Structure**: Follow Arrange-Act-Assert (AAA) pattern
- **Widget Testing**: Use `WidgetTester` and `pumpWidget` for widget tests
- **Async Testing**: Properly handle async operations with `pump()`, `pumpAndSettle()`, and `runAsync()`
- **Test Isolation**: Each test should be independent and not rely on others
- **Mock Strategy**: Mock external dependencies (API calls, services), use fakes for simple objects
- **Test Data**: Use fixtures and test data builders for consistent test data
- **Accessibility Testing**: Include semantic tests for accessibility compliance and screen readers
- **Integration Testing**: Test complete user flows and feature interactions
- **Component Isolation**: Test widgets in isolation with proper props/parameters

### Testing Patterns & Examples
```dart
// Good: Testing behavior from user perspective
testWidgets('should display error message on invalid login', (tester) async {
  // Arrange
  final mockAuthService = MockAuthService();
  when(() => mockAuthService.login(any(), any()))
      .thenThrow(InvalidCredentialsException());
  
  await tester.pumpWidget(
    MaterialApp(
      home: LoginScreen(authService: mockAuthService),
    ),
  );
  
  // Act
  await tester.enterText(find.byType(TextField).first, 'test@example.com');
  await tester.enterText(find.byType(TextField).last, 'wrongpassword');
  await tester.tap(find.widgetWithText(ElevatedButton, 'Login'));
  await tester.pumpAndSettle();
  
  // Assert
  expect(find.text('Invalid credentials'), findsOneWidget);
});

// Good: Testing widget composition
testWidgets('should render all required form fields', (tester) async {
  await tester.pumpWidget(
    MaterialApp(home: RegistrationForm()),
  );
  
  expect(find.byType(TextField), findsNWidgets(4)); // email, password, confirm, name
  expect(find.widgetWithText(ElevatedButton, 'Register'), findsOneWidget);
});
```

## 🚫 Flutter Anti-Patterns

### Performance Issues
- **Unnecessary Rebuilds**: Not using `const` constructors or proper state management (similar to React unnecessary re-renders)
- **Heavy Build Methods**: Performing expensive operations in `build()` method
- **Large Widget Trees**: Creating deeply nested widget trees without extraction
- **Memory Leaks**: Not disposing controllers, streams, animations, or subscriptions
- **Blocking UI**: Performing long operations on main thread without async
- **Inline Object Creation**: Creating objects/functions in build that cause unnecessary rebuilds
- **Key Misuse**: Using inappropriate keys or no keys for dynamic lists (similar to React key anti-pattern)

### Architecture Problems
- **Business Logic in UI**: Putting business logic directly in widgets (like React business logic in components)
- **God Widgets**: Creating massive widgets that do too many things (similar to React large components)
- **Direct API Calls**: Making HTTP requests directly from widgets without abstraction
- **State Management Misuse**: Using inappropriate state management for app complexity
- **Tight Coupling**: Creating tightly coupled components that can't be tested
- **Prop Drilling**: Passing data through multiple widget levels unnecessarily
- **Context Misuse**: Overusing inherited widgets for frequently changing values

### Code Quality Issues
- **Ignoring Linting**: Disabling lint rules without good reason
- **No Error Handling**: Not handling errors in async operations
- **String Hardcoding**: Hardcoding strings instead of using localization
- **Magic Numbers**: Using magic numbers instead of named constants
- **Poor Naming**: Using unclear or inconsistent naming conventions

## 🎯 Flutter Best Practices

### Performance Optimization
- **Const Widgets**: Use `const` constructors wherever possible (equivalent to React.memo)
- **Widget Memoization**: Extract expensive widgets and mark them as const to prevent rebuilds
- **ListView Builder**: Use `ListView.builder()` for long lists instead of `ListView()` (similar to React virtualization)
- **Image Optimization**: Optimize image assets, use appropriate formats, sizes, and caching
- **Lazy Loading**: Implement pagination and lazy loading for large datasets
- **Stream Management**: Properly close streams and dispose of controllers to prevent memory leaks
- **RepaintBoundary**: Use `RepaintBoundary` to isolate expensive widgets (similar to React.memo)
- **Compute Function**: Use `compute()` for CPU-intensive operations (similar to Web Workers)
- **Code Splitting**: Implement lazy loading with deferred imports for large dependencies
- **Bundle Optimization**: Analyze and optimize app bundle size with tree shaking
- **Callback Optimization**: Create callbacks outside build method or use factory methods
- **Avoid Inline Functions**: Don't create functions/objects in build method that cause unnecessary rebuilds
- **Performance Profiling**: Use Flutter DevTools to identify performance bottlenecks
- **Animation Performance**: Optimize animations with proper use of `AnimationController` disposal

### Code Quality & Maintainability
- **Linting**: Enable and follow `flutter_lints` or `very_good_analysis`
- **Code Formatting**: Use `dart format` consistently across the project
- **Documentation**: Document public APIs and complex logic
- **Type Safety**: Leverage Dart's type system, avoid `dynamic` when possible
- **Null Safety**: Utilize Dart's sound null safety features
- **Immutability**: Prefer immutable data structures with `@immutable` annotation

### UI/UX Best Practices
- **Platform Conventions**: Follow platform-specific design guidelines (Material/Cupertino)
- **Loading States**: Show appropriate loading indicators during async operations (skeleton screens, spinners)
- **Error States**: Display user-friendly error messages with recovery options
- **Empty States**: Design meaningful empty state screens with clear call-to-action
- **Success States**: Provide clear feedback for successful operations
- **Animations**: Use animations purposefully, not excessively (respect reduced motion preferences)
- **Haptic Feedback**: Implement appropriate haptic feedback for user interactions
- **Accessibility**: Support screen readers, high contrast modes, and semantic labels
- **Offline Support**: Gracefully handle offline scenarios with appropriate UI feedback

### Error Handling & Recovery
- **Error Boundaries**: Implement error catching widgets (similar to React Error Boundaries)
- **Custom Error Widgets**: Create reusable error display widgets with retry functionality
- **Async Error Handling**: Properly handle errors in Future/Stream operations
- **Error Logging**: Integrate error reporting (Firebase Crashlytics, Sentry)
- **Fallback UI**: Provide meaningful fallback UI for error scenarios
- **User Feedback**: Display contextual, actionable error messages to users
- **Error Recovery**: Implement retry mechanisms and error recovery flows
- **Network Errors**: Handle different network error types appropriately (timeout, no connection, server errors)
- **Validation Errors**: Show clear validation errors inline and on submit

### Security Best Practices
- **Secure Storage**: Use `flutter_secure_storage` for sensitive data (tokens, credentials)
- **API Keys**: Never commit API keys, use environment variables and build flavors
- **Input Validation**: Validate and sanitize all user inputs to prevent injection attacks
- **Certificate Pinning**: Implement certificate pinning for API calls in production
- **Deep Link Validation**: Validate deep links and external URLs before navigation
- **ProGuard/R8**: Enable code obfuscation for release builds (Android)
- **HTTPS Only**: Use HTTPS for all network requests
- **Authentication**: Implement secure authentication mechanisms (JWT, OAuth2, Biometrics)
- **Authorization**: Validate permissions and implement proper access control
- **Data Sanitization**: Escape and sanitize data before rendering to prevent XSS-like vulnerabilities
- **Session Management**: Implement proper session timeout and token refresh
- **Biometric Authentication**: Use `local_auth` package for fingerprint/face ID
- **Root/Jailbreak Detection**: Consider detecting compromised devices for sensitive apps

### DevOps & Deployment
- **CI/CD**: Implement automated testing and deployment pipelines
- **Environment Management**: Separate dev, staging, and production environments
- **Crash Reporting**: Integrate crash reporting (Firebase Crashlytics, Sentry)
- **Analytics**: Implement analytics tracking for user behavior
- **Feature Flags**: Use feature flags for gradual rollouts
- **App Versioning**: Follow semantic versioning for releases

## 🎨 Flutter Design Patterns

### Presentation Patterns
- **Provider Pattern**: Use for dependency injection and state sharing across widget tree
- **BLoC Pattern**: Separate business logic from UI with streams (Business Logic Component)
- **MVVM Pattern**: Model-View-ViewModel for clean architecture
- **Repository Pattern**: Abstract data sources behind repository interfaces
- **Factory Pattern**: Create widgets dynamically based on conditions

### Widget Composition Patterns
- **Builder Pattern**: Use builder widgets for dynamic content (similar to React render props)
- **Composition Pattern**: Build complex widgets from simple, reusable widgets
- **Wrapper Pattern**: Create wrapper widgets for common functionality (padding, decoration)
- **Compound Widgets**: Group related widgets together (similar to React compound components)
- **Higher-Order Widgets**: Create widgets that enhance other widgets with additional functionality

### State Management Patterns
- **Lifting State Up**: Move state to common ancestor when shared between widgets
- **State Colocation**: Keep state close to where it's used
- **Derived State**: Calculate values from state rather than storing duplicates
- **Controlled Widgets**: Parent controls widget state through callbacks (similar to React controlled components)
- **Uncontrolled Widgets**: Widget manages its own internal state

### Data Flow Patterns
- **Unidirectional Data Flow**: Data flows down, events flow up (similar to React)
- **Event-Driven Architecture**: Use streams and events for component communication
- **Observer Pattern**: Use ChangeNotifier/ValueNotifier for observable state
- **Command Pattern**: Encapsulate actions as objects for undo/redo functionality

## 🛠️ Development Workflow & Best Practices

### Code Quality & Documentation
- **Linting**: Enable and follow `flutter_lints` or `very_good_analysis`
- **Code Formatting**: Use `dart format` consistently across the project
- **Static Analysis**: Run `dart analyze` to catch potential issues
- **Documentation**: Document public APIs, complex logic, and custom widgets with DartDoc
- **Type Safety**: Leverage Dart's type system, avoid `dynamic` when possible
- **Null Safety**: Utilize Dart's sound null safety features consistently
- **Immutability**: Prefer immutable data structures with `@immutable` annotation
- **Naming Conventions**: Follow Dart naming conventions (PascalCase for classes, camelCase for variables)

### Development Tools & Productivity
- **Hot Reload**: Leverage Flutter's hot reload for rapid development iteration
- **Widget Inspector**: Use Flutter Inspector in DevTools for debugging widget trees
- **Performance Profiling**: Profile app performance with Flutter DevTools
- **Network Inspector**: Monitor network requests and responses
- **Code Generation**: Use build_runner for code generation (json_serializable, freezed)
- **IDE Integration**: Configure IDE (VS Code, Android Studio) with Flutter extensions
- **Git Workflow**: Use meaningful commit messages and maintain clean git history

### Production Monitoring & Analytics
- **Crash Reporting**: Integrate Firebase Crashlytics or Sentry for error tracking
- **Performance Monitoring**: Use Firebase Performance Monitoring
- **Analytics Integration**: Implement user analytics (Firebase Analytics, Mixpanel)
- **Feature Flags**: Use remote config for feature flags and A/B testing
- **App Updates**: Implement in-app update prompts and version checking
- **User Feedback**: Integrate feedback mechanisms and user surveys

## 📚 Reference Links

### Official Documentation
- [Flutter Documentation](https://docs.flutter.dev/)
- [Dart Language Tour](https://dart.dev/guides/language/language-tour)
- [Flutter Widget Catalog](https://docs.flutter.dev/ui/widgets)
- [Flutter Cookbook](https://docs.flutter.dev/cookbook)
- [Material Design 3](https://m3.material.io/)

### Essential Packages
- [pub.dev](https://pub.dev/) - Official Dart package repository
- [flutter_riverpod](https://pub.dev/packages/flutter_riverpod) - State management
- [go_router](https://pub.dev/packages/go_router) - Declarative routing
- [dio](https://pub.dev/packages/dio) - HTTP client
- [freezed](https://pub.dev/packages/freezed) - Code generation for immutable classes
- [json_serializable](https://pub.dev/packages/json_serializable) - JSON serialization
- [hive](https://pub.dev/packages/hive) - NoSQL database
- [flutter_bloc](https://pub.dev/packages/flutter_bloc) - BLoC pattern implementation

### Architecture & Best Practices
- [Flutter Architecture Samples](https://github.com/brianegan/flutter_architecture_samples)
- [Very Good Ventures Style Guide](https://github.com/VeryGoodOpenSource/very_good_analysis)
- [Effective Dart](https://dart.dev/guides/language/effective-dart)
- [Flutter Performance Best Practices](https://docs.flutter.dev/perf/best-practices)

### State Management Resources
- **Provider**: Simple and flexible state management
- **Riverpod**: Enhanced Provider with better testability
- **BLoC**: Business Logic Component pattern for complex apps
- **GetX**: All-in-one solution with routing and state management
- Choose based on team expertise and app complexity

### Testing Resources
- [Flutter Testing Documentation](https://docs.flutter.dev/testing)
- [Widget Testing](https://docs.flutter.dev/cookbook/testing/widget/introduction)
- [Integration Testing](https://docs.flutter.dev/testing/integration-tests)
- [Mockito Package](https://pub.dev/packages/mockito)
- [BLoC Testing](https://pub.dev/packages/bloc_test)

### Performance & Debugging
- [Flutter DevTools](https://docs.flutter.dev/tools/devtools/overview)
- [Performance Profiling](https://docs.flutter.dev/perf/ui-performance)
- [Memory Management](https://docs.flutter.dev/tools/devtools/memory)
- [Performance Best Practices](https://docs.flutter.dev/perf/best-practices)

### Platform-Specific Configuration
- **Android**: Configure `android/app/build.gradle` and `AndroidManifest.xml`
- **iOS**: Configure `ios/Runner/Info.plist` and Xcode project settings
- **Web**: Configure `web/index.html` and `web/manifest.json`
- **Desktop**: Configure platform-specific build files

### Build & Deployment
- **Build Commands**:
  - `flutter build apk` - Build Android APK (development)
  - `flutter build appbundle` - Build Android App Bundle (production, recommended)
  - `flutter build apk --split-per-abi` - Build APKs per ABI for smaller downloads
  - `flutter build ios` - Build iOS app (requires macOS and Xcode)
  - `flutter build web` - Build web app
  - `flutter build windows/macos/linux` - Build desktop apps
  - `flutter build apk --release --obfuscate --split-debug-info=/<output-dir>` - Production build with obfuscation
- **Build Optimization**: 
  - Enable code obfuscation and symbol stripping for release builds
  - Optimize image assets and bundle size
  - Use deferred loading for reducing initial bundle size
  - Analyze bundle size with `flutter build --analyze-size`
- **Code Signing**: 
  - Configure signing for iOS in Xcode with provisioning profiles
  - Set up keystore for Android in `android/key.properties`
- **Environment Configuration**:
  - Use build flavors for different environments (dev, staging, prod)
  - Configure flavor-specific configurations in platform files
  - Use `--dart-define` for environment-specific values
- **Release Preparation**: 
  - Update version in `pubspec.yaml` (version: 1.0.0+1)
  - Create changelogs and release notes
  - Test thoroughly on real devices
  - Run `flutter doctor -v` to verify setup
  - Check for deprecated API usage with `dart fix --dry-run`
- **Store Deployment**: 
  - Follow Google Play Store guidelines for Android
  - Follow App Store Connect guidelines for iOS
  - Prepare store listings, screenshots, and promotional materials
  - Set up staged rollouts for gradual releases
- **Continuous Deployment**:
  - Automate builds with CI/CD (GitHub Actions, Codemagic, Bitrise)
  - Implement automated testing in pipelines
  - Set up automatic deployment to internal testing tracks

---

## 🎓 Learning Resources

### Community & Support
- [Flutter Community](https://flutter.dev/community)
- [r/FlutterDev Reddit](https://www.reddit.com/r/FlutterDev/)
- [Flutter Discord](https://discord.gg/N7Yshp4)
- [Stack Overflow Flutter](https://stackoverflow.com/questions/tagged/flutter)

### Video Tutorials
- [Flutter Official YouTube Channel](https://www.youtube.com/c/flutterdev)
- [Flutter Widget of the Week](https://www.youtube.com/playlist?list=PLjxrf2q8roU23XGwz3Km7sQZFTdB996iG)
- [Boring Show - Flutter](https://www.youtube.com/playlist?list=PLOU2XLYxmsIK0r_D-zWcmJ1plIcDNnRkK)

### Blogs & Articles
- [Flutter Medium Publication](https://medium.com/flutter)
- [Very Good Ventures Blog](https://verygood.ventures/blog)
- [Flutter Community Medium](https://medium.com/flutter-community)

---

*Last Updated: 2025*
*Based on Flutter 3.x and Dart 3.x best practices*
*Enriched with React.js inspired patterns and best practices*

## 🚀 Flutter Implementation Process

### Project Setup Phase
1. **Initialize Project**: Create Flutter project with appropriate template
2. **Configure Dependencies**: Set up pubspec.yaml with required packages
3. **Project Structure**: Organize project following feature-first or layer-first architecture
4. **Environment Setup**: Configure development, staging, and production environments
5. **Build Flavors**: Set up build flavors for different environments

### Architecture & Design Phase
6. **Architecture Planning**: Define architecture pattern (Clean Architecture, MVVM, BLoC)
7. **State Management**: Choose and implement state management solution
8. **Navigation Structure**: Design navigation flow and route architecture
9. **Data Models**: Define data models with proper serialization
10. **API Integration**: Set up API client, endpoints, and data repositories

### Implementation Phase
11. **Core Features**: Implement core business logic and use cases
12. **UI Implementation**: Build screens and widgets following design system
13. **State Integration**: Connect UI with state management and business logic
14. **Form Handling**: Implement form validation and submission logic
15. **Error Handling**: Add comprehensive error handling and user feedback
16. **Loading States**: Implement loading indicators and skeleton screens

### Quality Assurance Phase
17. **Testing**: Write unit, widget, and integration tests
18. **Accessibility**: Ensure accessibility compliance with semantic labels
19. **Performance**: Optimize performance and reduce unnecessary rebuilds
20. **Code Review**: Conduct thorough code reviews
21. **Security**: Implement security best practices and code obfuscation

### Deployment Phase
22. **Documentation**: Add code documentation and technical guides
23. **CI/CD Setup**: Configure automated build and deployment pipelines
24. **Monitoring**: Integrate crash reporting and analytics
25. **Release Preparation**: Prepare store listings, screenshots, and release notes
26. **Deployment**: Deploy to app stores following platform guidelines

## 🔍 Flutter Code Review Checklist

### Architecture & Structure
- [ ] Follows chosen architecture pattern consistently
- [ ] Clear separation between presentation, domain, and data layers
- [ ] Appropriate use of state management solution
- [ ] Dependencies properly injected and testable

### Widget Implementation
- [ ] Widgets are appropriately sized and extracted
- [ ] Const constructors used where possible
- [ ] BuildContext not stored in widget state
- [ ] Keys used appropriately for widget identity
- [ ] No business logic in widget build methods

### Performance
- [ ] ListView.builder used for long lists
- [ ] Images optimized and cached appropriately
- [ ] Heavy computations moved off main thread
- [ ] Controllers and streams properly disposed
- [ ] No unnecessary rebuilds or rerenders

### Testing
- [ ] Unit tests for business logic and utilities
- [ ] Widget tests for UI components
- [ ] Integration tests for critical user flows
- [ ] Test coverage meets project standards
- [ ] Tests are independent and maintainable

### Accessibility (a11y)
- [ ] Semantic labels provided for all interactive widgets using `Semantics` widget
- [ ] Proper semantic order for screen readers with `semanticsLabel`
- [ ] All images have meaningful descriptions via `Semantics`
- [ ] Interactive elements have minimum touch target size (48x48dp)
- [ ] Color contrast ratios meet WCAG AA standards (4.5:1 for text)
- [ ] App works with TalkBack (Android) and VoiceOver (iOS)
- [ ] Keyboard navigation supported where applicable (web/desktop)
- [ ] Form fields have proper labels and hints via `labelText` and `hintText`
- [ ] Error messages are announced to screen readers
- [ ] Loading states are announced to screen readers
- [ ] Focus management handled properly for navigation
- [ ] Text scaling supported (respect system font size settings)
- [ ] Reduced motion respected (check MediaQuery.of(context).disableAnimations)

### Code Quality
- [ ] Follows Dart style guide and linting rules
- [ ] Proper error handling implemented
- [ ] No hardcoded strings (i18n used)
- [ ] Clear and consistent naming conventions
- [ ] Code properly documented

### Security
- [ ] No sensitive data in code or version control
- [ ] Secure storage used for credentials
- [ ] Input validation implemented
- [ ] HTTPS used for all network requests
- [ ] Proper authentication and authorization

## 📦 Recommended Flutter Packages

### State Management
- **riverpod / flutter_riverpod** - Modern, compile-safe state management
- **provider** - Simple and flexible dependency injection and state management
- **flutter_bloc / bloc** - Predictable state management with BLoC pattern
- **get** - Lightweight state management with routing
- **mobx / flutter_mobx** - Reactive state management

### Networking & Data
- **dio** - Powerful HTTP client with interceptors and request cancellation
- **http** - Simple HTTP client for basic needs
- **retrofit** - Type-safe HTTP client generator
- **json_serializable** - JSON serialization code generation
- **freezed** - Code generation for immutable classes and unions

### Storage & Database
- **shared_preferences** - Simple key-value storage
- **hive / hive_flutter** - Fast, NoSQL database
- **isar** - High-performance NoSQL database
- **sqflite** - SQLite plugin for Flutter
- **flutter_secure_storage** - Secure storage for sensitive data

### UI & Widgets
- **cached_network_image** - Image loading and caching
- **shimmer** - Shimmer effect for loading states
- **flutter_svg** - SVG rendering
- **lottie** - Lottie animations
- **flutter_animate** - Powerful animation library
- **auto_size_text** - Automatically resizing text
- **gap** - Better spacing widgets

### Forms & Validation
- **flutter_form_builder** - Form builder with built-in validators
- **reactive_forms** - Reactive forms with validation
- **formz** - Form state management with validation
- **validators** - Common validators

### Navigation & Routing
- **go_router** - Declarative routing (recommended)
- **auto_route** - Code generation for routing
- **beamer** - Router based on BeamerDelegate

### Development Tools
- **flutter_launcher_icons** - Generate app icons
- **flutter_native_splash** - Generate native splash screens
- **flutter_flavorizr** - Create flavors configuration
- **build_runner** - Code generation tool
- **very_good_analysis** - Strict lint rules

### Testing
- **mockito** - Mocking library for tests
- **mocktail** - Alternative modern mocking library
- **bloc_test** - Testing utilities for BLoC
- **golden_toolkit** - Golden/snapshot testing
- **patrol** - Native automation and testing

### Utilities
- **intl** - Internationalization and localization
- **easy_localization** - Easy i18n implementation
- **flutter_dotenv** - Environment variables
- **url_launcher** - Launch URLs, emails, phone calls
- **permission_handler** - Handle platform permissions
- **connectivity_plus** - Check network connectivity
- **device_info_plus** - Device information
- **package_info_plus** - Package information

### Analytics & Monitoring
- **firebase_analytics** - Google Analytics for Firebase
- **firebase_crashlytics** - Crash reporting
- **sentry_flutter** - Error tracking and monitoring
- **firebase_performance** - Performance monitoring

### Authentication
- **firebase_auth** - Firebase authentication
- **google_sign_in** - Google Sign-In
- **flutter_appauth** - OAuth 2.0 and OpenID Connect
- **local_auth** - Biometric authentication

---

## 📚 Reference Links

### Flutter
- [Flutter Documentation](https://docs.flutter.dev/) - Documentation officielle complète
- [Flutter API Reference](https://api.flutter.dev/) - Référence API complète
- [Flutter Cookbook](https://docs.flutter.dev/cookbook) - Recettes et solutions pratiques
- [Flutter Widget Catalog](https://docs.flutter.dev/ui/widgets) - Catalogue complet des widgets
- [Flutter Codelabs](https://docs.flutter.dev/codelabs) - Tutoriels interactifs étape par étape
- [Flutter Learning Resources](https://docs.flutter.dev/reference/learning-resources) - Ressources d'apprentissage officielles

### Dart
- [Dart Language Tour](https://dart.dev/guides/language/language-tour) - Guide complet du langage
- [Effective Dart](https://dart.dev/guides/language/effective-dart) - Bonnes pratiques Dart
- [Dart API Reference](https://api.dart.dev/stable/) - Documentation API Dart
- [Dart Null Safety](https://dart.dev/null-safety) - Guide de null safety

### Material Design
- [Material Design 3](https://m3.material.io/) - Spécifications Material Design (Material You)
- [Material Design Guidelines](https://material.io/design) - Principes et guidelines de design
- [Material Components](https://material.io/components) - Catalogue des composants Material
- [Material Design Color System](https://material.io/design/color) - Système de couleurs Material
- [Material Design Typography](https://material.io/design/typography) - Typographie Material
- [Material Motion](https://material.io/design/motion) - Animations et transitions Material
