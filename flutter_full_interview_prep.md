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


# Flutter Advanced Interview Questions and Answers

A complete technical preparation document covering Flutter architecture, performance, rendering, native integration, and clean code principles.

---

## 🧱 Clean Architecture & Code Design

### **1. How do you maintain modularity in a large Flutter project?**
I organize projects using feature-based clean architecture: each feature contains its own data, domain, and presentation layer. Shared logic (routes, themes, constants, network clients) stays in the `core/` folder. This makes the project scalable and modular.

### **2. How do you implement dependency inversion in Flutter?**
Define abstract repositories in the domain layer, and implement them in the data layer. Higher layers depend on abstractions, not concrete classes.
```dart
abstract class UserRepo { Future<User> getUser(); }
class UserRepoImpl implements UserRepo { ... }
```

### **3. How do you ensure clean separation between logic and UI?**
Keep business logic in state managers like BLoC or Provider. The UI only listens to state changes — it never directly executes logic or API calls.

### **4. How do you handle cross-feature communication?**
Use shared providers, event buses, or service locators (like GetIt). Avoid direct imports between features to prevent circular dependencies.

---

## ⚡ State Management & Data Flow

### **5. How do you structure a BLoC for API calls?**
Events trigger repository calls → emit loading/success/error states → UI listens using BlocBuilder. Keeps UI reactive and logic testable.

### **6. When should you prefer Cubit over BLoC?**
Cubit is ideal for simpler state flows without multiple events. BLoC fits complex, multi-event flows or async tasks.

### **7. How do you debug state issues in Flutter?**
Use BlocObserver for BLoC, debug flags in Provider, and Flutter DevTools’ rebuild tracker to spot unnecessary rebuilds.

---

## 🌐 Networking, GraphQL & WebSocket

### **8. How is GraphQL integration different from REST?**
GraphQL uses a single endpoint and allows querying only required fields — reducing payload and improving efficiency. I use `graphql_flutter` for caching and subscriptions.

### **9. How do you handle WebSocket reconnections?**
Use timers and exponential backoff retry logic. On reconnection, resubscribe to streams to restore real-time data flow.

### **10. How do you handle concurrent API calls efficiently?**
Use `Future.wait([])` for parallel execution and caching (Hive/SQLite) to prevent redundant requests.

---

## 🎨 UI, Rendering & Performance

### **11. How do you minimize frame drops during animation or scrolling?**
Move heavy logic to isolates, lazy load large lists, use RepaintBoundary for expensive widgets, and pre-cache assets.

### **12. What happens internally when `setState()` is called?**
Marks the widget subtree as dirty → rebuilds affected elements → updates render objects → triggers paint and compositing.

### **13. How does Flutter’s rendering pipeline handle a frame?**
Build → Layout → Paint → Compositing → Rasterization → Display. Only dirty widgets rebuild; Skia rasterizes to GPU.

### **14. How do you reduce widget rebuild cost?**
Use const widgets, extract child widgets, and apply `Selector` or `BlocBuilder` to rebuild only relevant UI parts.

---

## 🔌 Native Integration & Platform Channels

### **15. Difference between MethodChannel, EventChannel, and BasicMessageChannel**
| Channel | Purpose | Direction |
|----------|----------|-----------|
| MethodChannel | One-time call (request-response) | Dart ↔ Native |
| EventChannel | Continuous data stream | Native → Dart |
| BasicMessageChannel | Bidirectional message passing | Dart ↔ Native |

### **16. How does Flutter communicate with native Android/iOS code?**
Via binary messages handled by the Flutter Engine bridge. Dart calls native through `MethodChannel.invokeMethod()`, native executes and returns async results.

### **17. How can you embed a native view in Flutter UI?**
Use **PlatformView** (e.g., GoogleMap, WebView). Flutter composites it into the widget tree as a texture.

### **18. How do you handle heavy native computation efficiently?**
Run it on background threads (`Dispatchers.IO` in Kotlin, GCD in Swift), then return data to Flutter via MethodChannel.

---

## 🧵 Isolates & Concurrency

### **19. What are Isolates in Dart?**
Independent memory and event loops for parallel execution. Use for CPU-heavy work like JSON parsing or encryption.

### **20. How does Flutter’s garbage collection work?**
Automatic mark-and-sweep GC frees unreferenced objects. Avoid leaks by disposing controllers and subscriptions.

### **21. How do you detect memory leaks?**
Use Flutter DevTools (Memory tab) and look for growing heap usage. Dispose controllers, streams, and listeners properly.

### **22. How does Flutter use GPU and Skia for rendering?**
Flutter compiles UI into Skia draw commands → Skia rasterizes → GPU renders pixels. Provides consistent 60–120 FPS across devices.

