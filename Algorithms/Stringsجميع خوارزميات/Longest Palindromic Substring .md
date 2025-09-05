# Longest Palindromic Substring

## 🧠 ما هي المشكلة؟

> إعطاء نص (String)، نريد إيجاد أطول سلسلة فرعية (Substring) داخل النص تكون باليندروم (تقرأ نفسها من الأمام والخلف).
> 

---

### ✳️ مثال:

```dart
dart
نسختحرير
Input: "babad"
Output: "bab"  // أو "aba" كلاهما صحيح

Input: "cbbd"
Output: "bb"

```

---

## 🪜 خطوات الحل:

سنستخدم خوارزمية **Expand Around Center** (التوسّع حول المركز):

### ✅ الخطوة 1: لكل حرف في السلسلة، اعتبره مركزًا وحاول التوسّع في كل اتجاه

### ✅ الخطوة 2: نحاول التوسّع في شكل **باليندروم فردي الطول** (مركز واحد)

ونحاول أيضًا التوسّع في شكل **باليندروم زوجي الطول** (مركزين متجاورين)

### ✅ الخطوة 3: لكل توسع، نحسب طول السلسلة الفرعية وإذا كان أطول من السابق نخزنه

### ✅ الخطوة 4: في النهاية نعيد أطول سلسلة باليندرومية وجدوها

---

## 📦 كود Dart كامل مع شرح وتفصيل:

```dart
dart
نسختحرير
void main() {
  String s1 = "babad";
  String s2 = "cbbd";

  print("Input: $s1 → Longest Palindromic Substring: \"${longestPalindrome(s1)}\"");
  print("Input: $s2 → Longest Palindromic Substring: \"${longestPalindrome(s2)}\"");
}

/// دالة مساعدة توسع حول المركز وترجع الطول والنص للبلايندروم
String _expandAroundCenter(String s, int left, int right) {
  // توسع طالما الحدود داخل النص والحروف متساوية
  while (left >= 0 && right < s.length && s[left] == s[right]) {
    left--;
    right++;
  }

  // عند خروج الحلقة، النص من left+1 إلى right-1 هو بلايندروم
  return s.substring(left + 1, right);
}

/// الدالة الرئيسية لإيجاد أطول بلايندروم
String longestPalindrome(String s) {
  if (s.isEmpty) return "";

  String longest = "";

  // تمرير على كل حرف كمرکز توسع
  for (int i = 0; i < s.length; i++) {
    // 1. التوسّع حول مركز واحد (باليندروم فردي الطول)
    String oddPalindrome = _expandAroundCenter(s, i, i);

    // 2. التوسّع حول مركزين (باليندروم زوجي الطول)
    String evenPalindrome = _expandAroundCenter(s, i, i + 1);

    // اختيار أطول منهما
    String longerPalindrome =
        oddPalindrome.length > evenPalindrome.length ? oddPalindrome : evenPalindrome;

    // تحديث الأطول حتى الآن إذا وجدنا أطول
    if (longerPalindrome.length > longest.length) {
      longest = longerPalindrome;
    }
  }

  return longest;
}

```

---

## 🧪 مخرجات التجربة:

```
mathematica
نسختحرير
Input: babad → Longest Palindromic Substring: "bab"
Input: cbbd → Longest Palindromic Substring: "bb"

```

---

## 🔍 شرح تفصيلي:

| الجزء | الوصف | الكود / توضيح |
| --- | --- | --- |
| 1 | نمر على كل حرف في النص كمركز توسع | `for (int i = 0; i < s.length; i++)` |
| 2 | توسع فردي الطول (مرکز واحد) | `_expandAroundCenter(s, i, i)` |
| 3 | توسع زوجي الطول (مرکزين متجاورين) | `_expandAroundCenter(s, i, i + 1)` |
| 4 | نأخذ الأطول من الاثنين | `longerPalindrome = ...` |
| 5 | نحفظ الأطول من كل ما وجدنا | `if (longerPalindrome.length > longest.length)` |
| 6 | دالة التوسّع تستمر طالما الأحرف متساوية | `while (left >= 0 && right < s.length && s[left] == s[right])` |

---

## ✅ ميزات الحل:

| الميزة | التوضيح |
| --- | --- |
| كفاءة | زمن التنفيذ O(n²) (مناسب لمعظم الحالات) |
| سهولة الفهم | لا تحتاج تخزين معقد أو خوارزميات متقدمة |
| مرونة | يمكن تعديلها بسهولة |

---

## 📝 ملاحظة:

الخوارزمية جيدة للمدخلات المتوسطة. إذا كنت تريد خوارزمية أكثر كفاءة (O(n)) مثل Manacher's algorithm، يمكنني شرحها لاحقًا.