# Spiral Traversal

## 🌀 Spiral Traversal

**(طباعة عناصر المصفوفة في شكل حلزوني من الخارج للداخل)**

---

### 🎯 الهدف:

> لديك مصفوفة matrix ثنائية الأبعاد بحجم N×M،
> 
> 
> نريد قراءة جميع عناصرها بطريقة حلزونية تبدأ من الزاوية العلوية اليسرى،
> 
> تتحرك يمينًا، ثم أسفل، ثم يسارًا، ثم أعلى، وتكرر حتى تنتهي كل العناصر.
> 

---

### 🧠 الفكرة:

- نستخدم أربع مؤشرات:
    - `top` لأعلى الصفوف غير المزارَة
    - `bottom` لأسفل الصفوف غير المزارَة
    - `left` لأيسر الأعمدة غير المزارَة
    - `right` لأيمن الأعمدة غير المزارَة
- نقرأ العناصر من `left` إلى `right` في الصف `top` ثم نزيد `top`.
- نقرأ العناصر من `top` إلى `bottom` في العمود `right` ثم ننقص `right`.
- نقرأ العناصر من `right` إلى `left` في الصف `bottom` ثم ننقص `bottom`.
- نقرأ العناصر من `bottom` إلى `top` في العمود `left` ثم نزيد `left`.
- نكرر هذه الخطوات حتى نستعرض كل العناصر.

---

### ✅ كود Dart مع تعليقات:

```dart
dart
نسختحرير
List<int> spiralOrder(List<List<int>> matrix) {
  List<int> result = [];

  if (matrix.isEmpty) return result;

  int top = 0;
  int bottom = matrix.length - 1;
  int left = 0;
  int right = matrix[0].length - 1;

  while (top <= bottom && left <= right) {
    // 1. قراءة من اليسار إلى اليمين في الصف العلوي
    for (int col = left; col <= right; col++) {
      result.add(matrix[top][col]);
    }
    top++;

    // 2. قراءة من الأعلى إلى الأسفل في العمود الأيمن
    for (int row = top; row <= bottom; row++) {
      result.add(matrix[row][right]);
    }
    right--;

    // 3. التأكد من عدم تجاوز الحدود، ثم قراءة من اليمين إلى اليسار في الصف السفلي
    if (top <= bottom) {
      for (int col = right; col >= left; col--) {
        result.add(matrix[bottom][col]);
      }
      bottom--;
    }

    // 4. التأكد من عدم تجاوز الحدود، ثم قراءة من الأسفل إلى الأعلى في العمود الأيسر
    if (left <= right) {
      for (int row = bottom; row >= top; row--) {
        result.add(matrix[row][left]);
      }
      left++;
    }
  }

  return result;
}

```

---

### 🧪 تجربة:

```dart
dart
نسختحرير
void main() {
  List<List<int>> matrix = [
    [1, 2, 3, 4],
    [5, 6, 7, 8],
    [9,10,11,12],
  ];

  List<int> spiral = spiralOrder(matrix);

  print("🌀 عناصر المصفوفة بالترتيب الحلزوني:");
  print(spiral);
}

```

---

### ✅ الناتج المتوقع:

```
csharp
نسختحرير
🌀 عناصر المصفوفة بالترتيب الحلزوني:
[1, 2, 3, 4, 8, 12, 11, 10, 9, 5, 6, 7]

```

---

### 📦 التحليل:

| الخاصية | القيمة |
| --- | --- |
| الزمن | O(N * M) |
| الذاكرة | O(N * M) (للمصفوفة الناتجة) |

---