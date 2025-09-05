# Validate BST

## ✅ Validate Binary Search Tree (BST)

**التحقق مما إذا كانت شجرة معينة هي شجرة بحث ثنائية صحيحة أم لا**

---

## 📘 ما هي شجرة البحث الثنائية (Binary Search Tree)؟

- لكل عقدة:
    - جميع القيم في **الفرع الأيسر < القيمة الحالية**
    - جميع القيم في **الفرع الأيمن > القيمة الحالية**
- تنطبق هذه القاعدة **على كل عقدة في الشجرة** (ليس فقط على الجذر)

---

## 🧠 الهدف:

> اكتب دالة تأخذ جذر شجرة وتتحقق مما إذا كانت تلتزم بقواعد BST.
> 

---

## 🎯 مثال:

```
markdown
نسختحرير
        10
       /  \
      5    15
          /  \
        12    20

```

✅ هذه شجرة BST صحيحة

---

## 🛑 مثال غير صحيح:

```
markdown
نسختحرير
        10
       /  \
      5    15
          /  \
        6     20

```

❌ العقدة 6 موجودة في الفرع الأيمن من 10، لكنها أصغر منها → مخالفة لقواعد BST

---

## 🧱 الفكرة:

نستخدم **الاستدعاء الذاتي (Recursion)**، ونمرر في كل خطوة:

- **الحد الأدنى (min)** الذي يجب أن تكون القيمة أكبر منه
- **الحد الأقصى (max)** الذي يجب أن تكون القيمة أصغر منه

---

## 🔧 كود Dart: التحقق من صحة BST

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

  // ✅ التحقق من صحة BST
  bool isValidBST() {
    return _validate(root, null, null);
  }

  bool _validate(TreeNode? node, int? min, int? max) {
    if (node == null) return true;

    // شرط فشل BST
    if ((min != null && node.value <= min) ||
        (max != null && node.value >= max)) {
      return false;
    }

    // تحقق من الفرع الأيسر والأيمن
    return _validate(node.left, min, node.value) &&
           _validate(node.right, node.value, max);
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

  tree.insert(10);
  tree.insert(5);
  tree.insert(15);
  tree.insert(12);
  tree.insert(20);

  print("✅ هل الشجرة BST صحيحة؟ ${tree.isValidBST()}");

  // نحاول كسر القاعدة يدويًا
  tree.root?.right?.left = TreeNode(6); // خطأ: 6 في الفرع الأيمن من 10

  print("❌ بعد التعديل، هل الشجرة ما زالت صحيحة؟ ${tree.isValidBST()}");
}

```

---

## ✅ الناتج المتوقع:

```
arduino
نسختحرير
✅ هل الشجرة BST صحيحة؟ true
❌ بعد التعديل، هل الشجرة ما زالت صحيحة؟ false

```

---

## 📌 ملخص:

| الخاصية | Validate BST |
| --- | --- |
| الهدف | التأكد من صحة قواعد شجرة البحث الثنائية |
| الطريقة الأفضل | استخدام recursion وتمرير min/max |
| التعقيد الزمني | O(n) — زيارة كل عقدة مرة واحدة |