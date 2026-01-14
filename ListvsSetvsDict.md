Below is a **deep, interview-grade explanation of list vs set vs dict comprehensions**, followed by
**60 questions total (20 each)** at **medium → expert level**, **each explained with a code snippet**.

This is **dense by design**. Save it and study in passes.

---

# 1️⃣ First: Mental Model (Very Important)

| Comprehension | Purpose             | Allows duplicates | Key constraint            |
| ------------- | ------------------- | ----------------- | ------------------------- |
| **List**      | Ordered collection  | ✅ Yes             | None                      |
| **Set**       | Unique elements     | ❌ No              | Elements must be hashable |
| **Dict**      | Key → value mapping | ❌ Keys unique     | Keys must be hashable     |

---

# 2️⃣ Syntax Comparison (Same Logic, Different Output)

```python
nums = [1, 2, 2, 3]

lst = [x*x for x in nums]
st  = {x*x for x in nums}
dct = {x: x*x for x in nums}
```

Result:

```python
lst → [1, 4, 4, 9]
st  → {1, 4, 9}
dct → {1:1, 2:4, 3:9}
```

---

# 🔹 PART A — 20 LIST COMPREHENSION QUESTIONS (Medium → Expert)

---

### **L1. Why list comprehension preserves order?**

```python
[x for x in [3,1,2]]
```

**Answer:** Lists are ordered collections; comprehension respects iteration order.

---

### **L2. Difference between loop vs list comprehension in bytecode**

```python
[x*x for x in range(5)]
```

**Explanation:** Runs at C-level loop internally → fewer Python opcodes.

---

### **L3. Nested list comprehension execution order**

```python
[(i, j) for i in range(2) for j in range(3)]
```

**Order:** Outer loop (`i`) first, inner (`j`) second.

---

### **L4. Conditional filtering**

```python
[x for x in range(10) if x % 2 == 0]
```

Filter happens **after iteration**, not before.

---

### **L5. Conditional expression (ternary)**

```python
[x if x > 0 else 0 for x in [-1, 2, -3]]
```

Different from `if` filter.

---

### **L6. Scope isolation**

```python
x = 10
lst = [x for x in range(3)]
print(x)  # 10
```

Comprehension has its **own scope** (Python 3+).

---

### **L7. Late binding trap**

```python
funcs = [lambda: i for i in range(3)]
[f() for f in funcs]  # [2,2,2]
```

All lambdas reference **same `i`**.

---

### **L8. Fix late binding**

```python
funcs = [lambda i=i: i for i in range(3)]
```

---

### **L9. Memory impact**

```python
import sys
sys.getsizeof([i for i in range(10000)])
```

List stores **all elements eagerly**.

---

### **L10. Comprehension with function calls**

```python
[x for x in data if validate(x)]
```

Function runs **for every element** → expensive.

---

### **L11. Flatten nested list**

```python
[x for sub in [[1,2],[3,4]] for x in sub]
```

---

### **L12. Matrix transpose**

```python
[[row[i] for row in matrix] for i in range(len(matrix[0]))]
```

---

### **L13. Side effects inside comprehension (bad)**

```python
[x.append(1) for x in lists]  # anti-pattern
```

---

### **L14. Exception handling inside comprehension**

❌ Not allowed directly
✅ Must use function wrapper

---

### **L15. Readability vs cleverness**

```python
[x for x in data if x>0 if x%2==0 if x<100]
```

Hard to maintain → interview red flag.

---

### **L16. Performance vs generator**

```python
[x*x for x in range(1000)]
(x*x for x in range(1000))
```

---

### **L17. Why list comprehension faster than append loop?**

Fewer attribute lookups (`append` avoided).

---

### **L18. Copy list safely**

```python
new = [x for x in old]
```

---

### **L19. Filter + transform combined**

```python
[x*x for x in nums if x>0]
```

---

### **L20. When NOT to use list comprehension**

* Complex logic
* Side effects
* Very large data (use generator)

---

# 🔹 PART B — 20 SET COMPREHENSION QUESTIONS (Medium → Expert)

---

### **S1. Why duplicates removed automatically?**

```python
{x for x in [1,2,2,3]}
```

Set enforces uniqueness via hashing.

---

### **S2. Why order is lost?**

Sets are **hash tables**, not sequences.

