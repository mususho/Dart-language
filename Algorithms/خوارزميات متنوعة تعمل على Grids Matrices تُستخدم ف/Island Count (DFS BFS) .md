# Island Count (DFS/BFS)

## 🏝️ Island Count

**(عدد الجزر في مصفوفة ثنائية الأبعاد باستخدام DFS أو BFS)**

---

## 🎯 الهدف:

> لديك مصفوفة grid من 0 و1 حيث:
> 
> - `1` تمثل أرض (جزيرة)
> - `0` تمثل ماء
>     
>     المطلوب: حساب عدد الجزر (مجموعات الخانات المتصلة أفقيًا أو عموديًا).
>     

---

## 🧠 الفكرة:

- نتفحص كل خانة في المصفوفة.
- إذا وجدنا `1` ولم تُزر بعد، نبدأ بحث (DFS أو BFS) لتعليم كل الخانات المتصلة بها (جزء من نفس الجزيرة).
- نزيد عدد الجزر بواحد لكل بحث جديد.
- نستخدم مصفوفة `visited` أو نغير القيمة لتجنب العد المكرر.

---

## ✅ كود Dart باستخدام DFS:

```dart
dart
نسختحرير
void dfs(List<List<int>> grid, int r, int c, int rows, int cols) {
  if (r < 0 || c < 0 || r >= rows || c >= cols || grid[r][c] == 0) return;

  grid[r][c] = 0; // تعليم الزيارة بتغيير القيمة

  dfs(grid, r + 1, c, rows, cols);
  dfs(grid, r - 1, c, rows, cols);
  dfs(grid, r, c + 1, rows, cols);
  dfs(grid, r, c - 1, rows, cols);
}

int numIslands(List<List<int>> grid) {
  int rows = grid.length;
  int cols = grid[0].length;
  int count = 0;

  for (int r = 0; r < rows; r++) {
    for (int c = 0; c < cols; c++) {
      if (grid[r][c] == 1) {
        count++;
        dfs(grid, r, c, rows, cols);
      }
    }
  }

  return count;
}

```

---

## 🧪 تجربة:

```dart
dart
نسختحرير
void main() {
  List<List<int>> grid = [
    [1, 1, 0, 0, 0],
    [1, 1, 0, 0, 0],
    [0, 0, 1, 0, 0],
    [0, 0, 0, 1, 1],
  ];

  print("🏝️ عدد الجزر = ${numIslands(grid)}");
}

```

---

## ✅ الناتج المتوقع:

```
نسختحرير
🏝️ عدد الجزر = 3

```

---

## بديل باستخدام BFS:

```dart
dart
نسختحرير
import 'dart:collection';

void bfs(List<List<int>> grid, int r, int c, int rows, int cols) {
  Queue<List<int>> queue = Queue();
  queue.add([r, c]);
  grid[r][c] = 0;

  List<List<int>> directions = [
    [1, 0],
    [-1, 0],
    [0, 1],
    [0, -1]
  ];

  while (queue.isNotEmpty) {
    var cell = queue.removeFirst();
    int row = cell[0], col = cell[1];

    for (var dir in directions) {
      int newRow = row + dir[0];
      int newCol = col + dir[1];

      if (newRow >= 0 && newRow < rows && newCol >= 0 && newCol < cols && grid[newRow][newCol] == 1) {
        grid[newRow][newCol] = 0;
        queue.add([newRow, newCol]);
      }
    }
  }
}

```

---

## 📦 التحليل:

| الخاصية | القيمة |
| --- | --- |
| الزمن | O(N * M) حيث N، M أبعاد المصفوفة |
| الذاكرة | O(N * M) في أسوأ الحالات |
| النوع | DFS أو BFS |