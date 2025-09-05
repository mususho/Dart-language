# N-Queens

## 👑 N-Queens Problem

**(مشكلة ترتيب الملكات على الرقعة)**

---

## 🎯 الهدف:

> وضع N ملكات على رقعة N x N بحيث لا تهدد أي ملكة أخرى.
> 
> 
> الشرط: لا يوجد ملكتان في نفس الصف، العمود، أو القطريات.
> 

---

## 🧠 الفكرة (Backtracking):

- نضع الملكة في صف `row` في عمود مناسب.
- لكل صف نجرب كل الأعمدة الممكنة.
- إذا كان المكان آمن، نضع الملكة وننتقل للصف التالي.
- إذا وصلنا لنهاية الصفوف بنجاح، سجلنا حل.
- إذا تعذر الوضع، نعود خطوة للوراء (Backtrack).

---

## ✅ كود Dart مع شرح:

```dart
dart
نسختحرير
bool isSafe(List<List<int>> board, int row, int col, int n) {
  // تحقق من العمود للأعلى
  for (int i = 0; i < row; i++) {
    if (board[i][col] == 1) return false;
  }

  // تحقق من القطر الأعلى الأيسر
  for (int i = row - 1, j = col - 1; i >= 0 && j >= 0; i--, j--) {
    if (board[i][j] == 1) return false;
  }

  // تحقق من القطر الأعلى الأيمن
  for (int i = row - 1, j = col + 1; i >= 0 && j < n; i--, j++) {
    if (board[i][j] == 1) return false;
  }

  return true;
}

bool solveNQueensUtil(List<List<int>> board, int row, int n) {
  if (row == n) {
    return true; // تم وضع الملكات كلها
  }

  for (int col = 0; col < n; col++) {
    if (isSafe(board, row, col, n)) {
      board[row][col] = 1; // وضع الملكة

      if (solveNQueensUtil(board, row + 1, n)) {
        return true;
      }

      board[row][col] = 0; // تراجع (Backtrack)
    }
  }

  return false; // لم نجد مكان مناسب في هذا الصف
}

void printBoard(List<List<int>> board) {
  for (var row in board) {
    print(row.map((cell) => cell == 1 ? 'Q' : '.').join(' '));
  }
}

void main() {
  int n = 4;
  List<List<int>> board = List.generate(n, (_) => List.filled(n, 0));

  if (solveNQueensUtil(board, 0, n)) {
    printBoard(board);
  } else {
    print("لا يوجد حل");
  }
}

```

---

## 🧪 تجربة:

لـ `n = 4` الناتج المتوقع:

```
css
نسختحرير
. Q . .
. . . Q
Q . . .
. . Q .

```

---

## 📦 التحليل:

| الخاصية | القيمة |
| --- | --- |
| الزمن | O(N!) |
| الذاكرة | O(N²) (لوحة اللعب) |
| النوع | Backtracking |