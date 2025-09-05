# Letter Combinations of Phone Number

## 📞 Letter Combinations of Phone Number

**(توليد كل تركيبات الحروف الممكنة لرقم هاتف)**

---

## 🎯 الهدف:

> إعطاء سلسلة رقمية digits (من 2 إلى 9)،
> 
> 
> نريد توليد كل تركيبات الحروف الممكنة التي يمكن أن تمثلها هذه الأرقام على لوحة المفاتيح (مثل: 2 → "abc", 3 → "def"، وهكذا).
> 

---

## 🧠 الفكرة (Backtracking):

- لكل رقم نستبدله بمجموعة الحروف المقابلة.
- ننتقل رقم رقم ونضيف الحروف واحدًا تلو الآخر.
- نستخدم استدعاء ذاتي لبناء كل التركيبات الممكنة.

---

## ✅ الكود الكامل في Dart:

```dart
dart
نسختحرير
List<String> letterCombinations(String digits) {
  if (digits.isEmpty) return [];

  Map<String, String> phoneMap = {
    '2': 'abc',
    '3': 'def',
    '4': 'ghi',
    '5': 'jkl',
    '6': 'mno',
    '7': 'pqrs',
    '8': 'tuv',
    '9': 'wxyz',
  };

  List<String> result = [];
  StringBuffer current = StringBuffer();

  void backtrack(int index) {
    if (index == digits.length) {
      result.add(current.toString());
      return;
    }

    String letters = phoneMap[digits[index]] ?? '';
    for (int i = 0; i < letters.length; i++) {
      current.write(letters[i]);
      backtrack(index + 1);
      current.length = current.length - 1; // تراجع
    }
  }

  backtrack(0);
  return result;
}

```

---

## 🧪 تجربة:

```dart
dart
نسختحرير
void main() {
  String digits = "23";

  List<String> combos = letterCombinations(digits);

  print("📞 كل تركيبات الحروف لرقم $digits:");
  for (var combo in combos) {
    print(combo);
  }
}

```

---

## ✅ الناتج المتوقع:

```
bash
نسختحرير
ad
ae
af
bd
be
bf
cd
ce
cf

```

---

## 📦 التحليل:

| الخاصية | القيمة |
| --- | --- |
| الزمن | O(3^n * 4^m) حيث n هو عدد الأرقام التي لها 3 أحرف و m عدد الأرقام التي لها 4 أحرف |
| الذاكرة | O(n) |
| النوع | Backtracking |