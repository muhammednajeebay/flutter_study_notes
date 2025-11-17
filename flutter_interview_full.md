# Flutter Interview Preparation -- Complete Q&A Guide

## 1. Flutter Fundamentals

### Q1: What is Flutter?

Flutter is a UI toolkit by Google for building fast, cross-platform apps
(Android, iOS, Web, Desktop) using the Dart language. It renders UI
using its own engine, independent of OEM widgets.

### Q2: StatelessWidget vs StatefulWidget

  StatelessWidget     StatefulWidget
  ------------------- ------------------------------------------
  UI doesn't change   UI changes over time
  No internal state   Has internal state stored in State class
  Lightweight         Heavier due to lifecycle

### Q3: Why is Flutter fast?

Because Flutter draws UI using Skia engine --- no bridge, no Java/Kotlin
overhead. Everything is compiled to native ARM code.

------------------------------------------------------------------------

## 2. Dart, OOP & SOLID

### Q1: OOP Concepts

-   Encapsulation\
-   Inheritance\
-   Polymorphism\
-   Abstraction

### Q2: SOLID Principles

-   Single Responsibility\
-   Open/Closed\
-   Liskov Substitution\
-   Interface Segregation\
-   Dependency Inversion

------------------------------------------------------------------------

## 3. BLoC / Cubit

### Q1: Why BLoC?

-   Clear separation of UI and logic\
-   Predictable state transitions\
-   Test-friendly\
-   Good for medium--large apps

### Q2: Cubit vs BLoC

  Cubit           BLoC
  --------------- ------------------------
  Simpler         Complex but structured
  Direct emit()   Requires events
  Lightweight     Enterprise level

------------------------------------------------------------------------

## 4. Clean Architecture -- Simple Explanation

### Three Layers

    presentation/
    domain/
    data/

### 1. Data Layer

-   Talks to API/DB\
-   Uses DTO + Model\
-   Implements Repository

### 2. Domain Layer

-   Business rules\
-   Entities\
-   UseCases\
-   Abstract repository interfaces

### 3. Presentation Layer

-   UI → BLoC\
-   Uses UI models\
-   Calls UseCases

------------------------------------------------------------------------

## 5. Example: DTO → Entity → UI Model

### Example

``` dart
// DTO (Data Layer)
class UserDto {
  final String name;
  final int age;
}
```

``` dart
// Entity (Domain Layer)
class UserEntity {
  final String name;
  final int age;
}
```

``` dart
// UI Model (Presentation Layer)
class UserUiModel {
  final String displayName;
}
```

------------------------------------------------------------------------

## 6. Full Clean Architecture Folder Structure

``` plaintext
lib/
 ├── data/
 │    ├── datasources/
 │    ├── models/
 │    ├── repositories/
 │    └── mappers/
 │
 ├── domain/
 │    ├── entities/
 │    ├── repositories/
 │    └── usecases/
 │
 ├── presentation/
 │    ├── blocs/
 │    ├── pages/
 │    ├── widgets/
 │    └── ui_models/
```

------------------------------------------------------------------------

## 7. CRUD Example (Simple Explanation)

### Example Operation: Create User

### Presentation Layer

``` dart
createUser(user);
```

### Domain Layer

``` dart
class CreateUserUseCase {
  final UserRepository repo;

  Future<void> call(UserEntity user) {
    return repo.createUser(user);
  }
}
```

### Data Layer

``` dart
class UserRepoImpl implements UserRepository {
  final Api api;

  @override
  Future<void> createUser(UserEntity user) {
    final dto = UserDto.fromEntity(user);
    return api.post('/users', dto.toJson());
  }
}
```

------------------------------------------------------------------------

## 8. DSA -- Tree Example

### Tree

            Root
           /    \
        Child1  Child2
         /   \      \
     Leaf1  Leaf2   Leaf3

### Binary Tree

            10
          /    \
         5      20
        / \    /  \
       3   7  15  25

------------------------------------------------------------------------

## 9. Git & GitHub

### Q1: What is Git Rebase?

Rebase = rewrite branch history for cleaner commits.

### Q2: Feature Branch Workflow

-   main → stable\
-   develop → active\
-   feature/xyz → work

------------------------------------------------------------------------

## 10. Firebase

### Services used

-   Firebase Auth\
-   Firestore\
-   Cloud Functions\
-   Cloud Messaging\
-   Storage

### Firestore Security Example

``` json
allow read, write: if request.auth != null;
```

------------------------------------------------------------------------

## 11. CI/CD

### GitHub Actions Example

``` yaml
name: Flutter CI
on: [push]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: subosito/flutter-action@v2
      - run: flutter pub get
      - run: flutter test
```

------------------------------------------------------------------------

## 12. WebSockets & GraphQL

### When to use WebSockets?

-   Chat\
-   Live dashboards\
-   Presence updates

### GraphQL Advantages

-   Request only required fields\
-   Reduce over-fetching

------------------------------------------------------------------------

# END OF FILE
