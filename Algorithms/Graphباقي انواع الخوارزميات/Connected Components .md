# Connected Components

## 🧠 ما هي Connected Components؟

> في رسم بياني غير موجه (Undirected Graph)، Connected Components هي المجموعات الفرعية من العقد حيث كل عقدة في المجموعة مرتبطة بالعقد الأخرى ضمن نفس المجموعة عن طريق مسار.
> 

> بمعنى آخر: تقسيم الرسم البياني إلى أقسام حيث كل قسم "متصل داخليًا".
> 

---

## 🪜 خطوات الحل (باستخدام DFS أو BFS):

### ✅ الخطوة 1: تهيئة مجموعة `visited` لتتبع العقد التي تمت زيارتها

### ✅ الخطوة 2: المرور على كل عقدة في الرسم

### ✅ الخطوة 3: إذا لم تُزر العقدة، نبدأ استكشاف **DFS** أو **BFS** منها لتجميع كل العقد المتصلة معها

### ✅ الخطوة 4: جمع كل مجموعة كـ connected component

---

## 📦 كود Dart كامل مع شرح وتفصيل:

```dart
dart
نسختحرير
void main() {
  Map<int, List<int>> graph = {
    0: [1, 2],
    1: [0],
    2: [0],
    3: [4],
    4: [3],
    5: [],
  };

  List<Set<int>> components = connectedComponents(graph);

  print("مجموعات العقد المتصلة:");
  for (int i = 0; i < components.length; i++) {
    print("Component ${i + 1}: ${components[i]}");
  }
}

/// دالة لحساب connected components باستخدام DFS
List<Set<int>> connectedComponents(Map<int, List<int>> graph) {
  Set<int> visited = {};
  List<Set<int>> components = [];

  for (int node in graph.keys) {
    if (!visited.contains(node)) {
      Set<int> component = {};
      dfs(node, graph, visited, component);
      components.add(component);
    }
  }

  return components;
}

/// دالة DFS لزيارة كل العقد المتصلة
void dfs(int node, Map<int, List<int>> graph, Set<int> visited, Set<int> component) {
  visited.add(node);
  component.add(node);

  for (int neighbor in graph[node] ?? []) {
    if (!visited.contains(neighbor)) {
      dfs(neighbor, graph, visited, component);
    }
  }
}

```

---

## 🧪 مخرجات التجربة:

```
css
نسختحرير
مجموعات العقد المتصلة:
Component 1: {0, 1, 2}
Component 2: {3, 4}
Component 3: {5}

```

---

## 🔍 شرح تفصيلي:

| الخطوة | الوصف | الكود أو التعليق |
| --- | --- | --- |
| 1 | تهيئة visited ومصفوفة components | `Set<int> visited = {}; List<Set<int>> components = [];` |
| 2 | المرور على كل عقدة لم تبدأ بزيارتها | `for (int node in graph.keys)` |
| 3 | استدعاء DFS لتجميع العقد المتصلة | `dfs(node, graph, visited, component)` |
| 4 | إضافة المجموعة المجمعة إلى القائمة | `components.add(component);` |

---

## ملاحظات:

- يمكن تطبيق نفس الفكرة باستخدام BFS بدل DFS.
- هذه الخوارزمية تستخدم فقط في الرسوم غير الموجهة (Undirected).
- لرسم موجه يمكن استخدام خوارزمية **Strongly Connected Components** (مثل Kosaraju أو Tarjan).