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
| Render Tree | Layout & painting |Only affected subtrees rebuild and repaint for efficiency.|

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
