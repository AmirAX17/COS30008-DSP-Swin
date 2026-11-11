# COS30008 — Theory questions from past papers

These are the short-answer theory questions from the **2021 S1, 2022 S1, 2023 S1 and January 2024 final exams**, grouped so the repeated questions aren't printed three times. **20 distinct questions, 40 appearances across four finals.** The question wording is kept close to the papers; the answers below are **suggested revision answers**, not official marking solutions.

**Important — limited writing space in the real paper:** The past finals ask for answers in **one or two sentences** and provide small answer boxes. Don't prepare a paragraph for every question. Aim for the essential keywords and a concise, accurate explanation that fits the space. The answers here are intentionally short; adjust the detail to the marks and exact wording.

## Repeated theory questions — 2021, 2022 and January 2024

These ten questions appear in **2021 P1(a–j), 2022 P5(a–j), and January 2024 P5(a–j)**, though the order changes. Each paper allocates **50 marks** to this set.

### 1. How can we construct a tree where all nodes/subtrees have the same degree? — 4 marks

**Appears:** 2021 P1(a); 2022 P5(a); 2024 P5(a).

**Suggested answer:** Use a fixed-arity recursive tree definition: for a ternary tree, each non-empty node has three subtree positions (left, middle, right), with absent children represented by empty trees/NIL.

### 2. What is the difference between l-value and r-value references? — 6 marks

**Appears:** 2021 P1(c); 2022 P5(b); 2024 P5(b).

**Suggested answer:** `T&` normally binds to an lvalue (an object with identity), whereas `T&&` binds to rvalues such as temporaries or explicitly moved expressions. Rvalue references enable move semantics and resource transfer.

### 3. What is a key concept of abstract data types? — 4 marks

**Appears:** 2021 P1(e); 2022 P5(c); 2024 P5(c).

**Suggested answer:** An ADT specifies *what operations do* rather than *how data is stored*. Its interface and behaviour are separated from its hidden implementation.

### 4. How do we define mutually dependent classes in C++? — 4 marks

**Appears:** 2021 P1(f); 2022 P5(d); 2024 P5(d).

**Suggested answer:** Forward-declare a class before another class uses it through a pointer or reference; provide the full definitions where the complete types are required. This breaks circular definition dependencies.

### 5. What must a value-based data type define in C++? — 2 marks

**Appears:** 2021 P1(g); 2022 P5(e); 2024 P5(e).

**Suggested answer:** It should provide appropriate value semantics: construction, copying and assignment (plus destruction where needed), so independent objects behave like values. Resource-owning types may require the Rule of Three/Five.

### 6. What is an object adapter? — 6 marks

**Appears:** 2021 P1(d); 2022 P5(f); 2024 P5(f).

**Suggested answer:** An object adapter uses composition to wrap an existing object and translates its interface into one the client expects, forwarding operations to the wrapped object.

### 7. What is the difference between a copy constructor and assignment operator, and how do we guarantee safe operation? — 8 marks

**Appears:** 2021 P1(h); 2022 P5(g); 2024 P5(g).

**Suggested answer:** A copy constructor initialises a *new* object; copy assignment replaces an *existing* object's contents. Use a deep copy for owned resources and handle self-assignment and exceptions safely, for example with copy-and-swap.

### 8. What is the best-case, average-case and worst-case complexity for a lookup in a binary tree? — 6 marks

**Appears:** 2021 P1(i); 2022 P5(h); 2024 P5(h).

**Suggested answer:** For a **binary search tree**, best is `O(1)` (root), average is `O(log n)` for a reasonably balanced/random BST, and worst is `O(n)` when the tree is skewed. The paper says 'binary tree', but these figures require the search-tree assumption.

### 9. What are reference data members and how do we initialise them? — 2 marks

**Appears:** 2021 P1(b); 2022 P5(i); 2024 P5(i).

**Suggested answer:** They are class members declared as references (e.g. `T&`) and must be bound in the constructor's member-initialiser list; they cannot be rebound later.

### 10. Given n−1 distinct numbers from 1 to n, how can we find the missing number in linear time? — 8 marks

**Appears:** 2021 P1(j); 2022 P5(j); 2024 P5(j).

