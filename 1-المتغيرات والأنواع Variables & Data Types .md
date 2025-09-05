# 1-المتغيرات والأنواع Variables & Data Types

```dart
// Dart - جميع أنواع البيانات مع شرح وأمثلة مفصلة

void main() {
  // 🔹 int - عدد صحيح
  int age = 30;
  print("int: $age");

  // 🔹 double - عدد عشري
  double pi = 3.1415;
  print("double: $pi");

  // 🔹 num - يقبل int أو double
  num price = 100;
  price = 99.99;
  print("num: $price");

  // 🔹 bool - قيمة منطقية
  bool isOnline = true;
  print("bool: $isOnline");

  // 🔹 String - نصوص
  String name = "Ali";
  print("String: $name");

  // 🔹 List - قائمة مرتبة
  List<String> fruits = ["Apple", "Banana"];
  fruits.add("Mango");
  print("List: $fruits");

  // 🔹 Set - مجموعة بدون تكرار
  Set<int> numbers = {1, 2, 3};
  numbers.add(2); // لن يضيف 2 مجددًا
  print("Set: $numbers");

  // 🔹 Map - قاموس (مفتاح:قيمة)
  Map<String, String> capitals = {
    "Iraq": "Baghdad",
    "USA": "Washington"
  };
  print("Map: $capitals");

  // 🔹 dynamic - يمكن تغيير نوع القيمة في وقت التشغيل
  dynamic variable = 123;
  print("dynamic (int): $variable");
  variable = "Now I am a String";
  print("dynamic (String): $variable");

  // 🔹 var - نوع يتم تحديده تلقائيًا
  var city = "Erbil"; // String تلقائيًا
  print("var: $city");

  // 🔹 final - قيمة لا تتغير بعد التهيئة
  final country = "Iraq";
  print("final: $country");

  // 🔹 const - ثابت وقت الترجمة
  const gravity = 9.8;
  print("const: $gravity");

  // 🔹 Object - أعلى نوع في Dart (كل شيء يرث منه)
  Object anything = 5;
  anything = "Hello";
  print("Object: $anything");

  // 🔹 Null - القيمة الفارغة (مستخدمة مع ?)
  String? nullableName = null;
  print("Null (nullable): $nullableName");

  // 🔹 Function - دالة محفوظة داخل متغير
  Function greet = () => print("Hello from function variable");
  greet();

  // 🔹 Future - نتيجة غير متوفرة بعد (asynchronous)
  getFutureValue().then((value) => print("Future: $value"));

  // 🔹 Stream - تسلسل من القيم (مثل الأحداث)
  Stream<int> stream = numberStream();
  stream.listen((val) => print("Stream value: $val"));

  // 🔹 Record (من Dart 3.0)
  var person = ('Ali', 25);
  print("Record name: \${person.\$1}, age: \${person.\$2}");

  // 🔹 Symbol - يُستخدم في الانعكاس (نادر الاستخدام)
  Symbol sym = #myVariable;
  print("Symbol: \$sym");

  // 🔹 Never - دالة لا تعود أبدًا
  // Uncomment to test:
  // fail("Something went wrong");

  // 🔹 Iterable - النوع الأب لـ List و Set
  Iterable<int> iterable = [1, 2, 3];
  for (var item in iterable) {
    print("Iterable item: \$item");
  }
}

// دالة ترجع Future بعد تأخير
Future<String> getFutureValue() async {
  await Future.delayed(Duration(seconds: 1));
  return "Async data loaded";
}

// دالة ترجع Stream
Stream<int> numberStream() async* {
  yield 1;
  yield 2;
  yield 3;
}

// دالة لا تعود أبدًا (ترمي استثناء فقط)
Never fail(String message) {
  throw Exception(message);
}

```

### **المتغيرات (Variables) في دارت**

المتغير هو مكان في الذاكرة يتم تخزين قيمة فيه. يمكنك استخدامه لحفظ القيم مثل الأعداد أو النصوص أو أي نوع آخر من البيانات.

