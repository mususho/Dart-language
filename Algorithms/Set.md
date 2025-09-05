# Set

## ✅ ما هو الـ Set في Dart؟

الـ `Set` هو **مجموعة غير مرتبة (unordered)** من العناصر **الفريدة** (unique).

يعني:

- ما تقبل تكرار القيم.
- ما تضمن ترتيب معين للعناصر مثل الـ List.

---

```dart
void main() {
  // ===========================
  // 🟩 1. الإنشاء والإضافة   ✅
  // ===========================
  Set<int> mySet = {1, 2, 3};

  mySet.add(4); // ➤ إضافة عنصر جديد
  mySet.addAll([5, 6, 7]); // ➤ إضافة مجموعة عناصر

  // ===========================
  // 🟥 2. الحذف             ✅
  // ===========================
  mySet.remove(2); // ➤ حذف عنصر إذا كان موجودًا
  mySet.removeWhere((e) => e > 6); // ➤ حذف حسب شرط
  mySet.retainWhere((e) => e % 2 == 0); // ➤ الاحتفاظ بالعناصر حسب شرط
  mySet.clear(); // ➤ حذف كل العناصر

  // ===========================
  // 🔍 3. الفحص والتحقق    ✅
  // ===========================
  mySet = {1, 2, 3, 4, 5};
  print(mySet.contains(3)); // ➤ هل يحتوي على العنصر 3؟
  print(mySet.containsAll([2, 4])); // ➤ هل يحتوي على كل العناصر؟
  print(mySet.length); // ➤ عدد العناصر
  print(mySet.isEmpty); // ➤ هل المجموعة فارغة؟
  print(mySet.isNotEmpty); // ➤ هل تحتوي على عناصر؟
  print(mySet.lookup(4)); // ➤ البحث عن عنصر معين (يرجع العنصر نفسه أو null)

  // ===========================
  // 🟨 4. العمليات على المجموعات✅
  // ===========================
  Set<int> setA = {1, 2, 3, 4};
  Set<int> setB = {3, 4, 5, 6};

  var unionSet = setA.union(setB); // ➤ دمج المجموعتين بدون تكرار
  var intersectionSet = setA.intersection(setB); // ➤ العناصر المشتركة فقط
  var differenceSet = setA.difference(setB); // ➤ العناصر الموجودة في A وغير موجودة في B
  var symmetricDiff = setA.union(setB).difference(setA.intersection(setB)); // ➤ الفرق المتماثل

  print(unionSet);        // {1, 2, 3, 4, 5, 6}
  print(intersectionSet); // {3, 4}
  print(differenceSet);   // {1, 2}
  print(symmetricDiff);   // {1, 2, 5, 6}

  // ===========================
  // 🟣 5. التكرار والمعالجة✅
  // ===========================
  mySet.forEach((e) => print(e)); // ➤ طباعة كل عنصر
  for (var item in mySet) {
    print(item); // ➤ طريقة أخرى للطباعة باستخدام for-in
  }

  var doubledSet = mySet.map((e) => e * 2).toSet(); // ➤ إنشاء مجموعة جديدة بقيم مضاعفة
  var filtered = mySet.where((e) => e > 2).toSet(); // ➤ تصفية المجموعة حسب شرط

  // ===========================
  // ⚫️ 6. التحويلات         ✅
  // ===========================
  var listFromSet = mySet.toList(); // ➤ تحويل إلى List
  var stringSet = {'a', 'b', 'c'};
  var joined = stringSet.join(','); // ➤ تحويل إلى سلسلة نصية مفصولة بفواصل
  var asMap = mySet.asMap(); // ➤ تحويل إلى Map (index: value)
  var casted = mySet.cast<int>(); // ➤ تحويل نوع العناصر (casting)
  final unmodifiable = Set.unmodifiable([10, 20, 30]); // ➤ إنشاء مجموعة غير قابلة للتعديل

  // ===========================
  // 🧮 7. التجميع والتحليل✅
  // ===========================
  var sum = mySet.reduce((a, b) => a + b); // ➤ جمع العناصر
  var maxVal = mySet.reduce((a, b) => a > b ? a : b); // ➤ أكبر قيمة
  var avg = mySet.reduce((a, b) => a + b) / mySet.length; // ➤ متوسط القيم

  // ===========================
  // 🧩 8. أخرى مفيدة       ✅
  // ===========================
  print(mySet.runtimeType); // ➤ نوع الكائن (Set<int>)
  print(mySet.hashCode); // ➤ رقم تعريف فريد للمجموعة

  // مقارنة مجموعتين
  var setC = {1, 2, 3};
  var setD = {3, 2, 1};
  print(setC.containsAll(setD)); // ➤ true (هل تحتوي على كل عناصر D؟)

  // تحويل قائمة إلى مجموعة لإزالة التكرار
  List<int> withDuplicates = [1, 2, 2, 3, 3, 3];
  Set<int> noDuplicates = withDuplicates.toSet();
  print(noDuplicates); // ➤ {1, 2, 3}
}

```