---

## ⚙️ Architecture, Offline Mode & CI/CD

### **23. How do you structure an offline-first feature?**
Cache API data locally with Hive/Sqflite → serve cached data immediately → sync updates when online.

### **24. How do you manage multiple environments (dev/staging/prod)?**
Use `.env` + `flutter_dotenv`. Separate Firebase projects for each environment.

### **25. How do you implement CI/CD?**
Use GitHub Actions or Codemagic. Pipeline: Lint → Test → Build → Deploy (Firebase App Distribution / Play Store).

### **26. Common Flutter performance pitfalls**
Too many rebuilds, blocking isolate with sync work, deep widget trees, unoptimized image assets.

### **27. How do you handle version control and code reviews?**
Follow GitHub Flow (feature branches + PRs + reviews). Use commit conventions (feat/fix/chore) and enforce linting pre-merge.

---

## 🧠 Flutter Rendering & Trees

### **28. What are the three main trees in Flutter?**
| Tree | Purpose |
|------|----------|
| Widget Tree | UI blueprint (immutable) |
| Element Tree | Widget instances + state (mutable) |
| Render Tree | Layout & painting |

Only affected subtrees rebuild and repaint for efficiency.

### **29. What triggers a new frame in Flutter?**
UI changes (setState, notifyListeners), animations, or system-driven redraws.

### **30. How do you profile performance?**
Use Flutter DevTools → CPU profiler, memory tracker, rebuild monitor, and performance overlay.

---

## 🧾 Summary Notes

- **Focus Areas:** Clean Architecture, GraphQL, WebSocket, Performance Profiling, Native Integration.
- **Optimization Core Idea:** Rebuild less, repaint less, move heavy work off the UI isolate.
- **Architectural Mindset:** Keep data, logic, and UI independent and testable.
- **Real-Time Stack:** WebSocket + Stream + BLoC = reactive, low-latency data flow.


# 🧭 Flutter Technical Round Master Notes

**Target Topics:** Rendering, Performance, Trees, Skia, Isolates, Memory, Platform Channels, and Flutter–Native Communication Flow.  
**Goal:** High-confidence, deep yet concise understanding for technical interviews.

---

## ⚙️ Rendering Pipeline (Frame Rendering Flow)

**Steps (per frame):**

1. **Widget Tree** — Describes the UI (immutable blueprints).  
2. **Element Tree** — Maintains widget instances and state.  
3. **Render Tree** — Handles layout, painting, and compositing.

**Frame process:**
```
Widgets rebuild → Elements updated → RenderObjects re-layout/paint → Skia draws frame → GPU renders
```

**Performance goal:**  
→ Keep each frame under **16 ms** for **60 fps**.

---

## 🧩 Flutter’s Three Trees

| Tree | Purpose | Mutable? |
|------|----------|-----------|
| **Widget Tree** | Blueprint of the UI | ❌ Immutable |
| **Element Tree** | Links widgets and manages state | ✅ Mutable |
| **Render Tree** | Handles layout, painting | ✅ Mutable |

**Optimization Tip:**  
Flutter reuses elements and render objects where possible — only diffs and rebuilds the changed parts.

---

## ⚡ Widget Rebuild Efficiency

- Use `const` constructors whenever possible.  
- Extract reusable UI into smaller **StatelessWidgets**.  
- Use `Selector`, `ValueListenableBuilder`, or `BlocBuilder` to limit rebuild scope.  
- Avoid unnecessary `setState()` calls.  
- Use **RepaintBoundary** to isolate expensive paint regions.

---

## 🎨 Skia Rendering Engine

- Flutter uses **Skia**, a 2D graphics engine, to draw directly on the canvas.  
- Bypasses OEM widgets — gives **pixel-perfect** consistency across Android/iOS.  
- The **Render Tree → Layer Tree** is rasterized by Skia → GPU.  
- Each frame is **redrawn from scratch** for simplicity and speed.

---

## 🚀 Performance Optimization Checklist

✅ Use `const` where possible.  
✅ Split widgets to avoid deep rebuilds.  
✅ Use `ListView.builder` / `GridView.builder` for long lists.  
✅ Avoid heavy work on main isolate (use `compute()` or isolate).  
✅ Cache images (`cached_network_image`, `ImageCache`).  
✅ Profile performance in **Flutter DevTools → CPU & GPU Frame charts**.

---

## 🔀 Isolates & Concurrency

- **Main isolate:** Runs UI and all Dart code.  
- **Isolates:** Separate memory and event loops — perfect for CPU-heavy tasks.  
- No shared memory → communicate via **SendPort/ReceivePort**.  
- Built-in helper:  
 ```dart
 final result = await compute(expensiveTask, data);
 ```