### **1. تعريف المتغيرات في دارت**

في دارت، هناك طرق متعددة لتعريف المتغيرات. دعنا نتعرف على بعضها:

- **`var`**: تستخدم لتعريف متغير دون تحديد نوعه، ويقوم دارت بتحديد النوع تلقائيًا بناءً على القيمة التي تُعطى للمتغير عند تعريفه.
    - مثال:
        
        ```dart
        
        var age = 25;  // دارت سيحدد أن النوع هو int
        var name = "Alice";  // دارت سيحدد أن النوع هو String
        
        ```
        
- **`final`**: تستخدم لتعريف متغير لا يمكن تغيير قيمته بعد تعريفه. هذا المتغير يمكن تعيينه مرة واحدة فقط.
    - مثال:
        
        ```dart
        
        final double pi = 3.14;
        pi = 3.14159; // خطأ! لأنه لا يمكن تغيير قيمة المتغير النهائي.
        
        ```
        
- **`const`**: تستخدم لتعريف متغير ثابت لا يمكن تغييره أيضًا، لكنه يتم تحديده في وقت الترجمة (compile-time)، مما يعني أن القيمة ثابتة في وقت بناء البرنامج.
    - مثال:
        
        ```dart
        
        const int daysInWeek = 7;
        
        ```
        
- **`dynamic`**: تستخدم لتعريف متغير يمكن تغيير نوعه طوال مدة البرنامج.
    - مثال:
        
        ```dart
        
        dynamic variable = 10;
        variable = "Hello";  // يمكن تغيير القيمة من عدد إلى نص
        
        ```
        

### **2. المعرفات (Identifiers) في دارت**

- يجب أن تبدأ معرّف المتغير (اسم المتغير) بحرف أو underscore `_`.
- لا يمكن أن يكون اسم المتغير محجوزًا (مثل الكلمات المفتاحية `int`, `if`, `return`, وغيرها).
- يمكن أن يحتوي الاسم على أرقام، لكن لا يجب أن يبدأ برقم.

---

### **أنواع البيانات (Data Types) في دارت**

الأنواع هي تصنيف للقيم التي يمكن أن يخزنها المتغير. في دارت، هناك أنواع بيانات أساسية ومتقدمة.

### **1. الأنواع الأساسية (Primitive Data Types)**

- **`int` (الأعداد الصحيحة)**:
    - يتم استخدامه لتخزين الأعداد الصحيحة مثل 1، -5، 100.
    - **مثال**:
        
        ```dart
        
        int age = 30;
        int temperature = -5;
        
        ```
        
- **`double` (الأعداد العشرية)**:
    - يتم استخدامه لتخزين الأعداد العشرية (ذات الفاصلة العشرية).
    - **مثال**:
        
        ```dart
        
        double price = 99.99;
        double pi = 3.14159;
        
        ```
        
- **`String` (النصوص)**:
    - يتم استخدامه لتخزين النصوص مثل الكلمات والجمل.
    - **مثال**:
        
        ```dart
        
        String name = "Alice";
        String greeting = "Hello, how are you?";
        
        ```
        
- **`bool` (القيم المنطقية)**:
    - يتم استخدامه لتخزين القيم المنطقية (صح أو خطأ).
    - **مثال**:
        
        ```dart
        
        bool isStudent = true;
        bool isActive = false;
        
        ```
        

### **2. الأنواع المركبة (Composite Data Types)**

- **`List` (القوائم)**:
    - يُستخدم لتخزين مجموعة من العناصر المرتبة. يمكن أن تحتوي القائمة على أي نوع من البيانات.
    - **مثال**:
        
        ```dart
        
        List<int> numbers = [1, 2, 3, 4, 5];
        List<String> fruits = ["Apple", "Banana", "Orange"];
        
        ```
        
