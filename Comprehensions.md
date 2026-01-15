Below are **hard / interview-level** comprehension problems.
Each example is structured as:

* **Problem**
* **Code**
* **Final Answer**
* **Why it works (step-by-step, precise)**

No tricks skipped.

---

# 1️⃣ LIST COMPREHENSION — Hard (5)

---

## L1. Nested loops + condition order

### Problem

```python
result = [i * j for i in range(3) for j in range(3) if i != j]
```

### Final Answer

```python
[0, 0, 2, 0, 2, 0]
```

### Why

Execution order:

```text
for i in range(3):
    for j in range(3):
        if i != j:
            append(i*j)
```

| i | j | i!=j | i*j |
| - | - | ---- | --- |
| 0 | 1 | ✓    | 0   |
| 0 | 2 | ✓    | 0   |
| 1 | 0 | ✓    | 0   |
| 1 | 2 | ✓    | 2   |
| 2 | 0 | ✓    | 0   |
| 2 | 1 | ✓    | 2   |

---

## L2. Conditional expression inside comprehension

### Problem

```python
lst = [1, 2, 3, 4, 5]
res = [x if x % 2 == 0 else x * 10 for x in lst]
```

### Final Answer

```python
[10, 2, 30, 4, 50]
```

### Why

* `if-else` is **expression**, not filter
* Always returns one value per element

---

## L3. Function call + side effect logic

### Problem

```python
def f(x):
    return x + 1

res = [f(i) for i in range(3) if f(i) % 2 == 0]
```

### Final Answer

```python
[2, 4]
```

### Why

`f(i)` is called **twice** per iteration.

| i | f(i) | condition | output |
| - | ---- | --------- | ------ |
| 0 | 1    | False     | ❌      |
| 1 | 2    | True      | 2      |
| 2 | 3    | False     | ❌      |
| 3 | 4    | True      | 4      |

---

## L4. Shadowing variable names

### Problem

```python
res = [i for i in range(5) if i in [i*i for i in range(5)]]
```

### Final Answer

```python
[0, 1, 4]
```

### Why

Inner `i` is **independent**.

Inner list:

```python
[i*i for i in range(5)] → [0,1,4,9,16]
```

Outer checks:

```text
0 ✓, 1 ✓, 2 ✗, 3 ✗, 4 ✓
```

---

## L5. Flatten + filter

### Problem

```python
matrix = [[1,2,3],[4,5,6],[7,8,9]]
res = [x for row in matrix for x in row if x % 3 == 0]
```

### Final Answer

```python
[3, 6, 9]
```

### Why

Flatten first, then filter.

---

# 2️⃣ SET COMPREHENSION — Hard (5)

---

## S1. Duplicate elimination + math

### Problem

```python
res = {x % 3 for x in range(10)}
```

### Final Answer

```python
{0, 1, 2}
```

### Why

Set removes duplicates.

---

## S2. Nested comprehension inside set

### Problem

```python
res = {i*j for i in range(3) for j in range(3)}
```

### Final Answer

```python
{0, 1, 2, 4}
```

### Why

Generated values:

```text
0,0,0,0,1,2,0,2,4 → unique only
```

---

## S3. Conditional + boolean math

### Problem

```python
res = {x for x in range(6) if x % 2 == 0 or x % 3 == 0}
```

### Final Answer

```python
{0, 2, 3, 4}
```

### Why

* OR condition
* `0` satisfies both

---

## S4. Function call inside condition

### Problem

```python
def g(x):
    return x * x

res = {x for x in range(5) if g(x) < 10}
```

### Final Answer

```python
{0, 1, 2, 3}
```

### Why

`g(4) = 16` ❌

---

## S5. Set comprehension from list with duplicates

### Problem

```python
lst = [1,2,2,3,3,3]
res = {x for x in lst if x > 1}
```

### Final Answer

```python
{2, 3}
```

---

# 3️⃣ DICT COMPREHENSION — Hard (5)

---

## D1. Value overwrite (key collision)

### Problem

```python
res = {x % 3: x for x in range(6)}
```

### Final Answer

```python
{0: 3, 1: 4, 2: 5}
```

### Why

Later values overwrite earlier ones.

---

## D2. Conditional inside value

### Problem

```python
res = {x: "even" if x % 2 == 0 else "odd" for x in range(5)}
```

### Final Answer

```python
{0:'even', 1:'odd', 2:'even', 3:'odd', 4:'even'}
```

---

## D3. Filtering keys

### Problem

```python
res = {x: x*x for x in range(6) if x*x > 10}
```

### Final Answer

```python
{4: 16, 5: 25}
```

---

## D4. Swap keys and values (risk of loss)

### Problem

