# Insert/Delete at position

## ✍️ Insert & Delete at a Specific Position

**(إدراج أو حذف عنصر في موضع معين)**

---

## ✅ أولا: مراجعة قصيرة لهيكل القائمة

نفترض أننا نعمل على **Singly Linked List**:

```dart
dart
نسختحرير
class Node {
  int value;
  Node? next;

  Node(this.value);
}

```

```dart
dart
نسختحرير
class LinkedList {
  Node? head;

  ...
}

```

---

## ✅ 1. دالة `insertAt(int value, int position)`

### 📘 الفكرة:

- إذا `position == 0` ⇒ نستخدم `prepend`
- نمر عبر القائمة حتى نصل إلى **العقدة السابقة للموقع**
- نُدخل العقدة الجديدة في هذا الموضع

```dart
dart
نسختحرير
void insertAt(int value, int position) {
  Node newNode = Node(value);

  // إدراج في البداية
  if (position == 0) {
    newNode.next = head;
    head = newNode;
    return;
  }

  Node? current = head;
  int index = 0;

  // الوصول إلى العقدة السابقة للموقع
  while (current != null && index < position - 1) {
    current = current.next;
    index++;
  }

  if (current == null) {
    print("❌ الموضع غير صالح: القائمة أقصر من المطلوب.");
    return;
  }

  // الإدراج
  newNode.next = current.next;
  current.next = newNode;
}

```

---

## ✅ 2. دالة `deleteAt(int position)`

### 📘 الفكرة:

- إذا `position == 0` ⇒ نحذف الرأس
- نصل إلى **العقدة السابقة للعنصر المراد حذفه**
- نضبط `next` لتجاوز العقدة المحذوفة

```dart
dart
نسختحرير
void deleteAt(int position) {
  if (head == null) {
    print("❌ القائمة فارغة");
    return;
  }

  if (position == 0) {
    head = head!.next;
    return;
  }

  Node? current = head;
  int index = 0;

  // الوصول إلى العقدة السابقة للموقع
  while (current != null && index < position - 1) {
    current = current.next;
    index++;
  }

  if (current == null || current.next == null) {
    print("❌ الموضع غير صالح: لا يمكن الحذف");
    return;
  }

  // تجاوز العقدة المراد حذفها
  current.next = current.next!.next;
}

```

---

## 🧪 تجربة كاملة:

```dart
dart
نسختحرير
void main() {
  LinkedList list = LinkedList();

  list.append(10);
  list.append(20);
  list.append(30);
  list.append(40);

  print("📌 القائمة:");
  list.printList();

  list.insertAt(15, 1);
  print("✅ بعد إدراج 15 في الموضع 1:");
  list.printList();

  list.insertAt(5, 0);
  print("✅ بعد إدراج 5 في الموضع 0:");
  list.printList();

  list.insertAt(100, 10); // خاطئة

  list.deleteAt(2);
  print("🗑️ بعد حذف العقدة في الموضع 2:");
  list.printList();

  list.deleteAt(0);
  print("🗑️ بعد حذف العقدة في الموضع 0:");
  list.printList();

  list.deleteAt(20); // خاطئة
}

```

---

## ✅ الناتج المتوقع:

```
yaml
نسختحرير
📌 القائمة:
10
20
30
40
✅ بعد إدراج 15 في الموضع 1:
10
15
20
30
40
✅ بعد إدراج 5 في الموضع 0:
5
10
15
20
30
40
❌ الموضع غير صالح: القائمة أقصر من المطلوب.
🗑️ بعد حذف العقدة في الموضع 2:
5
10
20
30
40
🗑️ بعد حذف العقدة في الموضع 0:
10
20
30
40
❌ الموضع غير صالح: لا يمكن الحذف

```

---

## 📌 ملخص:

| العملية | الزمن المتوقع |
| --- | --- |
| `insertAt(position)` | O(n) |
| `deleteAt(position)` | O(n) |
| `prepend()` أو `append()` | O(1) أو O(n) |