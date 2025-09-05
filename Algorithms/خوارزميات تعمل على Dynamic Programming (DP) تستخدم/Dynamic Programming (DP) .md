# Dynamic Programming (DP)

## 🧠 Dynamic Programming (البرمجة الديناميكية)

> Dynamic Programming (DP) هي أسلوب لحل المشكلات التي تحتوي على حالات متكررة وقرارات تعتمد على نتائج سابقة، بطريقة أكثر كفاءة من التكرار العادي أو الحل العودي (recursion).
> 

---

## ✳️ متى نستخدم DP؟

عندما تجد في المشكلة:

1. ✅ **Subproblems** – مشكلة كبيرة يمكن تقسيمها إلى مشاكل فرعية.
2. ✅ **Overlapping subproblems** – المشاكل الفرعية تتكرر.
3. ✅ **Optimal substructure** – الحل النهائي يعتمد على الحلول المثلى للمشاكل الأصغر.

---

## 📘 أمثلة مشهورة:

| المشكلة | الشرح |
| --- | --- |
| Fibonacci | العدد التالي هو مجموع السابقين. |
| Climbing Stairs | كم طريقة للوصول إلى الدرجة n؟ |
| Knapsack | اختيار العناصر بأقصى فائدة. |
| Coin Change | أقل عدد عملات للوصول إلى المبلغ. |
| Longest Common Subseq | أطول سلسلة مشتركة. |

---

## 🧭 استراتيجيات الحل:

### 1. ✅ Top-Down (Memoization)

- حل باستخدام recursion مع تخزين النتائج السابقة.

### 2. ✅ Bottom-Up (Tabulation)

- نبني الحل خطوة بخطوة من البداية بدون recursion.

---

## ✅ مثال تطبيقي بسيط: Fibonacci باستخدام 3 طرق

### 1. 🔁 الطريقة الساذجة (Recursion فقط):

```dart
dart
نسختحرير
int fibNaive(int n) {
  if (n <= 1) return n;
  return fibNaive(n - 1) + fibNaive(n - 2);
}

```

❌ سيئة جدًا في الأداء – O(2^n)

---

### 2. ✅ Memoization (Top-Down):

```dart
dart
نسختحرير
Map<int, int> memo = {};

int fibMemo(int n) {
  if (n <= 1) return n;
  if (memo.containsKey(n)) return memo[n]!;

  memo[n] = fibMemo(n - 1) + fibMemo(n - 2);
  return memo[n]!;
}

```

✔️ أفضل بكثير – O(n) زمن و O(n) ذاكرة

---

### 3. ✅ Tabulation (Bottom-Up):

```dart
dart
نسختحرير
int fibTab(int n) {
  if (n <= 1) return n;

  List<int> dp = List.filled(n + 1, 0);
  dp[1] = 1;

  for (int i = 2; i <= n; i++) {
    dp[i] = dp[i - 1] + dp[i - 2];
  }

  return dp[n];
}

```

✔️ ممتاز – O(n) زمن و O(n) ذاكرة

💡 يمكن تحسين الذاكرة إلى O(1) باستخدام متغيرين فقط.

---

## 🧪 تجربة جميع الطرق:

```dart
dart
نسختحرير
void main() {
  int n = 10;

  print("🔁 Naive Recursion: ${fibNaive(n)}");
  print("🧠 Memoization: ${fibMemo(n)}");
  print("⬇️ Tabulation: ${fibTab(n)}");
}

```

---

## ✅ الناتج:

```
yaml
نسختحرير
🔁 Naive Recursion: 55
🧠 Memoization: 55
⬇️ Tabulation: 55

```

---

## 🧠 ملخص مقارنة:

| الطريقة | الزمن | الذاكرة | الأسلوب |
| --- | --- | --- | --- |
| Naive Recursion | O(2^n) | O(n) | تكرار |
| Memoization | O(n) | O(n) | أعلى لأسفل |
| Tabulation | O(n) | O(n) | أسفل لأعلى |

---

## 🚀 جاهز لتطبيق أقوى؟

هل ترغب أن ننتقل إلى: