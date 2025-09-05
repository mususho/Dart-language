# Trees

## 🔰 ما هي الأشجار (Trees) في البرمجة؟

شجرة هي بنية بيانات (Data Structure) غير خطية تتكون من **عُقد (Nodes)**، حيث:

- كل عقدة تحتوي على قيمة.
- كل عقدة قد يكون لها عقد فرعية (أبناء).
- العقدة العليا (الأساسية) تُسمى **الجذر (Root)**.
- العقد التي لا تحتوي على أبناء تُسمى **أوراق (Leaves)**.

---

## 🌳 أنواع الأشجار:

سنركز على **شجرة ثنائية (Binary Tree)**، حيث:

- كل عقدة يمكن أن تحتوي على **ابنين فقط كحد أقصى**: `left` و `right`.

---

## 🧱 خطوات إنشاء شجرة ثنائية في Dart:

1. إنشاء كلاس يمثل العقدة `TreeNode`.
2. إنشاء كلاس يمثل الشجرة نفسها `BinaryTree`.
3. كتابة دوال مثل:
    - الإدراج (insert)
    - الطباعة (traverse): preorder, inorder, postorder

---

## ✅ الكود الكامل مع الشرح:

```dart
dart
نسختحرير
// الخطوة 1: إنشاء كلاس يمثل العقدة في الشجرة
class TreeNode {
  int value; // قيمة العقدة
  TreeNode? left; // الإبن الأيسر
  TreeNode? right; // الإبن الأيمن

  TreeNode(this.value); // مُنشئ لتعيين القيمة عند إنشاء العقدة
}

// الخطوة 2: كلاس يمثل الشجرة الثنائية
class BinaryTree {
  TreeNode? root; // جذر الشجرة

  // الخطوة 3: دالة إدراج قيمة جديدة في الشجرة
  void insert(int value) {
    root = _insertRecursive(root, value);
  }

  // دالة خاصة (داخلية) لإدراج قيمة باستخدام الاستدعاء الذاتي (recursive)
  TreeNode _insertRecursive(TreeNode? node, int value) {
    // إذا كانت العقدة فارغة، ننشئ عقدة جديدة
    if (node == null) {
      return TreeNode(value); // خطوة النهاية في التكرار
    }

    // المقارنة لتحديد الاتجاه
    if (value < node.value) {
      // الإدراج في الفرع الأيسر
      node.left = _insertRecursive(node.left, value);
    } else {
      // الإدراج في الفرع الأيمن
      node.right = _insertRecursive(node.right, value);
    }

    return node; // نرجع العقدة بعد التعديل
  }

  // الخطوة 4: طباعة الشجرة - الترتيب داخل الشجرة (Inorder Traversal)
  void inorderTraversal() {
    _inorderHelper(root);
  }

  void _inorderHelper(TreeNode? node) {
    if (node == null) return;

    _inorderHelper(node.left); // زيارة الفرع الأيسر
    print(node.value); // طباعة القيمة الحالية
    _inorderHelper(node.right); // زيارة الفرع الأيمن
  }

  // الخطوة 5: طباعة بترتيب ما قبل الترتيب (Preorder)
  void preorderTraversal() {
    _preorderHelper(root);
  }

  void _preorderHelper(TreeNode? node) {
    if (node == null) return;

    print(node.value); // طباعة أولاً
    _preorderHelper(node.left); // ثم اليسار
    _preorderHelper(node.right); // ثم اليمين
  }

  // الخطوة 6: طباعة بترتيب ما بعد الترتيب (Postorder)
  void postorderTraversal() {
    _postorderHelper(root);
  }

  void _postorderHelper(TreeNode? node) {
    if (node == null) return;

    _postorderHelper(node.left); // زيارة اليسار
    _postorderHelper(node.right); // زيارة اليمين
    print(node.value); // طباعة في الأخير
  }
}

// مثال على الاستخدام:
void main() {
  BinaryTree tree = BinaryTree();

  // الخطوة 7: إدخال قيم في الشجرة
  tree.insert(50);
  tree.insert(30);
  tree.insert(70);
  tree.insert(20);
  tree.insert(40);
  tree.insert(60);
  tree.insert(80);

  print("🔸 Inorder Traversal:");
  tree.inorderTraversal(); // يجب أن تطبع القيم مرتبة تصاعدياً

  print("🔸 Preorder Traversal:");
  tree.preorderTraversal(); // الطباعة تبدأ من الجذر

  print("🔸 Postorder Traversal:");
  tree.postorderTraversal(); // الطباعة في النهاية
}

```

---

## 📝 شرح خطوات التنفيذ:

| الخطوة | التفاصيل |
| --- | --- |
| 1 | إنشاء كائن `TreeNode` لتمثيل كل عقدة بقيمة وارتباطات لليسار واليمين |
| 2 | تعريف شجرة ثنائية تحتوي على الجذر `root` |
| 3 | تنفيذ دالة `insert()` التي تستخدم طريقة **recursive** للإدراج الصحيح حسب القيم |
| 4 | تنفيذ دوال مختلفة لطباعة القيم بترتيبات مختلفة حسب الحاجة |
| 5 | اختبار الشجرة بإدخال عدة قيم وطباعة النتائج |

---

هل ترغب أن أضيف عمليات بحث (search) أو حذف (delete) من الشجرة أيضاً؟

يمكنك تجربة هذا الكود الكامل لشجرة ثنائية ومتابعة التعديلات عليه بسهولة.