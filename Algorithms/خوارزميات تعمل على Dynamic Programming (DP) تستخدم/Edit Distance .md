# Edit Distance

## ✏️ Edit Distance (Levenshtein Distance)

**(مسافة التحرير - أقل عدد من العمليات لتحويل سلسلة إلى أخرى)**

---

## 🎯 الهدف:

> إعطاء سلسلتين نصيتين s1 و s2، نريد حساب أقل عدد من العمليات اللازمة لتحويل s1 إلى s2.
> 

---

## 🔧 العمليات المسموحة:

- **إضافة حرف**
- **حذف حرف**
- **استبدال حرف**

---

## 📌 مثال:

```dart
dart
نسختحرير
String s1 = "horse";
String s2 = "ros";

```

التحويلات:

- horse → rorse (استبدال 'h' بـ 'r')
- rorse → rose (حذف 'r')
- rose → ros (حذف 'e')

الإجمالي: 3 عمليات

---

## 🧠 الفكرة (DP Tabulation):

- نستخدم جدول 2D `dp[i][j]` يمثل أقل عدد من العمليات لتحويل أول `i` أحرف من `s1` إلى أول `j` أحرف من `s2`.

### القاعدة:

- إذا كان الحرفان متساويين:
    
    `dp[i][j] = dp[i-1][j-1]`
    
- إذا مختلفين:
    
    `dp[i][j] = 1 + min(`
    
    `dp[i-1][j]` (حذف)،
    
    `dp[i][j-1]` (إضافة)،
    
    `dp[i-1][j-1]` (استبدال)
    
    `)`
    

---

## ✅ الكود الكامل في Dart:

```dart
dart
نسختحرير
int editDistance(String s1, String s2) {
  int m = s1.length;
  int n = s2.length;

  List<List<int>> dp = List.generate(
    m + 1,
    (_) => List.filled(n + 1, 0),
  );

  // الحالات القاعدية
  for (int i = 0; i <= m; i++) dp[i][0] = i; // حذف كل الحروف
  for (int j = 0; j <= n; j++) dp[0][j] = j; // إضافة كل الحروف

  for (int i = 1; i <= m; i++) {
    for (int j = 1; j <= n; j++) {
      if (s1[i - 1] == s2[j - 1]) {
        dp[i][j] = dp[i - 1][j - 1];
      } else {
        dp[i][j] = 1 +
            [
              dp[i - 1][j],     // حذف
              dp[i][j - 1],     // إضافة
              dp[i - 1][j - 1]  // استبدال
            ].reduce((a, b) => a < b ? a : b);
      }
    }
  }

  return dp[m][n];
}

```

---

## 🧪 تجربة:

```dart
dart
نسختحرير
void main() {
  String s1 = "horse";
  String s2 = "ros";

  print("✏️ Edit Distance: ${editDistance(s1, s2)}");
}

```

---

## ✅ الناتج المتوقع:

```
yaml
نسختحرير
✏️ Edit Distance: 3

```

---

## 📦 التحليل:

| الخاصية | القيمة |
| --- | --- |
| الزمن | O(m * n) |
| الذاكرة | O(m * n) |
| نوع | Tabulation DP |