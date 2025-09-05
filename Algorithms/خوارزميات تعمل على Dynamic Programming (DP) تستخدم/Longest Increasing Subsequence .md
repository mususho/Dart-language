# Longest Increasing Subsequence

## 📈 Longest Increasing Subsequence (LIS)

**أطول سلسلة متزايدة**

---

## 🎯 الهدف:

> إعطاءك مصفوفة من الأعداد، والمطلوب هو إيجاد أطول تسلسل فرعي (غير متصل بالضرورة) تكون قيمه متزايدة Strictly Increasing.
> 

---

### 📘 مثال:

```dart
dart
نسختحرير
List<int> nums = [10, 9, 2, 5, 3, 7, 101, 18];

```

أطول سلسلة متزايدة: `[2, 3, 7, 101]`

**الطول = 4**

---

## 🧠 الفكرة (Dynamic Programming – Tabulation):

- ننشئ مصفوفة `dp` حيث:
    - `dp[i]` = طول أطول سلسلة متزايدة **تنتهي بالعنصر i**
- نبدأ من `dp[i] = 1` لأن كل عنصر بحد ذاته سلسلة.
- نقارن `nums[i]` بجميع العناصر السابقة `nums[j]` (حيث `j < i`) و:
    - إذا `nums[i] > nums[j]`، نحدث:
        
        ```dart
        dart
        نسختحرير
        dp[i] = max(dp[i], dp[j] + 1)
        
        ```
        

---

## ✅ الكود الكامل بلغة Dart:

```dart
dart
نسختحرير
int longestIncreasingSubsequence(List<int> nums) {
  if (nums.isEmpty) return 0;

  int n = nums.length;
  List<int> dp = List.filled(n, 1); // كل عنصر يبدأ بسلسلة طوله 1

  for (int i = 1; i < n; i++) {
    for (int j = 0; j < i; j++) {
      if (nums[i] > nums[j]) {
        dp[i] = dp[i].clamp(0, dp[j] + 1).compareTo(dp[j] + 1) < 0
            ? dp[j] + 1
            : dp[i];
      }
    }
  }

  return dp.reduce((a, b) => a > b ? a : b); // أكبر طول من بين الكل
}

```

---

## 🧪 تجربة:

```dart
dart
نسختحرير
void main() {
  List<int> nums = [10, 9, 2, 5, 3, 7, 101, 18];

  int lisLength = longestIncreasingSubsequence(nums);
  print("📈 أطول سلسلة متزايدة: $lisLength");
}

```

---

### ✅ الناتج المتوقع:

```
نسختحرير
📈 أطول سلسلة متزايدة: 4

```

---

## 📌 التحليل:

| الخاصية | القيمة |
| --- | --- |
| الزمن | O(n²) |
| المساحة | O(n) |
| تعتمد على | مقارنة كل عنصر مع من قبله |

---

## 🧪 ملاحظة إضافية:

🔸 يمكن تحسين الزمن إلى **O(n log n)** باستخدام **binary search** + `List<int>` تمثل نهاية كل سلسلة محتملة.