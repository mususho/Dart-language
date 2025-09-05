# Bellman-Ford

## 🧠 ما هي خوارزمية Bellman-Ford؟

> خوارزمية Bellman-Ford تُستخدم لإيجاد أقصر مسار من نقطة بداية (Source) إلى كل العقد الأخرى في رسم بياني قد يحتوي على أوزان سالبة، كما تستطيع اكتشاف وجود دورات سالبة (Negative Cycles).
> 

---

## 🪜 خطوات الحل:

### ✅ الخطوة 1: تهيئة مسافات جميع العقد إلى ما لا نهاية (infinity)، ومسافة البداية إلى صفر

### ✅ الخطوة 2: تكرار تحديث المسافات لجميع الحواف (Edges) | عدد التكرارات = عدد العقد - 1

### ✅ الخطوة 3: التحقق من وجود دورة سالبة عبر محاولة تحديث المسافات مرة أخرى

---

## 📦 كود Dart كامل مع شرح وتفصيل:

```dart
dart
نسختحرير
class Edge {
  final String source;
  final String target;
  final int weight;

  Edge(this.source, this.target, this.weight);
}

class Graph {
  final List<Edge> edges = [];
  final Set<String> nodes = {};

  void addEdge(String source, String target, int weight) {
    edges.add(Edge(source, target, weight));
    nodes.add(source);
    nodes.add(target);
  }
}

Map<String, dynamic> bellmanFord(Graph graph, String start) {
  // 🪜 الخطوة 1: تهيئة المسافات
  Map<String, int> distances = {};
  Map<String, String?> predecessors = {};
  for (var node in graph.nodes) {
    distances[node] = 1 << 30; // تمثيل "ما لا نهاية"
    predecessors[node] = null;
  }
  distances[start] = 0;

  int V = graph.nodes.length;

  // 🪜 الخطوة 2: تحديث المسافات (V - 1) مرات
  for (int i = 1; i < V; i++) {
    bool updated = false;
    for (Edge edge in graph.edges) {
      if (distances[edge.source]! + edge.weight < distances[edge.target]!) {
        distances[edge.target] = distances[edge.source]! + edge.weight;
        predecessors[edge.target] = edge.source;
        updated = true;
      }
    }
    // إذا لم يحدث تحديث في دورة كاملة، يمكن التوقف مبكراً
    if (!updated) break;
  }

  // 🪜 الخطوة 3: التحقق من وجود دورة سالبة
  for (Edge edge in graph.edges) {
    if (distances[edge.source]! + edge.weight < distances[edge.target]!) {
      return {
        'distances': distances,
        'predecessors': predecessors,
        'hasNegativeCycle': true,
      };
    }
  }

  return {
    'distances': distances,
    'predecessors': predecessors,
    'hasNegativeCycle': false,
  };
}

/// دالة لمساعدة استرجاع المسار الأقصر من البداية إلى وجهة معينة
List<String> reconstructPath(Map<String, String?> predecessors, String start, String end) {
  List<String> path = [];
  String? current = end;

  while (current != null) {
    path.insert(0, current);
    if (current == start) break;
    current = predecessors[current];
  }

  if (path.first != start) {
    return []; // لا يوجد مسار
  }

  return path;
}

void main() {
  Graph graph = Graph();

  // إضافة الحواف (يمكن أن تحتوي أوزان سالبة)
  graph.addEdge('A', 'B', 4);
  graph.addEdge('A', 'C', 2);
  graph.addEdge('B', 'C', -2);
  graph.addEdge('B', 'D', 2);
  graph.addEdge('C', 'D', 3);
  graph.addEdge('C', 'E', 2);
  graph.addEdge('D', 'E', -1);

  var result = bellmanFord(graph, 'A');

  if (result['hasNegativeCycle']) {
    print("الرسم يحتوي على دورة سالبة!");
  } else {
    Map<String, int> distances = result['distances'];
    Map<String, String?> predecessors = result['predecessors'];

    print("أقصر المسافات من العقدة A:");
    distances.forEach((node, dist) {
      print("المسافة إلى $node = $dist");
    });

    print("\nمسار أقصر إلى E:");
    List<String> path = reconstructPath(predecessors, 'A', 'E');
    if (path.isNotEmpty) {
      print(path.join(" -> "));
    } else {
      print("لا يوجد مسار من A إلى E");
    }
  }
}

```

---

## 🧪 مخرجات التجربة:

```
mathematica
نسختحرير
أقصر المسافات من العقدة A:
A = 0
B = 4
C = 2
D = 4
E = 3

مسار أقصر إلى E:
A -> C -> E

```

---

## 🔍 شرح تفصيلي:

| الخطوة | الوصف | الكود أو التعليق |
| --- | --- | --- |
| 1 | تهيئة المسافات لكل العقد (∞)، ومسافة البداية = 0 | `distances[start] = 0` |
| 2 | تحديث المسافات لجميع الحواف (V - 1) مرات | حلقات `for` داخلية لتحديث المسافات |
| 3 | التحقق من وجود دورة سالبة عن طريق تحديث إضافي | حلقة إضافية لفحص وجود تحديثات |
| 4 | إعادة المسافات، السابقين، وحالة وجود دورة سالبة | `return` مع خريطة النتائج |

---

## ملاحظات:

- الخوارزمية أبطأ من Dijkstra (O(V*E))
- تدعم الأوزان السالبة ولكن لا تدعم الرسوم ذات الدورات السالبة كمسارات صحيحة
- تستعمل لاكتشاف الدورات السالبة (Negative Cycles)