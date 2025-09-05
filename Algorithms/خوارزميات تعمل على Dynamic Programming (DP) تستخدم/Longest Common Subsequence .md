# Longest Common Subsequence

## 📘 Longest Common Subsequence (LCS)

**أطول تسلسل مشترك**

---

## 🎯 الهدف:

> إعطاء سلسلتين (Strings)، والمطلوب إيجاد أطول سلسلة فرعية (subsequence) تظهر في كل منهما بنفس الترتيب (لكن ليس بالضرورة متتالية).
> 

---

### 📌 مثال:

```dart
dart
نسختحرير
String s1 = "abcde";
String s2 = "ace";

```

✅ النتيجة: `"ace"`

✅ الطول: `3`

---

## ✳️ الفرق بين Substring و Subsequence:

| الخاصية | Substring | Subsequence |
| --- | --- | --- |
| الترتيب | يجب أن تكون متتالية | فقط نفس الترتيب |
| المثال | "abc" ⊆ "abcde" | "ace" ⊆ "abcde" |

---

## 🧠 الفكرة (Dynamic Programming - Tabulation):

ننشىء جدول 2D `dp[i][j]` يمثل:

> LCS بين أول i حروف من s1 وأول j حروف من s2
> 

### القاعدة:

- إذا كان الحرفان متساويين:
    
    `dp[i][j] = dp[i-1][j-1] + 1`
    
- إذا لا:
    
    `dp[i][j] = max(dp[i-1][j], dp[i][j-1])`
    

---

## ✅ الكود الكامل في Dart مع شرح:

```dart
dart
نسختحرير
int longestCommonSubsequence(String s1, String s2) {
  int m = s1.length;
  int n = s2.length;

  List<List<int>> dp = List.generate(
    m + 1,
    (_) => List.filled(n + 1, 0),
  );

  for (int i = 1; i <= m; i++) {
    for (int j = 1; j <= n; j++) {
      if (s1[i - 1] == s2[j - 1]) {
        // إذا الحرفين متساويين
        dp[i][j] = dp[i - 1][j - 1] + 1;
      } else {
        // نأخذ الأفضل بين تجاهل حرف من s1 أو s2
        dp[i][j] = dp[i - 1][j] > dp[i][j - 1]
            ? dp[i - 1][j]
            : dp[i][j - 1];
      }
    }
  }

  return dp[m][n]; // الناتج النهائي
}

```

---

## 🧪 تجربة:

```dart
dart
نسختحرير
void main() {
  String s1 = "abcde";
  String s2 = "ace";

  int lcsLength = longestCommonSubsequence(s1, s2);
  print("🔗 LCS الطول: $lcsLength"); // 3
}

```

---

## ✅ الناتج المتوقع:

```
نسختحرير
🔗 LCS الطول: 3

```

---

## 📦 التحليل:

| الخاصية | القيمة |
| --- | --- |
| الزمن | O(m * n) |
| الذاكرة | O(m * n) |
| نوع | Tabulation DP |
| إعادة بناء LCS | ممكن ✅ (نوضحها لو أردت) |

---

## 💡 ملاحظة: إذا أردت استرجاع سلسلة LCS نفسها:

أضف دالة ترجع **String** وتبدأ من `dp[m][n]` وتتبع المسار للخلف

(أشرحها إذا طلبت).

---

هل تحب أن أشرح: