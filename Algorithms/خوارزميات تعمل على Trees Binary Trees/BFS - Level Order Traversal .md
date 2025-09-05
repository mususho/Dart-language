# BFS - Level Order Traversal

## 🌐 BFS - Level Order Traversal

وهو ما يُعرف بــ **"التمرير بمستوى تلو الآخر"**.

---

## 🧠 ما هو BFS أو Level Order Traversal؟

BFS (Breadth-First Search) يعني المرور على الشجرة **مستوى بمستوى (Level by Level)** من الأعلى للأسفل ومن اليسار لليمين.

---

### 📊 مثال على شجرة:

```
markdown
نسختحرير
        50
       /  \
     30    70
    / \    / \
  20  40  60  80

```

### ✅ التمرير يكون بهذا الترتيب:

```
نسختحرير
50 → 30 → 70 → 20 → 40 → 60 → 80🧱 كيف نطبّقه في Dart؟
```

---

نحتاج إلى:

- استخدام **صف (Queue)** لحفظ العقد أثناء المرور.
- البدء من الجذر وإضافة الأبناء إلى الصف من اليسار إلى اليمين.
- كل مرة نأخذ أول عنصر من الصف ونتابع بنفس الطريقة.

---

## 🔧 كود كامل بلغة Dart:

```dart
dart
نسختحرير
import 'dart:collection';

// تعريف عقدة الشجرة
class TreeNode {
  int value;
  TreeNode? left;
  TreeNode? right;

  TreeNode(this.value);
}

// تعريف الشجرة
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

  // BFS أو Level Order Traversal
  void levelOrderTraversal() {
    if (root == null) return;

    Queue<TreeNode> queue = Queue<TreeNode>();
    queue.add(root!); // نبدأ بالجذر

    while (queue.isNotEmpty) {
      TreeNode current = queue.removeFirst(); // أخذ أول عنصر من الصف
      print(current.value);

      // إضافة الأبناء إلى الصف
      if (current.left != null) {
        queue.add(current.left!);
      }
      if (current.right != null) {
        queue.add(current.right!);
      }
    }
  }
}

```

---

## 🧪 مثال تجربة في `main()`:

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

  print("🔹 Level Order Traversal (BFS):");
  tree.levelOrderTraversal();
}

```

---

## ✅ الناتج المتوقع:

```
scss
نسختحرير
🔹 Level Order Traversal (BFS):
50
30
70
20
40
60
80

```

---

## 📌 ملخص الفرق بين DFS و BFS:

| النوع | الترتيب | الاستخدام |
| --- | --- | --- |
| Inorder | يسار → جذر → يمين | BST ترتيب |
| Preorder | جذر → يسار → يمين | نسخ الشجرة |
| Postorder | يسار → يمين → جذر | حذف الشجرة |
| **LevelOrder (BFS)** | مستوى بمستوى (يسار → يمين) | الذكاء الاصطناعي، البحث السطحي |

---

هل تحب أن أضيف طباعة BFS مع **كل مستوى في سطر منفصل**؟

أو تنقل إلى BFS باستخدام قائمة انتظار ذات أولوية؟

الأدوات