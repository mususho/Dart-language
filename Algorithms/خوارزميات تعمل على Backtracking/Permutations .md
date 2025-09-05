# Permutations

---

## 🔄 Permutations

**(توليد كل التباديل الممكنة لعناصر مجموعة)**

---

## 🎯 الهدف:

> إعطاء قائمة nums (عناصر مميزة)،
> 
> 
> نريد توليد **كل الترتيبات الممكنة** للعناصر (كل التباديل).
> 

---

## 🧠 الفكرة (Backtracking):

- نستخدم استدعاء ذاتي مع تبديل العناصر.
- عند كل مستوى، نختار عنصرًا لموقع معين.
- نتابع لباقي المواقع.
- عند اكتمال الترتيب نضيفه للنتيجة.

---

## ✅ الكود الكامل في Dart:

```dart
dart
نسختحرير
List<List<int>> permute(List<int> nums) {
  List<List<int>> result = [];

  void backtrack(int start) {
    if (start == nums.length) {
      result.add(List.from(nums));
      return;
    }

    for (int i = start; i < nums.length; i++) {
      // تبادل العناصر
      int temp = nums[start];
      nums[start] = nums[i];
      nums[i] = temp;

      backtrack(start + 1);

      // تراجع (استرجاع الحالة)
      temp = nums[start];
      nums[start] = nums[i];
      nums[i] = temp;
    }
  }

  backtrack(0);
  return result;
}

```

---

## 🧪 تجربة:

```dart
dart
نسختحرير
void main() {
  List<int> nums = [1, 2, 3];
  List<List<int>> allPermutations = permute(nums);

  print("🔄 كل التباديل:");
  for (var perm in allPermutations) {
    print(perm);
  }
}

```

---

## ✅ الناتج المتوقع:

```
csharp
نسختحرير
[1, 2, 3]
[1, 3, 2]
[2, 1, 3]
[2, 3, 1]
[3, 2, 1]
[3, 1, 2]

```

---

## 📦 التحليل:

| الخاصية | القيمة |
| --- | --- |
| الزمن | O(n! * n) (عدد التباديل × نسخ القائمة) |
| الذاكرة | O(n) (للمكدس والاستدعاءات) |
| النوع | Backtracking / Recursion |