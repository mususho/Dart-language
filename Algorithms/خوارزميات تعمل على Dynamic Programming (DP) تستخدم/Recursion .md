# Recursion

## 🔁 Recursion في Dart

**(الاستدعاء الذاتي للدوال)**

---

## 🧠 ما هو Recursion؟

> الـ Recursion هو أسلوب في البرمجة تقوم فيه الدالة بنداء نفسها لحل مشكلة عبر تقسيمها إلى مشاكل أصغر.
> 

---

## ✳️ شروط استخدام Recursion:

1. **Base Case** (الحالة النهائية): شرط لإنهاء التكرار.
2. **Recursive Case** (الاستدعاء): حيث تنادي الدالة نفسها بحجم مشكلة أصغر.

---

## 📘 مثال بسيط: العد التنازلي

```dart
dart
نسختحرير
void countdown(int n) {
  if (n == 0) {
    print("🚀 انطلاق!");
    return;
  }

  print(n);
  countdown(n - 1); // استدعاء ذاتي
}

```

### ✅ الناتج:

```
نسختحرير
5
4
3
2
1
🚀 انطلاق!

```

---

## 📘 مثال رياضي: Factorial

> ![n] = n × (n - 1) × (n - 2) × ... × 1
> 

```dart
dart
نسختحرير
int factorial(int n) {
  if (n <= 1) return 1;        // base case
  return n * factorial(n - 1); // recursive case
}

```

### ✅ factorial(5):

```
python-repl
نسختحرير
= 5 * factorial(4)
= 5 * 4 * factorial(3)
...
= 5 * 4 * 3 * 2 * 1 = 120

```

---

## 📘 مثال شهير: Fibonacci

```dart
dart
نسختحرير
int fibonacci(int n) {
  if (n <= 1) return n;
  return fibonacci(n - 1) + fibonacci(n - 2);
}

```

❗️ هذا بطيء جدًا – يمكن تحسينه بـ Memoization أو Tabulation.

---

## 📘 Recursion مع قائمة:

### طباعة قائمة من الخلف إلى الأمام:

```dart
dart
نسختحرير
void printReverse(List<int> list, int index) {
  if (index < 0) return;
  print(list[index]);
  printReverse(list, index - 1);
}

```

---

## ❗️ ملاحظات هامة:

| نقطة | شرح |
| --- | --- |
| Stack Overflow | يحدث عند عدم وجود شرط نهائي مناسب. |
| Stack Frame | كل استدعاء ذاتي يتم حفظه مؤقتًا في الذاكرة. |
| قابلية التحويل | غالبًا يمكن تحويله إلى حل باستخدام حلقة. |

---

## ✅ متى تستخدم الـ Recursion؟

| تستخدم عندما تكون: | ✅ أمثلة |
| --- | --- |
| مشكلة قابلة للتقسيم | Factorial, Fibonacci, Trees |
| بنية بيانات متداخلة | شجرة، ملف داخل مجلد |
| تحتاج backtracking | حل المتاهة، الكلمات الممكنة |

---

## 🧪 تجربة كاملة:

```dart
dart
نسختحرير
void main() {
  print("📦 Factorial of 5: ${factorial(5)}");
  print("🔢 Fibonacci(6): ${fibonacci(6)}");

  List<int> nums = [10, 20, 30];
  print("\n🌀 Print List in Reverse:");
  printReverse(nums, nums.length - 1);
}

```

---

## 📌 ملخص:

| المصطلح | المعنى |
| --- | --- |
| Base Case | شرط إيقاف الاستدعاء الذاتي |
| Recursive Case | نداء الدالة لنفسها بمشكلة أصغر |
| Memoization | حفظ نتائج التكرار لتسريع الأداء |

---