## 🟢 المستوى المبتدئ: الأساسيات

### 1. **إنشاء Set**

```dart
dart
نسختحرير
void main() {
  Set<int> numbers = {1, 2, 3};
  print(numbers); // {1, 2, 3}
}

```

> ✅ ملاحظة: نستخدم {} بدل [] عند إنشاء Set.
> 

---

### 2. **إضافة عنصر**

```dart
numbers.add(4); // {1, 2, 3, 4}

```

### 3. **محاولة إضافة عنصر مكرر**

```dart
numbers.add(2); // ما يصير شيء، لأن 2 موجود مسبقًا

```

### 4. **حذف عنصر**

```dart
numbers.remove(3); // {1, 2, 4}

```

### 5. **التحقق من وجود عنصر**

```dart
print(numbers.contains(2)); // true

```

---

## 🟡 المستوى المتوسط: التعامل مع Sets

### 6. **التكرار على العناصر**

```dart
for (var n in numbers) {
  print(n);
}

```

### 7. **التحويل بين Set و List**

```dart
List<int> myList = numbers.toList(); // تحويل Set إلى List
Set<int> newSet = myList.toSet();   // تحويل List إلى Set وإزالة التكرارات

```

---

## 🟠 المستوى المتقدم: العمليات على الـ Sets

### 8. **الاتحاد (Union)**

```dart
Set<int> a = {1, 2, 3};
Set<int> b = {3, 4, 5};

Set<int> union = a.union(b);
print(union); // {1, 2, 3, 4, 5}

```

---

### 9. **التقاطع (Intersection)**

```dart
dart
نسختحرير
Set<int> intersection = a.intersection(b);
print(intersection); // {3}

```

---

### 10. **الفرق (Difference)**

```dart
dart
نسختحرير
Set<int> difference = a.difference(b);
print(difference); // {1, 2} العناصر اللي في a ومش موجودة في b

```

---

## 🟣 المستوى الاحترافي: التعامل مع أنواع مختلفة وميزات متقدمة

### 11. **Set ديناميكي (dynamic)**

```dart
dart
نسختحرير
Set<dynamic> mixed = {1, 'hello', true};

```

---

### 12. **Set من الكائنات (Objects)**

### تعريف كلاس بسيط:

```dart
class Person {
  String name;
  Person(this.name);

  @override
  String toString() => name;

  @override
  bool operator ==(other) => other is Person && name == other.name;
  @override
  int get hashCode => name.hashCode;
}

```

### استخدامه داخل Set:

```dart
void main() {
  Set<Person> people = {
    Person("Ali"),
    Person("Sara"),
    Person("Ali") // مكرر حسب الاسم
  };

  print(people); // {Ali, Sara}
}

```

> ✅ لازم نعرّف == و hashCode عشان Dart تعرف إن العنصر مكرر.
> 

---

## 🟥 استخدام شائع: إزالة التكرارات من List

```dart
List<int> listWithDuplicates = [1, 2, 2, 3, 3, 3, 4];
Set<int> unique = listWithDuplicates.toSet();
print(unique); // {1, 2, 3, 4}

```

---

## 🧠 مقارنة سريعة: `List` vs `Set`

| خاصية | List | Set |
| --- | --- | --- |
| التكرار | تسمح بالتكرار | تمنع التكرار |
| الترتيب | مرتبة (ordered) | غير مرتبة (unordered) |
| الوصول | عبر index | لا يوجد index مباشر |

---

## ✅ استخدامات عملية لـ Set:

| الاستخدام | مثال |
| --- | --- |
| التحقق من القيم الفريدة | حفظ المستخدمين بدون تكرار |
| العمليات بين المجموعات | إيجاد العناصر المشتركة بين قائمتين |
| تصفية القوائم من التكرارات | تحويل `List` إلى `Set` ثم إرجاعها `toList()` |

---

##