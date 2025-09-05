# Diameter of Tree

## 📏 Diameter of a Binary Tree

**(قطر الشجرة الثنائية)**

---

### 🎯 ما هو "القطر"؟

> القطر (Diameter) هو أطول مسار بين أي عقدتين في الشجرة
> 
> 
> هذا المسار **لا يشترط أن يمر بالجذر**.
> 

---

### 📘 كيف يتم قياسه؟

- يتم حسابه كـ **عدد الحواف (edges)** بين العقدتين.
- لكننا عادةً نستخدم **عدد العقد (nodes)** ثم نطرح 1 لتحويلها إلى حواف.

---

### 🌳 مثال:

```
markdown
نسختحرير
        1
       / \
      2   3
     / \
    4   5

```

- أطول مسار: `4 → 2 → 5` = 3 عقد ⇒ القطر = 2 (حافتان)
- أطول مسار آخر: `4 → 2 → 1 → 3` = 4 عقد ⇒ القطر = **3**

---

## 🧠 كيف نحله؟

1. عند كل عقدة:
    - نحسب **عمق الفرع الأيسر**.
    - نحسب **عمق الفرع الأيمن**.
2. **القطر عند هذه العقدة = leftDepth + rightDepth**
3. نحافظ على أكبر قطر ظهر حتى الآن.
4. نستخدم recursion لحساب العمق وتحديث القطر في نفس الوقت.

---

## 🔧 الكود بلغة Dart:

```dart
dart
نسختحرير
class TreeNode {
  int value;
  TreeNode? left, right;

  TreeNode(this.value);
}

class BinaryTree {
  TreeNode? root;

  void insert(int value) {
    root = _insert(root, value);
  }

  TreeNode _insert(TreeNode? node, int value) {
    if (node == null) return TreeNode(value);

    if (value < node.value) {
      node.left = _insert(node.left, value);
    } else {
      node.right = _insert(node.right, value);
    }
    return node;
  }

  int _maxDiameter = 0;

  int diameter() {
    _maxDiameter = 0; // نعيد ضبط القطر
    _calculateDepth(root);
    return _maxDiameter;
  }

  // تحسب العمق وتحدث القطر
  int _calculateDepth(TreeNode? node) {
    if (node == null) return 0;

    int leftDepth = _calculateDepth(node.left);
    int rightDepth = _calculateDepth(node.right);

    // تحديث القطر: مجموع العمق الأيسر + الأيمن
    int currentDiameter = leftDepth + rightDepth;
    if (currentDiameter > _maxDiameter) {
      _maxDiameter = currentDiameter;
    }

    // إرجاع العمق لهذه العقدة
    return 1 + (leftDepth > rightDepth ? leftDepth : rightDepth);
  }
}

```

---

## 🧪 تجربة في `main()`:

```dart
dart
نسختحرير
void main() {
  BinaryTree tree = BinaryTree();

  tree.insert(10);
  tree.insert(5);
  tree.insert(2);
  tree.insert(7);
  tree.insert(15);
  tree.insert(13);
  tree.insert(20);

  print("📏 قطر الشجرة هو: ${tree.diameter()}");
}

```

---

## ✅ مثال ناتج:

```
نسختحرير
📏 قطر الشجرة هو: 4

```

مثلاً لو أطول مسار هو: `2 → 5 → 10 → 15 → 20`

---

## 📌 ملخص:

| الخاصية | Diameter of Tree |
| --- | --- |
| التعريف | أطول مسار بين أي عقدتين في الشجرة |
| يشمل الجذر؟ | ليس بالضرورة |
| الخوارزمية | DFS + حساب العمق |
| الزمن | O(n) |