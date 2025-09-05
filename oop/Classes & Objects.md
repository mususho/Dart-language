# Classes & Objects

### **1. الكلاسات (Classes)**

**الفئة (Class)** هي **قالب** أو **نموذج** يتم تعريفه لإنشاء كائنات. وهي تحدد **الخصائص** و **السلوكيات** التي ستكون موجودة في الكائنات المشتقة منها. في الفئة، يتم تحديد المتغيرات (التي تمثل الخصائص) والدوال (التي تمثل السلوكيات) التي ستتمكن الكائنات من استخدامها.

### **بناء الجملة للفئة (Class)**:

```dart

class ClassName {
  // الخصائص (المتغيرات)
  String property1;
  int property2;

  // المُنشئ (Constructor)
  ClassName(this.property1, this.property2);

  // السلوكيات (الدوال)
  void displayInfo() {
    print("Property1: $property1, Property2: $property2");
  }
}

```

### **شرح المكونات**:

1. **الخصائص (Properties)**: هذه هي المتغيرات التي تحدد بيانات الكائن. في المثال السابق، لدينا **`property1`** من النوع **String** و **`property2`** من النوع **int**.
2. **المُنشئ (Constructor)**: هو دالة خاصة تُستخدم لإنشاء كائن من الفئة، وتقوم بتخصيص قيم للخصائص عندما يتم إنشاء الكائن. في المثال، **`ClassName(this.property1, this.property2)`** هو المُنشئ الذي يحدد كيفية إنشاء الكائن وتخصيص القيم.
3. **السلوكيات (Methods)**: هذه هي الدوال التي تحدد ما يمكن أن يفعله الكائن. في المثال السابق، **`displayInfo()`** هي دالة تقوم بعرض معلومات الكائن.

---

### **2. الكائنات (Objects)**

**الكائن (Object)** هو **نسخة** من الفئة. عند إنشاء كائن من الفئة، يتم تخصيص **ذاكرة** له، ويمكن استخدام الكائن للتفاعل مع البيانات والدوال التي تم تحديدها في الفئة. الكائن يمكن أن يحتوي على **قيم مخصصة** للخصائص التي تم تعريفها في الفئة.

### **كيفية إنشاء كائن (Object)**:

لإنشاء كائن من الفئة، نستخدم **المُنشئ** الذي تم تعريفه في الفئة.

### **بناء الجملة لإنشاء كائن**:

```dart

ClassName objectName = ClassName(value1, value2);

```

### **مثال على الفئة والكائنات**:

```dart

// تعريف الفئة (Class)
class Car {
  String model;
  int year;

  // المُنشئ
  Car(this.model, this.year);

  // دالة لعرض معلومات السيارة
  void displayInfo() {
    print("Car Model: $model, Year: $year");
  }
}

void main() {
  // إنشاء كائن من الفئة Car
  Car car1 = Car("Toyota", 2020);
  Car car2 = Car("Honda", 2021);

  // استدعاء دالة العرض
  car1.displayInfo();  // Car Model: Toyota, Year: 2020
  car2.displayInfo();  // Car Model: Honda, Year: 2021
}

```

**الإخراج**:

```

Car Model: Toyota, Year: 2020
Car Model: Honda, Year: 2021

```

### **شرح المثال**:

- **`Car`** هي **الفئة (Class)** التي تحتوي على خصائص **`model`** و **`year`**، ودالة **`displayInfo()`**.
- **`car1`** و **`car2`** هما **كائنان (Objects)** من الفئة **`Car`**. تم إنشاء كل كائن باستخدام المُنشئ `Car("Toyota", 2020)` و `Car("Honda", 2021)`.

---

### **3. التفاعل مع الكائنات (Interacting with Objects)**

بعد إنشاء الكائنات، يمكننا التفاعل معها من خلال:

1. **القراءة أو التعديل على خصائصها**: يمكن الوصول إلى الخصائص وتعديلها باستخدام الكائن.
2. **استدعاء دوالها**: يمكن استدعاء الدوال التي تم تعريفها في الفئة عن طريق الكائن.

