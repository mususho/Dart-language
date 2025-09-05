# Kadane's Algorithm (أقصى مجموع فرعي)

## 📌 ما هي خوارزمية Kadane’s؟

خوارزمية **Kadane's Algorithm** تُستخدم لإيجاد **أقصى مجموع جزئي متصل** (Maximum Subarray Sum) داخل قائمة من الأعداد الصحيحة (موجبة أو سالبة).

### 🎯 مثال:

```dart
dart
CopyEdit
[−2, 1, −3, 4, −1, 2, 1, −5, 4]
⟶ المجموع الفرعي الأعظمي = 6
⟶ القطعة: [4, -1, 2, 1]

```

---

## ✅ خطوات تنفيذ خوارزمية Kadane:

| رقم | الخطوة |
| --- | --- |
| 1 | التأكد أن القائمة غير فارغة. |
| 2 | تهيئة متغيرين: |
| `maxSoFar = list[0]` ← يمثل أقصى مجموع حتى الآن. |  |
| `currentMax = list[0]` ← يمثل المجموع الحالي. |  |
| 3 | المرور على القائمة من العنصر الثاني فصاعدًا. |
| 4 | في كل خطوة، نحسب `currentMax = max(list[i], currentMax + list[i])`. |
| 5 | نحدث `maxSoFar = max(maxSoFar, currentMax)`. |
| 6 | في النهاية نُعيد `maxSoFar`. |

---

## 💻 الكود الكامل مع التعليقات خطوة بخطوة:

```dart
dart
CopyEdit
// دالة لإيجاد أقصى مجموع فرعي متصل باستخدام Kadane's Algorithm
int kadanesAlgorithm(List<int> list) {
  // الخطوة 1: التحقق من أن القائمة غير فارغة
  if (list.isEmpty) {
    throw Exception("❌ لا يمكن الحساب على قائمة فارغة");
  }

  // الخطوة 2: تهيئة المتغيرات بالبداية إلى أول عنصر
  int maxSoFar = list[0];     // يمثل أكبر مجموع تم الوصول إليه
  int currentMax = list[0];   // يمثل المجموع الحالي المستمر

  print("🔢 البداية بالقيمة: ${list[0]}");

  // الخطوة 3: المرور من العنصر الثاني فصاعدًا
  for (int i = 1; i < list.length; i++) {
    int num = list[i];

    // الخطوة 4: نقرر هل نبدأ تسلسلًا جديدًا من هذا الرقم أم نكمل على المجموع السابق
    currentMax = num > (currentMax + num) ? num : currentMax + num;

    // الخطوة 5: تحديث أكبر مجموع تم الوصول إليه إذا كان currentMax أكبر
    maxSoFar = currentMax > maxSoFar ? currentMax : maxSoFar;

    print("📍 عند index $i:");
    print("    القيمة الحالية: $num");
    print("    المجموع الحالي (currentMax): $currentMax");
    print("    المجموع الأكبر حتى الآن (maxSoFar): $maxSoFar");
  }

  // الخطوة 6: إرجاع النتيجة النهائية
  return maxSoFar;
}

// دالة main لتجربة Kadane's Algorithm
void main() {
  // قائمة من الأعداد (قد تحتوي على قيم سالبة)
  List<int> numbers = [-2, 1, -3, 4, -1, 2, 1, -5, 4];

  print("🔍 القائمة: $numbers");

  // استدعاء دالة كادين
  int maxSum = kadanesAlgorithm(numbers);

  print("✅ أقصى مجموع فرعي متصل هو: $maxSum");
}

```

---

## 🧪 مثال عملي (شرح خطوة بخطوة):

القائمة:

`[-2, 1, -3, 4, -1, 2, 1, -5, 4]`

المسار الحسابي:

```
pgsql
CopyEdit
start: maxSoFar = -2
index 1 → currentMax = max(1, -2 + 1) = 1 → maxSoFar = 1
index 2 → currentMax = max(-3, 1 - 3) = -2 → maxSoFar = 1
index 3 → currentMax = max(4, -2 + 4) = 4 → maxSoFar = 4
index 4 → currentMax = max(-1, 4 -1) = 3 → maxSoFar = 4
index 5 → currentMax = max(2, 3 + 2) = 5 → maxSoFar = 5
index 6 → currentMax = max(1, 5 + 1) = 6 → maxSoFar = 6 ✅
index 7 → currentMax = max(-5, 6 - 5) = 1 → maxSoFar = 6
index 8 → currentMax = max(4, 1 + 4) = 5 → maxSoFar = 6

```

النتيجة النهائية: `6`

---

## ⏱️ تحليل الأداء:

| العامل | القيمة |
| --- | --- |
| الزمن | O(n) ← نمر على القائمة مرة واحدة فقط |
| الذاكرة | O(1) ← لا نستخدم أي بنية إضافية |

---

## 📘 ملاحظات مهمة:

- الخوارزمية **تعمل مع القيم السالبة والموجبة**.
- لا تحتاج إلى إنشاء قوائم فرعية أو مصفوفات إضافية.
- يمكن تعديلها لاستخراج **المجموعة الفرعية نفسها (subarray)** وليس فقط المجموع ← أخبرني إن أردت نسخة تفعل ذلك.