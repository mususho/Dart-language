# List

## 🟢 أولًا: ما هي الـ List في Dart؟

الـ `List` هي **مجموعة مرتبة** من العناصر (elements) يمكنك تخزينها واستخدامها بمرونة.

كل عنصر له **index** يبدأ من `0`.

### ✅ مثال بسيط:

```dart

void main() {
  List<String> names = ['Ali', 'Sara', 'Omar'];
  print(names[0]); // تطبع: Ali
}

```

| القسم | العدد |
| --- | --- |
| **المجموع الكلي** | 62 |

---

```dart
void main() {
  // ===============================================//
  // 📌 1. الإضافة                             ✅ //
  // ============================================//
  List<int> numbers = [1, 2];
  numbers.add(3); // ➤ إضافة عنصر واحد
  numbers.addAll([4, 5]); // ➤ إضافة مجموعة عناصر
  numbers.insert(1, 99); // ➤ إدراج عنصر عند index معين
  numbers.insertAll(2, [8, 9]); // ➤ إدراج مجموعة عناصر
  // ============================================== //
  // 🧹 2. الحذف                              ✅ 
  // ============================================== //
  numbers.remove(2); // ➤ حذف أول عنصر يطابق القيمة
  numbers.removeAt(0); // ➤ حذف العنصر في index معين
  numbers.removeLast(); // ➤ حذف آخر عنصر
  numbers.removeWhere((e) => e % 2 == 0); // ➤ حذف حسب شرط
  numbers.removeRange(0, 1); // ➤ حذف من index إلى آخر غير شامل
  numbers.clear(); // ➤ حذف جميع العناصر
  // ============================================== //
  // ✏️ 3. التعديل                            ✅ 
  // ============================================== //
  numbers[0] = 10; // ➤ تعديل مباشر لعُنصر
  numbers.fillRange(0, 2, 0); // ➤ ملء نطاق معين بقيمة واحدة
  numbers.setAll(1, [9, 9]); // ➤ استبدال عناصر من index محدد
  numbers.replaceRange(2, 4, [7, 8]); // ➤ استبدال نطاق بعناصر
  numbers.setRange(0, 2, [5, 6]); // ➤ تعيين قيم لعناصر ضمن نطاق
  // ============================================== //
  // 🔍 4. الفحص والبحث                       ✅ 
  // ============================================== //
  print(numbers.contains(3)); // ➤ هل القائمة تحتوي على 3؟
  print(numbers.indexOf(4)); // ➤ أول index للعنصر 4
  print(numbers.lastIndexOf(4)); // ➤ آخر index للعنصر 4
  print(numbers.indexWhere((e) => e == 9)); // ➤ أول index يحقق الشرط
  print(numbers.lastIndexWhere((e) => e < 10)); // ➤ آخر index يحقق الشرط
  print(numbers.elementAt(2)); // ➤ جلب العنصر في index معين
  print(numbers.first); // ➤ أول عنصر
  print(numbers.last); // ➤ آخر عنصر
  print(numbers.singleWhere((e) => e == 9)); // ➤ العنصر الوحيد المطابق
  print(numbers.firstWhere((e) => e > 5)); // ➤ أول عنصر يطابق شرط
  print(numbers.lastWhere((e) => e < 10)); // ➤ آخر عنصر يطابق شرط
  var filtered = numbers.where((e) => e > 3).toList(); // ➤ فلترة حسب شرط
  // ============================================== //
  // ✅ 5. التحقق                               ✅ 
  // ============================================== //
  print(numbers.isEmpty); // ➤ هل القائمة فارغة؟
  print(numbers.isNotEmpty); // ➤ هل القائمة غير فارغة؟
  print(numbers.any((e) => e > 5)); // ➤ هل يوجد عنصر يطابق شرط؟
  print(numbers.every((e) => e < 100)); // ➤ هل كل العناصر تحقق شرط؟
  print(numbers.length); // ➤ عدد العناصر
  // ============================================== //
  // 🔄 6. الترتيب والعكس والعشوائي          ✅ 
  // ============================================== //
  numbers.sort(); // ➤ ترتيب تصاعدي
  numbers.shuffle(); // ➤ ترتيب عشوائي
  print(numbers.reversed.toList()); // ➤ قائمة مقلوبة
  // ============================================== //
  // 🔁 7. التكرار والمعالجة                 ✅ 
  // ============================================== //
  numbers.forEach((e) => print(e)); // ➤ طباعة كل عنصر
  var doubled = numbers.map((e) => e * 2).toList(); // ➤ مضاعفة كل عنصر
  var expanded = [[1, 2], [3, 4]].expand((e) => e).toList(); // ➤ تحويل قائمة ثنائية لقائمة مسطحة
  // ============================================== //
  // 🧮 8. التجميع                            ✅ 
  // ============================================== //
  print(numbers.reduce((a, b) => a + b)); // ➤ جمع كل العناصر
  print(numbers.fold(10, (a, b) => a + b)); // ➤ جمع + قيمة ابتدائية
  // ============================================== //
  // 🔄 9. التقطيع والتخطي                   ✅ 
  // ============================================== //
  print(numbers.take(3).toList()); // ➤ أخذ أول 3 عناصر
  print(numbers.skip(2).toList()); // ➤ تجاوز أول 2
  print(numbers.takeWhile((e) => e < 5).toList()); // ➤ أخذ طالما تحقق شرط
  print(numbers.skipWhile((e) => e < 5).toList()); // ➤ تجاهل طالما تحقق شرط
  print(numbers.sublist(1, 3)); // ➤ جزء من القائمة من index إلى index غير شامل
  // ============================================== //
  // 🔁 10. التحويلات                          ✅ 
  // ============================================== //
  var joined = ['a', 'b', 'c'].join(','); // ➤ تحويل لقائمة مفصولة بفواصل
  var unique = [1, 2, 2, 3].toSet().toList(); // ➤ إزالة التكرار
  var asMap = numbers.asMap(); // ➤ تحويل إلى Map (index: value)
  var casted = numbers.cast<int>(); // ➤ تحويل النوع (cast)
  var copy = List.of(numbers); // ➤ نسخ القائمة
  var generated = List.generate(5, (i) => i * 2); // ➤ إنشاء قائمة بطول 5 بقيم محسوبة
  var filled = List.filled(5, 0); // ➤ إنشاء قائمة مملوءة بقيمة واحدة
  var emptyList = List.empty(growable: true); // ➤ إنشاء قائمة فارغة قابلة للنمو
  final fixedList = List,.unmodifiable([1, 2, 3]); // ➤ قائمة غير قابلة للتعديل
  // ============================================== //
  // 🔗 11. تقاطع/اتحاد القوائم يدويًا         ✅ 
  // ============================================== //
  var listA = [1, 2, 3];
  var listB = [3, 4, 5];

  var intersection = listA.where((e) => listB.contains(e)).toList(); // ➤ العناصر المشتركة
  var union = {...listA, ...listB}.toList(); // ➤ دمج بدون تكرار باستخدام Set
  // ============================================== //
  // 🧩 12. أخرى مفيدة                         ✅ 
  // ============================================== //
  print(numbers.runtimeType); // ➤ نوع الكائن
  print(numbers.hashCode); // ➤ الكود الخاص بالكائن (مفيد في المقارنة)
}

```

