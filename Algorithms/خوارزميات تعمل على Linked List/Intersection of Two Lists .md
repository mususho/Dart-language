# Intersection of Two Lists

## 🎯 الهدف:

> لديك قائمتين مرتبطتين (Singly Linked Lists)، قد تتقاطعان عند نقطة معينة
> 
> 
> نريد معرفة إن كانت هناك **عقدة مشتركة** (أي أن العقدة نفسها وليس فقط القيمة)، وإذا وُجدت، نرجع تلك العقدة.
> 

---

### 📘 مثال:

```
makefile
نسختحرير
listA: 1 → 3 → 5 \
                   → 7 → 9
listB:       2 → 4 /

```

**النتيجة:** العقدة `7`

(وليس لأن قيمتها 7، بل لأن نفس الكائن في الذاكرة هو ما تشير إليه كلتا القائمتين)

---

## 🧠 الحل: Two-Pointer Approach (ذكي جدًا)

1. استخدم مؤشرين `a` و `b` لكل من القائمتين.
2. كل مرة تحرك كل مؤشر إلى `next`.
3. عندما يصل أحدهما إلى `null`، ابدأ من رأس القائمة الأخرى.
4. سيلتقيان في **نقطة التقاطع** أو ينتهيان معًا في `null`.

---

## ✅ لماذا يعمل هذا؟

> كلا المؤشرين يسيران بنفس عدد الخطوات
> 
> 
> (A + B + الجزء المشترك)
> 

---

## 🔧 كود Dart كامل:

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

  void appendNode(Node node) {
    if (head == null) {
      head = node;
      return;
    }

    Node current = head!;
    while (current.next != null) {
      current = current.next!;
    }

    current.next = node;
  }

  void printList() {
    Node? current = head;
    while (current != null) {
      print(current.value);
      current = current.next;
    }
  }
}

// ✅ إيجاد نقطة الالتقاء
Node? getIntersection(Node? headA, Node? headB) {
  Node? a = headA;
  Node? b = headB;

  while (a != b) {
    a = (a != null) ? a.next : headB;
    b = (b != null) ? b.next : headA;
  }

  return a; // إما العقدة المشتركة أو null
}

```

---

## 🧪 تجربة في `main()`:

```dart
dart
نسختحرير
void main() {
  // إنشاء عقد مشتركة
  Node common = Node(7);
  common.next = Node(9);

  // إنشاء القائمة A: 1 → 3 → 5 → 7 → 9
  LinkedList listA = LinkedList();
  listA.appendNode(Node(1));
  listA.appendNode(Node(3));
  listA.appendNode(Node(5));
  listA.appendNode(common);

  // إنشاء القائمة B: 2 → 4 → 7 → 9
  LinkedList listB = LinkedList();
  listB.appendNode(Node(2));
  listB.appendNode(Node(4));
  listB.appendNode(common); // نفس العقدة المشتركة

  print("📋 القائمة A:");
  listA.printList();

  print("\n📋 القائمة B:");
  listB.printList();

  Node? intersection = getIntersection(listA.head, listB.head);
  print("\n🔍 نقطة التقاطع: ${intersection != null ? intersection.value : "❌ لا يوجد"}");
}

```

---

## ✅ الناتج المتوقع:

```
yaml
نسختحرير
📋 القائمة A:
1
3
5
7
9

📋 القائمة B:
2
4
7
9

🔍 نقطة التقاطع: 7

```

---

## 📌 ملخص:

| الخاصية | القيمة |
| --- | --- |
| الزمن | O(n + m) |
| المساحة | O(1) |
| المقارنة | بالعقد (المؤشرات)، وليس القيم |
| شرط أساسي | العقدة نفسها يجب أن تكون مشتركة |

---