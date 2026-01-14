Below is a **clean, interview-oriented master list** of
**25 frequently used methods / operations each** for **string, list, set, and dict**.

These are **usage-based**, not documentation dumps. If you know these well, you are **strong intermediate → advanced**.

---

# 🔹 25 Most Important **String (`str`) Methods / Operations**

1. `lower()`
2. `upper()`
3. `strip()`
4. `lstrip()`
5. `rstrip()`
6. `split()`
7. `join()`
8. `replace()`
9. `find()`
10. `index()`
11. `startswith()`
12. `endswith()`
13. `count()`
14. `isalpha()`
15. `isdigit()`
16. `isalnum()`
17. `isspace()`
18. `title()`
19. `capitalize()`
20. `swapcase()`
21. `format()`
22. f-strings (`f"{x}"`)
23. `len()`
24. `in` (substring check)
25. slicing (`s[start:end:step]`)

👉 **Interview focus**: immutability, `join` vs `+`, `find` vs `index`, slicing cost

---

# 🔹 25 Most Important **List (`list`) Methods / Operations**

1. `append()`
2. `extend()`
3. `insert()`
4. `remove()`
5. `pop()`
6. `clear()`
7. `index()`
8. `count()`
9. `sort()`
10. `sorted()`
11. `reverse()`
12. `copy()`
13. slicing (`[:]`)
14. list comprehension
15. `len()`
16. `in`
17. `enumerate()`
18. `zip()`
19. `any()`
20. `all()`
21. `sum()`
22. `min()`
23. `max()`
24. `+` (concatenation)
25. `*` (repetition)

👉 **Interview focus**: mutability, `append` vs `extend`, `pop(0)` cost, shallow copy bugs

---

# 🔹 25 Most Important **Set (`set`) Methods / Operations**

1. `add()`
2. `update()`
3. `remove()`
4. `discard()`
5. `pop()`
6. `clear()`
7. `union()`
8. `intersection()`
9. `difference()`
10. `symmetric_difference()`
11. `union (|)`
12. `intersection (&)`
13. `difference (-)`
14. `symmetric_difference (^)`
15. `issubset()`
16. `issuperset()`
17. `isdisjoint()`
18. `copy()`
19. `len()`
20. `in`
21. set comprehension
22. `frozenset()`
23. duplicate removal (`set(list)`)
24. iteration
25. hash-based membership check

👉 **Interview focus**: hashability, why lists not allowed, set vs list performance

---

# 🔹 25 Most Important **Dict (`dict`) Methods / Operations**

1. `get()`
2. `keys()`
3. `values()`
4. `items()`
5. `update()`
6. `pop()`
7. `popitem()`
8. `clear()`
9. `setdefault()`
10. `copy()`
11. dict comprehension
12. `len()`
13. `in` (key check)
14. `fromkeys()`
15. `dict()` constructor
16. key iteration
17. value iteration
18. item unpacking
19. nested dict access
20. merge (`|` in Python 3.9+)
21. `del dict[key]`
22. shallow copy behavior
23. insertion order (3.7+)
24. hashing of keys
25. immutability requirement for keys

👉 **Interview focus**: hashing, collisions, order guarantee, `get` vs `[]`, `setdefault` trap

---

## 🔑 If You Want to Be Interview-Strong

You should be able to answer:

* **What is mutable vs immutable here?**
* **Time complexity**
* **Common bug caused by misuse**
* **Why this method exists**

---

## Next Logical Step

I can:

1. Give **output-based interview questions** for all 4
2. Show **top 20 real bugs** using these methods
3. Create a **one-page printable cheat sheet**
4. Map this to **PySpark / Databricks transformations**

Say the number.
