# Map

## ✅ ما هو الـ `Map` في Dart؟

الـ `Map` هي **هيكل بيانات يحتوي على أزواج من المفاتيح والقيم (Key → Value)**.

- كل مفتاح (Key) مرتبط بقيمة (Value).
- لا يمكن أن يتكرر المفتاح، لكن القيم يمكن أن تتكرر.

---

```dart
void main() {
  // =======================
  // 🟩 1. الإنشاء والإضافة
  // =======================
  Map<String, int> scores = {'Ali': 10};

  scores['Hussein'] = 20; // ➤ إضافة أو تعديل مباشرة
  scores.putIfAbsent('Zain', () => 30); // ➤ إضافة فقط إذا المفتاح غير موجود
  scores.addAll({'Sam': 40, 'Lina': 50}); // ➤ إضافة عدة أزواج

  // إنشاء Map بطرق أخرى
  var fromMap = Map.from(scores); // ➤ إنشاء نسخة جديدة
  var ofMap = Map.of(scores); // ➤ إنشاء نسخة أخرى مشابهة
  var fixedMap = Map.unmodifiable({'x': 1, 'y': 2}); // ➤ خريطة غير قابلة للتعديل
  var identityMap = Map.identity(); // ➤ خريطة تقارن الكائنات بالهوية (وليس بالقيمة)

  identityMap[Object()] = 1; // مثال على Map.identity()

  // =======================
  // 🟨 2. التعديل والتحديث
  // =======================
  scores.update('Ali', (v) => v + 5); // ➤ تعديل قيمة موجودة
  scores.update('Sara', (v) => v + 1, ifAbsent: () => 100); // ➤ تعديل أو إضافة عند عدم وجود المفتاح
  scores['Lina'] = (scores['Lina'] ?? 0) + 10; // ➤ تعديل يدوي إذا المفتاح قد لا يكون موجودًا

  // =======================
  // 🟥 3. الحذف
  // =======================
  scores.remove('Sam'); // ➤ حذف زوج بمفتاح
  scores.removeWhere((key, value) => value > 40); // ➤ حذف أزواج تحقق شرط
  var removedValue = scores.remove('Ali'); // ➤ حذف المفتاح وإرجاع قيمته
  print(removedValue); // ➤ القيمة المحذوفة
  scores.clear(); // ➤ حذف كل العناصر

  // =======================
  // 🔵 4. الفحص والتحقق
  // =======================
  scores = {'Ali': 10, 'Hussein': 20, 'Zain': 30, 'Lina': 40};
  print(scores.containsKey('Ali')); // ➤ هل يوجد المفتاح؟
  print(scores.containsValue(20)); // ➤ هل توجد القيمة؟
  print(scores.isEmpty); // ➤ هل الماب فارغة؟
  print(scores.isNotEmpty); // ➤ هل تحتوي على عناصر؟
  print(scores.length); // ➤ عدد الأزواج
  print(scores['UnknownKey'] ?? 0); // ➤ قيمة افتراضية عند غياب المفتاح

  // =======================
  // 🟣 5. المفاتيح والقيم
  // =======================
  print(scores.keys); // ➤ جميع المفاتيح
  print(scores.values); // ➤ جميع القيم
  print(scores.entries); // ➤ قائمة من MapEntry (مفتاح وقيمة)

  // =======================
  // 🟤 6. التكرار والمعالجة
  // =======================
  scores.forEach((k, v) => print('$k: $v')); // ➤ طباعة كل زوج
  var newMap = scores.map((k, v) => MapEntry(k, v * 2)); // ➤ ماب جديدة مع تعديل القيم
  var filtered = Map.fromEntries(
    scores.entries.where((e) => e.value > 20)
  ); // ➤ فلترة القيم حسب شرط
  var modified = Map.from(scores); // ➤ نسخ ماب
  modified['Ali'] = 999; // ➤ تعديل على النسخة فقط
  var spreadCopy = {...scores}; // ➤ نسخة باستخدام spread operator

  // =======================
  // ⚫️ 7. التحويلات
  // =======================
  var asList = scores.entries.toList(); // ➤ تحويل إلى List<MapEntry>
  var fromList = Map.fromEntries([
    MapEntry('A', 1),
    MapEntry('B', 2)
  ]); // ➤ تحويل من List إلى Map

  var fromIterables = Map.fromIterables(
    ['one', 'two', 'three'], [1, 2, 3]
  ); // ➤ تحويل قائمتين إلى Map

  var casted = scores.cast<String, int>(); // ➤ تحويل نوع القيم أو المفاتيح

  // =======================
  // ⚪️ 8. التجميع والتحليل
  // =======================
  var sum = scores.values.reduce((a, b) => a + b); // ➤ جمع القيم
  var maxVal = scores.values.reduce((a, b) => a > b ? a : b); // ➤ إيجاد أكبر قيمة
  var average = scores.values.reduce((a, b) => a + b) / scores.length; // ➤ المتوسط

  // =======================
  // 🧩 9. الاستخدامات الخاصة
  // =======================
  // استخدام ماب كعداد:
  Map<String, int> counter = {};
  List<String> names = ['Ali', 'Ali', 'Hussein'];
  for (var name in names) {
    counter.update(name, (v) => v + 1, ifAbsent: () => 1); // ➤ عدّ التكرارات
  }
  print(counter); // ➤ {'Ali': 2, 'Hussein': 1}
}

```

