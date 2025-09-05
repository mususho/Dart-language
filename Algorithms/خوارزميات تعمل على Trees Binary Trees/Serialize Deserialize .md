# Serialize/Deserialize

## 🔄 Serialize & Deserialize Binary Tree

**(تسلسل وفك تسلسل الشجرة الثنائية)**

---

## 🎯 ما المقصود بـ "Serialize / Deserialize"؟

### ✅ Serialization:

> تحويل الشجرة إلى سلسلة نصية (String) تمثل كل العقد والفروع.
> 

### ✅ Deserialization:

> إعادة بناء الشجرة من نفس السلسلة النصية.
> 

---

### 📦 لماذا نحتاجها؟

- لنقل الشجرة عبر الشبكة (API أو ملفات).
- لتخزينها في قاعدة بيانات أو ملف.
- لنسخها أو مشاركتها بين التطبيقات.

---

## 🧠 الاستراتيجية:

نستخدم تمرير **Preorder Traversal** (جذر → يسار → يمين)، مع تمثيل العقد الفارغة بـ `null`.

### 📘 مثال على شجرة:

```
markdown
نسختحرير
        1
       / \
      2   3
         / \
        4   5

```

### ✅ Serialized شكلها:

```
arduino
نسختحرير
"1,2,null,null,3,4,null,null,5,null,null"

```

> (كل null يمثل فرع غير موجود)
> 

---

## 🔧 كود Dart لتسلسل وفك تسلسل الشجرة:

```dart

class TreeNode {
  int value;
  TreeNode? left, right;

  TreeNode(this.value);
}

class Codec {
  // ✅ تحويل الشجرة إلى سلسلة نصية (serialize)
  String serialize(TreeNode? root) {
    List<String> result = [];
    _serializeHelper(root, result);
    return result.join(',');
  }

  void _serializeHelper(TreeNode? node, List<String> result) {
    if (node == null) {
      result.add('null');
      return;
    }

    result.add(node.value.toString());
    _serializeHelper(node.left, result);
    _serializeHelper(node.right, result);
  }

  // ✅ تحويل السلسلة النصية إلى شجرة (deserialize)
  TreeNode? deserialize(String data) {
    List<String> values = data.split(',');
    return _deserializeHelper(values);
  }

  TreeNode? _deserializeHelper(List<String> values) {
    if (values.isEmpty) return null;

    String value = values.removeAt(0);
    if (value == 'null') return null;

    TreeNode node = TreeNode(int.parse(value));
    node.left = _deserializeHelper(values);
    node.right = _deserializeHelper(values);

    return node;
  }
}

```

---

## 🧪 تجربة في `main()`:

```dart

void main() {
  TreeNode root = TreeNode(1);
  root.left = TreeNode(2);
  root.right = TreeNode(3);
  root.right!.left = TreeNode(4);
  root.right!.right = TreeNode(5);

  Codec codec = Codec();

  String serialized = codec.serialize(root);
  print("📝 Serialized: $serialized");

  TreeNode? deserializedRoot = codec.deserialize(serialized);
  print("🌳 Deserialized Root Value: ${deserializedRoot?.value}");
  print("Left: ${deserializedRoot?.left?.value}");
  print("Right: ${deserializedRoot?.right?.value}");
}

```

---

## ✅ الناتج المتوقع:

```
sql
نسختحرير
📝 Serialized: 1,2,null,null,3,4,null,null,5,null,null
🌳 Deserialized Root Value: 1
Left: 2
Right: 3

```

---

## 📌 ملخص:

| العملية | الوصف |
| --- | --- |
| `serialize()` | تحويل الشجرة إلى سلسلة نصية باستخدام Preorder |
| `deserialize()` | إعادة بناء الشجرة من السلسلة النصية نفسها |
| البيانات | تمثل العقد الفارغة بـ `"null"` لتضمن الهيكل |

---