# Surrounded Regions

أكيد! سأشرح لك خوارزمية **Surrounded Regions** بالتفصيل مع كود Dart.

---

## 🌊 Surrounded Regions

**(تبديل مناطق محاطة بالكامل في مصفوفة 2D)**

---

### 🎯 الهدف:

> لديك مصفوفة 2D من الحروف board تحتوي فقط على 'X' و 'O'،
> 
> 
> المطلوب:
> 
> تبديل كل `'O'` التي **محاطة بالكامل بـ 'X'** إلى `'X'`،
> 
> بينما `'O'` التي ترتبط بحواف المصفوفة تبقى كما هي.
> 

---

### 🧠 الفكرة:

- أي `'O'` على الحواف أو متصل بها (عن طريق `'O'` آخر) **لا يتم تحويلها**.
- نحدد جميع `'O'` المرتبطة بالحواف (نستخدم DFS أو BFS).
- نعلم هذه الخانات مؤقتًا (مثلاً بعلامة `'#'`).
- في النهاية:
    - نبدل كل `'O'` غير المعلمة إلى `'X'`.
    - نعيد كل `'#'` إلى `'O'`.

---

### ✅ كود Dart مع تعليقات:

```dart
dart
نسختحرير
void solveSurroundedRegions(List<List<String>> board) {
  int rows = board.length;
  if (rows == 0) return;
  int cols = board[0].length;

  void dfs(int r, int c) {
    if (r < 0 || r >= rows || c < 0 || c >= cols) return;
    if (board[r][c] != 'O') return;

    board[r][c] = '#'; // تعليم الخانة لتجنب التبديل

    dfs(r + 1, c);
    dfs(r - 1, c);
    dfs(r, c + 1);
    dfs(r, c - 1);
  }

  // 1. نعلم كل 'O' المرتبطة بالحواف
  for (int r = 0; r < rows; r++) {
    if (board[r][0] == 'O') dfs(r, 0);
    if (board[r][cols - 1] == 'O') dfs(r, cols - 1);
  }
  for (int c = 0; c < cols; c++) {
    if (board[0][c] == 'O') dfs(0, c);
    if (board[rows - 1][c] == 'O') dfs(rows - 1, c);
  }

  // 2. تبديل 'O' إلى 'X'، و '#' إلى 'O'
  for (int r = 0; r < rows; r++) {
    for (int c = 0; c < cols; c++) {
      if (board[r][c] == 'O') {
        board[r][c] = 'X';
      } else if (board[r][c] == '#') {
        board[r][c] = 'O';
      }
    }
  }
}

```

---

### 🧪 تجربة:

```dart
dart
نسختحرير
void main() {
  List<List<String>> board = [
    ['X', 'X', 'X', 'X'],
    ['X', 'O', 'O', 'X'],
    ['X', 'X', 'O', 'X'],
    ['X', 'O', 'X', 'X'],
  ];

  solveSurroundedRegions(board);

  print("🌊 المصفوفة بعد المعالجة:");
  for (var row in board) {
    print(row);
  }
}

```

---

### ✅ الناتج المتوقع:

```
csharp
نسختحرير
🌊 المصفوفة بعد المعالجة:
[X, X, X, X]
[X, X, X, X]
[X, X, X, X]
[X, O, X, X]

```

---

### 📦 التحليل:

| الخاصية | القيمة |
| --- | --- |
| الزمن | O(N * M) |
| الذاكرة | O(N * M) (لمكدس الاستدعاءات DFS) |