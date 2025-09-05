# Jump Game

## 🏃‍♂️ Jump Game

**(هل يمكن القفز للنهاية؟)**

---

## 🎯 الهدف:

> لديك مصفوفة nums حيث كل عنصر يمثل أقصى عدد خطوات يمكنك القفز بها من هذا الموقع.
> 
> 
> المطلوب: التحقق مما إذا كان من الممكن الوصول إلى نهاية المصفوفة (آخر عنصر).
> 

---

## 🧠 الفكرة:

- نتابع من البداية، ونحتفظ بأبعد موقع يمكن الوصول إليه حتى الآن (`maxReach`).
- لكل موقع `i`:
    - إذا `i` أكبر من `maxReach`، فهذا يعني أننا لا نستطيع الوصول لهذا الموقع → نرجع `false`.
    - خلاف ذلك، نحدث `maxReach` إذا كان `i + nums[i]` أكبر من `maxReach`.
- إذا وصلنا أو تجاوزنا آخر موقع، نرجع `true`.

---

## ✅ الكود الكامل في Dart:

```dart
dart
نسختحرير
bool canJump(List<int> nums) {
  int maxReach = 0;
  int n = nums.length;

  for (int i = 0; i < n; i++) {
    if (i > maxReach) {
      return false; // لا يمكن الوصول لهذا الموقع
    }
    maxReach = maxReach > (i + nums[i]) ? maxReach : (i + nums[i]);
    if (maxReach >= n - 1) return true;
  }

  return true;
}

```

---

## 🧪 تجربة:

```dart
dart
نسختحرير
void main() {
  List<int> nums1 = [2, 3, 1, 1, 4];
  List<int> nums2 = [3, 2, 1, 0, 4];

  print("هل يمكن القفز للنهاية (مثال 1)؟ ${canJump(nums1)}"); // true
  print("هل يمكن القفز للنهاية (مثال 2)؟ ${canJump(nums2)}"); // false
}

```

---

## ✅ الناتج المتوقع:

```
arduino
نسختحرير
هل يمكن القفز للنهاية (مثال 1)؟ true
هل يمكن القفز للنهاية (مثال 2)؟ false

```

---

## 📦 التحليل:

| الخاصية | القيمة |
| --- | --- |
| الزمن | O(n) |
| الذاكرة | O(1) |
| النوع | Greedy Algorithm |