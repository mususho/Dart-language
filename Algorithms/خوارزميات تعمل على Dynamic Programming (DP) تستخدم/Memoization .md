# Memoization

## 🧠 Memoization (الحفظ المؤقت للنتائج) في Dart

**(تقنية لتسريع recursion عبر حفظ القيم المحسوبة مسبقًا)**

---

## 🎯 ما هو Memoization؟

> هو أسلوب نستخدمه لحل مشاكل الـ Recursion البطيئة، من خلال تخزين نتائج الدالة في جدول (cache)، حتى لا نكرر الحساب لنفس المدخلات.
> 

---

## 📉 بدون Memoization:

بعض المشاكل مثل Fibonacci تتكرر بشكل كبير:

مثلاً لحساب `fib(5)`:

```
scss
نسختحرير
fib(5)
→ fib(4) + fib(3)
→ fib(3) + fib(2) + fib(2) + fib(1)
→ fib(2) + fib(1) + fib(1) + fib(0) ...

```

👎 نفس القيم يتم حسابها أكثر من مرة!

---

## ✅ باستخدام Memoization:

نقوم بتخزين كل نتيجة نحصل عليها في `Map` أو `List`

وعند الحاجة إليها لاحقًا، نسترجعها بدلًا من إعادة الحساب.

---

## 🔧 مثال: Fibonacci باستخدام Memoization

```dart
dart
نسختحرير
Map<int, int> memo = {};

int fibMemo(int n) {
  if (n <= 1) return n;

  if (memo.containsKey(n)) {
    return memo[n]!;
  }

  memo[n] = fibMemo(n - 1) + fibMemo(n - 2);
  return memo[n]!;
}

```

---

## 🧪 تجربة:

```dart
dart
نسختحرير
void main() {
  int n = 40;
  print("🔢 Fibonacci($n): ${fibMemo(n)}");
}

```

### ✅ أسرع بكثيــر من النسخة العودية العادية

- الزمن: **O(n)**
- الذاكرة: **O(n)**

---

## 📦 يمكن استخدامه في أي دالة recursive تحتوي على:

- مشاكل مكررة.
- نفس المدخل يعطي نفس الإخراج.

---

## 📘 مثال آخر: Climbing Stairs (طرق الصعود)

```dart
dart
نسختحرير
Map<int, int> dp = {};

int climbStairs(int n) {
  if (n <= 2) return n;

  if (dp.containsKey(n)) return dp[n]!;

  dp[n] = climbStairs(n - 1) + climbStairs(n - 2);
  return dp[n]!;
}

```

---

## ✅ ما الفرق بين Memoization و Tabulation؟

|  | Memoization (Top-Down) | Tabulation (Bottom-Up) |
| --- | --- | --- |
| يعتمد على | Recursion | Loop |
| يستخدم | Map / List لتخزين | Array |
| من الأعلى للأسفل | ✅ | ❌ |
| من الأسفل للأعلى | ❌ | ✅ |

---

## 🧠 نصيحة: استخدم Memoization عندما:

- تستخدم recursion وتريد تسريع الأداء.
- لا تحتاج إلى بنية تكرار من البداية للنهاية.
- تريد وضوح الشيفرة وسهولة تتبعها.