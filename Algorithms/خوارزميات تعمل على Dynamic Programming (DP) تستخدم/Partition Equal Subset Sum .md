# Partition Equal Subset Sum

## ⚖️ Partition Equal Subset Sum

**(تقسيم المصفوفة إلى مجموعتين لهما نفس المجموع)**

---

## 🎯 الهدف:

> إعطاء مصفوفة أعداد صحيحة موجبة nums،
> 
> 
> نريد معرفة إذا يمكن تقسيم هذه الأعداد إلى **مجموعتين فرعيتين** بحيث يكون مجموع كل منهما **متساوي**.
> 

---

## 🧠 الفكرة:

- أولاً نحسب مجموع كل الأعداد: `sum`
- إذا كان `sum` فرديًا، فالإجابة **لا** لأننا لا نستطيع تقسيمه بالتساوي.
- إذا كان زوجيًا، نبحث إذا كانت هناك مجموعة فرعية بمجموع `sum / 2` (تمامًا مثل مشكلة **Subset Sum**).

---

## ✅ الكود الكامل في Dart:

```dart
dart
نسختحرير
bool canPartition(List<int> nums) {
  int sum = nums.reduce((a, b) => a + b);

  // إذا المجموع فردي، لا يمكن التقسيم بالتساوي
  if (sum % 2 != 0) return false;

  int target = sum ~/ 2;
  int n = nums.length;

  List<List<bool>> dp = List.generate(
    n + 1,
    (_) => List.filled(target + 1, false),
  );

  for (int i = 0; i <= n; i++) {
    dp[i][0] = true; // يمكن دائماً تكوين مجموع 0
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
  List<int> nums = [1, 5, 11, 5];

  bool canDivide = canPartition(nums);
  print("هل يمكن تقسيم المصفوفة إلى مجموعتين متساويتين؟ $canDivide");
}

```

---

## ✅ الناتج المتوقع:

```
arduino
نسختحرير
هل يمكن تقسيم المصفوفة إلى مجموعتين متساويتين؟ true

```

---

## 📦 التحليل:

| الخاصية | القيمة |
| --- | --- |
| الزمن | O(n * sum/2) |
| الذاكرة | O(n * sum/2) |
| النوع | Dynamic Programming |