# Binary Trees

## 🌳 ما هي الشجرة الثنائية (Binary Tree)؟

**شجرة ثنائية (Binary Tree)** هي بنية بيانات غير خطية حيث:

- كل **عقدة (Node)** تحتوي على قيمة.
- كل عقدة تحتوي على **فرعين كحد أقصى**:
    - `left` (الفرع الأيسر)
    - `right` (الفرع الأيمن)

يتم استخدامها في:

- تنظيم البيانات
- عمليات البحث
- تنفيذ هياكل بيانات أكثر تعقيدًا مثل Binary Search Trees و Heaps و AVL Trees وغيرها.

---

## ✅ أهم العمليات في Binary Tree:

1. **الإدراج (Insert)**
2. **الطباعة (Traversal)**:
    - Inorder
    - Preorder
    - Postorder
3. **البحث (Search)**
4. **الحذف (Delete)** – اختيارية

---

## 🧱 خطوات بناء Binary Tree في Dart:

سنقوم بكتابة الكود على مراحل مفصلة:

---

### 📌 الخطوة 1: تعريف `TreeNode`

```dart
dart
نسختحرير
// تعريف العقدة في الشجرة
class TreeNode {
  int value; // القيمة داخل العقدة
  TreeNode? left; // الإبن الأيسر
  TreeNode? right; // الإبن الأيمن

  TreeNode(this.value); // المُنشئ الأساسي للعقدة
}

```

---

### 📌 الخطوة 2: بناء الشجرة `BinaryTree`

```dart
dart
نسختحرير
class BinaryTree {
  TreeNode? root; // العقدة الجذرية (أول عنصر في الشجرة)

  // إدخال قيمة جديدة في الشجرة
  void insert(int value) {
    root = _insertNode(root, value);
  }

  // دالة مساعدة للإدراج بشكل متكرر (recursive)
  TreeNode _insertNode(TreeNode? node, int value) {
    if (node == null) {
      return TreeNode(value); // إذا وصلت لمكان فارغ، أنشئ عقدة جديدة
    }

    if (value < node.value) {
      node.left = _insertNode(node.left, value); // الإدراج في اليسار
    } else {
      node.right = _insertNode(node.right, value); // الإدراج في اليمين
    }

    return node; // ترجع العقدة الحالية بعد التعديل
  }
}

```

---

### 📌 الخطوة 3: الطباعة بأنواعها

```dart
dart
نسختحرير
  // طباعة العناصر Inorder (يسار -> جذر -> يمين)
  void inorder() {
    _inorderTraversal(root);
  }

  void _inorderTraversal(TreeNode? node) {
    if (node == null) return;
    _inorderTraversal(node.left);
    print(node.value);
    _inorderTraversal(node.right);
  }

  // طباعة Preorder (جذر -> يسار -> يمين)
  void preorder() {
    _preorderTraversal(root);
  }

  void _preorderTraversal(TreeNode? node) {
    if (node == null) return;
    print(node.value);
    _preorderTraversal(node.left);
    _preorderTraversal(node.right);
  }

  // طباعة Postorder (يسار -> يمين -> جذر)
  void postorder() {
    _postorderTraversal(root);
  }

  void _postorderTraversal(TreeNode? node) {
    if (node == null) return;
    _postorderTraversal(node.left);
    _postorderTraversal(node.right);
    print(node.value);
  }

```

---

### 📌 الخطوة 4: البحث عن عنصر

```dart

  bool contains(int value) {
    return _search(root, value);
  }

  bool _search(TreeNode? node, int value) {
    if (node == null) return false;

    if (value == node.value) return true;
    if (value < node.value) {
      return _search(node.left, value);
    } else {
      return _search(node.right, value);
    }
  }

```

---

### 📌 الخطوة 5: تجربة الشجرة في `main`

```dart
dart
نسختحرير
void main() {
  BinaryTree tree = BinaryTree();

  // إدخال عناصر في الشجرة
  tree.insert(50);
  tree.insert(30);
  tree.insert(70);
  tree.insert(20);
  tree.insert(40);
  tree.insert(60);
  tree.insert(80);

  print("Inorder Traversal:");
  tree.inorder();

  print("\nPreorder Traversal:");
  tree.preorder();

  print("\nPostorder Traversal:");
  tree.postorder();

  print("\nهل الشجرة تحتوي على 60؟ ${tree.contains(60)}");
  print("هل الشجرة تحتوي على 25؟ ${tree.contains(25)}");
}

```

---

## 📝 الناتج المتوقع:

```
yaml
نسختحرير
Inorder Traversal:
20
30
40
50
60
70
80

Preorder Traversal:
50
30
20
40
70
60
80

Postorder Traversal:
20
40
30
60
80
70
50

هل الشجرة تحتوي على 60؟ true
هل الشجرة تحتوي على 25؟ false

```

---

## 📌 ملخص:

- أنشأنا بنية أساسية لـ **Binary Tree**.
- أضفنا إدخالًا، وطباعة بأنواعها، وبحثًا داخل الشجرة.
- الكود منظم وواضح وسهل التوسعة مستقبلًا.