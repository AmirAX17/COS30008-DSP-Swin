# COS30008 — Identifying coding problem types

A quick index of the **coding problems in the past papers**, not a C++ tutorial or a set of full solutions. The idea is to recognise what a question is asking before you start writing.

**Real-exam note:** In handwritten finals, space is limited. Identify the required functions and write only what answers the specification. Don't waste the answer box rewriting provided headers, adding long comments, or explaining code unless asked. The 2026 midterm is a different, code-submission format, so this space warning mainly concerns the handwritten final papers.

## Coding problem categories

| Category | How to recognise it in the paper | What makes it different | Where it appears |
|---|---|---|---|
| **1. Ternary tree — basic infrastructure (raw pointers)** | `TTree<T>` / `TernaryTree<T>`, `fLeft/fMiddle/fRight` or `fSubTrees[3]`, `NIL`, `addSubTree`, `removeSubTree`, `empty`, `leaf`, sometimes `height` | Managing branches and the special empty-tree sentinel; no copy/move logic unless separately requested | **2021 P2; 2022 P1; Jan 2024 P1** |
| **2. Ternary tree — copy semantics** | `const TTree&`, copy constructor, `operator=(const TTree&)`, `clone()` | Must distinguish a deep copy of nodes from sharing the original pointers; empty/NIL cases matter | **2021 P3; 2022 P2; Jan 2024 P2** |
| **3. Ternary tree — move semantics** | `T&&`, `TTree&&`, move constructor, move assignment, `std::move` | Transfers ownership/branches instead of cloning; source is left in the specified valid state | **2021 P4; 2022 P3; Jan 2024 P3** |
| **4. Ternary tree — prefix iterator** | `TernaryTreePrefixIterator`, `std::stack`, `push_subtrees`, `begin/end`, iterator operators | **Preorder:** visit node, then left, middle, right; push children onto stack right-to-left | **2022 P4; Jan 2024 P4** |
| **5. Ternary tree — postfix iterator** | `TTreePostfixIterator`, `TTreeFrontier`, `stage`, `push_nodes`, `std::stack` | In these papers **postfix traversal** goes right, middle, left, then node; the frontier tracks which branch comes next. This is *not* merely `operator++(int)` | **2021 P5** |
| **6. Ternary tree — smart-pointer ownership** | `using Node = std::unique_ptr<TernaryTree>`, `makeNode`, `add(index, Node&)`, `remove(index)` | Ownership transfer through `unique_ptr`, rather than a `NIL` sentinel and manually owned raw-pointer subtrees | **2023 P2** |
| **7. Linked-list destruction / shared ownership** | `List`, `DoublyLinkedList`, `shared_ptr`, `weak_ptr`, `fHead/fTail`, destructor `~List()` | Breaking links iteratively from tail to head so large lists don't trigger recursive destruction and stack overflow | **2023 P1** |
| **8. Custom string — resource management** | `DSPString`, `char* fContents`, destructor, copy/move constructors and assignments, `size`, `operator[]`, `operator==` | Managing a dynamically allocated null-terminated character array and its value semantics | **2023 P3** |
| **9. Bidirectional string iterator** | `DSPStringIterator`, `fIndex`, `operator++`, `operator--`, `begin/end/rbegin/rend` | Index movement and four distinct boundary positions for forward and reverse iteration | **2023 P4** |
| **10. Circular-buffer key iterator** | `KeyIterator<N>`, array of offsets, circular buffer, `operator+=`, wraparound | Producing and updating the changing autokey using a fixed-size circular buffer | **2026 S1 midterm P1** |
| **11. Cipher-transforming forward iterator** | `AutoCaesarIterator`, `KeyIterator<KEY_LENGTH>`, `isalpha`, letter offsets, encoding on dereference | Iterator both traverses text and applies the autokey Caesar transformation; punctuation is not encoded | **2026 S1 midterm P2** |

## Quick differences people can mix up

### Basic tree vs copy vs move

- **Basic infrastructure:** create, access, attach, detach, destroy or measure tree nodes.
- **Copy:** make a separate tree with the same structure; look for `const ...&` and `clone()`.
- **Move:** transfer the existing resources; look for `&&` and `std::move`.
- **2023 smart-pointer tree:** primarily `unique_ptr` ownership, `add/remove`, `leaf/height`; the paper explicitly says to ignore copy and move semantics for that problem.

### Prefix vs postfix tree iterators

- **Prefix traversal (2022, 2024):** node → left → middle → right. Its stack stores nodes awaiting visits.
- **Postfix traversal (2021):** right → middle → left → node. Its stack uses `TTreeFrontier` records with a `stage`.
- **Don't confuse the name of traversal with `operator++(int)`:** postfix increment is a C++ operator form, not the same thing as postfix *tree traversal*.

### Iterator question vs data-structure question

- **Data-structure question:** you're implementing the underlying tree, list or string.
- **Iterator question:** you're implementing position, traversal, dereference, equality and boundaries.
- **Transforming iterator (2026):** dereferencing has an additional job: apply the cipher using the current autokey.

## Problem-by-problem lookup

| Paper | Coding problems in order | Separate theory |
|---|---|---|
| **2021 S1 final** | P2 tree basics → P3 tree copy → P4 tree move → P5 postfix tree iterator | P1 |
| **2022 S1 final** | P1 tree basics → P2 tree copy → P3 tree move → P4 prefix tree iterator | P5 |
| **2023 S1 final** | P1 list destructor → P2 `unique_ptr` ternary tree → P3 `DSPString` → P4 bidirectional string iterator | P5 |
| **January 2024 final** | P1 tree basics → P2 tree copy → P3 tree move → P4 prefix tree iterator | P5 |
| **2026 S1 midterm** | P1 `KeyIterator<N>` → P2 `AutoCaesarIterator` | No separate short-answer theory section |

**2025 midterm:** The PDF is in `past-papers/`, but its coding questions weren't available for review when this index was prepared. It hasn't been assigned categories here rather than guessing.

## What repeats?

- **2022 S1 and January 2024:** Almost the same four coding categories, in the same order.
- **2021 vs 2022/2024:** Tree basics, copy and move still appear, but the 2021 iterator is **postfix traversal**, not prefix.
- **2023:** Mostly different problem formats, especially smart pointers, list destruction, a custom string and its iterator.
- **2026 midterm:** Iterator-focused, but the problem is a **cipher and circular autokey**, not a ternary-tree traversal.

This is an index of **past questions**, not a prediction of future exams. Always follow the functions, data members and constraints supplied in the actual paper.
