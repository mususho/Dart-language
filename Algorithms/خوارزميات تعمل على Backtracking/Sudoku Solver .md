# Sudoku Solver

## 🔢 Sudoku Solver

**(حل لعبة السودوكو)**

---

## 🎯 الهدف:

> إعطاء مصفوفة 9x9 تمثل لوحة سودوكو (بعض الخانات مملوءة وبعضها فارغة)،
> 
> 
> المطلوب تعبئة الخانات الفارغة بحيث تكون اللوحة صحيحة وفق قواعد السودوكو:
> 
> - كل صف يحتوي الأرقام من 1 إلى 9 بدون تكرار
> - كل عمود يحتوي الأرقام من 1 إلى 9 بدون تكرار
> - كل مربع 3x3 يحتوي الأرقام من 1 إلى 9 بدون تكرار

---

## 🧠 الفكرة (Backtracking):

- نبحث عن أول خانة فارغة (تمثل بـ 0 أو أي قيمة تمثل فراغ).
- نجرب الأرقام من 1 إلى 9 في هذه الخانة.
- لكل رقم، نتحقق إذا كان صالح (لا يتعارض مع الصف، العمود، أو الصندوق 3x3).
- إذا صالح، نضع الرقم وننتقل للخانة التالية.
- إذا لم يكن صالح أي رقم، نرجع خطوة للوراء (Backtrack).

---

## ✅ الكود الكامل في Dart:

```dart
dart
نسختحرير
bool isSafe(List<List<int>> board, int row, int col, int num) {
  // تحقق الصف
  for (int x = 0; x < 9; x++) {
    if (board[row][x] == num) return false;
  }

  // تحقق العمود
  for (int x = 0; x < 9; x++) {
    if (board[x][col] == num) return false;
  }

  // تحقق الصندوق 3x3
  int startRow = row - row % 3;
  int startCol = col - col % 3;
  for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 3; j++) {
      if (board[startRow + i][startCol + j] == num) return false;
    }
  }

  return true;
}

bool solveSudoku(List<List<int>> board) {
  for (int row = 0; row < 9; row++) {
    for (int col = 0; col < 9; col++) {
      if (board[row][col] == 0) {
        for (int num = 1; num <= 9; num++) {
          if (isSafe(board, row, col, num)) {
            board[row][col] = num;

            if (solveSudoku(board)) {
              return true;
            }

            board[row][col] = 0; // تراجع
          }
        }
        return false; // لا يوجد رقم صالح لهذا الموقع
      }
    }
  }
  return true; // تم حل اللوحة
}

void printBoard(List<List<int>> board) {
  for (var row in board) {
    print(row.join(' '));
  }
}

```

---

## 🧪 تجربة:

```dart
dart
نسختحرير
void main() {
  List<List<int>> board = [
    [5, 3, 0, 0, 7, 0, 0, 0, 0],
    [6, 0, 0, 1, 9, 5, 0, 0, 0],
    [0, 9, 8, 0, 0, 0, 0, 6, 0],
    [8, 0, 0, 0, 6, 0, 0, 0, 3],
    [4, 0, 0, 8, 0, 3, 0, 0, 1],
    [7, 0, 0, 0, 2, 0, 0, 0, 6],
    [0, 6, 0, 0, 0, 0, 2, 8, 0],
    [0, 0, 0, 4, 1, 9, 0, 0, 5],
    [0, 0, 0, 0, 8, 0, 0, 7, 9],
  ];

  if (solveSudoku(board)) {
    printBoard(board);
  } else {
    print("لا يوجد حل للوحة");
  }
}

```

---

## ✅ الناتج المتوقع:

```
نسختحرير
5 3 4 6 7 8 9 1 2
6 7 2 1 9 5 3 4 8
1 9 8 3 4 2 5 6 7
8 5 9 7 6 1 4 2 3
4 2 6 8 5 3 7 9 1
7 1 3 9 2 4 8 5 6
9 6 1 5 3 7 2 8 4
2 8 7 4 1 9 6 3 5
3 4 5 2 8 6 1 7 9

```

---

## 📦 التحليل:

| الخاصية | القيمة |
| --- | --- |
| الزمن | تقريبًا O(9^(m)) حيث m = عدد الخانات الفارغة |
| الذاكرة | O(1) (لوحة اللعبة) |
| النوع | Backtracking |