**Suggested answer:** Calculate the expected sum `n(n+1)/2`, subtract the sum of the given numbers, and return the difference. This takes `O(n)` time and `O(1)` auxiliary space (assuming arithmetic does not overflow).

## 2023 Semester 1 final — Problem 5 (68 marks)

These are the ten short-answer questions from the 2023 paper. They differ substantially from the recurring set above.

### 11. What is a weak pointer and when do we use it? — 8 marks

**Appears:** 2023 P5(a).

**Suggested answer:** `std::weak_ptr` observes an object managed by `std::shared_ptr` without increasing its ownership count. It avoids reference cycles, for example in back-links; use `lock()` to access the object if it still exists.

### 12. How do we guarantee preconditions for operations in C++? — 2 marks

**Appears:** 2023 P5(b).

**Suggested answer:** Check programmer preconditions with `assert(condition)`; for invalid runtime input that must be handled, validate and report an error (for example by throwing an exception).

### 13. What are the canonical methods in C++? — 12 marks

**Appears:** 2023 P5(c).

**Suggested answer:** The usual special member functions are default constructor, destructor, copy constructor, copy assignment, move constructor and move assignment. For resource-owning classes, the latter five are commonly discussed as the **Rule of Five**.

### 14. Is Quick Sort strictly better than Merge Sort? Justify. — 8 marks

**Appears:** 2023 P5(d).

**Suggested answer:** No. Quick Sort is often fast and in-place on average (`O(n log n)`) but can take `O(n²)` in the worst case. Merge Sort guarantees `O(n log n)` and is stable, but generally requires `O(n)` extra space for arrays.

### 15. What is the purpose of an empty tree? Justify. — 8 marks

**Appears:** 2023 P5(e).

**Suggested answer:** An empty tree represents a missing subtree and provides the base case for recursive tree definitions and algorithms. A NIL sentinel can make child handling uniform without repeated null-pointer cases.

### 16. Which modern C++ abstraction do we use when we need to return a value that does not exist? — 2 marks

**Appears:** 2023 P5(f).

**Suggested answer:** `std::optional<T>` represents a value that may be absent; use `std::nullopt` for the no-value case.

### 17. What does amortized analysis show? — 4 marks

**Appears:** 2023 P5(g).

**Suggested answer:** It bounds the average cost **per operation over a sequence**, showing how occasional expensive actions (e.g. dynamic-array resizing) are spread across many cheap operations. It is not the same as average-case analysis over random inputs.

### 18. What is a load factor, and what are the recommended factors, thresholds and aims for expansion and contraction of dynamic memory? — 12 marks

**Appears:** 2023 P5(h).

**Suggested answer:** Load factor is `size / capacity`. A common dynamic-array policy is to grow (often double capacity) when full and shrink (often halve capacity) at about one-quarter full. These thresholds balance memory usage with amortized efficiency and avoid resizing back and forth.

**Caution:** The 2023 question does not state the exact numeric thresholds in its prompt. The values above are common implementation choices, **not a verified official marking scheme**.

### 19. What is required to test the equivalence of iterators? — 4 marks

**Appears:** 2023 P5(i).

**Suggested answer:** Check that the iterators belong to the same collection/range and have the same current position or traversal state, including an equivalent end state when applicable.

### 20. When do we need to implement a state machine? — 8 marks

**Appears:** 2023 P5(j).

**Suggested answer:** When the next action depends on a current state and events/input cause transitions between states, such as in parsing, protocols or multi-stage tree iterators.

## Coverage and limitations

| Paper | Theory section | Included here |
|---|---|---|
| 2021 S1 final | Problem 1, 50 marks | 10 questions (above) |
| 2022 S1 final | Problem 5, 50 marks | Same 10 questions, reordered |
| 2023 S1 final | Problem 5, 68 marks | 10 additional questions |
| January 2024 final | Problem 5, 50 marks | Same recurring 10 questions |
| 2026 S1 midterm | Solution Design & Iterators (two programming problems) | No separate short-answer theory section identified |
| 2025 midterm | File is on GitHub | **Not inspected for short-answer theory yet**; no claims made about its contents |

The papers and their marks vary by year. **The suggested answers are study notes, not official answers, and question repetition does not guarantee a future exam will use the same questions.**
