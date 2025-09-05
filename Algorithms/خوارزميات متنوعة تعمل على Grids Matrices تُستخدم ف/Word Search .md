# Word Search

## 🔍 Word Search

**(البحث عن كلمة في شبكة 2D من الحروف)**

---

### 🎯 الهدف:

لدينا شبكة أحرف `board` ثنائية الأبعاد، ونريد أن نتحقق إذا كانت كلمة `word` موجودة في هذه الشبكة من خلال التحرك لأعلى، أسفل، يمين، ويسار، مع عدم استخدام نفس الخانة مرتين في نفس البحث.

---

### 🧠 الفكرة:

- نبحث بدايةً في كل خلية من الشبكة.
- إذا الحرف الحالي يطابق أول حرف من الكلمة، نبدأ بحث عميق (DFS) من هذه الخانة.
- في البحث العميق، ننتقل إلى الخلايا المجاورة التي لم تُزر مسبقًا ونتحقق من الحرف التالي.
- نستخدم مصفوفة `visited` لمنع العودة إلى نفس الخانة أثناء البحث.
- إذا استطعنا إيجاد الكلمة بالكامل نرجع `true`.

---

### ✅ كود Dart مفصل مع تعليقات:

```dart
dart
نسختحرير
bool exist(List<List<String>> board, String word) {
  int rows = board.length;
  int cols = board[0].length;

  // مصفوفة لتتبع الخانات التي تم زيارتها
  List<List<bool>> visited = List.generate(rows, (_) => List.filled(cols, false));

  // دالة البحث العميق (DFS)
  bool dfs(int row, int col, int index) {
    // إذا وصلنا لنهاية الكلمة، هذا يعني أننا وجدنا الكلمة بالكامل
    if (index == word.length) return true;

    // تحقق من الحدود ومطابقة الحرف وزيارة الخانة
    if (row < 0 || row >= rows || col < 0 || col >= cols) return false;
    if (visited[row][col]) return false;
    if (board[row][col] != word[index]) return false;

    // تعليم الخانة على أنها زارت
    visited[row][col] = true;

    // بحث في الخانات المجاورة (أسفل، أعلى، يمين، يسار)
    bool found = dfs(row + 1, col, index + 1) ||
                 dfs(row - 1, col, index + 1) ||
                 dfs(row, col + 1, index + 1) ||
                 dfs(row, col - 1, index + 1);

    // تراجع: إعادة تعيين حالة الزيارة لتجربة مسارات أخرى
    visited[row][col] = false;

    return found;
  }

  // تفحص كل خلية كبداية محتملة للكلمة
  for (int i = 0; i < rows; i++) {
    for (int j = 0; j < cols; j++) {
      if (board[i][j] == word[0]) {
        if (dfs(i, j, 0)) return true;
      }
    }
  }

  // إذا لم نجد الكلمة في أي مكان
  return false;
}

```

---

### 🧪 مثال تجربة:

```dart
dart
نسختحرير
void main() {
  List<List<String>> board = [
    ['A','B','C','E'],
    ['S','F','C','S'],
    ['A','D','E','E']
  ];

  print(exist(board, "ABCCED")); // true
  print(exist(board, "SEE"));    // true
  print(exist(board, "ABCB"));   // false
}

```

---

### ✅ ناتج التجربة:

```
arduino
نسختحرير
true
true
false

```

---

### 📦 التحليل:

| الخاصية | القيمة |
| --- | --- |
| الزمن | O(N * 3^L) حيث N = عدد الخانات، L = طول الكلمة |
| الذاكرة | O(N) (للمصفوفة visited ومكدس الاستدعاءات) |

---