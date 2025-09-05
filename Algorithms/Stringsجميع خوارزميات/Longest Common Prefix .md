# Longest Common Prefix

## 🧠 ما هي مشكلة Longest Common Prefix؟

> معطى قائمة من السلاسل النصية (Strings)، نريد إيجاد أطول بادئة (Prefix) مشتركة بين كل هذه السلاسل.
> 

---

### ✳️ مثال:

```dart
dart
نسختحرير
Input: ["flower", "flow", "flight"]
Output: "fl"

Input: ["dog", "racecar", "car"]
Output: ""  // لا توجد بادئة مشتركة

```

---

## 🪜 خطوات الحل:

### ✅ الخطوة 1: إذا كانت القائمة فارغة، نرجع سلسلة فارغة

### ✅ الخطوة 2: نأخذ أول كلمة كبداية للبادئة المشتركة

### ✅ الخطوة 3: نمر على بقية الكلمات ونقارن البادئة الحالية مع كل كلمة ونحدث البادئة

### ✅ الخطوة 4: نعيد البادئة المشتركة النهائية

---

## 📦 كود Dart كامل مع شرح وتفصيل:

```dart
dart
نسختحرير
void main() {
  List<List<String>> testCases = [
    ["flower", "flow", "flight"],
    ["dog", "racecar", "car"],
    ["interview", "internet", "interval"],
    [],
    ["single"]
  ];

  for (var strs in testCases) {
    print("Input: $strs → Longest Common Prefix: \"${longestCommonPrefix(strs)}\"");
  }
}

/// دالة إيجاد أطول بادئة مشتركة بين قائمة كلمات
String longestCommonPrefix(List<String> strs) {
  // 🪜 الخطوة 1: تحقق إذا كانت القائمة فارغة
  if (strs.isEmpty) return "";

  // 🪜 الخطوة 2: أخذ أول كلمة كبداية للبادئة المشتركة
  String prefix = strs[0];

  // 🪜 الخطوة 3: المرور على بقية الكلمات وتحديث البادئة
  for (int i = 1; i < strs.length; i++) {
    prefix = commonPrefix(prefix, strs[i]);

    // إذا أصبحت البادئة فارغة، لا توجد بادئة مشتركة، نخرج
    if (prefix.isEmpty) {
      break;
    }
  }

  // 🪜 الخطوة 4: إعادة البادئة المشتركة
  return prefix;
}

/// دالة مساعدة لإيجاد البادئة المشتركة بين كلمتين
String commonPrefix(String str1, String str2) {
  int minLength = str1.length < str2.length ? str1.length : str2.length;
  int i = 0;

  // المرور حتى نجد أول اختلاف
  while (i < minLength && str1[i] == str2[i]) {
    i++;
  }

  // إعادة البادئة المشتركة حتى الموقع i
  return str1.substring(0, i);
}

```

---

## 🧪 مخرجات التجربة:

```
mathematica
نسختحرير
Input: [flower, flow, flight] → Longest Common Prefix: "fl"
Input: [dog, racecar, car] → Longest Common Prefix: ""
Input: [interview, internet, interval] → Longest Common Prefix: "int"
Input: [] → Longest Common Prefix: ""
Input: [single] → Longest Common Prefix: "single"

```

---

## 🔍 شرح تفصيلي:

| الجزء | الوصف |
| --- | --- |
| التحقق من القائمة | إذا كانت القائمة فارغة نرجع فارغ |
| بداية البادئة | نأخذ أول كلمة كبداية للبادئة المشتركة |
| تحديث البادئة | نمر على الكلمات ونحدث البادئة بأقصر بادئة مشتركة بين البادئة الحالية والكلمة |
| دالة commonPrefix | تقارن حرف بحرف بين كلمتين وتعيد البادئة المشتركة |

---

## ✅ ميزات الحل:

| الميزة | التوضيح |
| --- | --- |
| كفاءة جيدة | الوقت: O(S) حيث S مجموع طول كل الكلمات |
| سهل الفهم والتنفيذ | يعتمد على مقارنة مباشرة |
| مناسب للمدخلات المتوسطة والكبيرة | يمكن تحسينه بخوارزميات أخرى |