---

### **S3. Hashability requirement**

```python
{x for x in [(1,2), (3,4)]}  # OK
{x for x in [[1,2]]}        # ❌ TypeError
```

---

### **S4. Fast membership test**

```python
{x for x in data if x in lookup_set}
```

---

### **S5. Deduplication idiom**

```python
unique = {x for x in lst}
```

---

### **S6. Filtering large datasets**

```python
{x for x in logs if x.level=="ERROR"}
```

---

### **S7. Set vs list comprehension performance**

Membership check: **set wins**

---

### **S8. Set comprehension with function calls**

```python
{normalize(x) for x in data}
```

Duplicates may collapse after function call.

---

### **S9. Intersection via comprehension**

```python
{x for x in a if x in b}
```

---

### **S10. Difference vs built-in set ops**

```python
a & b  # faster than comprehension
```

---

### **S11. Removing falsy values**

```python
{x for x in data if x}
```

---

### **S12. Frozenset comprehension**

```python
frozenset(x for x in data)
```

---

### **S13. Side effects warning**

Same as list — avoid.

---

### **S14. Memory vs list**

Set uses **more memory per element**.

---

### **S15. Unpredictable iteration**

```python
list({1,2,3})
```

---

### **S16. Set of computed keys**

```python
{user.id for user in users}
```

---

### **S17. When set comprehension is wrong**

When **order matters**.

---

### **S18. Filtering unique transformed values**

```python
{email.lower() for email in emails}
```

---

### **S19. Why no index access?**

Sets have **no positional indexing**.

---

### **S20. Real-world use**

* Deduplication
* Membership tests
* Fast filtering

---

# 🔹 PART C — 20 DICT COMPREHENSION QUESTIONS (Medium → Expert)

---

### **D1. Basic structure**

```python
{x: x*x for x in range(5)}
```

---

### **D2. Duplicate keys overwrite**

```python
{x%2: x for x in range(5)}
```

Last value wins.

---

### **D3. Filtering keys**

```python
{k:v for k,v in data.items() if v>0}
```

---

### **D4. Transforming values**

```python
{k: v*2 for k,v in d.items()}
```

---

### **D5. Swapping keys & values**

```python
{v:k for k,v in d.items()}
```

Fails if values not unique.

---

### **D6. Nested dict comprehension**

```python
{k:{i:i*i for i in range(3)} for k in keys}
```

---

### **D7. Conditional expression**

```python
{k: v if v>0 else 0 for k,v in d.items()}
```

---

### **D8. Dictionary from two lists**

```python
{k:v for k,v in zip(keys, values)}
```

---

### **D9. Grouping pattern**

```python
groups = {}
for x in data:
    groups.setdefault(x.type, []).append(x)
```

(Dict comprehension **not ideal** here.)

---

### **D10. Counting pattern**

```python
{k: data.count(k) for k in set(data)}
```

Inefficient → interview trap.

---

### **D11. Efficient counting**

```python
from collections import Counter
```

---

### **D12. Default dict replacement**

```python
{k:0 for k in keys}
```

---

### **D13. Key hashability rule**

```python
{[1,2]:3}  # ❌
```

---

### **D14. Dict comprehension vs loop readability**

Loops preferred for complex logic.

---

### **D15. Flatten nested dict**

```python
{k2:v2 for k1,d2 in data.items() for k2,v2 in d2.items()}
```

---

### **D16. JSON transformation**

```python
{item["id"]: item["value"] for item in json_data}
```

---

### **D17. Performance note**

Dict comprehension faster than repeated assignment.

---

### **D18. Copy dict safely**

```python
{k:v for k,v in d.items()}
```

---

### **D19. Conditional key inclusion**

```python
{k:v for k,v in d.items() if k.startswith("a")}
```

---

### **D20. When dict comprehension is wrong**

* Multi-step logic
* Accumulation
* Grouping

---

# 🎯 Final Interview Rule (Memorize This)

> **List → order & duplicates
> Set → uniqueness & speed
> Dict → key-value mapping**

If you want next:

* 🔥 **30 output-based comprehension traps**
* ⚙ **Performance & internals deep dive**
* 🧠 **Comprehension vs PySpark transformations**
* 📄 **Printable cheat sheet**

Tell me which one.
