# Palindrome LinkedList

## 🔁 Palindrome Linked List

**(التحقق مما إذا كانت القائمة المرتبطة تمثل كلمة متناظرة - Palindrome)**

---

## 🎯 الهدف:

> التأكد إن كانت عناصر القائمة المرتبطة تمثل نفس القيمة إذا قرأناها من الأمام أو من الخلف.
> 

---

### 📘 مثال:

### ✅ قائمة Palindrome:

```
نسختحرير
1 → 2 → 3 → 2 → 1

```

### ❌ ليست Palindrome:

```
نسختحرير
1 → 2 → 3 → 4

```

---

## 🧠 الخوارزمية (فعالة بدون تحويل إلى قائمة):

1. **ابحث عن منتصف القائمة** باستخدام مؤشرين `slow` و `fast`.
2. **اعكس النصف الثاني** من القائمة.
3. **قارن** النصف الأول بالنصف المعكوس.
4. (اختياري: استرجاع القائمة كما كانت).

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

  // ✅ التحقق من إذا ما كانت القائمة Palindrome
  bool isPalindrome() {
    if (head == null || head!.next == null) return true;

    // 1. إيجاد المنتصف
    Node? slow = head;
    Node? fast = head;

    while (fast != null && fast.next != null) {
      slow = slow!.next;
      fast = fast.next!.next;
    }

    // 2. عكس النصف الثاني
    Node? secondHalf = _reverse(slow);
    Node? copySecondHalf = secondHalf; // للحفاظ على النسخة لاسترجاع القائمة (اختياري)

    // 3. مقارنة النصفين
    Node? firstHalf = head;
    bool isPalin = true;

    while (secondHalf != null) {
      if (firstHalf!.value != secondHalf.value) {
        isPalin = false;
        break;
      }
      firstHalf = firstHalf.next;
      secondHalf = secondHalf.next;
    }

    // 4. استرجاع القائمة لو أردنا (اختياري)
    _reverse(copySecondHalf);

    return isPalin;
  }

  // 🔁 دالة لعكس القائمة
  Node? _reverse(Node? node) {
    Node? prev = null;
    Node? current = node;

    while (current != null) {
      Node? next = current.next;
      current.next = prev;
      prev = current;
      current = next;
    }

    return prev;
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
  list.append(2);
  list.append(1);

  print("📋 القائمة:");
  list.printList();

  print("\n🔍 هل هي Palindrome؟ ${list.isPalindrome() ? "✅ نعم" : "❌ لا"}");
}

```

---

## ✅ الناتج المتوقع:

```
نسختحرير
📋 القائمة:
1
2
3
2
1

🔍 هل هي Palindrome؟ ✅ نعم

```

---

## 📌 ملخص:

| الخاصية | القيمة |
| --- | --- |
| الزمن | O(n) |
| المساحة | O(1) |
| تعيد بناء القائمة؟ | نعم (اختياري) |
| تستخدم عكس داخلي؟ | نعم (reverse نصف فقط) |