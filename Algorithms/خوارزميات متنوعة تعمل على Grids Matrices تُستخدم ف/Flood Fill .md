# Flood Fill

## 🌊 Flood Fill

**(تلوين منطقة متصلة في مصفوفة 2D)**

---

## 🎯 الهدف:

> لديك مصفوفة 2D تمثل صورة أو لوحة ألوان،
> 
> 
> وإحداثيات نقطة بداية `(sr, sc)`،
> 
> ولون جديد `newColor`،
> 
> المطلوب: تغيير لون كل الخانات المتصلة (عبر الأعلى، الأسفل، اليسار، اليمين) بنفس لون الخانة الأصلية إلى اللون الجديد.
> 

---

## 🧠 الفكرة (DFS / Backtracking):

- نبدأ من النقطة `(sr, sc)`.
- نحفظ اللون الأصلي `originalColor` لهذه النقطة.
- إذا كانت الخانة الحالية بنفس اللون الأصلي، نغيرها إلى `newColor`.
- نكرر العملية لجميع الخانات المجاورة (4 اتجاهات).
- نستخدم استدعاء ذاتي أو خوارزمية DFS.

---

## ✅ الكود الكامل في Dart:

```dart
dart
نسختحرير
void floodFill(List<List<int>> image, int sr, int sc, int newColor) {
  int rows = image.length;
  int cols = image[0].length;
  int originalColor = image[sr][sc];

  if (originalColor == newColor) return; // لا حاجة لتغيير اللون إذا كان جديد هو نفسه القديم

  void dfs(int r, int c) {
    if (r < 0 || r >= rows || c < 0 || c >= cols) return;
    if (image[r][c] != originalColor) return;

    image[r][c] = newColor;

    dfs(r + 1, c);
    dfs(r - 1, c);
    dfs(r, c + 1);
    dfs(r, c - 1);
  }

  dfs(sr, sc);
}

```

---

## 🧪 تجربة:

```dart
dart
نسختحرير
void main() {
  List<List<int>> image = [
    [1,1,1],
    [1,1,0],
    [1,0,1],
  ];

  floodFill(image, 1, 1, 2);

  print("🌊 الصورة بعد التلوين:");
  for (var row in image) {
    print(row);
  }
}

```

---

## ✅ الناتج المتوقع:

```
csharp
نسختحرير
🌊 الصورة بعد التلوين:
[2, 2, 2]
[2, 2, 0]
[2, 0, 1]

```

---

## 📦 التحليل:

| الخاصية | القيمة |
| --- | --- |
| الزمن | O(N * M) حيث N، M أبعاد الصورة |
| الذاكرة | O(N * M) (مكدس الاستدعاءات) |
| النوع | DFS / Backtracking |