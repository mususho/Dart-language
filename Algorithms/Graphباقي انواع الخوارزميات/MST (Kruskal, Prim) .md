# MST (Kruskal, Prim)

# 🧠 ما هي شجرة التغطية الصغرى (MST)؟

> هي شجرة فرعية من الرسم البياني غير الموجه (Undirected Graph) تربط كل العقد معًا بأقل مجموع أوزان للحواف، بدون دوائر.
> 

---

## 1. خوارزمية Kruskal

---

### 🪜 خطوات الحل:

- فرز كل الحواف حسب الوزن تصاعديًا.
- بدءًا من أقل وزن، نضيف الحواف التي لا تُكوّن دورة.
- نستخدم **Union-Find** لفحص الدورات بسرعة.
- نكرر حتى نحصل على n-1 حافة (n عدد العقد).

---

### 📦 كود Dart لخوارزمية Kruskal:

```dart
dart
نسختحرير
class Edge {
  int u, v, weight;
  Edge(this.u, this.v, this.weight);
}

class UnionFind {
  late List<int> parent, rank;

  UnionFind(int n) {
    parent = List.generate(n, (i) => i);
    rank = List.filled(n, 0);
  }

  int find(int x) {
    if (parent[x] != x) parent[x] = find(parent[x]);
    return parent[x];
  }

  bool union(int x, int y) {
    int rootX = find(x);
    int rootY = find(y);
    if (rootX == rootY) return false;

    if (rank[rootX] < rank[rootY]) {
      parent[rootX] = rootY;
    } else if (rank[rootX] > rank[rootY]) {
      parent[rootY] = rootX;
    } else {
      parent[rootY] = rootX;
      rank[rootX]++;
    }
    return true;
  }
}

List<Edge> kruskal(int n, List<Edge> edges) {
  // 1. فرز الحواف
  edges.sort((a, b) => a.weight.compareTo(b.weight));

  UnionFind uf = UnionFind(n);
  List<Edge> mst = [];

  // 2. إضافة الحواف مع التأكد من عدم وجود دورة
  for (var edge in edges) {
    if (uf.union(edge.u, edge.v)) {
      mst.add(edge);
      if (mst.length == n - 1) break;
    }
  }

  return mst;
}

void main() {
  int n = 5; // عدد العقد
  List<Edge> edges = [
    Edge(0, 1, 2),
    Edge(0, 3, 6),
    Edge(1, 3, 8),
    Edge(1, 2, 3),
    Edge(2, 3, 7),
    Edge(2, 4, 5),
    Edge(3, 4, 9),
  ];

  List<Edge> mst = kruskal(n, edges);

  print("حواف MST باستخدام Kruskal:");
  for (var e in mst) {
    print("${e.u} -- ${e.v} : ${e.weight}");
  }
}

```

---

## 2. خوارزمية Prim

---

### 🪜 خطوات الحل:

- نبدأ من عقدة عشوائية (مثلاً 0).
- نستخدم هيكل بيانات الأولوية لاختيار أقل حافة تربط العقدة الحالية بعقد غير مزارة.
- نكرر حتى يتم تغطية كل العقد.

---

### 📦 كود Dart لخوارزمية Prim:

```dart
dart
نسختحرير
import 'dart:collection';

class EdgePrim {
  final int target;
  final int weight;
  EdgePrim(this.target, this.weight);
}

List<EdgePrim> prim(int n, Map<int, List<EdgePrim>> graph) {
  Set<int> visited = {};
  List<EdgePrim> mstEdges = [];

  // Min-heap مبني على الأولوية بالوزن
  PriorityQueue<MapEntry<int, int>> pq = PriorityQueue(
      (a, b) => a.value.compareTo(b.value)); // (node, weight)

  pq.add(MapEntry(0, 0)); // بدءاً من العقدة 0 بوزن 0
  List<int> key = List.filled(n, 1 << 30);
  key[0] = 0;
  List<int?> parent = List.filled(n, null);

  while (pq.isNotEmpty) {
    int u = pq.removeFirst().key;
    if (visited.contains(u)) continue;

    visited.add(u);

    if (parent[u] != null) {
      mstEdges.add(EdgePrim(u, key[u]));
    }

    for (var edge in graph[u] ?? []) {
      int v = edge.target;
      int w = edge.weight;

      if (!visited.contains(v) && w < key[v]) {
        key[v] = w;
        parent[v] = u;
        pq.add(MapEntry(v, w));
      }
    }
  }

  return mstEdges;
}

void main() {
  int n = 5;

  Map<int, List<EdgePrim>> graph = {
    0: [EdgePrim(1, 2), EdgePrim(3, 6)],
    1: [EdgePrim(0, 2), EdgePrim(2, 3), EdgePrim(3, 8)],
    2: [EdgePrim(1, 3), EdgePrim(3, 7), EdgePrim(4, 5)],
    3: [EdgePrim(0, 6), EdgePrim(1, 8), EdgePrim(2, 7), EdgePrim(4, 9)],
    4: [EdgePrim(2, 5), EdgePrim(3, 9)],
  };

  List<EdgePrim> mst = prim(n, graph);

  print("حواف MST باستخدام Prim:");
  for (var e in mst) {
    print("العقدة: ${e.target}، الوزن: ${e.weight}");
  }
}

```

---

## 🔍 شرح تفصيلي

| الخوارزمية | الفكرة الأساسية | التعقيد الزمني |
| --- | --- | --- |
| Kruskal | فرز الحواف، دمج مجموعات باستخدام Union-Find لمنع الدورات | O(E log E) أو O(E log V) |
| Prim | بناء MST بزيارة العقد تدريجيًا واختيار أقل حافة متاحة | O(E log V) باستخدام PriorityQueue |