- **`Set` (المجموعات)**:
    - يُستخدم لتخزين مجموعة من العناصر غير المكررة وغير المرتبة.
    - **مثال**:
        
        ```dart
        
        Set<String> uniqueFruits = {"Apple", "Banana", "Orange"};
        uniqueFruits.add("Apple"); // لن تتم إضافة العنصر مرة أخرى
        
        ```
        
- **`Map` (القواميس أو الخرائط)**:
    - يُستخدم لتخزين أزواج من المفتاح والقيمة. يمكن أن تكون المفاتيح والقيم من أي نوع.
    - **مثال**:
        
        ```dart
        
        Map<String, String> capitals = {
          "USA": "Washington, D.C.",
          "France": "Paris",
          "Japan": "Tokyo"
        };
        
        ```
        

### **3. النوع `dynamic`**

- يتم استخدامه عندما تريد أن يكون المتغير مرنًا، ويُسمح له بتغيير النوع خلال البرنامج.
    - **مثال**:
        
        ```dart
        
        dynamic myVariable = 10;  // هو من نوع int
        myVariable = "Hello";    // هو الآن من نوع String
        
        ```
        

### **4. النوع `null`**

- في دارت، يمكنك تحديد أن المتغير يمكن أن يكون فارغًا أو يحتوي على قيمة `null` باستخدام النوع `Null`.
    - **مثال**:
        
        ```dart
        
        String? nullableString = null;  // المتغير يمكن أن يكون فارغًا
        
        ```
        

---

### **مثال كامل لتوضيح أنواع البيانات والمتغيرات**

```dart

void main() {
  // المتغيرات
  var name = "John";      // نوعه String يتم تحديده تلقائيًا
  final int age = 25;     // final: لا يمكن تغيير قيمته
  const double pi = 3.14; // const: قيمة ثابتة طوال الوقت

  // الأنواع
  int number = 100;       // عدد صحيح
  double temperature = 36.6; // عدد عشري
  bool isActive = true;   // قيمة منطقية

  // List
  List<String> fruits = ["Apple", "Banana", "Cherry"];
  fruits.add("Mango");  // إضافة عنصر جديد للقائمة

  // Set
  Set<int> uniqueNumbers = {1, 2, 3, 4};
  uniqueNumbers.add(3);  // لن يضيف الرقم 3 مرة أخرى

  // Map
  Map<String, String> countryCapital = {
    "USA": "Washington, D.C.",
    "Germany": "Berlin",
    "Japan": "Tokyo"
  };

  // dynamic
  dynamic myVariable = 42;   // يمكن أن يكون عددًا
  myVariable = "Hello";      // يمكن أن يصبح نصًا لاحقًا

  // Output
  print("Name: $name");
  print("Age: $age");
  print("Pi: $pi");
  print("Fruits: $fruits");
  print("Country Capital: $countryCapital");
  print("Is Active: $isActive");
}

```

---

### **ملاحظات مهمة**:

1. **القيم القابلة للتغيير (Mutable) والقيم غير القابلة للتغيير (Immutable)**:
    - **القيم القابلة للتغيير** مثل `List` و `Set` يمكن تعديل محتوياتها بعد إنشائها.
    - **القيم غير القابلة للتغيير** مثل `String` و `const` لا يمكن تعديل محتوياتها بعد إنشائها.
2. **الأنواع الاختيارية (`nullable types`)**:
    - اعتبارًا من دارت 2.12، يمكن أن تكون الأنواع قابلة لأن تكون `null` (أي فارغة) إذا كانت تحتوي على `?`.
    - **مثال**: `String? name;` يعني أن المتغير `name` قد يكون نصًا أو `null`.

---

### **خلاصة**

المتغيرات هي أساسيات البرمجة في دارت، حيث تخزن القيم التي تعمل عليها. فهم الأنواع المختلفة من البيانات وكيفية استخدام المتغيرات بشكل صحيح يساعدك في كتابة كود أكثر تنظيمًا وفعالية.