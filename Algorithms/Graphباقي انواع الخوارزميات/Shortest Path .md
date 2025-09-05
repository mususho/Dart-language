# Shortest Path

# ما هي خوارزمية Dijkstra؟

> خوارزمية Dijkstra تستخدم لإيجاد أقصر مسار من نقطة بداية (Source) إلى كل العقد الأخرى في رسم بياني موجه أو غير موجه، مع أوزان غير سالبة على الحواف.
> 

---

## 🪜 خطوات الحل:

### ✅ الخطوة 1: تهيئة مصفوفة المسافات مع قيمة كبيرة (∞) لكل عقدة ما عدا البداية (0)

### ✅ الخطوة 2: استخدام هيكل بيانات الأولوية (Priority Queue) لاختيار العقدة ذات أقل مسافة لم تُزر بعد

### ✅ الخطوة 3: تحديث المسافات عبر الجيران مع تحسين القيم

### ✅ الخطوة 4: تكرار حتى زيارة كل العقد أو استنفاد الأولوية

---

## 📦 كود Dart كامل مع شرح وتفصيل:

```dart
dart
نسختحرير
import 'dart:collection';

class Edge {
  final int target;
  final int weight;

  Edge(this.target, this.weight);
}

class Graph {
  final Map<int, List<Edge>> adj = {};

  void addEdge(int source, int target, int weight) {
    adj.putIfAbsent(source, () => []).add(Edge(target, weight));
    adj.putIfAbsent(target, () => []); // لضمان وجود كل العقد
  }
}

List<int> dijkstra(Graph graph, int start) {
  int n = graph.adj.length;
  List<int> dist = List.filled(n, 1 << 30);
  dist[start] = 0;

  // أولوية بناءً على أقل مسافة
  PriorityQueue<int> pq = PriorityQueue((a, b) => dist[a].compareTo(dist[b]));
  pq.add(start);

  while (pq.isNotEmpty) {
    int u = pq.removeFirst();

    for (Edge edge in graph.adj[u] ?? []) {
      int v = edge.target;
      int weight = edge.weight;

      // تحسين المسافة إذا وجدنا مسار أقصر
      if (dist[u] + weight < dist[v]) {
        dist[v] = dist[u] + weight;
        pq.add(v);
      }
    }
  }

  return dist;
}

void main() {
  Graph graph = Graph();

  // إضافة الحواف (المصدر، الوجهة، الوزن)
  graph.addEdge(0, 1, 4);
  graph.addEdge(0, 2, 1);
  graph.addEdge(2, 1, 2);
  graph.addEdge(1, 3, 1);
  graph.addEdge(2, 3, 5);
  graph.addEdge(3, 4, 3);

  List<int> distances = dijkstra(graph, 0);

  print("أقصر المسافات من العقدة 0:");
  for (int i = 0; i < distances.length; i++) {
    print("العقدة $i: المسافة = ${distances[i]}");
  }
}

```

---

## 🧪 مخرجات التجربة:

```
yaml
نسختحرير
أقصر المسافات من العقدة 0:
العقدة 0: المسافة = 0
العقدة 1: المسافة = 3
العقدة 2: المسافة = 1
العقدة 3: المسافة = 4
العقدة 4: المسافة = 7

```

---

## 🔍 شرح تفصيلي:

| الخطوة | الوصف | الكود أو التعليق |
| --- | --- | --- |
| 1 | تهيئة المسافات إلى ∞ والمسافة للبداية 0 | `dist[start] = 0` |
| 2 | استخدام PriorityQueue لاختيار العقدة الأقرب | `PriorityQueue<int>` |
| 3 | تحديث المسافات عبر جيران العقدة المختارة | داخل حلقة `for` على الجيران |
| 4 | إضافة العقدة الجديدة إلى قائمة الأولويات | `pq.add(v)` |

---

## ملاحظات:

- خوارزمية دجكسترا تعمل فقط مع أوزان غير سالبة.
- زمن التنفيذ يعتمد على هيكل بيانات الأولوية (في هذا المثال O(E log V)).
- يمكن تعديل الكود لإرجاع المسارات أيضاً عبر تخزين "السابق" لكل عقدة.