- **Use cases:** Parsing JSON, image processing, encryption, etc.

---

## 🧠 Memory Management in Flutter

- Dart VM uses **Garbage Collection (GC)** for automatic cleanup.  
- Always `dispose()` controllers:
- `AnimationController`, `StreamController`, `PageController`, etc.  
- Avoid keeping unnecessary lists or widgets in memory.  
- Prefer `const` and `final` → fewer allocations.  
- Detect leaks using **DevTools → Memory tab**.

---

## 🔌 Platform Channels Overview

**Flutter ↔ Native bridge** using Platform Channels.

---

### 📡 MethodChannel

**Use:** Call native methods and get results.  
**Direction:** Flutter → Native (async response)  
**Codec:** `StandardMethodCodec`

```dart
const platform = MethodChannel('battery');
final batteryLevel = await platform.invokeMethod('getBatteryLevel');
```

**Use cases:** Camera, permissions, GPS calls, etc.

---

### 🌊 EventChannel

**Use:** Continuous data stream from Native → Flutter.  
**Direction:** Native → Flutter  
**API:** `receiveBroadcastStream()`

```dart
const stream = EventChannel('battery_stream');
stream.receiveBroadcastStream().listen((event) {
 print('Battery level: $event');
});
```

**Use cases:** Sensors, Bluetooth, connectivity.

---

### 🔁 BasicMessageChannel

**Use:** Bidirectional messaging (both directions).  
**Supports:** Custom codecs (`StringCodec`, `JSONMessageCodec`, etc.)

```dart
const channel = BasicMessageChannel('chat', StringCodec());

channel.setMessageHandler((msg) async {
 print('From native: $msg');
 return 'Flutter received';
});

channel.send('Hello from Flutter');
```

---

## ⚖️ EventChannel vs BasicMessageChannel

| Aspect | EventChannel | BasicMessageChannel |
|---------|---------------|---------------------|
| **Purpose** | Continuous data stream | Bidirectional messaging |
| **Direction** | Native → Flutter | Flutter ↔ Native |
| **Data Type** | Stream (EventSink) | Arbitrary messages |
| **Codec** | StandardMessageCodec | Custom codecs |
| **Use Case** | Sensors, Bluetooth, etc. | Chat, logs, commands |
| **Lifecycle** | Starts on listen | Always active |

---

## 🧩 Flutter–Native Communication (Under the Hood)

**Layers:**

1. **Flutter Framework (Dart)** — Widgets, rendering logic, Platform Channels.  
2. **Flutter Engine (C++)** — Skia rendering, text, image, accessibility.  
3. **Platform (Android/iOS)** — Executes native plugins & APIs.

**Flow:**
```
Dart (Flutter Framework)
  ↓
Platform Channel (via BinaryMessenger)
  ↓
Flutter Engine (C++)
  ↓
Native Plugin (Java/Kotlin or Swift/Obj-C)
  ↓
Native OS APIs
```

**Data transfer:**  
Serialized → binary → transmitted → decoded asynchronously.

**Example Flow:**

```dart
await platform.invokeMethod('getBatteryLevel');
```

→ Engine passes message → Native plugin executes → returns via `result.success()` → back to Dart isolate.

**Key takeaway:**  
The Flutter Engine acts as a **binary messenger** — it routes data between Dart VM and native asynchronously.

---

## 🧩 Quick Recap Table

| Concept | Purpose | Direction | Key API / Note |
|----------|----------|------------|----------------|
| **MethodChannel** | One-time method calls | Flutter → Native | `invokeMethod()` |
| **EventChannel** | Continuous stream | Native → Flutter | `receiveBroadcastStream()` |
| **BasicMessageChannel** | Two-way messaging | Both ways | `send()`, `setMessageHandler()` |
| **Isolate** | Parallel computation | N/A | `compute()`, `Isolate.spawn()` |
| **RepaintBoundary** | Isolate paint ops | N/A | Used for performance |
| **Skia Engine** | Draws everything | N/A | Consistent GPU rendering |

---

## 🔥 One-Liners for Rapid Revision

- “Flutter re-renders UI at 60 fps via **Skia**, not native widgets.”  
- “Widget tree is **immutable**; Element tree manages lifecycle; Render tree draws.”  
- “Use `const`, avoid deep rebuilds, profile with DevTools.”  
- “**Isolates** prevent UI jank — use `compute()` for heavy tasks.”  
- “**Platform Channels** connect Dart isolate ↔ native plugins.”  
- “**EventChannel** is for native → Flutter streams; **BasicMessageChannel** is two-way.”

---