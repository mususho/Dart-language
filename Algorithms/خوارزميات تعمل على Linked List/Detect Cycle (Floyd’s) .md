# Detect Cycle (Floyd’s)

## 🔁 Detect Cycle in Linked List

**(اكتشاف دورة داخل القائمة المرتبطة باستخدام خوارزمية فلويد Floyd’s Algorithm)**

---

## 🎯 ما الهدف؟

> نريد معرفة إن كانت هناك حلقة مغلقة داخل القائمة المرتبطة، أي أن بعض العقد تشير إلى عقدة سابقة بدلًا من null.
> 

---

## 🧩 مثال:

### ✅ قائمة بدون دورة:

```
csharp
نسختحرير
1 → 2 → 3 → 4 → null

```

### ❌ قائمة بها دورة:

```
markdown
نسختحرير
1 → 2 → 3 → 4
          ↑   ↓
          ← ← ←

```

- العقدة `4.next = 2` ← حلقة

---

## 🧠 ما هي خوارزمية Floyd؟

> تُعرف أيضًا بـ Tortoise and Hare Algorithm
> 

### ✅ الفكرة:

- نستخدم مؤشرين:
    - `slow` يتحرك خطوة واحدة.
    - `fast` يتحرك خطوتين.
- إذا **وجدت دورة**، فإن `slow` و `fast` سيلتقيان داخل الحلقة.
- إذا وصلت `fast` إلى null → لا توجد دورة.

---

## ✅ الكود الكامل في Dart:

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

  // ✅ كشف وجود دورة باستخدام Floyd's Cycle Detection
  bool hasCycle() {
    Node? slow = head;
    Node? fast = head;

    while (fast != null && fast.next != null) {
      slow = slow!.next;
      fast = fast.next!.next;

      if (slow == fast) {
        return true; // ❌ دورة موجودة
      }
    }

    return false; // ✅ لا توجد دورة
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

  // لا دورة:
  print("🔍 هل توجد دورة؟ ${list.hasCycle()}");

  // نُنشئ دورة يدويًا: العقدة الأخيرة تشير إلى الثانية
  Node? node2 = list.head?.next;
  Node? last = list.head;
  while (last?.next != null) {
    last = last!.next;
  }
  last?.next = node2; // إنشاء دورة

  print("🔁 بعد إنشاء دورة يدويًا:");
  print("🔍 هل توجد دورة؟ ${list.hasCycle()}");
}

```

---

## ✅ الناتج المتوقع:

```
arduino
نسختحرير
🔍 هل توجد دورة؟ false
🔁 بعد إنشاء دورة يدويًا:
🔍 هل توجد دورة؟ true

```

---

## 📌 ملخص:

| الخاصية | Floyd’s Cycle Detection |
| --- | --- |
| هل تستهلك ذاكرة إضافية؟ | ❌ لا (O(1) space) |
| التعقيد الزمني | O(n) |
| الفكرة | مؤشرين يتحركان بسرعتين مختلفتين |

---

هل تحب أن أريك أيضًا كيف يمكن **تحديد بداية الحلقة داخل القائمة** بعد اكتشافها؟

أو تود تجربة حلقة في Doubly Linked List والتعامل معها؟

اطرح سؤالك على ChatGPT

الأدوات