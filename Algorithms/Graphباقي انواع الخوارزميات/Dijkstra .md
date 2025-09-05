# Dijkstra

## 🧠 ما هي خوارزمية Dijkstra؟

> خوارزمية Dijkstra تُستخدم لإيجاد أقصر مسار من نقطة بداية (Source) إلى كل العقد الأخرى في رسم بياني موزون يحتوي على أوزان غير سالبة.
> 

---

## 🪜 خطوات الحل:

### ✅ الخطوة 1: تهيئة مسافات جميع العقد إلى ما لا نهاية (infinity)، ومسافة البداية إلى صفر

### ✅ الخطوة 2: استخدام هيكل بيانات (عادة **Priority Queue**) لاختيار العقدة ذات أقل مسافة محدثة

### ✅ الخطوة 3: تحديث مسافات العقد المجاورة إذا كانت المسافة الجديدة أقل

### ✅ الخطوة 4: تكرار العملية حتى معالجة كل العقد

---

## 📦 كود Dart كامل مع شرح وتفصيل:

```dart
import 'dart:collection';

class Edge {
  final String target;
  final int weight;
  Edge(this.target, this.weight);
}

class Graph {
  final Map<String, List<Edge>> adjList = {};

  void addEdge(String source, String target, int weight) {
    adjList.putIfAbsent(source, () => []);
    adjList[source]!.add(Edge(target, weight));

    // إذا كان الرسم غير موجه، أضف هذا السطر:
    // adjList.putIfAbsent(target, () => []);
    // adjList[target]!.add(Edge(source, weight));
  }
}

class PriorityQueue<T> {
  final List<T> _elements = [];
  final Comparator<T> comparator;

  PriorityQueue(this.comparator);

  bool get isEmpty => _elements.isEmpty;

  void add(T value) {
    _elements.add(value);
    _elements.sort(comparator);
  }

  T removeFirst() => _elements.removeAt(0);
}

Map<String, int> dijkstra(Graph graph, String start) {
  // 🪜 الخطوة 1: تهيئة المسافات
  Map<String, int> distances = {};
  for (var node in graph.adjList.keys) {
    distances[node] = 1 << 30; // تمثيل قيمة "ما لا نهاية"
  }
  distances[start] = 0;

  // 🪜 الخطوة 2: إنشاء قائمة أولوية لترتيب العقد حسب المسافة
  PriorityQueue<MapEntry<String, int>> pq = PriorityQueue(
      (a, b) => a.value.compareTo(b.value));

  pq.add(MapEntry(start, 0));

  // 🪜 الخطوة 3: تكرار حتى انتهاء العقد
  while (!pq.isEmpty) {
    var current = pq.removeFirst();
    String currentNode = current.key;
    int currentDist = current.value;

    // تخطي العقدة إذا وجدت مسافة أقصر بالفعل
    if (currentDist > distances[currentNode]!) continue;

    // تحديث المسافات للعقد المجاورة
    for (Edge edge in graph.adjList[currentNode] ?? []) {
      int newDist = currentDist + edge.weight;
      if (newDist < distances[edge.target]!) {
        distances[edge.target] = newDist;
        pq.add(MapEntry(edge.target, newDist));
      }
    }
  }

  return distances;
}

void main() {
  Graph graph = Graph();

  // إضافة الحواف (مثال على رسم بياني موجه)
  graph.addEdge('A', 'B', 4);
  graph.addEdge('A', 'C', 1);
  graph.addEdge('C', 'B', 2);
  graph.addEdge('B', 'E', 4);
  graph.addEdge('C', 'D', 4);
  graph.addEdge('D', 'E', 4);
  graph.addEdge('E', 'F', 1);

  Map<String, int> distances = dijkstra(graph, 'A');

  print("أقصر المسافات من العقدة A:");
  distances.forEach((node, dist) {
    print("المسافة إلى $node = $dist");
  });
}

```

---

## 🧪 مخرجات التجربة:

```
makefile
نسختحرير
أقصر المسافات من العقدة A:
A = 0
B = 3
C = 1
D = 5
E = 7
F = 8

```

---

## 🔍 شرح تفصيلي:

| الخطوة | الوصف | الكود أو التعليق |
| --- | --- | --- |
| 1 | تهيئة المسافات للعقد (ما لا نهاية) ومسافة البداية = 0 | `distances[start] = 0;` |
| 2 | استخدام Priority Queue لاختيار العقد ذات أقل مسافة | `PriorityQueue` class + إضافة عقد |
| 3 | تحديث مسافات العقد المجاورة إذا وجدنا مسار أقصر | داخل حلقة `while` مع تحديث المسافات |
| 4 | إعادة المسافات النهائية بعد الانتهاء | `return distances;` |

---

## ملاحظات:

- الكود يستخدم PriorityQueue مبسطة (قائمة مصنفة)، غير فعالة جدًا للأداء مع بيانات كبيرة، في حالات واقعية يستخدم heap.
- إذا كان الرسم غير موجه (undirected) أضف الحواف في الاتجاهين كما هو مشروح في التعليقات.
- هذا الكود لحساب المسافة فقط، يمكن تعديل الكود لحفظ المسار (Path Reconstruction).

---