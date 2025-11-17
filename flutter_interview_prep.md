# Flutter Interview Prep -- Sentence-Style Answers

## 1. Memory Management in Flutter

Flutter handles memory automatically through Dart's garbage collector,
which continuously frees unused memory, optimizes object allocation in
the heap, and prevents leaks when widgets are correctly managed within
the widget lifecycle.

## 2. Flutter State Rebuild Flow

Flutter rebuilds UI by passing immutable widget configurations into the
widget tree, detecting changes, and updating only the affected elements
through its efficient render and element tree comparison.

## 3. BLoC Pattern (Business Logic Component)

The BLoC pattern separates presentation from business logic by using
streams where the UI sends events and listens for state updates,
allowing predictable, testable, and scalable architecture.

## 4. Clean Architecture in Flutter

Clean Architecture organizes the code into presentation, domain, and
data layers, ensuring that UI depends on use cases rather than
implementation details, and making refactoring, scaling, and testing
smoother.

## 5. BloC vs Provider

BLoC uses events and streams to manage complex, layered logic, while
Provider offers a simpler, lightweight, and reactive approach suitable
for smaller or less state-heavy applications.

## 6. `const` vs `final`

`const` guarantees compile-time constants and supports widget rebuild
optimization, whereas `final` assigns values only once at runtime
without the same performance advantage.

## 7. App Size Optimization

App size is reduced through tree-shaking, deferred imports, icon font
minimization, asset compression, and ProGuard/R8 when building release
versions.

## 8. Performance Optimization

Performance improves when expensive operations are isolated outside the
build method, widgets are kept pure, const widgets are used, and
unnecessary rebuilds are avoided through proper state management.

## 9. Isolates

Isolates run expensive tasks on separate threads without blocking the
main UI thread, making them ideal for heavy computations like
encryption, parsing, or image processing.

## 10. Future vs Stream

A Future resolves a single asynchronous value once, while a Stream emits
multiple values over time and is ideal for continuous updates such as
sockets or real-time data.

## 11. Algorithm

An algorithm is a structured and repeatable set of steps used to solve
problems efficiently by reducing time and space usage.

## 12. Time Complexity

Time complexity estimates how the execution time of an algorithm grows
relative to input size, helping compare efficiency between logical
approaches.

## 13. CI/CD

CI/CD automates building, testing, and deploying your Flutter app,
ensuring faster releases, fewer bugs, and consistent delivery across
environments.

## 14. Mixins

Mixins allow shared functionality to be included in multiple classes
without inheritance, making them useful for reusable methods like
validation or logging.

## 15. FutureBuilder vs StreamBuilder

FutureBuilder handles one-time future results, while StreamBuilder
listens to ongoing streams such as live updates or socket connections.

## 16. Keys

Keys help Flutter preserve widget state during reordering or rebuilding
by uniquely identifying widgets, especially in lists.

## 17. InheritedWidget

InheritedWidget provides an efficient way to share data down the widget
tree without rebuilding unrelated widgets, forming the base of state
management tools like Provider.

## 18. Abstraction

Abstraction hides implementation details and exposes essential
functionality so developers interact with cleaner and more flexible
interfaces.
