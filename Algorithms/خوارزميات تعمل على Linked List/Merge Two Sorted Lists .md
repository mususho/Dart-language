# Merge Two Sorted Lists

## 🔗 Merge Two Sorted Linked Lists

**(دمج قائمتين مرتبطتين مرتبتين بترتيب تصاعدي)**

---

## 🎯 الهدف:

> عندك قائمتين مرتبطتين list1 و list2، كل منهما مرتبة تصاعديًا
> 
> 
> المطلوب دمجهما في **قائمة واحدة جديدة مرتبة أيضًا**.
> 

---

### 📘 مثال:

### القائمة الأولى:

```
نسختحرير
1 → 3 → 5

```

### القائمة الثانية:

```
نسختحرير
2 → 4 → 6

```

### ✅ الناتج بعد الدمج:

```
نسختحرير
1 → 2 → 3 → 4 → 5 → 6

```

---

## 🧠 الفكرة:

- نستخدم **مؤشران** يتحركان على القائمتين.
- ننشئ **عقد جديدة** في قائمة الناتج.
- نضيف **أصغر قيمة** في كل خطوة.
- إذا انتهت واحدة، نكمل الثانية.

---

## 🔧 الكود الكامل بلغة Dart:

### ✅ تعريف العقدة والقائمة:

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
}

```

---

### ✅ دالة دمج قائمتين `mergeSortedLists`

```dart
dart
نسختحرير
LinkedList mergeSortedLists(LinkedList list1, LinkedList list2) {
  Node? l1 = list1.head;
  Node? l2 = list2.head;

  LinkedList merged = LinkedList();
  Node? dummy = Node(0); // عقدة مؤقتة لبداية القائمة
  Node current = dummy;

  while (l1 != null && l2 != null) {
    if (l1.value < l2.value) {
      current.next = Node(l1.value);
      l1 = l1.next;
    } else {
      current.next = Node(l2.value);
      l2 = l2.next;
    }
    current = current.next!;
  }

  // إذا بقي عناصر في أحد القوائم
  while (l1 != null) {
    current.next = Node(l1.value);
    current = current.next!;
    l1 = l1.next;
  }

  while (l2 != null) {
    current.next = Node(l2.value);
    current = current.next!;
    l2 = l2.next;
  }

  merged.head = dummy.next; // نتجاوز العقدة المؤقتة
  return merged;
}

```

---

## 🧪 تجربة كاملة في `main()`:

```dart
dart
نسختحرير
void main() {
  LinkedList list1 = LinkedList();
  list1.append(1);
  list1.append(3);
  list1.append(5);

  LinkedList list2 = LinkedList();
  list2.append(2);
  list2.append(4);
  list2.append(6);

  print("📋 القائمة 1:");
  list1.printList();

  print("\n📋 القائمة 2:");
  list2.printList();

  LinkedList merged = mergeSortedLists(list1, list2);

  print("\n🔗 القائمة المدموجة:");
  merged.printList();
}

```

---

## ✅ الناتج المتوقع:

```
yaml
نسختحرير
📋 القائمة 1:
1
3
5

📋 القائمة 2:
2
4
6

🔗 القائمة المدموجة:
1
2
3
4
5
6

```

---

## 📌 ملخص:

| الخاصية | القيمة |
| --- | --- |
| الزمن | O(n + m) حيث n و m أطوال القوائم |
| استخدام الذاكرة | O(n + m) لعقد جديدة (أو O(1) إن استخدمنا القائمة نفسها) |
| نوع الترتيب | تصاعدي |
| شرط أساسي | كلا القائمتين يجب أن تكونا مرتبتين مسبقًا ✅ |