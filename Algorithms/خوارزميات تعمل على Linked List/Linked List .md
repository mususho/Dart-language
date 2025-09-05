# Linked List

## 📘 ما هي Linked List؟

> Linked List هي هيكل بيانات خطي يتكون من عُقد (Nodes)، كل عقدة تحتوي على:
> 
- قيمة `value`
- مؤشر إلى العقدة التالية `next`

---

## 🧩 أنواع Linked List:

| النوع | التوضيح |
| --- | --- |
| **Singly Linked List** | عقدة تشير فقط إلى العقدة التالية. |
| **Doubly Linked List** | كل عقدة تشير إلى السابقة والتالية. |
| **Circular Linked List** | العقدة الأخيرة تشير إلى الأولى (دائري). |

---

## ✨ سنبدأ الآن بـ Singly Linked List — خطوة بخطوة

---

## ✅ 1. تعريف عقدة Node

```dart
dart
نسختحرير
class Node {
  int value;         // القيمة المخزنة في العقدة
  Node? next;        // الإشارة إلى العقدة التالية

  Node(this.value);  // constructor
}

```

---

## ✅ 2. تعريف قائمة مرتبطة LinkedList

```dart
dart
نسختحرير
class LinkedList {
  Node? head; // بداية القائمة

  // ✅ إضافة عنصر في النهاية
  void append(int value) {
    Node newNode = Node(value);

    if (head == null) {
      head = newNode;
      return;
    }

    Node current = head!;
    while (current.next != null) {
      current = current.next!;
    }

    current.next = newNode;
  }

  // ✅ إضافة عنصر في البداية
  void prepend(int value) {
    Node newNode = Node(value);
    newNode.next = head;
    head = newNode;
  }

  // ✅ طباعة القائمة
  void printList() {
    Node? current = head;
    while (current != null) {
      print(current.value);
      current = current.next;
    }
  }

  // ✅ حذف عنصر بالقيمة
  void delete(int value) {
    if (head == null) return;

    if (head!.value == value) {
      head = head!.next;
      return;
    }

    Node current = head!;
    while (current.next != null) {
      if (current.next!.value == value) {
        current.next = current.next!.next;
        return;
      }
      current = current.next!;
    }
  }

  // ✅ البحث عن قيمة
  bool contains(int value) {
    Node? current = head;
    while (current != null) {
      if (current.value == value) return true;
      current = current.next;
    }
    return false;
  }

  // ✅ حساب الطول
  int length() {
    int count = 0;
    Node? current = head;
    while (current != null) {
      count++;
      current = current.next;
    }
    return count;
  }
}

```

---

## 🧪 تجربة كاملة في `main()`:

```dart
dart
نسختحرير
void main() {
  LinkedList list = LinkedList();

  list.append(10);
  list.append(20);
  list.append(30);

  print("📌 القائمة بعد append:");
  list.printList();

  list.prepend(5);
  print("📌 القائمة بعد prepend:");
  list.printList();

  print("🔍 هل تحتوي على 20؟ ${list.contains(20)}");
  print("🔍 هل تحتوي على 99؟ ${list.contains(99)}");

  list.delete(20);
  print("🗑️ بعد حذف 20:");
  list.printList();

  print("📏 الطول الحالي: ${list.length()}");
}

```

---

## ✅ الناتج المتوقع:

```
yaml
نسختحرير
📌 القائمة بعد append:
10
20
30
📌 القائمة بعد prepend:
5
10
20
30
🔍 هل تحتوي على 20؟ true
🔍 هل تحتوي على 99؟ false
🗑️ بعد حذف 20:
5
10
30
📏 الطول الحالي: 3

```

---

## 📌 ملخص:

| العملية | الزمن المتوقع |
| --- | --- |
| `append` | O(n) |
| `prepend` | O(1) |
| `delete` | O(n) |
| `search` | O(n) |
| `print` | O(n) |