# Shortest Path in Grid

## 🚀 Shortest Path in Grid

**(أقصر مسار من نقطة بداية إلى نقطة نهاية في شبكة 2D، مع حواجز)**

---

## 🎯 الهدف:

> لديك مصفوفة grid بحجم N x M تحتوي:
> 
> - `0` لخانة مفتوحة (يمكن السير فيها)
> - `1` لخانة حائط أو عائق (لا يمكن المرور منها)
>     
>     مطلوب إيجاد أقصر مسار (أقل عدد خطوات) من نقطة البداية `(startX, startY)` إلى نقطة النهاية `(endX, endY)`،
>     
>     مع التحرك في 4 اتجاهات (أعلى، أسفل، يمين، يسار).
>     

---

## 🧠 الفكرة (BFS):

- نستخدم **بحث العرض (Breadth-First Search - BFS)** لأنه يضمن إيجاد أقصر مسار في شبكة غير موجهة بدون أوزان.
- نبدأ من نقطة البداية، نضيفها إلى طابور.
- نكرر زيارة الخانات المجاورة المفتوحة وغير المزارة.
- نحتفظ بمصفوفة `distance` لتسجيل المسافة من البداية لكل خانة.
- عندما نصل للنهاية نعيد المسافة.

---

## ✅ كود Dart كامل مع الشرح:

```dart
dart
نسختحرير
import 'dart:collection';

int shortestPath(List<List<int>> grid, int startX, int startY, int endX, int endY) {
  int n = grid.length;
  int m = grid[0].length;

  if (grid[startX][startY] == 1 || grid[endX][endY] == 1) return -1; // لا مسار ممكن

  List<List<bool>> visited = List.generate(n, (_) => List.filled(m, false));
  List<List<int>> distance = List.generate(n, (_) => List.filled(m, -1));

  Queue<List<int>> queue = Queue();

  // بدء البحث
  queue.add([startX, startY]);
  visited[startX][startY] = true;
  distance[startX][startY] = 0;

  List<List<int>> directions = [
    [1, 0],  // أسفل
    [-1, 0], // أعلى
    [0, 1],  // يمين
    [0, -1]  // يسار
  ];

  while (queue.isNotEmpty) {
    var cell = queue.removeFirst();
    int x = cell[0], y = cell[1];

    if (x == endX && y == endY) {
      return distance[x][y]; // وصلنا للنهاية
    }

    for (var dir in directions) {
      int newX = x + dir[0];
      int newY = y + dir[1];

      // تحقق من الحدود، عدم وجود حائط، وعدم زيارة الخانة مسبقًا
      if (newX >= 0 && newX < n && newY >= 0 && newY < m &&
          grid[newX][newY] == 0 && !visited[newX][newY]) {
        visited[newX][newY] = true;
        distance[newX][newY] = distance[x][y] + 1;
        queue.add([newX, newY]);
      }
    }
  }

  return -1; // لا يوجد مسار للنهاية
}

```

---

## 🧪 تجربة:

```dart
dart
نسختحرير
void main() {
  List<List<int>> grid = [
    [0, 0, 1, 0],
    [1, 0, 1, 0],
    [0, 0, 0, 0],
    [0, 1, 1, 0],
  ];

  int startX = 0, startY = 0;
  int endX = 3, endY = 3;

  int dist = shortestPath(grid, startX, startY, endX, endY);

  if (dist != -1) {
    print("🚀 أقصر مسار يحتوي $dist خطوة");
  } else {
    print("لا يوجد مسار ممكن");
  }
}

```

---

## ✅ الناتج المتوقع:

```
نسختحرير
🚀 أقصر مسار يحتوي 7 خطوة

```

---

## 📦 التحليل:

| الخاصية | القيمة |
| --- | --- |
| الزمن | O(N * M) حيث N، M أبعاد الشبكة |
| الذاكرة | O(N * M) |
| النوع | BFS |