### 1. **إنشاء List**

## 🟡 المستوى الأول: **الأساسيات**

```dart

List<int> numbers = [1, 2, 3, 4];
List<String> fruits = ['Apple', 'Banana'];

```

### 2. **إضافة عنصر**

```dart

fruits.add('Mango');

```

### 3. **حذف عنصر**

```dart

fruits.remove('Banana');       // يحذف العنصر بالقيمة
fruits.removeAt(0);            // يحذف العنصر حسب الـ index

```

### 4. **تعديل عنصر**

```dart

fruits[0] = 'Orange';

```

### 5. **طول القائمة**

```dart

print(fruits.length); // عدد العناصر

```

---

## 🟠 المستوى الثاني: **التحكم والتكرار**

### 6. **طباعة كل العناصر باستخدام for**

```dart

for (int i = 0; i < fruits.length; i++) {
  print(fruits[i]);
}

```

### 7. **باستخدام for-in**

```dart

for (var fruit in fruits) {
  print(fruit);
}

```

### 8. **باستخدام forEach**

```dart

fruits.forEach((fruit) {
  print(fruit);
});

```

---

## 🔵 المستوى الثالث: **قوائم ديناميكية وتحقق من القيم**

### 9. **List ديناميكية (تقبل أنواع مختلفة)**

```dart

List<dynamic> mixed = [1, 'Hello', true, 3.14];

```

### 10. **التحقق من وجود عنصر**

```dart

print(fruits.contains('Apple')); // true or false

```

---

## 🟣 المستوى الرابع: **طرق متقدمة على القوائم**

### 11. **تصفيه العناصر باستخدام `where()`**

```dart

List<int> numbers = [1, 2, 3, 4, 5, 6];
var even = numbers.where((n) => n % 2 == 0);
print(even.toList()); // [2, 4, 6]

```

### 12. **تغيير كل عنصر باستخدام `map()`**

```dart

var doubled = numbers.map((n) => n * 2).toList();
print(doubled); // [2, 4, 6, 8, 10, 12]

```

### 13. **ترتيب القائمة**

```dart
dart
نسختحرير
numbers.sort(); // تصاعدي

```

### 14. **نسخ القائمة**

```dart
dart
نسختحرير
List<int> copy = List.from(numbers);

```

---

## 🟥 المستوى الخامس: **List ثابتة وغير قابلة للتغيير**

### 15. **List ثابتة باستخدام `const`**

```dart

const List<String> fixedList = ['A', 'B', 'C'];
// fixedList.add('D'); ❌ Error!

```

---

## 🟤 المستوى السادس: **استخدام spread و null-aware**

### 16. **دمج قائمتين باستخدام spread operator**

```dart

List<String> list1 = ['A', 'B'];
List<String> list2 = ['C', 'D'];
List<String> all = [...list1, ...list2];

```

### 17. **null-aware spread operator**

```dart
dart
نسختحرير
List<String>? maybeList = null;
List<String> safeList = [...?maybeList]; // ما يعمل مشكلة حتى لو null

```

---

## 🟢 المستوى السابع: **List داخل Map والعكس**

### 18. **List داخل Map**

```dart

Map<String, List<String>> classes = {
  "Math": ["Ali", "Sara"],
  "English": ["Omar"]
};

print(classes["Math"]); // [Ali, Sara]

```

### 19. **Map داخل List**

```dart

List<Map<String, dynamic>> products = [
  {"name": "Phone", "price": 999},
  {"name": "Laptop", "price": 2500},
];

print(products[0]["name"]); // Phone

```

---

## 🧠 ملخص سريع: