# Most Frequent Element

## 🧠 ما هي المشكلة؟

> تُعطى قائمة (List) من العناصر، ونريد إيجاد العنصر الذي تكرّر أكثر من غيره، أي العنصر الذي لديه أعلى عدد مرات الظهور.
> 

---

## 🪜 خطوات الحل:

### ✅ الخطوة 1: إنشاء خريطة (Map) لحساب التكرارات.

- المفتاح (Key) = العنصر
- القيمة (Value) = عدد التكرارات

### ✅ الخطوة 2: التكرار على القائمة وتحديث التكرارات.

### ✅ الخطوة 3: البحث في الخريطة عن العنصر الذي يملك أعلى تكرار.

---

## 🎯 مثال:

```dart
dart
نسختحرير
List = [1, 3, 2, 3, 4, 3, 5, 1]
العنصر الأكثر تكرارًا = 3

```

---

## 📦 الكود الكامل مع الشرح خطوة بخطوة:

```dart
dart
نسختحرير
// 🟢 الدالة الرئيسية للتنفيذ
void main() {
  // قائمة من الأعداد (يمكن تغييرها لتجريب حالات أخرى)
  List<int> numbers = [1, 3, 2, 3, 4, 3, 5, 1];

  // استدعاء الدالة للحصول على العنصر الأكثر تكرارًا
  int? result = mostFrequentElement(numbers);

  // عرض النتيجة
  if (result != null) {
    print("🔝 العنصر الأكثر تكرارًا هو: $result");
  } else {
    print("❌ القائمة فارغة.");
  }
}

/// ✅ دالة للعثور على العنصر الأكثر تكرارًا
int? mostFrequentElement(List<int> list) {
  // 🛑 إذا كانت القائمة فارغة، نرجع null
  if (list.isEmpty) return null;

  // 🪜 الخطوة 1: إنشاء خريطة لحساب التكرارات
  Map<int, int> frequencyMap = {};

  // 🪜 الخطوة 2: التكرار على كل عنصر في القائمة
  for (int num in list) {
    // إذا كان العنصر موجودًا، نزيد عدّاده؛ إذا لا، نبدأ من 1
    frequencyMap[num] = (frequencyMap[num] ?? 0) + 1;
  }

  // 🪜 الخطوة 3: إيجاد العنصر بأعلى تكرار
  int mostFrequent = list[0]; // نبدأ بأول عنصر كفرضية
  int maxCount = frequencyMap[mostFrequent]!;

  // التكرار على الخريطة للعثور على التكرار الأعلى
  frequencyMap.forEach((key, count) {
    if (count > maxCount) {
      mostFrequent = key;
      maxCount = count;
    }
  });

  // 🟢 نرجع العنصر الأكثر تكرارًا
  return mostFrequent;
}

```

---

## 🧪 مخرجات المثال:

```bash
bash
نسختحرير
🔝 العنصر الأكثر تكرارًا هو: 3

```

---

## 🔍 شرح عملي مع الجدول:

| العنصر | عدد التكرارات |
| --- | --- |
| 1 | 2 |
| 2 | 1 |
| 3 | 3 ✅ الأكثر |
| 4 | 1 |
| 5 | 1 |

---

## ✅ هل الكود يعمل مع أي نوع بيانات؟

حاليًا الكود يعمل مع `List<int>`، لكن يمكن جعله عام باستخدام Generics كالتالي:

### 🔁 نسخة عامة (Generic Version):

```dart
dart
نسختحرير
T? mostFrequentElementGeneric<T>(List<T> list) {
  if (list.isEmpty) return null;

  Map<T, int> frequencyMap = {};
  for (T item in list) {
    frequencyMap[item] = (frequencyMap[item] ?? 0) + 1;
  }

  T mostFrequent = list[0];
  int maxCount = frequencyMap[mostFrequent]!;

  frequencyMap.forEach((key, count) {
    if (count > maxCount) {
      mostFrequent = key;
      maxCount = count;
    }
  });

  return mostFrequent;
}

```

---

## ✅ ملخص الخطوات:

| الخطوة | الوصف |
| --- | --- |
| 1 | أنشأنا خريطة لحفظ التكرارات |
| 2 | ملأنا الخريطة من خلال تكرار عناصر القائمة |
| 3 | بحثنا في الخريطة عن القيمة الأعلى |
| 4 | أرجعنا العنصر الذي يحمل هذا التكرار |

---