# 🔄 Palindromic Substrings

## 🔄 Palindromic Substrings

**(عدد السلاسل الفرعية التي هي Palindromes)**

---

## 🎯 الهدف:

> إعطاء سلسلة نصية، نريد حساب عدد السلاسل الفرعية (substrings) التي تكون Palindrome (تقرأ نفسها من الأمام والخلف).
> 

---

## 🧠 الفكرة:

- نستخدم **برمجة ديناميكية** مع جدول 2D `dp[i][j]`
- `dp[i][j] = true` إذا كانت السلسلة من `i` إلى `j` هي Palindrome
- قاعدة تحديد Palindrome:
    - الحرف الأول يساوي الأخير، و
    - إما طول السلسلة ≤ 2 (أي حرف واحد أو حرفين متطابقين)
    - أو السلسلة الداخلية `dp[i+1][j-1]` هي Palindrome
- نحسب ونعد كل مرة نجد فيها `dp[i][j] = true`.

---

## ✅ الكود الكامل في Dart:

```dart
dart
نسختحرير
int countPalindromicSubstrings(String s) {
  int n = s.length;
  List<List<bool>> dp = List.generate(n, (_) => List.filled(n, false));
  int count = 0;

  for (int length = 1; length <= n; length++) {
    for (int start = 0; start <= n - length; start++) {
      int end = start + length - 1;

      if (s[start] == s[end]) {
        if (length <= 2) {
          dp[start][end] = true;
        } else {
          dp[start][end] = dp[start + 1][end - 1];
        }
      } else {
        dp[start][end] = false;
      }

      if (dp[start][end]) count++;
    }
  }

  return count;
}

```

---

## 🧪 تجربة:

```dart
dart
نسختحرير
void main() {
  String s = "aaa";

  print("🔄 عدد السلاسل الفرعية الباليندرومية: ${countPalindromicSubstrings(s)}");
}

```

---

## ✅ الناتج المتوقع:

```
نسختحرير
🔄 عدد السلاسل الفرعية الباليندرومية: 6

```

(السلاسل: "a", "a", "a", "aa", "aa", "aaa")

---

## 📦 التحليل:

| الخاصية | القيمة |
| --- | --- |
| الزمن | O(n²) |
| الذاكرة | O(n²) |
| النوع | Dynamic Programming |