# Invert Tree

## 🔁 Invert Binary Tree (عكس الشجرة)

---

### 📘 ما معنى Invert Tree؟

**Inverting a Binary Tree** تعني:

> تحويل الشجرة بحيث يتم تبديل كل فرع أيمن بفرع أيسر والعكس، على كل مستوى من مستويات الشجرة.
> 

---

### 🎯 مثال مرئي قبل وبعد:

### قبل العكس:

```
markdown
نسختحرير
        1
       / \
      2   3
     / \   \
    4   5   6

```

### بعد العكس:

```
markdown
نسختحرير
        1
       / \
      3   2
     /   / \
    6   5   4

```

---

## 🧱 كيف يتم ذلك؟

نستخدم **الاستدعاء الذاتي (recursion)**:

1. نبدل بين `left` و `right`.
2. نكرر نفس العملية على الفرعين (الأيسر والأيمن).

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

  // ✅ دالة لعكس الشجرة
  void invert() {
    root = _invertTree(root);
  }

  TreeNode? _invertTree(TreeNode? node) {
    if (node == null) return null;

    // تبديل اليمين واليسار
    TreeNode? temp = node.left;
    node.left = _invertTree(node.right);
    node.right = _invertTree(temp);

    return node;
  }

  // طباعة Inorder للمقارنة
  void inorder() => _inorder(root);
  void _inorder(TreeNode? node) {
    if (node == null) return;
    _inorder(node.left);
    print(node.value);
    _inorder(node.right);
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
  tree.insert(15);
  tree.insert(3);
  tree.insert(7);
  tree.insert(13);
  tree.insert(18);

  print("🔹 Inorder قبل العكس:");
  tree.inorder();

  tree.invert();

  print("\n🔹 Inorder بعد العكس:");
  tree.inorder();
}

```

---

## ✅ الناتج المتوقع:

```
نسختحرير
🔹 Inorder قبل العكس:
3
5
7
10
13
15
18

🔹 Inorder بعد العكس:
18
15
13
10
7
5
3

```

---

## 📌 ملخص:

| الخاصية | Invert Tree |
| --- | --- |
| الوظيفة | تبديل الفروع اليمنى واليسرى في كل عقدة |
| الفكرة | تعتمد على recursion أو BFS (اختياري) |
| الاستخدام | معالجة الأشجار – أسئلة مقابلات – بيانات عكسية |