### **مثال على التفاعل مع الكائنات**:

```dart

class Person {
  String name;
  int age;

  // المُنشئ
  Person(this.name, this.age);

  // دالة لعرض المعلومات
  void greet() {
    print("Hello, my name is $name, and I am $age years old.");
  }

  // دالة لتغيير العمر
  void setAge(int newAge) {
    age = newAge;
  }
}

void main() {
  // إنشاء كائن من الفئة Person
  Person person1 = Person("Alice", 30);

  // استدعاء دالة greet
  person1.greet();  // Hello, my name is Alice, and I am 30 years old.

  // تغيير العمر باستخدام الدالة setAge
  person1.setAge(31);
  person1.greet();  // Hello, my name is Alice, and I am 31 years old.
}

```

**الإخراج**:

```

Hello, my name is Alice, and I am 30 years old.
Hello, my name is Alice, and I am 31 years old.

```

في هذا المثال:

- **`greet()`** تعرض رسالة تحتوي على معلومات عن الشخص.
- **`setAge()`** تقوم بتعديل خاصية **`age`**.

---

### **4. التوارث (Inheritance)**

في البرمجة الكائنية التوجه (OOP)، يمكن لفئة أن ترث خصائص وسلوكيات فئة أخرى. يُسمى هذا **الوراثة**.

### **كيفية استخدام الوراثة**:

```dart

class SubClass extends SuperClass {
  // خصائص وسلوكيات إضافية
}

```

### **مثال على الوراثة**:

```dart

class Animal {
  String name;

  // المُنشئ
  Animal(this.name);

  // دالة للصوت
  void sound() {
    print("$name makes a sound");
  }
}

class Dog extends Animal {
  // المُنشئ
  Dog(String name) : super(name);

  // دالة خاصة بالكلب
  void bark() {
    print("$name barks!");
  }
}

void main() {
  // إنشاء كائن من فئة Dog
  Dog dog = Dog("Buddy");

  // استخدام دوال ورثتها من فئة Animal
  dog.sound();  // Buddy makes a sound

  // استخدام الدالة الخاصة بالكلب
  dog.bark();   // Buddy barks!
}

```

**الإخراج**:

```

Buddy makes a sound
Buddy barks!

```

- في هذا المثال، **`Dog`** يرث من **`Animal`** ويكتسب سلوكيات مثل **`sound()`**. لكن يمكنه أيضًا إضافة سلوكيات جديدة مثل **`bark()`**.

---

### **5. الأنواع المختلفة للكائنات**

الكائنات في البرمجة الكائنية التوجه يمكن أن تكون متنوعة بناءً على الفئة التي تنتمي إليها. مثلاً:

- **الكائنات الأولية (Primitive Objects)**: مثل الأرقام أو السلاسل النصية.
- **الكائنات المركبة (Composite Objects)**: مثل الكائنات التي تحتوي على خصائص ودوال.

### **مثال**: كائن من نوع **`List`** (قائمة)

```dart

void main() {
  List<int> numbers = [1, 2, 3, 4, 5];

  // الوصول إلى عنصر من القائمة
  print(numbers[2]);  // 3

  // إضافة عنصر جديد
  numbers.add(6);
  print(numbers);  // [1, 2, 3, 4, 5, 6]
}

```

---

### **الخلاصة**

- **الكلاس (Class)** هو القالب أو النموذج الذي يُحدد خصائص وسلوكيات الكائنات.
- **الكائن (Object)** هو نسخة من الفئة، ويمكنه أن يحتوي على بيانات ويقوم بتنفيذ وظائف.
- **الوراثة (Inheritance)** تسمح لفئة بأن ترث خصائص وسلوكيات فئة أخرى.
- الكائنات يمكن أن تكون **بسيطة** أو **معقدة** بناءً على الفئة التي تنتمي إليها.

البرمجة الكائنية التوجه (OOP) تُسهل تنظيم الكود، وزيادة القابلية لإعادة الاستخدام، وتقليل التعقيد من خلال تقسيم البرنامج إلى **كائنات مستقلة**.