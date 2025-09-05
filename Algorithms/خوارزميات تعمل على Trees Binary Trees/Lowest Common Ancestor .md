# Lowest Common Ancestor

## 🧬 Lowest Common Ancestor (LCA)

**(أقل سلف مشترك بين عقدتين)**

---

## 🎯 ما هو Lowest Common Ancestor؟

> في شجرة ثنائية (Binary Tree)، أقل سلف مشترك (LCA) بين عقدتين p و q هو أعمق عقدة تحتوي كلا من p و q كأحفاد (في الفرع الأيسر أو الأيمن أو أحدهم مباشرة).
> 

---

### 📘 مثال:

لنفترض هذه الشجرة:

```
markdown
نسختحرير
        3
       / \
      5   1
     / \ / \
    6  2 0  8
      / \
     7   4

```

- LCA(5, 1) = 3
- LCA(6, 4) = 5
- LCA(7, 8) = 3

---

## 🧱 كيف نحله باستخدام Recursion؟

الخطوات:

1. إذا كانت العقدة الحالية `null`، نرجع null.
2. إذا كانت العقدة الحالية تساوي `p` أو `q`، نرجع هذه العقدة.
3. نبحث في الفرع الأيسر والفرع الأيمن.
4. إذا وُجدت كلا العقدتين في فرعين مختلفين، فالعقدة الحالية هي LCA.
5. إذا وُجدت في أحد الفرعين فقط، نرجع هذا الفرع.

---

## 🔧 كود Dart كامل مع `TreeNode` و `lowestCommonAncestor`:

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

  // ✅ إيجاد أقل سلف مشترك
  TreeNode? lowestCommonAncestor(TreeNode? node, TreeNode p, TreeNode q) {
    if (node == null || node == p || node == q) return node;

    TreeNode? left = lowestCommonAncestor(node.left, p, q);
    TreeNode? right = lowestCommonAncestor(node.right, p, q);

    if (left != null && right != null) {
      return node; // كلا العقدتين موجودتين في فرعين مختلفين
    }

    return left ?? right; // نرجع الفرع غير الفارغ
  }

  // 🔍 إيجاد عقدة تحتوي على قيمة معينة
  TreeNode? find(TreeNode? node, int value) {
    if (node == null) return null;
    if (node.value == value) return node;
    TreeNode? left = find(node.left, value);
    if (left != null) return left;
    return find(node.right, value);
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
  tree.insert(20);
  tree.insert(10);
  tree.insert(30);
  tree.insert(5);
  tree.insert(15);
  tree.insert(25);
  tree.insert(35);

  TreeNode? node1 = tree.find(tree.root, 5);
  TreeNode? node2 = tree.find(tree.root, 15);

  TreeNode? lca = tree.lowestCommonAncestor(tree.root, node1!, node2!);

  print("🔹 أقل سلف مشترك بين ${node1.value} و ${node2.value} هو: ${lca?.value}");
}

```

---

## ✅ الناتج المتوقع:

```
نسختحرير
🔹 أقل سلف مشترك بين 5 و 15 هو: 10

```

---

## 📌 ملخص:

| الخاصية | Lowest Common Ancestor |
| --- | --- |
| التعريف | أقرب عقدة تشترك كجد للعقدتين المستهدفتين |
| التقنية | Recursion أو Stack أو Parent Mapping |
| الوقت | O(n) في الشجرة العادية (DFS أو BFS) |