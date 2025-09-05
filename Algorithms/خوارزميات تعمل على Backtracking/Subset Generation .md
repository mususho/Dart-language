# Subset Generation

## 🔢 Subset Generation

**(توليد كل المجموعات الفرعية الممكنة من مجموعة عناصر)**

---

## 🎯 الهدف:

> إعطاء مجموعة nums (قائمة أعداد)،
> 
> 
> نريد توليد **كل المجموعات الفرعية الممكنة** (subsets أو power set).
> 

---

## 🧠 الفكرة:

- نستخدم **الاستدعاء الذاتي (Recursion)** أو **Backtracking**.
- عند كل عنصر، نقرر إما:
    - **أخذ العنصر** في المجموعة الفرعية.
    - **عدم أخذه**.
- نكرر حتى ننتهي من كل العناصر.
- نضيف المجموعة الفرعية الناتجة إلى النتائج.

---

## ✅ الكود الكامل في Dart:

```dart
dart
نسختحرير
List<List<int>> subsets(List<int> nums) {
  List<List<int>> result = [];
  List<int> current = [];

  void backtrack(int index) {
    // إضافة النسخة الحالية إلى النتيجة
    result.add(List.from(current));

    for (int i = index; i < nums.length; i++) {
      // خذ العنصر الحالي
      current.add(nums[i]);

      // استمر
      backtrack(i + 1);

      // تراجع: أزل العنصر الحالي
      current.removeLast();
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
  List<List<int>> allSubsets = subsets(nums);

  print("🔢 كل المجموعات الفرعية:");
  for (var subset in allSubsets) {
    print(subset);
  }
}

```

---

## ✅ الناتج المتوقع:

```
css
نسختحرير
[]
[1]
[1, 2]
[1, 2, 3]
[1, 3]
[2]
[2, 3]
[3]

```

---

## 📦 التحليل:

| الخاصية | القيمة |
| --- | --- |
| الزمن | O(2^n * n) (لإنشاء كل مجموعة) |
| الذاكرة | O(n) (للمكدس والاستدعاءات) |
| النوع | Backtracking / Recursion |