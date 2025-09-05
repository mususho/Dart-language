# Palindrome Check

## 🧠 ما هو الـ Palindrome؟

> الـ Palindrome هو كلمة أو جملة تقرأ نفسها بالعكس تمامًا (من اليسار إلى اليمين ومن اليمين إلى اليسار).
> 

### ✳️ أمثلة:

| الإدخال | Palindrome؟ |
| --- | --- |
| `racecar` | ✅ نعم |
| `level` | ✅ نعم |
| `hello` | ❌ لا |
| `A man a plan a canal Panama` | ✅ نعم (مع تجاهل الفراغات والأحرف الكبيرة) |

---

## 🪜 خطوات إنشاء الخوارزمية:

### ✅ الخطوة 1: تنظيف السلسلة (إزالة الفراغات وتحويل الأحرف إلى صغيرة)

> لتجاهل الفروقات في الحروف والفراغات
> 

### ✅ الخطوة 2: استخدام مؤشرين `start` و `end` لمقارنة الحروف

> إذا اختلف أي حرف من الطرفين → ليست Palindrome
> 

### ✅ الخطوة 3: الاستمرار بالمقارنة حتى يتقاطع المؤشران

---

## 📦 الكود الكامل مع الشرح المفصل:

```dart
dart
نسختحرير
// 🟢 الدالة الرئيسية لتجربة الخوارزمية
void main() {
  // أمثلة متنوعة لاختبار الدالة
  List<String> testCases = [
    "racecar",
    "Level",
    "A man a plan a canal Panama",
    "Hello",
    "No lemon no melon"
  ];

  for (String input in testCases) {
    bool result = isPalindrome(input);
    print("🧪 \"$input\" → ${result ? '✅ Palindrome' : '❌ Not Palindrome'}");
  }
}

/// ✅ دالة التحقق من كون النص Palindrome
bool isPalindrome(String text) {
  // -------------------------------
  // 🪜 الخطوة 1: تنظيف السلسلة
  // إزالة الفراغات وتحويل إلى أحرف صغيرة
  String cleaned = text
      .replaceAll(RegExp(r'\s+'), '') // إزالة كل الفراغات
      .toLowerCase(); // تحويل إلى حروف صغيرة

  // -------------------------------
  // 🪜 الخطوة 2: تعريف مؤشرين لبداية ونهاية السلسلة
  int start = 0;
  int end = cleaned.length - 1;

  // -------------------------------
  // 🪜 الخطوة 3: المقارنة بين الأحرف من الطرفين
  while (start < end) {
    if (cleaned[start] != cleaned[end]) {
      // ❌ إذا اختلف الحرفان → ليست Palindrome
      return false;
    }

    // 📝 تحريك المؤشرات
    start++;
    end--;
  }

  // ✅ إذا مررنا من كل الحروف بدون اختلاف → Palindrome
  return true;
}

```

---

## 🧪 مخرجات التجربة:

```bash
bash
نسختحرير
🧪 "racecar" → ✅ Palindrome
🧪 "Level" → ✅ Palindrome
🧪 "A man a plan a canal Panama" → ✅ Palindrome
🧪 "Hello" → ❌ Not Palindrome
🧪 "No lemon no melon" → ✅ Palindrome

```

---

## 🔍 الشرح حسب الخطوات:

| الخطوة | التفسير | الكود |
| --- | --- | --- |
| 1 | تنظيف السلسلة | `replaceAll` و `toLowerCase` |
| 2 | المقارنة بين الأحرف الأولى والأخيرة | `cleaned[start] != cleaned[end]` |
| 3 | إذا اختلفت → ليست Palindrome | `return false;` |
| 4 | إذا انتهت الحلقة بدون اختلاف | `return true;` |

---

## ✅ مزايا هذا الحل:

| الميزة | الشرح |
| --- | --- |
| كفاءة عالية | زمن التنفيذ O(n) |
| لا حاجة إلى تخزين إضافي كبير | فقط مؤشرين ومقارنة مباشرة |
| معالجة قوية للجمل | حذف الفراغات وتجاهل الحروف الكبيرة |

---

## 🔁 نسخة مبسطة بدون تنظيف:

إذا كنت تريد فقط مقارنة نص حرفي بدون تجاهل الفراغات والحروف الكبيرة:

```dart
dart
نسختحرير
bool isStrictPalindrome(String text) {
  int start = 0;
  int end = text.length - 1;

  while (start < end) {
    if (text[start] != text[end]) return false;
    start++;
    end--;
  }

  return true;
}

```

---

## 🎁 هل تريد نسخة تتجاهل علامات الترقيم؟

يمكن تعديل `cleaned` ليصبح:

```dart
dart
نسختحرير
String cleaned = text
    .replaceAll(RegExp(r'[^a-zA-Z0-9]'), '') // يحذف كل ما عدا الحروف والأرقام
    .toLowerCase();

```

---

## ✅ الخلاصة:

| المرحلة | العمل |
| --- | --- |
| التنظيف | إزالة الفراغات وتوحيد الأحرف |
| المقارنة | من الطرفين نحو المركز |
| القرار | هل تطابق الجميع؟ نعم = Palindrome |