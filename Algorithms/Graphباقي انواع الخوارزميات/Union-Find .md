# Union-Find

## 🧠 ما هي خوارزمية Union-Find؟

> خوارزمية Union-Find تُستخدم لإدارة تقسيم مجموعة من العناصر إلى مجموعات غير متداخلة (disjoint sets)، وتدعم عمليتين أساسيتين بكفاءة عالية:
> 
> - **Find:** إيجاد المجموعة التي ينتمي إليها عنصر معين.
> - **Union:** دمج مجموعتين في مجموعة واحدة.

---

## 🪜 خطوات الحل:

### ✅ الخطوة 1: تمثيل كل عنصر بمؤشر الأب (parent) الخاص به، في البداية كل عنصر هو أب نفسه

### ✅ الخطوة 2: دالة **find** لإيجاد الأب الأعلى (التمثيل) مع تقنية ضغط المسار (Path Compression) لتحسين الأداء

### ✅ الخطوة 3: دالة **union** لدمج مجموعتين بناءً على تمثيلات الأب، مع تقنية الاتحاد حسب الحجم أو الرتبة (Union by Rank/Size)

---

## 📦 كود Dart كامل مع شرح وتفصيل:

```dart
dart
نسختحرير
class UnionFind {
  late List<int> parent;
  late List<int> rank; // أو يمكن استخدام size

  /// تهيئة Union-Find لعدد n من العناصر (0 إلى n-1)
  UnionFind(int n) {
    parent = List.generate(n, (index) => index); // كل عنصر أب نفسه
    rank = List.filled(n, 0); // رتبة كل عنصر صفر في البداية
  }

  /// دالة find مع ضغط المسار Path Compression
  int find(int x) {
    if (parent[x] != x) {
      parent[x] = find(parent[x]); // تحديث الأب مباشرة
    }
    return parent[x];
  }

  /// دالة union لدمج مجموعتين
  bool union(int x, int y) {
    int rootX = find(x);
    int rootY = find(y);

    if (rootX == rootY) {
      // العنصران في نفس المجموعة مسبقاً
      return false;
    }

    // دمج المجموعة الأقل رتبة في الأعلى رتبة
    if (rank[rootX] < rank[rootY]) {
      parent[rootX] = rootY;
    } else if (rank[rootX] > rank[rootY]) {
      parent[rootY] = rootX;
    } else {
      parent[rootY] = rootX;
      rank[rootX]++;
    }

    return true;
  }

  /// دالة للتحقق إذا عنصرين في نفس المجموعة
  bool connected(int x, int y) {
    return find(x) == find(y);
  }
}

void main() {
  int n = 7; // عدد العناصر (0 إلى 6)
  UnionFind uf = UnionFind(n);

  // دمج بعض المجموعات
  uf.union(0, 1);
  uf.union(1, 2);
  uf.union(3, 4);
  uf.union(5, 6);

  print("هل 0 و 2 في نفس المجموعة؟ ${uf.connected(0, 2)}"); // true
  print("هل 0 و 3 في نفس المجموعة؟ ${uf.connected(0, 3)}"); // false

  uf.union(2, 4);

  print("بعد الدمج بين 2 و 4:");
  print("هل 0 و 4 في نفس المجموعة؟ ${uf.connected(0, 4)}"); // true
}

```

---

## 🧪 مخرجات التجربة:

```
yaml
نسختحرير
هل 0 و 2 في نفس المجموعة؟ true
هل 0 و 3 في نفس المجموعة؟ false
بعد الدمج بين 2 و 4:
هل 0 و 4 في نفس المجموعة؟ true

```

---

## 🔍 شرح تفصيلي:

| الخطوة | الوصف | الكود أو التعليق |
| --- | --- | --- |
| 1 | تهيئة المصفوفات parent و rank | `UnionFind` constructor |
| 2 | دالة find مع ضغط المسار | `find` مع التحديث الذاتي للأب |
| 3 | دالة union مع دمج المجموعات حسب الرتبة | `union` بدمج الأب الأقل رتبة للأعلى |
| 4 | دالة connected للتحقق من الانتماء لنفس المجموعة | مقارنة نتائج find |

---

## ملاحظات:

- Union-Find فعالة جداً في خوارزميات **Connected Components**، **Kruskal MST**، وحل مشاكل الشبكات.
- زمن كل عملية تقريباً O(α(n)) حيث α هي دالة Inverse Ackermann وهي شبه ثابتة.