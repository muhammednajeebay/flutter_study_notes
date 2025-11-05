🧭 Flutter Technical Round Master Notes

Target Topics: Rendering, Performance, Trees, Skia, Isolates, Memory, Platform Channels, and Flutter–Native Communication Flow.
Goal: High-confidence, deep yet concise understanding for technical interviews.

⚙️ Rendering Pipeline (Frame Rendering Flow)

Steps (per frame):

Widget Tree — Describes the UI (immutable blueprints).

Element Tree — Maintains widget instances and state.

Render Tree — Handles layout, painting, and compositing.

Frame process:

Widgets rebuild → Elements updated → RenderObjects re-layout/paint → Skia draws frame → GPU renders


Performance goal:
→ Keep each frame under 16 ms for 60 fps.

🧩 Flutter’s Three Trees
Tree	Purpose	Mutable?
Widget Tree	Blueprint of the UI	❌ Immutable
Element Tree	Links widgets and manages state	✅ Mutable
Render Tree	Handles layout, painting	✅ Mutable

Optimization Tip: Flutter reuses elements and render objects where possible — only diffs and rebuilds the changed parts.

⚡ Widget Rebuild Efficiency

Use const constructors whenever possible.

Extract reusable UI into smaller stateless widgets.

Use Selector, ValueListenableBuilder, or BlocBuilder to limit rebuild scope.

Avoid unnecessary setState() calls.

Use RepaintBoundary to isolate expensive paint regions.

🎨 Skia Rendering Engine

Flutter uses Skia, a 2D graphics engine, to draw directly on the canvas.

Bypasses OEM widgets, giving pixel-perfect consistency across Android/iOS.

The Render Tree → Layer Tree is rasterized by Skia → GPU.

Each frame is redrawn from scratch for simplicity and speed.

🚀 Performance Optimization Checklist

✅ Use const where possible.
✅ Split widgets to avoid deep rebuilds.
✅ Use ListView.builder and GridView.builder for long lists.
✅ Avoid heavy work on main isolate (move to compute() or isolate).
✅ Cache images (cached_network_image or ImageCache).
✅ Profile performance with Flutter DevTools → CPU & GPU Frame charts.

🔀 Isolates & Concurrency

Main isolate: Runs UI and all Dart code.

Isolates: Separate memory and event loops — perfect for CPU-heavy tasks.

No shared memory → communicate via ports (SendPort/ReceivePort).

Built-in helper: compute(fn, arg) for quick background tasks.

Example:

final result = await compute(expensiveTask, data);


Use cases: Parsing JSON, image processing, encryption, etc.

🧠 Memory Management in Flutter

Dart VM uses Garbage Collection (GC) for automatic cleanup.

Dispose of controllers:

AnimationController, StreamController, PageController, etc.

Avoid holding unnecessary lists or widgets in memory.

Prefer const and final → fewer allocations.

Detect leaks in DevTools → Memory tab.

🔌 Platform Channels Overview

Flutter communicates with native code through Platform Channels — bridges between Dart and platform (Android/iOS) layers.

📡 MethodChannel

Use: Call native methods and get results.

Direction: Flutter → Native (with async response).
Codec: StandardMethodCodec.

Example:

const platform = MethodChannel('battery');
final batteryLevel = await platform.invokeMethod('getBatteryLevel');


Use cases: Camera, permissions, GPS calls, etc.

🌊 EventChannel

Use: Continuous streams of data from native → Flutter.
Example: Sensors, Bluetooth, connectivity.

Direction: Native → Flutter (stream).
API: receiveBroadcastStream()

Example:

const stream = EventChannel('battery_stream');
stream.receiveBroadcastStream().listen((event) {
  print('Battery level: $event');
});

🔁 BasicMessageChannel

Use: Bidirectional message passing (both directions).
Supports: Custom codecs (StringCodec, JSONMessageCodec, etc.)

Example:

const channel = BasicMessageChannel('chat', StringCodec());

channel.setMessageHandler((msg) async {
  print('From native: $msg');
  return 'Flutter received';
});

channel.send('Hello from Flutter');

⚖️ EventChannel vs BasicMessageChannel
Aspect	EventChannel	BasicMessageChannel
Purpose	Continuous data stream	Bidirectional messaging
Direction	Native → Flutter	Flutter ↔ Native
Data Type	Stream (EventSink)	Arbitrary messages
Codec	StandardMessageCodec	Custom codecs
Use Case	Sensors, Bluetooth, etc.	Chat, logs, commands
Lifecycle	Starts on listen	Always active
🧩 How Flutter Communicates with Native Code (Under the Hood)

Layers:

Flutter Framework (Dart) — Widgets, rendering logic, Platform Channels.

Flutter Engine (C++) — Skia rendering, text, image, accessibility.

Platform (Android/iOS) — Executes native plugins & APIs.

Communication Flow:

Dart (Flutter Framework)
   ↓
Platform Channel (via BinaryMessenger)
   ↓
Flutter Engine (C++)
   ↓
Native Plugin (Java/Kotlin or Swift/Obj-C)
   ↓
Native OS APIs


Data transfer:

Serialized via codecs → binary → transmitted → decoded on other side.

Messages are asynchronous.

Each channel identified by a unique string name shared by Dart & native.

Example Flow:

await platform.invokeMethod('getBatteryLevel');


→ Engine passes message → native plugin executes → returns via result.success() → back to Dart isolate.

Key takeaway:

The Flutter engine acts as a binary messenger — it doesn’t interpret data, only routes it between Dart VM and platform code asynchronously.

🧩 Quick Recap Table
Concept	Purpose	Direction	Key API / Note
MethodChannel	One-time method calls	Flutter → Native	invokeMethod()
EventChannel	Continuous stream	Native → Flutter	receiveBroadcastStream()
BasicMessageChannel	Two-way messaging	Both ways	send(), setMessageHandler()
Isolate	Parallel computation	N/A	compute() or Isolate.spawn()
RepaintBoundary	Isolate paint operations	N/A	Used for performance
Skia Engine	Draws everything to GPU	N/A	Consistent, fast rendering
🔥 One-Liners for Rapid Revision

“Flutter re-renders UI at 60 fps via Skia — not native widgets.”

“Widget tree is immutable; Element tree holds lifecycle; Render tree draws.”

“Use const, avoid deep rebuilds, and profile with DevTools.”

“Isolates prevent UI jank — compute() for offloading CPU-heavy work.”

“Platform channels connect Dart isolate ↔ native plugins through the engine.”

“EventChannel is for native → Flutter streams; BasicMessageChannel is two-way.”
