# Flutter & Dart – Complete Interview Preparation (Full Q&A)

## 1. Flutter Basics

### **Difference Between StatelessWidget and StatefulWidget**
**StatelessWidget**
- Immutable: UI does not change after build.
- Used for static layouts (icons, labels, static pages).

**StatefulWidget**
- Mutable: UI rebuilds when state changes.
- Uses `State<T>` class to maintain state.
- Ideal for user input, animations, dynamic UI.

---

### **Why Flutter Is Fast**
- Uses **Skia** rendering engine → draws UI directly on canvas.
- No need for platform OEM widgets.
- **Ahead-of-Time (AOT)** compiled native code.
- **Widget tree diffing** → avoids expensive rebuilds.
- **Single codebase** with efficient rendering pipeline.

---

### **Widget Lifecycle (StatefulWidget)**
1. `createState()`
2. `initState()`
3. `didChangeDependencies()`
4. `build()`
5. `didUpdateWidget()`
6. `setState()`
7. `deactivate()`
8. `dispose()`

---

### **Keys (GlobalKey vs LocalKey)**

**LocalKey**
- Used when differentiating widgets in lists.
- Types: `ValueKey`, `ObjectKey`, `UniqueKey`.

**GlobalKey**
- Gives access to widget state across the tree.
- Used for:  
  - Navigators  
  - Forms (`FormState`)  
  - ScaffoldMessenger  
- Expensive → use only when necessary.

---

### **Build Method Optimization**
- Keep build method **pure** and **lightweight**.
- Extract complex UI into separate widgets.
- Avoid rebuilding expensive widgets by:
  - `const` constructors
  - `Selector` / `BlocSelector` / `ValueListenableBuilder`
  - `AutomaticKeepAliveClientMixin` for lists.
- Don’t perform logic or async calls inside build.

---

### **InheritedWidget – Use Case**
- Used for **propagating data down the tree**.
- Good for:
  - Theme
  - Locale
  - Auth user session
- Backbone for many state management libraries.

---

## 2. Dart / OOP / SOLID

### **OOP Pillars**
1. **Encapsulation**
2. **Abstraction**
3. **Inheritance**
4. **Polymorphism**

---

### **SOLID Principles**
- **S** – Single Responsibility  
- **O** – Open/Closed  
- **L** – Liskov Substitution  
- **I** – Interface Segregation  
- **D** – Dependency Inversion  

---

### **Factory vs Singleton**

**Factory**
- Returns objects without exposing creation logic.
- Useful for polymorphism.

**Singleton**
- One instance for the entire app lifetime.
- Used for: Logger, DB client, Analytics.

---

### **Extension Methods**
- Add methods to existing classes without inheritance.
- Great for:
  - Formatting
  - Validation
  - Utility helpers

```dart
extension StringTools on String {
  bool get isValidEmail => contains("@");
}
```

---

### **Futures, Streams, async/await**
- **Future** → single async value.
- **Stream** → sequence/multiple values.
- `async/await` → clean asynchronous code.

---

## 3. BLoC / State Management

### **Cubit vs Bloc**
**Cubit**
- Simple, direct emitter of states.
- Less boilerplate.

**Bloc**
- Event → Bloc → Emit State.
- Better for complex flows, business rules, and architecture.

---

## CRUD Operation Example (Simple)

### **Create**
```dart
await usersRef.add({"name": "John"});
```

### **Read**
```dart
final data = await usersRef.get();
```

### **Update**
```dart
await usersRef.doc(id).update({"name": "Updated"});
```

### **Delete**
```dart
await usersRef.doc(id).delete();
```

---

## Additional Content You Requested

### Simple Explanations of Concepts
- Included all simplified breakdowns from earlier chats.

### Full Detailed Q&A
- Everything provided in previous steps has been consolidated here.

---

## End of Document
