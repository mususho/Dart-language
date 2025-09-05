# Lists

## 📦 ما هي `List` في Dart؟

> الـ List هي مجموعة مرتبة من العناصر يمكن أن تحتوي على أي نوع من القيم (مثل int, String, وغيرها).
> 

✅ وهي النوع المكافئ لـ **المصفوفة (Array)** في لغات أخرى.

---

## 🧱 إنشاء `List` في Dart:

### 🔹 قائمة قابلة للتغيير (growable):

```dart
dart
نسختحرير
List<int> numbers = [1, 2, 3];

```

### 🔹 قائمة ثابتة الطول:

```dart
dart
نسختحرير
List<int> fixedList = List.filled(5, 0); // [0, 0, 0, 0, 0]

```

### 🔹 قائمة فارغة تنمو تلقائيًا:

```dart
dart
نسختحرير
List<String> names = [];

```

---

## 🧪 الوصول للعناصر:

```dart
dart
نسختحرير
print(numbers[0]); // 1
print(numbers.length); // 3

```

---

## ✍️ تعديل وإضافة عناصر:

```dart
dart
نسختحرير
numbers.add(4);            // [1, 2, 3, 4]
numbers.insert(1, 10);     // [1, 10, 2, 3, 4]
numbers[0] = 100;          // [100, 10, 2, 3, 4]

```

---

## ❌ حذف العناصر:

```dart
dart
نسختحرير
numbers.remove(10);        // حذف أول عنصر قيمته 10
numbers.removeAt(2);       // حذف العنصر في index 2
numbers.clear();           // حذف كل العناصر

```

---

## 🔄 التكرار على القائمة:

```dart
dart
نسختحرير
for (int num in numbers) {
  print(num);
}

// أو باستخدام for التقليدية
for (int i = 0; i < numbers.length; i++) {
  print(numbers[i]);
}

```

---

## 🧠 بعض الدوال المفيدة:

```dart
dart
نسختحرير
List<int> nums = [5, 3, 9, 1];

nums.sort();           // [1, 3, 5, 9]
nums.contains(3);      // true
nums.indexOf(9);       // 3
nums.reversed.toList(); // [9, 5, 3, 1]

```

---

## 🧬 خرائط وتحويلات:

```dart
dart
نسختحرير
List<String> names = ['Ali', 'Omar'];

List<int> nameLengths = names.map((name) => name.length).toList();
// [3, 4]

```

---

## 🎯 التصفية:

```dart
dart
نسختحرير
List<int> even = nums.where((n) => n % 2 == 0).toList();

```

---

## 💡 spread operator & null safety:

```dart
dart
نسختحرير
List<int> a = [1, 2];
List<int> b = [0, ...a]; // [0, 1, 2]

List<int>? c;
List<int> d = [0, ...?c]; // null-safe spread

```

---

## ✅ ملخص:

| العملية | المثال |
| --- | --- |
| إنشاء | `List<int> l = [1, 2];` |
| إضافة | `add, insert` |
| حذف | `remove, removeAt, clear` |
| ترتيب/عكس | `sort, reversed` |
| تصفية وتحويل | `where, map` |
| دمج القوائم | `[...a, ...b]` |

---

## 🧪 مثال كامل:

```dart
dart
نسختحرير
void main() {
  List<String> fruits = ['apple', 'banana', 'orange'];
  fruits.add('grape');
  fruits.remove('banana');

  for (var fruit in fruits) {
    print(fruit.toUpperCase());
  }
}

```