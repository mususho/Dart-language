# Backtracking

## 🔍 Backtracking (الرجوع للخلف) في Dart

**(أسلوب لاختبار جميع الاحتمالات والرجوع عند الوصول لطريق مسدود)**

---

## 🎯 ما هو Backtracking؟

> هو أسلوب لحل المشاكل بطريقة تجربة الخيارات جميعها بشكل متسلسل، وإذا وصلنا لطريق غير صالح، نتراجع (Backtrack) ونجرّب خيارًا آخر.
> 

🔄 يشبه شجرة قرارات – تستكشف كل فرع وتعود إن لم تصل للحل.

---

## 🧠 خطوات خوارزمية Backtracking:

1. **اختر خيارًا.**
2. **تحقق هل نصل إلى هدف؟**
3. إذا نعم، ✅ احفظ الحل.
4. إذا لا، تابع بمحاولة الخيارات التالية.
5. **إذا فشلت، تراجع** (Undo).

---

## 📘 أشهر التطبيقات:

| المسألة | النوع |
| --- | --- |
| Permutations | جميع التباديل الممكنة |
| N-Queens | وضع الملكات في الشطرنج |
| Sudoku Solver | حل ألعاب الأرقام |
| Subsets / Combinations | كل المجموعات الممكنة |
| Word Search | البحث في جدول أحرف |

---

## 🔧 مثال بسيط: كل التباديل الممكنة `permutations`

### ⚙️ الهدف:

> أعطني كل الترتيبات الممكنة لعناصر [1, 2, 3].
> 

### ✅ كود Dart:

```dart
dart
نسختحرير
void generatePermutations(List<int> nums) {
  List<List<int>> result = [];
  _backtrack(nums, [], result);
  for (var perm in result) {
    print(perm);
  }
}

void _backtrack(List<int> nums, List<int> path, List<List<int>> result) {
  if (path.length == nums.length) {
    result.add(List.from(path));
    return;
  }

  for (int i = 0; i < nums.length; i++) {
    if (path.contains(nums[i])) continue;

    path.add(nums[i]);
    _backtrack(nums, path, result);
    path.removeLast(); // 🧹 تراجع للخلف
  }
}

```

---

### 🧪 تجربة:

```dart
dart
نسختحرير
void main() {
  List<int> input = [1, 2, 3];
  generatePermutations(input);
}

```

### ✅ الناتج:

```
csharp
نسختحرير
[1, 2, 3]
[1, 3, 2]
[2, 1, 3]
[2, 3, 1]
[3, 1, 2]
[3, 2, 1]

```

---

## 🔁 مثال آخر: Subsets (جميع المجموعات الممكنة)

```dart
dart
نسختحرير
void generateSubsets(List<int> nums) {
  List<List<int>> result = [];
  _subsetsBacktrack(nums, 0, [], result);
  for (var subset in result) {
    print(subset);
  }
}

void _subsetsBacktrack(List<int> nums, int start, List<int> path, List<List<int>> result) {
  result.add(List.from(path));

  for (int i = start; i < nums.length; i++) {
    path.add(nums[i]);
    _subsetsBacktrack(nums, i + 1, path, result);
    path.removeLast(); // 🧹 رجوع
  }
}

```

---

## 📌 أهم مميزات Backtracking:

| خاصية | شرح |
| --- | --- |
| نوع من أنواع الـ DFS | نعم، هو نسخة من الاستكشاف العمق أولًا |
| يحتاج إلى رجوع | دائمًا بعد تجربة خيار غير صالح |
| يستخدم غالبًا مع | Arrays, Strings, Grids, Combinatorics |
| الأداء | قد يكون O(2^n) أو أكثر، حسب عدد الاحتمالات |

---

## 🚦 حالات يُستخدم فيها Backtracking:

- الألعاب المنطقية (مثل Sudoku)
- مشاكل الترتيب والتجميع
- البحث في المسارات (مثل إيجاد طريق في متاهة)
- حل المعادلات المقيدة