## 🟢 المستوى المبتدئ: الأساسيات

### 1. **إنشاء Map**

```dart

void main() {
  Map<String, int> ages = {
    'Ali': 25,
    'Sara': 22,
    'Omar': 30,
  };

  print(ages); // {Ali: 25, Sara: 22, Omar: 30}
}

```

---

### 2. **الوصول إلى قيمة معينة باستخدام المفتاح**

```dart
print(ages['Sara']); // 22

```

---

### 3. **إضافة عنصر جديد**

```dart

ages['Mona'] = 28;

```

---

### 4. **تعديل قيمة**

```dart

ages['Ali'] = 26;

```

---

### 5. **حذف عنصر**

```dart

ages.remove('Omar');

```

---

## 🟡 المستوى المتوسط: التكرار والتحكم

### 6. **التكرار على المفاتيح**

```dart
for (var key in ages.keys) {
  print('Name: $key');
}

```

---

### 7. **التكرار على القيم**

```dart

for (var value in ages.values) {
  print('Age: $value');
}

```

---

### 8. **التكرار على الأزواج (key-value)**

```dart
ages.forEach((key, value) {
  print('$key is $value years old');
});

```

---

### 9. **التحقق من وجود مفتاح أو قيمة**

```dart

print(ages.containsKey('Sara'));   // true
print(ages.containsValue(30));     // false (تم حذف Omar)

```

---

## 🟠 المستوى المتقدم: التلاعب والتحويل

### 10. **تحويل Map إلى List**

```dart
List<String> names = ages.keys.toList();
List<int> allAges = ages.values.toList();

```

---

### 11. **تصفيه Map**

```dart

var filtered = ages.entries.where((entry) => entry.value > 23);
print(filtered.map((e) => '${e.key}: ${e.value}').toList());

```

---

### 12. **Map داخل List**

```dart

List<Map<String, dynamic>> students = [
  {'name': 'Ali', 'grade': 90},
  {'name': 'Sara', 'grade': 85},
];

print(students[0]['name']); // Ali

```

---

### 13. **List داخل Map**

```dart

Map<String, List<String>> classes = {
  'Math': ['Ali', 'Sara'],
  'Science': ['Omar']
};

print(classes['Math']); // ['Ali', 'Sara']

```

---

### 14. **Map ديناميكي (Dynamic)**

```dart

Map<dynamic, dynamic> mixedMap = {
  1: 'One',
  'two': 2,
  true: false,
};

```

---

## 🟣 المستوى الاحترافي: Map من كائنات (Objects)

### 15. **تعريف كائن داخل Map**

```dart

class Product {
  String name;
  double price;

  Product(this.name, this.price);
}

void main() {
  Map<int, Product> products = {
    1: Product('Laptop', 1500),
    2: Product('Phone', 999),
  };

  print(products[1]?.name); // Laptop
}

```

---

### 16. **تحديث متعدد العناصر**

```dart

ages.addAll({
  'Rami': 20,
  'Noor': 24,
});

```

---

## 🧠 مقارنة Map بـ Structures أخرى:

| ميزة | Map | List | Set |
| --- | --- | --- | --- |
| يحتوي مفتاح وقيمة | ✅ | ❌ (قائمة عادية فقط) | ❌ (قيم فقط بدون مفتاح) |
| ترتيب | ❌ (غير مضمونة) | ✅ (مرتبة) | ❌ (غير مرتبة) |
| تكرار | مفاتيح لا، قيم نعم | نعم | لا |

---

## ✅ استخدامات عملية لـ Map:

| الحالة | مثال |
| --- | --- |
| تخزين بيانات مستخدمين باسم ومعرّف | `Map<String, int>` |
| تصنيف الطلاب حسب الفصل | `Map<String, List<String>>` |
| حفظ المنتجات حسب المعرف | `Map<int, Product>` |
| عمل قاموس ترجمة | `Map<String, String>`📌 تمرين تطبيقي سريع: |

---

```dart

void main() {
  Map<String, List<String>> school = {
    "Class A": ["Ali", "Sara"],
    "Class B": ["Omar", "Noor"],
  };

  String targetClass = "Class A";
  print("Students in $targetClass:");
  school[targetClass]?.forEach((name) => print(name));
}

```