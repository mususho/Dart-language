# Cycle Detection

# 🧠 ما هي مشكلة اكتشاف الدورات (Cycle Detection)؟

> هدفنا هو التحقق مما إذا كان هناك دورة (Cycle) في الرسم البياني، أي مسار يبدأ وينتهي عند نفس العقدة.
> 

> تختلف طريقة الكشف حسب نوع الرسم:
> 
- **رسم بياني غير موجه (Undirected Graph)**
- **رسم بياني موجه (Directed Graph)**

---

# 1. Cycle Detection في رسم غير موجه (Undirected Graph)

---

## 🪜 خطوات الحل (باستخدام DFS):

### ✅ الخطوة 1: زيارة العقدة، مع تتبع الأب (Parent) لها

### ✅ الخطوة 2: إذا وجدنا جاراً زُرنا سابقاً ولكنه ليس الأب، إذن هناك دورة

---

## 📦 كود Dart للكشف عن دورة في رسم غير موجه:

```dart
dart
نسختحرير
void main() {
  Map<int, List<int>> graph = {
    0: [1, 2],
    1: [0, 3],
    2: [0],
    3: [1, 4],
    4: [3],
  };

  bool hasCycle = hasCycleUndirected(graph);
  print("هل الرسم يحتوي على دورة؟ $hasCycle");
}

bool hasCycleUndirected(Map<int, List<int>> graph) {
  Set<int> visited = {};

  for (int node in graph.keys) {
    if (!visited.contains(node)) {
      if (dfsCycleUndirected(node, -1, graph, visited)) {
        return true;
      }
    }
  }
  return false;
}

bool dfsCycleUndirected(int node, int parent, Map<int, List<int>> graph, Set<int> visited) {
  visited.add(node);

  for (int neighbor in graph[node] ?? []) {
    if (!visited.contains(neighbor)) {
      if (dfsCycleUndirected(neighbor, node, graph, visited)) {
        return true;
      }
    } else if (neighbor != parent) {
      // وجدنا جار مزور سابقاً وهو ليس الأب => دورة
      return true;
    }
  }
  return false;
}

```

---

# 2. Cycle Detection في رسم موجه (Directed Graph)

---

## 🪜 خطوات الحل (باستخدام DFS مع تتبع الحالة):

- نستخدم ثلاث حالات للعقد:
    - **غير مزارة (0)**
    - **قيد المعالجة (1)** (داخل مسار الاستدعاء الحالي)
    - **تمت معالجتها (2)**
- إذا وصلنا لعقدة بحالة **قيد المعالجة** خلال الزيارة، فهذا يعني وجود دورة.

---

## 📦 كود Dart للكشف عن دورة في رسم موجه:

```dart
dart
نسختحرير
void main() {
  Map<String, List<String>> graph = {
    'A': ['B'],
    'B': ['C'],
    'C': ['A'], // دورة A->B->C->A
    'D': ['E'],
    'E': [],
  };

  bool hasCycle = hasCycleDirected(graph);
  print("هل الرسم الموجه يحتوي على دورة؟ $hasCycle");
}

bool hasCycleDirected(Map<String, List<String>> graph) {
  Map<String, int> state = {}; // 0: unvisited, 1: visiting, 2: visited

  for (String node in graph.keys) {
    if (state[node] == null) {
      if (dfsCycleDirected(node, graph, state)) {
        return true;
      }
    }
  }
  return false;
}

bool dfsCycleDirected(String node, Map<String, List<String>> graph, Map<String, int> state) {
  state[node] = 1; // قيد المعالجة

  for (String neighbor in graph[node] ?? []) {
    if (state[neighbor] == 1) {
      // وجدنا عقدة قيد المعالجة => دورة
      return true;
    }
    if (state[neighbor] == null && dfsCycleDirected(neighbor, graph, state)) {
      return true;
    }
  }

  state[node] = 2; // تم المعالجة
  return false;
}

```

---

## 🧪 مخرجات التجربة:

```
arduino
نسختحرير
هل الرسم يحتوي على دورة؟ false
هل الرسم الموجه يحتوي على دورة؟ true

```

---

## 🔍 شرح تفصيلي:

| الحالة | التفسير |
| --- | --- |
| غير مزارة (0) | لم تُزر العقدة بعد |
| قيد المعالجة (1) | العقدة ضمن مسار الاستدعاء الحالي |
| تمت معالجتها (2) | انتهى استكشاف العقدة وجيرانها |

---

## ملخص:

| النوع | الخوارزمية | التعقيد الزمني |
| --- | --- | --- |
| غير موجه | DFS مع تتبع الأب | O(V + E) |
| موجه | DFS مع تتبع الحالة | O(V + E) |