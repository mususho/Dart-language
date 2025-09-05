# Balanced Tree Check

## ⚖️ Balanced Binary Tree Check

**(التحقق مما إذا كانت الشجرة الثنائية متوازنة أم لا)**

---

### 📘 ما هي الشجرة المتوازنة (Balanced Tree)؟

> شجرة ثنائية تُعتبر متوازنة إذا كان فرق العمق بين الفرع الأيسر والفرع الأيمن لأي عقدة لا يزيد عن 1.
> 

---

### 🎯 مثال على شجرة **متوازنة**:

```
markdown
نسختحرير
      10
     /  \
    5   15
   / \   \
  3   7  20

```

- كل فرع يختلف في العمق عن الآخر بـ 0 أو 1 → ✅ متوازنة

---

### 🛑 مثال على شجرة **غير متوازنة**:

```
markdown
نسختحرير
      10
     /
    5
   /
  3
 /
1

```

- كل الفرع الأيسر أطول بكثير من الأيمن → ❌ غير متوازنة

---

## 🧱 كيف نتحقق من التوازن؟

### الطريقة المثالية (O(n)):

1. استخدم **الاستدعاء الذاتي (recursion)** لحساب العمق.
2. في كل خطوة:
    - نحسب عمق الفرع الأيسر والأيمن.
    - نتحقق من الفرق بينهما.
3. إذا تجاوز الفرق 1 → **غير متوازنة**.
4. نستخدم قيمة خاصة (مثل `1`) كعلامة على وجود خلل.

---

## 🔧 كود Dart للتحقق من توازن الشجرة:

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

  // ✅ تحقق مما إذا كانت الشجرة متوازنة
  bool isBalanced() {
    return _checkBalance(root) != -1;
  }

  // ترجع -1 إذا لم تكن متوازنة، أو ترجع عمق العقدة
  int _checkBalance(TreeNode? node) {
    if (node == null) return 0;

    int left = _checkBalance(node.left);
    if (left == -1) return -1;

    int right = _checkBalance(node.right);
    if (right == -1) return -1;

    if ((left - right).abs() > 1) {
      return -1; // غير متوازنة
    }

    return 1 + (left > right ? left : right); // عمق هذه العقدة
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

  // شجرة متوازنة
  tree.insert(10);
  tree.insert(5);
  tree.insert(15);
  tree.insert(3);
  tree.insert(7);

  print("✅ هل الشجرة متوازنة؟ ${tree.isBalanced()}");

  // نكسر التوازن يدويًا:
  TreeNode unbalanced = TreeNode(1);
  unbalanced.left = TreeNode(0);
  unbalanced.left!.left = TreeNode(-1);
  tree.root!.left!.left = unbalanced; // ندفع فرع للأعمق يدويًا

  print("❌ بعد التعديل، هل الشجرة متوازنة؟ ${tree.isBalanced()}");
}

```

---

## ✅ الناتج المتوقع:

```
arduino
نسختحرير
✅ هل الشجرة متوازنة؟ true
❌ بعد التعديل، هل الشجرة متوازنة؟ false

```

---

## 📌 ملخص:

| الخاصية | Balanced Binary Tree |
| --- | --- |
| الشرط | فرق العمق بين الفرعين ≤ 1 |
| الطريقة الأفضل | DFS مع إرجاع -1 كعلامة للخلل |
| الزمن | O(n) |
| الفائدة | تحسين الأداء وضمان الاستجابة المتوازنة |