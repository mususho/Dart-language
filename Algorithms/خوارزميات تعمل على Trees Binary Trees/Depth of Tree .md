# Depth of Tree

## 🌳 **Depth of Tree** (عمق الشجرة)

---

### 🧠 ما هو عمق الشجرة (Depth أو Height)؟

- **العمق (Depth)**: هو عدد الحواف (edges) من **الجذر (root)** حتى **أبعد عقدة (leaf)**.
- بعض التعريفات تسمي هذا أيضًا **ارتفاع الشجرة (Height of Tree)**.

> 🎯 مهم: شجرة تحتوي على عقدة واحدة (الجذر فقط) يكون عمقها = 1.
> 

---

## 🌰 مثال توضيحي:

```
markdown
نسختحرير
        50
       /  \
     30    70
    / \    / \
  20  40  60  80

```

- من الجذر `50` إلى العقدة `20` أو `80` هناك 3 مستويات.
- إذًا العمق = **3**

---

## 🧱 كيف نحسبه في Dart؟

نحسب العمق باستخدام **الاستدعاء الذاتي (recursion)**:

- نحسب العمق في الفرع الأيسر.
- نحسب العمق في الفرع الأيمن.
- العمق الكلي = أكبر العمقين + 1 (لأننا نحتسب الجذر).

---

## 🔧 الكود بلغة Dart:

```dart
dart
نسختحرير
class TreeNode {
  int value;
  TreeNode? left;
  TreeNode? right;

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

  // ✅ حساب عمق الشجرة
  int depth() {
    return _depthRecursive(root);
  }

  int _depthRecursive(TreeNode? node) {
    if (node == null) return 0;

    int leftDepth = _depthRecursive(node.left);   // عمق الفرع الأيسر
    int rightDepth = _depthRecursive(node.right); // عمق الفرع الأيمن

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

  tree.insert(50);
  tree.insert(30);
  tree.insert(70);
  tree.insert(20);
  tree.insert(40);
  tree.insert(60);
  tree.insert(80);

  print("🔹 عمق الشجرة هو: ${tree.depth()}");
}

```

---

## ✅ الناتج المتوقع:

```
نسختحرير
🔹 عمق الشجرة هو: 3

```

---

## 📌 ملخص سريع:

| المصطلح | المعنى |
| --- | --- |
| Depth of Node | عدد الحواف من الجذر حتى العقدة |
| Depth of Tree | أكبر عمق لأي عقدة (عادةً ورقة leaf) |
| Height | في كثير من السياقات = Depth of Tree |