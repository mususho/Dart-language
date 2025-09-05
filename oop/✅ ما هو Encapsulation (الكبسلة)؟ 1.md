# ✅ ما هو Encapsulation (الكبسلة)؟

## ✅ ما هو **Encapsulation** (الكبسلة)؟

> الكبسلة تعني: إخفاء التفاصيل الداخلية للكائن (Object) وجعل التفاعل معه فقط من خلال واجهات (Methods) نحددها نحن.
> 

بمعنى:

- لا يستطيع المستخدم تعديل أو الوصول مباشرة للبيانات الحساسة.
- يتم التحكم في الوصول باستخدام **Getters و Setters**.
- الهدف: **الأمان + التنظيم + تقليل الأخطاء**.

---

## 🧠 الفكرة بالتشبيه:

تخيل عندك "ماكينة قهوة":

- فيها أزرار (public methods): زر تشغيل، زر إيقاف.
- وفيها أجزاء داخلية (private): تسخين الماء، ضغط، الخ…

المستخدم يتعامل مع الأزرار فقط، ما له علاقة بكيفية عمل الماكينة داخليًا.

---

## 🟢 المستوى المبتدئ: مثال بسيط

```dart
dart
نسختحرير
class BankAccount {
  double _balance = 0; // خاص (private)

  void deposit(double amount) {
    if (amount > 0) {
      _balance += amount;
    }
  }

  void withdraw(double amount) {
    if (amount > 0 && amount <= _balance) {
      _balance -= amount;
    }
  }

  double getBalance() {
    return _balance;
  }
}

void main() {
  var account = BankAccount();
  account.deposit(1000);
  account.withdraw(200);
  print(account.getBalance()); // 800
}

```

### ✅ شرح المثال:

- `_balance`: متغير خاص لا يمكن الوصول له من خارج الكلاس.
- `deposit()` و `withdraw()`: دوال تتحكم في التفاعل مع الرصيد.
- `getBalance()`: Getter مخصص لعرض الرصيد.

---

## 🟡 المستوى المتوسط: استخدام **Getters & Setters**

```dart
dart
نسختحرير
class Student {
  String _name = '';

  // Getter
  String get name => _name;

  // Setter
  set name(String value) {
    if (value.length >= 3) {
      _name = value;
    } else {
      print("الاسم قصير جدًا");
    }
  }
}

void main() {
  var student = Student();
  student.name = "Ali"; // setter
  print(student.name);  // getter
}

```

### ✅ لماذا نستخدم Getters/Setters بدلًا من الوصول المباشر؟

- نقدر نضيف شروط قبل التغيير أو العرض.
- نمنع قيم غير صالحة.
- نحمي الكلاس من العبث العشوائي.

---

## 🟠 المستوى المتقدم: كبسلة أكثر احترافًا

```dart
dart
نسختحرير
class Temperature {
  double _celsius = 0;

  // Getter يحول للـ Fahrenheit
  double get fahrenheit => (_celsius * 9 / 5) + 32;

  // Setter يحول من Fahrenheit إلى Celsius
  set fahrenheit(double value) {
    _celsius = (value - 32) * 5 / 9;
  }

  double get celsius => _celsius;
}

void main() {
  var temp = Temperature();
  temp.fahrenheit = 98.6; // دخلنا Fahrenheit
  print(temp.celsius);    // طبعنا Celsius
}

```

### ✅ ليه استخدمنا encapsulation هنا؟

- عشان نتحكم بكيفية التحويل من/إلى درجات الحرارة.
- منع التلاعب بالقيم الداخلية بشكل مباشر.

---

## ✅ الخلاصة:

| الفائدة من Encapsulation | كيف تتحقق؟ |
| --- | --- |
| حماية البيانات | باستخدام private variables (`_`) |
| تنظيم الوصول للبيانات | من خلال `get` و `set` |
| إضافة منطق خاص عند التعديل/العرض | في الدوال أو الـ setters |
| منع التلاعب الغير مقصود بالبيانات | بمنع الوصول المباشر |

---

## 📌 علامات تدل على أنك تستخدم Encapsulation بشكل صحيح:

- تبدأ الخصائص المهمة بـ `_`.
- تستخدم `get` و `set` للوصول لها.
- يوجد منطق داخلي للتحقق من القيم.