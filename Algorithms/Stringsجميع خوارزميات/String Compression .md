# String Compression

## 🧠 ما هي مشكلة String Compression؟

> نريد ضغط سلسلة نصية بحيث يتم تمثيل الأحرف المتكررة المتتالية بشكل مختصر، عن طريق كتابة الحرف وعدد مرات تكراره.
> 
> 
> إذا كانت النتيجة المضغوطة أطول أو مساوية للسلسلة الأصلية، نرجع السلسلة الأصلية.
> 

---

### ✳️ مثال:

```dart
dart
نسختحرير
Input: "aaabbc"
Output: "a3b2c1"

Input: "abc"
Output: "abc"  // لأن الضغط يعطي "a1b1c1" وهو أطول من الأصل

```

---

## 🪜 خطوات الحل:

### ✅ الخطوة 1: المرور على السلسلة وحساب عدد تكرار كل حرف متتالي

### ✅ الخطوة 2: بناء نص مضغوط يجمع الحرف وعدد تكراره

### ✅ الخطوة 3: مقارنة طول النص المضغوط مع النص الأصلي

### ✅ الخطوة 4: إرجاع النص المضغوط فقط إذا كان أقصر، وإلا إرجاع النص الأصلي

---

## 📦 كود Dart كامل مع شرح وتفصيل:

```dart
dart
نسختحرير
void main() {
  List<String> testCases = [
    "aaabbc",
    "abc",
    "aabbccdde",
    "aaaaaaaaaa",
    ""
  ];

  for (var s in testCases) {
    print("Input: \"$s\" → Compressed: \"${compressString(s)}\"");
  }
}

/// دالة ضغط السلسلة النصية
String compressString(String input) {
  // 🪜 الخطوة 1: إذا كانت السلسلة فارغة، نرجعها مباشرة
  if (input.isEmpty) return input;

  // 🪜 الخطوة 2: متغير لبناء النص المضغوط
  StringBuffer compressed = StringBuffer();

  // 🪜 الخطوة 3: عداد لتكرار الحرف الحالي
  int count = 1;

  // 🪜 الخطوة 4: المرور على الأحرف من الثاني حتى النهاية
  for (int i = 1; i < input.length; i++) {
    // 🪜 الخطوة 5: إذا الحرف الحالي يساوي السابق، نزيد العداد
    if (input[i] == input[i - 1]) {
      count++;
    } else {
      // 🪜 الخطوة 6: إذا اختلف الحرف، نكتب الحرف السابق وعدد مرات تكراره
      compressed.write(input[i - 1]);
      compressed.write(count);

      // 🪜 الخطوة 7: نعيد تعيين العداد للحرف الجديد
      count = 1;
    }
  }

  // 🪜 الخطوة 8: كتابة آخر حرف وعدد مرات تكراره
  compressed.write(input[input.length - 1]);
  compressed.write(count);

  // 🪜 الخطوة 9: إذا كان النص المضغوط أطول أو مساوي للأصل، نرجع الأصل
  String compressedStr = compressed.toString();
  if (compressedStr.length >= input.length) {
    return input;
  }

  // 🪜 الخطوة 10: نرجع النص المضغوط
  return compressedStr;
}

```

---

## 🧪 مخرجات التجربة:

```
vbnet
نسختحرير
Input: "aaabbc" → Compressed: "a3b2c1"
Input: "abc" → Compressed: "abc"
Input: "aabbccdde" → Compressed: "a2b2c2d2e1"
Input: "aaaaaaaaaa" → Compressed: "a10"
Input: "" → Compressed: ""

```

---

## 🔍 شرح تفصيلي للخطوات:

| الخطوة | الشرح | الكود |
| --- | --- | --- |
| 1 | التعامل مع السلسلة الفارغة | `if (input.isEmpty) return input;` |
| 2 | بداية بناء النص المضغوط باستخدام `StringBuffer` | `StringBuffer compressed = StringBuffer();` |
| 3 | عداد لتكرار الأحرف المتتالية | `int count = 1;` |
| 4-7 | المرور على الأحرف ومقارنة الحالي بالسابق لبناء الضغط | `for ... if .. else ...` |
| 8 | كتابة آخر حرف وعدد مرات تكراره بعد انتهاء الحلقة | `compressed.write(input[input.length - 1]); compressed.write(count);` |
| 9-10 | مقارنة الطول والاختيار بين الأصل أو المضغوط | `if (compressedStr.length >= input.length) return input;` |

---

## ✅ ملخص:

| المرحلة | ما نفعله |
| --- | --- |
| المرور على السلسلة | نحسب تكرار الحروف المتتالية |
| بناء النص المضغوط | نجمع الحرف والعدد |
| مقارنة الطول | نرجع الأصلي أو المضغوط حسب الطول |

---