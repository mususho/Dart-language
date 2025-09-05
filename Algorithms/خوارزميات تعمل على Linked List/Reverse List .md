# Reverse List

## 🔄 Reverse Linked List

**(عكس اتجاه قائمة مرتبطة Singly أو Doubly)**

---

## 🎯 الهدف:

> تحويل القائمة المرتبطة بحيث تصبح آخر عقدة هي الأولى، والعكس.
> 

مثلاً من:

```
csharp
نسختحرير
1 → 2 → 3 → null

```

تصبح:

```
csharp
نسختحرير
3 → 2 → 1 → null

```

---

## 🧠 طريقة العكس في Singly Linked List

### الخطوات:

1. نحافظ على ثلاثة مؤشرات:
    - `prev` → العقدة السابقة (تبدأ بـ null)
    - `current` → العقدة الحالية (تبدأ بـ head)
    - `next` → نحفظ العقدة التالية مؤقتًا
2. في كل تكرار:
    - نوجّه `current.next` إلى `prev`
    - نحرّك `prev` و `current` خطوة للأمام
3. في النهاية، نعيد `prev` كـ `head` الجديد.

---

## 🔧 كود Dart لعكس Singly Linked List:

### ✅ تحديث `LinkedList`:

```dart
dart
نسختحرير
class Node {
  int value;
  Node? next;

  Node(this.value);
}

class LinkedList {
  Node? head;

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

  void printList() {
    Node? current = head;
    while (current != null) {
      print(current.value);
      current = current.next;
    }
  }

  // ✅ عكس القائمة
  void reverse() {
    Node? prev = null;
    Node? current = head;
    Node? next;

    while (current != null) {
      next = current.next;      // حفظ العقدة التالية
      current.next = prev;      // عكس الاتجاه
      prev = current;           // تحريك المؤشر السابق
      current = next;           // تحريك الحالي
    }

    head = prev; // الرأس الجديد هو آخر عنصر قديم
  }
}

```

---

## 🧪 تجربة في `main()`:

```dart
dart
نسختحرير
void main() {
  LinkedList list = LinkedList();

  list.append(1);
  list.append(2);
  list.append(3);
  list.append(4);

  print("📋 القائمة قبل العكس:");
  list.printList();

  list.reverse();

  print("🔁 القائمة بعد العكس:");
  list.printList();
}

```

---

## ✅ الناتج المتوقع:

```
نسختحرير
📋 القائمة قبل العكس:
1
2
3
4
🔁 القائمة بعد العكس:
4
3
2
1

```

---

## 📌 ملخص:

| العملية | الزمن | الفكرة |
| --- | --- | --- |
| `reverse()` | O(n) | استخدام 3 مؤشرات لعكس كل `next` pointer |

---

## 🧠 ملاحظة: ماذا عن Doubly Linked List؟

في `DoublyLinkedList`:

- تحتاج إلى **تبديل `next` و `prev`** في كل عقدة.
- ثم **تحديث `head` و `tail`** بعد الانتهاء.