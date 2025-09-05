# Matrix Rotation

## 🔄 Matrix Rotation

**(تدوير مصفوفة مربعة 90 درجة باتجاه عقارب الساعة)**

---

### 🎯 الهدف:

> لديك مصفوفة مربعة matrix بحجم N×N،
> 
> 
> المطلوب تدويرها 90 درجة باتجاه عقارب الساعة **دون استخدام مصفوفة إضافية** (in-place).
> 

---

### 🧠 الفكرة:

- التدوير 90 درجة عقارب الساعة يمكن تحقيقه بخطوتين:
    1. **انعكاس المصفوفة أفقياً** (Reverse each row)
    2. **أخذ المصفوفة المعكوسة ونعمل لها Transpose** (تبديل الصفوف مع الأعمدة)

---

### ✅ كود Dart مع تعليقات خطوة بخطوة:

```dart
dart
نسختحرير
void rotate(List<List<int>> matrix) {
  int n = matrix.length;

  // 1. عكس كل صف (reverse)
  for (int i = 0; i < n; i++) {
    matrix[i] = matrix[i].reversed.toList();
  }

  // 2. عمل transpose للمصفوفة (تبديل الصفوف مع الأعمدة)
  for (int i = 0; i < n; i++) {
    for (int j = i + 1; j < n; j++) {
      int temp = matrix[i][j];
      matrix[i][j] = matrix[j][i];
      matrix[j][i] = temp;
    }
  }
}

```

---

### 🧪 تجربة:

```dart
dart
نسختحرير
void main() {
  List<List<int>> matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9],
  ];

  rotate(matrix);

  print("🔄 المصفوفة بعد التدوير 90 درجة:");
  for (var row in matrix) {
    print(row);
  }
}

```

---

### ✅ الناتج المتوقع:

```
csharp
نسختحرير
🔄 المصفوفة بعد التدوير 90 درجة:
[7, 4, 1]
[8, 5, 2]
[9, 6, 3]

```

---

### 📦 التحليل:

| الخاصية | القيمة |
| --- | --- |
| الزمن | O(N²) |
| الذاكرة | O(1) (in-place) |
| النوع | تعديل مباشر للمصفوفة |