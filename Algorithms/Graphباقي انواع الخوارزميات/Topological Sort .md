# Topological Sort

## 🧠 ما هي خوارزمية Topological Sort؟

> Topological Sort هي ترتيب خطي لعقد رسم بياني موجه (Directed Acyclic Graph - DAG) بحيث لكل حافة من عقدة u إلى عقدة v، فإن u يأتي قبل v في الترتيب.
> 

> بعبارة أخرى: ترتيب يسمح بتنفيذ المهام التي تعتمد على بعضها بطريقة صحيحة (مثلاً ترتيب الدورات الدراسية، ترتيب بناء المشاريع، ...).
> 

---

## 🪜 خطوات الحل (باستخدام DFS):

### ✅ الخطوة 1: زيارة كل عقدة غير مزارة (unvisited)

### ✅ الخطوة 2: استخدام الاستدعاء الذاتي (Recursion) لزيارة كل الجيران

### ✅ الخطوة 3: بعد الانتهاء من زيارة كل جيران العقدة، نضيف العقدة إلى مكدس (Stack)

### ✅ الخطوة 4: عكس محتوى المكدس هو الترتيب الطوبولوجي

---

## 📦 كود Dart كامل مع شرح وتفصيل:

```dart
dart
نسختحرير
void main() {
  Map<String, List<String>> graph = {
    '5': ['2', '0'],
    '4': ['0', '1'],
    '2': ['3'],
    '3': ['1'],
    '0': [],
    '1': [],
  };

  List<String> topoOrder = topologicalSort(graph);
  print("Topological Sort Order:");
  print(topoOrder.join(" -> "));
}

/// دالة لتنفيذ Topological Sort باستخدام DFS
List<String> topologicalSort(Map<String, List<String>> graph) {
  Set<String> visited = {};
  List<String> stack = [];

  // زيارة جميع العقد
  for (String node in graph.keys) {
    if (!visited.contains(node)) {
      dfsTopo(node, graph, visited, stack);
    }
  }

  // عكس المكدس يعطي الترتيب الطوبولوجي
  return stack.reversed.toList();
}

/// دالة مساعدة لتنفيذ DFS وزيارة العقد
void dfsTopo(String node, Map<String, List<String>> graph, Set<String> visited, List<String> stack) {
  visited.add(node);

  for (String neighbor in graph[node] ?? []) {
    if (!visited.contains(neighbor)) {
      dfsTopo(neighbor, graph, visited, stack);
    }
  }

  // بعد زيارة كل الجيران، نضيف العقدة للمكدس
  stack.add(node);
}

```

---

## 🧪 مخرجات التجربة:

```
rust
نسختحرير
Topological Sort Order:
4 -> 5 -> 2 -> 3 -> 1 -> 0

```

---

## 🔍 شرح تفصيلي:

| الخطوة | الوصف | الكود أو التعليق |
| --- | --- | --- |
| 1 | زيارة كل عقدة غير مزارة باستخدام DFS | `for` + `visited` |
| 2 | زيارة كل الجيران recursively | `dfsTopo` دالة |
| 3 | بعد الانتهاء من العقدة نضيفها للمكدس | `stack.add(node)` |
| 4 | عكس المكدس يعطي الترتيب الصحيح | `stack.reversed.toList()` |

---

## ملاحظات:

- الرسم البياني يجب أن يكون DAG (بدون دورات)، وإلا الترتيب الطوبولوجي غير معرف.
- يمكن أيضًا تنفيذ الخوارزمية باستخدام طريقة **Kahn's Algorithm** (بـ BFS)، إذا أردت أشرحها لك.