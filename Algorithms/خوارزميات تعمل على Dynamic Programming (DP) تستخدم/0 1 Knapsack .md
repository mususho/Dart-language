# 0/1 Knapsack

## 🎒 0/1 Knapsack Problem

**(مشكلة حقيبة الظهر – اختيار العناصر لتحقيق أقصى قيمة دون تجاوز الوزن)**

---

## 🧠 الفكرة:

> لديك عدد من العناصر، كل عنصر له:
> 
- `وزن weight[i]`
- `قيمة value[i]`

وتمتلك حقيبة تستطيع حمل وزن لا يزيد عن `W`.

المطلوب: **اختر العناصر (بدون تكرار – إما تأخذه أو لا)** بحيث تحصل على **أقصى قيمة ممكنة**، ولا تتجاوز الوزن `W`.

---

## ✳️ الصيغة العامة:

```
txt
نسختحرير
n = عدد العناصر
W = السعة الكلية للحقيبة
weight[i] = وزن العنصر i
value[i]  = قيمته

dp[i][w] = أقصى قيمة يمكن الحصول عليها من أول i عناصر بوزن w

```

---

## ✅ الخوارزمية:

### الخيارات لكل عنصر:

- ✋ لا نأخذ العنصر: `dp[i-1][w]`
- ✅ نأخذ العنصر (إن أمكن): `value[i] + dp[i-1][w - weight[i]]`

---

## 🔧 كود Dart باستخدام Tabulation (Bottom-Up DP):

```dart
dart
نسختحرير
int knapsack(List<int> weights, List<int> values, int W) {
  int n = weights.length;
  List<List<int>> dp = List.generate(n + 1, (_) => List.filled(W + 1, 0));

  for (int i = 1; i <= n; i++) {
    for (int w = 0; w <= W; w++) {
      if (weights[i - 1] <= w) {
        dp[i][w] =
          dp[i - 1][w].clamp(0, double.infinity.toInt()).toInt().compareTo(
            values[i - 1] + dp[i - 1][w - weights[i - 1]]
          ) < 0
            ? values[i - 1] + dp[i - 1][w - weights[i - 1]]
            : dp[i - 1][w];
      } else {
        dp[i][w] = dp[i - 1][w];
      }
    }
  }

  return dp[n][W];
}

```

---

## 🧪 تجربة:

```dart
dart
نسختحرير
void main() {
  List<int> weights = [1, 3, 4, 5];
  List<int> values = [1, 4, 5, 7];
  int capacity = 7;

  print("🎒 أقصى قيمة ممكنة = ${knapsack(weights, values, capacity)}");
}

```

---

### ✅ الناتج المتوقع:

```
نسختحرير
🎒 أقصى قيمة ممكنة = 9

```

> (أخذنا العنصرين بوزن 3 و 4 وقيمتهما 4 + 5 = 9)
> 

---

## ⏱️ التحليل:

| الخاصية | القيمة |
| --- | --- |
| الزمن | O(n * W) |
| الذاكرة | O(n * W) |
| النوع | Tabulation (Bottom-Up) |
| التكرار | لا، كل عنصر مرة واحدة فقط |

---

## 💡 تحسينات إضافية:

- يمكن استخدام قائمة واحدة 1D بدلًا من 2D لتقليل المساحة.
- يمكن تنفيذها باستخدام **Memoization** بدلاً من Tabulation.