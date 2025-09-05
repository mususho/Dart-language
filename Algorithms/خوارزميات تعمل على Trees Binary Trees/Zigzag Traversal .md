# Zigzag Traversal

## 🔀 Zigzag Level Order Traversal

**(التمرير المتعرج لمستويات الشجرة)**

---

## 🎯 ما هو Zigzag Traversal؟

> هو تمرير الشجرة مستوى بمستوى (مثل BFS) لكن باتجاه متناوب:
> 
- المستوى الأول → من **اليسار إلى اليمين**
- المستوى الثاني → من **اليمين إلى اليسار**
- المستوى الثالث → من **اليسار إلى اليمين**
- وهكذا...

---

### 📘 مثال:

لنفترض لدينا الشجرة التالية:

```
markdown
نسختحرير
        1
       / \
      2   3
     / \   \
    4   5   6

```

### ✅ Zigzag Traversal:

```
css
نسختحرير
1         → left to right
3 2       → right to left
4 5 6     → left to right

```

**النتيجة:** `[[1], [3, 2], [4, 5, 6]]`

---

## 🧠 كيف ننفّذها؟

- نستخدم **صف (Queue)** لتنفيذ BFS.
- نحتفظ بمستوى العقدة.
- نستخدم `List<List<int>>` لتخزين النتيجة.
- إذا كنا في مستوى زوجي (0، 2...) → نضيف من اليسار إلى اليمين.
- إذا كنا في مستوى فردي (1، 3...) → نضيف من اليمين إلى اليسار.

---

## 🔧 كود Dart كامل:

```dart
dart
نسختحرير
import 'dart:collection';

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

  // ✅ Zigzag Traversal
  List<List<int>> zigzagTraversal() {
    List<List<int>> result = [];

    if (root == null) return result;

    Queue<TreeNode> queue = Queue<TreeNode>();
    queue.add(root!);

    bool leftToRight = true;

    while (queue.isNotEmpty) {
      int levelSize = queue.length;
      List<int> level = List.filled(levelSize, 0);

      for (int i = 0; i < levelSize; i++) {
        TreeNode node = queue.removeFirst();

        // ضع القيمة حسب الاتجاه
        int index = leftToRight ? i : levelSize - 1 - i;
        level[index] = node.value;

        if (node.left != null) queue.add(node.left!);
        if (node.right != null) queue.add(node.right!);
      }

      result.add(level);
      leftToRight = !leftToRight; // قلب الاتجاه
    }

    return result;
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
  tree.insert(12);
  tree.insert(18);

  List<List<int>> result = tree.zigzagTraversal();

  print("🔀 Zigzag Level Order Traversal:");
  for (var level in result) {
    print(level);
  }
}

```

---

## ✅ الناتج المتوقع (مثلاً):

```
csharp
نسختحرير
🔀 Zigzag Level Order Traversal:
[10]
[15, 5]
[3, 7, 12, 18]

```

---

## 📌 ملخص:

| الخاصية | Zigzag Traversal |
| --- | --- |
| يشبه | BFS (Level Order) |
| الفرق | كل مستوى يتم تمريره بعكس الاتجاه السابق |
| التركيبة المستخدمة | Queue + اتجاه متناوب (`leftToRight`) |
| الوقت | O(n) – حيث n عدد العقد |

---