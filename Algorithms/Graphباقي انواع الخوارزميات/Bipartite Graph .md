# Bipartite Graph

# 🧠 ما هو الرسم البياني الثنائي (Bipartite Graph)؟

> رسم بياني ثنائي هو رسم بياني يمكن تقسيم عقده إلى مجموعتين بحيث لا توجد حافة تربط عقدتين من نفس المجموعة.
> 

> ببساطة: يمكن تلوين كل عقدة بأحد لونين فقط بحيث لا تتصل عقدتان بنفس اللون.
> 

---

# 🪜 خطوات التحقق إذا كان الرسم ثنائي (باستخدام BFS أو DFS):

### ✅ الخطوة 1: نستخدم مصفوفة أو خريطة `color` لتخزين لون كل عقدة (0 أو 1)

### ✅ الخطوة 2: نبدأ من عقدة غير ملونة، ونعطيها لون (مثلاً 0)

### ✅ الخطوة 3: نزور الجيران، نعطيهم اللون المعاكس

### ✅ الخطوة 4: إذا وجدنا جار له نفس اللون، فالرسم غير ثنائي

---

## 📦 كود Dart كامل مع شرح وتفصيل:

```dart
dart
نسختحرير
void main() {
  Map<int, List<int>> graph = {
    0: [1, 3],
    1: [0, 2],
    2: [1, 3],
    3: [0, 2],
  };

  bool result = isBipartite(graph);
  print("هل الرسم ثنائي؟ $result");

  // مثال آخر غير ثنائي
  Map<int, List<int>> graph2 = {
    0: [1, 2],
    1: [0, 2],
    2: [0, 1],
  };

  print("هل الرسم الثاني ثنائي؟ ${isBipartite(graph2)}");
}

/// دالة لفحص إذا كان الرسم ثنائي باستخدام BFS
bool isBipartite(Map<int, List<int>> graph) {
  Map<int, int> color = {}; // لون كل عقدة: 0 أو 1

  for (int node in graph.keys) {
    if (!color.containsKey(node)) {
      if (!bfsCheck(node, graph, color)) {
        return false;
      }
    }
  }

  return true;
}

/// BFS لتلوين العقد والتحقق
bool bfsCheck(int start, Map<int, List<int>> graph, Map<int, int> color) {
  List<int> queue = [start];
  color[start] = 0;

  while (queue.isNotEmpty) {
    int node = queue.removeAt(0);
    int currentColor = color[node]!;

    for (int neighbor in graph[node] ?? []) {
      if (!color.containsKey(neighbor)) {
        color[neighbor] = 1 - currentColor; // اللون المعاكس
        queue.add(neighbor);
      } else if (color[neighbor] == currentColor) {
        // وجدنا جار له نفس اللون => غير ثنائي
        return false;
      }
    }
  }

  return true;
}

```

---

## 🧪 مخرجات التجربة:

```
arduino
نسختحرير
هل الرسم ثنائي؟ true
هل الرسم الثاني ثنائي؟ false

```

---

## 🔍 شرح تفصيلي:

| الخطوة | الوصف | الكود أو التعليق |
| --- | --- | --- |
| 1 | تعيين لون للعقدة الأولى | `color[start] = 0` |
| 2 | زيارة الجيران وتلوينهم باللون المعاكس | `color[neighbor] = 1 - currentColor` |
| 3 | التحقق من عدم وجود جيران بنفس اللون | شرط `color[neighbor] == currentColor` |
| 4 | تكرار الخطوات لكل عقدة غير ملونة | في الحلقة الرئيسية |

---

## ملاحظات:

- الخوارزمية تعمل على الرسوم غير الموجهة.
- يمكن تعديل الكود لاستخدام DFS بدل BFS حسب الحاجة.
- تستخدم في التحقق من خصائص الرسوم، تقسيمات المشاكل، وألعاب الألوان.