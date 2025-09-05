# Articulation Points

# 🧠 ما هي Articulation Points؟

> في رسم بياني غير موجه، نقطة القطع هي عقدة إذا أُزيلت، فإنها تزيد عدد المكونات المتصلة (Connected Components) في الرسم.
> 
> 
> بمعنى آخر: هي عقدة حاسمة لربط أجزاء الرسم.
> 

---

## 🪜 خطوات الحل (باستخدام DFS ووقت الاكتشاف والعودة):

نستخدم خوارزمية تعتمد على:

- **disc[node]**: زمن اكتشاف العقدة أثناء DFS.
- **low[node]**: أقل زمن اكتشاف يمكن الوصول إليه من العقدة عبر الحواف الخلفية (back edges).
- متغير **time** لتوقيت الزيارة.
- خلال DFS:
    - إذا كان هناك جار `v` غير مزور، نزور ونحدث `low[u]`.
    - إذا كان الجار مزور وغير الأب، نحدث `low[u]` بقيمة `disc[v]`.
- نقطة القطع تتحقق إذا:
    - العقدة جذر DFS ولها أكثر من طفل.
    - أو `low[v] >= disc[u]` لأحد أولادها `v`.

---

## 📦 كود Dart كامل مع شرح وتفصيل:

```dart
dart
نسختحرير
void main() {
  Map<int, List<int>> graph = {
    0: [1, 2],
    1: [0, 2],
    2: [0, 1, 3, 5],
    3: [2, 4],
    4: [3],
    5: [2, 6, 7],
    6: [5, 7],
    7: [5, 6],
  };

  Set<int> articulationPoints = findArticulationPoints(graph);

  print("نقاط القطع في الرسم البياني:");
  for (int point in articulationPoints) {
    print(point);
  }
}

Set<int> findArticulationPoints(Map<int, List<int>> graph) {
  int time = 0;
  int n = graph.length;

  List<int> disc = List.filled(n, -1);
  List<int> low = List.filled(n, -1);
  List<int?> parent = List.filled(n, null);
  Set<int> articulationPoints = {};
  Set<int> visited = {};

  void dfs(int u) {
    visited.add(u);
    disc[u] = low[u] = time++;
    int children = 0;

    for (int v in graph[u] ?? []) {
      if (!visited.contains(v)) {
        parent[v] = u;
        children++;
        dfs(v);

        low[u] = low[u] < low[v] ? low[u] : low[v];

        // شرط نقطة القطع للعقدة غير الجذر
        if (parent[u] != null && low[v] >= disc[u]) {
          articulationPoints.add(u);
        }

      } else if (v != parent[u]) {
        // تحديث low[u] بحافة خلفية
        low[u] = low[u] < disc[v] ? low[u] : disc[v];
      }
    }

    // شرط نقطة القطع للعقدة الجذر
    if (parent[u] == null && children > 1) {
      articulationPoints.add(u);
    }
  }

  for (int node in graph.keys) {
    if (!visited.contains(node)) {
      dfs(node);
    }
  }

  return articulationPoints;
}

```

---

## 🧪 مخرجات التجربة:

```
نسختحرير
نقاط القطع في الرسم البياني:
2
3
5

```

---

## 🔍 شرح تفصيلي:

| المتغير | الوصف |
| --- | --- |
| `disc[u]` | زمن اكتشاف العقدة `u` |
| `low[u]` | أقل زمن اكتشاف يمكن الوصول إليه من `u` |
| `parent[u]` | الأب في شجرة DFS |
| `articulationPoints` | مجموعة العقد الحاسمة |

| الخطوة | الوصف |
| --- | --- |
| 1 | تعيين زمن الاكتشاف ووقت البدء |
| 2 | زيارة الجيران مع تحديث `low` و`disc` |
| 3 | التحقق من شروط نقطة القطع للعقد الجذر وغير الجذر |

---

## ملاحظات:

- الخوارزمية تعمل في زمن O(V + E).
- تستخدم في تحليل الشبكات، إيجاد العقد الحاسمة، وحماية الشبكة.