# Remove Nth From End

## 🧹 Remove N-th Node From End

**(إزالة العقدة رقم N من نهاية القائمة المرتبطة)**

---

## 🎯 الهدف:

> عندك قائمة مرتبطة مفردة (Singly Linked List)
> 
> 
> المطلوب: حذف العقدة التي تقع في **الترتيب N من النهاية**.
> 

---

### 📘 مثال:

القائمة:

```
نسختحرير
1 → 2 → 3 → 4 → 5

```

لو `n = 2`، نحذف:

```
نسختحرير
4

```

النتيجة:

```
نسختحرير
1 → 2 → 3 → 5

```

---

## 🧠 الفكرة: استخدام مؤشرين (Two-Pointer Technique)

### ✅ الخوارزمية:

1. استخدم مؤشرين: `fast` و `slow` يبدأان من `head`.
2. حرّك `fast` إلى الأمام `n` خطوات.
3. حرّك `fast` و `slow` معًا حتى يصل `fast` إلى نهاية القائمة.
4. الآن `slow` يقف قبل العقدة المطلوب حذفها.
5. نعيد توجيه `slow.next` لتجاوز العقدة المحذوفة.

---

## 🔧 كود Dart كامل:

### ✅ تعريف `Node` و `LinkedList`:

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

  // ✅ إزالة العنصر رقم n من نهاية القائمة
  void removeNthFromEnd(int n) {
    Node dummy = Node(0);
    dummy.next = head;

    Node? fast = dummy;
    Node? slow = dummy;

    // حرّك fast n خطوات للأمام
    for (int i = 0; i < n; i++) {
      if (fast?.next == null) return; // n أكبر من طول القائمة
      fast = fast!.next;
    }

    // حرّك fast و slow معًا حتى نهاية القائمة
    while (fast?.next != null) {
      fast = fast!.next;
      slow = slow!.next;
    }

    // حذف العقدة
    slow!.next = slow.next?.next;

    // تحديث الرأس إذا لزم الأمر
    head = dummy.next;
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
  list.append(5);

  print("📋 قبل الحذف:");
  list.printList();

  list.removeNthFromEnd(2);

  print("\n❌ بعد حذف العقدة رقم 2 من النهاية:");
  list.printList();
}

```

---

## ✅ الناتج المتوقع:

```
نسختحرير
📋 قبل الحذف:
1
2
3
4
5

❌ بعد حذف العقدة رقم 2 من النهاية:
1
2
3
5

```

---

## 📌 ملخص:

| الخاصية | القيمة |
| --- | --- |
| الزمن | O(n) |
| المساحة | O(1) |
| الفكرة | مؤشرين + عقدة وهمية (dummy node) |
| الحذف من النهاية مباشرة؟ | نعم ✅ |

---