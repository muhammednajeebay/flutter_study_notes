# Flutter Interview Prep -- Complete Guide

## Flutter

### Stateless vs Stateful

**StatelessWidget** - No internal state - Depends only on constructor
values

**StatefulWidget** - Maintains state across rebuilds - Uses a separate
`State` object

------------------------------------------------------------------------

### Why Flutter Is Fast

-   Uses Skia engine to render every pixel
-   AOT-compiled Dart → near-native performance
-   Avoids OEM widgets
-   Efficient widget diffing for rebuilds

------------------------------------------------------------------------

### Widget Lifecycle

1.  `createState()`
2.  `initState()`
3.  `didChangeDependencies()`
4.  `build()`
5.  `didUpdateWidget()`
6.  `setState()`
7.  `deactivate()`
8.  `dispose()`

------------------------------------------------------------------------

### Keys (GlobalKey vs LocalKey)

**LocalKey** - Identifies widgets among siblings

**GlobalKey** - Access widget state from anywhere\
- Expensive → use only when needed

------------------------------------------------------------------------

### Build Method Optimization

-   Keep build pure
-   Extract widgets
-   Use `const`
-   Use selective rebuild widgets
-   Use `RepaintBoundary` when needed

------------------------------------------------------------------------

### InheritedWidget Use Case

-   Share data down the widget tree efficiently\
-   Basis for Provider and Theme system

------------------------------------------------------------------------

## Dart / OOP / SOLID

### OOP Pillars

-   Encapsulation\
-   Abstraction\
-   Inheritance\
-   Polymorphism

------------------------------------------------------------------------

### SOLID Principles

-   Single Responsibility\
-   Open/Closed\
-   Liskov Substitution\
-   Interface Segregation\
-   Dependency Inversion

------------------------------------------------------------------------

### Factory vs Singleton

**Factory** - Controls object creation logic

**Singleton** - One instance only\
- Used for logging, caching

------------------------------------------------------------------------

### Extension Methods

Add functionality without modifying source class.

``` dart
extension StringX on String {
  bool get isValidEmail => contains('@');
}
```

------------------------------------------------------------------------

### Futures, Streams, async, await

-   Future: single async value\
-   Stream: multiple async values\
-   async/await: readable async code

------------------------------------------------------------------------

## BLoC / State Management

### Cubit vs BLoC

**Cubit** - Simple - Emits state directly

**BLoC** - Event → State mapping\
- Scalable, testable

------------------------------------------------------------------------

### Stream & Sink

-   Stream: output states\
-   Sink: input events (older BLoC)

------------------------------------------------------------------------

### Hydrated BLoC

-   Persists state to disk\
-   Restores after restart

------------------------------------------------------------------------

### Best Folder Structure

    lib/
      src/
        presentation/
        domain/
        data/
        core/

------------------------------------------------------------------------

## Clean Architecture

### 3-Layer Explanation

**Domain** - Entities\
- UseCases\
- Repository interfaces

**Data** - DTOs\
- Repo implementation\
- Data sources

**Presentation** - UI\
- BLoC\
- Screens & widgets

------------------------------------------------------------------------

### Why Domain Should Be Pure

-   No Flutter imports\
-   No Firebase\
-   Testable and reusable

------------------------------------------------------------------------

### DTO vs Entity vs UI Model

-   DTO → API/DB\
-   Entity → domain rules\
-   UI Model → presentation

------------------------------------------------------------------------

### CRUD Flow Example

UI → BLoC → UseCase → Repository → DataSource → API\
API → DTO → Entity → BLoC → UI

------------------------------------------------------------------------

## DSA

### Tree vs Binary Tree

-   Tree: unlimited children\
-   Binary Tree: max 2 children

------------------------------------------------------------------------

### Stack & Queue

-   Stack: LIFO\
-   Queue: FIFO

------------------------------------------------------------------------

### HashMap in Dart

-   `Map<K, V>`
-   O(1) average lookup

------------------------------------------------------------------------

### Time Complexity

-   O(1) → Map\
-   O(n) → Loop\
-   O(log n) → Binary search\
-   O(n log n) → Sorting\
-   O(n²) → Nested loops

------------------------------------------------------------------------

## Firebase

### Firestore vs Realtime DB

**Firestore** - Document-based\
- Better querying\
- Scalable

**Realtime DB** - JSON tree\
- Very fast but less structured

------------------------------------------------------------------------

### Cloud Functions

-   Serverless backend\
-   Triggers + custom API logic

------------------------------------------------------------------------

### FCM

-   Push notifications\
-   Topics + token-based messaging
