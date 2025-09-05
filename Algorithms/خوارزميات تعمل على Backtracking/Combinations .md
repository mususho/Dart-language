# Combinations

## ➕ Combinations

**(توليد كل التوافيق الممكنة بحجم معين من مجموعة عناصر)**

---

## 🎯 الهدف:

> إعطاء قائمة nums وعدد k،
> 
> 
> نريد توليد كل المجموعات الفرعية (combinations) بحجم `k` (أي اختيار `k` عناصر بدون تكرار ومن دون ترتيب).
> 

---

## 🧠 الفكرة (Backtracking):

- نستخدم استدعاء ذاتي مع مؤشر بداية.
- نختار العناصر بشكل تتابعي.
- نضيف المجموعة إلى النتيجة إذا وصل حجمها `k`.
- نمنع التكرار باختيار العناصر فقط من الفهرس الحالي للأمام.

---

## ✅ الكود الكامل في Dart:

```dart
dart
نسختحرير
List<List<int>> combine(List<int> nums, int k) {
  List<List<int>> result = [];
  List<int> current = [];

  void backtrack(int start) {
    if (current.length == k) {
      result.add(List.from(current));
      return;
    }

    for (int i = start; i < nums.length; i++) {
      current.add(nums[i]);
      backtrack(i + 1);
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
  List<int> nums = [1, 2, 3, 4];
  int k = 2;

  List<List<int>> combos = combine(nums, k);

  print("➕ التوافيق بحجم $k:");
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
[1, 2]
[1, 3]
[1, 4]
[2, 3]
[2, 4]
[3, 4]

```

---

## 📦 التحليل:

| الخاصية | القيمة |
| --- | --- |
| الزمن | O(n! / (k! * (n-k)!)) (عدد التوافيق) |
| الذاكرة | O(k) (للمكدس والاستدعاءات) |
| النوع | Backtracking / Recursion |