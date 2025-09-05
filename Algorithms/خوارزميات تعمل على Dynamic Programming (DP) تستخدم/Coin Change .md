# Coin Change

## 🪙 Coin Change Problem

**(مسألة تغيير العملة)**

---

## 🎯 الهدف:

> لديك مجموعة من العملات بقيم مختلفة (coins)،
> 
> 
> وهدفك هو معرفة **أقل عدد عملات** تحتاجها لتكوين مبلغ معين (amount).
> 

---

## ✳️ القواعد:

- يمكنك استخدام كل عملة عدة مرات.
- إن لم يكن المبلغ ممكنًا تكون النتيجة `1`.

---

## 🧠 الفكرة (Dynamic Programming - Tabulation):

- ننشئ مصفوفة `dp` طولها `amount + 1`،
- كل خانة `dp[i]` تمثل **أقل عدد عملات** لتكوين المبلغ `i`.
- نملأها بداية بـ `dp[0] = 0` (لأن 0 مبلغ يحتاج 0 عملات).
- لباقي القيم نبدأ بـ قيمة كبيرة (مثل `amount + 1`).
- ثم نحدث `dp[i]` عبر محاولة كل عملة `coin`:
    
    ```dart
    dart
    نسختحرير
    dp[i] = min(dp[i], dp[i - coin] + 1)
    
    ```
    

---

## ✅ الكود الكامل في Dart:

```dart
dart
نسختحرير
int coinChange(List<int> coins, int amount) {
  List<int> dp = List.filled(amount + 1, amount + 1);
  dp[0] = 0;

  for (int i = 1; i <= amount; i++) {
    for (int coin in coins) {
      if (coin <= i) {
        dp[i] = dp[i] < dp[i - coin] + 1 ? dp[i] : dp[i - coin] + 1;
      }
    }
  }

  return dp[amount] > amount ? -1 : dp[amount];
}

```

---

## 🧪 تجربة:

```dart
dart
نسختحرير
void main() {
  List<int> coins = [1, 2, 5];
  int amount = 11;

  print("🪙 أقل عدد عملات = ${coinChange(coins, amount)}");
}

```

---

## ✅ الناتج المتوقع:

```
نسختحرير
🪙 أقل عدد عملات = 3

```

(مثلاً: 5 + 5 + 1)

---

## 📦 التحليل:

| الخاصية | القيمة |
| --- | --- |
| الزمن | O(amount * n) |
| الذاكرة | O(amount) |
| النوع | Dynamic Programming |