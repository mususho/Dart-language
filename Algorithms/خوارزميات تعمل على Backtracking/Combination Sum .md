# Combination Sum

## ➕ Combination Sum

**(توليد كل التوافيق التي يكون مجموع عناصرها يساوي الهدف)**

---

## 🎯 الهدف:

> لديك قائمة أعداد موجبة candidates (بدون تكرار)،
> 
> 
> ومجموع هدف `target`،
> 
> نريد توليد **كل المجموعات الفرعية (combinations)** التي يكون مجموعها **يساوي الهدف**.
> 
> يمكن استخدام نفس العنصر أكثر من مرة.
> 

---

## 🧠 الفكرة (Backtracking):

- نستكشف كل عنصر بدءًا من موقع معين.
- في كل استدعاء، نجرب:
    - **اخذ العنصر الحالي** (ونخفض الهدف).
    - **تخطي العنصر الحالي** (الانتقال للعنصر التالي).
- إذا وصل الهدف لـ0، نضيف المجموعة الحالية للنتيجة.
- نستخدم `start` لتجنب التكرار.

---

## ✅ الكود الكامل في Dart:

```dart
dart
نسختحرير
List<List<int>> combinationSum(List<int> candidates, int target) {
  List<List<int>> result = [];
  List<int> current = [];

  void backtrack(int start, int remaining) {
    if (remaining == 0) {
      result.add(List.from(current));
      return;
    }

    for (int i = start; i < candidates.length; i++) {
      int num = candidates[i];
      if (num > remaining) continue;

      current.add(num);
      backtrack(i, remaining - num); // نسمح بإعادة استخدام نفس العنصر
      current.removeLast();
    }
  }

  backtrack(0, target);
  return result;
}

```

---

## 🧪 تجربة:

```dart
dart
نسختحرير
void main() {
  List<int> candidates = [2, 3, 6, 7];
  int target = 7;

  List<List<int>> combos = combinationSum(candidates, target);

  print("➕ مجموعات الأعداد التي تعطي $target:");
  for (var combo in combos) {
    print(combo);
  }
}

```

---

## ✅ الناتج المتوقع:

```
csharp
نسختحرير
[2, 2, 3]
[7]

```

---

## 📦 التحليل:

| الخاصية | القيمة |
| --- | --- |
| الزمن | Exponential (يعتمد على الحلول الممكنة) |
| الذاكرة | O(target) |
| النوع | Backtracking |