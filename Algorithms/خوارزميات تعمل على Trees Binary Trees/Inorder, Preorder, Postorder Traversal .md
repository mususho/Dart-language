# Inorder, Preorder, Postorder Traversal

## 🌳 مثال مرئي على شجرة ثنائية:

نفترض أن لدينا الشجرة التالية:

```
markdown
نسختحرير
        50
       /  \
     30    70
    / \    / \
  20  40  60  80

```

---

## 🟩 1. Inorder Traversal (يسار → جذر → يمين)

### ✅ الترتيب:

```
نسختحرير
20 → 30 → 40 → 50 → 60 → 70 → 80

```

### 📘 الوصف:

- زر أولاً الفرع الأيسر.
- ثم العقدة الحالية (الجذر).
- ثم الفرع الأيمن.

### 🧠 استخدامه:

- يُستخدم في **الترتيب التصاعدي** لشجرة بحث ثنائية (BST).

### 🔧 الكود:

```dart
dart
نسختحرير
void inorder(TreeNode? node) {
  if (node == null) return;
  inorder(node.left);         // 1. زر الفرع الأيسر
  print(node.value);          // 2. طباعة الجذر
  inorder(node.right);        // 3. زر الفرع الأيمن
}

```

---

## 🟨 2. Preorder Traversal (جذر → يسار → يمين)

### ✅ الترتيب:

```
نسختحرير
50 → 30 → 20 → 40 → 70 → 60 → 80

```

### 📘 الوصف:

- طبع الجذر أولاً.
- ثم زيارة الفرع الأيسر.
- ثم الفرع الأيمن.

### 🧠 استخدامه:

- مفيد في **نسخ أو حفظ** الشجرة.
- مفيد في **بناء الشجرة من تمثيل نصي**.

### 🔧 الكود:

```dart
dart
نسختحرير
void preorder(TreeNode? node) {
  if (node == null) return;
  print(node.value);          // 1. طباعة الجذر
  preorder(node.left);        // 2. زر الفرع الأيسر
  preorder(node.right);       // 3. زر الفرع الأيمن
}

```

---

## 🟦 3. Postorder Traversal (يسار → يمين → جذر)

### ✅ الترتيب:

```
نسختحرير
20 → 40 → 30 → 60 → 80 → 70 → 50

```

### 📘 الوصف:

- زيارة الفرع الأيسر أولاً.
- ثم الأيمن.
- ثم الجذر في النهاية.

### 🧠 استخدامه:

- مفيد في حذف الشجرة أو تنظيف الذاكرة.
- يُستخدم في العمليات التي تتطلب إغلاق فرع بالكامل قبل التراجع.

### 🔧 الكود:

```dart
dart
نسختحرير
void postorder(TreeNode? node) {
  if (node == null) return;
  postorder(node.left);       // 1. زر الفرع الأيسر
  postorder(node.right);      // 2. زر الفرع الأيمن
  print(node.value);          // 3. طباعة الجذر
}

```

---

## ✅ كود Dart كامل لتجربة الثلاث طرق:

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
    root = _insertRecursive(root, value);
  }

  TreeNode _insertRecursive(TreeNode? node, int value) {
    if (node == null) return TreeNode(value);

    if (value < node.value) {
      node.left = _insertRecursive(node.left, value);
    } else {
      node.right = _insertRecursive(node.right, value);
    }
    return node;
  }

  void inorder() => _inorder(root);
  void _inorder(TreeNode? node) {
    if (node == null) return;
    _inorder(node.left);
    print(node.value);
    _inorder(node.right);
  }

  void preorder() => _preorder(root);
  void _preorder(TreeNode? node) {
    if (node == null) return;
    print(node.value);
    _preorder(node.left);
    _preorder(node.right);
  }

  void postorder() => _postorder(root);
  void _postorder(TreeNode? node) {
    if (node == null) return;
    _postorder(node.left);
    _postorder(node.right);
    print(node.value);
  }
}

void main() {
  BinaryTree tree = BinaryTree();
  tree.insert(50);
  tree.insert(30);
  tree.insert(70);
  tree.insert(20);
  tree.insert(40);
  tree.insert(60);
  tree.insert(80);

  print('🔹 Inorder Traversal:');
  tree.inorder();

  print('\n🔹 Preorder Traversal:');
  tree.preorder();

  print('\n🔹 Postorder Traversal:');
  tree.postorder();
}

```

---