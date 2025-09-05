# Rotate Array

## 🔁 ما هي خوارزمية Rotate Array؟

هي خوارزمية تقوم **بتدوير عناصر القائمة** إلى اليمين أو اليسار بعدد معين من الخطوات `k`.

---

## 🎯 مثال توضيحي:

### إذا كانت القائمة:

```dart
dart
CopyEdit
[1, 2, 3, 4, 5, 6, 7]

```

### وطلبنا تدويرها 3 خطوات إلى اليمين:

```dart
dart
CopyEdit
[5, 6, 7, 1, 2, 3, 4]

```

---

## ✅ خطوات تنفيذ التدوير لليمين (Rotate Right by k steps):

| رقم | الخطوة |
| --- | --- |
| 1 | نأخذ `k = k % length` ← للتعامل مع القيم الأكبر من الطول. |
| 2 | نقسم القائمة إلى جزئين: |
| - الجزء الأخير: `list.sublist(length - k)` |  |
| - الجزء الأول: `list.sublist(0, length - k)` |  |
| 3 | ندمج الجزأين: `rotated = lastPart + firstPart` |
| 4 | نُرجع النتيجة الجديدة. |

---

## 💻 الكود الكامل بلغة Dart مع تعليقات توضيحية:

```dart
dart
CopyEdit
// دالة لتدوير القائمة k خطوات إلى اليمين
List<int> rotateArrayRight(List<int> list, int k) {
  int n = list.length;

  // الخطوة 1: معالجة القيم الكبيرة لـ k
  k = k % n;

  print("🔢 القائمة الأصلية: $list");
  print("🔁 عدد خطوات التدوير: $k");

  // إذا لم يكن هناك حاجة للتدوير
  if (k == 0 || n == 0) return list;

  // الخطوة 2: تقسيم القائمة إلى جزئين
  List<int> lastPart = list.sublist(n - k);         // الجزء الأخير
  List<int> firstPart = list.sublist(0, n - k);     // الجزء الأول

  print("📦 الجزء الأخير: $lastPart");
  print("📦 الجزء الأول: $firstPart");

  // الخطوة 3: دمج الجزأين
  List<int> rotated = [...lastPart, ...firstPart];

  print("✅ النتيجة بعد التدوير: $rotated");

  // الخطوة 4: إعادة النتيجة
  return rotated;
}

// دالة لتجربة الخوارزمية
void main() {
  List<int> numbers = [1, 2, 3, 4, 5, 6, 7];
  int steps = 3;

  List<int> result = rotateArrayRight(numbers, steps);

  print("🔚 الناتج النهائي: $result");
}

```

---

## 🧪 مثال عملي:

```dart
dart
CopyEdit
list = [1, 2, 3, 4, 5, 6, 7], k = 3

length = 7
k = 3 % 7 = 3

lastPart = [5, 6, 7]
firstPart = [1, 2, 3, 4]
rotated = [5, 6, 7, 1, 2, 3, 4]

```

---

## 🔄 هل يمكن تدوير القائمة لليسار أيضًا؟

نعم! ✅ إليك تعديل بسيط لتدوير القائمة `k` خطوات إلى **اليسار**:

```dart
dart
CopyEdit
List<int> rotateArrayLeft(List<int> list, int k) {
  int n = list.length;
  k = k % n;

  if (k == 0 || n == 0) return list;

  List<int> firstPart = list.sublist(k);      // من k إلى النهاية
  List<int> lastPart = list.sublist(0, k);    // من 0 إلى k

  return [...firstPart, ...lastPart];
}

```

---

## ⏱️ تحليل الأداء:

| النوع | القيمة |
| --- | --- |
| الزمن (Time) | ✅ O(n) ← مرور واحد فقط |
| الذاكرة (Space) | ✅ O(n) ← إنشاء قائمة جديدة |

---

## 📘 ملاحظات إضافية:

- إن أردت تنفيذ التدوير **في نفس القائمة (in-place)** دون استخدام قوائم جديدة، فيمكننا استخدام خوارزمية تعتمد على **عكس (Reverse)** العناصر.
- التقنية المتقدمة هي:
    1. عكس القائمة كلها
    2. عكس أول `k` عنصر
    3. عكس باقي العناصر

أخبرني إن أردت هذا النوع كذلك، وسأرسله لك مباشرة.