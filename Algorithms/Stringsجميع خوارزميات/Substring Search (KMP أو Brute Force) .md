# Substring Search (KMP أو Brute Force)

# 1. طريقة Brute Force (البحث البسيط)

---

## 🧠 فكرة الخوارزمية:

نبحث عن ظهور النمط (pattern) داخل النص (text) عن طريق فحص كل موقع في النص بشكل متتابع ونقارن الأحرف.

---

## 🪜 خطوات الحل:

- نمر على كل موقع ممكن في النص (حتى `text.length - pattern.length`)
- في كل موقع نقارن حرف بحرف مع النمط
- إذا وجدنا تطابق كامل، نرجع موقع البداية
- إذا لم نجد نرجع -1

---

## كود Dart مع شرح:

```dart
dart
نسختحرير
int bruteForceSearch(String text, String pattern) {
  int n = text.length;
  int m = pattern.length;

  // المرور على كل موقع محتمل
  for (int i = 0; i <= n - m; i++) {
    int j = 0;

    // مقارنة الأحرف مع النمط
    while (j < m && text[i + j] == pattern[j]) {
      j++;
    }

    // إذا وصلنا لنهاية النمط، وجدنا التطابق
    if (j == m) {
      return i; // موقع بداية التطابق
    }
  }

  // لم نجد التطابق
  return -1;
}

```

---

# 2. خوارزمية KMP (Knuth-Morris-Pratt)

---

## 🧠 فكرة الخوارزمية:

تحسن عملية البحث عن طريق بناء مصفوفة **LPS (Longest Prefix Suffix)** التي تخبرنا إلى أي موقع نعود عندما يحدث تعارض أثناء المقارنة، دون الحاجة للرجوع للنص بشكل كامل.

---

## 🪜 خطوات الحل:

- بناء مصفوفة LPS للنمط (تحسب أطول بادئة هي أيضًا لاحقة لكل موقع)
- المرور على النص مع مؤشر ونمط مع مؤشر آخر
- إذا تطابق حرفان نتحرك للأمام
- إذا تعارضنا نستخدم LPS للانتقال بمؤشر النمط فقط

---

## كود Dart مفصل مع تعليقات:

```dart
dart
نسختحرير
// دالة لبناء مصفوفة LPS
List<int> buildLPS(String pattern) {
  int length = 0; // طول البادئة القصوى التي هي لاحقة
  int i = 1;
  List<int> lps = List.filled(pattern.length, 0);

  while (i < pattern.length) {
    if (pattern[i] == pattern[length]) {
      length++;
      lps[i] = length;
      i++;
    } else {
      if (length != 0) {
        length = lps[length - 1];
      } else {
        lps[i] = 0;
        i++;
      }
    }
  }

  return lps;
}

// دالة البحث باستخدام KMP
int kmpSearch(String text, String pattern) {
  int n = text.length;
  int m = pattern.length;

  if (m == 0) return 0; // نمط فارغ => موقع 0

  List<int> lps = buildLPS(pattern);

  int i = 0; // مؤشر النص
  int j = 0; // مؤشر النمط

  while (i < n) {
    if (text[i] == pattern[j]) {
      i++;
      j++;
    }

    if (j == m) {
      // وجدنا النمط كاملاً
      return i - j;
    } else if (i < n && text[i] != pattern[j]) {
      if (j != 0) {
        j = lps[j - 1];
      } else {
        i++;
      }
    }
  }

  return -1; // لم نجد تطابق
}

```

---

## اختبار الخوارزميات:

```dart
dart
نسختحرير
void main() {
  String text = "abxabcabcaby";
  String pattern = "abcaby";

  print("Brute Force Search index: ${bruteForceSearch(text, pattern)}");
  print("KMP Search index: ${kmpSearch(text, pattern)}");
}

```

---

## 🧪 مخرجات:

```
pgsql
نسختحرير
Brute Force Search index: 6
KMP Search index: 6

```

---

## ملخص:

| الطريقة | الوقت في أسوأ الحالات | الفكرة الأساسية |
| --- | --- | --- |
| Brute Force | O(n*m) | مقارنة حرف بحرف في كل موقع |
| KMP | O(n + m) | استخدام مصفوفة LPS لتجنب التكرار |