# Kosaraju’s SCC

# 🧠 ما هي خوارزمية Kosaraju؟

> خوارزمية Kosaraju تستخدم لإيجاد المكونات المتصلة بقوة (SCC) في رسم بياني موجه (Directed Graph).
> 
> 
> مكون متصل بقوة هو مجموعة من العقد حيث كل عقدة يمكن الوصول إليها من كل عقدة أخرى داخل نفس المجموعة.
> 

---

## 🪜 خطوات الحل (بشكل مبسط):

1. **الخطوة 1: ترتيب العقد**
    - نستخدم DFS لنزور كل العقد ونضعها في مكدس حسب وقت الانتهاء (تخزين العقد بعد الانتهاء من زيارة جميع جيرانها).
2. **الخطوة 2: عكس الرسم البياني**
    - نعكس اتجاه كل الحواف في الرسم.
3. **الخطوة 3: زيارة العقد بناءً على الترتيب في المكدس**
    - نستخدم DFS على الرسم المعكوس، نزور العقد حسب الترتيب العكسي للمكدس من الخطوة 1.
    - كل استدعاء DFS جديد يمثل مكون متصل بقوة.

---

## 📦 كود Dart كامل مع شرح وتفصيل:

```dart
dart
نسختحرير
void main() {
  Map<int, List<int>> graph = {
    0: [1],
    1: [2],
    2: [0, 3],
    3: [4],
    4: [],
  };

  List<List<int>> sccs = kosarajuSCC(graph);

  print("المكونات المتصلة بقوة (SCC):");
  for (int i = 0; i < sccs.length; i++) {
    print("SCC ${i + 1}: ${sccs[i]}");
  }
}

List<List<int>> kosarajuSCC(Map<int, List<int>> graph) {
  Set<int> visited = {};
  List<int> stack = [];

  // 1. DFS لإيجاد ترتيب العقد (عند الانتهاء من زيارة العقدة نضيفها للمكدس)
  for (int node in graph.keys) {
    if (!visited.contains(node)) {
      dfs1(node, graph, visited, stack);
    }
  }

  // 2. عكس الرسم البياني
  Map<int, List<int>> reversedGraph = reverseGraph(graph);

  visited.clear();
  List<List<int>> sccs = [];

  // 3. استخدام الترتيب من المكدس لزيارة العقد في الرسم المعكوس
  while (stack.isNotEmpty) {
    int node = stack.removeLast();
    if (!visited.contains(node)) {
      List<int> component = [];
      dfs2(node, reversedGraph, visited, component);
      sccs.add(component);
    }
  }

  return sccs;
}

// DFS للترتيب (الخطوة 1)
void dfs1(int node, Map<int, List<int>> graph, Set<int> visited, List<int> stack) {
  visited.add(node);

  for (int neighbor in graph[node] ?? []) {
    if (!visited.contains(neighbor)) {
      dfs1(neighbor, graph, visited, stack);
    }
  }

  stack.add(node);
}

// عكس الرسم البياني (الخطوة 2)
Map<int, List<int>> reverseGraph(Map<int, List<int>> graph) {
  Map<int, List<int>> reversed = {};

  for (int node in graph.keys) {
    for (int neighbor in graph[node]!) {
      reversed.putIfAbsent(neighbor, () => []).add(node);
    }
    reversed.putIfAbsent(node, () => []);
  }

  return reversed;
}

// DFS في الرسم المعكوس (الخطوة 3)
void dfs2(int node, Map<int, List<int>> graph, Set<int> visited, List<int> component) {
  visited.add(node);
  component.add(node);

  for (int neighbor in graph[node] ?? []) {
    if (!visited.contains(neighbor)) {
      dfs2(neighbor, graph, visited, component);
    }
  }
}

```

---

## 🧪 مخرجات التجربة:

```
yaml
نسختحرير
المكونات المتصلة بقوة (SCC):
SCC 1: [4]
SCC 2: [3]
SCC 3: [0, 2, 1]

```

---

## 🔍 شرح تفصيلي:

| الخطوة | الوصف | الكود أو التعليق |
| --- | --- | --- |
| 1 | DFS للترتيب وتخزين العقد بعد الزيارة | `dfs1` + `stack.add(node)` |
| 2 | عكس اتجاهات الحواف | `reverseGraph` |
| 3 | DFS في الرسم المعكوس حسب الترتيب | `dfs2` مع تجميع العقد في `component` |

---

## ملاحظات:

- خوارزمية Kosaraju تعمل في زمن O(V + E).
- مهمة جداً في تحليل الرسوم الموجهة، التفكيك لمكونات قوية، وتحليل الشبكات.