# Doubly Linked List؟

## 🧩 ما هي Doubly Linked List؟

> هي قائمة مرتبطة تحتوي على مؤشرين في كل عقدة:
> 
- `next` → يشير إلى العقدة التالية
- `prev` → يشير إلى العقدة السابقة

---

## 🔄 الفرق بينها وبين Singly Linked List:

| الخاصية | Singly Linked List | Doubly Linked List |
| --- | --- | --- |
| اتجاه المؤشرات | واحد فقط (→) | اتجاهين (← →) |
| الوصول للخلف | غير ممكن مباشرة | ممكن باستخدام `prev` |
| الإضافة/الحذف من الخلف | O(n) | O(1) (لو عندنا tail) |
| الحجم | أقل حجمًا | أكبر حجمًا (بسبب `prev`) |

---

## ✅ الخطوات الأساسية:

### 1. إنشاء `DoublyNode`

### 2. إنشاء `DoublyLinkedList`

### 3. دعم العمليات: append, prepend, delete, print, insertAt, reverse, length

---

## 🧱 الكود الكامل:

```dart
dart
نسختحرير
class DoublyNode {
  int value;
  DoublyNode? prev;
  DoublyNode? next;

  DoublyNode(this.value);
}

class DoublyLinkedList {
  DoublyNode? head;
  DoublyNode? tail;
  int _length = 0;

  // ✅ إضافة في النهاية
  void append(int value) {
    DoublyNode newNode = DoublyNode(value);

    if (head == null) {
      head = tail = newNode;
    } else {
      tail!.next = newNode;
      newNode.prev = tail;
      tail = newNode;
    }

    _length++;
  }

  // ✅ إضافة في البداية
  void prepend(int value) {
    DoublyNode newNode = DoublyNode(value);

    if (head == null) {
      head = tail = newNode;
    } else {
      newNode.next = head;
      head!.prev = newNode;
      head = newNode;
    }

    _length++;
  }

  // ✅ طباعة من البداية للنهاية
  void printForward() {
    DoublyNode? current = head;
    while (current != null) {
      print(current.value);
      current = current.next;
    }
  }

  // ✅ طباعة من النهاية للبداية
  void printBackward() {
    DoublyNode? current = tail;
    while (current != null) {
      print(current.value);
      current = current.prev;
    }
  }

  // ✅ حذف أول عنصر يحمل القيمة المعطاة
  void delete(int value) {
    DoublyNode? current = head;

    while (current != null) {
      if (current.value == value) {
        if (current == head) {
          head = head!.next;
          head?.prev = null;
        } else if (current == tail) {
          tail = tail!.prev;
          tail?.next = null;
        } else {
          current.prev!.next = current.next;
          current.next!.prev = current.prev;
        }
        _length--;
        return;
      }
      current = current.next;
    }
  }

  // ✅ طول القائمة
  int length() => _length;
}

```

---

## 🧪 تجربة في `main()`:

```dart
dart
نسختحرير
void main() {
  DoublyLinkedList list = DoublyLinkedList();

  list.append(10);
  list.append(20);
  list.append(30);

  print("📋 القائمة من البداية للنهاية:");
  list.printForward();

  print("\n📋 القائمة من النهاية للبداية:");
  list.printBackward();

  print("\n🗑️ حذف العنصر 20:");
  list.delete(20);
  list.printForward();

  print("\n📌 الطول: ${list.length()}");

  print("\n🔼 إضافة 5 في البداية:");
  list.prepend(5);
  list.printForward();
}

```

---

## ✅ الناتج المتوقع:

```
yaml
نسختحرير
📋 القائمة من البداية للنهاية:
10
20
30

📋 القائمة من النهاية للبداية:
30
20
10

🗑️ حذف العنصر 20:
10
30

📌 الطول: 2

🔼 إضافة 5 في البداية:
5
10
30

```

---

## 📌 ملخص:

| العملية | الزمن |
| --- | --- |
| append / prepend | O(1) |
| delete by value | O(n) |
| print forward/back | O(n) |
| الوصول للعناصر | O(n) |