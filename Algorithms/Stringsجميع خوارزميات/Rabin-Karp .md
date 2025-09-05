# Rabin-Karp

## 🧠 ما هي خوارزمية Rabin-Karp؟

> خوارزمية Rabin-Karp تستخدم التجزئة (Hashing) للبحث عن نمط داخل نص بشكل سريع، عن طريق حساب قيمة تجزئة للنمط وقيم تجزئة للنص في مواقع مختلفة، ثم مقارنة هذه القيم قبل مقارنة الأحرف فعليًا لتقليل عمليات المقارنة المكلفة.
> 

---

### ✳️ الفكرة الأساسية:

- نحسب تجزئة (hash) للنمط.
- نحسب تجزئة لكل نافذة من النص بنفس طول النمط (using rolling hash).
- إذا تطابقت التجزئات، نقوم بمقارنة الأحرف حرف بحرف للتحقق من التطابق.
- استخدام تجزئة متجددة (rolling hash) لتحديث قيمة التجزئة عند الانتقال للنافذة التالية بسرعة.

---

## 🪜 خطوات الحل:

### ✅ الخطوة 1: اختيار قاعدة و MOD (لتقليل الاصطدام)

### ✅ الخطوة 2: حساب تجزئة النمط وتجزئة أول نافذة في النص

### ✅ الخطوة 3: المرور على النص مع تحديث التجزئة لكل نافذة

### ✅ الخطوة 4: إذا تطابقت التجزئات نقوم بمقارنة الأحرف

---

## 📦 كود Dart كامل مع شرح مفصل وتعليقات:

```dart
dart
نسختحرير
int rabinKarpSearch(String text, String pattern) {
  int n = text.length;
  int m = pattern.length;

  if (m == 0 || m > n) return -1;

  const int base = 256; // عدد الأحرف الممكنة (مثلاً 256 للـ ASCII)
  const int mod = 101;  // عدد أولي كبير لتقليل الاصطدامات

  // حساب قيمة base^(m-1) % mod لاستخدامها في rolling hash
  int highOrder = 1;
  for (int i = 0; i < m - 1; i++) {
    highOrder = (highOrder * base) % mod;
  }

  // حساب تجزئة النمط وتجزيء أول نافذة من النص
  int patternHash = 0;
  int windowHash = 0;

  for (int i = 0; i < m; i++) {
    patternHash = (base * patternHash + pattern.codeUnitAt(i)) % mod;
    windowHash = (base * windowHash + text.codeUnitAt(i)) % mod;
  }

  // المرور على النص ومقارنة التجزئات
  for (int i = 0; i <= n - m; i++) {
    // إذا تطابقت التجزئات، نقارن حرف بحرف للتأكد
    if (patternHash == windowHash) {
      bool match = true;
      for (int j = 0; j < m; j++) {
        if (text[i + j] != pattern[j]) {
          match = false;
          break;
        }
      }
      if (match) {
        return i; // وجدنا التطابق عند الموقع i
      }
    }

    // تحديث التجزئة للنص للنافذة التالية (rolling hash)
    if (i < n - m) {
      windowHash = (base * (windowHash - text.codeUnitAt(i) * highOrder) + text.codeUnitAt(i + m)) % mod;

      // التأكد من أن التجزئة ليست سالبة
      if (windowHash < 0) {
        windowHash += mod;
      }
    }
  }

  // لم نجد تطابق
  return -1;
}

```

---

## اختبار الخوارزمية:

```dart
dart
نسختحرير
void main() {
  String text = "abxabcabcaby";
  String pattern = "abcaby";

  int index = rabinKarpSearch(text, pattern);
  if (index != -1) {
    print("تم العثور على النمط في الموقع: $index");
  } else {
    print("النمط غير موجود في النص.");
  }
}

```

---

## 🧪 مخرجات:

```
نسختحرير
تم العثور على النمط في الموقع: 6

```

---

## شرح إضافي:

| المتغير | الشرح |
| --- | --- |
| base | عدد الأحرف الممكنة (مثلاً 256 للـ ASCII) |
| mod | عدد أولي كبير لتقليل الاصطدامات في التجزئة |
| highOrder | قيمة `base^(m-1) % mod` لتحديث التجزئة |
| patternHash | التجزئة الخاصة بالنمط |
| windowHash | التجزئة الخاصة بالنافذة الحالية من النص |

---

## مزايا Rabin-Karp:

| الميزة | الشرح |
| --- | --- |
| سرعة في المتوسط | أفضل من Brute Force عندما يكون النص كبير |
| مقارنة أقل | تجزئة أولًا ثم مقارنة إذا تطابقت التجزئات |
| مناسب للبحث عن عدة أنماط | يمكن تعديل الخوارزمية للبحث عن عدة أنماط في نفس النص |