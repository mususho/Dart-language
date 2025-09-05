# Remove Duplicates

## 🧽 ما هي خوارزمية Remove Duplicates؟

هي خوارزمية تُستخدم لحذف العناصر **المكررة** من قائمة، بحيث **تُترك نسخة واحدة فقط من كل عنصر**.

---

## 🎯 أهداف الخوارزمية:

- إذا كانت القائمة:

```dart
dart
CopyEdit
[1, 2, 3, 2, 1, 4]

```

تصبح:

```dart
dart
CopyEdit
[1, 2, 3, 4]

```

---

## ✅ خطوات تصميم الخوارزمية:

| رقم | الخطوة |
| --- | --- |
| 1 | تعريف دالة تأخذ `List<int>` كوسيط. |
| 2 | إنشاء `Set` لتخزين العناصر الفريدة. |
| 3 | المرور على كل عنصر في القائمة. |
| 4 | إضافة العنصر إلى `Set` (الـ Set يزيل التكرارات تلقائيًا). |
| 5 | تحويل `Set` إلى `List` وإرجاعها. |

---

## 💻 الكود الكامل مع التعليقات التفصيلية:

```dart
dart
CopyEdit
// دالة لإزالة العناصر المكررة من قائمة
List<int> removeDuplicates(List<int> list) {
  // الخطوة 2: إنشاء Set لتخزين العناصر الفريدة
  Set<int> uniqueItems = {};

  // الخطوة 3: المرور على القائمة
  for (int item in list) {
    // الخطوة 4: إضافة العنصر إلى الـ Set (لن يُضاف إن كان مكررًا)
    uniqueItems.add(item);
  }

  // الخطوة 5: تحويل Set إلى List وإرجاعها
  return uniqueItems.toList();
}

// دالة main لتجربة الخوارزمية
void main() {
  // قائمة تحتوي على عناصر مكررة
  List<int> numbers = [1, 2, 3, 2, 4, 1, 5, 3, 6];

  print("📋 القائمة الأصلية:");
  print(numbers);

  // استدعاء دالة إزالة التكرارات
  List<int> result = removeDuplicates(numbers);

  print("✅ القائمة بعد إزالة التكرارات:");
  print(result);
}

```

---

## 🧪 مثال عملي:

```dart
dart
CopyEdit
[1, 2, 3, 2, 4, 1, 5, 3, 6]

```

بعد تحويلها إلى Set:

```dart
dart
CopyEdit
{1, 2, 3, 4, 5, 6}

```

ثم تحويلها إلى قائمة:

```dart
dart
CopyEdit
[1, 2, 3, 4, 5, 6]

```

---

## ⏱️ تحليل الأداء:

| الحالة | الزمن (Time Complexity) | الذاكرة (Space Complexity) |
| --- | --- | --- |
| جميع الحالات | O(n) | O(n) ← لاستخدام Set |

---

## 📘 ملاحظات إضافية:

- `Set` يحافظ فقط على العناصر **الفريدة**.
- لا يضمن `Set` **الترتيب الأصلي** في Dart.

### ✅ إذا أردت **الحفاظ على الترتيب الأصلي**:

استخدم هذا التعديل:

```dart
dart
CopyEdit
List<int> removeDuplicatesWithOrder(List<int> list) {
  Set<int> seen = {};
  List<int> result = [];

  for (int item in list) {
    if (!seen.contains(item)) {
      seen.add(item);
      result.add(item); // نحافظ على الترتيب
    }
  }

  return result;
}

```