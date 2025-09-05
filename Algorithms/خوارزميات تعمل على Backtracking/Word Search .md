# Word Search

## 🔍 Word Search

**(البحث عن كلمة داخل شبكة حروف 2D)**

---

## 🎯 الهدف:

> إعطاء شبكة حروف 2D (مثل لوحة من الأحرف) وكلمة word،
> 
> 
> نريد التحقق إذا يمكن إيجاد الكلمة عبر تحركات متتالية متجاورة (أعلى، أسفل، يسار، يمين) بحيث لا يُعاد استخدام نفس الخانة.
> 

---

## 🧠 الفكرة (Backtracking + DFS):

- نتصفح كل خانة في الشبكة.
- إذا الحرف يطابق أول حرف في الكلمة، نبدأ بحث عميق (DFS) منها.
- في كل خطوة، ننتقل إلى الخانات المجاورة (4 اتجاهات) ونبحث عن الحرف التالي.
- نستخدم مصفوفة `visited` لتجنب إعادة زيارة الخانات نفسها في نفس البحث.
- إذا تم إيجاد الكلمة بالكامل نرجع `true`.

---

## ✅ الكود الكامل في Dart:

```dart
dart
نسختحرير
bool exist(List<List<String>> board, String word) {
  int rows = board.length;
  int cols = board[0].length;
  List<List<bool>> visited = List.generate(rows, (_) => List.filled(cols, false));

  bool dfs(int row, int col, int index) {
    if (index == word.length) return true;

    if (row < 0 || row >= rows || col < 0 || col >= cols) return false;
    if (visited[row][col]) return false;
    if (board[row][col] != word[index]) return false;

    visited[row][col] = true;

    bool found = dfs(row + 1, col, index + 1) ||
                 dfs(row - 1, col, index + 1) ||
                 dfs(row, col + 1, index + 1) ||
                 dfs(row, col - 1, index + 1);

    visited[row][col] = false; // تراجع

    return found;
  }

  for (int i = 0; i < rows; i++) {
    for (int j = 0; j < cols; j++) {
      if (board[i][j] == word[0]) {
        if (dfs(i, j, 0)) return true;
      }
    }
  }

  return false;
}

```

---

## 🧪 تجربة:

```dart
dart
نسختحرير
void main() {
  List<List<String>> board = [
    ['A','B','C','E'],
    ['S','F','C','S'],
    ['A','D','E','E']
  ];

  print("هل الكلمة 'ABCCED' موجودة؟ ${exist(board, 'ABCCED')}"); // true
  print("هل الكلمة 'SEE' موجودة؟ ${exist(board, 'SEE')}");     // true
  print("هل الكلمة 'ABCB' موجودة؟ ${exist(board, 'ABCB')}");   // false
}

```

---

## ✅ الناتج المتوقع:

```
bash
نسختحرير
هل الكلمة 'ABCCED' موجودة؟ true
هل الكلمة 'SEE' موجودة؟ true
هل الكلمة 'ABCB' موجودة؟ false

```

---

## 📦 التحليل:

| الخاصية | القيمة |
| --- | --- |
| الزمن | O(N * 3^L) حيث N = عدد الخانات، L = طول الكلمة |
| الذاكرة | O(N) (لـ visited ومكدس الاستدعاءات) |
| النوع | Backtracking / DFS |