# Rat in a Maze

## 🐀 Rat in a Maze

**(حل متاهة - إيجاد مسار من البداية للنهاية)**

---

## 🎯 الهدف:

> لديك مصفوفة maze ثنائية الأبعاد بحجم N x N،
> 
> 
> حيث `1` يعني مسار مفتوح، و`0` يعني جدار أو عائق،
> 
> المطلوب: إيجاد مسار من الزاوية العلوية اليسرى `(0,0)` إلى الزاوية السفلية اليمنى `(N-1, N-1)`،
> 
> يتحرك الجرذ لأعلى، أسفل، يسار، يمين دون الخروج عن حدود المصفوفة.
> 

---

## 🧠 الفكرة (Backtracking):

- نبدأ من `(0,0)` ونحاول التنقل إلى الخانات المجاورة المفتوحة.
- نستخدم مصفوفة `visited` لتجنب زيارة نفس الخانة أكثر من مرة.
- إذا وصلنا للنهاية، نحتفظ بالمسار.
- إذا لم نجد، نتراجع ونحاول مسار آخر.

---

## ✅ الكود الكامل في Dart:

```dart
dart
نسختحرير
bool isSafe(List<List<int>> maze, List<List<bool>> visited, int x, int y, int n) {
  return (x >= 0 && x < n && y >= 0 && y < n && maze[x][y] == 1 && !visited[x][y]);
}

bool solveMazeUtil(List<List<int>> maze, List<List<bool>> visited, int x, int y, int n, List<List<int>> path) {
  if (x == n - 1 && y == n - 1) {
    path.add([x, y]);
    return true;
  }

  if (isSafe(maze, visited, x, y, n)) {
    visited[x][y] = true;
    path.add([x, y]);

    // الاتجاهات: أسفل، يمين، أعلى، يسار
    List<List<int>> moves = [[1, 0], [0, 1], [-1, 0], [0, -1]];

    for (var move in moves) {
      int nextX = x + move[0];
      int nextY = y + move[1];

      if (solveMazeUtil(maze, visited, nextX, nextY, n, path)) {
        return true;
      }
    }

    // تراجع
    path.removeLast();
    visited[x][y] = false;
  }

  return false;
}

List<List<int>> solveMaze(List<List<int>> maze) {
  int n = maze.length;
  List<List<bool>> visited = List.generate(n, (_) => List.filled(n, false));
  List<List<int>> path = [];

  if (solveMazeUtil(maze, visited, 0, 0, n, path)) {
    return path;
  } else {
    return [];
  }
}

```

---

## 🧪 تجربة:

```dart
dart
نسختحرير
void main() {
  List<List<int>> maze = [
    [1, 0, 0, 0],
    [1, 1, 0, 1],
    [0, 1, 0, 0],
    [1, 1, 1, 1],
  ];

  List<List<int>> path = solveMaze(maze);

  if (path.isNotEmpty) {
    print("🐀 مسار الجرذ:");
    for (var step in path) {
      print("(${step[0]}, ${step[1]})");
    }
  } else {
    print("لا يوجد مسار");
  }
}

```

---

## ✅ الناتج المتوقع:

```
نسختحرير
🐀 مسار الجرذ:
(0, 0)
(1, 0)
(1, 1)
(2, 1)
(3, 1)
(3, 2)
(3, 3)

```

---

## 📦 التحليل:

| الخاصية | القيمة |
| --- | --- |
| الزمن | Exponential (يعتمد على حجم المتاهة) |
| الذاكرة | O(N²) |
| النوع | Backtracking |