```python
d = {'a':1, 'b':1, 'c':2}
res = {v: k for k, v in d.items()}
```

### Final Answer

```python
{1: 'b', 2: 'c'}
```

### Why

Key `1` overwritten (`'a'` lost).

---

## D5. Nested dict comprehension

### Problem

```python
matrix = [[1,2],[3,4]]
res = {(i,j): matrix[i][j] for i in range(2) for j in range(2)}
```

### Final Answer

```python
{(0,0):1, (0,1):2, (1,0):3, (1,1):4}
```

---

## 🔑 Key Interview Takeaways

1. **Order matters** (`for → for → if`)
2. **Expression vs filter** is a common trap
3. **Functions inside comprehensions can execute multiple times**
4. **Dict keys overwrite silently**
5. **Inner variable names do NOT leak**

---

Below is the **exact execution order of comprehensions**, explained **formally and precisely**, with **no shortcuts**.
This is a **frequent interview trap**.

---

# 1️⃣ General Rule (Applies to list / set / dict)

A comprehension executes **left to right**, exactly like **nested `for` loops written in the same order**.

### General form

```python
[ EXPR for A in iterable1 for B in iterable2 if CONDITION ]
```

### Equivalent expanded form

```python
result = []
for A in iterable1:
    for B in iterable2:
        if CONDITION:
            result.append(EXPR)
```

➡️ **All `for` clauses run first (left → right)**
➡️ `if` is evaluated **last**
➡️ Expression (`EXPR`) is evaluated **only if `if` passes**

---

# 2️⃣ Step-by-Step Execution Order

### Comprehension Syntax Order

```
EXPR
for x in X
for y in Y
if CONDITION
```

### Runtime Execution Order

1. `for x in X`
2. `for y in Y`
3. evaluate `CONDITION`
4. evaluate `EXPR`
5. append / insert result

⚠️ **The EXPR is written first but executed last**

---

# 3️⃣ Example 1 — Simple Case

```python
res = [x*y for x in [1,2] for y in [3,4]]
```

### Execution

```python
for x in [1,2]:
    for y in [3,4]:
        res.append(x*y)
```

### Output

```python
[3, 4, 6, 8]
```

---

# 4️⃣ Example 2 — `if` filter position matters

```python
res = [x*y for x in range(3) for y in range(3) if x != y]
```

### Execution

```python
for x in range(3):
    for y in range(3):
        if x != y:
            res.append(x*y)
```

### Output

```python
[0, 0, 2, 0, 2, 0]
```

✔ `if` applies to **both loops**

---

# 5️⃣ Example 3 — Multiple `if` conditions

```python
res = [x*y for x in range(5) if x % 2 == 0 for y in range(5) if y > x]
```

### Execution Order

```python
for x in range(5):
    if x % 2 == 0:
        for y in range(5):
            if y > x:
                res.append(x*y)
```

### Output

```python
[0, 0, 0, 4, 6, 8]
```

---

# 6️⃣ Example 4 — `if-else` inside expression (NOT a filter)

```python
res = [x if x % 2 == 0 else -x for x in range(5)]
```

### Execution

```python
for x in range(5):
    res.append(x if x % 2 == 0 else -x)
```

### Output

```python
[0, -1, 2, -3, 4]
```

⚠️ **This does NOT filter elements**

---

# 7️⃣ Example 5 — Function calls (important trap)

```python
def f(x):
    print(f"f({x})")
    return x + 1

res = [f(i) for i in range(3) if f(i) % 2 == 0]
```

### Execution Order

```
f(0) → condition check → skip
f(1) → condition check → f(1) again → append
f(2) → condition check → skip
```

### Output

```python
f(0)
f(1)
f(1)
f(2)
[2]
```

⚠️ **Function called twice per element**

---

# 8️⃣ Dict Comprehension Execution Order

```python
res = {x % 2: x for x in range(5)}
```

### Execution

```python
for x in range(5):
    res[x % 2] = x
```

### Final Output

```python
{0: 4, 1: 3}
```

✔ Last write wins

---

# 9️⃣ Set Comprehension Execution Order

```python
res = {x % 3 for x in range(6)}
```

### Execution

```python
for x in range(6):
    res.add(x % 3)
```

### Output

```python
{0, 1, 2}
```

---

# 🔟 Mental Model (Interview Gold)

### Always rewrite comprehension into loops

If you can convert:

```python
[expr for a in A for b in B if cond]
```

Into:

```python
for a in A:
    for b in B:
        if cond:
            expr
```

➡️ You **will never get it wrong**

---

## One-line Rule to Remember

> **Read comprehension left-to-right, execute it top-to-bottom as nested loops.**

---





Tell me what to continue with.
