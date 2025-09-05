# Path Sum

## 🌳 Path Sum

**(هل يوجد مسار من الجذر إلى ورقة في الشجرة بحيث يكون مجموع قيم العقد يساوي هدف معين؟)**

---

### 🎯 الهدف:

> لديك شجرة ثنائية (Binary Tree) وجذرها root، وقيمة هدف targetSum،
> 
> 
> نريد معرفة إذا كان هناك مسار من الجذر إلى إحدى الأوراق حيث مجموع قيم العقد في ذلك المسار يساوي `targetSum`.
> 

---

### 🧠 الفكرة:

- نستخدم استدعاء ذاتي (recursion).
- عند كل عقدة، نطرح قيمة العقدة من `targetSum` وننتقل إلى الأبناء.
- إذا وصلنا إلى ورقة (عقدة بلا أبناء) وكانت قيمة المتبقي من `targetSum` تساوي قيمة العقدة، نرجع `true`.
- إذا لم نجد أي مسار يحقق الشرط نرجع `false`.

---

### ✅ تعريف Node لشجرة ثنائية في Dart:

```dart
dart
نسختحرير
class TreeNode {
  int val;
  TreeNode? left;
  TreeNode? right;

  TreeNode(this.val, {this.left, this.right});
}

```

---

### ✅ كود الحل مع تعليقات:

```dart
dart
نسختحرير
bool hasPathSum(TreeNode? root, int targetSum) {
  if (root == null) return false;

  // إذا هذه ورقة (لا يوجد أبناء)
  if (root.left == null && root.right == null) {
    return root.val == targetSum;
  }

  // استدعاء ذاتي على الأبناء مع تعديل المجموع المطلوب
  int remainingSum = targetSum - root.val;

  return hasPathSum(root.left, remainingSum) || hasPathSum(root.right, remainingSum);
}

```

---

### 🧪 تجربة:

```dart
dart
نسختحرير
void main() {
  TreeNode root = TreeNode(5,
    left: TreeNode(4,
      left: TreeNode(11,
        left: TreeNode(7),
        right: TreeNode(2),
      )
    ),
    right: TreeNode(8,
      left: TreeNode(13),
      right: TreeNode(4,
        right: TreeNode(1),
      ),
    )
  );

  print(hasPathSum(root, 22)); // true (5->4->11->2)
  print(hasPathSum(root, 26)); // true (5->8->13)
  print(hasPathSum(root, 18)); // true (5->8->4->1)
  print(hasPathSum(root, 27)); // false
}

```

---

### ✅ ناتج التجربة:

```
arduino
نسختحرير
true
true
true
false

```

---

### 📦 التحليل:

| الخاصية | القيمة |
| --- | --- |
| الزمن | O(N) حيث N عدد العقد في الشجرة |
| الذاكرة | O(H) حيث H ارتفاع الشجرة (لمكدس الاستدعاءات) |