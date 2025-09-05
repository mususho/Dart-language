# Grouping Elements

## ✅ ما هي خوارزمية Grouping Elements؟

هي خوارزمية تقوم بـ **تجميع العناصر حسب خاصية مشتركة** بينها. على سبيل المثال:

- تجميع الكلمات حسب أول حرف
- تجميع الأرقام حسب الزوجي والفردي
- تجميع العناصر حسب تكرارها
- تجميع الكائنات حسب التصنيف أو النوع

---

### 🎯 مثال واقعي:

```dart
dart
CopyEdit
List<String> names = ['Alice', 'Ahmed', 'Bob', 'Amal', 'Bashar'];

```

نريد تجميع الأسماء حسب أول حرف:

```
makefile
CopyEdit
A: [Alice, Ahmed, Amal]
B: [Bob, Bashar]

```

---

## ✳️ خطوات بناء الخوارزمية:

1. تعريف خريطة (`Map`) لتخزين المجموعات.
2. المرور على كل عنصر في القائمة.
3. تحديد الـ **مفتاح التجميع** (مثل: أول حرف، النوع، الرقم، إلخ).
4. إذا لم يكن المفتاح موجودًا في الخريطة → نضيفه مع قائمة جديدة.
5. نضيف العنصر إلى المجموعة المناسبة.
6. في النهاية نعيد أو نطبع الخريطة.

---

## 🧾 كود Dart كامل وطويل مشروح خطوة بخطوة:

### 🧪 الحالة 1: تجميع كلمات حسب أول حرف

```dart
dart
CopyEdit
// الخطوة 1: تعريف دالة لتجميع الكلمات حسب أول حرف
Map<String, List<String>> groupByFirstLetter(List<String> words) {
  // الخطوة 2: إنشاء خريطة للتجميع
  Map<String, List<String>> grouped = {};

  // الخطوة 3: المرور على كل كلمة في القائمة
  for (String word in words) {
    if (word.isEmpty) continue; // تخطى الكلمات الفارغة

    // الخطوة 4: تحديد مفتاح التجميع (الحرف الأول)
    String key = word[0].toUpperCase(); // يمكن جعله case-insensitive

    // الخطوة 5: إذا لم يكن المفتاح موجود، أنشئ قائمة جديدة
    if (!grouped.containsKey(key)) {
      grouped[key] = [];
    }

    // الخطوة 6: أضف الكلمة إلى المجموعة المناسبة
    grouped[key]!.add(word);
  }

  // الخطوة 7: إرجاع خريطة التجميع
  return grouped;
}

// الخطوة 8: دالة لطباعة النتائج بشكل منسق
void printGroupedWords(Map<String, List<String>> grouped) {
  for (var entry in grouped.entries) {
    print("المجموعة '${entry.key}': ${entry.value}");
  }
}

// الخطوة 9: تجربة الخوارزمية في دالة main
void main() {
  // قائمة من الأسماء
  List<String> names = ['Alice', 'Ahmed', 'Bob', 'Amal', 'Bashar', 'adam', 'Brian', ''];

  // تطبيق الدالة
  Map<String, List<String>> result = groupByFirstLetter(names);

  // طباعة النتيجة
  print("نتيجة التجميع حسب أول حرف:");
  printGroupedWords(result);
}

```

---

## 🧪 الإخراج المتوقع:

```
arduino
CopyEdit
نتيجة التجميع حسب أول حرف:
المجموعة 'A': [Alice, Ahmed, Amal, adam]
المجموعة 'B': [Bob, Bashar, Brian]

```

---

## 🔁 الحالة 2: تجميع الأرقام حسب كونها زوجية أو فردية

```dart
dart
CopyEdit
// دالة لتجميع الأرقام حسب الزوجي والفردي
Map<String, List<int>> groupByEvenOdd(List<int> numbers) {
  Map<String, List<int>> grouped = {
    "Even": [],
    "Odd": [],
  };

  for (int number in numbers) {
    String key = (number % 2 == 0) ? "Even" : "Odd";
    grouped[key]!.add(number);
  }

  return grouped;
}

void main() {
  List<int> nums = [1, 2, 3, 4, 5, 6, 7];

  Map<String, List<int>> grouped = groupByEvenOdd(nums);

  print("تجميع الأرقام إلى فردي/زوجي:");
  grouped.forEach((key, value) {
    print("$key: $value");
  });
}

```

---

## 🧠 الفكرة الأساسية:

| عنصر | الشرح |
| --- | --- |
| `Map<key, List<values>>` | نستخدم خريطة تربط كل مفتاح بمجموعة من القيم |
| المفتاح `key` | يُحسب حسب خاصية معينة: الحرف الأول، الزوجي/الفردي، الفئة |
| القيمة `List<T>` | هي العناصر التي تنتمي إلى نفس المفتاح |

---

## 📌 ملاحظات تقنية:

- يمكن استخدام `Map<String, List<T>>` لأي نوع من البيانات.
- التجميع مفيد جدًا في قواعد البيانات، التصنيفات، التحليل.
- يمكن تحويل الخوارزمية للعمل مع كائنات (مثل تجميع مستخدمين حسب العمر أو القسم).

---

## 🎯 تطبيقات عملية:

- تجميع الطلاب حسب الصف
- تجميع المنتجات حسب الفئة
- تجميع الكلمات حسب عدد الحروف
- تجميع السجلات حسب التاريخ

---

## ✅ الخلاصة:

| العنصر | القيمة |
| --- | --- |
| النوع | `Map<مفتاح التجميع, قائمة بالعناصر>` |
| الأداء | `O(n)` — سريع |
| قابلية التخصيص | عالي جدًا (يمكن تغيير مفتاح التجميع بسهولة) |