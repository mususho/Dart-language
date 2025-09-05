# Subset Sum

## ✅ Subset Sum Problem

**(هل يوجد مجموعة فرعية بمجموع معين؟)**

---

## 🎯 الهدف:

> إعطاء مجموعة من الأعداد nums ومجموع هدف target،
> 
> 
> نريد معرفة إذا كان يمكننا اختيار مجموعة فرعية من `nums` بحيث يكون مجموعها **يساوي** `target`.
> 

---

## 🧠 الفكرة (Dynamic Programming):

- نستخدم جدول `dp` حيث:
    - `dp[i][j]` يعني: هل يمكن تكوين المجموع `j` باستخدام أول `i` عناصر؟
- القاعدة:
    - إذا `nums[i-1] <= j`:
        
        ```dart
        dart
        نسختحرير
        dp[i][j] = dp[i-1][j] || dp[i-1][j - nums[i-1]]
        
        ```
        
    - وإلا:
        
        ```dart
        dart
        نسختحرير
        dp[i][j] = dp[i-1][j]
        
        ```
        

---

## ✅ الكود الكامل في Dart:

```dart
dart
نسختحرير
bool subsetSum(List<int> nums, int target) {
  int n = nums.length;

  List<List<bool>> dp = List.generate(
    n + 1,
    (_) => List.filled(target + 1, false),
  );

  for (int i = 0; i <= n; i++) {
    dp[i][0] = true; // مجموع 0 ممكن دائمًا (باختيار مجموعة فارغة)
  }

  for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= target; j++) {
      if (nums[i - 1] <= j) {
        dp[i][j] = dp[i - 1][j] || dp[i - 1][j - nums[i - 1]];
      } else {
        dp[i][j] = dp[i - 1][j];
      }
    }
  }

  return dp[n][target];
}

```

---

## 🧪 تجربة:

```dart
dart
نسختحرير
void main() {
  List<int> nums = [3, 34, 4, 12, 5, 2];
  int target = 9;

  bool canSum = subsetSum(nums, target);
  print("هل يمكن تكوين $target؟ $canSum");
}

```

---

## ✅ الناتج المتوقع:

```
arduino
نسختحرير
هل يمكن تكوين 9؟ true

```

---

## 📦 التحليل:

| الخاصية | القيمة |
| --- | --- |
| الزمن | O(n * target) |
| الذاكرة | O(n * target) |
| النوع | Dynamic Programming |