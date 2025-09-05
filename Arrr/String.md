# String

```dart
void main() {
  String text = "Hello Dart!";

  // ============================================== //
  // ✏️ 1. التعديل والتحويل                      ✅
  // ============================================== //
  print(text.toLowerCase()); // ➤ إلى أحرف صغيرة: "hello dart!"
  print(text.toUpperCase()); // ➤ إلى أحرف كبيرة: "HELLO DART!"
  print(text.trim()); // ➤ إزالة الفراغات من البداية والنهاية
  print(text.trimLeft()); // ➤ إزالة الفراغات من اليسار
  print(text.trimRight()); // ➤ إزالة الفراغات من اليمين
  print(text.replaceAll("l", "x")); // ➤ استبدال كل "l" بـ "x"
  print(text.replaceFirst("l", "X")); // ➤ استبدال أول "l" بـ "X"
  print(text.replaceRange(0, 5, "Hi")); // ➤ استبدال جزء من النص
  print(text.padLeft(15, "*")); // ➤ إضافة padding من اليسار
  print(text.padRight(15, "#")); // ➤ إضافة padding من اليمين
  print(text.runes.toList()); // ➤ قائمة الأكواد (Unicode)

  // ============================================== //
  // 🧪 2. الفحص                                 ✅
  // ============================================== //
  print(text.isEmpty); // ➤ هل النص فارغ؟
  print(text.isNotEmpty); // ➤ هل النص غير فارغ؟
  print(text.contains("Dart")); // ➤ هل يحتوي على "Dart"؟
  print(text.startsWith("Hello")); // ➤ هل يبدأ بـ "Hello"؟
  print(text.endsWith("!")); // ➤ هل ينتهي بـ "!"؟
  print(text == "Hello Dart!"); // ➤ مقارنة مباشرة
  print(text.compareTo("hello")); // ➤ مقارنة حسب الترتيب (lexicographically)

  // ============================================== //
  // 🔍 3. البحث                                 ✅
  // ============================================== //
  print(text.indexOf("l")); // ➤ أول index لـ "l"
  print(text.lastIndexOf("l")); // ➤ آخر index لـ "l"
  print(text.indexOf("Dart")); // ➤ بداية وجود "Dart"

  // ============================================== //
  // 🧩 4. التقطيع والتقسيم                    ✅
  // ============================================== //
  print(text.split(" ")); // ➤ تقسيم حسب فراغ
  print(text.substring(0, 5)); // ➤ استخراج جزء من النص
  print(text.characters); // ➤ تقسيم النص لأحرف حقيقية (حتى الإيموجي)

  // ============================================== //
  // 🔄 5. التكرار والمعالجة                  ✅
  // ============================================== //
  print(text * 3); // ➤ تكرار النص 3 مرات
  text.split('').forEach(print); // ➤ طباعة كل حرف على حدة
  var mapped = text.split('').map((e) => e + '-').join(); // ➤ تعديل كل حرف

  // ============================================== //
  // 🧮 6. الطول والتحويلات                    ✅
  // ============================================== //
  print(text.length); // ➤ عدد الأحرف
  print(text.codeUnits); // ➤ قائمة الأكواد (UTF-16)
  print(String.fromCharCode(65)); // ➤ تحويل كود لحرف (A)
  print("A".codeUnitAt(0)); // ➤ تحويل حرف إلى كود

  // ============================================== //
  // 🔗 7. الدمج                                ✅
  // ============================================== //
  print("Hello" + " " + "World"); // ➤ دمج النصوص
  print(["Dart", "is", "fun"].join(" ")); // ➤ دمج باستخدام join

  // ============================================== //
  // 🧠 8. مع الـ RegExp                       ✅
  // ============================================== //
  var pattern = RegExp(r"\bDart\b"); // ➤ كلمة Dart فقط
  print(pattern.hasMatch(text)); // ➤ هل يوجد تطابق؟
  print(pattern.allMatches(text)); // ➤ كل أماكن التطابق
  print(text.replaceAll(pattern, "Flutter")); // ➤ استبدال بناءً على نمط

  // ============================================== //
  // 🔍 9. الفحص اليدوي بالحروف                ✅
  // ============================================== //
  for (var ch in text.runes) {
    print(String.fromCharCode(ch)); // ➤ تحليل النص كرموز Unicode
  }

  // ============================================== //
  // 🧷 10. ثوابت مفيدة                        ✅
  // ============================================== //
  print(text.runtimeType); // ➤ نوع المتغير
  print(text.hashCode); // ➤ كود خاص بالنص (للمقارنة)
}

```