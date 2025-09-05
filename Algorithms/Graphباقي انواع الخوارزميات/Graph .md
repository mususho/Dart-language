# Graph

---

# 1. ما هو الـ Graph؟

> Graph هو هيكل بيانات يتكون من مجموعة من العُقد (Nodes أو Vertices) ومجموعة من الحواف (Edges) التي تربط بين هذه العُقد.
> 

---

## أنواع الرسوم البيانية

| النوع | الوصف |
| --- | --- |
| **موجه (Directed)** | الحواف لها اتجاه معين (من عقدة إلى أخرى) |
| **غير موجه (Undirected)** | الحواف غير موجهة، تربط عقدتين بشكل ثنائي الاتجاه |
| **موزون (Weighted)** | لكل حافة وزن أو تكلفة (مثلاً المسافة أو الزمن) |
| **غير موزون (Unweighted)** | الحواف بدون وزن |

---

# 2. تمثيل Graph في Dart

---

## 2.1 باستخدام قائمة الجوار (Adjacency List)

- نستخدم `Map` حيث المفتاح هو العقدة، والقيمة هي قائمة العقد المرتبطة بها.
- مناسب لمعظم العمليات والكفاءة.

---

## مثال: تمثيل Graph غير موجه (Undirected)

```dart
dart
نسختحرير
void main() {
  // تعريف الرسم البياني باستخدام Map
  Map<String, List<String>> graph = {
    'A': ['B', 'C'],
    'B': ['A', 'D', 'E'],
    'C': ['A', 'F'],
    'D': ['B'],
    'E': ['B', 'F'],
    'F': ['C', 'E'],
  };

  printGraph(graph);
}

/// دالة لطباعة الرسم البياني
void printGraph(Map<String, List<String>> graph) {
  graph.forEach((node, neighbors) {
    print('$node -> ${neighbors.join(', ')}');
  });
}

```

---

## 2.2 تمثيل Graph موجه (Directed)

```dart
dart
نسختحرير
void main() {
  Map<String, List<String>> directedGraph = {
    'A': ['B', 'C'],
    'B': ['D'],
    'C': ['E'],
    'D': [],
    'E': ['F'],
    'F': ['C'],
  };

  printGraph(directedGraph);
}

```

---

# 3. عمليات شائعة على الرسوم البيانية

---

## 3.1 بحث **BFS** (Breadth-First Search)

- يستخدم لاستكشاف العقد بترتيب المستوى.
- مفيد لإيجاد أقصر مسار في رسم غير موزون.

```dart
dart
نسختحرير
import 'dart:collection';

void bfs(Map<String, List<String>> graph, String start) {
  Queue<String> queue = Queue();
  Set<String> visited = {};

  queue.add(start);
  visited.add(start);

  while (queue.isNotEmpty) {
    String node = queue.removeFirst();
    print(node);

    for (String neighbor in graph[node] ?? []) {
      if (!visited.contains(neighbor)) {
        queue.add(neighbor);
        visited.add(neighbor);
      }
    }
  }
}

```

---

## 3.2 بحث **DFS** (Depth-First Search)

- يستخدم لاستكشاف عمق الرسم البياني.
- يمكن تنفيذه بالاستدعاء الذاتي (Recursion).

```dart
dart
نسختحرير
void dfs(Map<String, List<String>> graph, String node, Set<String> visited) {
  visited.add(node);
  print(node);

  for (String neighbor in graph[node] ?? []) {
    if (!visited.contains(neighbor)) {
      dfs(graph, neighbor, visited);
    }
  }
}

```

---

# 4. مثال عملي: استخدام Graph و BFS و DFS

```dart
dart
نسختحرير
void main() {
  Map<String, List<String>> graph = {
    'A': ['B', 'C'],
    'B': ['D', 'E'],
    'C': ['F'],
    'D': [],
    'E': ['F'],
    'F': [],
  };

  print("BFS starting from A:");
  bfs(graph, 'A');

  print("\nDFS starting from A:");
  dfs(graph, 'A', <String>{});
}

```

---

## ناتج المثال:

```
less
نسختحرير
BFS starting from A:
A
B
C
D
E
F

DFS starting from A:
A
B
D
E
F
C

```

---

# 5. ملخص:

| المفهوم | الشرح |
| --- | --- |
| Graph | مجموعة عقد وحواف |
| تمثيل Graph | باستخدام قائمة الجوار (Map) |
| BFS | بحث بالعرض (المستوى الأول) |
| DFS | بحث بالعمق (استدعاء ذاتي) |

---

هل تريدني أشرح لك تمثيل **Graphs** باستخدام **Matrix (Adjacency Matrix)**؟

أو كيفية التعامل مع **Graphs موزونة Weighted Graphs**، أو خوارزميات متقدمة مثل **Dijkstra** أو **Topological Sort**؟

أو تريد كود Flutter لتصور رسم بياني؟

2/2