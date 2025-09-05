# Anagram Check

## 🧠 ما هو الـ Anagram؟

> كلمتان تعتبران Anagrams إذا كانتا تحتويان على نفس الأحرف بنفس الكمية ولكن بترتيب مختلف.
> 

---

### ✳️ أمثلة:

| الكلمة 1 | الكلمة 2 | Anagram؟ |
| --- | --- | --- |
| `listen` | `silent` | ✅ نعم |
| `heart` | `earth` | ✅ نعم |
| `hello` | `world` | ❌ لا |
| `Triangle` | `Integral` | ✅ نعم (مع تجاهل الأحرف الكبيرة والصغيرة) |

---

## 🪜 خطوات إنشاء الخوارزمية:

### ✅ الخطوة 1: تنظيف الكلمتين (إزالة الفراغات، وتوحيد الأحرف إلى صغيرة)

> لأننا نتجاهل حالة الحرف والمسافات
> 

### ✅ الخطوة 2: التحقق من تساوي الطول

> لأن كلمتين بـ Anagram يجب أن يكون لهما نفس عدد الأحرف
> 

### ✅ الخطوة 3: إنشاء خريطتي تكرار (Map) لكل كلمة

> المفتاح = الحرف، القيمة = عدد مرات ظهوره
> 

### ✅ الخطوة 4: مقارنة الخريطتين

> إذا تساوت في المفاتيح والقيم، فهما Anagram
> 

---

## 📦 الكود الكامل مع الشرح والتعليق:

```dart
dart
نسختحرير
// 🟢 نقطة البداية
void main() {
  // أمثلة لاختبار الدالة
  List<List<String>> testCases = [
    ["listen", "silent"],
    ["hello", "world"],
    ["Triangle", "Integral"],
    ["a gentleman", "elegant man"],
    ["rat", "car"]
  ];

  // تنفيذ الدالة على كل زوج كلمات
  for (var pair in testCases) {
    String str1 = pair[0];
    String str2 = pair[1];
    bool result = areAnagrams(str1, str2);

    print("🧪 \"$str1\" و \"$str2\" → ${result ? '✅ Anagram' : '❌ Not Anagram'}");
  }
}

/// ✅ دالة التحقق من كون الكلمتين Anagrams
bool areAnagrams(String str1, String str2) {
  // -------------------------------
  // 🪜 الخطوة 1: تنظيف السلاسل
  // نحذف الفراغات ونحوّل الأحرف إلى صغيرة
  String clean1 = str1.replaceAll(RegExp(r'\s+'), '').toLowerCase();
  String clean2 = str2.replaceAll(RegExp(r'\s+'), '').toLowerCase();

  // -------------------------------
  // 🪜 الخطوة 2: التحقق من تساوي الطول بعد التنظيف
  if (clean1.length != clean2.length) return false;

  // -------------------------------
  // 🪜 الخطوة 3: إنشاء خريطتي تكرار لكل حرف
  Map<String, int> countMap1 = {};
  Map<String, int> countMap2 = {};

  for (var ch in clean1.split('')) {
    countMap1[ch] = (countMap1[ch] ?? 0) + 1;
  }

  for (var ch in clean2.split('')) {
    countMap2[ch] = (countMap2[ch] ?? 0) + 1;
  }

  // -------------------------------
  // 🪜 الخطوة 4: مقارنة الخريطتين
  if (countMap1.length != countMap2.length) return false;

  for (var entry in countMap1.entries) {
    String key = entry.key;
    int value = entry.value;

    if (countMap2[key] != value) {
      return false;
    }
  }

  // -------------------------------
  // ✅ إذا وصلت هنا، الكلمتان Anagrams
  return true;
}

```

---

## 🧪 مخرجات التجربة:

```bash
bash
نسختحرير
🧪 "listen" و "silent" → ✅ Anagram
🧪 "hello" و "world" → ❌ Not Anagram
🧪 "Triangle" و "Integral" → ✅ Anagram
🧪 "a gentleman" و "elegant man" → ✅ Anagram
🧪 "rat" و "car" → ❌ Not Anagram

```

---

## 🔍 شرح عملي للكود:

### 1. التنظيف:

```dart
dart
نسختحرير
str1.replaceAll(RegExp(r'\s+'), '').toLowerCase();

```

- إزالة الفراغات
- توحيد حالة الأحرف

---

### 2. إنشاء خريطة تكرار:

```dart
dart
نسختحرير
for (var ch in clean1.split('')) {
  countMap1[ch] = (countMap1[ch] ?? 0) + 1;
}

```

- كل حرف يمثل مفتاحًا
- كل مرة يظهر فيها الحرف نزيد العداد

---

### 3. المقارنة:

```dart
dart
نسختحرير
if (countMap2[key] != value) return false;

```

- إذا لم تتطابق القيم أو المفتاح غير موجود → فليس Anagram

---

## ✅ مزايا الحل:

| الميزة | التفاصيل |
| --- | --- |
| كفاءة عالية | الزمن: O(n) |
| تجاهل للحالة والمسافات | مفيد للجمل وليس الكلمات فقط |
| قابل للتعميم | يمكنك جعله يعمل مع Unicode بسهولة |

---

## 🔁 كود مبسط باستخدام الترتيب فقط (بديل سريع):

```dart
dart
نسختحرير
bool areAnagramsSimple(String a, String b) {
  var cleanA = a.replaceAll(RegExp(r'\s+'), '').toLowerCase();
  var cleanB = b.replaceAll(RegExp(r'\s+'), '').toLowerCase();

  if (cleanA.length != cleanB.length) return false;

  var sortedA = cleanA.split('')..sort();
  var sortedB = cleanB.split('')..sort();

  return sortedA.join() == sortedB.join();
}

```

> لكن هذا أبطأ قليلًا بسبب sort() والتي تأخذ O(n log n)
> 

---

## ✅ الخلاصة:

| الخطوة | الشرح |
| --- | --- |
| 1 | تنظيف السلسلة من الفراغات والأحرف الكبيرة |
| 2 | التحقق من تساوي الطول |
| 3 | عدّ الأحرف لكل سلسلة |
| 4 | مقارنة عدد مرات الظهور |
| 5 | النتيجة = هل هما متماثلتان؟ |