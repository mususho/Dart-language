# Edit Distance

## 🧠 ما هي مشكلة Edit Distance؟

> نريد حساب الحد الأدنى لعدد العمليات المطلوبة لتحويل سلسلة نصية إلى أخرى. العمليات الممكنة هي:
> 
> - حذف حرف (Delete)
> - إدخال حرف (Insert)
> - استبدال حرف (Replace)

---

### ✳️ مثال:

```dart
dart
نسختحرير
Input: word1 = "horse", word2 = "ros"
Output: 3
Explanation:
horse → rorse (replace 'h' with 'r')
rorse → rose  (delete 'r')
rose → ros    (delete 'e')

```

---

## 🪜 خطوات الحل:

### ✅ الخطوة 1: إنشاء مصفوفة `dp` بحجم (len(word1)+1) × (len(word2)+1)

### ✅ الخطوة 2: تهيئة الصف الأول والعمود الأول في المصفوفة بناءً على عمليات الحذف والإدخال

### ✅ الخطوة 3: ملء باقي الخلايا حسب الحالة:

- إذا كان الحرفان متساويين، القيمة هي نفس القيمة من الخلية السابقة (بدون تعديل)
- إذا كانا مختلفين، نأخذ أقل قيمة من عمليات الحذف، الإدخال، أو الاستبدال زائد 1

### ✅ الخطوة 4: الخلية الأخيرة في المصفوفة تحتوي على النتيجة

---

## 📦 كود Dart كامل مع شرح مفصل:

```dart
dart
نسختحرير
void main() {
  String word1 = "horse";
  String word2 = "ros";

  int distance = editDistance(word1, word2);
  print("Edit Distance between \"$word1\" and \"$word2\" is: $distance");
}

/// دالة حساب المسافة التحويلية بين كلمتين (Edit Distance)
int editDistance(String word1, String word2) {
  int m = word1.length;
  int n = word2.length;

  // إنشاء مصفوفة dp بحجم (m+1) x (n+1)
  List<List<int>> dp = List.generate(m + 1, (_) => List.filled(n + 1, 0));

  // تهيئة الصف الأول (تحويل كلمة فارغة لكلمة word2)
  for (int j = 0; j <= n; j++) {
    dp[0][j] = j; // إدخال j أحرف
  }

  // تهيئة العمود الأول (تحويل word1 لكلمة فارغة)
  for (int i = 0; i <= m; i++) {
    dp[i][0] = i; // حذف i أحرف
  }

  // ملء باقي المصفوفة
  for (int i = 1; i <= m; i++) {
    for (int j = 1; j <= n; j++) {
      if (word1[i - 1] == word2[j - 1]) {
        // إذا كان الحرفان متساويين، لا نحتاج تعديل
        dp[i][j] = dp[i - 1][j - 1];
      } else {
        // حساب أقل تكلفة من العمليات الثلاث + 1
        int insertOp = dp[i][j - 1] + 1;   // إدخال حرف
        int deleteOp = dp[i - 1][j] + 1;   // حذف حرف
        int replaceOp = dp[i - 1][j - 1] + 1; // استبدال حرف

        dp[i][j] = [insertOp, deleteOp, replaceOp].reduce((a, b) => a < b ? a : b);
      }
    }
  }

  // النتيجة النهائية في الخلية الأخيرة
  return dp[m][n];
}

```

---

## 🧪 مخرجات التجربة:

```
pgsql
نسختحرير
Edit Distance between "horse" and "ros" is: 3

```

---

## 🔍 شرح تفصيلي:

| الخطوة | الوصف | الكود/التعليق |
| --- | --- | --- |
| 1 | إنشاء مصفوفة `dp` بحجم (m+1) × (n+1) | `List.generate` |
| 2 | تهيئة الصف الأول والعمود الأول | `dp[0][j] = j; dp[i][0] = i;` |
| 3 | ملء الخلايا بحساب الحد الأدنى من العمليات | `if (chars equal) dp[i][j] = dp[i-1][j-1] else min(...)` |
| 4 | قراءة القيمة النهائية من الخلية الأخيرة | `return dp[m][n];` |

---

## ✅ ملاحظات:

- الخوارزمية زمنها O(m * n)
- تحتاج مساحة O(m * n) في هذه النسخة
- يمكن تحسين استخدام الذاكرة لتصبح O(min(m,n)) إذا أردت

---