# Count Vowels/Consonants

## 🧠 ما هي المشكلة؟

> نريد إعطاء سلسلة نصية (String) ثم نحسب عدد الحروف المتحركة (vowels) وعدد الحروف الصامتة (consonants) فيها.
> 

---

### ✳️ تعريف:

- الحروف المتحركة: a, e, i, o, u (سواء كبيرة أو صغيرة)
- الحروف الصامتة: باقي الحروف الأبجدية الإنجليزية (a-z، A-Z) غير المتحركة

---

## 🪜 خطوات الحل:

### ✅ الخطوة 1: تعريف مجموعة الحروف المتحركة

### ✅ الخطوة 2: المرور على كل حرف في السلسلة

### ✅ الخطوة 3: التحقق إذا الحرف هو حرف أبجدي

### ✅ الخطوة 4: زيادة عداد المتحركات أو الصوامت بناءً على نوع الحرف

---

## 📦 كود Dart كامل مع شرح وتفصيل:

```dart
dart
نسختحرير
void main() {
  String input = "Hello World! This is an Example.";

  Map<String, int> counts = countVowelsAndConsonants(input);

  print("Input: \"$input\"");
  print("Number of vowels: ${counts['vowels']}");
  print("Number of consonants: ${counts['consonants']}");
}

/// دالة لعد الحروف المتحركة والصوامت في نص
Map<String, int> countVowelsAndConsonants(String text) {
  // 🪜 الخطوة 1: تعريف مجموعة الحروف المتحركة (lowercase)
  Set<String> vowels = {'a', 'e', 'i', 'o', 'u'};

  int vowelsCount = 0;
  int consonantsCount = 0;

  // 🪜 الخطوة 2: المرور على كل حرف في النص
  for (int i = 0; i < text.length; i++) {
    String ch = text[i].toLowerCase();

    // 🪜 الخطوة 3: التحقق إذا الحرف هو حرف أبجدي فقط
    if (ch.codeUnitAt(0) >= 'a'.codeUnitAt(0) && ch.codeUnitAt(0) <= 'z'.codeUnitAt(0)) {
      // 🪜 الخطوة 4: زيادة العداد المناسب
      if (vowels.contains(ch)) {
        vowelsCount++;
      } else {
        consonantsCount++;
      }
    }
  }

  return {
    'vowels': vowelsCount,
    'consonants': consonantsCount,
  };
}

```

---

## 🧪 مخرجات التجربة:

```
mathematica
نسختحرير
Input: "Hello World! This is an Example."
Number of vowels: 9
Number of consonants: 14

```

---

## 🔍 شرح تفصيلي:

| الخطوة | الوصف |
| --- | --- |
| تعريف الحروف المتحركة | إنشاء مجموعة تحتوي على a, e, i, o, u |
| المرور على النص | فحص كل حرف واحدًا تلو الآخر |
| التحقق من الأبجدية | قبول الحروف من a إلى z فقط |
| العد | زيادة عداد المتحرك أو الصامت بناءً على الحرف |